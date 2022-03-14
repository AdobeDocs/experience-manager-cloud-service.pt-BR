---
title: 'Consultas persistentes de GraphQL '
description: Saiba como criar consultas persistentes de GraphQL no Adobe Experience Manager para otimizar o desempenho. As consultas persistentes podem ser solicitadas por aplicativos clientes usando o método GET do HTTP e a resposta pode ser armazenada em cache nas camadas do Dispatcher e do CDN, melhorando, em última análise, o desempenho dos aplicativos clientes.
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 100%

---

# Consultas persistentes de GraphQL  {#persisted-queries-caching}

Consultas persistentes são consultas de GraphQL criadas e armazenadas no servidor do AEM. As consultas de GraphQL padrão são executadas usando solicitações POST e a resposta não pode ser armazenada em cache com facilidade. Consultas persistentes podem ser feitas através de uma solicitação GET de aplicativos clientes. A resposta para uma solicitação GET pode ser armazenada em cache nas camadas do Dispatcher e do CDN, melhorando, em última análise, o desempenho do aplicativo cliente solicitante.

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
>As **Consultas de persistência GraphQL** precisam estar habilitadas para a configuração apropriada do Sites.

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

## Como criar uma consulta persistente de GraphQL

É recomendável criar consultas persistentes inicialmente em um ambiente de criação do AEM e, em seguida, [publicar a consulta](#publish-persisted-query) em um ambiente de publicação do AEM. Ferramentas como [Postman](https://www.postman.com/) ou ferramentas de linha de comando como [curl](https://curl.se/) podem ser usadas.

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

## Publicar uma consulta persistente {#publish-persisted-query}

As consultas persistentes podem ser publicadas em um ambiente de publicação do AEM, onde podem ser solicitadas por aplicativos clientes. Para usar uma consulta persistente na publicação, a árvore persistente relacionada precisa ser replicada.

Há várias abordagens para a publicação de uma consulta persistente:

* **Uso de POST para replicação**:

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
   1. Replique o pacote.

* **Uso da ferramenta de replicação/distribuição**:
   1. Vá para a ferramenta de Distribuição.
   1. Selecione a ativação em árvore para a configuração (por exemplo, `/conf/wknd/settings/graphql/persistentQueries`).

* **Uso de um fluxo de trabalho (por meio da configuração do iniciador do fluxo de trabalho)**:
   1. Defina uma regra do iniciador do fluxo de trabalho para executar um modelo de fluxo de trabalho que replique a configuração em eventos diferentes (por exemplo, criar, modificar, entre outros).

Quando a configuração da consulta estiver em publicação, os mesmos princípios de autenticação serão aplicados no uso do endpoint de publicação.

>[!NOTE]
>
>Para acesso anônimo, o sistema assume que a ACL permite que “todos” tenham acesso à configuração da consulta.
>
>Se esse não for o caso, não será possível executar.

>[!NOTE]
>
>Qualquer ponto e vírgula (&quot;;&quot;) nos URLs precisa ser codificado.
>
>Por exemplo, como na solicitação para executar uma consulta persistente:
>
>```xml
>curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
>```
