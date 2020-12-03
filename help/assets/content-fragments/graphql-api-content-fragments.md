---
title: Delivery de conteúdo usando fragmentos de conteúdo com o Adobe Experience Manager como uma API Cloud Service GraphQL
description: Saiba como usar Fragmentos de conteúdo no Adobe Experience Manager (AEM) como um Cloud Service com a API AEM GraphQL para o Delivery de conteúdo sem cabeçalho.
translation-type: tm+mt
source-git-commit: 1e9596fb12a38f5c4c6e15d7c33af86e59e76083
workflow-type: tm+mt
source-wordcount: '2491'
ht-degree: 1%

---


# AEM API GraphQL para uso com Fragmentos de conteúdo {#graphql-api-for-use-with-content-fragments}

>[!CAUTION]
>
>A API AEM GraphQL, para o Delivery de fragmento de conteúdo, será lançada no início de 2021.
>
>A documentação relacionada já está disponível para fins de pré-visualização.

A API Adobe Experience Manager como Cloud Service (AEM) GraphQL usada com Fragmentos de conteúdo é altamente baseada na API GraphQL de código aberto e padrão.

Usar a API GraphQL no AEM permite o delivery eficiente dos Fragmentos de conteúdo para clientes JavaScript em implementações CMS sem cabeçalho:

* Evitar solicitações iterativas de API como com REST,
* Assegurar que o delivery se limite aos requisitos específicos,
* Permitindo o delivery em massa do que é necessário para renderização como resposta a um único query de API.

## A API GraphQL {#graphql-api}

