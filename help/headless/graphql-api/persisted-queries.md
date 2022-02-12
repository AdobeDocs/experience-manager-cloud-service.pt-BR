---
title: Consultas GraphQL persistentes
description: Saiba como persistir consultas GraphQL no Adobe Experience Manager para otimizar o desempenho. As consultas persistentes podem ser solicitadas por aplicativos clientes usando o método HTTP GET e a resposta pode ser armazenada em cache nas camadas do dispatcher e CDN, melhorando, em última análise, o desempenho dos aplicativos clientes.
feature: Content Fragments,GraphQL API
source-git-commit: 0912cadeae13050c9cfc606d1c2b8f4236cd78ed
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---


# Consultas GraphQL persistentes {#persisted-queries-caching}

As consultas persistentes são consultas GraphQL criadas e armazenadas no servidor AEM. As consultas GraphQL padrão são executadas usando solicitações POST e a resposta não pode ser facilmente armazenada em cache. Consultas persistentes podem ser solicitadas com uma solicitação GET por aplicativos clientes. A resposta de uma solicitação de GET pode ser armazenada em cache nas camadas do dispatcher e CDN, melhorando, em última análise, o desempenho do aplicativo cliente solicitante.

As consultas persistentes devem sempre usar o terminal relacionado ao [configuração apropriada do Sites](graphql-endpoint.md); para que possam usar ou ambos:

* A configuração global e o terminal A consulta tem acesso a todos os Modelos de fragmento de conteúdo.
* Configuração(ões) de sites específicos e endpoint(s) A criação de uma consulta persistente para uma configuração de sites específica requer um endpoint específico para a configuração de sites correspondente (para fornecer acesso aos Modelos de fragmento de conteúdo relacionados).
Por exemplo, para criar uma consulta persistente especificamente para a configuração de Sites WKND, uma configuração de Sites específica de WKND correspondente e um endpoint específico de WKND devem ser criados antecipadamente.

>[!NOTE]
>
>Consulte [Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) para obter mais detalhes.
>
>O **Consultas de persistência GraphQL** precisam ser ativados para a configuração apropriada do Sites.

Por exemplo, se houver um query específico chamado `my-query`, que usa um modelo `my-model` na configuração Sites `my-conf`:

* Você pode criar um query usando o `my-conf` endpoint específico e, em seguida, o query será salvo da seguinte maneira:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Você pode criar a mesma query usando `global` endpoint, mas a consulta será salva como a seguir:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Essas são duas consultas diferentes - salvas em caminhos diferentes.
>
>Acontece que eles apenas usam o mesmo modelo - mas por diferentes endpoints.

## Como persistir uma consulta GraphQL

É recomendável manter consultas em um ambiente de criação de AEM inicialmente e, em seguida, [publicar o query](#publish-persisted-query) para um ambiente de publicação de AEM. Ferramentas como [Postman](https://www.postman.com/) ou ferramentas de linha de comando como [curl](https://curl.se/) pode ser usada.

Estas são as etapas para persistir um determinado query usando o **curl** ferramenta de linha de comando:

1. Prepare a consulta colocando-a no novo URL do ponto final `/graphql/persist.json/<config>/<persisted-label>`.

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

1. Você pode solicitar a consulta persistente usando GETthe URL `/graphql/execute.json/<shortPath>`.

   Por exemplo, use a consulta persistente:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Atualize uma consulta persistente do POSTing para um caminho de consulta já existente.

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

1. Crie uma consulta simples encapsulada.

   Por exemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Crie uma consulta simples encapsulada com controle de cache.

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

## Publicar uma consulta persistente {#publish-persisted-query}

As consultas persistentes podem ser publicadas em um ambiente de publicação do AEM, onde podem ser solicitadas por aplicativos clientes. Para usar uma consulta persistente na publicação, a árvore persistente relacionada precisa ser replicada.

Há várias abordagens para a publicação de uma consulta persistente:

* **Uso de um POST para replicação**:

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

* **Uso de um pacote**:
   1. Crie uma nova definição de pacote.
   1. Inclua a configuração (por exemplo, `/conf/wknd/settings/graphql/persistentQueries`).
   1. Crie o pacote.
   1. Replicar o pacote.

* **Uso da ferramenta de replicação/distribuição**:
   1. Vá para a ferramenta Distribution .
   1. Selecione a ativação em árvore para a configuração (por exemplo, `/conf/wknd/settings/graphql/persistentQueries`).

* **Uso de um workflow (por meio da configuração do iniciador do workflow)**:
   1. Defina uma regra do iniciador do workflow para executar um modelo de workflow que replicaria a configuração em eventos diferentes (por exemplo, criar, modificar, entre outros).

Quando a configuração da consulta estiver em publicação, os mesmos princípios de autenticação serão aplicados, usando o endpoint de publicação.

>[!NOTE]
>
>Para acesso anônimo, o sistema assume que a ACL permite que &quot;todos&quot; tenham acesso à configuração da consulta.
>
>Se esse não for o caso, não será possível executar.

>[!NOTE]
>
>Qualquer ponto e vírgula (&quot;;&quot;) nos URLs precisa ser codificado.
>
>Por exemplo, como na solicitação para executar uma consulta mantida:
>
>
```xml
>curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
>```
