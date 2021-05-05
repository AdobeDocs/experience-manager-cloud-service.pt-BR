---
title: Como acessar seu conteúdo por meio AEM APIs de entrega
description: Nesta parte da Jornada do desenvolvedor sem cabeçalho do AEM, saiba como usar consultas GraphQL para acessar o conteúdo dos Fragmentos de conteúdo.
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 7b04ae2bfa75fe3d3af13271efe567a5fc401f49
workflow-type: tm+mt
source-wordcount: '4636'
ht-degree: 1%

---

# Como acessar seu conteúdo por meio AEM APIs de entrega {#access-your-content}

>[!CAUTION]
>
>TRABALHO EM ANDAMENTO - A criação deste documento está em curso e não deve ser entendida como completa ou definitiva, nem deve ser usada para fins de produção.

Nesta parte da [AEM Jornada de desenvolvedores headless,](overview.md) você pode aprender a usar consultas GraphQL para acessar o conteúdo dos Fragmentos de conteúdo.

## A história até agora {#story-so-far}

No documento anterior da jornada sem cabeçalho AEM, [Como modelar seu conteúdo](model-your-content.md) você aprendeu as noções básicas da modelagem de dados no AEM, portanto, agora você deve entender como modelar sua estrutura de conteúdo e perceber essa estrutura usando AEM Modelos de fragmento de conteúdo e Fragmentos de conteúdo:

