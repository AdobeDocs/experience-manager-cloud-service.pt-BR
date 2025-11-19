---
title: Usar Pipelines De Configuração
description: Saiba como você pode usar pipelines de configuração para implantar diferentes configurações no AEM as a Cloud Service, como configurações de encaminhamento de logs, tarefas de manutenção relacionadas à limpeza e várias configurações de CDN.
feature: Operations
role: Admin
exl-id: bd121d31-811f-400b-b3b8-04cdee5fe8fa
source-git-commit: 5e0626c57f233ac3814355d7efe7db010897d72b
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 2%

---

# Usar pipelines de configuração {#config-pipelines}

Saiba como você pode usar pipelines de configuração para implantar diferentes configurações no AEM as a Cloud Service, como configurações de encaminhamento de logs, tarefas de manutenção relacionadas à limpeza e várias configurações de CDN.

## Visão geral {#overview}

Um pipeline de configuração do Cloud Manager implanta arquivos de configuração (criados no formato YAML) em um ambiente de destino. Vários recursos do AEM as a Cloud Service podem ser configurados dessa maneira, incluindo o encaminhamento de logs, tarefas de manutenção relacionadas à limpeza e vários recursos de CDN.

Para projetos do **Entrega de publicação**, os pipelines de configuração podem ser implantados via Cloud Manager para tipos de ambiente de desenvolvimento, preparo e produção. Os arquivos de configuração podem ser implantados em ambientes de desenvolvimento rápido (RDEs) usando a [ferramenta de linha de comando](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline).

Os pipelines de configuração também podem ser implantados por meio do Cloud Manager para Projetos do **Edge Delivery**.

As seções a seguir deste documento fornecem uma visão geral de informações importantes sobre como os pipelines de configuração podem ser usados e como as configurações para eles devem ser estruturadas. Ele descreve conceitos gerais compartilhados entre todos ou um subconjunto dos recursos compatíveis com os pipelines de configuração.

