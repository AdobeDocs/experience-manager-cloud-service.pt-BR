---
title: Integração de AEM e Magento usando o Commerce Integration Framework
description: Integração de AEM e Magento usando o Commerce Integration Framework
translation-type: tm+mt
source-git-commit: 48805b21500ff3f2629efd6aecb40bb1cdc38cd6
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 1%

---


# AEM and Magento Integration using Commerce Integration Framework {#aem-magento-framework}

AEM e Magento são perfeitamente integrados usando o Commerce Integration Framework (CIF). O CIF permite que AEM acesse uma instância de Magento e comunique-se com o Magento via GraphQL. Ele também permite que os AEM Author usem Seletores de produtos e Categorias e o Console de produtos para navegar pelos dados de produtos e categorias obtidos por demanda do Magento. Além disso, o CIF fornece uma vitrine pronta para uso que pode acelerar projetos de comércio.

## Visão geral da arquitetura {#overview}

A arquitetura geral é a seguinte:

![Visão geral da arquitetura CIF](../assets/AEM_Magento_Architecture.JPG)

CIF baseia-se no suporte ao GraphQL. O principal canal de comunicação entre AEM e Magento é a API API Magento [GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/) do. Há diferentes maneiras de configurar a comunicação entre AEM como Cloud Service e Magento, consulte a página [Introdução](../getting-started.md) para obter detalhes.

Dentro do CIF há suporte para padrões de comunicação do lado do servidor e do cliente.
As chamadas de APIs do lado do servidor são implementadas usando o cliente [GraphQL](https://github.com/adobe/commerce-cif-graphql-client) integrado e genérico em combinação com um [conjunto de modelos](https://github.com/adobe/commerce-cif-magento-graphql) de dados gerados para o schema GraphQL do Magento. Além disso, qualquer query ou mutação GraphQL no formato GQL pode ser usado.

Para os componentes do cliente, que são criados usando o [React](https://reactjs.org/), o [Apollo Client](https://www.apollographql.com/docs/react/) é usado.

## Arquitetura de componentes principais AEM CIF {#cif-core-components}

![Arquitetura de componentes principais AEM CIF](../assets/cif-component-architecture.jpg)

[AEM CIF Componentes](https://github.com/adobe/aem-core-cif-components) principais seguem padrões de design e práticas recomendadas muito semelhantes aos [AEM componentes](https://github.com/adobe/aem-core-wcm-components)principais do WCM.

A lógica comercial e a comunicação de backend com o Magento para os componentes principais AEM CIF são implementadas nos Modelos Sling. Caso seja necessário personalizar essa lógica para atender aos requisitos específicos do projeto, o Padrão de delegação para Modelos Sling pode ser usado.

>[!TIP]
>
>A página [Personalizar AEM componentes](../customizing/customize-cif-components.md) principais CIF contém um exemplo detalhado e uma prática recomendada de como personalizar os componentes principais CIF.

Em projetos, AEM componentes principais CIF e componentes de projeto personalizados podem recuperar facilmente o cliente configurado para uma loja de Magento associados a uma página AEM por meio da configuração Sling Context-Aware.