*&quot;O GraphQL é uma linguagem e especificação de query de dados desenvolvida internamente pelo Facebook em 2012 antes de ser publicamente aberto e ter origem em 2015. Fornece uma alternativa às arquiteturas baseadas em REST com o objetivo de aumentar a produtividade do desenvolvedor e minimizar a quantidade de dados transferidos. O GraphQL é usado na produção por centenas de organizações de todos os tamanhos...&quot;* Consulte [GraphQL Foundation](https://foundation.graphql.org/).

Para obter mais informações sobre a API do GraphQL, consulte as seguintes seções (entre muitos outros recursos):

* Em [grafql.org](https://graphql.org):

   * [Introdução ao GraphQL](https://graphql.org/learn)

   * [A especificação do GraphQL](http://spec.graphql.org/)

* Em [grafql.com](https://graphql.com):

   * [Guias](https://www.graphql.com/guides/)

   * [Tutoriais](https://www.graphql.com/tutorials/)

   * [Estudos de caso](https://www.graphql.com/case-studies/)

A implementação do GraphQL para AEM se baseia na Biblioteca padrão do GraphQL Java. Consulte:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GraphQL Java no GitHub](https://github.com/graphql-java)

## Interface GraphiQL {#graphiql-interface}

AEM API de gráfico inclui uma implementação da interface padrão [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql). Isso permite inserir e testar diretamente query.

Por exemplo:

* `http://localhost:4502/content/graphiql.html`

Isso fornece recursos como realce de sintaxe, preenchimento automático, sugestão automática, juntamente com um histórico e documentação online:

![Interface GraphiQL ](assets/cfm-graphiql-interface.png "Interface GraphiQL")

## Casos de uso para Ambientes de autor e publicação {#use-cases-author-publish-environments}

Os casos de uso podem depender do tipo de AEM como um ambiente Cloud Service:

* Ambiente de publicação; usado para:
   * Dados do query para o aplicativo JS (caso de uso padrão)

* Ambiente do autor; usado para:
   * Dados do query para &quot;fins de gestão de conteúdo&quot;:
      * O GraphQL no AEM como Cloud Service é atualmente uma API somente leitura.
      * A REST API pode ser usada para operações de CR(u)D.

## Geração de schema {#schema-generation}

O GraphQL é uma API fortemente tipada, o que significa que os dados devem ser claramente estruturados e organizados por tipo.

A especificação GraphQL fornece uma série de diretrizes sobre como criar uma API robusta para interrogar dados em uma determinada instância. Para fazer isso, um cliente precisa buscar o [Schema](#schema-generation), que contém todos os tipos necessários para um query.

Para Fragmentos de conteúdo, os schemas GraphQL (estrutura e tipos) são baseados em [Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) e seus tipos de dados.

Por exemplo, se um usuário criou um Modelo de fragmento de conteúdo chamado `Article`, AEM gera o objeto `article` que é do tipo `ArticleModel`. Os campos nesse tipo correspondem aos campos e aos tipos de dados definidos no modelo.

1. Um modelo de fragmento de conteúdo:

   ![Modelo de fragmento de conteúdo para uso com ](assets/cfm-graphqlapi-01.png "GraphQLContent Fragment Model para uso com GraphQL")

1. O schema GraphQL correspondente (saída da documentação automática do GraphiQL):
   ![Schema GraphQL com base no ](assets/cfm-graphqlapi-02.png "Modelo de fragmento do conteúdoSchema GraphQL com base no Modelo de fragmento do conteúdo")

   Isso mostra que o tipo gerado `ArticleModel` contém vários [campos](#fields).

   * Três deles foram controlados pelo usuário: `author`, `main` e `linked_article`.

   * Os outros campos foram adicionados automaticamente por AEM e representam métodos úteis para fornecer informações sobre um determinado Fragmento do conteúdo; neste exemplo, `_path`, `_metadata`, `_variations`. Esses [campos auxiliares](#helper-fields) são marcados com um `_` anterior para distinguir entre o que foi definido pelo usuário e o que foi gerado automaticamente.

1. Depois que um usuário cria um Fragmento de conteúdo com base no modelo de artigo, ele pode ser interrogado pelo GraphQL. Para obter exemplos, consulte [Query de amostra](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (com base em uma [estrutura de fragmento de conteúdo de amostra para uso com GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

No GraphQL para AEM, o schema é flexível. Isso significa que ele é gerado automaticamente cada vez que um Modelo de fragmento de conteúdo é criado, atualizado ou excluído. Os caches de schema de dados também são atualizados quando você atualiza um Modelo de fragmento de conteúdo.

O serviço Sites GraphQL escuta (em segundo plano) quaisquer modificações feitas em um Modelo de fragmento de conteúdo. Quando as atualizações são detectadas, apenas a parte do schema é regenerada. Essa otimização economiza tempo e proporciona estabilidade.

Por exemplo, se você:

1. Instale um pacote contendo `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. Os tipos GraphQL para `Model-1` e `Model-2` serão gerados.

1. Em seguida, modifique `Content-Fragment-Model-2`:

   1. Somente o tipo GraphQL `Model-2` será atualizado.

   1. Enquanto `Model-1` permanecerá o mesmo.

>[!NOTE]
>
>Isso é importante para observar caso deseje fazer atualizações em massa nos Modelos de fragmento de conteúdo por meio da API REST ou de outra forma.

O schema é servido pelo mesmo terminal dos query GraphQL, com o cliente lidando com o fato de que o schema é chamado com a extensão `GQLschema`. Por exemplo, a execução de uma solicitação `GET` simples em `/content/graphql/endpoint.GQLschema` resultará na saída do schema com o Tipo de conteúdo: `text/x-graphql-schema;charset=iso-8859-1`.

## Fields {#fields}

Dentro do schema há campos individuais, de duas categorias básicas:

* Campos que você gera.

   Uma seleção de [Tipos de campo](#field-types) é usada para criar campos com base em como você configura o Modelo de fragmento de conteúdo. Os nomes dos campos são obtidos do campo **Nome da propriedade** do **Tipo de dados**.

   * Há também a propriedade **Renderizar como** a ser considerada, pois os usuários podem configurar certos tipos de dados; por exemplo, como um texto de linha única ou vários campos.

* O GraphQL para AEM também gera vários [campos auxiliares](#helper-fields).

   Eles são usados para identificar um Fragmento de conteúdo ou para obter mais informações sobre um fragmento de conteúdo.

### Tipos de campo {#field-types}

O GraphQL para AEM suporta uma lista de tipos. Todos os tipos de dados do modelo de fragmento de conteúdo suportados e os tipos GraphQL correspondentes são representados:

| Modelo de fragmento de conteúdo - Tipo de dados | Tipo GraphQL | Descrição |
|--- |--- |--- |
| Texto em linha única | String, [String] |  Usado para strings simples, como nomes de autor, nomes de localização etc |
| Texto de várias linhas | Sequência de caracteres |  Usado para texto de saída, como o corpo de um artigo |
| Número |  Flutuante, [Flutuante] | Usado para exibir números de ponto flutuante e números regulares |
| Booleano |  Booleano |  Usado para exibir caixas de seleção → declarações simples verdadeiras/falsas |
| Data E Hora | Calendário |  Usado para exibir a data e a hora em um formato ISO 8086 |
| Enumeração |  Sequência de caracteres |  Usado para exibir uma opção de uma lista de opções definidas na criação do modelo |
|  Tags |  [Sequência de caracteres] |  Usado para exibir uma lista de strings que representam tags usadas em AEM |
| Referência de conteúdo |  Sequência de caracteres |  Usado para exibir o caminho para outro ativo no AEM |
| Referência do fragmento |  *Um tipo de modelo* |  Usado para fazer referência a outro Fragmento de conteúdo de um tipo de modelo específico, definido quando o modelo foi criado |

### Campos de ajuda {#helper-fields}

Além dos tipos de dados para campos gerados pelo usuário, o GraphQL para AEM também gera vários campos *helper* para ajudar a identificar um Fragmento de conteúdo ou fornecer informações adicionais sobre um Fragmento de conteúdo.

#### Caminho {#path}

O campo path é usado como um identificador no GraphQL. Representa o caminho do ativo de Fragmento de conteúdo dentro do repositório AEM. Optamos por isso como o identificador de um fragmento de conteúdo, pois ele:

* é único em AEM,
* podem ser facilmente buscados.

O código a seguir exibirá os caminhos de todos os Fragmentos de conteúdo criados com base no Modelo de fragmento de conteúdo `Person`.

```xml
{
  persons {
    items {
      _path
    }
  }
}
```

Para recuperar um único Fragmento de conteúdo de um tipo específico, também é necessário determinar seu caminho primeiro. por exemplo:

```xml
{
    person(_path="/content/dam/path/to/fragment/john-doe") {
        _path
        name
        first-name
    }
}
```

Consulte [Query de amostra - Um fragmento de cidade única](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-city-fragment).

#### Metadados {#metadata}

Por meio do GraphQL, AEM também expõe os metadados de um Fragmento do conteúdo. Metadados são as informações que descrevem um fragmento de conteúdo, como o título de um fragmento de conteúdo, o caminho de miniatura, a descrição de um Fragmento de conteúdo, a data em que foi criado, entre outros.

Como os Metadados são gerados pelo Editor de Schemas e, como tal, não têm uma estrutura específica, o tipo `TypedMetaData` GraphQL foi implementado para expor os metadados de um Fragmento de conteúdo. `TypedMetaData` expõe as informações agrupadas pelos seguintes tipos escalares:

| Texto |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!`  |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Cada tipo escalar representa um único par nome-valor ou uma matriz de pares nome-valor, em que o valor desse par é do tipo em que foi agrupado.

Por exemplo, se você deseja recuperar o título de um Fragmento de conteúdo, sabemos que essa propriedade é uma propriedade String, portanto, faremos query para todos os Metadados de string:

Para query de metadados:

```xml
{
  person(_path: "/content/dam/path/to/fragment/john-doe") {
    _path
    _metadata {
      stringMetadata {
        name
        value
      }
    }
  }
}
```

É possível visualização todos os tipos de metadados GraphQL se você visualização o schema GraphQL gerado. Todos os tipos de modelo têm o mesmo `TypedMetaData`.

>[!NOTE]
>
>**Diferença entre metadados normais e de matriz**
>Lembre-se de que `StringMetadata` e `StringArrayMetadata` ambos referem-se ao que está armazenado no repositório, e não a como recuperá-los.
>
>Por exemplo, ao chamar o campo `stringMetadata`, você receberá uma matriz de todos os metadados armazenados no repositório como `String` e, se você chamar `stringArrayMetadata`, receberá uma matriz de todos os metadados armazenados no repositório como `String[]`.

Consulte [Query de amostra para Metadados - Lista dos Metadados para Prêmios GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

#### Variações {#variations}

O campo `_variations` foi implementado para simplificar a consulta das variações que um Fragmento de conteúdo possui. Por exemplo:

```xml
{
  person(_path: "/content/dam/path/to/fragment/john-doe") {
    _variations
  }
}
```

Consulte [Query de amostra - Todas as cidades com uma Variação nomeada](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## Variáveis GraphQL {#graphql-variables}

O GraphQL permite que as variáveis sejam colocadas no query. Para obter mais informações, consulte a documentação do [GraphQL para GraphiQL](https://graphql.org/learn/queries/#variables).

Por exemplo, para obter todos os Fragmentos de conteúdo do tipo `Article` que têm uma variação específica, você pode especificar a variável `variation` no GraphiQL:

![Variáveis GraphQL](assets/cfm-graphqlapi-03.png "Variáveis GraphQL")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articles(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## Diretivas GraphQL {#graphql-directives}

No GraphQL, há uma possibilidade de alterar o query com base em variáveis, chamadas de diretivas GraphQL.

Por exemplo, é possível incluir o campo `adventurePrice` em um query para todos os `AdventureModels`, com base em uma variável `includePrice`.

![Diretivas GraphQL](assets/cfm-graphqlapi-04.png "Diretivas GraphQL")

```xml
query getAdventureByType($includePrice: Boolean!) {
  adventures {
    items {
      adventureType
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## Query Persistentes (Cache) {#persisted-queries-caching}

Depois de preparar um query com uma solicitação de POST, ele pode ser executado com uma solicitação de GET que pode ser armazenada em cache por caches HTTP ou um CDN.

Isso é necessário porque os query POST geralmente não são armazenados em cache e, se estiver usando o GET como parâmetro, há um risco significativo de o parâmetro se tornar grande demais para os serviços HTTP e os intermediários.

Estas são as etapas necessárias para persistir um determinado query:

>[!NOTE]
>Antes disso, os **Query de persistência GraphQL** precisam ser ativados para a configuração apropriada. Consulte [Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) para obter mais detalhes.

1. Prepare o query colocando-o no novo URL de ponto de extremidade `/graphql/persist.json/<config>/<persisted-label>`.

   Por exemplo, crie um query persistente:

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

1. Nesse ponto, verifique a resposta.

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

1. Você pode reproduzir o query persistente ao GETing o URL `/graphql/execute.json/<shortPath>`.

   Por exemplo, use o query persistente:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Atualize um query persistente ao executar o POST para um caminho de query já existente.

   Por exemplo, use o query persistente:

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

1. Crie um query simples encapsulado.

   Por exemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Crie um query simples encapsulado com controle de cache.

   Por exemplo:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Crie um query persistente com parâmetros:

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

1. Execução de um query com parâmetros.

   Por exemplo:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. Para executar o query na publicação, a árvore persistente relacionada precisa ser replicada

   * Usando um POST para replicação:

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * Uso de um pacote:
      1. Criar uma nova definição de pacote.
      1. Inclua a configuração (por exemplo, `/conf/wknd/settings/graphql/persistentQueries`).
      1. Crie o pacote.
      1. Replicar o pacote.
   * Usando a ferramenta de replicação/distribuição.
      1. Vá para a ferramenta Distribuição.
      1. Selecione a ativação em árvore para a configuração (por exemplo, `/conf/wknd/settings/graphql/persistentQueries`).
   * Usando um fluxo de trabalho (por meio da configuração do iniciador do fluxo de trabalho):
      1. Defina uma regra de inicializador de fluxo de trabalho para executar um modelo de fluxo de trabalho que replicaria a configuração em eventos diferentes (por exemplo, criar, modificar, entre outros).



1. Quando a configuração do query estiver ativada, os mesmos princípios se aplicam, usando apenas o ponto de extremidade de publicação.

   >[!NOTE]
   >
   >Para acesso anônimo, o sistema pressupõe que a ACL permita que &quot;todos&quot; tenham acesso à configuração do query.
   >
   >Se esse não for o caso, ele não poderá ser executado.

   >[!NOTE]
   >
   >Qualquer ponto-e-vírgula (&quot;;&quot;) nos URLs precisa ser codificado.
   >
   >Por exemplo, como na solicitação para Executar um query persistente:
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## Consultando o ponto de extremidade GraphQL de um site externo {#query-graphql-endpoint-from-external-website}

>[!NOTE]
>
>Para obter uma visão geral detalhada da política de compartilhamento de recursos do CORS em AEM, consulte [Entender o compartilhamento de recursos entre Origens (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors)).

Para permitir que um site de terceiros consuma saída JSON, uma política CORS deve ser configurada no repositório Git do cliente. Isso é feito adicionando um arquivo de configuração OSGi CORS apropriado para o terminal desejado. Essa configuração deve especificar um nome de site (ou regex) confiável para o qual o acesso deve ser concedido.

* Acessar o ponto de extremidade GraphQL:

   * alopirina: [o seu domínio] ou aloworiginregexp: [seu regex de domínio]
   * supported methods: [POST]
   * caminhos permitidos: [&quot;/apps/graphql-enablement/content/endpoint.gql(/persistente)?&quot;]

* Acessar o ponto de extremidade de query persistentes do GraphQL:

   * alopirina: [o seu domínio] ou aloworiginregexp: [seu regex de domínio]
   * supported methods: [GET]
   * caminhos permitidos: [&quot;/graphql/execute.json/.*&quot;]

>[!CAUTION]
>
>O cliente continua sendo responsável por:
>
>* conceder acesso somente a domínios confiáveis
>* não use uma sintaxe curinga [*]; que exporá os pontos finais do GraphQL ao mundo inteiro.



## Filtragem {#filtering}

Você também pode usar a filtragem em seus query GraphQL para retornar dados específicos.

A filtragem usa uma sintaxe com base em operadores lógicos e expressões.

Para obter exemplos, consulte:

* detalhes do [GraphQL para extensões AEM](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-some-extensions)

* [Conteúdo de amostra e ](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) estrutura preparados para uso em query de amostra

* [Query de amostra usando este conteúdo de amostra e estrutura](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

* [Query de amostra baseados no projeto WKND](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## Permissões  {#permission}

As permissões são aquelas necessárias para acessar os Ativos.

<!-- to be addressed later -->

<!-- 
## Authentication {#authentication}
-->

<!-- to be addressed later -->

<!-- 
## Caching {#caching}
-->

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## Pontos finais {#end-points}

O terminal é o caminho usado para acessar o GraphQL para AEM. Usando esse caminho você (ou seu aplicativo) pode:

* acessar o schema GraphQL,
* envie seus query GraphQL,
* receba as respostas (para seus query GraphQL).

Para ter acesso aos servlets GraphQL no AEM é necessário configurar um terminal. Isso também inclui duas configurações OSGi.

1. O servlet de schema Sling que responde às solicitações para recuperar o schema GraphQL:

   ![Servlet de Schema AEM Sites GraphQL](assets/cfm-endpoint-01.png)

   * **Seletores** (`sling.servlet.selectors`) devem ser deixados em branco.

   * **Tipos**  de recursos(`sling.servlet.resourceTypes`) Defina o tipo de recurso que o servlet GraphQL deve escutar.
Por exemplo:
      `graphql-enablement/components/endpoint`.

   * **Métodos** (`sling.servlet.methods^)

      O método HTTP que o servlet deve ouvir; geralmente `GET`.

   * **Extensões** (`sling.servlet.extensions`)

      Especifique a extensão à qual o Servlet de Schema deve responder. Nesse caso, é `GQLschema`, para ser compatível com as especificações GraphQL.

2. O servlet que responde às solicitações gráficas:

   ![Apache Sling GraphQL Servlet](assets/cfm-endpoint-02.png)

   * **Seletores** (`sling.servlet.selectors`) devem ser deixados em branco.

   * **Tipo** (`sling.servlet.resourceTypes`) de recurso O tipo de recurso ao qual o servlet GraphQL deve responder.
Por exemplo, `graphql-enablement/components/endpoint`.

   * **Métodos** (`sling.servlet.methods`) Os métodos HTTP aos quais o servlet GraphQL deve responder, normalmente  `GET` e  `POST`.

   * **Extensões** (`sling.servlet.extensions`) A extensão para acompanhar solicitações GraphQL, normalmente  `gql`.

3. Agora é necessário criar um terminal - um nó do sling:resourceType definido nessas configurações.
Por exemplo, para criar um terminal para recuperar o Schema GraphQL, crie um novo nó em `/apps/<my-site>/graphql`:

   * Nome: `endpoint`
   * Tipo principal: `nt:unstructured`
   * sling:resourceType: `graphql-enablement/components/endpoint`

## Perguntas frequentes {#faqs}

Questões levantadas:

1. **P**: &quot;*Como a API do GraphQL para AEM é diferente da API do Construtor de Query?*&quot;

   * **A**: &quot;*A API AEM GraphQL oferta o controle total na saída JSON e é um padrão do setor para consulta de conteúdo.
A partir de agora, AEM planeja investir na API AEM GraphQL.*&quot;

## Tutorial - Introdução ao AEM sem cabeçalho e ao GraphQL {#tutorial}

Procurando um tutorial prático? Consulte [Introdução com AEM GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) tutorial completo ilustrando como criar e expor conteúdo usando as APIs GraphQL da AEM e consumidas por um aplicativo externo, em um cenário CMS sem cabeçalho.