* [Configurações com Suporte](#configurations) - Uma lista de configurações que podem ser implantadas com pipelines de configuração.
* [Criar e gerenciar pipelines de configuração](#creating-and-managing) - Como criar um pipeline de configuração
* [Sintaxe comum](#common-syntax) - Sintaxe compartilhada entre configurações.
* [Estrutura de pasta](#folder-structure) - Descreve a configuração de estrutura que os pipelines esperam para as configurações.
* [Variáveis de ambiente secretas](#secret-env-vars) - Exemplos de uso de variáveis de ambiente para não revelar segredos em suas configurações.
* [Variáveis de pipeline secretas](#secret-pipeline-vars) - Exemplos de uso de variáveis de ambiente para não divulgar segredos em suas configurações para projetos Edge Delivery Services.

## Configurações compatíveis {#configurations}

A tabela a seguir oferece uma lista abrangente dessas configurações com links para a documentação dedicada descrevendo sua sintaxe de configuração distinta e outras informações.

| Tipo | Valor `kind` YAML | Descrição | Publicar entrega | Edge Delivery |
|---|---|---|---|---|
| [Regras de Filtro de Tráfego, incluindo o WAF](/help/security/traffic-filter-rules-including-waf.md) | `CDN` | Declarar regras para bloquear tráfego mal-intencionado | X | X |
| [Solicitar transformações](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) | `CDN` | Declarar regras para transformar a forma da solicitação de tráfego | X | X |
| [Transformações de Resposta](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) | `CDN` | Declarar regras para transformar a forma da resposta para uma determinada solicitação | X | X |
| [Redirecionamentos do lado do servidor](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) | `CDN` | Declarar redirecionamentos do lado do servidor no estilo 301/302 | X | X |
| [Seletores de Origem](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) | `CDN` | Declarar regras para rotear o tráfego para diferentes backends, incluindo aplicativos que não sejam da Adobe | X | X |
| [Páginas de erro da CDN](/help/implementing/dispatcher/cdn-error-pages.md) | `CDN` | Substitua a página de erro padrão se a origem do AEM não puder ser acessada, fazendo referência ao local do conteúdo estático auto-hospedado no arquivo de configuração | X |  |
| [Limpeza da CDN](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) | `CDN` | Declarar as chaves de API de limpeza usadas para limpar a CDN | X |  |
| [Token HTTP CDN gerenciado pelo cliente](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value) | `CDN` | Declarar o valor da X-AEM-Edge-Key necessário para chamar a CDN da Adobe a partir de um CDN do cliente | X |  |
| [Autenticação básica](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#basic-auth) | `CDN` | Declarar os nomes de usuário e senhas para uma caixa de diálogo de autenticação básica que protege determinados URLs. | X | X |
| [Tarefa de manutenção de limpeza de versão](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Otimizar o repositório do AEM declarando regras sobre quando as versões de conteúdo devem ser removidas | X |  |
| [Tarefa de manutenção de limpeza de log de auditoria](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Otimizar o log de auditoria do AEM para aumentar o desempenho, declarando regras sobre quando os logs devem ser removidos | X |  |
| [Encaminhamento de logs](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | Configure os endpoints e as credenciais para encaminhar logs para vários destinos, incluindo Azure Blob Storage, Datadog, HTTPS, Elasticsearch, Splunk | X | X |
| [Registrando uma ID de Cliente](/help/implementing/developing/open-api-based-apis.md) | `API` | Escopo de projetos da API do Adobe Developer Console para um ambiente específico do AEM registrando a ID do cliente. Necessário para o uso de APIs baseadas em OpenAPI que exigem autenticação | X |  |

## Criar e gerenciar pipelines de configuração {#creating-and-managing}

Para obter informações sobre como criar e configurar os pipelines de configuração do **Entrega de publicação**, consulte [Pipelines de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). Ao criar um pipeline de configuração no Cloud Manager, selecione uma **Implantação direcionada** em vez de **Código de pilha completa** ao configurar o pipeline. Como observado anteriormente, a configuração de RDEs é implantada usando a [ferramenta de linha de comando](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline), em vez de um pipeline.

Para obter informações sobre como criar e configurar pipelines de configuração do **Edge Delivery**, consulte o artigo [Adicionar um pipeline de Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).

## Sintaxe comum {#common-syntax}

Cada arquivo de configuração começa com propriedades que se assemelham ao seguinte trecho de exemplo:

```yaml
   kind: "CDN"
   version: "1"
   metadata: ...
   data: ...
```

| Propriedade | Descrição | Padrão |
|---|---|---|
| `kind` | Uma string que determina o tipo de configuração, como encaminhamento de logs, regras de filtro de tráfego ou transformações de solicitações | Obrigatório, sem padrão |
| `version` | Uma string que representa a versão do esquema | Obrigatório, sem padrão |
| `metadata` | (Opcional) Contém uma matriz de cadeias de caracteres `envTypes` que determina para quais tipos de ambiente a configuração é processada. Para **Publicar Entrega**, os valores possíveis são `dev`, `stage` e `prod`. Para **Edge Delivery**, somente um valor de `prod` deve ser usado. Por exemplo, se a matriz incluir apenas `dev`, a configuração não será carregada em ambientes de preparo ou produção, mesmo se a configuração for implantada lá. | Todos os tipos de ambiente, que é (dev, stage, prod) para Entrega de publicação ou apenas prod para Edge Delivery. |

Você pode usar o utilitário `yq` para validar localmente a formatação YAML do seu arquivo de configuração (por exemplo, `yq cdn.yaml`).

## Publicar entrega {#yamls-for-aem}

As configurações de **Entrega de Publicação** serão implantadas em um ambiente de destino. Ao direcionar vários ambientes, é possível organizar os diferentes arquivos de maneiras diferentes. Por exemplo, se a matriz incluir apenas `dev`, a configuração não será carregada em ambientes de preparo ou produção, mesmo se a configuração for implantada lá.

```yaml
   kind: "CDN"
   version: "1"
   metadata:
    envType: ["dev"]
```

### Estrutura de pastas {#folder-structure}

Uma pasta chamada `/config` ou semelhante deve estar na parte superior da árvore, com mais um arquivo YAML em algum lugar em uma árvore abaixo dela.

Por exemplo:

```text
/config
  cdn.yaml
```

Ou

```text
/config
  /dev
    cdn.yaml
```

Os nomes de pasta e arquivos abaixo de `/config` são arbitrários. Entretanto, o arquivo YAML deve incluir um valor de propriedade [`kind` válido](#configurations).

Normalmente, as configurações são implantadas em todos os ambientes. Se todos os valores de propriedade forem idênticos para cada ambiente, um único arquivo YAML será suficiente. No entanto, é comum que os valores de propriedade sejam diferentes entre os ambientes, por exemplo, ao testar um ambiente mais baixo.

As seções a seguir ilustram algumas estratégias para estruturar seus arquivos.

### Um único arquivo de configuração para todos os ambientes {#single-file}

A estrutura do arquivo é semelhante ao seguinte:

```text
/config
  cdn.yaml
  logForwarding.yaml
```

Use essa estrutura quando a mesma configuração for suficiente para todos os ambientes e para todos os tipos de configuração (CDN, encaminhamento de logs etc.). Neste cenário, a propriedade de matriz `envTypes` incluiria todos os tipos de ambiente.

```yaml
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev", "stage", "prod"]
```

Usando variáveis de ambiente (ou pipeline) do tipo secreto, é possível que as [propriedades secretas](#secret-env-vars) variem em cada ambiente, conforme ilustrado pela seguinte referência `${{SPLUNK_TOKEN}}`.

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

### Um arquivo separado por tipo de ambiente {#file-per-env}

A estrutura do arquivo é semelhante ao seguinte:

```text
/config
  cdn-dev.yaml
  cdn-stage.yaml
  cdn-prod.yaml
  logForwarding-dev.yaml
  logForwarding-stage.yaml
  logForwarding-prod.yaml
```

Use esta estrutura quando houver diferenças nos valores de propriedade. Nos arquivos, é de se esperar que o valor da matriz `envTypes` corresponda ao sufixo. Por exemplo, `cdn-dev.yaml` e `logForwarding-dev.yaml` com um valor de `["dev"]`, `cdn-stage.yaml` e `logForwarding-stage.yaml` com um valor de `["stage"]`, e assim por diante.

### Uma pasta por ambiente {#folder-per-env}

Nesta estratégia, há uma pasta `config` separada por ambiente, com um pipeline separado declarado no Cloud Manager para cada uma.

Essa abordagem é particularmente útil se você tiver vários ambientes de desenvolvimento, em que cada um tem valores de propriedade exclusivos.

A estrutura do arquivo é semelhante ao seguinte:

```text
/config/dev1
  cdn.yaml
  logForwarding.yaml
/config/dev2
  cdn.yaml
  logForwarding.yaml
/config/prod  
  cdn.yaml
  logForwarding.yaml
```

Uma variação dessa abordagem é manter uma ramificação separada por ambiente.

## Edge Delivery Services {#yamls-for-eds}

Os pipelines de configuração do Edge Delivery não têm ambientes de desenvolvimento, preparo e produção separados. Em ambientes de Entrega de publicação, as alterações avançam pelos níveis de desenvolvimento, preparo e produção. Por outro lado, um pipeline de configuração do Edge Delivery aplica a configuração diretamente a todos os mapeamentos de domínio registrados no Cloud Manager para um site do Edge Delivery.


Assim, implante uma estrutura de arquivo simples como:

```text
/config
  cdn.yaml
  logForwarding.yaml
```

Se uma regra precisar diferir de acordo com o site do Edge Delivery, use a sintaxe *when* para distinguir as regras umas das outras. Por exemplo, observe que o domínio corresponde a dev.example.com no trecho abaixo, que pode ser diferenciado do domínio `www.example.com`.

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
    # Block simple path
    - name: block-path
      when:
        allOf:
          - reqProperty: domain
            equals: "dev.example.com"
          - reqProperty: path
            equals: '/block/me'
      action: block
```

Ao incluir o campo de metadados *envTypes*, somente o valor **prod** deve ser usado (a omissão do campo de metadados envTypes também é boa). Para a *tier* reqProperty, somente o valor **publish** deve ser usado.

## Variáveis de ambiente secreto {#secret-env-vars}

Para que informações confidenciais não precisem ser armazenadas no controle do código-fonte, os arquivos de configuração dão suporte a variáveis de ambiente do Cloud Manager do tipo **secret**. Para algumas configurações, incluindo o encaminhamento de logs, as variáveis de ambiente secretas são obrigatórias para determinadas propriedades.

Observe que as variáveis de ambiente secretas são usadas para publicar projetos de entrega; consulte a seção Variáveis de pipeline secretas para projetos Edge Delivery Services.

O trecho a seguir é um exemplo de como a variável de ambiente secreta `${{SPLUNK_TOKEN}}` é usada na configuração.

```
kind: "LogForwarding"
version: "1"
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

Para obter detalhes sobre como usar variáveis de ambiente, consulte [Variáveis de ambiente do Cloud Manager](/help/implementing/cloud-manager/environment-variables.md).

## Variáveis de pipeline secretas {#secret-pipeline-vars}

Para Projetos Edge Delivery Services, use variáveis de pipeline do Cloud Manager do tipo **segredo** para que informações confidenciais não precisem ser armazenadas no controle do código-fonte. A caixa de seleção *Etapa Aplicada* deve usar a opção **implantar**.

A sintaxe é idêntica ao trecho mostrado na seção anterior.

Para obter detalhes sobre como usar variáveis de pipeline, consulte [Variáveis de pipeline no Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).
