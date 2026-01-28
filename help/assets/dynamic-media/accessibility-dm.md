---
title: Acessibilidade no Dynamic Media
description: Saiba como trabalhar com vídeo no Dynamic Media, como as práticas recomendadas para codificação de vídeos e publicação de vídeos no YouTube. Saiba também como adicionar legendas ocultas, legendas ou marcadores de capítulo a vídeos.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
exl-id: f8d2dcbf-f61a-4b27-a3fc-406e3662adcb
source-git-commit: 4a09e74ae62dba40deb192b1dfe38860bdb43921
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---

# Acessibilidade no Dynamic Media {#accessibility-in-dm}

{{work-with-dynamic-media}}

O Dynamic Media é compatível com controle de teclado e tecnologias assistivas, como leitores de tela JAWS e NVDA, na interface do usuário de criação.

## Suporte para acessibilidade do teclado no Dynamic Media {#keyboard-support-in-dm}

Como o Dynamic Media é um plug-in para [!DNL Experience Manager Assets], a maioria do comportamento de controle do teclado é igual ao de [!DNL Experience Manager Assets]. Por exemplo, o botão `Cancel` no Dynamic Media tem o mesmo destaque de foco que em [!DNL Experience Manager Assets]. Ele também reage à chave `Spacebar` como em [!DNL Experience Manager Assets]. Consulte [atalhos de teclado no Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Os pressionamentos de tecla suportados por elementos individuais da interface do usuário no Dynamic Media são, na maioria dos casos, óbvios e fáceis de encontrar. O controle do teclado no Dynamic Media é sobre o seguinte:

* Capacidade de usar as teclas `Tab` e `Shift+Tab` para navegar entre elementos interativos na página.
O uso de `Tab` avança o foco de entrada para o próximo elemento da interface do usuário na ordem de tabulação; o uso de `Shift+Tab` traz o foco de entrada de volta para o elemento da interface do usuário anterior.
O percurso do foco segue o local natural do elemento da interface do usuário na tela e se move da esquerda para a direita e de cima para baixo. Além disso, se qualquer campo tiver um erro, você pode pressionar `Tab` para mover o foco para ele.
* Capacidade de usar as teclas `Spacebar` e `Enter` para ativar elementos padrão da interface do usuário, como botões e listas suspensas.
* Capacidade de ver o foco do teclado destacado no elemento ativo. O elemento da interface do usuário que tem foco de entrada recebeu uma indicação de foco visual como uma borda renderizada ao redor do elemento da interface do usuário.
* No editor de ponto de acesso, é possível usar alguns pressionamentos de tecla personalizados, como teclas de seta, para interagir com elementos complexos da interface do usuário e reposicionar pontos de acesso.
* No editor de Vídeo Interativo, você pode usar o `Spacebar` para selecionar uma imagem e adicioná-la a um segmento. Além disso, você pode usar a chave `Backspace` para excluir o item selecionado da guia **[!UICONTROL Conteúdo]**. Além disso, pressionar `Tab` funções conforme desejado para navegar entre elementos interativos na página.
* No editor de Recorte de imagem/Recorte inteligente, você pode fazer o seguinte:
   * Use as teclas de seta para recortar o tamanho do quadro ou reposicionar a imagem, ou ambos.
   * A primeira parada de `Tab` realça o quadro de imagem inteiro. Em seguida, é possível usar as teclas de seta no teclado para reposicionar o quadro.
   * As próximas quatro `Tab` paradas são os quatro cantos do quadro. Quando o foco é colocado em um canto do quadro, o canto é realçado. Novamente, você pode usar as teclas de seta no teclado para mover o canto focalizado.
Consulte [Edição do recorte inteligente ou da amostra inteligente de uma única imagem](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md#adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Suporte de tecnologia assistiva no Dynamic Media {#assistive-technology=support-for-dm}

Os elementos da interface do usuário do Dynamic Media funcionam com tecnologias assistivas, como leitores de tela. Por exemplo, ela reconhece pontos de referência em uma página quando você navega em pontos de referência usando o atalho de teclado `D` ou regiões usando o atalho de teclado `R`. Ele também narra o cabeçalho ao navegar usando o atalho de teclado de cabeçalho `H`.

## Suporte para acessibilidade do teclado em visualizadores do Dynamic Media {#keyboard-accessibility-for-dm-viewers}

Todos os componentes de visualizadores do Dynamic Media prontos para uso oferecem suporte à acessibilidade do teclado para seus clientes.

Consulte [Acessibilidade e navegação do teclado](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility#) no Guia de Referência de Visualizadores do Dynamic Media.

## Suporte de tecnologia assistiva em visualizadores do Dynamic Media {#assistive-technology=support-for-dm-viewers}

Todos os componentes do visualizador do Dynamic Media são compatíveis com funções e atributos ARIA (Accessible Rich Internet Applications) para melhorar a integração com tecnologias assistivas, como leitores de tela.
Consulte o tópico de Ajuda **Suporte à tecnologia assistiva** em qualquer tópico de personalização do visualizador no Guia de referência do visualizador do Dynamic Media. Por exemplo, consulte o [Suporte de tecnologia assistiva](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive#) para o visualizador de vídeo ou o [Suporte de tecnologia assistiva](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive#viewers-for-aem-assets-only) para o visualizador de imagem interativa.

## Suporte a legendas ocultas em [!DNL Dynamic Media] {#closed-caption-support}

O Dynamic Media é compatível com a entrega de vídeos e conjuntos de vídeos adaptáveis com legendas ocultas. As legendas devem ser exibidas sobre o conteúdo do vídeo.

Consulte [Vídeo no Dynamic Media - Adicionar legendas ocultas ao vídeo](/help/assets/dynamic-media/video.md#adding-captions-to-video).


>[!MORELIKETHIS]
>
>* [Acessibilidade para soluções da Adobe](https://www.adobe.com/trust/accessibility.html)
>* [Acessibilidade no Experience Manager Assets](/help/assets/dynamic-media/accessibility-dm.md)
