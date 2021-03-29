---
title: AEM API GraphQL para uso com Fragmentos de conteúdo
description: Saiba como usar os Fragmentos de conteúdo no Adobe Experience Manager (AEM) como Cloud Service com a API GraphQL AEM para entrega de conteúdo sem periféricos.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '3253'
ht-degree: 1%

---


# AEM API GraphQL para uso com Fragmentos de conteúdo {#graphql-api-for-use-with-content-fragments}

Saiba como usar os Fragmentos de conteúdo no Adobe Experience Manager (AEM) como Cloud Service com a API GraphQL AEM para entrega de conteúdo sem periféricos.

AEM como uma API GraphQL do Cloud Service usada com Fragmentos de conteúdo é altamente baseada na API GraphQL de código aberto padrão.

Usar a API GraphQL no AEM permite a entrega eficiente dos Fragmentos de conteúdo aos clientes JavaScript em implementações CMS sem periféricos:

* Evitar solicitações de API iterativas como com REST,
* Garantir que a entrega se limite aos requisitos específicos,
* Permite a entrega em massa do exatamente o que é necessário para renderização como resposta a uma única consulta de API.

>[!NOTE]
>
>O GraphQL é usado atualmente em dois cenários (separados) no Adobe Experience Manager (AEM) como Cloud Service:
>
>* [O AEM Commerce consome dados de uma plataforma do Commerce via GraphQL](/help/commerce-cloud/architecture/magento.md).
>* AEM Fragmentos de conteúdo trabalham com a API GraphQL AEM (uma implementação personalizada, com base no GraphQL padrão), para fornecer conteúdo estruturado para uso em seus aplicativos.


## A API GraphQL {#graphql-api}

GraphQL é:

* &quot;*...um idioma de consulta para APIs e um tempo de execução para realizar essas consultas com seus dados existentes. O GraphQL fornece uma descrição completa e compreensível dos dados em sua API, fornece aos clientes o poder de solicitar exatamente o que precisam e nada mais, facilita a evolução das APIs ao longo do tempo e permite ferramentas poderosas de desenvolvedor.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

