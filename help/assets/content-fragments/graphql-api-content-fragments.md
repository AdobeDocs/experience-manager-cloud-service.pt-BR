---
title: AEM API GraphQL para uso com Fragmentos de conteúdo
description: Saiba como usar Fragmentos de conteúdo no Adobe Experience Manager (AEM) como um Cloud Service com a API AEM GraphQL para o Delivery de conteúdo sem cabeçalho.
translation-type: tm+mt
source-git-commit: 20f90d46d24fa211d51ef4b59bb56f4b9f963bc3
workflow-type: tm+mt
source-wordcount: '3167'
ht-degree: 1%

---


# AEM API GraphQL para uso com Fragmentos de conteúdo {#graphql-api-for-use-with-content-fragments}

A API Adobe Experience Manager como Cloud Service (AEM) GraphQL usada com Fragmentos de conteúdo é altamente baseada na API GraphQL de código aberto e padrão.

Usar a API GraphQL no AEM permite o delivery eficiente dos Fragmentos de conteúdo para clientes JavaScript em implementações CMS sem cabeçalho:

* Evitar solicitações iterativas de API como com REST,
* Assegurar que o delivery se limite aos requisitos específicos,
* Permitindo o delivery em massa do que é necessário para renderização como resposta a um único query de API.

## A API GraphQL {#graphql-api}

GraphQL é:

* &quot;*...um idioma de query para APIs e um tempo de execução para realizar esses query com seus dados existentes. O GraphQL fornece uma descrição completa e compreensível dos dados em sua API, fornece aos clientes o poder de solicitar exatamente o que eles precisam e nada mais, facilita a evolução das APIs ao longo do tempo e habilita poderosas ferramentas de desenvolvedor.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

