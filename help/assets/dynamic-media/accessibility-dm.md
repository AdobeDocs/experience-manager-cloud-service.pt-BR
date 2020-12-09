---
title: Acessibilidade em [!DNL Dynamic Media]
description: Saiba mais sobre a acessibilidade no Dynamic Media e no Dynamic Media Viewers.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: fd75af0bf0c16e20c3b98703af14f329ea6c6371
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---


# Acessibilidade no Dynamic Media {#working-with-three-d-assets-dm}

A Dynamic Media oferece suporte a tecnologias de controle de teclado e assistência, como leitores de tela JAWS e NVDA, na interface do usuário de criação.

## Suporte de acessibilidade de teclado no Dynamic Media

Como o Dynamic Media é um plug-in para o Experience Manager Assets, a maioria do comportamento de controle do teclado é exatamente igual ao dos Experience Manager Assets. Por exemplo, o botão `Cancel` no Dynamic Media tem o mesmo realce de foco que nos Ativos do Experience Manager e reage à tecla `Spacebar` como nos Ativos do Experience Manager. Consulte [Atalhos de teclado em Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Os pressionamentos de teclas suportados por elementos individuais da interface do usuário no Dynamic Media são, na maioria dos casos, óbvios e fáceis de descobrir. O controle de teclado no Dynamic Media é sobre o seguinte:

* Capacidade de usar `Tab` e `Shift+Tab` pressionamentos de teclas para navegar entre elementos interativos na página.
Usar `Tab` avança o foco de entrada para o próximo elemento da interface do usuário na ordem de tabulação; usar `Shift+Tab` traz o foco de entrada de volta ao elemento anterior da interface do usuário.
O foco transversal segue a localização do elemento natural da interface do usuário na tela e se move de esquerda para direita e de cima para baixo. Além disso, se algum campo tiver um erro, pressione `Tab` para mover o foco para ele.
* Capacidade de usar as teclas `Spacebar` e `Enter` para ativar elementos padrão da interface do usuário, como botões, lista suspensa e assim por diante.
* A capacidade de ver o foco do teclado é realçada no elemento ativo. O elemento da interface do usuário que tem foco de entrada pode receber uma indicação de foco visual como uma borda renderizada ao redor do elemento da interface do usuário.
* No editor do Hotspot, você pode usar alguns pressionamentos de teclas personalizados, como teclas de seta, para interagir com elementos complexos da interface do usuário para reposicionar pontos de conexão.
* No editor de vídeo interativo, você pode usar `Spacebar` para selecionar uma imagem e adicioná-la a um segmento. Além disso, você pode usar a tecla `Backspace` para excluir o item selecionado da guia **[!UICONTROL Conteúdo]**. Além disso, pressionar `Tab` funciona conforme desejado para navegar entre os elementos interativos na página.
* No editor de recorte de imagem/recorte inteligente, você pode fazer o seguinte:
   * Use as teclas de seta para recortar o tamanho do quadro, reposicionar a imagem ou ambas.
   * A primeira parada `Tab` realça todo o quadro da imagem. Você pode usar as teclas de seta no teclado para reposicionar o quadro.
   * As quatro próximas `Tab` paradas são os quatro cantos do quadro. Quando o foco é colocado em um canto do quadro, o canto é realçado. Novamente, você pode usar as teclas de seta no teclado para mover o canto focalizado.
Consulte [Editar o recorte inteligente ou a amostra inteligente de uma única imagem](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Suporte a tecnologia assistiva na Dynamic Media {#assistive-technology=support-for-dm}

Os elementos da interface do usuário Dynamic Media funcionam com tecnologias de assistência, como leitores de tela. Por exemplo, ele reconhece marcos em uma página quando você navega por marcos usando o atalho de teclado `D` ou regiões que usam o atalho de teclado `R`. Ele também narrará o cabeçalho ao navegar usando o atalho de cabeçalho do teclado `H`.

## Suporte de acessibilidade de teclado nos visualizadores Dynamic Media {#keyboard-accessibility-for-dm-viewers}

Todos os componentes predefinidos do visualizador Dynamic Media suportam a acessibilidade do teclado para seus clientes.

Consulte [Acesso ao teclado e navegação](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) no Guia de referência do Dynamic Media Viewers.

## Suporte a tecnologia assistiva em visualizadores Dynamic Media {#assistive-technology=support-for-dm-viewers}

Todos os componentes do visualizador Dynamic Media suportam funções e atributos ARIA (Accessible Rich Internet Applications) para melhorar a integração com tecnologias de assistência, como leitores de tela.
Consulte o tópico **Suporte à tecnologia assistiva** Ajuda em qualquer tópico personalizado do visualizador no Guia de Referência do Dynamic Media Viewers. Por exemplo, consulte [Suporte à tecnologia assistiva](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) para o Visualizador de vídeo, ou [Suporte à tecnologia assistiva](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) para o Visualizador de imagem interativa.

>[!MORELIKETHIS]
>
>* [Acessibilidade para soluções de Adobe](https://www.adobe.com/accessibility.html)
>* [Acessibilidade nos ativos Experience Manager](/help/assets/dynamic-media/accessibility-dm.md)

