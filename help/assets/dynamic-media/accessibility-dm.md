---
title: Acessibilidade no Dynamic Media
description: Saiba como trabalhar com vídeo no Dynamic Media, como práticas recomendadas para codificação de vídeos, publicação de vídeos no YouTube e exibição de relatórios de vídeo. Saiba também como adicionar legendas ocultas, legendas ou marcadores de capítulo aos vídeos.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
exl-id: f8d2dcbf-f61a-4b27-a3fc-406e3662adcb
source-git-commit: 0d3262a3182063e69f764339e7937e2f83ad7bbb
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---

# Acessibilidade no Dynamic Media {#accessibility-in-dm}

O Dynamic Media oferece suporte a tecnologias de assistência e controle de teclado, como leitores de tela JAWS e NVDA, na interface de criação do usuário.

## Suporte à acessibilidade de teclado no Dynamic Media {#keyboard-support-in-dm}

Como o Dynamic Media é um plug-in para [!DNL Experience Manager Assets], a maioria do comportamento de controle do teclado é igual ao comportamento do [!DNL Experience Manager Assets]. Por exemplo, a variável `Cancel` no Dynamic Media tem o mesmo realce de foco do [!DNL Experience Manager Assets]. Reage também ao `Spacebar` como em [!DNL Experience Manager Assets]. Consulte [atalhos de teclado do Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Os pressionamentos de tecla suportados pelos elementos da interface do usuário individual no Dynamic Media são, na maioria dos casos, óbvios e fáceis de encontrar. O controle de teclado no Dynamic Media é sobre o seguinte:

* Capacidade de usar `Tab` e `Shift+Tab` pressionamentos de teclas para navegar entre elementos interativos na página.
Usando `Tab` avança o foco de entrada para o próximo elemento da interface do usuário na ordem de tabulação; usar `Shift+Tab` traz o foco de entrada de volta ao elemento anterior da interface do usuário.
A travessia de foco segue a localização do elemento da interface de usuário natural na tela e se move de esquerda para direita e de cima para baixo. Além disso, se algum campo tiver um erro, você poderá pressionar `Tab` para mover o foco para ele.
* Capacidade de usar o `Spacebar` e `Enter` tecla para ativar elementos padrão da interface do usuário, como botões e listas suspensas.
* Capacidade de ver o foco do teclado realçar no elemento ativo. O elemento da interface do usuário que tem o foco de entrada recebeu uma indicação do foco visual como uma borda renderizada em torno do elemento da interface do usuário.
* No editor de ponto de acesso, você pode usar alguns pressionamentos de tecla personalizados, como teclas de seta, para interagir com elementos complexos da interface do usuário e reposicionar pontos de acesso.
* No editor de Vídeo interativo, você pode usar o `Spacebar` para selecionar uma imagem e adicioná-la a um segmento. Além disso, você pode usar o `Backspace` chave para excluir o item selecionado da **[!UICONTROL Conteúdo]** guia . Além disso, pressionar `Tab` conforme desejado para navegar entre elementos interativos na página.
* No editor Recortar de imagem/Recorte inteligente, você pode fazer o seguinte:
   * Use as teclas de seta para recortar o tamanho do quadro ou reposicionar a imagem, ou ambos.
   * O primeiro `Tab` a parada realça todo o quadro da imagem. Você pode usar as teclas de seta no teclado para reposicionar o quadro.
   * Os próximos quatro `Tab` as paradas são os quatro cantos do quadro. Quando o foco é colocado em um canto do quadro, o canto é realçado. Novamente, você pode usar as teclas de seta no teclado para mover o canto focado.
Consulte [Edição do recorte inteligente ou da amostra inteligente de uma única imagem](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Suporte à tecnologia assistiva no Dynamic Media {#assistive-technology=support-for-dm}

Os elementos da interface do usuário do Dynamic Media funcionam com tecnologias de assistência, como leitores de tela. Por exemplo, ele reconhece marcos em uma página ao navegar por marcos usando o atalho do teclado `D` ou regiões que usam atalho do teclado `R`. Ele também narra o cabeçalho ao navegar usando o atalho do teclado do cabeçalho `H`.

## Suporte para acessibilidade de teclado em visualizadores Dynamic Media {#keyboard-accessibility-for-dm-viewers}

Todos os componentes prontos para uso dos visualizadores Dynamic Media suportam a acessibilidade do teclado para seus clientes.

Consulte [Acessibilidade e navegação do teclado](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) no Guia de referência de visualizadores do Dynamic Media.

## Suporte à tecnologia assistiva em visualizadores Dynamic Media {#assistive-technology=support-for-dm-viewers}

Todos os componentes do visualizador do Dynamic Media suportam funções e atributos ARIA (Accessible Rich Internet Applications) para melhorar a integração com tecnologias de assistência, como leitores de tela.
Consulte a **Suporte à tecnologia assistiva** Tópico de Ajuda em qualquer tópico de personalização do visualizador no Guia de Referência de Visualizadores do Dynamic Media. Por exemplo, consulte [Suporte à tecnologia assistiva](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) para o visualizador de vídeo ou [Suporte à tecnologia assistiva](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) para o visualizador de Imagem interativa .

## Suporte a legendas ocultas em [!DNL Dynamic Media] {#closed-caption-support}

O Dynamic Media oferece suporte para vídeos e conjuntos de vídeos adaptáveis com legendas ocultas. As legendas devem ser exibidas sobre o conteúdo do vídeo.

Consulte [Vídeo no Dynamic Media - Adicionar legendas ou legendas ocultas ao vídeo](/help/assets/dynamic-media/video.md#adding-captions-to-video).


>[!MORELIKETHIS]
>
>* [Acessibilidade para soluções Adobe](https://www.adobe.com/accessibility.html)
>* [Acessibilidade no Experience Manager Assets](/help/assets/dynamic-media/accessibility-dm.md)

