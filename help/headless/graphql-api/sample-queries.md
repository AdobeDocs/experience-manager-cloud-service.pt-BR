---
title: Saiba como usar o GraphQL com o AEM - Exemplos de conteúdo e consultas
description: Saiba como usar o GraphQL com o AEM para fornecer conteúdo de forma headless, explorando exemplos de conteúdo e consultas.
feature: Headless, Content Fragments,GraphQL API
exl-id: b60fcf97-4736-4606-8b41-4051b8b0c8a7
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1927'
ht-degree: 89%

---

# Saiba como usar o GraphQL com o AEM - Exemplos de conteúdo e consultas {#learn-graphql-with-aem-sample-content-queries}

Saiba como usar o GraphQL com o AEM para fornecer conteúdo de forma headless, explorando exemplos de conteúdo e consultas.

>[!NOTE]
>
>Leia esta página juntamente com o seguinte conteúdo:
>
>* [Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)
>* [Modelos de fragmentos do conteúdo](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
>* [API GraphQL do AEM para uso com Fragmentos de conteúdo](/help/headless/graphql-api/content-fragments.md)

Para começar a usar consultas GraphQL e aprender como elas funcionam com fragmentos de conteúdo do AEM, é útil examinar alguns exemplos práticos.

Para isso, consulte:

* Um [exemplo de estrutura do Fragmento de conteúdo](#content-fragment-structure-graphql)

* E alguns [exemplos de consultas GraphQL](#graphql-sample-queries), com base no exemplo de estrutura de fragmento de conteúdo (modelos de fragmento de conteúdo e fragmentos de conteúdo relacionados).

>[!CONTEXTUALHELP]
>id="aemcloud_headless_graphql_sample"
>title="Saiba como usar o GraphQL com o AEM - Exemplos de conteúdo e consultas"
>abstract="Saiba como usar o GraphQL com o AEM para fornecer conteúdo em headless, explorando exemplos de conteúdo e consultas."

## GraphQL - Exemplos de consultas usando o Exemplo de estrutura do Fragmento de conteúdo {#graphql-sample-queries-sample-content-fragment-structure}

Veja esses exemplos de consultas para obter ilustrações de como criar consultas, e veja também os exemplos de resultados.

>[!NOTE]
>
>Dependendo do caso, você pode acessar diretamente a [interface GraphiQL incluída na API GraphQL do AEM](/help/headless/graphql-api/graphiql-ide.md) para enviar e testar consultas.
>
>É possível acessar o editor de consultas por meio de:
>
>* **Ferramentas** > **Geral** > **Editor de Consultas do GraphQL**
>* diretamente; por exemplo, `http://localhost:4502/aem/graphiql.html`

>[!NOTE]
>
>Os exemplos de consultas são baseados no [Exemplo de estrutura de Fragmento de conteúdo para uso com o GraphQL](#content-fragment-structure-graphql)

### Exemplo de consulta - Todos os esquemas e tipos de dados disponíveis {#sample-all-schemes-datatypes}

Retorna todos os `types` para todos os esquemas disponíveis.

**Exemplo de consulta**

```graphql
{
  __schema {
    types {
      name
      description
    }
  }
}
```

**Exemplo de resultado**

```json
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

### Exemplo de consulta - Todas as informações sobre todas as cidades {#sample-all-information-all-cities}

Para recuperar todas as informações sobre todas as cidades, você pode usar essa consulta básica:
**Exemplo de consulta**

```graphql
{
  cityList {
    items
  }
}
```

Quando executada, o sistema expande automaticamente a consulta para incluir todos os campos:

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta - Nomes de todas as cidades {#sample-names-all-cities}

Esta é uma consulta simples para retornar o `name` de todas as entradas no esquema `city`.

**Exemplo de consulta**

```graphql
query {
  cityList {
    items {
      name
    }
  }
}
```

**Exemplo de resultados**

```json
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

### Exemplo de consulta - Um único fragmento de cidade específico {#sample-single-specific-city-fragment}

Esta é uma consulta para retornar os detalhes de uma única entrada de fragmento em um local específico no repositório.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta - Todas as cidades com uma variação nomeada {#sample-cities-named-variation}

Se você criar uma nova variação chamada “Centro de Berlim” (`berlin_centre`) para a `city` Berlim, é possível usar uma consulta para retornar detalhes da variação.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta - Nomes de todas as cidades marcadas como Quebras de cidade {#sample-names-all-cities-tagged-city-breaks}

Se você:

* criar várias tags chamadas `Tourism` : `Business`, `City Break`, `Holiday`
* e atribuí-las à variação principal de várias instâncias de `City`

É possível usar uma consulta para retornar detalhes de `name` e `tags` de todas as entradas marcadas como Cidades para passeio no esquema de `city`.

**Exemplo de consulta**

```xml
query {
  cityList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "tourism:city-break", _operator: CONTAINS}]}}
  ){
    items {
      name,
      _tags
    }
  }
}
```

**Exemplo de resultados**

```xml
{
  "data": {
    "cityList": {
      "items": [
        {
          "name": "Berlin",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        },
        {
          "name": "Zurich",
          "_tags": [
            "tourism:city-break",
            "tourism:business"
          ]
        }
      ]
    }
  }
}
```

### Exemplo de consulta - Detalhes completos do CEO e funcionários de uma empresa {#sample-full-details-company-ceos-employees}

Usando a estrutura dos fragmentos aninhados, essa consulta retorna os detalhes completos do CEO de uma empresa e de todos os funcionários dela.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta - Todas as pessoas com o nome de &quot;Jobs&quot; ou &quot;Smith&quot; {#sample-all-persons-jobs-smith}

Uma consulta que filtra todas as `persons` para encontrar as que possuam o nome `Jobs` ou `Smith`.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta - Todas as pessoas que não tenham o nome &quot;Jobs&quot; {#sample-all-persons-not-jobs}

Uma consulta que filtra todas as `persons` para encontrar as que possuam o nome `Jobs` ou `Smith`.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta - Todas as aventuras cujo `_path` comece com um prefixo específico {#sample-wknd-all-adventures-cycling-path-filter}

Todas as `adventures` em que o `_path` comece com um prefixo específico (`/content/dam/wknd/en/adventures/cycling`).

**Exemplo de consulta**

```graphql
query {
  adventureList(
    filter: {
      _path: {
        _expressions: [
        {
          value: "/content/dam/wknd/en/adventures/cycling"
         _operator: STARTS_WITH
        }]
       }
    })
    {
    items {
      _path
    }
  }
}
```

**Exemplo de resultados**

```json
{
  "data": {
    "adventureList": {
      "items": [
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-southern-utah/cycling-southern-utah"
        },
        {
          "_path": "/content/dam/wknd/en/adventures/cycling-tuscany/cycling-tuscany"
        }
      ]
    }
  }
}
```

### Exemplo de consulta - Todas as cidades localizadas na Alemanha ou na Suíça com uma população de 400.000 a 999.999 pessoas {#sample-all-cities-d-ch-population}

Aqui, uma combinação de campos é filtrada. Um `AND` (implícito) é usado para selecionar o intervalo `population`, enquanto um `OR` (explícito) é usado para selecionar as cidades necessárias.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta - todas as cidades com SAN no nome, podendo ser maiúsculas ou minúsculas {#sample-all-cities-san-ignore-case}

Esta consulta interroga todas as cidades que tenham `SAN` no nome, podendo ser maiúsculas ou minúsculas.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta - filtrar em uma matriz com um item que deve ocorrer pelo menos uma vez {#sample-array-item-occur-at-least-once}

Essa consulta filtra em uma matriz com um item (`city:na`) que deve ocorrer pelo menos uma vez.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta - filtrar em um valor de matriz exato {#sample-array-exact-value}

Essa consulta filtra em um valor de matriz exato.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta para fragmentos de conteúdo aninhados - todas as empresas que tenham pelo menos um funcionário com o nome &quot;Smith&quot; {#sample-companies-employee-smith}

Esta consulta ilustra a filtragem de qualquer `person` de `name` &quot;Smith&quot;, retornando informações de dois fragmentos aninhados - `company` e `employee`.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta para fragmentos de conteúdo aninhados - todas as empresas em que todos os funcionários ganharam o prêmio &quot;Gamestar&quot; {#sample-all-companies-employee-gamestar-award}

Esta consulta ilustra a filtragem entre três fragmentos aninhados - `company`, `employee` e `award`.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

### Exemplo de consulta para metadados - listar os metadados para prêmios denominados GB {#sample-metadata-awards-gb}

Esta consulta ilustra a filtragem entre três fragmentos aninhados - `company`, `employee` e `award`.

**Exemplo de consulta**

```graphql
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

**Exemplo de resultados**

```json
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

## Exemplo de consulta usando o projeto WKND {#sample-queries-using-wknd-project}

Esses exemplos de consultas são baseadas no projeto WKND. Ele tem o seguinte:

* Modelos de fragmentos de conteúdo disponíveis em:
  `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Fragmentos de conteúdo (e outro conteúdo) disponíveis em:
  `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
  `http://<hostname>:<port>/assets.html/content/dam/wknd-shared/en`

>[!NOTE]
>
>Visto que podem haver inúmeros resultados, eles não serão reproduzidos aqui.

### Exemplo de consulta para todos os Fragmentos de conteúdo de um determinado modelo com as propriedades especificadas {#sample-wknd-all-model-properties}

Este exemplo de consulta interroga:

* por todos os Fragmentos de conteúdo do tipo `article`
* com o `_path` e as propriedades do `authorFragment`.

**Exemplo de consulta**

```graphql
{
  articleList {
    items {
      _path
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
    }
 }
}
```

### Exemplo de consulta para metadados {#sample-wknd-metadata}

Esta consulta interroga:

* por todos os Fragmentos de conteúdo do tipo `adventure`
* metadados

**Exemplo de consulta**

```graphql
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

### Exemplo de consulta para um único Fragmento de conteúdo de um determinado modelo {#sample-wknd-single-content-fragment-of-given-model}

Este exemplo de consulta interroga:

* por um único Fragmento de conteúdo do tipo `article` em um caminho específico
   * dentro desse fragmento, todos os formatos de conteúdo:
      * HTML
      * Markdown
      * Texto sem formatação
      * JSON

**Exemplo de consulta**

```graphql
{
  articleByPath(_path: "/content/dam/wknd-shared/en/magazine/alaska-adventure/alaskan-adventures") {
    item {
        _path
        authorFragment {
          _path
          firstName
          lastName
          birthDay
        }
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

### Exemplo de consulta para um modelo de fragmento de conteúdo a partir de um modelo {#sample-wknd-content-fragment-model-from-model}

Este exemplo de consulta interroga:

* por um único Fragmento de conteúdo
   * detalhes do modelo de Fragmento de conteúdo subjacente

**Exemplo de consulta**

```graphql
{
  adventureByPath(_path: "/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van") {
    item {
      _path
      title
      _model {
        _path
        title
      }
    }
  }
}
```

### Exemplo de consulta para um Fragmento de conteúdo aninhado - tipo de modelo único{#sample-wknd-nested-fragment-single-model}

Esta consulta interroga:

* por um único Fragmento de conteúdo do tipo `article` em um caminho específico
   * dentro desse fragmento, o caminho e autor(a) do fragmento referenciado (aninhado)

>[!NOTE]
>
>O campo `referencearticle` tem o tipo de dados `fragment-reference`.

**Exemplo de consulta**

```graphql
{
  adventureByPath(_path: "/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van") {
    item {
      _path
      title
      _model {
        _path
        title
      }
    }
  }
}
```

### Exemplo de consulta para um Fragmento de conteúdo aninhado - tipo de modelo múltiplo{#sample-wknd-nested-fragment-multiple-model}

#### Tipo de modelo referenciado único

Esta consulta interroga:

* por vários Fragmentos de conteúdo do tipo `bookmark`
   * com referências de fragmentos a outros fragmentos dos tipos de modelo específicos `Article`

>[!NOTE]
>
>O campo `fragments` tem o tipo de dados `fragment-reference`, com o modelo `Article` selecionado. A consulta fornece `fragments` como uma matriz de `[Article]`.

```graphql
{
  bookmarkList {
    items {
        fragments {
          _path
          author
        }
     }
  }
}
```

#### Vários tipos de modelo referenciados

Esta consulta interroga:

* por vários Fragmentos de conteúdo do tipo `bookmark`
   * com Referências de fragmentos a outros fragmentos dos tipos de modelo específicos `Article` e `Adventure`

>[!NOTE]
>
>O campo `fragments` tem o tipo de dados `fragment-reference`, com os modelos `Article` e `Adventure` selecionados. A consulta entrega `fragments` como uma matriz de `[AllFragmentModels]`, que é desreferenciada com o tipo de união.

```graphql
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

### Exemplo de consulta para um Fragmento de conteúdo de um modelo específico com Referências de conteúdo{#sample-wknd-fragment-specific-model-content-reference}

Há duas opções desta consulta:

1. Para retornar todas as referências de conteúdo.
1. Para retornar as referências de conteúdo específicas do tipo `attachments`.

Essas consultas interrogam:

* por vários Fragmentos de conteúdo do tipo `bookmark`
   * com Referências de conteúdo a outros fragmentos

#### Exemplo de consulta para vários Fragmentos de conteúdo com Referências previamente buscadas {#sample-wknd-multiple-fragments-prefetched-references}

A consulta a seguir retorna todas as referências de conteúdo usando `_references`:

<!-- need replacement query -->

```graphql
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

#### Exemplo de consulta para vários Fragmentos de conteúdo com anexos {#sample-wknd-multiple-fragments-attachments}

A consulta a seguir retorna todos os `attachments` - um campo específico (subgrupo) do tipo `content-reference`:

>[!NOTE]
>
>O campo `attachments` tem o tipo de dados `content-reference`, com vários formulários selecionados.

<!-- need replacement query -->

```graphql
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

### Exemplos de consultas para um fragmento de conteúdo de um modelo específico usando referências UUID {#sample-wknd-fragment-specific-model-uuid-references}

Essas consultas interrogam:

* a UUID de um fragmento de conteúdo e de fragmentos ou ativos de conteúdo referenciados
* o resultado é retornado por meio da propriedade JSON `_id`

#### Exemplo de consulta para um Fragmento de conteúdo de um modelo específico usando uma referência UUID {#sample-wknd-fragment-specific-model-using-a-uuid-reference}

A consulta a seguir retorna todas as referências de conteúdo usando `_id` e `_path`:

```graphql
{
  articleList {
    items {
        _id
        _path
        title
        featuredImage {
          ... on ImageRef {
            _id
            _path           
          }
        }
        authorFragment {
          firstName
          lastName
          profilePicture {
            ... on ImageRef {
              _id
              _path
            }
          }
        }
      }
  }
}
```

#### Exemplo de consulta para fragmentos de conteúdo por referência UUID {#sample-wknd-fragment-specific-model-by-uuid-reference}

A consulta a seguir retorna todas as referências de conteúdo relacionadas a uma `_id` específica:

```graphql
{
  articleById(_id: "3ce2bf53-7436-4d3e-b19a-2793bc2ca63e") {
    item {
      _id
      _path
      title
      featuredImage {
        ... on ImageRef {
          _id
          _path
        }
      }
      authorFragment {
        firstName
        lastName
        profilePicture {
          ... on ImageRef {
            _id
            _path
          }
        }
      }
    }
  }
}
```

### Exemplo de consulta para um único Fragmento de conteúdo com Referência em linha do RTE {#sample-wknd-single-fragment-rte-inline-reference}

Esta consulta interroga:

* por um único Fragmento de conteúdo do tipo `bookmark` em um caminho específico
   * dentro disso, referências em linha do RTE

>[!NOTE]
>
>As referências em linha do RTE são hidratadas em `_references`.

<!-- need replacement query -->

**Exemplo de consulta**

```graphql
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

### Exemplo de consulta para uma única variação do Fragmento de conteúdo de um determinado modelo {#sample-wknd-single-fragment-given-model}

Esta consulta interroga:

* por um único Fragmento de conteúdo do tipo `author` em um caminho específico
   * dentro desse fragmento, os dados relativos à variação: `another`

**Exemplo de consulta**

```graphql
{
  authorByPath(_path: "/content/dam/wknd-shared/en/contributors/ian-provo", variation: "another") {
    item {
        _path
        _variation
        firstName
        lastName
        birthDay
    }
  }
}
```

### Exemplo de consulta para uma variação nomeada de vários Fragmentos de conteúdo de um determinado modelo {#sample-wknd-variation-multiple-fragment-given-model}

Esta consulta interroga:

* por Fragmentos de conteúdo do tipo `author` com uma variação específica: `another`

>[!NOTE]
>
>Essa consulta demonstra o fallback dos fragmentos de conteúdo que não têm uma [variação](/help/headless/graphql-api/content-fragments.md#variations) do nome especificado.

**Exemplo de consulta**

```graphql
{
  authorList(variation: "another") {
    items {
        _path
        _variation
        firstName
        lastName
        birthDay
    }
  }
}
```

### Exemplo de consulta para vários fragmentos de conteúdo e suas variações em um determinado modelo {#sample-wknd-multiple-fragment-variations-given-model}

Esta consulta interroga:

* fragmentos de conteúdo do tipo `article` e todas as variações

**Exemplo de consulta**

```xml
query {
  articleList(
    includeVariations: true  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### Exemplo de consulta para variações de fragmento de conteúdo de um determinado modelo que tem uma tag específica anexada{#sample-wknd-fragment-variations-given-model-specific-tag}

Esta consulta interroga:

* fragmentos de conteúdo do tipo `article` com uma ou mais variações que possuem a tag `WKND : Activity / Hiking`

**Exemplo de consulta**

```xml
{
  articleList(
    includeVariations: true,
    filter: {_tags: {_expressions: [{value: "wknd:activity/hiking", _operator: CONTAINS}]}}
  ){
    items {
      _variation
      _path
      _tags
      _metadata {
        stringArrayMetadata {
          name
          value
        }
      }
    }
  }
}
```

### Exemplo de consulta para vários Fragmentos de conteúdo de uma determinada localidade {#sample-wknd-multiple-fragments-given-locale}

Esta consulta interroga:

* por Fragmentos de conteúdo do tipo `article` na localidade `fr`

**Exemplo de consulta**

```graphql
{ 
  articleList(_locale: "fr") {
    items {
      _path
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
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

### Exemplo de consulta de lista usando deslocamento e limite {#sample-list-offset-limit}

Esta consulta interroga:

* para a página de resultados que contém até cinco artigos, a partir do quinto artigo da lista de resultados *completa*

**Exemplo de consulta**

```graphql
{
   articleList(offset: 5, limit: 5) {
    items {
      authorFragment {
        _path
        firstName
        lastName
        birthDay
      }
      _path
    }
  }
}
```

### Exemplo de consulta de paginação usando primeiro e depois  {#sample-pagination-first-after}

Esta consulta interroga:

* para a página de resultados que contém até cinco aventuras, a partir do item de cursor especificado na lista de resultados *completa*

**Exemplo de consulta**

```graphql
{
    adventurePaginated(first: 5, after: "ODg1MmMyMmEtZTAzMy00MTNjLThiMzMtZGQyMzY5ZTNjN2M1") {
        edges {
          cursor
          node {
            title
          }
        }
        pageInfo {
          endCursor
          hasNextPage
        }
    }
}
```

### Exemplo de consulta com filtragem por ID de _tags, excluindo variações {#sample-filtering-tag-not-variations}

Esta consulta interroga:

* fragmentos de conteúdo do tipo `vehicle` que possuem a tag `big-block`,
* excluindo variações

**Exemplo de consulta**

```graphql
query {
  vehicleList(
    filter: {
    _tags: {
      _expressions: [
        {
          value: "vehicles:big-block"
          _operator: CONTAINS
        }
      ]
    }
  }) {
    items {
      _variation
      _path
      type
      name
      model
      fuel
      _tags
    }
  }
} 
```

### Exemplo de consulta com filtragem por ID de _tags, incluindo variações {#sample-filtering-tag-with-variations}

Esta consulta interroga:

* fragmentos de conteúdo do tipo `vehicle` que possuem a tag `big-block`,
* incluindo variações

**Exemplo de consulta**

```graphql
{
  enginePaginated(after: "SjkKNmVkODFmMGQtNTQyYy00NmQ4LTljMzktMjhlNzQwZTY1YWI2Cmo5", first: 9 ,includeVariations:true, sort: "name",
    filter: {
    _tags: {
      _expressions: [
        {
          value: "vehicles:big-block"
          _operator: CONTAINS
        }
      ]
    }
  }) {
    edges{
    node {
        _variation
        _path
        name
        type
        size
        _tags
        _metadata {
          stringArrayMetadata {
            name
            value
          }
        }
    }
      cursor
    }
  }
} 
```

## Exemplos de consulta para entrega de DAM e Dynamic Media Assets {#sample-queries-delivery-DAM-DM}

Para entrega de imagens otimizadas para a Web (de ativos DAM):

* [Exemplo de consulta para entrega de imagens otimizadas para a Web com parâmetros completos](/help/headless/graphql-api/content-fragments.md#web-optimized-image-delivery-full-parameters)

* [Exemplo de consulta para entrega de imagens otimizadas para a Web com um único parâmetro especificado](/help/headless/graphql-api/content-fragments.md#web-optimized-image-delivery-single-query-variable)

Para a entrega do URL a um ativo do Dynamic Media

* Consulte [Exemplo de consulta para entrega de ativos do Dynamic Media por URL - Referência da imagem](/help/headless/graphql-api/content-fragments.md#sample-query-dynamic-media-asset-delivery-by-url-imageref)

* Consulte [Exemplo de consulta para entrega de ativos do Dynamic Media por URL - Várias Referências](/help/headless/graphql-api/content-fragments.md#sample-query-dynamic-media-asset-delivery-by-url-multiple-refs)

Para a entrega de ativos remotos, que não são locais para a instância atual do AEM, por meio do Editor de fragmentos de conteúdo.

* Consulte [Exemplo de consulta para Dynamic Media para suporte a ativos OpenAPI (Assets Remoto)](/help/headless/graphql-api/content-fragments.md#sample-query-dynamic-media-for-openapi-asset-support)

## Exemplo de estrutura do fragmento de conteúdo (usada com GraphQL) {#content-fragment-structure-graphql}

Os exemplos de consultas são baseados na seguinte estrutura, que usa:

* Um ou mais, [exemplos de Modelos de fragmento de conteúdo](#sample-content-fragment-models-schemas) - formam a base para os esquemas GraphQL

* [Exemplos de Fragmentos de conteúdo](#sample-content-fragments) com base nos modelos acima referidos

### Exemplos de Modelos de fragmento de conteúdo (esquemas) {#sample-content-fragment-models-schemas}

Para as consultas de exemplo, utilize os seguintes modelos de conteúdo e suas inter-relações (referências ->):

* [Empresa](#model-company)
-> [Pessoa](#model-person)
-> [Prêmio](#model-award)

* [Cidade](#model-city)

#### Empresa {#model-company}

Os campos básicos que definem a empresa são:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Nome da empresa | Texto em linha única | |
| CEO | Referência do fragmento (único) | [Pessoa](#model-person) |
| Empregados | Referência do fragmento (vários campos) | [Pessoa](#model-person) |

#### Pessoa {#model-person}

Os campos que definem uma pessoa, que também pode ser um funcionário:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Nome | Texto em linha única | |
| Nome | Texto em linha única | |
| Prêmios | Referência do fragmento (vários campos) | [Prêmio](#model-award) |

#### Prêmio {#model-award}

Os campos que definem um prêmio são:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Atalho/ID | Texto em linha única | |
| Título | Texto em linha única | |

#### Cidade {#model-city}

Os campos para definir uma cidade são:

| Nome do campo | Tipo de dados | Referência |
|--- |--- |--- |
| Nome | Texto em linha única | |
| País | Texto em linha única | |
| População | Número | |
| Categorias | Tags | |

### Exemplos de Fragmentos de conteúdo {#sample-content-fragments}

Os fragmentos a seguir são usados para o modelo apropriado.

#### Empresa {#fragment-company}

| Nome da empresa | CEO | Empregados |
|--- |--- |--- |
| Apple | Steve Jobs | Duke Marsh<br>Max Caulfield |
| Little Pony Inc. | Adam Smith | Lara Croft<br>Cutter Slade |
| NextStep Inc. | Steve Jobs | Joe Smith<br>Abe Lincoln |

#### Pessoa {#fragment-person}

| Nome | Nome | Prêmios |
|--- |--- |--- |
| Lincoln | Abe | |
| Smith | Adam | |
| Slade | Cutter | Gameblitz<br>Gamestar |
| Marsh | Duke | |
| Smith | Joe | |
| Croft | Lara | Gamestar |
| Caulfield | Max | Gameblitz |
| Tarefas | Steve | |

#### Prêmio {#fragment-award}

| Atalho/ID | Título |
|--- |--- |
| GB | Gameblitz |
| GS | Gamestar |
| OSC | Oscar |

#### Cidade {#fragment-city}

| Nome | País | População | Categorias |
|--- |--- |--- |--- |
| Basileia | Suíça | 172258 | cidade:emea |
| Berlim | Alemanha | 3669491 | cidade:capital<br>cidade:emea |
| Bucareste | Romênia | 1821000 | cidade:capital<br>cidade:emea |
| São Francisco | EUA | 883306 | cidade:beach<br>cidade:na |
| San Jose | EUA | 102635 | cidade:na |
| Stuttgart | Alemanha | 634830 | cidade:emea |
| Zurique | Suíça | 415367 | cidade:capital<br>cidade:emea |