* Reconhecer os conceitos e a terminologia relacionados à [modelagem de dados](#data-modeling).
* Entenda [por que a modelagem de dados é necessária para a entrega de conteúdo sem cabeçalho](#data-modeling-for-aem-headless).
* Entenda [como realizar essa estrutura usando AEM Modelos de fragmento de conteúdo](#create-structure-content-fragment-models) (e criar conteúdo com [Fragmentos de conteúdo](#use-content-to-author-content)).
* Entenda [como modelar seu conteúdo](#getting-started-examples); princípios com amostras básicas.

Este artigo se baseia nesses fundamentos para que você entenda como acessar o conteúdo headless existente no AEM usando a API GraphQL AEM.

* **Público-alvo**: Iniciante
* **Objetivo**: Saiba como acessar o conteúdo dos Fragmentos de conteúdo usando AEM consultas GraphQL:
   * Apresente GraphQL e a API GraphQL AEM.
   * Saiba mais sobre os detalhes da API GraphQL da AEM.
   * Observe algumas consultas de amostra para ver como as coisas funcionam na prática.

## Então, gostaria de acessar seus dados? {#so-youd-like-to-access-your-data}

Então...você tem todo esse conteúdo, perfeitamente estruturado (em Fragmentos de conteúdo) e apenas esperando para alimentar seu novo aplicativo. A questão é: como chegar lá?

O que você precisa é de uma maneira de direcionar conteúdo específico, selecionar o que precisa e retorná-lo ao seu aplicativo para processamento adicional.

Com o Adobe Experience Manager (AEM) as a Cloud Service, é possível acessar seletivamente os Fragmentos de conteúdo, usando a API GraphQL AEM, para retornar somente o conteúdo necessário. Isso significa que você pode realizar a entrega sem interface de conteúdo estruturado para uso em seus aplicativos.

>[!NOTE]
>
>AEM API GraphQL é uma implementação personalizada, com base no GraphQL padrão.

## GraphQL - Uma Introdução {#graphql-introduction}

GraphQL é uma especificação de código aberto que fornece:

* um idioma de consulta que permite selecionar conteúdo específico de objetos estruturados.
* um tempo de execução para realizar essas consultas com seu conteúdo estruturado.

GraphQL é uma API do tipo *strong*. Isso significa que o conteúdo *all* deve ser claramente estruturado e organizado por tipo, para que GraphQL *entenda* o que acessar e como. Os campos de dados são definidos em esquemas GraphQL, que definem a estrutura dos objetos de conteúdo.

Os pontos de extremidade GraphQL fornecem os caminhos que respondem às consultas GraphQL.

Tudo isso significa que seu aplicativo pode selecionar com precisão, confiabilidade e eficiência os dados de que precisa - exatamente o que você precisa quando usado com o AEM.

>[!NOTE]
>
>Consulte *GraphQL*.org e *GraphQL*.com.

## AEM e GraphQL {#aem-graphql}

GraphQL é usado em vários locais no AEM; por exemplo:

* Commerce
   * Há integrações GraphQL entre o AEM e várias soluções comerciais de terceiros, usadas com os ganchos de extensão fornecidos pelos Componentes principais da CIF.
* Fragmentos de conteúdo
   * Uma API personalizada foi desenvolvida para este caso de uso.
   * Esta é a API GraphQL AEM.

>[!NOTE]
>
>Essa etapa da Jornada sem cabeçalho só se refere à API GraphQL AEM e aos Fragmentos de conteúdo.

## AEM API GraphQL {#aem-graphql-api}

A API GraphQL da AEM é uma versão personalizada da API GraphQL padrão, especialmente configurada para permitir a execução de consultas (complexas) nos Fragmentos de conteúdo.

Fragmentos de conteúdo são usados, pois o conteúdo é estruturado de acordo com Modelos de fragmento de conteúdo. Isso atende a um requisito básico do GraphQL.

* Um Modelo de fragmento de conteúdo é composto de um ou mais campos.
   * Cada campo é definido de acordo com um Tipo de dados.
* Os Modelos de Fragmento de conteúdo são usados para gerar os Esquemas GraphQL AEM correspondentes.

Para realmente acessar GraphQL para AEM (e o conteúdo), um ponto de extremidade é usado para fornecer o caminho de acesso.

O conteúdo retornado, por meio da API GraphQL da AEM, pode ser usado pelos seus aplicativos.

>[!NOTE]
>
>A implementação AEM da API GraphQL é baseada nas bibliotecas GraphQL Java.

### Casos de uso para ambientes de autor e publicação {#use-cases-author-publish-environments}

Os casos de uso da API GraphQL da AEM podem depender do tipo de AEM como um ambiente de Cloud Service:

* Ambiente de publicação; usado para:
   * Dados de consulta para aplicativo JS (caso de uso padrão)

* Ambiente de criação; usado para:
   * Consultar dados para &quot;fins de gerenciamento de conteúdo&quot;:
      * No momento, a GraphQL no AEM as a Cloud Service é uma API somente leitura.
      * A REST API pode ser usada para operações de CR(u)D.

## Fragmentos de conteúdo para uso com a API GraphQL AEM {#content-fragments-use-with-aem-graphql-api}

Os Fragmentos de conteúdo podem ser usados como base para GraphQL para AEM schemas e consultas como:

* Eles permitem projetar, criar, preparar e publicar conteúdo independente da página.
* Elas são baseadas em um Modelo de fragmento de conteúdo, que predefine a estrutura do fragmento resultante por meio de tipos de dados definidos.
* É possível obter camadas adicionais de estrutura com o tipo de dados Referência de fragmento , disponível ao definir um modelo.

### Modelos de fragmentos do conteúdo {#content-fragments-models}

Esses modelos de fragmentos de conteúdo:

* São usados para gerar os Esquemas, uma vez **Enabled**.

* Forneça os tipos de dados e campos necessários para GraphQL. Eles garantem que seu aplicativo solicite apenas o que é possível e receba o que é esperado.

* O tipo de dados **Referências de fragmento** pode ser usado em seu modelo para fazer referência a outro Fragmento de conteúdo e, portanto, introduzir níveis adicionais de estrutura.

### Referências do fragmento {#fragment-references}

A **Referência do fragmento**:

* É de especial interesse em conjunto com GraphQL.

* É um tipo de dados específico que pode ser usado ao definir um Modelo de fragmento de conteúdo.

* Faz referência a outro fragmento, dependendo de um modelo de fragmento de conteúdo específico.

* Permite recuperar dados estruturados.

   * Quando definido como **multifeed**, vários subfragmentos podem ser referenciados (recuperados) pelo fragmento principal.

### Visualização JSON {#json-preview}

Para ajudar na criação e desenvolvimento dos Modelos de fragmento de conteúdo, é possível visualizar a saída JSON no Editor de fragmento de conteúdo.

## Geração de esquema GraphQL a partir dos fragmentos de conteúdo {#graphql-schema-generation-content-fragments}

GraphQL é uma API altamente digitada, o que significa que os dados devem ser estruturados e organizados claramente por tipo. A especificação GraphQL fornece uma série de diretrizes sobre como criar uma API robusta para interrogar dados em uma determinada instância. Para fazer isso, um cliente precisa buscar o Esquema, que contém todos os tipos necessários para uma consulta.

Para Fragmentos de conteúdo, os esquemas GraphQL (estrutura e tipos) são baseados em **Modelos de fragmento de conteúdo ativados** e seus tipos de dados.

>[!CAUTION]
>
>Todos os esquemas GraphQL (derivados dos Modelos de fragmento de conteúdo que foram **Enabled**) podem ser lidos pelo ponto de extremidade GraphQL.
>
>Isso significa que você precisa garantir que não haja dados confidenciais disponíveis, pois eles poderiam ser vazados dessa forma; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.

Por exemplo, se um usuário criou um Modelo de fragmento de conteúdo chamado `Article`, AEM gera o objeto `article` que é do tipo `ArticleModel`. Os campos desse tipo correspondem aos campos e tipos de dados definidos no modelo.

1. Um modelo de fragmento de conteúdo:

   ![Modelo de fragmento de conteúdo para uso com o ](assets/graphqlapi-cfmodel.png "GraphQLContent Fragment Model para uso com GraphQL")

1. O esquema GraphQL correspondente (saída da documentação automática GraphiQL):
   ![Esquema GraphQL com base no ](assets/graphqlapi-cfm-schema.png "modelo de fragmento de conteúdoGraphQL com base no modelo de fragmento de conteúdo")

   Isso mostra que o tipo gerado `ArticleModel` contém vários [campos](#fields).

   * Três delas foram controladas pelo usuário: `author`, `main` e `referencearticle`.

   * Os outros campos foram adicionados automaticamente por AEM e representam métodos úteis para fornecer informações sobre um determinado Fragmento de conteúdo; neste exemplo, `_path`, `_metadata`, `_variations`. Esses [campos auxiliares](#helper-fields) são marcados com um `_` anterior para distinguir entre o que foi definido pelo usuário e o que foi gerado automaticamente.

1. Depois que um usuário cria um Fragmento de conteúdo com base no modelo de Artigo, ele pode ser interrogado por meio de GraphQL. Para obter exemplos, consulte a Amostra de consultas.md#grafql-sample-queries) (com base em uma amostra da estrutura do Fragmento de conteúdo para ser usada com GraphQL.

No GraphQL para AEM, o esquema é flexível. Isso significa que ele é gerado automaticamente cada vez que um Modelo de fragmento de conteúdo é criado, atualizado ou excluído. Os caches de esquema de dados também são atualizados quando você atualiza um Modelo de fragmento de conteúdo.

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

## Pontos finais GraphQL AEM {#aem-graphql-endpoints}

<!--
need details/examples
-->

Um endpoint é o caminho usado para acessar GraphQL para AEM. Usando esse caminho você (ou seu aplicativo) pode:

* acessar os esquemas GraphQL,
* enviar suas consultas GraphQL,
* receba as respostas (para suas consultas GraphQL).

AEM permite:

* Um endpoint global - disponível para uso por todos os sites.
* Endpoints do locatário - que você pode configurar, específicos de um site/projeto especificado.

## Permissões  {#permissions}

As permissões são as necessárias para acessar o Assets.

## A interface GraphiQL AEM {#aem-graphiql-interface}

Para ajudá-lo a inserir diretamente e testar consultas, uma implementação da interface GraphiQL padrão está disponível para uso com AEM GraphQL. Isso pode ser instalado com AEM.

Ele fornece recursos como realce de sintaxe, preenchimento automático, sugestão automática, juntamente com um histórico e documentação online.

![Interface GraphiQL ](assets/graphiql-interface.png "InterfaceInterface GraphiQL")

<!--
new page?
-->

## Uso da API GraphQL AEM {#using-aem-graphiql}

### Endpoints {#endpoints}

O caminho do repositório do GraphQL para AEM endpoint global é:

`/content/cq:graphql/global/endpoint`

Para o qual seu aplicativo pode usar o seguinte caminho no URL da solicitação:

`/content/_cq_graphql/global/endpoint.json`

Para um terminal de locatário, os caminhos são comparáveis:

`/content/cq:graphql/your-tenant/endpoint`
`/content/_cq_graphql/your-tenant/endpoint.json`

Antes de usar, todos os pontos de extremidade devem estar habilitados. Para ativar um terminal, global ou locatário, para o GraphQL para AEM é necessário:

* Ativar o terminal GraphQL
* Publicar seu terminal

>[!CAUTION]
>
>O Editor de fragmento de conteúdo pode permitir que um Fragmento de conteúdo de um locatário faça referência a um Fragmento de conteúdo de outro locatário (por meio de políticas).
>
>Nesse caso, nem todo o conteúdo poderá ser recuperado usando um endpoint específico de locatário.
>
>O autor de conteúdo deve controlar esse cenário; por exemplo, pode ser útil considerar colocar Modelos de fragmento de conteúdo compartilhados no locatário Global.

### Ativando seu ponto de extremidade GraphQL {#enabling-graphql-endpoint}

Para habilitar um Endpoint GraphQL, primeiro é necessário ter uma configuração apropriada no Navegador de configuração.

>[!CAUTION]
>
>Se o uso de modelos de fragmento de conteúdo não tiver sido ativado, a opção **Criar** não estará disponível.

Para ativar o endpoint correspondente:

1. Navegue até **Ferramentas**, **Sites**, em seguida selecione **GraphQL**.
1. Selecione **Criar**.
1. A caixa de diálogo **Criar novo Ponto de Extremidade GraphQL** será aberta. Aqui você pode especificar:
   * **Nome**: nome do ponto final; você pode inserir qualquer texto.
   * **Use o esquema GraphQL fornecido por**: use a lista suspensa para selecionar o site/projeto necessário.

   >[!NOTE]
   >
   >O seguinte aviso é mostrado na caixa de diálogo:
   >
   >* *Os pontos de extremidade do GraphQL podem causar problemas de segurança e desempenho de dados se não forem gerenciados com cuidado. Defina as permissões apropriadas após criar um ponto de extremidade.*


1. Confirme com **Create**.
1. A caixa de diálogo **Próximas etapas** fornecerá um link direto para o console Segurança para que você possa garantir que o endpoint recém-criado tenha as permissões adequadas.

   >[!CAUTION]
   >
   >O endpoint é acessível a todos. Isso pode - especialmente em instâncias de publicação - causar uma preocupação de segurança, já que as consultas GraphQL podem impor uma carga pesada no servidor.
   >
   >Você pode configurar ACLs, apropriadas ao seu caso de uso, no terminal.

### Publicar seu ponto de extremidade GraphQL {#publishing-graphql-endpoint}

Selecione o novo terminal e **Publish** para torná-lo totalmente disponível em todos os ambientes.

>[!CAUTION]
>
>O endpoint é acessível a todos.
>
>Em instâncias de publicação, isso pode causar uma preocupação de segurança, já que as consultas GraphQL podem impor uma carga pesada no servidor.
>
>Você deve configurar as ACLs apropriadas ao seu caso de uso no terminal.

### Instalação da interface GraphiQL AEM {#installing-graphiql-interface}

A interface do usuário GraphiQL pode ser instalada no AEM com um pacote dedicado: o pacote [Pacote de Conteúdo GraphiQL v0.0.6 (2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip).

### AEM Esquemas GraphQL {#aem-graphql-schemas}

Para acessar seus dados, primeiro é necessário selecionar o tipo de Modelo de fragmento de conteúdo necessário - representado por um esquema GraphQL. AEM Esquemas GraphQL são derivados dos Modelos de fragmento de conteúdo - para uso em consultas GraphQL.

<!--
Confirm is the schema city or CityModel? -->

Se você tiver um Modelo de fragmento de conteúdo chamado `City`, haverá um esquema correspondente chamado `city`. Você pode usar a consulta a seguir para listar o `name` de todos os Fragmentos de conteúdo com base nesse Modelo.

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

Você pode usar a seguinte query para listar os `name` e `description` de todos os `types` para todos os schemas disponíveis:

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

### AEM Campos GraphQL {#aem-graphql-fields}

Após selecionar o esquema necessário, é necessário acessar dados específicos - representados pelos campos no esquema.

Dentro do schema há campos individuais, de duas categorias básicas:

* Campos gerados.

   Uma seleção de [Tipos de campo](#field-types) é usada para criar campos com base em como você configura o Modelo de fragmento de conteúdo. Os nomes de campo são obtidos do campo **Nome da propriedade** do **Tipo de dados**.

   * Também há a propriedade **Renderizar como** a ser levada em consideração, pois os usuários podem configurar determinados tipos de dados; por exemplo, como um texto de linha única ou um multicampo.

* GraphQL para AEM também gera vários campos auxiliares.

   Eles são usados para identificar um Fragmento de conteúdo ou para obter mais informações sobre um fragmento de conteúdo.

### Tipos de campo {#field-types}

GraphQL para AEM oferece suporte a uma lista de tipos. Todos os tipos de dados do modelo de fragmento de conteúdo suportados e os tipos GraphQL correspondentes são representados:

| Modelo de fragmento de conteúdo - Tipo de dados | Tipo GraphQL | Descrição |
|--- |--- |--- |
| Texto de linha única | String, [String] | Usado para strings simples, como nomes de autor, nomes de localização etc. |
| Texto de várias linhas | Sequência de caracteres | Usado para saída de texto, como o corpo de um artigo |
| Número | Flutuante, [Flutuante] | Usado para exibir números de ponto flutuante e números regulares |
| Booleano | Booleano | Usado para exibir caixas de seleção → declarações simples verdadeiras/falsas |
| Data E Hora | Calendário | Usado para exibir data e hora em um formato ISO 8086. Dependendo do tipo selecionado, há três opções disponíveis para uso em GraphQL AEM: `onlyDate`, `onlyTime`, `dateTime` |
| Enumeração | Sequência de caracteres | Usado para exibir uma opção de uma lista de opções definidas na criação do modelo |
| Tags | [Sequência de caracteres] | Usado para exibir uma lista de strings que representam tags usadas em AEM |
| Referência de conteúdo | Sequência de caracteres | Usado para exibir o caminho para outro ativo no AEM |
| Referência do fragmento | *Um tipo de modelo* | Usado para fazer referência a outro Fragmento de conteúdo de um determinado Tipo de modelo, definido quando o modelo foi criado |

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

>[!NOTE]
>
>Consulte Exemplo de consulta - Um único fragmento de cidade específico.

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
| `booleanArrayMetadata:[booleanArrayMetadata]!` |
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

>[!NOTE]
>
>Consulte Exemplo de consulta para metadados - Liste os metadados para prêmios denominados GB.

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

>[!NOTE]
>
>Consulte Exemplo de consulta - Todas as cidades com uma variável nomeada.

### Variáveis GraphQL AEM {#aem-graphql-variables}

As variáveis são úteis em qualquer forma de programação ou consulta, pois permitem armazenar valores diferentes em um local. Para AEM GraphQL, isso significa que, em vez de ter que gravar uma consulta separada para cada valor, você pode gravar sua consulta para uma variável, e o valor dessa variável pode ser alterado conforme necessário.

GraphQL permite que as variáveis sejam colocadas no query.

>[!NOTE]
>
>Para obter mais informações, consulte a documentação GraphQL para variáveis.

Por exemplo, para obter todos os Fragmentos de conteúdo do tipo `Article` que têm uma variação específica, você pode especificar a variável `variation` em GraphiQL. Todas as instâncias serão recuperadas em `GetArticlesByVariation` e passadas para usadas em `articleList`.

![Variáveis GraphQL ](assets/graphqlapi-variables.png "Variáveis GraphQL")

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

### Diretivas GraphQL AEM {#aem-graphql-directives}

No GraphQL há uma possibilidade de alterar o query com base em variáveis, chamadas de Diretivas GraphQL.

Por exemplo, é possível incluir o campo `adventurePrice` em uma consulta para todos os `AdventureModels`, com base em uma variável `includePrice`.

!![GraphQL Directives](assets/grafqlapi-guidelines.png &quot;Diretivas GraphQL&quot;)

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

### AEM Filtros GraphQL {#aem-graphql-filters}

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

* detalhes do GraphQL para extensões de AEM

* Consultas de exemplo usando este conteúdo e estrutura de amostra

### Extensões GraphQL AEM {#aem-graphql-extensions}

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

### Consultas Persistentes (Cache) {#persisted-queries-caching}

Após preparar uma consulta com uma solicitação POST, ela pode ser executada com uma solicitação GET que pode ser armazenada em cache por caches HTTP ou um CDN.

Isso é necessário, pois as consultas do POST geralmente não são armazenadas em cache e, se estiver usando o GET com o query como parâmetro, há um risco significativo de o parâmetro se tornar muito grande para serviços HTTP e intermediários.

As consultas persistentes devem sempre usar o terminal relacionado à configuração apropriada (locatário); para que possam usar ou ambos:

* A configuração global e o terminal
O query tem acesso a todos os Modelos de fragmento de conteúdo.
* Configuração(ões) específica(s) do locatário e endpoint(s)
A criação de uma consulta persistente para uma configuração de locatário específica requer um endpoint específico de locatário correspondente (para fornecer acesso aos Modelos de fragmento de conteúdo relacionados).
Por exemplo, para criar uma consulta persistente especificamente para o locatário do WKND, uma configuração de locatário específica do WKND correspondente e um endpoint específico do WKND devem ser criados antecipadamente.

>[!NOTE]
>
>Consulte Ativar a funcionalidade de fragmento de conteúdo no Navegador de configuração para obter mais detalhes.
>
>As **Consultas de persistência GraphQL** precisam ser ativadas para a configuração apropriada do locatário.

Por exemplo, se houver uma consulta específica chamada `my-query`, que usa um modelo `my-model` da configuração do locatário `my-conf`:

* Você pode criar uma consulta usando o terminal específico `my-conf` e, em seguida, a consulta será salva da seguinte maneira:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Você pode criar a mesma consulta usando o ponto de extremidade `global`, mas a consulta será salva da seguinte maneira:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Essas são duas consultas diferentes - salvas em caminhos diferentes.
>
>Acontece que eles apenas usam o mesmo modelo - mas por diferentes endpoints.

Estas são as etapas necessárias para persistir uma determinada query:

1. Prepare a query colocando-a no novo URL de ponto de extremidade `/graphql/persist.json/<config>/<persisted-label>`.

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

1. Em seguida, você pode repetir a consulta persistente usando GETo URL `/graphql/execute.json/<shortPath>`.

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

1. Para executar o query na publicação, a árvore persistente relacionada precisa ser replicada

   * Usando um POST para replicação:

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * Uso de um pacote:
      1. Crie uma nova definição de pacote.
      1. Inclua a configuração (por exemplo, `/conf/wknd/settings/graphql/persistentQueries`).
      1. Crie o pacote.
      1. Replicar o pacote.
   * Uso da ferramenta de replicação/distribuição.
      1. Vá para a ferramenta Distribution .
      1. Selecione ativação em árvore para a configuração (por exemplo, `/conf/wknd/settings/graphql/persistentQueries`).
   * Uso de um workflow (por meio da configuração do iniciador do workflow):
      1. Defina uma regra do iniciador do workflow para executar um modelo de workflow que replicaria a configuração em eventos diferentes (por exemplo, criar, modificar, entre outros).



1. Quando a configuração do query estiver em publicação, os mesmos princípios se aplicarão, apenas usando o endpoint de publicação.

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

### Consultando o ponto de extremidade GraphQL de um site externo {#query-graphql-endpoint-from-external-website}

Para acessar o ponto de extremidade GraphQL de um site externo, é necessário configurar o:

* Filtro CORS
* Filtro referenciador

#### Filtro CORS {#cors-filter}

>[!NOTE]
>
>Para obter uma visão geral detalhada da política de compartilhamento de recursos do CORS no AEM, consulte Compreender o compartilhamento de recursos entre origens (CORS).

Para acessar o ponto de extremidade GraphQL, uma política CORS deve ser configurada no repositório Git do cliente. Isso é feito adicionando um arquivo de configuração de CORS OSGi apropriado para os endpoints desejados.

Essa configuração deve especificar uma origem de site confiável `alloworigin` ou `alloworiginregexp` para a qual o acesso deve ser concedido.

Por exemplo, para conceder acesso ao ponto de extremidade GraphQL e ao ponto de extremidade de consultas persistentes para `https://my.domain` é possível usar:

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

Se você tiver configurado um caminho personalizado para o endpoint, também poderá usá-lo em `allowedpaths`.

#### Filtro de referência {#referrer-filter}

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
>Todos os esquemas GraphQL (derivados dos Modelos de fragmento de conteúdo que foram **Enabled**) podem ser lidos pelo ponto de extremidade GraphQL.
>
>Isso significa que você precisa garantir que não haja dados confidenciais disponíveis, pois eles poderiam ser vazados dessa forma; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.

### Autenticação GraphQL AEM {#aem-graphql-authentication}

Um caso de uso principal da API GraphQL do Adobe Experience Manager as a Cloud Service (AEM) para entrega de fragmentos de conteúdo é aceitar consultas remotas de aplicativos ou serviços de terceiros. Essas consultas remotas podem exigir acesso à API autenticada para proteger a entrega de conteúdo sem cabeçalho.

>[!NOTE]
>
>Para testes e desenvolvimento, também é possível acessar a API GraphQL da AEM diretamente usando a interface GraphiQL.

Para autenticação, o serviço de terceiros precisa usar um Token de acesso, que pode ser usado na solicitação GraphQL.

#### Recuperar um token de acesso {#retrieving-access-token}

Consulte Gerar tokens de acesso para APIs do lado do servidor para obter detalhes completos.

#### Usar o token de acesso em uma solicitação GraphQL {#use-access-token-in-graphql-request}

Para que um serviço de terceiros se conecte a uma instância de AEM, ele precisa ter um *Token de acesso*. O serviço deve então adicionar esse token ao cabeçalho `Authorization` na solicitação do POST.

Por exemplo, um cabeçalho de autorização GraphQL:

```xml
Authorization: Bearer <access_token>
```

#### Requisitos de permissão {#permission-requirements}

Todas as solicitações feitas usando o token de acesso serão feitas *pela conta de usuário que gerou o token*.

Isso significa que é necessário verificar se a conta tem as permissões necessárias para executar consultas GraphQL.

Você pode verificar isso usando GraphiQL na instância local.

## Amostras de consultas GraphQL AEM {#samples-aem-graphql-queries}

Consulte Saiba como usar GraphQL com AEM - Conteúdo de amostra e Consultas para obter um intervalo abrangente de consultas de amostra.

<!--
## Code Samples for AEM GraphQL Queries {#code-samples-aem-graphql-queries}
-->

## O que vem a seguir {#whats-next}

Agora que você aprendeu a acessar e consultar o conteúdo sem periféricos usando a API GraphQL AEM, agora é possível [aprender a usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo](/help/implementing/developing/headless-journey/update-your-content.md).

## Recursos adicionais {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [Esquema](https://graphql.org/learn/schema/)
   * [Variáveis](https://graphql.org/learn/queries/#variables)
   * [Bibliotecas GraphQL Java](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [A estrutura do fragmento de conteúdo de amostra](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Saiba como usar GraphQL com AEM - Conteúdo de amostra e consultas](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [Exemplo de consulta - Um único fragmento de cidade específico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [Exemplo de consulta para metadados - Lista os metadados para prêmios denominados GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [Consulta de exemplo - Todas as cidades com uma variável nomeada](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [Ativar a funcionalidade de fragmento de conteúdo no navegador de configuração](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [Trabalho com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
   * [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
   * [Saída JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
* [Entenda o CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [Gerar tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [Introdução ao AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  - Uma pequena série de tutoriais em vídeo que fornece uma visão geral do uso de AEM recursos headless, incluindo modelagem de dados e GraphQL.