* &quot;*...uma especificação aberta para uma camada de API flexível. Coloque GraphQL sobre seus back-end existentes para criar produtos mais rápido do que nunca....*&quot;.

   Consulte [Explorar GraphQL](https://www.graphql.com).

* *&quot;...uma linguagem de consulta de dados e especificação desenvolvidas internamente pelo Facebook em 2012 antes de serem disponibilizadas publicamente em 2015. Ele oferece uma alternativa às arquiteturas baseadas em REST com o objetivo de aumentar a produtividade do desenvolvedor e minimizar as quantidades de dados transferidos. GraphQL é usado na produção por centenas de organizações de todos os tamanhos...&quot;*

   Consulte [Base GraphQL](https://foundation.graphql.org/).

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

Para obter mais informações sobre a API GraphQL, consulte as seguintes seções (entre muitos outros recursos):

* Em [grafql.org](https://graphql.org):

   * [Introdução ao GraphQL](https://graphql.org/learn)

   * [A especificação GraphQL](http://spec.graphql.org/)

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

* **[Endpoint GraphQL](#graphql-aem-endpoint)**
   * O caminho no AEM que responde a consultas GraphQL e fornece acesso aos esquemas GraphQL.

   * Consulte [Ativar o Ponto de Extremidade GraphQL](#enabling-graphql-endpoint) para obter mais detalhes.

Consulte a [(GraphQL.org) Introdução ao GraphQL](https://graphql.org/learn/) para obter detalhes abrangentes, incluindo as [Práticas recomendadas](https://graphql.org/learn/best-practices/).

### Tipos de consulta GraphQL {#graphql-query-types}

Com GraphQL, você pode executar consultas para retornar:

* Uma **entrada única**

* Uma **[lista de entradas](https://graphql.org/learn/schema/#lists-and-non-null)**

<!--
You can also perform:

* [Persisted Queries, that are cached](#persisted-queries-caching)
-->

## GraphQL para AEM Endpoint {#graphql-aem-endpoint}

O endpoint é o caminho usado para acessar GraphQL para AEM. Usando esse caminho você (ou seu aplicativo) pode:

* acesse o esquema GraphQL,
* enviar suas consultas GraphQL,
* receba as respostas (para suas consultas GraphQL).

O caminho do repositório de GraphQL para AEM ponto de extremidade é:

`/content/cq:graphql/global/endpoint`

Seu aplicativo pode usar o seguinte caminho no URL da solicitação:

`/content/_cq_graphql/global/endpoint.json`

Para ativar o ponto de extremidade para GraphQL para AEM, é necessário:

>[!CAUTION]
>
>Essas etapas podem mudar em breve.

* [Ativar o terminal GraphQL](#enabling-graphql-endpoint)
* [Executar configurações adicionais](#additional-configurations-graphql-endpoint)

### Ativando seu ponto de extremidade GraphQL {#enabling-graphql-endpoint}

>[!NOTE]
>
>Consulte [Supporting Packages](#supporting-packages) para obter detalhes dos pacotes que o Adobe fornece para ajudar a simplificar essas etapas.

Para ativar consultas GraphQL no AEM, crie um terminal em `/content/cq:graphql/global/endpoint`:

* Os nós `cq:graphql` e `global` devem ser do tipo `sling:Folder`.
* O nó `endpoint` deve ser do tipo `nt:unstructured` e conter um `sling:resourceType` de `graphql/sites/components/endpoint`.

>[!CAUTION]
>
>O endpoint é acessível a todos. Isso pode - especialmente em instâncias de publicação - causar uma preocupação de segurança, já que as consultas GraphQL podem impor uma carga pesada no servidor.
>
>Você pode configurar ACLs, apropriadas ao seu caso de uso, no terminal.

>[!NOTE]
>
>Seu terminal não funcionará imediatamente. Será necessário fornecer [Configurações adicionais para o Ponto de extremidade GraphQL](#additional-configurations-graphql-endpoint) separadamente.

>[!NOTE]
>Além disso, você pode testar e depurar consultas GraphQL usando o [GraphiQL IDE](#graphiql-interface).

### Configurações adicionais para o ponto de extremidade GraphQL {#additional-configurations-graphql-endpoint}

>[!NOTE]
>
>Consulte [Supporting Packages](#supporting-packages) para obter detalhes dos pacotes que o Adobe fornece para ajudar a simplificar essas etapas.

Configurações adicionais são necessárias:

* Dispatcher:
   * Para permitir URLs necessários
   * Obrigatório
* URL personalizada:
   * Para alocar um URL simplificado para o endpoint
   * Opcional

### Suporte para pacotes {#supporting-packages}

Para simplificar a configuração de um ponto de extremidade GraphQL, o Adobe fornece o pacote [GraphQL Sample Project (2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphql-sample1.zip).

Este arquivo contém [a configuração adicional necessária](#additional-configurations-graphql-endpoint) e [o ponto de extremidade GraphQL](#enabling-graphql-endpoint). Se instalado em uma instância de AEM simples, ele exporá um ponto de extremidade GraphQL em funcionamento completo em `/content/cq:graphql/global/endpoint`.

Este pacote deve ser um blueprint para seus próprios projetos GraphQL. Consulte o pacote **README** para obter detalhes sobre como usar o pacote.

Se você preferir criar manualmente a configuração necessária, o Adobe também fornece um [Pacote de Conteúdo de Ponto de Extremidade GraphQL](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faemcloud%2Fpublic%2Faem-graphql%2Fgraphql-global-endpoint.zip) dedicado. Este pacote de conteúdo contém somente o ponto de extremidade GraphQL, sem qualquer configuração.

## Interface GraphiQL {#graphiql-interface}

<!--
AEM Graph API includes an implementation of the standard [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) interface. This allows you to directly input, and test, queries.
-->

Uma implementação da interface [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) padrão está disponível para uso com AEM GraphQL. Pode ser [instalado com AEM](#installing-graphiql-interface).

Essa interface permite que você insira e teste diretamente consultas.

Por exemplo:

* `http://localhost:4502/content/graphiql.html`

Isso fornece recursos como realce de sintaxe, preenchimento automático, sugestão automática, juntamente com um histórico e documentação online:

![Interface GraphiQL ](assets/cfm-graphiql-interface.png "InterfaceInterface GraphiQL")

### Instalação da interface GraphiQL AEM {#installing-graphiql-interface}

A interface do usuário GraphiQL pode ser instalada no AEM com um pacote dedicado: o pacote [Pacote de Conteúdo GraphiQL v0.0.6 (2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip).

<!--
See the package **README** for full details; including full details of how it can be installed on an AEM instance - in a variety of scenarios.
-->

## Casos de uso para ambientes de autor e publicação {#use-cases-author-publish-environments}

Os casos de uso podem depender do tipo de AEM como um ambiente de Cloud Service:

* Ambiente de publicação; usado para:
   * Dados de consulta para aplicativo JS (caso de uso padrão)

* Ambiente de criação; usado para:
   * Consultar dados para &quot;fins de gerenciamento de conteúdo&quot;:
      * No momento, a GraphQL no AEM as a Cloud Service é uma API somente leitura.
      * A REST API pode ser usada para operações de CR(u)D.

## Permissões  {#permission}

As permissões são as necessárias para acessar o Assets.

## Geração de esquema {#schema-generation}

GraphQL é uma API altamente digitada, o que significa que os dados devem ser estruturados e organizados claramente por tipo.

A especificação GraphQL fornece uma série de diretrizes sobre como criar uma API robusta para interrogar dados em uma determinada instância. Para fazer isso, um cliente precisa buscar o [Schema](#schema-generation), que contém todos os tipos necessários para um query.

Para Fragmentos de conteúdo, os esquemas GraphQL (estrutura e tipos) são baseados em **Ativado** [Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) e seus tipos de dados.

>[!CAUTION]
>
>Todos os esquemas GraphQL (derivados dos Modelos de fragmento de conteúdo que foram **Enabled**) podem ser lidos pelo ponto de extremidade GraphQL.
>
>Isso significa que você precisa garantir que não haja dados confidenciais disponíveis, pois eles poderiam ser vazados dessa forma; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.

Por exemplo, se um usuário criou um Modelo de fragmento de conteúdo chamado `Article`, AEM gera o objeto `article` que é do tipo `ArticleModel`. Os campos desse tipo correspondem aos campos e tipos de dados definidos no modelo.

1. Um modelo de fragmento de conteúdo:

   ![Modelo de fragmento de conteúdo para uso com o ](assets/cfm-graphqlapi-01.png "GraphQLContent Fragment Model para uso com GraphQL")

1. O esquema GraphQL correspondente (saída da documentação automática GraphiQL):
   ![Esquema GraphQL com base no ](assets/cfm-graphqlapi-02.png "modelo de fragmento de conteúdoGraphQL com base no modelo de fragmento de conteúdo")

   Isso mostra que o tipo gerado `ArticleModel` contém vários [campos](#fields).

   * Três delas foram controladas pelo usuário: `author`, `main` e `referencearticle`.

   * Os outros campos foram adicionados automaticamente por AEM e representam métodos úteis para fornecer informações sobre um determinado Fragmento de conteúdo; neste exemplo, `_path`, `_metadata`, `_variations`. Esses [campos auxiliares](#helper-fields) são marcados com um `_` anterior para distinguir entre o que foi definido pelo usuário e o que foi gerado automaticamente.

1. Depois que um usuário cria um Fragmento de conteúdo com base no modelo de Artigo, ele pode ser interrogado por meio de GraphQL. Para obter exemplos, consulte as [Consultas de amostra](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries) (com base em uma [estrutura de fragmento de conteúdo de amostra para usar com GraphQL](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)).

No GraphQL para AEM, o esquema é flexível. Isso significa que ele é gerado automaticamente cada vez que um Modelo de fragmento de conteúdo é criado, atualizado ou excluído. Os caches de esquema de dados também são atualizados quando você atualiza um Modelo de fragmento de conteúdo.

<!--
>[!NOTE]
>
>AEM does not use the concept of namespacing for Content Fragment Models. 
>
>If required, you can edit the **[GraphQL](/help/assets/content-fragments/content-fragments-models.md#content-fragment-model-properties)** properties of a Model to assign specific names.
-->

O serviço GraphQL do Sites escuta (em segundo plano) quaisquer modificações feitas em um Modelo de fragmento de conteúdo. Quando as atualizações são detectadas, somente essa parte do esquema é regenerada. Essa otimização economiza tempo e oferece estabilidade.

Por exemplo, se você:

1. Instale um pacote contendo `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. Os tipos GraphQL para `Model-1` e `Model-2` serão gerados.

1. Em seguida, modifique `Content-Fragment-Model-2`:

   1. Somente o tipo GraphQL `Model-2` será atualizado.

   1. Enquanto `Model-1` permanecerá o mesmo.

>[!NOTE]
>
>Isso é importante observar caso queira fazer atualizações em massa nos Modelos de fragmento de conteúdo por meio da api REST ou de outra forma.

O esquema é distribuído por meio do mesmo terminal que as consultas GraphQL, com o cliente lidando com o fato de que o esquema é chamado com a extensão `GQLschema`. Por exemplo, executar uma solicitação `GET` simples em `/content/cq:graphql/global/endpoint.GQLschema` resultará na saída do schema com o Tipo de conteúdo: `text/x-graphql-schema;charset=iso-8859-1`.

### Geração de esquema - Modelos não publicados {#schema-generation-unpublished-models}

Quando os Fragmentos de conteúdo são aninhados, pode acontecer que um Modelo de fragmento de conteúdo principal seja publicado, mas um modelo referenciado não é.

>[!NOTE]
>
>A interface do usuário do AEM impede que isso aconteça, mas se a publicação for feita de forma programática ou com pacotes de conteúdo, ela poderá ocorrer.

Quando isso acontece, o AEM gera um esquema *incompleto* para o modelo de fragmento de conteúdo pai. Isso significa que a Referência do fragmento, que depende do modelo não publicado, é removida do esquema.

## Fields {#fields}

Dentro do schema há campos individuais, de duas categorias básicas:

* Campos gerados.

   Uma seleção de [Tipos de campo](#field-types) é usada para criar campos com base em como você configura o Modelo de fragmento de conteúdo. Os nomes de campo são obtidos do campo **Nome da propriedade** do **Tipo de dados**.

   * Também há a propriedade **Renderizar como** a ser levada em consideração, pois os usuários podem configurar determinados tipos de dados; por exemplo, como um texto de linha única ou um multicampo.

* GraphQL para AEM também gera vários [campos auxiliares](#helper-fields).

   Eles são usados para identificar um Fragmento de conteúdo ou para obter mais informações sobre um fragmento de conteúdo.

### Tipos de campo {#field-types}

GraphQL para AEM oferece suporte a uma lista de tipos. Todos os tipos de dados do modelo de fragmento de conteúdo suportados e os tipos GraphQL correspondentes são representados:

| Modelo de fragmento de conteúdo - Tipo de dados | Tipo GraphQL | Descrição |
|--- |--- |--- |
| Texto de linha única | String, [String] |  Usado para strings simples, como nomes de autor, nomes de localização etc. |
| Texto de várias linhas | Sequência de caracteres |  Usado para saída de texto, como o corpo de um artigo |
| Número |  Flutuante, [Flutuante] | Usado para exibir números de ponto flutuante e números regulares |
| Booleano |  Booleano |  Usado para exibir caixas de seleção → declarações simples verdadeiras/falsas |
| Data E Hora | Calendário |  Usado para exibir data e hora em um formato ISO 8086 |
| Enumeração |  Sequência de caracteres |  Usado para exibir uma opção de uma lista de opções definidas na criação do modelo |
|  Tags |  [Sequência de caracteres] |  Usado para exibir uma lista de strings que representam tags usadas em AEM |
| Referência de conteúdo |  Sequência de caracteres |  Usado para exibir o caminho para outro ativo no AEM |
| Referência do fragmento |  *Um tipo de modelo* |  Usado para fazer referência a outro Fragmento de conteúdo de um determinado Tipo de modelo, definido quando o modelo foi criado |

### Campos de ajuda {#helper-fields}

Além dos tipos de dados para campos gerados pelo usuário, o GraphQL para AEM também gera vários campos *helper* para ajudar a identificar um Fragmento de conteúdo ou para fornecer informações adicionais sobre um Fragmento de conteúdo.

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

Consulte [Exemplo de consulta - Um único fragmento de cidade específico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment).

#### Metadados {#metadata}

Por meio do GraphQL, o AEM também expõe os metadados de um Fragmento de conteúdo. Metadados são as informações que descrevem um fragmento de conteúdo, como o título de um fragmento de conteúdo, o caminho de miniatura, a descrição de um Fragmento de conteúdo, a data de criação, entre outros.

Como os metadados são gerados por meio do Editor de esquemas e, como tal, não têm uma estrutura específica, o tipo GraphQL `TypedMetaData` foi implementado para expor os metadados de um Fragmento de conteúdo. `TypedMetaData` expõe as informações agrupadas pelos seguintes tipos escalares:

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
>Lembre-se de que `StringMetadata` e `StringArrayMetadata` ambos se referem ao que é armazenado no repositório, não como você os recupera.
>
>Assim, por exemplo, ao chamar o campo `stringMetadata`, você receberia uma matriz de todos os metadados que foram armazenados no repositório como um `String` , e se chamar `stringArrayMetadata` você receberia uma matriz de todos os metadados que foram armazenados no repositório como `String[]`.

Consulte [Exemplo de consulta para metadados - Liste os metadados para prêmios denominados GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb).

#### Variações {#variations}

O campo `_variations` foi implementado para simplificar a consulta das variações que um Fragmento de conteúdo tem. Por exemplo:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

Consulte [Exemplo de consulta - Todas as cidades com uma variável nomeada](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation).

<!--
## Security Considerations {#security-considerations}
-->

## Variáveis GraphQL {#graphql-variables}

GraphQL permite que as variáveis sejam colocadas no query. Para obter mais informações, consulte a documentação de GraphQL para GraphiQL](https://graphql.org/learn/queries/#variables).[

Por exemplo, para obter todos os Fragmentos de conteúdo do tipo `Article` que têm uma variação específica, você pode especificar a variável `variation` em GraphiQL.

![Variáveis GraphQL ](assets/cfm-graphqlapi-03.png "Variáveis GraphQL")

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

Por exemplo, é possível incluir o campo `adventurePrice` em uma consulta para todos os `AdventureModels`, com base em uma variável `includePrice`.

![Diretivas GraphQL ](assets/cfm-graphqlapi-04.png "Diretivas GraphQL")

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

Por exemplo, a consulta a seguir (básica) filtra todas as pessoas que têm um nome `Jobs` ou `Smith`:

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

* detalhes do [GraphQL para extensões de AEM](#graphql-extensions)

* [Consultas de exemplo usando este conteúdo e estrutura de amostra](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * E o [Conteúdo e estrutura de amostra](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql) preparado para uso em consultas de amostra

* [Consultas de exemplo com base no projeto WKND](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## GraphQL para AEM - Resumo das extensões {#graphql-extensions}

A operação básica de consultas com GraphQL para AEM adere à especificação GraphQL padrão. Para consultas GraphQL com AEM, há algumas extensões:

* Se você precisar de um único resultado:
   * Utilizar o nome do modelo; cidade eg

* Se você espera uma lista de resultados:
   * adicionar `List` ao nome do modelo; por exemplo, `cityList`
   * Consulte [Exemplo de consulta - Todas as informações sobre todas as cidades](#sample-all-information-all-cities)

* Se quiser usar um OR lógico:
   * use ` _logOp: OR`
   * Consulte [Exemplo de Consulta - Todas as Pessoas que têm o nome de &quot;Trabalhos&quot; ou &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* AND lógico também existe, mas está (muitas vezes) implícito

* Você pode consultar nomes de campos que correspondem aos campos no Modelo de fragmento de conteúdo
   * Consulte [Exemplo de consulta - Detalhes completos do CEO e funcionários de uma empresa](#sample-full-details-company-ceos-employees)

* Além dos campos do modelo, há alguns campos gerados pelo sistema (precedidos pelo sublinhado ):

   * Para conteúdo:

      * `_locale` : Revelar a língua; com base no Gerenciador de idiomas
         * Consulte [Exemplo de consulta para vários fragmentos de conteúdo de uma determinada localidade](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : para revelar metadados para o fragmento
         * Consulte [Exemplo de consulta para metadados - Liste os metadados para prêmios denominados GB](#sample-metadata-awards-gb)
      * `_model` : permitir consulta para um Modelo de fragmento de conteúdo (caminho e título)
         * Consulte [Exemplo de consulta para um modelo de fragmento de conteúdo de um modelo](#sample-wknd-content-fragment-model-from-model)
      * `_path` : o caminho para o Fragmento do conteúdo no repositório
         * Consulte [Exemplo de consulta - Um único fragmento de cidade específico](#sample-single-specific-city-fragment)
      * `_reference` : revelar referências; incluindo referências em linha no Editor de Rich Text
         * Consulte [Exemplo de consulta para vários fragmentos de conteúdo com referências pré-buscadas](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : para revelar variações específicas no Fragmento de conteúdo
         * Consulte [Exemplo de consulta - Todas as cidades com uma variável nomeada](#sample-cities-named-variation)
   * E operações:

      * `_operator` : Aplicar operadores específicos;  `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`,  `STARTS_WITH`
         * Consulte [Consulta de Amostra - Todas as Pessoas que não têm um nome &quot;Trabalhos&quot;](#sample-all-persons-not-jobs)
         * Consulte [Exemplo de consulta - Todas as empresas onde o `_path` começa com um prefixo específico](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : Aplicar condições específicas; por exemplo,   `AT_LEAST_ONCE`
         * Consulte [Exemplo de consulta - Filtrar em uma matriz com um item que deve ocorrer pelo menos uma vez](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : para ignorar o caso ao consultar
         * Consulte [Exemplo de consulta - Todas as cidades com SAN no nome, independentemente do caso](#sample-all-cities-san-ignore-case)










* Os tipos de união GraphQL são suportados:

   * use `... on`
      * Consulte [Exemplo de consulta para um fragmento de conteúdo de um modelo específico com uma referência de conteúdo](#sample-wknd-fragment-specific-model-content-reference)

<!--
## Persisted Queries (Caching) {#persisted-queries-caching}

After preparing a query with a POST request, it can be executed with a GET request that can be cached by HTTP caches or a CDN.

This is required as POST queries are usually not cached, and if using GET with the query as a parameter there is a significant risk of the parameter becoming too large for HTTP services and intermediates.

Here are the steps required to persist a given query:

>[!NOTE]
>Prior to this the **GraphQL Persistence Queries** need to be enabled, for the appropriate configuration. See [Enable Content Fragment Functionality in Configuration Browser](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) for more details.

1. Prepare the query by PUTing it to the new endpoint URL `/graphql/persist.json/<config>/<persisted-label>`.

   For example, create a persisted query:

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

1. At this point, check the response.

   For example, check for success:

     ```xml
     {
       "action": "create",
       "configurationName": "wknd",
       "name": "plain-article-query",
       "shortPath": "/wknd/plain-article-query",
       "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
     }
     ```

1. You can then replay the persisted query by GETing the URL `/graphql/execute.json/<shortPath>`.

   For example, use the persisted query:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Update a persisted query by POSTing to an already existing query path.

   For example, use the persisted query:

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

1. Create a wrapped plain query.

   For example:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Create a wrapped plain query with cache control.

   For example:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Create a persisted query with parameters:

   For example:

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

1. Executing a query with parameters.

   For example:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"

   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. To execute the query on publish, the related persist tree need to replicated

   * Using a POST for replication:

     ```xml
     $curl -X POST   http://localhost:4502/bin/replicate.json \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
       -F cmd=activate
     ```

   * Using a package:
     1. Create a new package definition.
     1. Include the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).
     1. Build the package.
     1. Replicate the package.

   * Using replication/distribution tool.
     1. Go to the Distribution tool.
     1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

   * Using a workflow (via workflow launcher configuration):
     1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).

1. Once the query configuration is on publish, the same principles apply, just using the publish endpoint.

   >[!NOTE]
   >
   >For anonymous access the system assumes that the ACL allows "everyone" to have access to the query configuration.
   >
   >If that is not the case it will not be able to execute.

   >[!NOTE]
   >
   >Any semicolons (";") in the URLs need to be encoded.
   >
   >For example, as in the request to Execute a persisted query:
   >
   >```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```
-->

## Consultando o ponto de extremidade GraphQL de um site externo {#query-graphql-endpoint-from-external-website}

Para acessar o ponto de extremidade GraphQL de um site externo, é necessário configurar o:

* [Filtro CORS](#cors-filter)
* [Filtro referenciador](#referrer-filter)

### Filtro CORS {#cors-filter}

>[!NOTE]
>
>Para obter uma visão geral detalhada da política de compartilhamento de recursos do CORS em AEM consulte [Entender o compartilhamento de recursos entre origens (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors)).

Para acessar o ponto de extremidade GraphQL, uma política CORS deve ser configurada no repositório Git do cliente. Isso é feito adicionando um arquivo de configuração de CORS OSGi apropriado para os endpoints desejados.

Essa configuração deve especificar uma origem de site confiável `alloworigin` ou `alloworiginregexp` para a qual o acesso deve ser concedido.

<!--
For example, to grant access to the GraphQL endpoint and persisted queries endpoint for `https://my.domain` you can use:
-->

Por exemplo, para conceder acesso ao ponto de extremidade GraphQL para `https://my.domain` você pode usar:

<!--
```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```
-->

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json"
  ]
}
```

Se você tiver configurado um caminho personalizado para o endpoint, também poderá usá-lo em `allowedpaths`.

### Filtro de referência {#referrer-filter}

Além da configuração do CORS, um filtro Referenciador deve ser configurado para permitir acesso de hosts de terceiros.

Isso é feito adicionando um arquivo de configuração do Filtro de referenciador OSGi apropriado que:

* especifica um nome de host de site confiável; `allow.hosts` ou `allow.hosts.regexp`,
* concede acesso a esse nome de host.

Por exemplo, para conceder acesso a solicitações com o Referenciador `my.domain` você pode:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Continua a ser responsabilidade do cliente:
>
>* conceder acesso somente a domínios confiáveis
>* certifique-se de que nenhuma informação sensível seja exposta
>* não use uma sintaxe curinga [*]; isso desativará o acesso autenticado ao ponto de extremidade GraphQL e também o exporá ao mundo inteiro.


>[!CAUTION]
>
>Todos os esquemas GraphQL [](#schema-generation) (derivados dos Modelos de Fragmento de Conteúdo que foram **Ativado**) podem ser lidos pelo ponto de extremidade GraphQL.
>
>Isso significa que você precisa garantir que não haja dados confidenciais disponíveis, pois eles poderiam ser vazados dessa forma; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.

## Autenticação {#authentication}

Consulte [Autenticação para consultas GraphQL de AEM Remotas em Fragmentos de Conteúdo](/help/assets/content-fragments/graphql-authentication-content-fragments.md).

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

1. **P**: &quot;*Como a API GraphQL para AEM diferente da API do Query Builder?*&quot;

   * **A**: &quot;*A API GraphQL da AEM oferece controle total sobre a saída JSON e é um padrão do setor para consulta de conteúdo.
A partir de agora, AEM planeja investir na API GraphQL AEM.*&quot;

## Tutorial - Introdução ao AEM Headless e GraphQL {#tutorial}

Procurando um tutorial prático? Confira o [Introdução ao AEM Headless e o tutorial GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) completo ilustrando como criar e expor conteúdo usando as APIs GraphQL da AEM e consumidas por um aplicativo externo, em um cenário de CMS sem periféricos.
