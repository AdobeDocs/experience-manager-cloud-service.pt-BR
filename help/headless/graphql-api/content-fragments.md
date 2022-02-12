---
title: AEM API GraphQL para uso com Fragmentos de conteúdo
description: Saiba como usar os Fragmentos de conteúdo no Adobe Experience Manager (AEM) as a Cloud Service com a API GraphQL AEM para a entrega de conteúdo sem interface.
feature: Content Fragments,GraphQL API
exl-id: bdd60e7b-4ab9-4aa5-add9-01c1847f37f6
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 1%

---


# AEM API GraphQL para uso com Fragmentos de conteúdo {#graphql-api-for-use-with-content-fragments}

Saiba como usar os Fragmentos de conteúdo no Adobe Experience Manager (AEM) as a Cloud Service com a API GraphQL AEM para a entrega de conteúdo sem interface.

AEM API GraphQL as a Cloud Service usada com Fragmentos de conteúdo é altamente baseada na API GraphQL padrão de código aberto.

Usar a API GraphQL no AEM permite a entrega eficiente dos Fragmentos de conteúdo aos clientes JavaScript em implementações CMS sem periféricos:

* Evitar solicitações de API iterativas como com REST,
* Garantir que a entrega se limite aos requisitos específicos,
* Permite a entrega em massa do exatamente o que é necessário para renderização como resposta a uma única consulta de API.

>[!NOTE]
>
>O GraphQL é usado atualmente em dois cenários (separados) no Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [O AEM Commerce consome dados de uma plataforma do Commerce via GraphQL](/help/commerce-cloud/integrating/magento.md).
>* AEM Fragmentos de conteúdo trabalham com a API GraphQL AEM (uma implementação personalizada, com base no GraphQL padrão), para fornecer conteúdo estruturado para uso em seus aplicativos.


## A API GraphQL {#graphql-api}

GraphQL é:

* &quot;*...um idioma de consulta para APIs e um tempo de execução para realizar essas consultas com seus dados existentes. O GraphQL fornece uma descrição completa e compreensível dos dados em sua API, fornece aos clientes o poder de solicitar exatamente o que precisam e nada mais, facilita a evolução das APIs ao longo do tempo e habilita poderosas ferramentas de desenvolvedor.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

