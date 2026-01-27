---
title: Introdução e visão geral
description: Entenda as diferentes opções de vitrine
thumbnail: introducing-aem-commerce.jpg
exl-id: 29410f76-a63f-4b0a-b817-2ed724ad1a3c
feature: Commerce Integration Framework
role: Admin
source-git-commit: e707bddc17208d599491d27c5bc0134cb41233e0
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 1%

---


# Content and Commerce {#content-commerce}

À medida que crescem as expectativas dos clientes quanto a experiências comerciais intencionais e de alto desempenho, as marcas são pressionadas a fornecer mais conteúdo rapidamente, sem sacrificar a qualidade. Com o Adobe Experience Manager, as marcas podem dimensionar e inovar com mais rapidez para criar experiências de comércio imersivas e capturar mais tráfego e o aumento do investimento online.

O Adobe Experience Manager oferece ferramentas eficientes para criar e gerenciar experiências personalizadas e ricas em conteúdo para o cliente. Ao integrar o AEM a uma solução comercial — como Adobe Commerce, Salesforce Commerce, SAP Commerce Cloud ou qualquer outra solução — as marcas podem unificar o conteúdo e o comércio para oferecer jornadas de compra perfeitas em todos os canais.

## Visão geral das abordagens da loja {#overview}

O AEM pode apoiá-lo com base na sua situação e preferências. Use a orientação a seguir para escolher a abordagem certa para você:

* [Usar o Edge Delivery Services (recomendado)](#edge)
* [Usar sua própria loja (integração com o AEM headless)](#own-storefront)
* [Usar a vitrine do AEM CIF](#cif)

### Usar O Edge Delivery Services (Recomendado) {#edge}

Se a sua empresa deseja uma loja mais rápida e com a melhor IA na Web, e se os seus desenvolvedores desejam uma experiência avançada de desenvolvedor, use o [Edge Delivery Services.O ](../edge/overview.md) Edge Delivery Services atende a todas as necessidades atuais e futuras. Dependendo do back-end e da solução, você tem opções diferentes:

#### &#x200B;1. Integração com o Adobe Commerce as a Cloud Service {#acaacs}

A Adobe recomenda usar o Edge Delivery e a [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) como ponto de partida. A loja vem com uma placa-chave pré-integrada com serviços e APIs da Adobe Commerce e oferece vários componentes integrados do Commerce para criar rapidamente uma loja.

Boa opção: experiência típica de vitrine com o Adobe Commerce as a Cloud Service

#### &#x200B;2. Integração com a Adobe Commerce Optimizer (para qualquer solução de terceiros) {#aco}

Se você quiser integrar sua solução comercial existente e melhorar o desempenho do catálogo, a recomendação da Adobe é usar o [Adobe Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview) como a camada de integração moderna. A Commerce Optimizer aprimora sua solução comercial com serviços SaaS de alto desempenho para catálogo e merchandising. Assim como no Adobe Commerce as a Cloud Service, a [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) funciona imediatamente com ela.

Integrações com soluções de comércio comercial, como o Salesforce Commerce, estão disponíveis. Entre em contato com seu representante da Adobe.

Boa opção: experiência típica de vitrine com uma solução comercial existente

#### &#x200B;3. Integração personalizada {#custom}

A Adobe também recomenda usar o Edge Delivery Services se você quiser criar uma integração personalizada. Você pode começar do zero ou reutilizar componentes comerciais existentes da estrutura JS (por exemplo, para a parte transacional) na loja da Edge Delivery. Dessa forma, seus clientes terão uma experiência de compras ultrarrápida, que é amigável para os agentes, enquanto você pode reutilizar seus investimentos existentes para aumentar a TV. Seu ponto de partida é o [Modelo do Edge Delivery](https://www.aem.live/developer/tutorial) padrão.

Boa opção: baixo valor da loja da Edge Delivery

### Usar sua própria loja (integração com o Headless AEM) {#own-storefront}

Você tem uma loja existente (por exemplo, criada com o React JS) e deseja usar o Adobe Experience Manager para gerenciamento e entrega de conteúdo (fragmentos de conteúdo), ativos, além de edição de contexto (editor universal). Seu ponto de partida para uma integração é a [Introdução ao Adobe Experience Manager as a Headless CMS](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/headless/introduction) e o [complemento do CIF](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/authoring/enrich-product-associated-content). O complemento CIF permite uma integração perfeita dos dados do produto no AEM (Pesquisar, navegar e encontrar produtos na interface do usuário do AEM), que você pode usar para criar experiências específicas de comércio.

### vitrine da AEM CIF {#cif}

A recomendação e a arquitetura de referência da Adobe é usar o Edge Delivery Services. A loja da CIF com seus Componentes principais do AEM CIF agora está em modo de manutenção e não deve ser usada em novos projetos. Para referência, consulte a [documentação do CIF.](/help/commerce-cloud/cif-storefront/introduction.md)

>[!NOTE]
>
>Os clientes existentes que desejam aproveitar a nova funcionalidade AEM/Commerce devem mover seu site para o Edge Delivery. Um padrão comum é começar movendo apenas um subconjunto de páginas para o Edge Delivery e executando páginas do Edge Delivery e do CIF lado a lado. Também é possível substituir os componentes do AEM CIF pelos novos [componentes internos do Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/) para aproveitar os novos recursos do Commerce.
