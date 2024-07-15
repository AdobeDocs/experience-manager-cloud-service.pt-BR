---
title: Trabalhar com o Dynamic Media
description: Saiba como usar o Dynamic Media para fornecer ativos para consumo na Web, em dispositivos móveis e em sites sociais.
contentOwner: Rick Brough
feature: Dynamic Media,Asset Management
role: Admin,User
exl-id: 3ec3cb85-88ce-4277-a45c-30e52c75ed42
source-git-commit: 26afff3a39a2a80c1f730287b99f3fb33bff0673
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 6%

---

# Trabalhar com o Dynamic Media {#working-with-dynamic-media}

O [Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) ajuda a fornecer ativos avançados de marketing e merchandising visual sob demanda, dimensionados automaticamente para consumo em sites da Web, móveis e sociais. Usando um conjunto de ativos de origem primária, a Dynamic Media gera e fornece várias variações de conteúdo avançado em tempo real por meio de sua rede global, dimensionável e com desempenho otimizado.

O Dynamic Media oferece experiências de visualização interativa, incluindo zoom, rotação de 360° e vídeo. A Dynamic Media incorpora exclusivamente os fluxos de trabalho da solução Adobe Experience Manager digital asset management (Assets) para simplificar e simplificar o processo de gerenciamento de campanhas digitais.

<!-- >[!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## O que você pode fazer com o Dynamic Media {#what-you-can-do-with-dynamic-media}

O Dynamic Media permite gerenciar os ativos antes de publicá-los. Como trabalhar com ativos em geral é abordado em detalhes em [Trabalhar com o Digital Assets](/help/assets/manage-digital-assets.md). Os tópicos gerais incluem upload, download, edição e publicação de ativos, visualização e edição de propriedades e pesquisa de ativos.

Os recursos exclusivos do Dynamic Media incluem o seguinte:

* [Banners em carrossel](carousel-banners.md)
* [Conjuntos de imagem](image-sets.md)
* [Imagens interativas](interactive-images.md)
* [Vídeos interativos](interactive-videos.md)
* [Conjuntos de mídia mista](mixed-media-sets.md)
* [Imagens panorâmicas](panoramic-images.md)

* [Conjuntos de rotação](spin-sets.md)
* [Vídeo](video.md)
* [Entrega do Dynamic Media Assets](delivering-dynamic-media-assets.md)
* [Gerenciamento do Assets](managing-assets.md)
* [Utilização de visualizações rápidas para criar janelas pop-up personalizadas](custom-pop-ups.md)

Consulte também [Configuração do Dynamic Media](administering-dynamic-media.md).

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media ativado versus Dynamic Media desativado {#dynamic-media-on-versus-dynamic-media-off}

Você pode saber se o Dynamic Media está ativado pelas seguintes características:

* As representações dinâmicas estão disponíveis ao baixar ou visualizar ativos.
* Conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista estão disponíveis.
* As representações PTIFF são criadas.

Ao clicar em um ativo de imagem, a visualização do ativo é diferente com o Dynamic Media ativado. O Dynamic Media usa visualizadores HTML5 sob demanda.

### Representações dinâmicas {#dynamic-renditions}

Representações dinâmicas, como imagens e predefinições do visualizador (em **[!UICONTROL Dynamic]**), estarão disponíveis quando o Dynamic Media for habilitado.

![chlimage_1-358](assets/chlimage_1-358.png)

### Conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista {#image-sets-spins-sets-mixed-media-sets}

Conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista estarão disponíveis se o Dynamic Media estiver ativado.

![chlimage_1-359](assets/chlimage_1-359.png)

### Representações PTIFF {#ptiff-renditions}

Os ativos habilitados para Dynamic Media incluem `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Exibições de ativos alteradas {#asset-views-change}

Com o Dynamic Media habilitado, você pode ampliar e reduzir clicando nos botões `+` e `-`. Você também pode optar por ampliar para uma determinada área. Reverter leva à versão original e você pode tornar a imagem em tela cheia clicando nas setas diagonais. Dynamic Media ativado aparece da seguinte forma:

![chlimage_1-361](assets/chlimage_1-361.png)

Com o Dynamic Media desativado, você pode aumentar ou diminuir o zoom e reverter para o tamanho original:

![chlimage_1-362](assets/chlimage_1-362.png)
