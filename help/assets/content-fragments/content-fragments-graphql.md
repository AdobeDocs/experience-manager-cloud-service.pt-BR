---
title: Entrega de conteúdo sem cabeçalho usando Fragmentos de conteúdo com GraphQL
description: Saiba como usar AEM Fragmentos de conteúdo com GraphQL para a entrega de conteúdo sem interface.
feature: Content Fragments
role: User
exl-id: 4a3b030d-ed59-4920-bf94-e00a45f85b51
source-git-commit: e592dd7a3a717259493f23943933fe3d0e71b7ab
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 20%

---

# Entrega de conteúdo sem cabeçalho usando Fragmentos de conteúdo com GraphQL {#headless-content-delivery-using-content-fragments-with-graphQL}

Com o Adobe Experience Manager (AEM) as a Cloud Service, é possível usar os Fragmentos de conteúdo, juntamente com a API GraphQL AEM (uma implementação personalizada, com base no GraphQL padrão), para fornecer conteúdo estruturado de maneira contínua para uso em seus aplicativos. A capacidade de personalizar uma única consulta de API permite recuperar e entregar o conteúdo específico que você deseja/precisa renderizar (como resposta à única consulta de API).

>[!NOTE]
>
>Consulte [Sem cabeça e AEM](/help/headless/introduction.md) para obter uma introdução ao Headless Development for AEM Sites as a Cloud Service.

>[!NOTE]
>
>O GraphQL é usado atualmente em dois cenários (separados) no Adobe Experience Manager (AEM) as a Cloud Service:
>
>* [O AEM Commerce consome dados de uma plataforma de comércio via GraphQL](/help/commerce-cloud/integrating/magento.md).
>* [Fragmentos de conteúdo do AEM trabalham em conjunto com a API GraphQL do AEM (uma implementação personalizada, com base no GraphQL padrão), para fornecer conteúdo estruturado para uso em seus aplicativos](/help/headless/graphql-api/content-fragments.md).


## CMS sem periféricos {#headless-cms}

Um Sistema de Gerenciamento de Conteúdo Sem Cabeçalho (CMS) é:

* &quot;*Um sistema de gerenciamento de conteúdo sem periféricos, ou CMS sem periféricos, é um sistema de gerenciamento de conteúdo (CMS) de back-end criado desde o início como um repositório de conteúdo que torna o conteúdo acessível por meio de uma API para exibição em qualquer dispositivo.*

   Consulte [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

Em termos de criação de Fragmentos de conteúdo no AEM isso significa que:

* Você pode usar Fragmentos de conteúdo para criar conteúdo que não se destina principalmente a ser publicado diretamente (1:1) em páginas formatadas.

* O conteúdo dos Fragmentos de conteúdo será estruturado de maneira predeterminada, de acordo com os Modelos de fragmento de conteúdo. Isso simplifica o acesso para seus aplicativos, o que processará ainda mais seu conteúdo.

## GraphQL - Uma visão geral {#graphql-overview}

O GraphQL é:

* &quot;*...um idioma de consulta para APIs e um tempo de execução para realizar essas consultas com seus dados existentes.*&quot;.

   Consulte [GraphQL.org](https://graphql.org)

O [AEM API GraphQL](#aem-graphql-api) O permite executar consultas (complexas) no [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md); com cada query de acordo com um tipo de modelo específico. O conteúdo retornado pode ser usado pelos seus aplicativos.

## AEM API GraphQL {#aem-graphql-api}

Para o Adobe Experience as a Cloud Experience, uma implementação personalizada da API GraphQL padrão foi desenvolvida. Consulte [AEM API GraphQL para uso com Fragmentos de conteúdo](/help/headless/graphql-api/content-fragments.md) para obter detalhes.

A implementação AEM da API GraphQL é baseada no [Bibliotecas GraphQL Java](https://graphql.org/code/#java).

## Fragmentos de conteúdo para uso com a API GraphQL da AEM {#content-fragments-use-with-aem-graphql-api}

[Fragmentos de conteúdo](#content-fragments) pode ser usado como base para GraphQL para consultas de AEM como:

* Eles permitem projetar, criar, preparar e publicar conteúdo independente da página.
* O [Modelos de fragmentos do conteúdo](#content-fragments-models) fornecer a estrutura necessária por meio de tipos de dados definidos.
* O [Referência do fragmento](#fragment-references), disponíveis ao definir um modelo, podem ser usadas para definir camadas adicionais de estrutura.

![Fragmentos de conteúdo para uso com GraphQL](assets/cfm-nested-01.png "Fragmentos de conteúdo para uso com GraphQL")

### Fragmentos de conteúdo {#content-fragments}

Fragmentos de conteúdo:

* Contém conteúdo estruturado.

* Eles se baseiam em um [Modelo de fragmento de conteúdo](#content-fragments-models), que predefine a estrutura do fragmento resultante.

### Modelos de fragmentos do conteúdo {#content-fragments-models}

Esses [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md):

* São usados para gerar a variável [Esquemas](https://graphql.org/learn/schema/), uma vez **Ativado**.

* Forneça os tipos de dados e campos necessários para GraphQL. Eles garantem que seu aplicativo solicite apenas o que é possível e receba o que é esperado.

* O tipo de dados **[Referências de fragmento](#fragment-references)** O pode ser usado no modelo para fazer referência a outro Fragmento de conteúdo e, portanto, introduzir níveis adicionais de estrutura.

### Referências de fragmento {#fragment-references}

O **[Referência do fragmento](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**:

* É de especial interesse em conjunto com GraphQL.

* É um tipo de dados específico que pode ser usado ao definir um Modelo de fragmento de conteúdo.

* Faz referência a outro fragmento, dependendo de um modelo de fragmento de conteúdo específico.

* Permite recuperar dados estruturados.

   * Quando definido como um **multifeed**, vários subfragmentos podem ser referenciados (recuperados) pelo fragmento principal.

### Visualização JSON {#json-preview}

Para ajudar a projetar e desenvolver os Modelos de fragmentos de conteúdo, você pode visualizar [Saída JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

## Saiba como usar o GraphQL com o AEM - Exemplos de conteúdo e consultas {#learn-graphql-with-aem-sample-content-queries}

Consulte [Saiba como usar GraphQL com AEM - Conteúdo de amostra e consultas](/help/headless/graphql-api/sample-queries.md) para obter uma introdução ao uso da API GraphQL da AEM.

## Tutorial - Introdução ao AEM Headless e GraphQL

Procurando um tutorial prático? Veja o tutorial completo de [Introdução ao AEM Headless e GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=pt-BR) que ilustra como criar e expor conteúdo usando as APIs GraphQL do AEM e consumi-lo por meio de um aplicativo externo, em um cenário de CMS headless.
