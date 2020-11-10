---
title: Acessibilidade em [!DNL Dynamic Media]
description: Saiba como trabalhar com ativos 3D no Dynamic Media
contentOwner: Rick Brough
topic-tags: introduction
content-type: reference
translation-type: tm+mt
source-git-commit: 7af8ddda4aee093b22147db9be9f65cd0c131c04
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# Acessibilidade no Dynamic Media {#working-with-three-d-assets-dm}

O Dynamic Media suporta o controle de teclado e tecnologias de assistência, como leitores de tela JAWS e NVDA, na interface do usuário de criação.



## Suporte de acessibilidade de teclado no Dynamic Media

Os pressionamentos de teclas suportados por elementos individuais da interface do usuário são, na maioria dos casos, óbvios e fáceis de descobrir. O controle de teclado no Dynamic Media é sobre o seguinte:

* Capacidade de usar `Tab` e `Shift+Tab` pressionar teclas para navegar entre elementos interativos na página.
O uso `Tab` avança o foco de entrada para o próximo elemento da interface do usuário na ordem de tabulação; o uso `Shift+Tab` traz o foco de entrada de volta ao elemento anterior da interface do usuário.
O foco transversal segue a localização do elemento natural da interface do usuário na tela e se move de esquerda para direita e de cima para baixo.
* Capacidade de usar a tecla `Spacebar` e `Enter` para ativar elementos padrão da interface do usuário, como botões, lista suspensa e assim por diante.
* A capacidade de ver o foco do teclado é realçada no elemento ativo. O elemento da interface do usuário que tem foco de entrada pode receber uma indicação de foco visual como uma borda renderizada ao redor do elemento da interface do usuário.
* Capacidade de usar alguns pressionamentos de teclas personalizados para interagir com elementos complexos da interface do usuário, como teclas de seta no Editor de ponto de acesso. No Editor de recorte de imagem/recorte inteligente, você pode usar as teclas de seta para recortar o tamanho do quadro ou reposicionar a imagem, ou ambos.

Como o Dynamic Media é um plug-in para AEM Assets, a maioria do comportamento de controle do teclado é exatamente o mesmo do AEM Assets. Por exemplo, o `Cancel` botão no Dynamic Media tem o mesmo realce de foco do AEM Assets e reage à `Spacebar` tecla do AEM Assets. Consulte Atalhos de [teclado em Ativos](/help/assets/accessibility.md#keyboard-shortcuts). As exceções são o editor de Hotspot e os editores de Recorte de imagem/Recorte inteligente.

<!-- Keyboarding is the same because Dynamic Media is using the same UI library (Coral 3 (AEM 6.5) or Coral Spectrum (in Skyline)) as entire AEM Assets.  -->

No editor de Hotspot, o Dynamic Media permite que você use teclas de seta para controlar a posição de um hot spot. Consulte Banners [de](/help/assets/dynamic-media/carousel-banners.md##adding-hotspots-or-image-maps-to-an-image-banner) carrossel ou imagens [interativas](/help/assets/dynamic-media/interactive-images.md#adding-hotspots-to-an-image-banner)

No editor de Recorte de imagem/Recorte inteligente, use as teclas de seta para recortar o tamanho do quadro ou reposicionar a imagem, ou ambos. Consulte [Editar o recorte inteligente ou a amostra inteligente de uma única imagem](/help/assets/dynamic-media/image-profiles.md#editing-the-smart-crop-or-smart-swatch-of-a-single-image)

<!-- I think we should definitely mention this in the DM-specific area of documentation for keyboard support. -->

<!-- I would not get into much of details of specific keyboard support logic of these editors. One of the reasons - chances are that accessibility support will receive Phase2-like attention, with more holistic approach. -->

## Suporte de acessibilidade de teclado para visualizadores de Dynamic Media {#keyboard-accessibility-for-dm-viewers}

Todos os componentes predefinidos do visualizador de Dynamic Media oferecem suporte à acessibilidade do teclado para seus clientes.

Consulte Acesso ao [teclado e navegação](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/c-keyboard-accessibility.html) no Guia de Referência do Visualizador de Mídia Dinâmica.

## Suporte técnico de assistência para visualizadores de Dynamic Media {#assistive-technology=support-for-dm-viewers}

Todos os componentes do visualizador no Dynamic Media suportam funções e atributos ARIA (Accessible Rich Internet Applications) para melhorar a integração com tecnologias de assistência, como leitores de tela.

Consulte o tópico Ajuda para suporte **à tecnologia** Assistive em qualquer tópico do visualizador personalizado no Guia de Referência do Visualizador de Mídia Dinâmica. Por exemplo, consulte Suporte [à tecnologia](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/r-html5-video-viewer-20-assistive.html) Assistive para o Visualizador de vídeo ou Suporte [à tecnologia](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-images/c-html5-aem-interactive-image-assistive.html?lang=en#viewers-for-aem-assets-only) Assistive para o Visualizador de Imagem interativa.

>[!MORELIKETHIS]
>
>* [Acessibilidade para soluções de Adobe](https://www.adobe.com/accessibility.html)
>* [Acessibilidade nos ativos Experience Manager](/help/assets/dynamic-media/accessibility-dm.md)

