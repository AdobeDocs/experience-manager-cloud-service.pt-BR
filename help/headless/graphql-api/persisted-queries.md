---
title: Consultas persistentes de GraphQL
description: Saiba como criar consultas persistentes de GraphQL no Adobe Experience Manager as a Cloud Service para otimizar o desempenho. As consultas persistentes podem ser solicitadas por aplicativos clientes usando o método GET do HTTP e a resposta pode ser armazenada em cache nas camadas do Dispatcher e do CDN, melhorando, em última análise, o desempenho dos aplicativos clientes.
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 9bfb5bc4b340439fcc34e97f4e87d711805c0d82
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 100%

---

# Consultas persistentes de GraphQL  {#persisted-queries-caching}

As consultas persistentes são consultas de GraphQL criadas e armazenadas no servidor do Adobe Experience Manager (AEM) as a Cloud Service. Elas podem ser solicitadas com uma solicitação GET por aplicativos clientes. A resposta para uma solicitação GET pode ser armazenada em cache nas camadas do Dispatcher e do CDN, melhorando, em última análise, o desempenho do aplicativo cliente solicitante. Isso é diferente das consultas de GraphQL padrão, que são executadas usando solicitações POST, onde a resposta não pode ser facilmente armazenada em cache.

>[!NOTE]
>
>Consultas persistentes são recomendadas. Consulte [Práticas recomendadas de consulta GraphQL (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) para obter detalhes e a configuração relacionada do Dispatcher.

O [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) está disponível no AEM para que você desenvolva, teste e crie consultas GraphQL persistentes antes de [transferi-las para o ambiente de produção](#transfer-persisted-query-production). Para casos que precisam de personalização (por exemplo, ao [personalizar o cache](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)), é possível usar a API; consulte o exemplo de curl fornecido em [Como criar uma consulta persistente de GraphQL](#how-to-persist-query).

## Endpoints e consultas persistentes {#persisted-queries-and-endpoints}

Consultas persistentes devem sempre usar o endpoint relacionado à [configuração apropriada do Sites](graphql-endpoint.md); para que possam usar um desses, ou ambos:

* A configuração global e o endpoint 
A consulta tem acesso a todos os modelos de fragmento de conteúdo.
* Configuração(ões) e endpoint(s) do Sites específicos 
A criação de uma consulta persistente para uma configuração do Sites específica requer um endpoint correspondente específico para a configuração do Sites (para fornecer acesso aos modelos de fragmento de conteúdo relacionados).
Por exemplo, para criar uma consulta persistente especificamente para a configuração do Sites WKND, uma configuração do Sites correspondente específica de WKND e um endpoint específico de WKND devem ser criados antecipadamente.

>[!NOTE]
>
>Consulte [Habilitar a funcionalidade de fragmentos de conteúdo no Navegador de configuração](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) para obter mais detalhes.
>
>As **Consultas GraphQL persistidas** precisam estar habilitadas para a configuração apropriada do Sites.

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

* GraphiQL IDE - consulte [Salvar consultas persistentes](/help/headless/graphql-api/graphiql-ide.md#saving-persisted-queries) (método preferencial)
* curl - consulte o exemplo a seguir
* Outras ferramentas, incluindo o [Postman](https://www.postman.com/)

O GraphiQL IDE é o método **preferencial** para consultas persistentes. Para criar uma determinada consulta persistente usando a ferramenta de linha de comando **curl**:

1. Prepare a consulta utilizando o método PUT no novo URL do endpoint `/graphql/persist.json/<config>/<persisted-label>`.

   Por exemplo, crie uma consulta persistente:

   ```shell
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

   ```json
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

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Atualize uma consulta persistente utilizando o método POST em um caminho de consulta já existente.

   Por exemplo, use a consulta persistente:

   ```shell
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

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Crie uma consulta agrupada simples com controle de cache.

   Por exemplo:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Crie uma consulta persistente com parâmetros:

   Por exemplo:

   ```shell
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


## Como executar uma consulta persistente {#execute-persisted-query}

Para executar uma consulta persistente, um aplicativo cliente faz uma solicitação GET usando a seguinte sintaxe:

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

Onde `PERSISTENT_PATH` é um caminho encurtado no qual a consulta persistida é salva.

1. Por exemplo, `wknd` é o nome da configuração e `plain-article-query` é o nome da consulta persistida. Para executar a consulta:

   ```shell
   $ curl -X GET \
       https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query
   ```

1. Execução de uma consulta com parâmetros.

   >[!NOTE]
   >
   > As variáveis e os valores de consulta devem ser corretamente [codificados](#encoding-query-url) ao executar uma consulta persistida.

   Por exemplo:

   ```xml
   $ curl -X GET \
       "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   Consulte o uso de [variáveis de consulta](#query-variables) para obter mais detalhes.

## Uso de variáveis de consulta {#query-variables}

As variáveis de consulta podem ser usadas com consultas persistentes. As variáveis de consulta são anexadas à solicitação e prefixadas por ponto e vírgula (`;`), usando o nome e o valor da variável. As variáveis são separadas por ponto e vírgula.

O padrão é semelhante ao seguinte:

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

Por exemplo, a consulta a seguir contém uma variável `activity` para filtrar uma lista com base em um valor de atividade:

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

Esta consulta pode ser persistida em um caminho `wknd/adventures-by-activity`. Para chamar a consulta persistente onde `activity=Camping`, a solicitação terá esta aparência:

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

Observe que `%3B` é a codificação UTF-8 para `;` e `%3D` é a codificação para `=`. As variáveis de consulta e quaisquer caracteres especiais devem ser [corretamente codificados](#encoding-query-url) para que a consulta persistente seja executada.

## Armazenamento em cache de consultas persistentes {#caching-persisted-queries}

As consultas persistentes são recomendadas pois podem ser armazenadas em cache nas camadas do Dispatcher e do CDN, o que melhora o desempenho do aplicativo cliente solicitante.

Por padrão, o AEM invalidará o cache da rede de entrega de conteúdo (CDN) com base em um TTL (Time To Live) padrão.

Esse valor é definido como:

* 7200 segundos é o TTL padrão para o Dispatcher e o CDN; também conhecido como *caches compartilhados*
   * padrão: s-maxage=7200
* 60 é o TTL padrão para o cliente (por exemplo, um navegador)
   * padrão: maxage=60

Caso deseje alterar o TTL para sua consulta GraphLQ, ela deverá ser:

* persistida após gerenciar os [Cabeçalhos de cache HTTP do GraphQL IDE](#http-cache-headers)
* persistida usando o [método da API](#cache-api).

### Gerenciar cabeçalhos de cache HTTP no GraphQL  {#http-cache-headers-graphql}

O GraphiQL IDE - consulte [Salvar consultas persistentes](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

### Gerenciamento de cache a partir da API {#cache-api}

Isso envolve postar a consulta no AEM usando o CURL na interface da linha de comando.

Por exemplo:

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "https://publish-p123-e456.adobeaemcloud.com/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

O `cache-control` pode ser definido no momento da criação (PUT) ou posteriormente (por exemplo, por meio de uma solicitação POST por instância). O controle de cache é opcional ao criar a consulta persistente, pois o AEM pode fornecer o valor padrão. Consulte [Como criar uma consulta persistente de GraphQL](/help/headless/graphql-api/persisted-queries.md#how-to-persist-query), para obter um exemplo de criação de consulta persistente usando curl.

## Codificação do URL de consulta para uso por um aplicativo {#encoding-query-url}

Para uso por um aplicativo, quaisquer caracteres especiais usados ao criar variáveis de consulta (ou seja, ponto e vírgula (`;`), sinal de igual (`=`), barras `/`) devem ser convertidos para usar a codificação UTF-8 correspondente.

Por exemplo:

```xml
curl -X GET \ "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

O URL pode ser dividido nas seguintes partes:

| Parte do URL | Descrição |
|----------| -------------|
| `/graphql/execute.json` | Endpoint de consulta persistida |
| `/wknd/adventure-by-path` | Caminho de consulta persistida |
| `%3B` | Codificação de `;` |
| `adventurePath` | Variável de consulta |
| `%3D` | Codificação de `=` |
| `%2F` | Codificação de `/` |
| `%2Fcontent%2Fdam...` | Caminho codificado para o fragmento de conteúdo |

Em textos sem formatação, o URI da solicitação tem a seguinte aparência:

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

Para usar uma consulta persistente em um aplicativo cliente, o SDK do cliente do AEM Headless deve ser usado para [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java) ou [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). O SDK do cliente headless codificará automaticamente todas as variáveis de consulta apropriadamente na solicitação.

## Transferir uma consulta persistente para o ambiente de produção  {#transfer-persisted-query-production}

As consultas persistentes devem sempre ser criadas em um serviço de autor do AEM e publicadas (replicadas) em um serviço de publicação do AEM. Geralmente, as consultas persistentes são criadas e testadas em ambientes inferiores, como ambientes locais ou de desenvolvimento. Então, é necessário promover consultas persistentes a ambientes de nível superior, disponibilizando-as em um ambiente de publicação do AEM em produção para que os aplicativos clientes as consumam.

### Pacote de consultas persistidas

As consultas persistidas podem ser inseridas em [pacotes do AEM](/help/implementing/developing/tools/package-manager.md). Os pacotes do AEM podem ser baixados e instalados em diferentes ambientes. Os pacotes do AEM também podem ser replicados de um ambiente de autor do AEM para ambientes de publicação do AEM.

Para criar um pacote:

1. Navegue até **Ferramentas** > **Implantação** > **Pacotes**.
1. Crie um novo pacote tocando em **Criar pacote**. Isso abrirá uma caixa de diálogo para definir o pacote.
1. Em **Geral** na caixa de diálogo Definição do pacote, insira um **Nome** como “wknd-persistent-queries”.
1. Insira um número de versão como “1.0”.
1. Em **Filtros**, adicione um novo **Filtro**. Use o Localizador de caminhos para selecionar a pasta `persistentQueries`, abaixo da configuração. Por exemplo, para a configuração `wknd`, o caminho completo será `/conf/wknd/settings/graphql/persistentQueries`.
1. Toque em **Salvar** para salvar a nova definição de pacote e fechar a caixa de diálogo.
1. Toque no botão **Criar** na definição de pacote recém-criada.

Depois que o pacote tiver sido criado, você poderá:

* **Baixar** o pacote e fazer upload dele em um ambiente diferente.
* **Replicar** o pacote tocando em **Mais** > **Replicar**. Isso replicará o pacote no ambiente de publicação conectado do AEM.

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
