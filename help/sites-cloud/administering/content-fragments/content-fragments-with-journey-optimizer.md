---
title: Uso de fragmentos de conteúdo com o Adobe Journey Optimizer
description: Saiba como os fragmentos de conteúdo podem ser integrados e usados com o Adobe Journey Optimizer.
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
exl-id: 4090ee41-80f1-4389-8961-e4af891f01ff
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 7%

---

# Fragmentos de conteúdo com o Adobe Journey Optimizer {#content-fragments-with-journey-optimizer}

O [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/get-started/get-started) ajuda a fornecer experiências conectadas, contextuais e personalizadas aos seus clientes. Ao integrar o Adobe Experience Manager (AEM) as a Cloud Service ao Adobe Journey Optimizer (AJO), é possível reutilizar o conteúdo do AEM nos canais de entrada do AJO e nos canais de saída do AJO, incluindo Web, SMS, email e outros.

Por exemplo, você pode:

* incorpore facilmente seus [Fragmentos de conteúdo do AEM](/help/sites-cloud/administering/content-fragments/overview.md) ao seu conteúdo de [email do Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/channels/email/email-landing-page)
* visualizar a experiência do AJO diretamente do AEM

A conexão entre os Fragmentos de conteúdo e o AJO simplifica o processo de acesso e aproveitamento do conteúdo do AEM, permitindo a criação de campanhas e jornadas personalizadas e dinâmicas.

Para obter detalhes, comece com a documentação do AJO:

* [Usando fragmentos de conteúdo no AJO](https://experienceleague.adobe.com/docs/journey-optimizer/using/integrations/aem-fragments.html?lang=pt-BR#integrations)
* [Ofertas de Integração do AJO com o Fragmento de Conteúdo](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/decisioning/offer-decisioning/managing-offers-in-the-offer-library/configure-offers/add-representations#urls)

## Configuração do Dispatcher {#dispatcher-configuration}

Para permitir que o AJO acesse os Fragmentos de conteúdo do AEM por meio da [API de gerenciamento de fragmento de conteúdo](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/), é necessário configurar o Dispatcher:

* Em `dispatcher/src/conf.dispatcher.d/filters/filters.any`:

* Adicionar:

  ```xml
  # Allow Content Fragments API requests, required for integration with AJO 
  /200 {/type "allow" /url "/adobe/sites/cf/*" }
  ```

## Informações adicionais {#further-information}

Para obter mais informações, consulte:

* A [Extensão de Referências Externas do AJO](/help/sites-cloud/administering/content-fragments/extension-content-fragment-ajo-external-references.md)
