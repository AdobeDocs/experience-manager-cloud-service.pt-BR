---
title: 'Consultas persistentes de GraphQL '
description: Saiba como criar consultas persistentes de GraphQL no Adobe Experience Manager as a Cloud Service para otimizar o desempenho. As consultas persistentes podem ser solicitadas por aplicativos clientes usando o método GET do HTTP e a resposta pode ser armazenada em cache nas camadas do Dispatcher e do CDN, melhorando, em última análise, o desempenho dos aplicativos clientes.
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 2ee21b507b5dcc9471063b890976a504539b7e10
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 96%

---

# Consultas persistentes de GraphQL  {#persisted-queries-caching}

As consultas persistentes são consultas de GraphQL criadas e armazenadas no servidor do Adobe Experience Manager (AEM) as a Cloud Service. Elas podem ser solicitadas com uma solicitação GET por aplicativos clientes. A resposta para uma solicitação GET pode ser armazenada em cache nas camadas do Dispatcher e do CDN, melhorando, em última análise, o desempenho do aplicativo cliente solicitante. Isso é diferente das consultas de GraphQL padrão, que são executadas usando solicitações POST, onde a resposta não pode ser facilmente armazenada em cache.

O [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) está disponível no AEM para que você desenvolva, teste e persista suas consultas GraphQL, antes [transferência para o ambiente de produção](#transfer-persisted-query-production). Para casos que precisam de personalização (por exemplo, ao [personalizar o cache](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)), é possível usar a API; consulte o exemplo de curl fornecido em [Como criar uma consulta persistente de GraphQL](#how-to-persist-query).

## Endpoints e consultas persistentes {#persisted-queries-and-endpoints}

Consultas persistentes devem sempre usar o endpoint relacionado à [configuração apropriada do Sites](graphql-endpoint.md); para que possam usar um desses, ou ambos:

* A configuração global e o endpoint 
A consulta tem acesso a todos os modelos de fragmento de conteúdo.
* Configuração(ões) e endpoint(s) do Sites específicos 
A criação de uma consulta persistente para uma configuração do Sites específica requer um endpoint correspondente específico para a configuração do Sites (para fornecer acesso aos modelos de fragmento de conteúdo relacionados).
Por exemplo, para criar uma consulta persistente especificamente para a configuração do Sites WKND, uma configuração do Sites correspondente específica de WKND e um endpoint específico de WKND devem ser criados antecipadamente.

>[!NOTE]
>
>Consulte [Habilitar a funcionalidade de fragmentos de conteúdo no Navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) para obter mais detalhes.
>
>As **consultas persistentes de GraphQL** precisam estar habilitadas na configuração apropriada do Sites.

Por exemplo, se houver uma consulta específica chamada `my-query`, que usa um modelo `my-model` da configuração `my-conf` do Sites:

* É possível criar uma consulta usando o endpoint específico `my-conf` e, em seguida, a consulta será salva da seguinte maneira:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* É possível criar a mesma consulta usando o endpoint `global`, mas a consulta será salva da seguinte maneira:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Essas são duas consultas diferentes - salvas em caminhos diferentes.
>
>Por acaso, elas usam o mesmo modelo - mas por meio de diferentes endpoints.

## Como criar uma consulta persistente de GraphQL {#how-to-persist-query}

É recomendável criar consultas persistentes em um ambiente de criação do AEM inicialmente e, em seguida, [transferir a consulta](#transfer-persisted-query-production) para o ambiente de publicação da sua produção do AEM para ser usada pelos aplicativos.

Há vários métodos para criar consultas persistentes, incluindo:

* o GraphiQL IDE - consulte [Salvar consultas persistentes](/help/headless/graphql-api/graphiql-ide.md##saving-persisted-queries)
* curl - consulte o exemplo a seguir
* Outras ferramentas, incluindo o [Postman](https://www.postman.com/)

Estas são as etapas para criar uma determinada consulta persistente usando a ferramenta de linha de comando **curl**:

1. Prepare a consulta utilizando o método PUT no novo URL do endpoint `/graphql/persist.json/<config>/<persisted-label>`.

   Por exemplo, crie uma consulta persistente:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. Neste ponto, verifique a resposta.

   Por exemplo, verifique se há sucesso:

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. É possível solicitar a consulta persistente utilizando o método GET com o URL `/graphql/execute.json/<shortPath>`.

   Por exemplo, use a consulta persistente:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Atualize uma consulta persistente utilizando o método POST em um caminho de consulta já existente.

   Por exemplo, use a consulta persistente:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Crie uma consulta agrupada simples.

   Por exemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Crie uma consulta agrupada simples com controle de cache.

   Por exemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Crie uma consulta persistente com parâmetros:

   Por exemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. Execução de uma consulta com parâmetros.

   Por exemplo:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

## Transferir uma consulta persistente para o ambiente de produção  {#transfer-persisted-query-production}

A consulta persistente precisa estar em seu ambiente de publicação de produção (do AEM as a Cloud Service), onde pode ser solicitada pelos aplicativos clientes. Para usar uma consulta persistente no ambiente de publicação de produção, a árvore persistente relacionada precisa ser replicada:

* inicialmente no autor de produção para validar o conteúdo recém-criado com as consultas
* e, por fim, na publicação da produção para consumo em tempo real

Existem várias abordagens para transferir a consulta persistente:

1. Uso de um pacote:
   1. Crie uma nova definição de pacote.
   1. Inclua a configuração (por exemplo, `/conf/wknd/settings/graphql/persistentQueries`).
   1. Crie o pacote.
   1. Transfira o pacote (baixe/carregue ou replique).
   1. Instale o pacote.

1. Uso de POST para replicação:

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->

Assim que a configuração da consulta estiver no ambiente de publicação em produção, os mesmos princípios de autenticação se aplicam, apenas usando o endpoint de publicação.

>[!NOTE]
>
>Para acesso anônimo, o sistema assume que a ACL permite que “todos” tenham acesso à configuração da consulta.
>
>Se esse não for o caso, não será possível executar.

## Codificação do URL de consulta para uso por um aplicativo {#encoding-query-url}

Para uso por um aplicativo, qualquer ponto e vírgula (“;”) nos URLs precisa ser codificado.

Por exemplo, como na solicitação para executar uma consulta persistente:

```xml
curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
```

Para usar uma consulta persistente em um aplicativo cliente, o SDK cliente do AEM headless deve ser usado [Cliente do AEM headless para JavaScript](https://github.com/adobe/aem-headless-client-js).