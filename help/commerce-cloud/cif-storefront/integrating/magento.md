---
title: Integração do AEM e da Adobe Commerce usando o Commerce integration framework
description: O AEM e o Adobe Commerce são perfeitamente integrados usando o Commerce integration framework (CIF). O CIF permite que o AEM acesse uma instância do Adobe Commerce e se comunique com o Adobe Commerce por meio do GraphQL. Ela também permite que os autores do AEM usem seletores de produtos e categorias e o console de produtos para navegar pelos dados de produtos e categorias obtidos da Adobe Commerce sob demanda. Além disso, a CIF fornece uma vitrine pronta para uso que agiliza projetos de comércio.
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 16%

---


# Integração do AEM e da Adobe Commerce usando o Commerce integration framework {#aem-framework}

O Experience Manager e o Adobe Commerce são perfeitamente integrados usando o Commerce integration framework (CIF). O CIF permite que o AEM acesse diretamente e se comunique com a instância de comércio usando as [APIs do GraphQL da Adobe Commerce.](https://devdocs.magento.com/guides/v2.4/graphql/)

>[!NOTE]
>
> A versão mínima da API do GraphQL com suporte é 2.3.5. Alguns recursos são compatíveis somente com versões mais recentes ou apenas com a edição do Adobe Commerce.

>[!NOTE]
>
>O GraphQL é usado atualmente em dois cenários (separados) no Adobe Experience Manager (AEM) as a Cloud Service:
>
>* Nesse cenário, o CIF se comunica com o comércio por meio do GraphQL.
>* [Fragmentos de conteúdo do AEM trabalham em conjunto com a API do AEM GraphQL (uma implementação personalizada, com base no GraphQL padrão), para fornecer conteúdo estruturado para uso em seus aplicativos.](/help/headless/graphql-api/content-fragments.md)

## Visão geral da arquitetura {#overview}

Esta é a arquitetura geral:

![Visão geral da arquitetura da CIF](../assets/AEM_Magento_Architecture.png)

No CIF, há suporte para padrões de comunicação do lado do servidor e do lado do cliente.
As chamadas de APIs do lado do servidor são implementadas usando o [cliente GraphQL](https://github.com/adobe/commerce-cif-graphql-client) interno e genérico junto com um [conjunto de modelos de dados gerados](https://github.com/adobe/commerce-cif-magento-graphql) para o esquema GraphQL de comércio. Além disso, qualquer consulta ou mutação do GraphQL no formato GQL pode ser usada.

Para os componentes do lado do cliente, que são compilados usando o [React](https://reactjs.org/), o [Cliente Apollo](https://www.apollographql.com/docs/react/) é usado.

## Arquitetura dos Componentes principais do AEM CIF {#cif-core-components}

![Arquitetura dos Componentes principais da CIF do AEM](../assets/cif-component-architecture.jpg)

Os [Componentes principais do AEM CIF](https://github.com/adobe/aem-core-cif-components) seguem padrões de design e práticas recomendadas muito semelhantes aos dos [Componentes principais do AEM WCM](https://github.com/adobe/aem-core-wcm-components).

A lógica de negócios e a comunicação de back-end com o Adobe Commerce para os Componentes principais do AEM CIF são implementadas nos Modelos do Sling. Caso seja necessário personalizar essa lógica para atender aos requisitos específicos do projeto, o padrão de delegação para Modelos do Sling pode ser usado.

>[!TIP]
>
>A página [Personalizar os Componentes principais da CIF do AEM](/help/commerce-cloud/cif-storefront/customizing/customize-cif-components.md) tem um exemplo detalhado e oferece as práticas recomendadas para personalizar os componentes principais da CIF.

Nos projetos, os Componentes principais do AEM CIF e os componentes do projeto personalizado podem recuperar facilmente o cliente configurado para uma loja da Adobe Commerce associada a uma página do AEM por meio da configuração com reconhecimento de contexto do Sling.

## Pesquisar

A CIF fornece um [Componente principal de pesquisa](https://www.aemcomponents.dev/content/core-components-examples/library/commerce/search.html) pronto para uso, que é uma experiência de pesquisa renderizada no lado do servidor com base na [API do Commerce GraphQL.](https://developer.adobe.com/commerce/webapi/graphql/) clientes do Commerce têm a opção de usar o [Live Search](https://experienceleague.adobe.com/docs/commerce-merchant-services/live-search/guide-overview.html?lang=pt-BR). Siga este [link](/help/commerce-cloud/cif-storefront/integrating/live-search-plp.md) para saber mais sobre a integração CIF - Live Search.
