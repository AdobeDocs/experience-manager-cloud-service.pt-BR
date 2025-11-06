---
title: Consultas persistentes de GraphQL
description: Saiba como criar consultas persistentes de GraphQL no Adobe Experience Manager as a Cloud Service para otimizar o desempenho. As consultas persistentes podem ser solicitadas por aplicativos clientes usando o método GET do HTTP e a resposta pode ser armazenada em cache nas camadas do Dispatcher e do CDN, melhorando, em última análise, o desempenho dos aplicativos clientes.
feature: Headless, Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 79%

---

# Consultas persistentes de GraphQL {#persisted-graphql-queries}

As consultas persistentes são consultas de GraphQL criadas e armazenadas no servidor do Adobe Experience Manager (AEM) as a Cloud Service. Elas podem ser solicitadas com uma solicitação GET por aplicativos clientes. A resposta para uma solicitação GET pode ser armazenada em cache nas camadas do Dispatcher e do CDN, melhorando, em última análise, o desempenho do aplicativo cliente solicitante. Isso é diferente das consultas de GraphQL padrão, que são executadas usando solicitações POST, onde a resposta não pode ser facilmente armazenada em cache.

>[!NOTE]
>
>Consultas persistentes são recomendadas. Consulte [Práticas recomendadas de consulta GraphQL (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) para obter detalhes e a configuração relacionada do Dispatcher.

O [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md) está disponível no AEM para que você desenvolva, teste e crie consultas GraphQL persistentes antes de [transferi-las para o ambiente de produção](#transfer-persisted-query-production). Para casos que precisam de personalização (por exemplo, ao [personalizar o armazenamento em cache](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)), é possível usar a API; consulte o exemplo de cURL fornecido em [Como criar uma consulta persistente de GraphQL](#how-to-persist-query).

## Endpoints e consultas persistentes {#persisted-queries-and-endpoints}

Consultas persistentes devem sempre usar o endpoint relacionado à [configuração apropriada do Sites](graphql-endpoint.md); para que possam usar um desses, ou ambos:

* A configuração global e o endpoint 
A consulta tem acesso a todos os modelos de fragmento de conteúdo.
* Configuração(ões) e endpoint(s) do Sites específicos 
A criação de uma consulta persistente para uma configuração do Sites específica requer um endpoint correspondente específico para a configuração do Sites (para fornecer acesso aos modelos de fragmento de conteúdo relacionados).
Por exemplo, para criar uma consulta persistente especificamente para a configuração do Sites WKND, uma configuração do Sites correspondente específica de WKND e um endpoint específico de WKND devem ser criados antecipadamente.

>[!NOTE]
>
>Consulte [Habilitar a funcionalidade de fragmentos de conteúdo no Navegador de configuração](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser) para obter mais detalhes.
>
>As **Consultas GraphQL persistidas** precisam estar habilitadas para a configuração apropriada do Sites.

Por exemplo, se houver uma consulta específica chamada `my-query`, que usa um modelo `my-model` da configuração `my-conf` do Sites:

* É possível criar uma consulta usando o ponto de acesso específico `my-conf` e, em seguida, a consulta será salva da seguinte maneira:
  `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* É possível criar a mesma consulta usando o ponto de acesso `global`, mas a consulta será salva da seguinte maneira:
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
* cURL - consulte o exemplo a seguir
* Outras ferramentas, incluindo o [Postman](https://www.postman.com/)

O GraphiQL IDE é o método **preferencial** para consultas persistentes. Para criar uma determinada consulta persistente usando a ferramenta de linha de comando **cURL**:

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

1. Por exemplo, `wknd` é o nome da configuração e `plain-article-query` é o nome da consulta persistente. Para executar a consulta:

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

A codificação UTF-8 `%3B` é para `;` e `%3D` é a codificação para `=`. As variáveis de consulta e quaisquer caracteres especiais devem ser [corretamente codificados](#encoding-query-url) para que a consulta persistente seja executada.

### Uso de variáveis de consulta - Práticas recomendadas {#query-variables-best-practices}

Ao usar variáveis em suas consultas, há algumas práticas recomendadas que devem ser seguidas:

* Codificação
Como uma abordagem geral, é sempre recomendável codificar todos os caracteres especiais; por exemplo, `;`, `=`, `?`, `&`, entre outros.

* Ponto e vírgula
As consultas persistentes que usam várias variáveis (separadas por ponto e vírgula) precisam ter:
   * o ponto e vírgula codificado (`%3B`); a codificação da URL também alcançará isso
   * ou um ponto e vírgula à direita adicionado ao final da consulta

* `CACHE_GRAPHQL_PERSISTED_QUERIES`
Quando `CACHE_GRAPHQL_PERSISTED_QUERIES` é habilitado para a Dispatcher, os parâmetros que contêm os caracteres `/` ou `\` em seus valores são codificados duas vezes no nível da Dispatcher.
Para evitar essa situação:

   * Habilitar `DispatcherNoCanonURL` no Dispatcher.
Isso instruirá o Dispatcher a encaminhar o URL original para o AEM, evitando codificações duplicadas.
No entanto, no momento, essa configuração só funciona no nível `vhost`, portanto, se você já tiver configurações do Dispatcher para regravar URLs (por exemplo, ao usar URLs encurtadas), talvez precise de um `vhost` separado para URLs de consulta persistente.

   * Enviar `/` ou `\` caracteres sem codificação.

     Ao chamar a URL da consulta persistente, certifique-se de que todos os `/` ou `\` caracteres permaneçam não codificados no valor das variáveis de consulta persistente.

     >[!NOTE]
     >
     >Essa opção só é recomendada para quando a solução `DispatcherNoCanonURL` não puder ser implementada por algum motivo.

* `CACHE_GRAPHQL_PERSISTED_QUERIES`

  Quando `CACHE_GRAPHQL_PERSISTED_QUERIES` está habilitado para a Dispatcher, o caractere `;` não pode ser usado no valor de uma variável.

## Armazenamento em cache de consultas persistentes {#caching-persisted-queries}

Consultas persistentes são recomendadas, pois elas podem ser armazenadas em cache nas camadas do [Dispatcher](/help/headless/deployment/dispatcher.md) e da Rede de entrega de conteúdo (CDN), melhorando o desempenho do aplicativo do cliente solicitante.

Por padrão, o AEM invalidará o cache com base em uma definição de Time To Live (TTL). Esses TTLs podem ser definidos pelos seguintes parâmetros. Estes parâmetros podem ser acessados por vários meios, com variações nos nomes de acordo com o mecanismo usado:

| Tipo de cache | [Cabeçalho HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Headers/Cache-Control)  | cURL  | Configuração OSGi | Cloud Manager |
|--- |--- |--- |--- |--- |
| Navegador | `max-age` | `cache-control : max-age` | `cacheControlMaxAge` | `graphqlCacheControl` |
| CDN | `s-maxage` | `surrogate-control : max-age` | `surrogateControlMaxAge` | `graphqlSurrogateControl` | 60 |
| CDN | `stale-while-revalidate` | `surrogate-control : stale-while-revalidate ` | `surrogateControlStaleWhileRevalidate` | `graphqlStaleWhileRevalidate` |
| CDN | `stale-if-error` | `surrogate-control : stale-if-error` | `surrogateControlStaleIfError` | `graphqlStaleIfError` |

{style="table-layout:auto"}

### Instâncias de criação {#author-instances}

Para instâncias de criação, os valores padrão são:

* `max-age`  : 60
* `s-maxage` : 60
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

Estes:

* não pode ser substituído:
   * por uma configuração OSGi
* pode ser substituído:
   * por uma solicitação que define as configurações do cabeçalho HTTP usando cURL; deve incluir configurações adequadas para `cache-control` e/ou `surrogate-control`; para obter exemplos, consulte [Gerenciamento do cache no nível de consulta persistente](#cache-persisted-query-level)
   * se você especificar valores na caixa de diálogo **Cabeçalhos** do [GraphiQL IDE](#http-cache-headers-graphiql-ide)

### Publicar instâncias {#publish-instances}

Para instâncias de publicação, os valores padrão são:

* `max-age`  : 60
* `s-maxage` : 7200
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

Eles podem ser substituídos:

* [no GraphQL IDE](#http-cache-headers-graphiql-ide)

* [no Nível de consulta persistente](#cache-persisted-query-level); envolve postar a consulta no AEM usando cURL na interface da linha de comando e publicar a consulta persistente.

* [com variáveis do Cloud Manager](#cache-cloud-manager-variables)

* [por uma configuração OSGi](#cache-osgi-configration)

### Gerenciamento de cabeçalhos de cache HTTP no GraphiQL IDE {#http-cache-headers-graphiql-ide}

O GraphiQL IDE - consulte [Salvar consultas persistentes](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

### Gerenciamento de cache no nível de Consulta persistente {#cache-persisted-query-level}

Envolve postar a consulta no AEM usando o cURL na interface da linha de comando.

Para obter um exemplo do método PUT (criar):

```bash
curl -u admin:admin -X PUT \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

Para obter um exemplo do método POST (atualizar):

```bash
curl -u admin:admin -X POST \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

O `cache-control` pode ser definido no momento da criação (PUT) ou posteriormente (por exemplo, por meio de uma solicitação POST por instância). O controle de cache é opcional ao criar a consulta persistente, pois o AEM pode fornecer o valor padrão. Consulte [Como criar uma consulta persistente de GraphQL](#how-to-persist-query), para obter um exemplo de criação de consulta persistente usando cURL.

### Gerenciamento de cache com variáveis do Cloud Manager {#cache-cloud-manager-variables}

[Variáveis de ambiente do Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) podem ser definidas com o Cloud Manager para definir os valores necessários:

| Nome | Valor | Serviço aplicado | Tipo |
|--- |--- |--- |--- |
| `graphqlStaleIfError` | 86400 | *conforme adequado* | *conforme adequado* |
| `graphqlSurrogateControl` | 600 | *conforme adequado* | *conforme adequado* |

{style="table-layout:auto"}

### Gerenciamento de cache com uma configuração OSGi {#cache-osgi-configration}

Para gerenciar o cache globalmente, você pode [definir as configurações do OSGi](/help/implementing/deploying/configuring-osgi.md) para a **Configuração do Serviço de consulta persistente**.

>[!NOTE]
>
>Para controle de cache, a configuração do OSGi é apropriada somente para instâncias de publicação. A configuração existe nas instâncias de criação, mas é ignorada.

>[!NOTE]
>
>A **configuração do Serviço de consulta persistente** também é usada para [configurar o código de resposta da consulta](#configuring-query-response-code).

A configuração padrão OSGi para instâncias de publicação:

* lê as variáveis do Cloud Manager, se disponíveis:

  | Propriedade de configuração OSGi | lê isto | Variável do Cloud Manager |
  |--- |--- |--- |
  | `cacheControlMaxAge` | lê | `graphqlCacheControl` |
  | `surrogateControlMaxAge` | lê | `graphqlSurrogateControl` |
  | `surrogateControlStaleWhileRevalidate` | lê | `graphqlStaleWhileRevalidate` |
  | `surrogateControlStaleIfError` | lê | `graphqlStaleIfError` |

  {style="table-layout:auto"}

* e, se não estiver disponível, a configuração OSGi usará os [valores padrão para instâncias de publicação](#publish-instances).

## Configuração do código de resposta da consulta {#configuring-query-response-code}

Por padrão, a variável `PersistedQueryServlet` envia uma resposta `200` quando executa uma consulta, independentemente do resultado real.

Você pode [definir as configurações de OSGi](/help/implementing/deploying/configuring-osgi.md) para a **Configuração do Serviço de Consulta Persistente** para controlar se códigos de status mais detalhados são retornados pelo ponto de extremidade `/execute.json/persisted-query` quando há um erro na consulta persistente.

>[!NOTE]
>
>A variável **configuração do Serviço de consulta persistente** também é usada para [gerenciamento de cache](#cache-osgi-configration).

O campo `Respond with application/graphql-response+json` (`responseContentTypeGraphQLResponseJson`) pode ser definido conforme necessário:

* `false` (valor padrão):
não importa se a consulta persistente é bem-sucedida ou não. O cabeçalho `Content-Type` retornado é `application/json`, e o `/execute.json/persisted-query` *sempre* retorna o código de status `200`.

* `true`:
O `Content-Type` retornado é `application/graphql-response+json`, e o ponto de extremidade retornará o código de resposta apropriado quando houver qualquer forma de erro ao executar a consulta persistente:

  | Código | Descrição |
  |--- |--- |
  | 200 | Resposta bem-sucedida |
  | 400 | Indica que há cabeçalhos ausentes ou um problema com o caminho de consulta persistente. Por exemplo, nome de configuração não especificado, sufixo não especificado e outros.<br>Consulte [Solução de problemas - Ponto de extremidade do GraphQL não configurado](/help/headless/graphql-api/persisted-queries-troubleshoot.md#missing-path-query-url). |
  | 404 | O recurso solicitado não foi encontrado. Por exemplo, o endpoint do Graphql não está disponível no servidor.<br>Consulte [Solução de problemas - Caminho ausente na URL de consulta persistente do GraphQL](/help/headless/graphql-api/persisted-queries-troubleshoot.md#graphql-endpoint-not-configured). |
  | 500 | Erro interno do servidor. Por exemplo, erros de validação, erro de persistência e outros. |

  >[!NOTE]
  >
  >Consulte também https://graphql.github.io/graphql-over-http/draft/#sec-Status-Codes

## Codificação do URL da consulta para uso por um aplicativo {#encoding-query-url}

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
1. Crie um novo pacote tocando em **Criar pacote**. Isso abre uma caixa de diálogo para definir o pacote.
1. Em **Geral** na caixa de diálogo Definição do pacote, insira um **Nome** como “wknd-persistent-queries”.
1. Insira um número de versão como “1.0”.
1. Em **Filtros**, adicione um novo **Filtro**. Use o Localizador de caminhos para selecionar a pasta `persistentQueries`, abaixo da configuração. Por exemplo, para a configuração `wknd`, o caminho completo será `/conf/wknd/settings/graphql/persistentQueries`.
1. Selecione **Salvar** para salvar a nova definição de pacote e fechar a caixa de diálogo.
1. Selecione o botão **Criar** na definição de pacote criada.

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
