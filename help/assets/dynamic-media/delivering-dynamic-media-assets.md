---
title: Entrega de ativos de Mídia dinâmica
description: Saiba como fornecer ativos de mídia dinâmica
translation-type: tm+mt
source-git-commit: 7a2eef19a3807d02e7eba0ce177465aabc35a53e
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 15%

---


# Entrega de ativos de Mídia dinâmica{#delivering-dynamic-media-assets}

A forma como você pode fornecer seus ativos de mídia dinâmica - vídeo e imagens - depende de como seu site é implementado.

Com a Mídia dinâmica, você tem várias opções:

* Se o seu site estiver hospedado no AEM, convém adicionar os ativos de mídia dinâmica diretamente à sua página.
* Se o site não estiver no AEM, você terá a opção de:

   * Incorporar seu vídeo ou imagem em seu site.
   * Vincule URLs ao seu aplicativo da Web. Use a vinculação quando quiser fornecer um player de vídeo como uma janela pop-up ou modal.
   * Se o site estiver respondendo, você poderá [fornecer imagens otimizadas.](/help/assets/dynamic-media/responsive-site.md)

>[!NOTE]
>
>A geração de imagens inteligentes funciona com as predefinições de imagens existentes e usa inteligência no último milissegundo do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte [Imagens inteligentes](/help/assets/dynamic-media/imaging-faq.md) para obter mais informações.

Para obter mais informações, consulte os seguintes tópicos:

* [Adicionar ativos de mídia dinâmica a páginas da Web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Incorporação do visualizador de vídeo ou imagem em uma página da Web](/help/assets/dynamic-media/embed-code.md)
* [Ativação da proteção de hotlink no Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Vincular URLs à sua Aplicação web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Fornecer imagens otimizadas para um site responsivo](/help/assets/dynamic-media/responsive-site.md)
* [DELIVERY HTTP2 do conteúdo](/help/assets/dynamic-media/http2faq.md)
* [Invalidar o cache CDN por meio do Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidar o cache CDN por meio do Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Uso de conjuntos de regras para transformar URLs](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## DELIVERY HTTP/2 de ativos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM agora suporta o delivery de todo o conteúdo de Dynamic Media (imagens e vídeo) por HTTP/2. Ou seja, um URL publicado ou um código incorporado para a imagem ou o vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é então entregue por meio do protocolo HTTP/2. Este método de delivery melhora a maneira como os navegadores e servidores se comunicam, permitindo uma melhor resposta e tempos de carregamento de todos os seus ativos de Dynamic Media.

Consulte [Delivery HTTP/2 de Perguntas frequentes sobre conteúdo](/help/assets/dynamic-media/http2faq.md) para saber mais.
