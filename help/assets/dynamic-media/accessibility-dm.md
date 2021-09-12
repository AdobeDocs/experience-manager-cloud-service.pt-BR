---
title: Acessibilidade no Dynamic Media
description: Saiba mais sobre acessibilidade no Dynamic Media e no Dynamic Media Viewers.
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
feature: Accessibility
role: Admin,User
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 1%

---


# Acessibilidade no Dynamic Media {#accessibility-in-dm}

O Dynamic Media oferece suporte a tecnologias de assistência e controle de teclado, como leitores de tela JAWS e NVDA, na interface de criação do usuário.

## Suporte à acessibilidade de teclado no Dynamic Media {#keyboard-support-in-dm}

Como o Dynamic Media é um plug-in para [!DNL Experience Manager Assets], a maioria do comportamento de controle do teclado é igual ao comportamento em [!DNL Experience Manager Assets]. Por exemplo, o botão `Cancel` no Dynamic Media tem o mesmo realce de foco que em [!DNL Experience Manager Assets]. Ele também reage à chave `Spacebar` como em [!DNL Experience Manager Assets]. Consulte [atalhos de teclado em Assets](/help/assets/accessibility.md#keyboard-shortcuts).

Os pressionamentos de tecla suportados pelos elementos da interface do usuário individual no Dynamic Media são, na maioria dos casos, óbvios e fáceis de encontrar. O controle de teclado no Dynamic Media é sobre o seguinte:

* Capacidade de usar `Tab` e `Shift+Tab` pressionamentos de teclas para navegar entre elementos interativos na página.
Usar `Tab` avança o foco de entrada para o próximo elemento da interface do usuário na ordem de tabulação; usar `Shift+Tab` traz o foco de entrada de volta ao elemento anterior da interface do usuário.
A travessia de foco segue a localização do elemento da interface de usuário natural na tela e se move de esquerda para direita e de cima para baixo. Além disso, se qualquer campo tiver um erro, você poderá pressionar `Tab` para mover o foco para ele.
* Capacidade de usar as teclas `Spacebar` e `Enter` para ativar elementos padrão da interface do usuário, como botões e listas suspensas.
* Capacidade de ver o foco do teclado realçar no elemento ativo. O elemento da interface do usuário que tem o foco de entrada recebeu uma indicação do foco visual como uma borda renderizada em torno do elemento da interface do usuário.
* No editor de ponto de acesso, você pode usar alguns pressionamentos de tecla personalizados, como teclas de seta, para interagir com elementos complexos da interface do usuário e reposicionar pontos de acesso.
* No editor de Vídeo interativo, você pode usar o `Spacebar` para selecionar uma imagem e adicioná-la a um segmento. Além disso, você pode usar a tecla `Backspace` para excluir o item selecionado da guia **[!UICONTROL Content]**. Além disso, pressionar `Tab` funções conforme desejado para navegar entre elementos interativos na página.
* No editor Recortar de imagem/Recorte inteligente, você pode fazer o seguinte:
   * Use as teclas de seta para recortar o tamanho do quadro ou reposicionar a imagem, ou ambos.
   * A primeira interrupção `Tab` destaca todo o quadro da imagem. Você pode usar as teclas de seta no teclado para reposicionar o quadro.
   * As próximas quatro paradas `Tab` são os quatro cantos do quadro. Quando o foco é colocado em um canto do quadro, o canto é realçado. Novamente, você pode usar as teclas de seta no teclado para mover o canto focado.
Consulte [Editar o recorte inteligente ou a amostra inteligente de uma única imagem](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (Experience Manager 6.5) or Coral Spectrum (in Skyline)) as entire Experience Manager Assets.  -->

<!-- In the Hotspot editor, Dynamic Media lets you use arrow keys to control the position of a hot spot. See [Carousel Banners](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) or [Interactive Images](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)  -->

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Suporte à tecnologia assistiva no Dynamic Media {#assistive-technology=support-for-dm}

Os elementos da interface do usuário do Dynamic Media funcionam com tecnologias de assistência, como leitores de tela. Por exemplo, ele reconhece marcos em uma página ao navegar por marcos usando o atalho de teclado `D` ou regiões usando o atalho de teclado `R`. Ele também narra o cabeçalho ao navegar usando o atalho de teclado do cabeçalho `H`.

## Suporte para acessibilidade de teclado em visualizadores Dynamic Media {#keyboard-accessibility-for-dm-viewers}

Todos os componentes prontos para uso dos visualizadores Dynamic Media suportam a acessibilidade do teclado para seus clientes.

Consulte [Acessibilidade e navegação do teclado](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) no Guia de Referência de Visualizadores do Dynamic Media.

## Suporte à tecnologia assistiva em visualizadores Dynamic Media {#assistive-technology=support-for-dm-viewers}

Todos os componentes do visualizador do Dynamic Media suportam funções e atributos ARIA (Accessible Rich Internet Applications) para melhorar a integração com tecnologias de assistência, como leitores de tela.
Consulte o tópico de Ajuda **Suporte à tecnologia assistiva** em qualquer tópico de personalização do visualizador no Guia de referência de visualizadores do Dynamic Media. Por exemplo, consulte [Suporte à tecnologia assistiva](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) para o visualizador de Vídeo ou [Suporte à tecnologia assistiva](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html#viewers-for-aem-assets-only) para o visualizador de Imagem interativa.

>[!MORELIKETHIS]
>
>* [Acessibilidade para soluções Adobe](https://www.adobe.com/accessibility.html)
>* [Acessibilidade em ativos Experience Manager](/help/assets/dynamic-media/accessibility-dm.md)

