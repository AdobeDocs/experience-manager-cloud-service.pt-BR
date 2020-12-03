---
title: Delivery de conteúdo sem cabeçalho usando fragmentos de conteúdo com GraphQL
description: Saiba como usar Fragmentos de conteúdo no Adobe Experience Manager (AEM) como um Cloud Service com o GraphQL para o Delivery de conteúdo sem cabeçalho.
translation-type: tm+mt
source-git-commit: 1e9596fb12a38f5c4c6e15d7c33af86e59e76083
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---


# Delivery de conteúdo sem cabeçalho usando fragmentos de conteúdo com GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

>[!CAUTION]
>
>A API AEM GraphQL, para o Delivery de fragmento de conteúdo, será lançada no início de 2021.
>
>A documentação relacionada já está disponível para fins de pré-visualização.

Com o Adobe Experience Manager (AEM) como Cloud Service, você pode usar os Fragmentos de conteúdo, juntamente com a API AEM GraphQL (uma implementação personalizada, baseada no GraphQL padrão), para fornecer conteúdo estruturado para uso em seus aplicativos.

## CMS sem cabeçalho {#headless-cms}

Um sistema de Gestão de conteúdo sem cabeça (CMS) é:

* &quot;*Um sistema de gestão de conteúdo sem cabeçalho, ou CMS sem cabeçalho, é um sistema de gestão de conteúdo (CMS) de back-end criado desde o início como um repositório de conteúdo que torna o conteúdo acessível por meio de uma API para exibição em qualquer dispositivo.*

   *O termo &quot;sem cabeça&quot; vem do conceito de cortar o &quot;cabeçote&quot; (o front-end, ou seja, o site) do &quot;body&quot; (o back-end, ou seja, o repositório de conteúdo).*&quot;

   Consulte [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

Em termos de criação de Fragmentos de conteúdo em AEM isso significa que:

* Você pode usar Fragmentos de conteúdo para criar conteúdo que não se destina principalmente a ser publicado diretamente (1:1) em páginas formatadas.

* O conteúdo dos seus Fragmentos de conteúdo será estruturado de maneira predeterminada - de acordo com os Modelos de fragmento de conteúdo. Isso simplifica o acesso de seus aplicativos, o que processará ainda mais seu conteúdo.

>[!NOTE]
>
>Consulte [Ausente de cabeçalho e AEM](/help/implementing/developing/headless/introduction.md) para obter uma introdução ao Desenvolvimento sem cabeçalho para AEM Sites como Cloud Service.

## GraphQL - uma visão geral {#graphql-overview}

GraphQL é:

* &quot;*...um idioma de query para APIs e um tempo de execução para realizar esses query com seus dados existentes. O GraphQL fornece uma descrição completa e compreensível dos dados em sua API, fornece aos clientes o poder de solicitar exatamente o que eles precisam e nada mais, facilita a evolução das APIs ao longo do tempo e habilita poderosas ferramentas de desenvolvedor.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

* &quot;*...uma especificação aberta para uma camada de API flexível. Coloque o GraphQL sobre seus backends existentes para criar produtos mais rápido do que nunca....*&quot;.

   Consulte [Explorar GraphQL](https://www.graphql.com). &quot;*Explorar GraphQL é mantido pela equipe do Apollo. Nosso objetivo é dar aos desenvolvedores e líderes técnicos em todo o mundo todas as ferramentas de que precisam para entender e adotar o GraphQL.*&quot;.

A [API AEM GraphQL](#aem-graphql-api) permite executar query (complexos) em [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md); com cada query de acordo com um tipo de modelo específico. O conteúdo retornado pode ser usado pelos seus aplicativos.

### Terminologia GraphQL {#graphql-terminology}

O GraphQL usa o seguinte:

* **[Query](https://graphql.org/learn/queries/)**

* **[Schemas e tipos](https://graphql.org/learn/schema/)**  - usando esses itens, o GraphQL apresenta os tipos e as operações permitidos para o GraphQL para AEM implementação.

* **[Campos](https://graphql.org/learn/queries/#fields)**

* **Endpoint**  GraphQL - o caminho no AEM que responde aos query GraphQL e fornece acesso aos schemas GraphQL.

Consulte a [(GraphQL.org) Introduction to GraphQL](https://graphql.org/learn/) para obter detalhes abrangentes, incluindo as [Práticas recomendadas](https://graphql.org/learn/best-practices/).

### Tipos de Query GraphQL {#graphql-query-types}

Com o GraphQL, é possível executar query para:

* **Entrada única**

* **[Lista das entradas](https://graphql.org/learn/schema/#lists-and-non-null)**

## API AEM GraphQL {#aem-graphql-api}

Para [Adobe Experience como uma Experience Cloud, uma implementação personalizada da API GraphQL padrão](/help/assets/content-fragments/graphql-api-content-fragments.md) foi implementada.

A implementação da API AEM GraphQL é baseada nas [bibliotecas Java GraphQL](https://graphql.org/code/#java).

## Fragmentos de conteúdo para uso com a API AEM GraphQL {#content-fragments-use-with-aem-graphql-api}

[O Content ](#content-fragments) Fragmentscan pode ser usado como base para o GraphQL para AEM query como:

* Eles permitem que você projete, crie, prepare e publique conteúdo independente de página.
* Os [Modelos de fragmento de conteúdo](#content-fragments-models) fornecem a estrutura necessária por meio de tipos de dados definidos.
* A [Referência de fragmento](#fragment-references), disponível ao definir um modelo, pode ser usada para definir camadas adicionais de estrutura.

![Fragmentos de conteúdo para uso com ](assets/cfm-nested-01.png "GraphQLContent Fragments para uso com GraphQL")

### Fragmentos de conteúdo {#content-fragments}

Fragmentos de conteúdo:

* Contém conteúdo estruturado.

* Eles são baseados em um [Modelo de fragmento de conteúdo](#content-fragments-models), que predefine a estrutura do fragmento resultante.

### Modelos de fragmentos do conteúdo {#content-fragments-models}

Estes [Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md):

* Forneça os tipos de dados e campos necessários para o GraphQL. Eles garantem que seu aplicativo solicite somente o que é possível e receba o que é esperado.

* O tipo de dados **[Referências de fragmento](#fragment-references)** pode ser usado em seu modelo para fazer referência a outro Fragmento de conteúdo e, portanto, introduzir níveis adicionais de estrutura.

### Referências de fragmento {#fragment-references}

A **[Referência do fragmento](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* É de especial interesse em conjunto com o GraphQL.

* É um tipo de dados específico que pode ser usado ao definir um Modelo de fragmento de conteúdo.

* Faz referência a outro fragmento, dependendo de um modelo de fragmento de conteúdo específico.

* Permite recuperar dados estruturados.

   * Quando definido como **multifeed**, vários subfragmentos podem ser referenciados (recuperados) pelo fragmento principal.

### Pré-visualização JSON {#json-preview}

Para ajudar a projetar e desenvolver seus Modelos de fragmento de conteúdo, você pode pré-visualização [saída JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

## Aprendendo a usar o GraphQL com AEM - Conteúdo de amostra e Query {#learn-graphql-with-aem-sample-content-queries}

Consulte [Aprendendo a usar o GraphQL com AEM - Conteúdo de amostra e Query](/help/assets/content-fragments/content-fragments-graphql-samples.md) para obter uma introdução ao uso da API AEM GraphQL.

## Tutorial - Introdução ao AEM sem cabeçalho e ao GraphQL

Procurando um tutorial prático? Consulte [Introdução com AEM GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) tutorial completo ilustrando como criar e expor conteúdo usando as APIs GraphQL da AEM e consumidas por um aplicativo externo, em um cenário CMS sem cabeçalho.