---
title: Configurando Credenciais e Autenticação da CDN
description: Saiba como configurar credenciais e autenticação de CDN declarando regras em um arquivo de configuração que é implantado usando o pipeline de configuração do Cloud Manager.
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---


# Configurando Credenciais e Autenticação da CDN {#cdn-credentials-authentication}

A CDN fornecida por Adobe tem vários recursos e serviços, alguns dos quais dependem de credenciais e autenticação para garantir um nível apropriado de segurança corporativa. Ao declarar regras em um arquivo de configuração implantado com o uso do [pipeline de configuração](/help/operations/config-pipeline.md) do Cloud Manager, os clientes podem configurar, por autoatendimento, o seguinte:

* O valor do cabeçalho HTTP X-AEM-Edge-Key usado pelo CDN Adobe para validar solicitações provenientes de um CDN gerenciado pelo Cliente.
* O token de API usado para limpar recursos no cache do CDN.
* Uma lista de combinações de nome de usuário/senha que podem acessar conteúdo restrito, enviando um formulário de Autenticação básica.

Cada uma dessas opções, incluindo a sintaxe de configuração, é descrita em sua própria seção abaixo.

Há uma seção sobre como [girar chaves](#rotating-secrets), o que é uma boa prática de segurança.

## Valor do cabeçalho HTTP da CDN gerenciada pelo cliente {#CDN-HTTP-value}

Conforme descrito na página [CDN no AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN), os clientes podem optar por rotear o tráfego por meio de sua própria CDN, que é chamada de CDN do cliente (também chamada às vezes de BYOCDN).

Como parte da configuração, o CDN do Adobe e o CDN do cliente devem concordar com um valor do Cabeçalho HTTP `X-AEM-Edge-Key`. Esse valor é definido em cada solicitação no CDN do cliente, antes de ser roteado para o CDN do Adobe, que então valida se o valor está conforme o esperado, para que possa confiar em outros cabeçalhos HTTP, incluindo aqueles que ajudam a rotear a solicitação para a origem AEM apropriada.

O valor *X-AEM-Edge-Key* é referenciado pelas propriedades `edgeKey1` e `edgeKey2` em um arquivo chamado `cdn.yaml` ou similar, em algum lugar sob uma pasta `config` de nível superior. Leia [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#folder-structure) para obter detalhes sobre a estrutura de pastas e como implantar a configuração.  A sintaxe é descrita no exemplo abaixo.

Para obter mais informações sobre depuração e erros comuns, verifique [Erros Comuns](/help/implementing/dispatcher/cdn.md#common-errors).

>[!WARNING]
>O acesso direto sem uma X-AEM-Edge-Key correta será negado para todas as solicitações que correspondam à condição (na amostra abaixo, isso significa todas as solicitações para o nível de publicação). Se você precisar introduzir a autenticação gradualmente, consulte a seção [Migração segura para reduzir o risco de tráfego bloqueado](#migrating-safely).

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
    authenticators:
      - name: edge-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_052824}}
        edgeKey2: ${{CDN_EDGEKEY_041425}}
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

Consulte [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#common-syntax) para obter uma descrição das propriedades acima do nó `data`. O valor da propriedade `kind` deve ser *CDN* e a propriedade `version` deve ser definida como `1`.

Consulte a etapa do tutorial [Configurar e implantar regra CDN de validação de cabeçalho HTTP](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/content-delivery/custom-domain-names-with-customer-managed-cdn#configure-and-deploy-http-header-validation-cdn-rule) para obter mais detalhes.

As propriedades adicionais incluem:

* Nó `Data` que contém um nó `authentication` filho.
* Em `authentication`, um nó `authenticators` e um nó `rules`, ambos com matrizes.
* Autenticadores: permite declarar um tipo de token ou credencial, que, nesse caso, é uma chave de borda. Inclui as seguintes propriedades:
   * name - uma cadeia de caracteres descritiva.
   * tipo - deve ser `edge`.
   * edgeKey1 - o valor de *X-AEM-Edge-Key*, que deve fazer referência a uma [variável de ambiente do tipo secreto do Cloud Manager](/help/operations/config-pipeline.md#secret-env-vars). Para o campo Serviço Aplicado, selecione Todos. É recomendável que o valor (por exemplo, `${{CDN_EDGEKEY_052824}}`) reflita o dia em que foi adicionado.
   * edgeKey2 - usado para a rotação de segredos, que é descrita na [seção de rotação de segredos](#rotating-secrets) abaixo. Defina-a de forma semelhante a edgeKey1. Pelo menos um de `edgeKey1` e `edgeKey2` deve ser declarado.
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* Regras: permite declarar quais dos autenticadores devem ser usados e se são para o nível de publicação e/ou pré-visualização.  Inclui:
   * name - uma cadeia de caracteres descritiva.
   * when - uma condição que determina quando a regra deve ser avaliada, de acordo com a sintaxe no artigo [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md). Normalmente, ela incluirá uma comparação da camada atual (por exemplo, publicar) para que todo o tráfego ativo seja validado como roteamento pela CDN do cliente.
   * ação - deve especificar &quot;autenticar&quot;, com o autenticador desejado referenciado.

>[!NOTE]
>A Chave do Edge deve ser configurada como uma [variável de ambiente do Cloud Manager do tipo secreto](/help/operations/config-pipeline.md#secret-env-vars), antes da implantação da configuração que faz referência a ela. É recomendável usar uma chave aleatória exclusiva com comprimento mínimo de 32 bytes; por exemplo, a biblioteca criptográfica Open SSL pode gerar uma chave aleatória executando o comando `openssl rand -hex 32`.

### Migração segura para reduzir o risco de tráfego bloqueado {#migrating-safely}

Se o site já estiver ativo, tenha cuidado ao migrar para o CDN gerenciado pelo cliente, pois uma configuração incorreta pode bloquear o tráfego público; isso ocorre porque somente as solicitações com o valor esperado do cabeçalho X-AEM-Edge-Key serão aceitas pelo CDN Adobe. Uma abordagem é recomendada quando uma condição adicional é temporariamente incluída na regra de autenticação, o que faz com que ela bloqueie a solicitação somente se um cabeçalho de teste for incluído ou se um caminho for correspondido:

```
    - name: edge-auth-rule
        when:
          allOf:  
            - { reqProperty: tier, equals: "publish" }
            - { reqHeader: x-edge-test, equals: "test" }
        action:
          type: authenticate
          authenticator: edge-auth
```

```
    - name: edge-auth-rule
        when:
          allOf:
            - { reqProperty: tier, equals: "publish" }
            - { reqProperty: path, like: "/test*" }
        action:
          type: authenticate
          authenticator: edge-auth
```

O seguinte padrão de solicitação `curl` pode ser usado:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <CONFIGURED_EDGE_KEY>" -H "x-edge-test: test"
```

Após um teste bem-sucedido, a condição adicional pode ser removida e a configuração reimplantada.

## Limpar token de API {#purge-API-token}

Os clientes podem [limpar o cache da CDN](/help/implementing/dispatcher/cdn-cache-purge.md) usando um token de API de limpeza declarado. O token é declarado em um arquivo chamado `cdn.yaml` ou similar, em algum lugar sob uma pasta `config` de nível superior. Leia [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#folder-structure) para obter detalhes sobre a estrutura de pastas e como implantar a configuração.

A sintaxe é descrita abaixo:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
    authenticators:
       - name: purge-auth
         type: purge
         purgeKey1: ${{CDN_PURGEKEY_031224}}
         purgeKey2: ${{CDN_PURGEKEY_021225}}
    rules:
       - name: purge-auth-rule
         when: { reqProperty: tier, equals: "publish" }
         action:
           type: authenticate
           authenticator: purge-auth
```

Consulte [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#common-syntax) para obter uma descrição das propriedades acima do nó `data`. O valor da propriedade `kind` deve ser *CDN* e a propriedade `version` deve ser definida como `1`.

As propriedades adicionais incluem:

* Nó `data` que contém um nó `authentication` filho.
* Em `authentication`, um nó `authenticators` e um nó `rules`, ambos com matrizes.
* Autenticadores: permite declarar um tipo de token ou credencial, que, nesse caso, é uma chave de limpeza. Inclui as seguintes propriedades:
   * name - uma cadeia de caracteres descritiva.
   * tipo - deve ser expurgado.
   * purgeKey1 - o valor deve fazer referência a uma [Variável de ambiente do tipo secreto do Cloud Manager](/help/operations/config-pipeline.md#secret-env-vars). Para o campo Serviço Aplicado, selecione Todos. Recomenda-se que o valor (por exemplo, `${{CDN_PURGEKEY_031224}}`) reflita o dia em que foi adicionado.
   * purgeKey2 - usado para a rotação de segredos, que é descrita na seção [segredos em rotação](#rotating-secrets) abaixo. Pelo menos um de `purgeKey1` e `purgeKey2` deve ser declarado.
* Regras: permite declarar quais dos autenticadores devem ser usados e se são para o nível de publicação e/ou pré-visualização.  Inclui:
   * nome - uma sequência descritiva
   * when - uma condição que determina quando a regra deve ser avaliada, de acordo com a sintaxe no artigo [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md). Normalmente, incluirá uma comparação do nível atual (por exemplo, publicar).
   * ação - deve especificar &quot;autenticar&quot;, com o autenticador desejado referenciado.

>[!NOTE]
>A Chave de Limpeza deve ser configurada como uma [Variável de Ambiente Cloud Manager do tipo secreto](/help/operations/config-pipeline.md#secret-env-vars), antes da implantação da configuração que faz referência a ela. É recomendável usar uma chave aleatória exclusiva com comprimento mínimo de 32 bytes; por exemplo, a biblioteca criptográfica Open SSL pode gerar uma chave aleatória executando o comando openssl rand -hex 32

Você pode fazer referência a [um tutorial](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache) focado na configuração de chaves de limpeza e na execução da limpeza do cache do CDN.

## Autenticação básica {#basic-auth}

Protect determinados recursos de conteúdo, exibindo uma caixa de diálogo de autenticação básica que requer um nome de usuário e senha. Esse recurso destina-se principalmente a casos de uso de autenticação simples, como a análise de conteúdo pelas partes interessadas, e não como uma solução completa para os direitos de acesso do usuário final.

O usuário final terá uma caixa de diálogo de autenticação básica surgindo da seguinte maneira:

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


A sintaxe é a seguinte:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
    authenticators:
       - name: my-basic-authenticator
         type: basic
         credentials:
           - user: johndoe
             password: ${{JOHN_DOE_PASSWORD}}
           - user: janedoe
             password: ${{JANE_DOE_PASSWORD}}
    rules:
       - name: basic-auth-rule
         when: { reqProperty: path, like: "/summercampaign" }
         action:
           type: authenticate
           authenticator: my-basic-authenticator
```

Consulte [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#common-syntax) para obter uma descrição das propriedades acima do nó `data`. O valor da propriedade `kind` deve ser *CDN* e a propriedade `version` deve ser definida como `1`.

Além disso, a sintaxe inclui:

* um nó `data` que contém um nó `authentication`.
* Em `authentication`, um nó `authenticators` e um nó `rules`, ambos com matrizes.
* Autenticadores: neste cenário, declare um autenticador básico, que tenha a seguinte estrutura:
   * nome - uma sequência descritiva
   * tipo - deve ser `basic`
   * uma matriz de até 10 credenciais, cada uma incluindo os seguintes pares de nome/valor, que os usuários finais podem inserir na caixa de diálogo de autenticação básica:
      * usuário - o nome do usuário.
      * senha - seu valor deve fazer referência a uma [variável de ambiente do tipo secreto do Cloud Manager](/help/operations/config-pipeline.md#secret-env-vars), com **Todos** selecionados como o campo de serviço.
* Regras: permite declarar quais dos autenticadores devem ser usados e quais recursos devem ser protegidos. Cada regra inclui:
   * nome - uma sequência descritiva
   * when - uma condição que determina quando a regra deve ser avaliada, de acordo com a sintaxe no artigo [Regras de filtro de tráfego](/help/security/traffic-filter-rules-including-waf.md). Normalmente, isso incluirá uma comparação do nível de publicação ou caminhos específicos.
   * ação - deve especificar &quot;autenticar&quot;, com o autenticador desejado referenciado, que é basic-auth para este cenário

>[!NOTE]
>As senhas devem ser configuradas como [variáveis de ambiente do Cloud Manager do tipo secreto](/help/operations/config-pipeline.md#secret-env-vars), antes da implantação da configuração que faz referência a elas.

## Rotação de segredos {#rotating-secrets}

1. É uma boa prática de segurança alterar ocasionalmente as credenciais. Isso pode ser feito conforme exemplificado abaixo, usando o exemplo de uma chave de borda, embora a mesma estratégia seja usada para chaves de limpeza.

1. Inicialmente, apenas `edgeKey1` foi definido, neste caso referenciado como `${{CDN_EDGEKEY_052824}}`, que, como uma convenção recomendada, reflete a data em que foi criado.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
   ```

1. Quando for a hora de girar a chave, crie um novo segredo do Cloud Manager, por exemplo `${{CDN_EDGEKEY_041425}}`.
1. Na configuração, faça referência a ele a partir de `edgeKey2` e implante.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. Depois de ter certeza de que a chave de borda antiga não será mais usada, remova-a removendo `edgeKey1` da configuração.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. Exclua a referência secreta antiga (`${{CDN_EDGEKEY_052824}}`) da Cloud Manager e implante.

1. Quando estiver pronto para a próxima rotação, siga o mesmo procedimento. No entanto, dessa vez, você adicionará `edgeKey1` à configuração, fazendo referência a um novo segredo do ambiente do Cloud Manager chamado, por exemplo, `${{CDN_EDGEKEY_031426}}`.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
         edgeKey1: ${{CDN_EDGEKEY_031426}}
   ```