* &quot;*...uma especificação aberta para uma camada de API flexível. Coloque o GraphQL sobre seus backends existentes para criar produtos mais rápido do que nunca....*&quot;.

   Consulte [Explorar GraphQL](https://www.graphql.com).

* *&quot;...uma linguagem e especificação de query de dados desenvolvida internamente pelo Facebook em 2012 antes de ser publicamente disponível em 2015. Fornece uma alternativa às arquiteturas baseadas em REST com o objetivo de aumentar a produtividade do desenvolvedor e minimizar a quantidade de dados transferidos. O GraphQL é usado na produção por centenas de organizações de todos os tamanhos...&quot;*

   Consulte [GraphQL Foundation](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

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

### Terminologia GraphQL {#graphql-terminology}

O GraphQL usa o seguinte:

* **[Query](https://graphql.org/learn/queries/)**

* **[Schemas e tipos](https://graphql.org/learn/schema/)**:

   * Schemas são gerados por AEM com base nos Modelos de fragmento de conteúdo.
   * Usando seus schemas, o GraphQL apresenta os tipos e as operações permitidas para o GraphQL para AEM implementação.

* **[Campos](https://graphql.org/learn/queries/#fields)**

* **[Endpoint GraphQL](#graphql-aem-endpoint)**
   * O caminho no AEM que responde aos query GraphQL e fornece acesso aos schemas GraphQL.

   * Consulte [Habilitando seu Ponto Final GraphQL](#enabling-graphql-endpoint) para obter mais detalhes.

Consulte a [(GraphQL.org) Introduction to GraphQL](https://graphql.org/learn/) para obter detalhes abrangentes, incluindo as [Práticas recomendadas](https://graphql.org/learn/best-practices/).

### Tipos de Query GraphQL {#graphql-query-types}

Com o GraphQL, é possível executar query para retornar:

* Uma **entrada única**

* Uma **[lista de entradas](https://graphql.org/learn/schema/#lists-and-non-null)**

Você também pode executar:

* [Query persistentes em cache](#persisted-queries-caching)

## O GraphQL para AEM Endpoint {#graphql-aem-endpoint}

O terminal é o caminho usado para acessar o GraphQL para AEM. Usando esse caminho você (ou seu aplicativo) pode:

* acessar o schema GraphQL,
* envie seus query GraphQL,
* receba as respostas (para seus query GraphQL).

O caminho do repositório do GraphQL para AEM endpoint é:

`/content/cq:graphql/global/endpoint`

Seu aplicativo pode usar o seguinte caminho no URL da solicitação:

`/content/_cq_graphql/global/endpoint.json`

Para habilitar o ponto de extremidade do GraphQL para AEM é necessário:

>[!CAUTION]
>
>Essas etapas poderão mudar em breve.

* [Ativar seu Ponto Final GraphQL](#enabling-graphql-endpoint)
* [Execute configurações adicionais](#additional-configurations-graphql-endpoint)

### Habilitando seu Ponto Final GraphQL {#enabling-graphql-endpoint}

>[!NOTE]
>
>Consulte [Supporting Packages](#supporting-packages) para obter detalhes dos pacotes que o Adobe fornece para ajudar a simplificar essas etapas.

Para habilitar query GraphQL em AEM, crie um terminal em `/content/cq:graphql/global/endpoint`:

* Os nós `cq:graphql` e `global` devem ser do tipo `sling:Folder`.
* O nó `endpoint` deve ser do tipo `nt:unstructured` e conter um `sling:resourceType` de `graphql/sites/components/endpoint`.

>[!CAUTION]
>
>Atualmente, há um problema conhecido com o endpoint:
>
>* A entrada `cq:graphql` é vista no console **Sites**; no nível superior.
   >  Isto não deve ser utilizado.


>[!CAUTION]
>
>O terminal é acessível a todos. Isso pode - especialmente em instâncias de publicação - causar problemas de segurança, já que os query GraphQL podem impor uma carga pesada no servidor.
>
>Você pode configurar ACLs, apropriadas ao caso de uso, no terminal.

>[!NOTE]
>
>Seu terminal não funcionará prontamente. Você terá que fornecer [Configurações adicionais para o Endpoint do GraphQL](#additional-configurations-graphql-endpoint) separadamente.

>[!NOTE]
>Além disso, você pode testar e depurar query GraphQL usando o [GraphiQL IDE](#graphiql-interface).

### Configurações adicionais para o Ponto Final GraphQL {#additional-configurations-graphql-endpoint}

>[!NOTE]
>
>Consulte [Supporting Packages](#supporting-packages) para obter detalhes dos pacotes que o Adobe fornece para ajudar a simplificar essas etapas.

Configurações adicionais são necessárias:

* Dispatcher:
   * Para permitir URLs necessários
   * Obrigatório
* URL personalizada:
   * Para alocar um URL simplificado para o ponto final
   * Opcional
* Configuração do OSGi:
   * Configuração do Servlet GraphQL:
      * Processa solicitações ao ponto de extremidade
      * O nome da configuração é `org.apache.sling.graphql.core.GraphQLServlet`. Deve ser fornecida como uma configuração de fábrica OSGi
      * `sling.servlet.extensions` deve ser definido como  `[json]`
      * `sling.servlet.methods` deve ser definido como  `[GET,POST]`
      * `sling.servlet.resourceTypes` deve ser definido como  `[graphql/sites/components/endpoint]`
      * Obrigatório
   * Configuração do Servlet de schema:
      * Cria o schema GraphQL
      * O nome da configuração é `com.adobe.aem.graphql.sites.adapters.SlingSchemaServlet`. Deve ser fornecida como uma configuração de fábrica OSGi
      * `sling.servlet.extensions` deve ser definido como  `[GQLschema]`
      * `sling.servlet.methods` deve ser definido como  `[GET]`
      * `sling.servlet.resourceTypes` deve ser definido como  `[graphql/sites/components/endpoint]`
      * Obrigatório
   * Configuração do CSRF:
      * Proteção de segurança para o terminal
      * O nome da configuração é `com.adobe.granite.csrf.impl.CSRFFilter`
      * Adicionar `/content/cq:graphql/global/endpoint` à lista existente de caminhos excluídos (`filter.excluded.paths`)
      * Obrigatório

### Pacotes de suporte {#supporting-packages}

Para simplificar a configuração de um endpoint GraphQL, o Adobe fornece o pacote [Projeto de amostra GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-sample.zip).

Este arquivo contém [as configurações adicionais necessárias](#additional-configurations-graphql-endpoint) e [o endpoint do GraphQL](#enabling-graphql-endpoint). Se instalado em uma instância AEM simples, exporá um ponto final GraphQL totalmente funcional em `/content/cq:graphql/global/endpoint`.

Este pacote deve ser um projeto para seus próprios projetos do GraphQL. Consulte o pacote **README** para obter detalhes sobre como usar o pacote.

Se você preferir criar manualmente a configuração necessária, o Adobe também fornecerá um [Pacote de conteúdo do GraphQL Endpoint](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-global-endpoint.zip) dedicado. Este pacote de conteúdo contém apenas o endpoint GraphQL, sem qualquer configuração.

## Interface GraphiQL {#graphiql-interface}

<!--
AEM Graph API includes an implementation of the standard [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) interface. This allows you to directly input, and test, queries.
-->

Uma implementação da interface padrão [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) está disponível para uso com AEM GraphQL. Pode ser [instalado com AEM](#installing-graphiql-interface).

Essa interface permite inserir e testar diretamente query.

Por exemplo:

* `http://localhost:4502/content/graphiql.html`

Isso fornece recursos como realce de sintaxe, preenchimento automático, sugestão automática, juntamente com um histórico e documentação online:

![Interface GraphiQL ](assets/cfm-graphiql-interface.png "Interface GraphiQL")

### Instalando a interface AEM GraphiQL {#installing-graphiql-interface}

A interface do usuário do GraphiQL pode ser instalada em AEM com um pacote dedicado: o pacote [GraphiQL Content Package v0.0.4](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphiql-0.0.4.zip).

<!--
See the package **README** for full details; including full details of how it can be installed on an AEM instance - in a variety of scenarios.
-->

## Casos de uso para Ambientes de autor e publicação {#use-cases-author-publish-environments}

Os casos de uso podem depender do tipo de AEM como um ambiente Cloud Service:

* Ambiente de publicação; usado para:
   * Dados do query para o aplicativo JS (caso de uso padrão)

* Ambiente do autor; usado para:
   * Dados do query para &quot;fins de gestão de conteúdo&quot;:
      * O GraphQL no AEM como Cloud Service é atualmente uma API somente leitura.
      * A REST API pode ser usada para operações de CR(u)D.

## Permissões  {#permission}

As permissões são aquelas necessárias para acessar os Ativos.

## Geração de schema {#schema-generation}

O GraphQL é uma API fortemente tipada, o que significa que os dados devem ser claramente estruturados e organizados por tipo.

A especificação GraphQL fornece uma série de diretrizes sobre como criar uma API robusta para interrogar dados em uma determinada instância. Para fazer isso, um cliente precisa buscar o [Schema](#schema-generation), que contém todos os tipos necessários para um query.

Para Fragmentos de conteúdo, os schemas GraphQL (estrutura e tipos) são baseados em **Enabled** [Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) e seus tipos de dados.

>[!CAUTION]
>
>Todos os schemas GraphQL (derivados dos Modelos de fragmento do conteúdo que foram **Ativados**) podem ser lidos pelo endpoint GraphQL.
>
>Isto significa que é necessário garantir que não existem dados sensíveis disponíveis, uma vez que podem ser vazados desta forma; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.

Por exemplo, se um usuário criou um Modelo de fragmento de conteúdo chamado `Article`, AEM gera o objeto `article` que é do tipo `ArticleModel`. Os campos nesse tipo correspondem aos campos e aos tipos de dados definidos no modelo.

1. Um modelo de fragmento de conteúdo:

   ![Modelo de fragmento de conteúdo para uso com ](assets/cfm-graphqlapi-01.png "GraphQLContent Fragment Model para uso com GraphQL")

1. O schema GraphQL correspondente (saída da documentação automática do GraphiQL):
   ![Schema GraphQL com base no ](assets/cfm-graphqlapi-02.png "Modelo de fragmento do conteúdoSchema GraphQL com base no Modelo de fragmento do conteúdo")

   Isso mostra que o tipo gerado `ArticleModel` contém vários [campos](#fields).

   * Três deles foram controlados pelo usuário: `author`, `main` e `referencearticle`.

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

O schema é servido pelo mesmo terminal dos query GraphQL, com o cliente lidando com o fato de que o schema é chamado com a extensão `GQLschema`. Por exemplo, a execução de uma solicitação `GET` simples em `/content/cq:graphql/global/endpoint.GQLschema` resultará na saída do schema com o Tipo de conteúdo: `text/x-graphql-schema;charset=iso-8859-1`.

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
  personList {
    items {
      _path
    }
  }
}
```

Para recuperar um único Fragmento de conteúdo de um tipo específico, também é necessário determinar seu caminho primeiro. por exemplo:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

Consulte [Query de amostra - Um único fragmento de cidade específico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

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
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
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
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Consulte [Query de amostra - Todas as cidades com uma Variação nomeada](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## Variáveis GraphQL {#graphql-variables}

O GraphQL permite que as variáveis sejam colocadas no query. Para obter mais informações, consulte a documentação do [GraphQL para GraphiQL](https://graphql.org/learn/queries/#variables).

Por exemplo, para obter todos os Fragmentos de conteúdo do tipo `Article` que têm uma variação específica, você pode especificar a variável `variation` no GraphiQL.

![Variáveis GraphQL](assets/cfm-graphqlapi-03.png "Variáveis GraphQL")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
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
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## Filtragem {#filtering}

Você também pode usar a filtragem em seus query GraphQL para retornar dados específicos.

A filtragem usa uma sintaxe com base em operadores lógicos e expressões.

Por exemplo, o seguinte query (básico) filtros todas as pessoas que têm um nome de `Jobs` ou `Smith`:

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

Para obter mais exemplos, consulte:

* detalhes do [GraphQL para extensões AEM](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-extensions)

* [Query de amostra usando este conteúdo de amostra e estrutura](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * E o [Amostra de conteúdo e estrutura](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) preparado para uso em query de amostra

* [Query de amostra baseados no projeto WKND](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

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
   * caminhos permitidos: [&quot;/content/graphql/global/endpoint.json&quot;]

* Acessar o ponto de extremidade de query persistentes do GraphQL:

   * alopirina: [o seu domínio] ou aloworiginregexp: [seu regex de domínio]
   * supported methods: [GET]
   * caminhos permitidos: [&quot;/graphql/execute.json/.*&quot;]

>[!CAUTION]
>
>O cliente continua sendo responsável por:
>
>* conceder acesso somente a domínios confiáveis
>* certifique-se de que nenhuma informação confidencial seja exposta
>* não use uma sintaxe curinga [*]; isso desativará o acesso autenticado ao endpoint GraphQL e também o exporá ao mundo inteiro.


>[!CAUTION]
>
>Todos os schemas GraphQL [](#schema-generation) (derivados de Modelos de fragmento de conteúdo que foram **Ativados**) podem ser lidos pelo endpoint GraphQL.
>
>Isto significa que é necessário garantir que não existem dados sensíveis disponíveis, uma vez que podem ser vazados desta forma; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.

## Autenticação {#authentication}

Consulte [Autenticação para Query GraphQL de AEM Remotos em Fragmentos de Conteúdo](/help/assets/content-fragments/graphql-authentication-content-fragments.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## Perguntas frequentes {#faqs}

Questões levantadas:

1. **P**: &quot;*Como a API do GraphQL para AEM é diferente da API do Construtor de Query?*&quot;

   * **A**: &quot;*A API AEM GraphQL oferta o controle total na saída JSON e é um padrão do setor para consulta de conteúdo.
A partir de agora, AEM planeja investir na API AEM GraphQL.*&quot;

## Tutorial - Introdução ao AEM sem cabeçalho e ao GraphQL {#tutorial}

Procurando um tutorial prático? Consulte [Introdução com AEM GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) tutorial completo ilustrando como criar e expor conteúdo usando as APIs GraphQL da AEM e consumidas por um aplicativo externo, em um cenário CMS sem cabeçalho.