* &quot;*...uma especificação aberta para uma camada de API flexível. Coloque GraphQL sobre seus back-end existentes para criar produtos mais rápido do que nunca....*&quot;.

   Consulte [Explorar GraphQL](https://www.graphql.com).

* *&quot;...uma linguagem de consulta de dados e especificação desenvolvidas internamente pela Facebook em 2012 antes de serem disponibilizadas publicamente em 2015. Ele oferece uma alternativa às arquiteturas baseadas em REST com o objetivo de aumentar a produtividade do desenvolvedor e minimizar as quantidades de dados transferidos. GraphQL é usado na produção por centenas de organizações de todos os tamanhos...&quot;*

   Consulte [Base GraphQL](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Para obter mais informações sobre a API GraphQL, consulte as seguintes seções (entre muitos outros recursos):

* Em [grafql.org](https://graphql.org):

   * [Introdução ao GraphQL](https://graphql.org/learn)

   * [A especificação GraphQL](https://spec.graphql.org/)

* Em [grafql.com](https://graphql.com):

   * [Guias](https://www.graphql.com/guides/)

   * [Tutoriais](https://www.graphql.com/tutorials/)

   * [Estudos de caso](https://www.graphql.com/case-studies/)

A implementação de GraphQL para AEM é baseada na Biblioteca GraphQL Java padrão. Consulte:

* [graphQL.org - Java](https://graphql.org/code/#java)

* [Java GraphQL no GitHub](https://github.com/graphql-java)

### Terminologia GraphQL {#graphql-terminology}

GraphQL usa o seguinte:

* **[Queries](https://graphql.org/learn/queries/)**

* **[Esquemas e tipos](https://graphql.org/learn/schema/)**:

   * Os esquemas são gerados por AEM com base nos Modelos de fragmento de conteúdo.
   * Usando seus esquemas, GraphQL apresenta os tipos e as operações permitidas para GraphQL para AEM implementação.

* **[Campos](https://graphql.org/learn/queries/#fields)**

* **[Endpoint GraphQL](graphql-endpoint.md)**
   * O caminho no AEM que responde a consultas GraphQL e fornece acesso aos esquemas GraphQL.

   * Consulte [Ativação do terminal GraphQL](graphql-endpoint.md) para obter mais detalhes.

Consulte a [(GraphQL.org) Introdução ao GraphQL](https://graphql.org/learn/) para obter detalhes abrangentes, incluindo o [Práticas recomendadas](https://graphql.org/learn/best-practices/).

### Tipos de consulta GraphQL {#graphql-query-types}

Com GraphQL, você pode executar consultas para retornar:

* A **entrada única**

* A **[lista de entradas](https://graphql.org/learn/schema/#lists-and-non-null)**

Também é possível executar:

* [Consultas Persistentes, que estão em cache](/help/headless/graphql-api/persisted-queries.md)

### GraphiQL IDE {#graphiql-ide}

Você pode testar e depurar consultas GraphQL usando o [GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md).

## Casos de uso para ambientes de autor e publicação {#use-cases-author-publish-environments}

Os casos de uso podem depender do tipo de AEM ambiente as a Cloud Service:

* Ambiente de publicação; usado para:
   * Dados de consulta para aplicativo JS (caso de uso padrão)

* Ambiente de criação; usado para:
   * Consultar dados para &quot;fins de gerenciamento de conteúdo&quot;:
      * GraphQL em AEM as a Cloud Service é atualmente uma API somente leitura.
      * A REST API pode ser usada para operações de CR(u)D.

## Permissões {#permission}

As permissões são as necessárias para acessar o Assets.

## Geração de esquema {#schema-generation}

GraphQL é uma API altamente digitada, o que significa que os dados devem ser estruturados e organizados claramente por tipo.

A especificação GraphQL fornece uma série de diretrizes sobre como criar uma API robusta para interrogar dados em uma determinada instância. Para fazer isso, um cliente precisa buscar a variável [Esquema](#schema-generation), que contém todos os tipos necessários para um query.

Para Fragmentos de conteúdo, os esquemas GraphQL (estrutura e tipos) são baseados em **Ativado** [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md) e seus tipos de dados.

>[!CAUTION]
>
>Todos os esquemas GraphQL (derivados dos Modelos de fragmento de conteúdo que foram **Ativado**) são legíveis por meio do ponto de extremidade GraphQL.
>
>Isso significa que você precisa garantir que não haja dados confidenciais disponíveis, pois eles poderiam ser vazados dessa forma; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.

Por exemplo, se um usuário criou um Modelo de fragmento de conteúdo chamado `Article`e AEM gera o objeto `article` que é de um tipo `ArticleModel`. Os campos desse tipo correspondem aos campos e tipos de dados definidos no modelo.

1. Um modelo de fragmento de conteúdo:

   ![Modelo de fragmento de conteúdo para uso com GraphQL](assets/cfm-graphqlapi-01.png "Modelo de fragmento de conteúdo para uso com GraphQL")

1. O esquema GraphQL correspondente (saída da documentação automática GraphiQL):
   ![Esquema GraphQL com base no modelo de fragmento de conteúdo](assets/cfm-graphqlapi-02.png "Esquema GraphQL com base no modelo de fragmento de conteúdo")

   Isso mostra que o tipo gerado `ArticleModel` contém vários [campos](#fields).

   * Três delas foram controladas pelo usuário: `author`, `main` e `referencearticle`.

   * Os outros campos foram adicionados automaticamente por AEM e representam métodos úteis para fornecer informações sobre um determinado Fragmento de conteúdo; neste exemplo, `_path`, `_metadata`, `_variations`. Esses [campos auxiliares](#helper-fields) estejam marcados com um `_` para distinguir entre o que foi definido pelo usuário e o que foi gerado automaticamente.

1. Depois que um usuário cria um Fragmento de conteúdo com base no modelo de Artigo, ele pode ser interrogado por meio de GraphQL. Para obter exemplos, consulte a [Consultas de exemplo](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries) (com base em [exemplo da estrutura do Fragmento de conteúdo para uso com GraphQL](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql)).

No GraphQL para AEM, o esquema é flexível. Isso significa que ele é gerado automaticamente cada vez que um Modelo de fragmento de conteúdo é criado, atualizado ou excluído. Os caches de esquema de dados também são atualizados quando você atualiza um Modelo de fragmento de conteúdo.

O serviço GraphQL do Sites escuta (em segundo plano) quaisquer modificações feitas em um Modelo de fragmento de conteúdo. Quando as atualizações são detectadas, somente essa parte do esquema é regenerada. Essa otimização economiza tempo e oferece estabilidade.

Por exemplo, se você:

1. Instale um pacote contendo `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. Tipos GraphQL para `Model-1` e `Model-2` serão geradas.

1. Em seguida, modifique `Content-Fragment-Model-2`:

   1. Somente a variável `Model-2` O tipo GraphQL será atualizado.

   1. Considerando que `Model-1` permanecerá o mesmo.

>[!NOTE]
>
>Isso é importante observar caso queira fazer atualizações em massa nos Modelos de fragmento de conteúdo por meio da api REST ou de outra forma.

O esquema é distribuído por meio do mesmo terminal que as consultas GraphQL, com o cliente lidando com o fato de que o esquema é chamado com a extensão `GQLschema`. Por exemplo, executar uma `GET` solicitação em `/content/cq:graphql/global/endpoint.GQLschema` resultará na saída do schema com o Content-type: `text/x-graphql-schema;charset=iso-8859-1`.

### Geração de esquema - Modelos não publicados {#schema-generation-unpublished-models}

Quando os Fragmentos de conteúdo são aninhados, pode acontecer que um Modelo de fragmento de conteúdo principal seja publicado, mas um modelo referenciado não é.

>[!NOTE]
>
>A interface do usuário do AEM impede que isso aconteça, mas se a publicação for feita de forma programática ou com pacotes de conteúdo, ela poderá ocorrer.

Quando isso acontece, o AEM gera um *incompleto* Esquema do modelo de fragmento de conteúdo principal. Isso significa que a Referência do fragmento, que depende do modelo não publicado, é removida do esquema.

## Fields {#fields}

Dentro do schema há campos individuais, de duas categorias básicas:

* Campos gerados.

   Uma seleção de [Tipos de campos](#field-types) são usados para criar campos com base em como você configura o Modelo de fragmento de conteúdo. Os nomes de campo são retirados do **Nome da propriedade** do **Tipo de dados**.

   * Há também o **Renderizar como** propriedade a ser considerada, pois os usuários podem configurar determinados tipos de dados; por exemplo, como um texto de linha única ou um multicampo.

* GraphQL para AEM também gera um número de [campos auxiliares](#helper-fields).

   Eles são usados para identificar um Fragmento de conteúdo ou para obter mais informações sobre um fragmento de conteúdo.

### Tipos de campos {#field-types}

GraphQL para AEM oferece suporte a uma lista de tipos. Todos os tipos de dados do modelo de fragmento de conteúdo suportados e os tipos GraphQL correspondentes são representados:

| Modelo de fragmento de conteúdo - Tipo de dados | Tipo GraphQL | Descrição |
|--- |--- |--- |
| Texto de linha única | String, [String] |  Usado para strings simples, como nomes de autor, nomes de localização etc. |
| Texto de várias linhas | Sequência de caracteres |  Usado para saída de texto, como o corpo de um artigo |
| Número |  Flutuante, [Flutuar] | Usado para exibir números de ponto flutuante e números regulares |
| Booleano |  Booleano |  Usado para exibir caixas de seleção → declarações simples verdadeiras/falsas |
| Data E Hora | Calendário |  Usado para exibir data e hora em um formato ISO 8086. Dependendo do tipo selecionado, há três opções disponíveis para uso em GraphQL AEM: `onlyDate`, `onlyTime`, `dateTime` |
| Enumeração |  Sequência de caracteres |  Usado para exibir uma opção de uma lista de opções definidas na criação do modelo |
|  Tags |  [Sequência de caracteres] |  Usado para exibir uma lista de strings que representam tags usadas em AEM |
| Referência de conteúdo |  Sequência de caracteres |  Usado para exibir o caminho para outro ativo no AEM |
| Referência do fragmento |  *Um tipo de modelo* |  Usado para fazer referência a outro Fragmento de conteúdo de um determinado Tipo de modelo, definido quando o modelo foi criado |

### Campos de ajuda {#helper-fields}

Além dos tipos de dados para campos gerados pelo usuário, o GraphQL para AEM também gera vários *auxiliar* para ajudar a identificar um Fragmento de conteúdo ou fornecer informações adicionais sobre um Fragmento de conteúdo.

#### Caminho {#path}

O campo de caminho é usado como um identificador em GraphQL. Ele representa o caminho do ativo Fragmento de conteúdo dentro do repositório de AEM. Optamos por isso como o identificador de um fragmento de conteúdo, pois ele:

* é único no AEM,
* podem ser buscadas facilmente.

O código a seguir exibirá os caminhos de todos os Fragmentos de conteúdo que foram criados com base no Modelo do Fragmento de conteúdo `Person`.

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

Consulte [Exemplo de consulta - Um único fragmento de cidade específico](/help/headless/graphql-api/sample-queries.md#sample-single-specific-city-fragment).

#### Metadados {#metadata}

Por meio do GraphQL, o AEM também expõe os metadados de um Fragmento de conteúdo. Metadados são as informações que descrevem um fragmento de conteúdo, como o título de um fragmento de conteúdo, o caminho de miniatura, a descrição de um Fragmento de conteúdo, a data de criação, entre outros.

Como os metadados são gerados por meio do Editor de esquemas e, como tal, não têm uma estrutura específica, a variável `TypedMetaData` O tipo GraphQL foi implementado para expor os metadados de um Fragmento de conteúdo. `TypedMetaData` expõe as informações agrupadas pelos seguintes tipos escalares:

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

Cada tipo escalar representa um único par de nome-valor ou uma matriz de pares de nome-valor, onde o valor desse par é do tipo em que foi agrupado.

Por exemplo, se você quiser recuperar o título de um Fragmento de conteúdo, sabemos que essa propriedade é uma propriedade de String, portanto, consultaríamos todos os Metadados de String:

Para consultar metadados:

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

Você pode exibir todos os tipos de metadados GraphQL se exibir o esquema GraphQL gerado. Todos os tipos de modelo têm o mesmo `TypedMetaData`.

>[!NOTE]
>
>**Diferença entre metadados normais e de matriz**
>Lembre-se `StringMetadata` e `StringArrayMetadata` ambos se referem ao que é armazenado no repositório, não a como você os recupera.
>
>Por exemplo, chamando a função `stringMetadata` , você receberia uma matriz de todos os metadados que foram armazenados no repositório como um `String` e se você chamar `stringArrayMetadata` você receberia uma matriz de todos os metadados que foram armazenados no repositório como `String[]`.

Consulte [Exemplo de consulta para metadados - Lista os metadados para prêmios denominados GB](/help/headless/graphql-api/sample-queries.md#sample-metadata-awards-gb).

#### Variações {#variations}

O `_variations` O campo foi implementado para simplificar a consulta das variações que um Fragmento de conteúdo tem. Por exemplo:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Consulte [Consulta de exemplo - Todas as cidades com uma variável nomeada](/help/headless/graphql-api/sample-queries.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## Variáveis GraphQL {#graphql-variables}

GraphQL permite que as variáveis sejam colocadas no query. Para obter mais informações, você pode visualizar o [Documentação GraphQL para variáveis](https://graphql.org/learn/queries/#variables).

Por exemplo, para obter todos os Fragmentos de conteúdo do tipo `Article` que tenham uma variação específica, você pode especificar a variável `variation` em GraphiQL.

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

No GraphQL há uma possibilidade de alterar o query com base em variáveis, chamadas de Diretivas GraphQL.

Por exemplo, é possível incluir a variável `adventurePrice` em uma consulta para todas as `AdventureModels`, com base em uma variável `includePrice`.

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

Você também pode usar a filtragem em consultas GraphQL para retornar dados específicos.

A filtragem usa uma sintaxe baseada em operadores lógicos e expressões.

Por exemplo, a consulta a seguir (básica) filtra todas as pessoas que têm um nome de `Jobs` ou `Smith`:

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

* detalhes da [GraphQL para extensões de AEM](#graphql-extensions)

* [Consultas de exemplo usando este conteúdo e estrutura de amostra](/help/headless/graphql-api/sample-queries.md#graphql-sample-queries-sample-content-fragment-structure)

   * E o [Conteúdo e estrutura de amostra](/help/headless/graphql-api/sample-queries.md#content-fragment-structure-graphql) preparado para uso em consultas de amostra

* [Consultas de exemplo com base no projeto WKND](/help/headless/graphql-api/sample-queries.md#sample-queries-using-wknd-project)

## GraphQL para AEM - Resumo das extensões {#graphql-extensions}

A operação básica de consultas com GraphQL para AEM adere à especificação GraphQL padrão. Para consultas GraphQL com AEM, há algumas extensões:

* Se você precisar de um único resultado:
   * Utilizar o nome do modelo; cidade eg

* Se você espera uma lista de resultados:
   * adicionar `List` ao nome do modelo; por exemplo,  `cityList`
   * Consulte [Consulta de exemplo - Todas as informações sobre todas as cidades](#sample-all-information-all-cities)

* Se quiser usar um OR lógico:
   * use ` _logOp: OR`
   * Consulte [Consulta de amostra - Todas as pessoas com o nome de &quot;Trabalhos&quot; ou &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* AND lógico também existe, mas está (muitas vezes) implícito

* Você pode consultar nomes de campos que correspondem aos campos no Modelo de fragmento de conteúdo
   * Consulte [Exemplo de consulta - Detalhes completos do CEO e funcionários de uma empresa](#sample-full-details-company-ceos-employees)

* Além dos campos do modelo, há alguns campos gerados pelo sistema (precedidos pelo sublinhado ):

   * Para conteúdo:

      * `_locale` : Revelar a língua; com base no Gerenciador de idiomas
         * Consulte [Consulta de amostra para vários Fragmentos de conteúdo de uma determinada localidade](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : para revelar metadados para o fragmento
         * Consulte [Exemplo de consulta para metadados - Lista os metadados para prêmios denominados GB](#sample-metadata-awards-gb)
      * `_model` : permitir consulta para um Modelo de fragmento de conteúdo (caminho e título)
         * Consulte [Exemplo de consulta para um modelo de fragmento de conteúdo de um modelo](#sample-wknd-content-fragment-model-from-model)
      * `_path` : o caminho para o Fragmento do conteúdo no repositório
         * Consulte [Exemplo de consulta - Um único fragmento de cidade específico](#sample-single-specific-city-fragment)
      * `_reference` : revelar referências; incluindo referências em linha no Editor de Rich Text
         * Consulte [Exemplo de consulta para vários fragmentos de conteúdo com referências previamente buscadas](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : para revelar variações específicas no Fragmento de conteúdo
         * Consulte [Consulta de exemplo - Todas as cidades com uma variável nomeada](#sample-cities-named-variation)
   * E operações:

      * `_operator` : Aplicar operadores específicos; `EQUALS`, `EQUALS_NOT`, `GREATER_EQUAL`, `LOWER`, `CONTAINS`, `STARTS_WITH`
         * Consulte [Consulta de Amostra - Todas as Pessoas que não têm um nome de &quot;Trabalhos&quot;](#sample-all-persons-not-jobs)
         * Consulte [Consulta de exemplo - Todas as Aventuras em que o `_path` começa com um prefixo específico](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : Aplicar condições específicas; por exemplo,  `AT_LEAST_ONCE`
         * Consulte [Consulta de amostra - Filtrar em uma matriz com um item que deve ocorrer pelo menos uma vez](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : para ignorar o caso ao consultar
         * Consulte [Consulta de exemplo - Todas as cidades com SAN no nome, independentemente do caso](#sample-all-cities-san-ignore-case)









* Os tipos de união GraphQL são suportados:

   * use `... on`
      * Consulte [Exemplo de consulta para um fragmento de conteúdo de um modelo específico com uma referência de conteúdo](#sample-wknd-fragment-specific-model-content-reference)

* Fallback ao consultar fragmentos aninhados:

   * Se uma determinada variação não existir em um fragmento aninhado, a variável **Principal** seria retornada.

## Consultando o ponto de extremidade GraphQL de um site externo {#query-graphql-endpoint-from-external-website}

Para acessar o ponto de extremidade GraphQL de um site externo, é necessário configurar o:

* [Filtro CORS](/help/headless/deployment/cross-origin-resource-sharing.md)
* [Filtro referenciador](/help/headless/deployment/referrer-filter.md)

## Autenticação {#authentication}

Consulte [Autenticação para consultas GraphQL de AEM Remotas em Fragmentos de Conteúdo](/help/headless/security/authentication.md).

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## Perguntas frequentes {#faqs}

Questões que surgiram:

1. **Q**: &quot;*Como a API GraphQL para AEM diferente da API do Query Builder?*&quot;

   * **A**: &quot;*A API GraphQL da AEM oferece controle total sobre a saída JSON e é um padrão do setor para consulta de conteúdo.
A partir de agora, o AEM planeja investir na API GraphQL AEM.*&quot;

## Tutorial - Introdução ao AEM Headless e GraphQL {#tutorial}

Procurando um tutorial prático? Veja [Introdução ao AEM Headless e GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) Tutorial completo que ilustra como criar e expor conteúdo usando as APIs GraphQL da AEM e consumido por um aplicativo externo, em um cenário de CMS sem cabeçalho.
