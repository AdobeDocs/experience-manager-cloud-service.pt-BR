---
title: Como atualizar seu conteúdo por meio das APIs do AEM
description: Nesta parte da Jornada de desenvolvedores headless do AEM, saiba como usar as APIs disponíveis para acessar e atualizar o conteúdo dos fragmentos de conteúdo.
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments, GraphQL API
role: Admin, Architect, Developer
source-git-commit: 8a3ee333a0bd5904c43c424967a7b9c752fd38c2
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 29%

---

# Como atualizar seu conteúdo por meio das APIs do AEM {#update-your-content}

Nesta parte da [Jornada de desenvolvedores headless do AEM](overview.md), saiba como usar as APIs disponíveis para acessar e atualizar o conteúdo dos fragmentos de conteúdo.

## A história até agora {#story-so-far}

No documento anterior da jornada headless do AEM, [Como acessar seu conteúdo por meio das APIs de entrega do AEM](access-your-content.md), você aprendeu a acessar o conteúdo headless no AEM por meio da API GraphQL do AEM; agora você deve:

* Ter um alto nível de compreensão sobre GraphQL.
* Entender como a API GraphQL do AEM funciona.
* Conhecer alguns exemplos de consultas práticas.

Este artigo se baseia nesses fundamentos para que você entenda como atualizar seu conteúdo headless existente no AEM por meio das APIs disponíveis.

## Objetivo {#objective}

* **Público-alvo**: avançado
* **Objetivo**: saiba mais sobre as APIs disponíveis para acessar e atualizar o conteúdo dos fragmentos de conteúdo.

## APIs do AEM para uso com Fragmentos de conteúdo {#aem-apis-for-use-with-content-fragments}

O Adobe Experience Manager (AEM) as a Cloud Service oferece várias APIs para entrega de conteúdo estruturado a partir de fragmentos de conteúdo e do gerenciamento de fragmentos de conteúdo. Consulte as páginas individuais para obter mais detalhes sobre as APIs específicas.

* Entrega de fragmento de conteúdo do AEM com OpenAPI
   * Essa API cria respostas JSON para fornecer conteúdo estruturado de fragmentos de conteúdo no AEM.
   * Ele usa um caminho para um fragmento de conteúdo como endpoint.
   * Essa API é baseada em REST.
   * Ele é otimizado para entrega de conteúdo, incluindo integração de CDN.
* API do AEM GraphQL para entrega de fragmentos de conteúdo
   * Essa API é baseada em esquemas. Os esquemas de API são representados por Modelos de fragmento de conteúdo, que definem a estrutura do conteúdo.
   * Essa API é baseada no GraphQL.
* Fragmentos de conteúdo e OpenAPIs de modelos de fragmento de conteúdo
   * Essas APIs são destinadas ao gerenciamento de conteúdo estruturado.
   * Os respectivos operadores do GET não estão otimizados para a entrega de conteúdo.
   * Essa API é baseada em REST.

>[!NOTE]
>
>O [Suporte a Fragmento de Conteúdo na API HTTP do Assets](/help/assets/content-fragments/assets-api-content-fragments.md) agora está [obsoleto](/help/release-notes/deprecated-removed-features.md). Ele foi substituído por [Entrega de fragmento de conteúdo com OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md), juntamente com [Fragmentos de conteúdo e OpenAPIs de gerenciamento de modelos de fragmento de conteúdo](/help/headless/content-fragment-openapis.md).

## O que vem a seguir {#whats-next}

Agora que concluiu esta parte da jornada de desenvolvedores headless do AEM, você deve:

* Entender as APIs do AEM disponíveis.
* Entenda como os Fragmentos de conteúdo são compatíveis com essas APIs.

Você deve continuar a jornada headless do AEM revisando o documento [Como unir os conceitos: aplicativo e conteúdo no AEM headless](put-it-all-together.md), onde você se familiarizará com as noções básicas e as ferramentas da arquitetura do AEM necessárias para unir seu aplicativo.

## Recursos adicionais {#additional-resources}

* [APIs do Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [APIs do AEM para entrega e gerenciamento de conteúdo estruturado](/help/headless/apis-headless-and-content-fragments.md)
* [Entrega de fragmento de conteúdo do AEM com OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md)
* [API do AEM GraphQL para entrega de fragmentos de conteúdo](/help/headless/graphql-api/content-fragments.md)
* [Fragmentos de conteúdo e OpenAPIs de modelos de fragmento de conteúdo](/help/headless/content-fragment-openapis.md)
* [Suporte a fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
* [Trabalho com fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)
* [Componentes principais do AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction)
* [Explicação sobre o CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
* [Vídeo - Desenvolvimento do CORS com o AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
* [Introdução ao AEM as a Headless CMS](/help/headless/introduction.md)
* [Portal do Desenvolvedor do AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)
* [Tutoriais do Headless no AEM](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/getting-started-with-aem-headless/overview)
