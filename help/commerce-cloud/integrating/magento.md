---
title: Integração do AEM e do Adobe Commerce usando a Commerce Integration Framework
description: O AEM e o Adobe Commerce são perfeitamente integrados usando a Commerce Integration Framework (CIF). A CIF permite que o AEM acesse uma instância do Adobe Commerce e estabeleça uma comunicação com a Adobe Commerce por meio do GraphQL. Também permite que os autores do AEM usem seletores de produto e de categoria e o console do produto para navegar pelos dados de produto e categoria obtidos do Adobe Commerce sob demanda. Além disso, a CIF fornece uma loja pronta para uso que agiliza projetos de comércio.
thumbnail: aem-magento-architecture.jpg
exl-id: 110ceef5-2c35-4b81-8e89-26929c0da91b,1cdfda88-a728-432f-b24a-f81347572bcf
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 22%

---

# Integração do AEM e do Adobe Commerce usando a Commerce Integration Framework {#aem-framework}

O Experience Manager e o Adobe Commerce são perfeitamente integrados usando a Commerce Integration Framework (CIF). A CIF permite que o AEM acesse e comunique diretamente com a instância de comércio usando o Adobe Commerce [APIs GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/).

>[!NOTE]
>
> A versão mínima da API GraphQL compatível é a 2.3.5. Alguns recursos são compatíveis apenas com versões mais recentes ou apenas na edição do Adobe Commerce.

>[!NOTE]
>
>O GraphQL é usado atualmente em dois cenários (separados) no Adobe Experience Manager (AEM) as a Cloud Service:
>
>* Nesse cenário, a CIF se comunica com comércio via GraphQL.
>* [AEM Fragmentos de conteúdo trabalham com a API GraphQL AEM (uma implementação personalizada, com base no GraphQL padrão), para fornecer conteúdo estruturado para uso em seus aplicativos](/help/assets/content-fragments/graphql-api-content-fragments.md).


## Visão geral da arquitetura {#overview}

Esta é a arquitetura geral:

![Visão geral da arquitetura da CIF](../assets/AEM_Magento_Architecture.png)

Na CIF, há suporte para padrões de comunicação do lado do servidor e do lado do cliente.
As chamadas de APIs do lado do servidor são implementadas usando o [Cliente GraphQL](https://github.com/adobe/commerce-cif-graphql-client) em combinação com [conjunto de modelos de dados gerados](https://github.com/adobe/commerce-cif-magento-graphql) para o schema GraphQL de comércio. Além disso, podem ser usados qualquer consulta ou mutação GraphQL no formato GQL.

Para os componentes do lado do cliente, que são criados usando [Reagir](https://reactjs.org/), o [Cliente Apollo](https://www.apollographql.com/docs/react/) é usada.

## Arquitetura dos Componentes principais da CIF do AEM {#cif-core-components}

![Arquitetura dos Componentes principais da CIF do AEM](../assets/cif-component-architecture.jpg)

[Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) siga padrões de design e práticas recomendadas muito semelhantes à [Componentes principais do WCM AEM](https://github.com/adobe/aem-core-wcm-components).

A lógica de negócios e a comunicação de back-end com o Adobe Commerce para os Componentes principais da CIF do AEM são implementadas nos Modelos do Sling. Caso seja necessário personalizar essa lógica para atender aos requisitos específicos do projeto, o padrão de delegação para Modelos do Sling pode ser usado.

>[!TIP]
>
>A página [Personalizar os Componentes principais da CIF do AEM](../customizing/customize-cif-components.md) tem um exemplo detalhado e oferece as práticas recomendadas para personalizar os componentes principais da CIF.

Nos projetos, AEM os Componentes principais da CIF e os componentes do projeto personalizado podem recuperar facilmente o cliente configurado para uma loja da Adobe Commerce associada a uma página AEM por meio da configuração Sling sensível ao contexto.
