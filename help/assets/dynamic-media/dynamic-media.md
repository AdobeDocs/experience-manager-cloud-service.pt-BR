---
title: Trabalhar com o Dynamic Media
description: Saiba como usar o Dynamic Media para fornecer ativos para consumo em sites da Web, móveis e sociais.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 28%

---


# Trabalhar com o Dynamic Media {#working-with-dynamic-media}

O [Dynamic Media](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) ajuda a fornecer ativos de marketing e merchandising visual por demanda, automaticamente dimensionados para o consumo na Web, em dispositivos móveis e sites sociais. Usando um conjunto de ativos principais, o Dynamic Media gera e oferece diversas variações de conteúdo atraente em tempo real na rede global, dimensionável e otimizada para desempenho.

O Dynamic Media oferece experiências de visualização interativas, incluindo zoom, rotação de 360 graus e vídeo. O Dynamic Media incorpora de forma exclusiva os fluxos de trabalho da solução de gerenciamento de ativos digitais do Adobe Experience Manager (Assets) para simplificar e agilizar o processo de gerenciamento de campanhas digitais.

>[!NOTE]
>
>Um artigo da Comunidade está disponível em [Trabalhar com o Adobe Experience Manager e o Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html).

## O que você pode fazer com o Dynamic Media {#what-you-can-do-with-dynamic-media}

O Dynamic Media permite que você gerencie seus ativos antes de publicá-los. Como trabalhar com ativos em geral é abordado detalhadamente em [Trabalhar com ativos](/help/assets/manage-digital-assets.md)digitais. Tópicos gerais incluem upload, download, edição e publicação de ativos; visualizar e editar propriedades e procurar ativos.

Os recursos exclusivos do Dynamic Media incluem o seguinte:

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
* [Uso do Quickviews para criar pop-ups personalizados](custom-pop-ups.md)

Consulte também [Configuração do Dynamic Media](administering-dynamic-media.md).

<!-- 

OBSOLETE UNTIL INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE
>[!NOTE]
>
>To understand the differences between using Dynamic Media and integrating Dynamic Media Classic with AEM, see [Dynamic Media Classic integration versus Dynamic Media](/help/sites-cloud/administering/integrating-scene7.md#aem-scene-integration-versus-dynamic-media).

-->

## Dynamic Media ativado versus Dynamic Media desativado {#dynamic-media-on-versus-dynamic-media-off}

Você pode saber se o Dynamic Media está ativado (ativado) pelas seguintes características:

* As representações dinâmicas estão disponíveis ao baixar ou visualizar ativos.
* Conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista estão disponíveis.
* Execuções PTIFF são criadas.

Quando você clica em um ativo de imagem, a visualização do ativo é diferente com o Dynamic Media ativado. O Dynamic Media usa visualizadores HTML5 sob demanda.

### Execuções dinâmicas {#dynamic-renditions}

Execuções dinâmicas, como predefinições de imagem e visualizador (em **[!UICONTROL Dinâmico]**), estão disponíveis quando o Dynamic Media está ativado.

![chlimage_1-358](assets/chlimage_1-358.png)

### Conjuntos de imagens, conjuntos de rotação, conjuntos de mídia mista {#image-sets-spins-sets-mixed-media-sets}

Conjuntos de imagens, conjuntos de rotação e conjuntos de mídia mista estarão disponíveis se o Dynamic Media estiver ativado.

![chlimage_1-359](assets/chlimage_1-359.png)

### Execuções PTIFF {#ptiff-renditions}

Os ativos habilitados para mídia dinâmica incluem `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Alteração de visualizações de ativos {#asset-views-change}

Com o Dynamic Media ativado, você pode aumentar e diminuir o zoom clicando nos botões `+` e `-` . Você também pode clicar/tocar para aplicar zoom em determinada área. O Reverter leva você para a versão original e você pode tornar a imagem em tela cheia clicando nas setas diagonais. O Dynamic Media ativado tem a seguinte aparência:

![chlimage_1-361](assets/chlimage_1-361.png)

Com o Dynamic Media desativado, é possível aumentar e diminuir o zoom e reverter para o tamanho original:

![chlimage_1-362](assets/chlimage_1-362.png)
