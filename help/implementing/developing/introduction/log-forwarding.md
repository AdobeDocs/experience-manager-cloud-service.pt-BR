---
title: Encaminhamento de logs para o AEM as a Cloud Service
description: Saiba mais sobre como encaminhar logs para fornecedores de registro no AEM as a Cloud Service
exl-id: 27cdf2e7-192d-4cb2-be7f-8991a72f606d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 9c258e2906c37ee9b91d2faa78f7dfdaa5956dc2
workflow-type: tm+mt
source-wordcount: '1985'
ht-degree: 0%

---

# Encaminhamento de logs {#log-forwarding}

>[!NOTE]
>
>O encaminhamento de logs agora é configurado no modo de autoatendimento, diferente do método herdado, que exigiu o envio de um tíquete de Suporte Adobe. Consulte a seção [Migrando](#legacy-migration) se o encaminhamento de log foi configurado pelo Adobe.

Os clientes com uma licença de um fornecedor de registro em log ou que hospedam um produto de registro em log podem ter registros AEM (incluindo Apache/Dispatcher) e registros CDN encaminhados ao destino de registro em log associado. O AEM as a Cloud Service oferece suporte aos seguintes destinos de registro:

* Armazenamento Azure Blob
* Datadog
* Elasticsearch ou OpenSearch
* HTTPS
* Splunk

O encaminhamento de logs é configurado de maneira automatizada declarando uma configuração no Git e pode ser implantado por meio de pipelines de configuração do Cloud Manager para tipos de ambiente de desenvolvimento, preparo e produção. O arquivo de configuração pode ser implantado em RDEs (Rapid Development Environments, ambientes de desenvolvimento rápido) usando ferramentas de linha de comando.

Há uma opção para que os registros AEM e Apache/Dispatcher sejam roteados por meio da infraestrutura de rede avançada do AEM, como IP de saída dedicado.

Observe que a largura de banda da rede associada aos registros enviados ao destino de registro é considerada parte do uso de E/S da rede da organização.

## Como este artigo está organizado {#how-organized}

Este artigo está organizado da seguinte maneira:

* Configuração - comum para todos os destinos de registro
* Transporte e rede avançada - considere a configuração da rede antes de criar a configuração de registro
* Configurações de destino de registro - cada destino tem um formato um pouco diferente
* Formatos de Entrada de Log - informações sobre os formatos de entrada de log
* Migração do encaminhamento de log herdado - como migrar do encaminhamento de log previamente configurado pelo Adobe para a abordagem de autoatendimento

## Configurar {#setup}

1. Crie um arquivo chamado `logForwarding.yaml`. Ele deve conter metadados, conforme descrito no [artigo sobre o pipeline de configuração](/help/operations/config-pipeline.md#common-syntax) (**kind** deve ser definido como `LogForwarding` e a versão definida como &quot;1&quot;), com uma configuração semelhante à seguinte (usamos o Splunk como exemplo).

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

1. Coloque o arquivo em algum lugar em uma pasta de nível superior chamada *config* ou similar, conforme descrito em [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#folder-structure).

1. Para tipos de ambiente diferentes de RDE (que usa ferramentas de linha de comando), crie um pipeline de configuração de implantação direcionada no Cloud Manager, conforme referenciado por [esta seção](/help/operations/config-pipeline.md#creating-and-managing); observe que os pipelines de Empilhamento completo e de Camada da Web não implantam o arquivo de configuração.

1. Implante a configuração.

Os tokens na configuração (como `${{SPLUNK_TOKEN}}`) representam segredos que não devem ser armazenados no Git. Em vez disso, declare-as como [Variáveis de ambiente secreto](/help/operations/config-pipeline.md#secret-env-vars) do Cloud Manager. Selecione **Todos** como o valor suspenso do campo Serviço aplicado, para que os logs possam ser encaminhados para os níveis de criação, publicação e visualização.

É possível definir valores diferentes entre logs CDN e logs AEM (incluindo Apache/Dispatcher), incluindo um bloco **cdn** e/ou **aem** adicional após o bloco **padrão**, em que as propriedades podem substituir as definidas no bloco **padrão**; somente a propriedade habilitada é necessária. Um possível caso de uso poderia ser o uso de um índice do Splunk diferente para logs CDN, como ilustra o exemplo abaixo.

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
       cdn:
         enabled: true
         token: "${{SPLUNK_TOKEN_CDN}}"
         index: "AEMaaCS_CDN"   
```

Outro cenário é desabilitar o encaminhamento dos logs CDN ou dos logs AEM (incluindo o Apache/Dispatcher). Por exemplo, para encaminhar apenas os logs CDN, é possível configurar o seguinte:

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
       aem:
         enabled: false
```

## Transporte e rede avançada {#transport-advancednetworking}

Algumas organizações escolhem restringir qual tráfego pode ser recebido pelos destinos de registro, outras podem exigir o uso de portas diferentes de HTTPS (443).  Nesse caso, a [Rede Avançada](/help/security/configuring-advanced-networking.md) precisará ser configurada antes da implantação da configuração de encaminhamento de log.

Use a tabela abaixo para ver quais são os requisitos para a configuração avançada de rede e registro com base no fato de você estar usando ou não a porta 443 e se você precisa ou não que seus registros apareçam a partir de um endereço IP fixo.
<html>
<style>
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
  text-align: center;
}
</style>
<table>
  <tbody>
    <tr>
      <th>Porta de destino</th>
      <th>Requisito para que os registros apareçam do IP fixo?</th>
      <th>Redes avançadas necessárias</th>
      <th>Definição de Porta LogForwarding.yaml Necessária</th>
    </tr>
    <tr>
      <td rowspan="2">HTTPS (443)</td>
      <td>Não</td>
      <td>Não</td>
      <td>Não</td>
    </tr>
    <tr>
      <td>Sim</td>
      <td>Sim, <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">Saída Dedicada</a></td>
      <td>Não</td>
    <tr>
    <tr>
      <td rowspan="2">Porta não padrão (por exemplo, 8088)</td>
      <td>Não</td>
      <td>Sim, <a href="/help/security/configuring-advanced-networking.md#flexible-port-egress-flexible-port-egress">Saída flexível</a></td>
      <td>Sim</td>
    </tr>
    <tr>
      <td>Sim</td>
      <td>Sim, <a href="/help/security/configuring-advanced-networking.md#dedicated-egress-ip-address-dedicated-egress-ip-address">Saída Dedicada</a></td>
      <td>Sim</td>
  </tbody>
</table>
</html>

>[!NOTE]
>O fato de seus registros serem exibidos a partir de um único endereço IP é determinado pela sua escolha de configuração avançada de rede.  A saída dedicada deve ser usada para facilitar isso.
>
> A configuração avançada de rede é um [processo de duas etapas](/help/security/configuring-advanced-networking.md#configuring-and-enabling-advanced-networking-configuring-enabling) que requer ativação no nível do programa e do ambiente.

Para logs AEM (incluindo Apache/Dispatcher), se você tiver configurado a [Rede Avançada](/help/security/configuring-advanced-networking.md), poderá usar a propriedade `aem.advancedNetworking` para encaminhá-los de um endereço IP de Saída Dedicado ou através de uma VPN.

O exemplo abaixo mostra como configurar o registro em uma porta HTTPS padrão com rede avançada.

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
      port: 443
      token: "${{SPLUNK_TOKEN}}"
      index: "aemaacs"
    aem:
      advancedNetworking: true
```

Para logs CDN, você pode adicionar os endereços IP à lista de permissões, conforme descrito em [Documentação do Fastly - Lista de IP Públicos](https://www.fastly.com/documentation/reference/api/utils/public-ip-list/). Se essa lista de endereços IP compartilhados for muito grande, considere enviar tráfego para um servidor https ou (não Adobe) Azure Blob Store, onde a lógica pode ser gravada para enviar os logons de um IP conhecido para seu destino final.

>[!NOTE]
>Não é possível que os registros CDN apareçam a partir do mesmo endereço IP que os registros AEM aparecem. Isso ocorre porque os registros são enviados diretamente do Fastly e não do AEM Cloud Service.

## Configuração de destino de registro {#logging-destinations}

As configurações para os destinos de registro compatíveis estão listadas abaixo, juntamente com considerações específicas.

### Armazenamento Azure Blob {#azureblob}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  azureBlob:
    default:
      enabled: true       
      storageAccountName: "example_acc"
      container: "aem_logs"
      sasToken: "${{AZURE_BLOB_SAS_TOKEN}}
      
```

Um token SAS deve ser usado para autenticação. Ela deve ser criada na página Shared access signature, em vez de na página Shared access token, e deve ser configurada com estas configurações:

* Serviços permitidos: o blob deve ser selecionado.
* Recursos permitidos: o objeto deve ser selecionado.
* Permissões permitidas: Gravar, Adicionar, Criar devem ser selecionadas.
* Uma data/hora de início e expiração válidas.

Esta é uma captura de tela de um exemplo de configuração de token SAS:

![Configuração de token SAS do Azure Blob](/help/implementing/developing/introduction/assets/azureblob-sas-token-config.png)

Se os registros pararem de ser entregues depois de antes funcionarem corretamente, verifique se o token SAS configurado ainda é válido, pois pode ter expirado.

#### Logs CDN do Armazenamento de Blobs do Azure {#azureblob-cdn}

Cada um dos servidores de log distribuídos globalmente produzirá um novo arquivo a cada poucos segundos, na pasta `aemcdn`. Depois de criado, o arquivo não será mais anexado ao. O formato do nome do arquivo é AAAA-MM-DDThh:mm:ss.sss-uniqueid.log. Por exemplo, 2024-03-04T10:00:00.000-WnFWYN9BpOUs2aOVn4ee.log.

Como exemplo, em algum momento:

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
```

E 30 segundos depois:

```text
aemcdn/
   2024-03-04T10:00:00.000-abc.log
   2024-03-04T10:00:00.000-def.log
   2024-03-04T10:00:30.000-ghi.log
   2024-03-04T10:00:30.000-jkl.log
   2024-03-04T10:00:30.000-mno.log
```

Cada arquivo contém várias entradas de log json, cada uma em uma linha separada. Os formatos de entrada de log estão descritos em [Logs para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md), e cada entrada de log também inclui as propriedades adicionais mencionadas na seção [Formatos de Entrada de Log](#log-formats) abaixo.

#### Logs AEM do Armazenamento Azure Blob {#azureblob-aem}

Os logs de AEM (incluindo o Apache/Dispatcher) aparecem abaixo de uma pasta com a seguinte convenção de nomenclatura:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

Em cada pasta, um único arquivo será criado e anexado a. Os clientes são responsáveis pelo processamento e gerenciamento desse arquivo, de modo que ele não fique muito grande.

Consulte os formatos de entrada de log em [Log para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). As entradas de log também incluirão as propriedades adicionais mencionadas na seção [Formatos de Entrada de Log](#log-formats) abaixo.

### Datadog {#datadog}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  datadog:
    default:
      enabled: true       
      host: "http-intake.logs.datadoghq.eu"
      token: "${{DATADOG_API_KEY}}"
      tags:
         tag1: value1
         tag2: value2
      
```

Considerações:

* Crie uma Chave de API sem nenhuma integração com um provedor de nuvem específico.
* A propriedade das tags é opcional
* Para logs AEM, a marca de origem do Datadog está definida como `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` ou `aemhttpderror`
* Para logs CDN, a marca de origem do Datadog está definida como `aemcdn`
* A etiqueta de serviço do Datadog está definida como `adobeaemcloud`, mas você pode substituí-la na seção de etiquetas
* Se o pipeline de assimilação usar tags Datadog para determinar o índice apropriado para logs de encaminhamento, verifique se essas tags estão configuradas corretamente no arquivo YAML de encaminhamento de logs. As tags ausentes podem impedir a assimilação de logs bem-sucedida se o pipeline depender delas.

### Elasticsearch e OpenSearch {#elastic}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  elasticsearch:
    default:
      enabled: true
      host: "example.com"
      user: "${{ELASTICSEARCH_USER}}"
      password: "${{ELASTICSEARCH_PASSWORD}}"
      pipeline: "ingest pipeline name"
```

Considerações:

* por padrão, a porta é 443. Opcionalmente, ele pode ser substituído por uma propriedade chamada `port`
* Para credenciais, certifique-se de usar as credenciais de implantação, em vez das credenciais de conta. Estas são as credenciais geradas em uma tela que pode se parecer com esta imagem:

![Credenciais de implantação elástica](/help/implementing/developing/introduction/assets/ec-creds.png)

* Para logs AEM, `index` está definido como `aemaccess`, `aemerror`, `aemrequest`, `aemdispatcher`, `aemhttpdaccess` ou `aemhttpderror`
* A propriedade opcional do pipeline deve ser definida como o nome do pipeline de assimilação de Elasticsearch ou OpenSearch, que pode ser configurado para rotear a entrada de log para o índice apropriado. O tipo de Processador do pipeline deve ser definido como *script* e a linguagem de script deve ser definida como *indolor*. Este é um exemplo de trecho de script para rotear entradas de log em um índice, como aemaccess_dev_26_06_2024:

```text
def envType = ctx.aem_env_type != null ? ctx.aem_env_type : 'unknown';
def sourceType = ctx._index;
def date = new SimpleDateFormat('dd_MM_yyyy').format(new Date());
ctx._index = sourceType + "_" + envType + "_" + date;
```

### HTTPS {#https}

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  https:
    default:
      enabled: true
      url: "https://example.com/aem_logs/aem"
      authHeaderName: "X-AEMaaCS-Log-Forwarding-Token"
      authHeaderValue: "${{HTTPS_LOG_FORWARDING_TOKEN}}"
```

Considerações:

* A cadeia de caracteres da URL deve incluir **https://** ou a validação falhará.
* O URL pode incluir uma porta. Por exemplo, `https://example.com:8443/aem_logs/aem`. Se nenhuma porta for incluída na string do URL, a porta 443 (a porta HTTPS padrão) será considerada.

#### Logs HTTPS CDN {#https-cdn}

As solicitações da Web (POSTs) serão enviadas continuamente, com uma carga json que é uma matriz de entradas de log, com o formato de entrada de log descrito em [Logon para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md#cdn-log). Propriedades adicionais são mencionadas na seção [Formatos de Entrada de Log](#log-formats) abaixo.

Também existe uma propriedade chamada `sourcetype`, que é definida como o valor `aemcdn`.

>[!NOTE]
>
> Antes de enviar a primeira entrada de log CDN, o servidor HTTP deve concluir com êxito um desafio único: uma solicitação enviada para o caminho ``/.well-known/fastly/logging/challenge`` deve responder com um asterisco ``*`` no corpo e código de status 200.

#### Logs AEM HTTPS {#https-aem}

Para logs AEM (incluindo apache/dispatcher), as solicitações da Web (POSTs) serão enviadas continuamente, com uma carga json que é uma matriz de entradas de log, com os vários formatos de entrada de log, conforme descrito em [Logs para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md). Propriedades adicionais são mencionadas na seção [Formatos de Entrada de Log](#log-formats) abaixo.

Também há uma propriedade chamada `Source-Type`, que é definida como um destes valores:

* aemaccess
* aemerror
* aemrequest
* aemdispatcher
* aemhttpdaccess
* aemhttpderror

### Splunk {#splunk}

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
      index: "aemaacs"
```

Considerações:

* A porta padrão é 443. Opcionalmente, ele pode ser substituído por uma propriedade chamada `port`.
* Dependendo do log específico, o campo sourcetype terá um dos seguintes valores: *aemaccess*, *aemerror*,
  *aemrequest*, *aemdispatcher*, *aemhttpdaccess*, *aemhttpderror*, *aemcdn*
* Incluir na lista de permissões Se os IPs necessários tiverem sido migrados e os registros ainda não estiverem sendo entregues, verifique se não há regras de firewall impondo a validação do token de Splunk. O Fastly executa uma etapa de validação inicial na qual um token do Splunk inválido é enviado intencionalmente. Se o firewall estiver definido para encerrar conexões com tokens inválidos do Splunk, o processo de validação falhará, impedindo que o Fastly entregue logs para a instância do Splunk.

>[!NOTE]
>
> [Ao migrar](#legacy-migration) do encaminhamento de logs herdado para este modelo de autoatendimento, os valores do campo `sourcetype` enviados para o índice do Splunk podem ter sido alterados, portanto, ajuste-os adequadamente.

<!--
### Sumo Logic {#sumologic}

   ```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     splunk:
       default:
         enabled: true
         host: "https://collectors.de.sumologic.com"
         uri: "/receiver/v1/http"
         privateKey: "${{SomeOtherToken}}"
   
   ```   
-->

## Formatos de entrada de log {#log-formats}

Consulte [Logs para AEM as a Cloud Service](/help/implementing/developing/introduction/logging.md) para o formato de cada respectivo tipo de log (logs CDN e logs AEM, incluindo Apache/Dispatcher).

Como os registros de vários programas e ambientes podem ser encaminhados para o mesmo destino de registro, além da saída descrita no artigo de registro, as seguintes propriedades serão incluídas em cada entrada de registro:

* aem_env_id
* aem_env_type
* aem_program_id
* aem_tier

Como exemplo, as propriedades podem ter os seguintes valores:

```text
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
```

## Migrando do Encaminhamento de Log Herdado {#legacy-migration}

Antes de a configuração do encaminhamento de logs ser obtida por meio de um modelo de autoatendimento, os clientes eram solicitados a abrir tíquetes de suporte, em que o Adobe iniciaria a integração.

Os clientes que foram configurados dessa maneira pelo Adobe são bem-vindos para se adaptarem ao modelo de autoatendimento de sua conveniência. Há vários motivos para fazer essa transição:

* Um novo ambiente (por exemplo, um novo ambiente de desenvolvimento ou RDE) foi provisionado.
* Alterações nas credenciais ou no ponto de extremidade existente do Splunk.
* O Adobe configurou o encaminhamento de log antes que os logs CDN estivessem disponíveis e você gostaria de receber logs CDN.
* Uma decisão consciente de se adaptar proativamente ao modelo de autoatendimento para que sua organização tenha o conhecimento mesmo antes de uma alteração sensível ao tempo ser necessária.

Quando estiver pronto para migrar, basta configurar o arquivo YAML conforme descrito nas seções anteriores. Use o pipeline de configuração do Cloud Manager para implantar em cada um dos ambientes em que a configuração deve ser aplicada.

Recomenda-se, mas não é necessário, que uma configuração seja implantada em todos os ambientes para que todos estejam sob controle de autoatendimento. Caso contrário, você pode esquecer quais ambientes foram configurados pelo Adobe e os configurados de forma automatizada.

>[!NOTE]
>Os valores do campo `sourcetype` enviados para o índice do Splunk podem ter sido alterados, portanto, ajuste de acordo.
>
>Quando o encaminhamento de registros é implantado em um ambiente previamente configurado pelo suporte para Adobe, você pode receber registros duplicados por até algumas horas. Isso acabará sendo resolvido automaticamente.
