---
title: Trabalhar com o Dynamic Media
description: Saiba como usar o Dynamic Media para fornecer ativos para consumo na Web, em dispositivos móveis e em sites sociais.
contentOwner: Rick Brough
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 13%

---

# Trabalhar com o Dynamic Media {#working-with-dynamic-media}

O [Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) ajuda a fornecer ativos de marketing e merchandising visual por demanda, automaticamente dimensionados para o consumo na Web, em dispositivos móveis e sites sociais. Usando um conjunto de ativos de origem primária, a Dynamic Media gera e fornece várias variações de conteúdo rico em tempo real por meio de sua rede global, escalável e otimizada para desempenho.

O Dynamic Media fornece experiências de visualização interativas, incluindo zoom, rotação de 360° e vídeo. O Dynamic Media incorpora exclusivamente os fluxos de trabalho da solução de gerenciamento de ativos digitais (Assets) da Adobe Experience Manager para simplificar e simplificar o processo de gerenciamento de campanhas digitais.

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## O que você pode fazer com o Dynamic Media {#what-you-can-do-with-dynamic-media}

O Dynamic Media permite gerenciar seus ativos antes de publicá-los. Como trabalhar com ativos em geral é abordado detalhadamente em [Trabalhar com ativos digitais](/help/assets/manage-digital-assets.md). Os tópicos gerais incluem upload, download, edição e publicação de ativos; visualizar e editar propriedades e procurar ativos.

Os recursos exclusivos ao Dynamic Media incluem o seguinte:

* [Banners em carrossel](carousel-banners.md)
* [Conjuntos de imagem](image-sets.md)
* [Imagens interativas](interactive-images.md)
* [Vídeos interativos](interactive-videos.md)
* [Conjuntos de mídia mista](mixed-media-sets.md)
* [Imagens panorâmicas](panoramic-images.md)

* [Conjuntos de rotação](spin-sets.md)
* [Vídeo](video.md)
* [Entrega de ativos de Mídia dinâmica](delivering-dynamic-media-assets.md)
* [Gerenciar ativos](managing-assets.md)
* [Usar o Quick views para criar janelas pop-up personalizadas](custom-pop-ups.md)

Consulte também [Configuração do Dynamic Media](administering-dynamic-media.md).

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media ativado versus Dynamic Media desativado {#dynamic-media-on-versus-dynamic-media-off}

É possível saber se o Dynamic Media está ativado (ativado) pelas seguintes características:

* As representações dinâmicas estão disponíveis ao baixar ou visualizar ativos.
* Conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista estão disponíveis.
* As representações PTIFF são criadas.

Quando você clica em um ativo de imagem, a exibição do ativo é diferente com o Dynamic Media ativado. O Dynamic Media usa os visualizadores HTML5 sob demanda.

### Representações dinâmicas {#dynamic-renditions}

Representações dinâmicas, como predefinições de imagem e do visualizador (em **[!UICONTROL Dinâmico]**) estão disponíveis quando o Dynamic Media está ativado.

![chlimage_1-358](assets/chlimage_1-358.png)

### Conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista {#image-sets-spins-sets-mixed-media-sets}

Conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista estarão disponíveis se o Dynamic Media estiver ativado.

![chlimage_1-359](assets/chlimage_1-359.png)

### Representações PTIFF {#ptiff-renditions}

Os ativos habilitados para Dynamic Media incluem `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Alteração nas exibições de ativos {#asset-views-change}

Com o Dynamic Media ativado, é possível ampliar e diminuir o zoom clicando no botão `+` e `-` botões. Também é possível clicar/tocar para ampliar determinadas áreas. Reverter o traz para a versão original e você pode fazer a imagem em tela cheia clicando nas setas diagonais. O Dynamic Media ativado é exibido da seguinte maneira:

![chlimage_1-361](assets/chlimage_1-361.png)

Com o Dynamic Media desativado, é possível ampliar e diminuir o zoom e reverter para o tamanho original:

![chlimage_1-362](assets/chlimage_1-362.png)
