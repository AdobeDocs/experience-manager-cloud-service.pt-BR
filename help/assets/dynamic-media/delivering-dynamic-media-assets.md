---
title: Entregar ativos do Dynamic Media
description: Saiba como fornecer ativos do Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 7%

---

# Entregar ativos do Dynamic Media{#delivering-dynamic-media-assets}

A maneira de fornecer os ativos do Dynamic Media, como vídeo e imagens, depende de como o site é implementado.

Com o Dynamic Media, você tem várias opções:

* Se o seu site estiver hospedado no Adobe Experience Manager, será necessário adicionar os ativos do Dynamic Media diretamente à sua página.
* Se o site não estiver no Experience Manager, você terá a opção de:

   * Incorporar o vídeo ou a imagem no site.
   * Vincule URLs ao aplicativo da Web. Use a vinculação quando quiser fornecer um reprodutor de vídeo como uma janela pop-up ou modal.
   * Se o site for responsivo, você poderá [fornecer imagens otimizadas](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>As imagens inteligentes funcionam com as predefinições de imagens existentes. Ele usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte [Imagem inteligente](/help/assets/dynamic-media/imaging-faq.md) para obter mais informações.

Para obter mais informações, consulte os seguintes tópicos:

* [Adicionar ativos do Dynamic Media a páginas da Web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Incorporar o visualizador de vídeo ou imagem em uma página da Web](/help/assets/dynamic-media/embed-code.md)
* [Ativar proteção de hotlink no Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Vincular URLs ao aplicativo web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Entregar imagens otimizadas para um site responsivo](/help/assets/dynamic-media/responsive-site.md)
* [Entrega de conteúdo HTTP2](/help/assets/dynamic-media/http2faq.md)
* [Invalidar o cache da CDN por meio do Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidar o cache da CDN por meio do Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Usar conjuntos de regras para transformar URLs](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Entrega HTTP/2 de ativos do Dynamic Media {#http-delivery-of-dynamic-media-assets}

O Experience Manager agora é compatível com a entrega de todo o conteúdo do Dynamic Media (imagens e vídeo) via HTTP/2. Ou seja, um URL publicado ou código incorporado para a imagem ou vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é entregue por meio do protocolo HTTP/2. Esse método de entrega melhora a maneira como os navegadores e servidores se comunicam, permitindo melhores tempos de resposta e carregamento de todos os ativos do Dynamic Media.

Para saber mais, consulte [Perguntas frequentes sobre entrega de conteúdo HTTP/2](/help/assets/dynamic-media/http2faq.md).
