---
title: Aprendendo a usar o GraphQL com AEM - Conteúdo de amostra e Query
description: Aprendendo a usar o GraphQL com AEM - Conteúdo de amostra e Query.
translation-type: tm+mt
source-git-commit: 6a60238b13d66ea2705063670295a62e3cbf6255
workflow-type: tm+mt
source-wordcount: '1707'
ht-degree: 5%

---


# Aprendendo a usar o GraphQL com AEM - Conteúdo de amostra e Query {#learn-graphql-with-aem-sample-content-queries}

>[!NOTE]
>
>Esta página deve ser lida juntamente com:
>
>* [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
>* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
>* [AEM API GraphQL para uso com Fragmentos de conteúdo](/help/assets/content-fragments/graphql-api-content-fragments.md)


Para começar a usar query GraphQL e como eles trabalham com AEM Fragmentos de conteúdo, é útil ver alguns exemplos práticos.

Para ajudar com isso, consulte:

* Uma [amostra da estrutura do fragmento de conteúdo](#content-fragment-structure-graphql)

* E alguns [query GraphQL de amostra](#graphql-sample-queries), com base na estrutura do fragmento de conteúdo de amostra (Modelos de fragmento de conteúdo e Fragmentos de conteúdo relacionados).

## GraphQL para AEM - Resumo das extensões {#graphql-extensions}

A operação básica de query com GraphQL para AEM obedece à especificação GraphQL padrão. Para query GraphQL com AEM há algumas extensões:

* Se você precisar de um único resultado:
   * Utilizar o nome do modelo; cidade eg

* Se você espera uma lista de resultados:
   * adicione `List` ao nome do modelo; por exemplo, `cityList`
   * Consulte [Query de amostra - Todas as informações sobre todas as cidades](#sample-all-information-all-cities)

* Se quiser usar um OU lógico:
   * use ` _logOp: OR`
   * Consulte [Query de amostra - Todas as pessoas que têm o nome &quot;Jobs&quot; ou &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* E lógico também existe, mas é (muitas vezes) implícito

* Você pode query em nomes de campos que correspondam aos campos no Modelo de fragmento de conteúdo
   * Consulte [Query de amostra - Detalhes completos de um CEO e Funcionários da Empresa](#sample-full-details-company-ceos-employees)

* Além dos campos do modelo, há alguns campos gerados pelo sistema (precedidos por sublinhado):

   * Para conteúdo:

      * `_locale` : revelar a língua; com base no Gerenciador de idiomas
         * Consulte [Query de amostra para vários Fragmentos de conteúdo de uma determinada localidade](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : para revelar metadados para o fragmento
         * Consulte [Query de amostra para Metadados - Lista dos Metadados para Prêmios GB](#sample-metadata-awards-gb)
      * `_model` : permitir consulta para um Modelo de fragmento de conteúdo (caminho e título)
         * Consulte [Query de amostra para um Modelo de fragmento de conteúdo de um Modelo](#sample-wknd-content-fragment-model-from-model)
      * `_path` : o caminho para o fragmento do conteúdo no repositório
         * Consulte [Query de amostra - Um único fragmento de cidade específico](#sample-single-specific-city-fragment)
      * `_reference` : revelar referências; incluindo referências em linha no Editor de Rich Text
         * Consulte [Query de amostra para vários fragmentos de conteúdo com referências pré-definidas](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : para revelar variações específicas em seu fragmento de conteúdo
         * Consulte [Query de amostra - Todas as cidades com uma Variação nomeada](#sample-cities-named-variation)
   * E operações:

      * `_operator` : Aplicar operadores específicos;  `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`
         * Consulte [Query de amostra - Todas as pessoas que não têm o nome de &quot;Tarefas&quot;](#sample-all-persons-not-jobs)
      * `_apply` : Aplicar condições específicas; por exemplo,   `AT_LEAST_ONCE`
         * Consulte [Query de amostra - Filtrar em uma matriz com um item que deve ocorrer pelo menos uma vez](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : para ignorar o caso ao consultar
         * Consulte [Query de amostra - Todas as cidades com SAN no nome, independentemente de maiúsculas e minúsculas](#sample-all-cities-san-ignore-case)









* Os tipos de união GraphQL são suportados:

   * use `... on`
      * Consulte [Query de amostra para obter um fragmento de conteúdo de um modelo específico com uma Referência de conteúdo](#sample-wknd-fragment-specific-model-content-reference)

## GraphQL - Query de amostra usando a Amostra da estrutura do fragmento do conteúdo {#graphql-sample-queries-sample-content-fragment-structure}

Consulte estes query de amostra para obter ilustrações de criação de query, juntamente com resultados de amostra.

>[!NOTE]
>
>Dependendo da sua instância, você pode acessar diretamente a [interface Graph *i* QL incluída com AEM API do GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface) para enviar e testar query.
>
>Por exemplo: `http://localhost:4502/content/graphiql.html`

>[!NOTE]
>
>Os query de amostra são baseados na [Exemplo de estrutura de fragmento de conteúdo para uso com GraphQL](#content-fragment-structure-graphql)

### Query de amostra - Todos os Schemas e tipos de dados disponíveis {#sample-all-schemes-datatypes}

Isso retornará todos os `types` para todos os schemas disponíveis.

**Query de amostra**

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**Resultado da amostra**

```xml
{
  "data": {
    "__schema": {
      "types": [
        {
          "name": "AdventureModel",
          "description": null
        },
        {
          "name": "AdventureModelArrayFilter",
          "description": null
        },
        {
          "name": "AdventureModelFilter",
          "description": null
        },
        {
          "name": "AdventureModelResult",
          "description": null
        },
        {
          "name": "AdventureModelResults",
          "description": null
        },
        {
          "name": "AllFragmentModels",
          "description": null
        },
        {
          "name": "ArchiveRef",
          "description": null
        },
        {
          "name": "ArrayMode",
          "description": null
        },
        {
          "name": "ArticleModel",
          "description": null
        },

...more results...

        {
          "name": "__EnumValue",
          "description": null
        },
        {
          "name": "__Field",
          "description": null
        },
        {
          "name": "__InputValue",
          "description": null
        },
        {
          "name": "__Schema",
          "description": "A GraphQL Introspection defines the capabilities of a GraphQL server. It exposes all available types and directives on the server, the entry points for query, mutation, and subscription operations."
        },
        {
          "name": "__Type",
          "description": null
        },
        {
          "name": "__TypeKind",
          "description": "An enum describing what kind of type a given __Type is"
        }
      ]
    }
  }
}
```

### Query de amostra - Todas as informações sobre todas as cidades {#sample-all-information-all-cities}

Para recuperar todas as informações sobre todas as cidades, você pode usar o query básico:
**Query de amostra**

```xml
{
  cityList {
    items
  }
}
```

Quando executado, o sistema expandirá automaticamente o query para incluir todos os campos:

```xml
{
  cityList {
    items {
      _path
      name
      country
      population
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/basel",
          "name": "Basel",
          "country": "Switzerland",
          "population": 172258
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/bucharest",
          "name": "Bucharest",
          "country": "Romania",
          "population": 1821000
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-francisco",
          "name": "San Francisco",
          "country": "USA",
          "population": 883306
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/san-jose",
          "name": "San Jose",
          "country": "USA",
          "population": 1026350
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/stuttgart",
          "name": "Stuttgart",
          "country": "Germany",
          "population": 634830
        },
        {
          "_path": "/content/dam/sample-content-fragments/cities/zurich",
          "name": "Zurich",
          "country": "Switzerland",
          "population": 415367
        }
      ]
    }
  }
}
```

### Query de amostra - Nomes de todas as cidades {#sample-names-all-cities}

Este é um query simples para retornar `name`de todas as entradas no schema `city`.

**Query de amostra**

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Basel"
        },
        {
          "name": "Berlin"
        },
        {
          "name": "Bucharest"
        },
        {
          "name": "San Francisco"
        },
        {
          "name": "San Jose"
        },
        {
          "name": "Stuttgart"
        },
        {
          "name": "Zurich"
        }
      ]
    }
  }
}
```

### Query de amostra - Um único fragmento de cidade específico {#sample-single-specific-city-fragment}

Este é um query para retornar os detalhes de uma única entrada de fragmento em um local específico no repositório.

**Query de amostra**

```xml
{
  cityByPath (_path: "/content/dam/sample-content-fragments/cities/berlin") {
    item {
      _path
      name
      country
      population
     categories
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityByPath": {
      "item": {
        "_path": "/content/dam/sample-content-fragments/cities/berlin",
        "name": "Berlin",
        "country": "Germany",
        "population": 3669491,
        "categories": [
          "city:capital",
          "city:emea"
        ]
      }
    }
  }
}
```

### Query de amostra - Todas as cidades com uma Variação nomeada {#sample-cities-named-variation}

Se você criar uma nova variação, chamada &quot;Berlin Center&quot; (`berlin_centre`), para o `city` Berlim, você poderá usar um query para retornar detalhes da variação.

**Query de amostra**

```xml
{
  cityList (variation: "berlin_center") {
    items {
      _path
      name
      country
      population
      categories
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "_path": "/content/dam/sample-content-fragments/cities/berlin",
          "name": "Berlin",
          "country": "Germany",
          "population": 3669491,
          "categories": [
            "city:capital",
            "city:emea"
          ]
        }
      ]
    }
  }
}
```

### Query de amostra - Detalhes completos de um CEO de Empresa e funcionários {#sample-full-details-company-ceos-employees}

Usando a estrutura dos fragmentos aninhados, esse query retorna os detalhes completos de um CEO da empresa e de todos os seus funcionários.

**Query de amostra**

```xml
query {
  companyList {
    items {
      name
      ceo {
        _path
        name
        firstName
        awards {
        id
          title
        }
      }
      employees {
       name
        firstName
       awards {
         id
          title
        }
      }
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Apple Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Marsh",
              "firstName": "Duke",
              "awards": []
            },
            {
              "name": "Caulfield",
              "firstName": "Max",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                }
              ]
            }
          ]
        },
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/adam-smith",
            "name": "Smith",
            "firstName": "Adam",
            "awards": []
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        },
        {
          "name": "NextStep Inc.",
          "ceo": {
            "_path": "/content/dam/sample-content-fragments/persons/steve-jobs",
            "name": "Jobs",
            "firstName": "Steve",
            "awards": []
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe",
              "awards": []
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham",
              "awards": []
            }
          ]
        }
      ]
    }
  }
}
```

### Query de amostra - Todas as pessoas que têm o nome &quot;Jobs&quot; ou &quot;Smith&quot; {#sample-all-persons-jobs-smith}

Isso filtrará todos os `persons` para qualquer um que tenha o nome `Jobs`ou `Smith`.

**Query de amostra**

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

**Resultados da amostra**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Jobs",
          "firstName": "Steve"
        }
      ]
    }
  }
}
```

### Query de amostra - Todas as pessoas que não têm o nome &quot;Jobs&quot; {#sample-all-persons-not-jobs}

Isso filtrará todos os `persons` para qualquer um que tenha o nome `Jobs`ou `Smith`.

**Query de amostra**

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
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

**Resultados da amostra**

```xml
{
  "data": {
    "personList": {
      "items": [
        {
          "name": "Lincoln",
          "firstName": "Abraham"
        },
        {
          "name": "Smith",
          "firstName": "Adam"
        },
        {
          "name": "Slade",
          "firstName": "Cutter"
        },
        {
          "name": "Marsh",
          "firstName": "Duke"
        },
        {
          "name": "Smith",
          "firstName": "Joe"
        },
        {
          "name": "Croft",
          "firstName": "Lara"
        },
        {
          "name": "Caulfield",
          "firstName": "Max"
        }
      ]
    }
  }
}
```

### Query de amostra - Todas as cidades situadas na Alemanha ou na Suíça com uma população entre 400000 e 9999999 {#sample-all-cities-d-ch-population}

Aqui, uma combinação de campos é filtrada. Um `AND` (implícito) é usado para selecionar o intervalo `population`enquanto um `OR` (explícito) é usado para selecionar as cidades necessárias.

**Query de amostra**

```xml
query {
  cityList(filter: {
    population: {
      _expressions: [
        {
          value: 400000
          _operator: GREATER_EQUAL
        }, {
          value: 1000000
          _operator: LOWER
        }
      ]
    },
    country: {
      _logOp: OR
      _expressions: [
        {
          value: "Germany"
        }, {
          value: "Switzerland"
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Stuttgart",
          "population": 634830,
          "country": "Germany"
        },
        {
          "name": "Zurich",
          "population": 415367,
          "country": "Switzerland"
        }
      ]
    }
  }
}
```

### Query de amostra - Todas as cidades com SAN no nome, independentemente do caso {#sample-all-cities-san-ignore-case}

Este query interroga todas as cidades que tenham `SAN` no nome, independentemente do caso.

**Query de amostra**

```xml
query {
  cityList(filter: {
    name: {
      _expressions: [
        {
          value: "SAN"
          _operator: CONTAINS
          _ignoreCase: true
        }
      ]
    }
  }) {
    items {
      name
      population
      country
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA"
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA"
        }
      ]
    }
  }
}
```

### Query de amostra - Filtre em uma matriz com um item que deve ocorrer pelo menos uma vez {#sample-array-item-occur-at-least-once}

Este query filtros em uma matriz com um item (`city:na`) que deve ocorrer pelo menos uma vez.

**Query de amostra**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          value: "city:na"
          _apply: AT_LEAST_ONCE
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        },
        {
          "name": "San Jose",
          "population": 1026350,
          "country": "USA",
          "categories": [
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Query de amostra - Filtrar em um valor de matriz exato {#sample-array-exact-value}

Este query filtros em um valor de matriz exato.

**Query de amostra**

```xml
query {
  cityList(filter: {
    categories: {
      _expressions: [
        {
          values: [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }) {
    items {
      name
      population
      country
      categories
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "San Francisco",
          "population": 883306,
          "country": "USA",
          "categories": [
            "city:beach",
            "city:na"
          ]
        }
      ]
    }
  }
}
```

### Query de amostra para fragmentos de conteúdo aninhados - Todas as empresas que têm pelo menos um funcionário com o nome &quot;Smith&quot; {#sample-companies-employee-smith}

Este query ilustra a filtragem de `person` de `name` &quot;Smith&quot;, retornando informações de dois fragmentos aninhados - `company` e `employee`.

**Query de amostra**

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "NextStep Inc.",
          "ceo": {
            "name": "Jobs",
            "firstName": "Steve"
          },
          "employees": [
            {
              "name": "Smith",
              "firstName": "Joe"
            },
            {
              "name": "Lincoln",
              "firstName": "Abraham"
            }
          ]
        }
      ]
    }
  }
}
```

### Query de amostra para fragmentos de conteúdo aninhados - Todas as empresas em que todos os funcionários ganharam o prêmio &quot;Gamestar&quot; {#sample-all-companies-employee-gamestar-award}

Este query ilustra a filtragem em três fragmentos aninhados - `company`, `employee` e `award`.

**Query de amostra**

```xml
query {
  companyList(filter: {
    employees: {
      _apply: ALL
      _match: {
        awards: {
          _match: {
            id: {
              _expressions: [
                {
                  value: "GS"
                  _operator:EQUALS
                }
              ]
            }
          }
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
        awards {
          id
          title
        }
      }
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "companyList": {
      "items": [
        {
          "name": "Little Pony, Inc.",
          "ceo": {
            "name": "Smith",
            "firstName": "Adam"
          },
          "employees": [
            {
              "name": "Croft",
              "firstName": "Lara",
              "awards": [
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            },
            {
              "name": "Slade",
              "firstName": "Cutter",
              "awards": [
                {
                  "id": "GB",
                  "title": "Gameblitz"
                },
                {
                  "id": "GS",
                  "title": "Gamestar"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```

### Query de amostra para metadados - Lista dos metadados para prêmios com o título GB {#sample-metadata-awards-gb}

Este query ilustra a filtragem em três fragmentos aninhados - `company`, `employee` e `award`.

**Query de amostra**

```xml
query {
  awardList(filter: {
      id: {
        _expressions: [
          {
            value:"GB"
          }
        ]
    }
  }) {
    items {
      _metadata {
        stringMetadata {
          name,
          value
        }
      }
      id
      title
    }
  }
}
```

**Resultados da amostra**

```xml
{
  "data": {
    "awardList": {
      "items": [
        {
          "_metadata": {
            "stringMetadata": [
              {
                "name": "title",
                "value": "Gameblitz Award"
              },
              {
                "name": "description",
                "value": ""
              }
            ]
          },
          "id": "GB",
          "title": "Gameblitz"
        }
      ]
    }
  }
}
```

## Query de amostra usando o projeto WKND {#sample-queries-using-wknd-project}

Esses query de amostra são baseados no projeto WKND. Isso tem:

* Modelos de fragmento de conteúdo disponíveis em:
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Fragmentos de conteúdo (e outro conteúdo) disponíveis em:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`

>[!NOTE]
>
>Como os resultados podem ser extensos, eles não são reproduzidos aqui.

### Query de amostra para todos os Fragmentos de conteúdo de um determinado modelo com as propriedades especificadas {#sample-wknd-all-model-properties}

Este query de amostra interroga:

* para todos os fragmentos de conteúdo do tipo `article`
* com as propriedades `path`e `author`.

**Query de amostra**

```xml
{
  articleList {
    items {
      _path
      author
    }
  }
}
```

### Query de amostra para metadados {#sample-wknd-metadata}

Este query interroga:

* para todos os fragmentos de conteúdo do tipo `adventure`
* metadados

**Query de amostra**

```xml
{
  adventureList {
    items {
      _path,
      _metadata {
        stringMetadata {
          name,
          value
        }
        stringArrayMetadata {
          name,
          value
        }
        intMetadata {
          name,
          value
        }
        intArrayMetadata {
          name,
          value
        }
        floatMetadata {
          name,
          value
        }
        floatArrayMetadata {
          name,
          value
        }
        booleanMetadata {
          name,
          value
        }
        booleanArrayMetadata {
          name,
          value
        }
        calendarMetadata {
          name,
          value
        }
        calendarArrayMetadata {
          name,
          value
        }
      }
    }
  }
}
```

### Query de amostra para um único fragmento de conteúdo de um determinado modelo {#sample-wknd-single-content-fragment-of-given-model}

Este query de amostra interroga:

* para um único Fragmento de conteúdo do tipo `article` em um caminho específico
   * dentro desse conteúdo, todos os formatos de conteúdo:
      * HTML
      * Markdown
      * Texto sem formatação
      * JSON 

**Query de amostra**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        author
        main {
          html
          markdown
          plaintext
          json
        }
    }
  }
}
```

### Query de amostra para um modelo de fragmento de conteúdo de um modelo {#sample-wknd-content-fragment-model-from-model}

Este query de amostra interroga:

* para um único fragmento de conteúdo
   * detalhes do Modelo de fragmento de conteúdo subjacente

**Query de amostra**

```xml
{
  adventureByPath(_path: "/content/dam/wknd/en/adventures/riverside-camping-australia/riverside-camping-australia") {
    item {
      _path
      adventureTitle
      _model {
        _path
        title
      }
    }
  }
}
```

### Query de amostra para um fragmento de conteúdo aninhado - Tipo de modelo único{#sample-wknd-nested-fragment-single-model}

Este query interroga:

* para um único Fragmento de conteúdo do tipo `article` em um caminho específico
   * dentro disso, o caminho e o autor do fragmento referenciado (aninhado)

>[!NOTE]
>
>O campo `referencearticle` tem o tipo de Dados `fragment-reference`.

**Query de amostra**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/skitouring/skitouring") {
    item {
        _path
        author
        referencearticle {
          _path
          author
      }
    }
  }
}
```

### Query de amostra para um fragmento de conteúdo aninhado - Tipo de vários modelos{#sample-wknd-nested-fragment-multiple-model}

Este query interroga:

* para vários Fragmentos de conteúdo do tipo `bookmark`
   * com referências de fragmento a outros fragmentos dos tipos de modelo específicos `article` e `adventure`

>[!NOTE]
>
>O campo `fragments` tem o tipo de Dados `fragment-reference`, com os modelos `Article`, `Adventure` selecionados.

```xml
{
  bookmarkList {
    items {
        fragments {
          ... on ArticleModel {
            _path
            author
          }
          ... on AdventureModel {
            _path
            adventureTitle
          }
        }
     }
  }
}
```

### Query de amostra para um fragmento de conteúdo de um modelo específico com referências de conteúdo{#sample-wknd-fragment-specific-model-content-reference}

Há dois sabores deste query:

1. Para retornar todas as referências de conteúdo.
1. Para retornar as referências de conteúdo específicas do tipo `attachments`.

Estes query interrogam:

* para vários Fragmentos de conteúdo do tipo `bookmark`
   * com referências de conteúdo para outros fragmentos

#### Query de amostra para vários fragmentos de conteúdo com referências pré-definidas {#sample-wknd-multiple-fragments-prefetched-references}

O query a seguir retorna todas as referências de conteúdo usando `_references`:

```xml
{
  bookmarkList {
     _references {
         ... on ImageRef {
          _path
          type
          height
        }
        ... on MultimediaRef {
          _path
          type
          size
        }
        ... on DocumentRef {
          _path
          type
          author
        }
        ... on ArchiveRef {
          _path
          type
          format
        }
    }
    items {
        _path
    }
  }
}
```

#### Query de amostra para vários fragmentos de conteúdo com Anexos {#sample-wknd-multiple-fragments-attachments}

O query a seguir retorna todos os `attachments` - um campo específico (subgrupo) do tipo `content-reference`:

>[!NOTE]
>
>O campo `attachments` tem o tipo de Dados `content-reference`, com vários formulários selecionados.

```xml
{
  bookmarkList {
    items {
      attachments {
        ... on PageRef {
          _path
          type
        }
        ... on ImageRef {
          _path
          width
        }
        ... on MultimediaRef {
          _path
          size
        }
        ... on DocumentRef {
          _path
          author
        }
        ... on ArchiveRef {
          _path
          format
        }
      }
    }
  }
}
```

### Query de amostra para um único fragmento de conteúdo com referência em linha RTE {#sample-wknd-single-fragment-rte-inline-reference}

Este query interroga:

* para um único Fragmento de conteúdo do tipo `bookmark` em um caminho específico
   * dentro disso, referências em linha do RTE

>[!NOTE]
>
>As referências em linha do RTE são hidratadas em `_references`.

**Query de amostra**

```xml
{
  bookmarkByPath(_path: "/content/dam/wknd/en/bookmarks/skitouring") {
    item {
      _path
      description {
        json
      }
    }
    _references {
      ... on ArticleModel {
        _path
      }
      ... on AdventureModel {
        _path
      }
      ... on ImageRef {
        _path
      }
      ... on MultimediaRef {
        _path
      }
      ... on DocumentRef {
        _path
      }
      ... on ArchiveRef {
        _path
      }
    }
  }
}
```

### Query de amostra para uma única variação de Fragmento de conteúdo de um determinado Modelo {#sample-wknd-single-fragment-given-model}

Este query interroga:

* para um único Fragmento de conteúdo do tipo `article` em um caminho específico
   * nesse contexto, os dados relativos à variação: `variation1`

**Query de amostra**

```xml
{
  articleByPath (_path: "/content/dam/wknd/en/magazine/alaska-adventure/alaskan-adventures", variation: "variation1") {
    item {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Query de amostra para uma Variação nomeada de vários Fragmentos de conteúdo de um determinado Modelo {#sample-wknd-variation-multiple-fragment-given-model}

Este query interroga:

* para Fragmentos de conteúdo do tipo `article` com uma variação específica: `variation1`

**Query de amostra**

```xml
{
  articleList (variation: "variation1") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

### Query de amostra para vários Fragmentos de conteúdo de uma determinada localidade {#sample-wknd-multiple-fragments-given-locale}

Este query interroga:

* para Fragmentos de conteúdo do tipo `article` na localidade `fr`

**Query de amostra**

```xml
{ 
  articleList (_locale: "fr") {
    items {
      _path
      author
      main {
        html
        markdown
        plaintext
        json
      }
    }
  }
}
```

## A Amostra da estrutura do fragmento do conteúdo (usada com GraphQL) {#content-fragment-structure-graphql}

Os query de amostra são baseados na seguinte estrutura, que usa:

* Um ou mais, [Amostra de modelos de fragmento de conteúdo](#sample-content-fragment-models-schemas) - formam a base para os schemas GraphQL

* [Amostra de ](#sample-content-fragments) fragmentos de conteúdo com base nos modelos acima

### Modelos de fragmento de conteúdo de amostra (Schemas) {#sample-content-fragment-models-schemas}

Para os query de amostra, usaremos os seguintes Modelos de conteúdo e suas inter-relações (referências ->):

* [Empresa](#model-company)
->  [Pessoa](#model-person)
    ->  [Prêmio](#model-award)

* [Cidade](#model-city)

#### Empresa {#model-company}

Os campos básicos que definem a empresa são:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Nome da empresa | Texto em linha única |  |
| CEO | Referência do fragmento (único) | [Person](#model-person) |
| Funcionários | Referência do fragmento (vários campos) | [Pessoa](#model-person) |

#### Person {#model-person}

Os campos que definem uma pessoa, que também pode ser um funcionário:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Nome | Texto em linha única |  |
| Nome | Texto em linha única |  |
| Prêmios | Referência do fragmento (vários campos) | [Prêmio](#model-award) |

#### Prêmio {#model-award}

Os campos que definem um prêmio são:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Atalho/ID | Texto em linha única |  |
| Título | Texto em linha única |  |

#### Cidade {#model-city}

Os campos para definir uma cidade são:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Nome | Texto em linha única |  |
| País | Texto em linha única |  |
| População | Número |  |
| Categorias | Tags |  |

### Amostra de fragmentos de conteúdo {#sample-content-fragments}

Os seguintes fragmentos são usados para o modelo apropriado.

#### Empresa {#fragment-company}

| Nome da empresa | CEO | Funcionários |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max Caulfield |
|  Little Pony Inc. | Adam Smith | Lara Croft<br>Escória Cortadora |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Pessoa {#fragment-person}

| Nome | Nome | Prêmios |
|--- |--- |--- |
| Lincoln |  Abe |  |
| Smith | Adam |   |
| Barra |  Cortador |  Gameblitz<br>Gamestar |
| pântano |  Duke |   |   |
|  Smith |  Joe |   |
| Corte |  Lara | Gamestar |
| Caulfield |  Máximo |  Gameblitz |
|  Tarefas |  Steve |   |

#### Prêmio {#fragment-award}

| Atalho/ID | Título |
|--- |--- |
| GB | Gameblitz |
|  GS | Gamestar |
|  OSC | Oscar |

#### Cidade {#fragment-city}

| Nome | País | População | Categorias |
|--- |--- |--- |--- |
| Basileia | Suíça | 172258 | cidade:emea |
| Berlim | Alemanha | 3669491 | cidade:capital<br>cidade:emea |
| Bucareste | Romênia | 1821000 |  cidade:capital<br>cidade:emea |
| São Francisco |  EUA |  883306 |  cidade:praia<br>cidade:na |
| San Jose |  EUA |  102635 |  cidade:na |
| Stuttgart |  Alemanha |  634830 |  cidade:emea |
|  Zurique |  Suíça |  415367 |  cidade:capital<br>cidade:emea |
