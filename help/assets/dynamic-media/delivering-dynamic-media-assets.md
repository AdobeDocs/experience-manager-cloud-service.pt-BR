---
title: Entrega de ativos de Mídia dinâmica
description: Saiba como fornecer ativos do Dynamic Media.
feature: Asset Management
topic: Business Practitioner
role: Business Practitioner
exl-id: 4557b561-b3c4-4d6f-8044-2069bda41613
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 7%

---

# Entrega de ativos de Mídia dinâmica{#delivering-dynamic-media-assets}

A maneira de fornecer os ativos da Dynamic Media - vídeo e imagens - depende de como o site está implementado.

Com o Dynamic Media, você tem várias opções:

* Se o seu site estiver hospedado no AEM, você deseja adicionar os ativos do Dynamic Media diretamente à sua página.
* Se o seu site não estiver no AEM, você terá a opção de:

   * Incorporação do vídeo ou imagem ao seu site.
   * Vincule URLs ao aplicativo da Web. Use a vinculação quando desejar fornecer um reprodutor de vídeo como uma janela pop-up ou modal.
   * Se seu site for responsivo, você poderá [fornecer imagens otimizadas](/help/assets/dynamic-media/responsive-site.md).

>[!NOTE]
>
>A geração de imagens inteligentes funciona com as predefinições de imagens existentes. Ele usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade de conexão do navegador ou da rede. Consulte [Imagem inteligente](/help/assets/dynamic-media/imaging-faq.md) para obter mais informações.

Para obter mais informações, consulte os seguintes tópicos:

* [Adicionar ativos Dynamic Media às páginas da Web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md)
* [Incorporação do visualizador de vídeo ou imagem em uma página da Web](/help/assets/dynamic-media/embed-code.md)
* [Ativação da proteção de hotlink no Dynamic Media](/help/assets/dynamic-media/hotlink-protection.md)
* [Vincular URLs ao seu aplicativo web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md)
* [Fornecer imagens otimizadas para um site responsivo](/help/assets/dynamic-media/responsive-site.md)
* [Entrega de conteúdo HTTP2](/help/assets/dynamic-media/http2faq.md)
* [Invalidar o cache CDN por meio do Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
* [Invalidar o cache CDN por meio do Dynamic Media Classic](/help/assets/dynamic-media/invalidate-cdn-cache-dm-classic.md)
* [Uso de conjuntos de regras para transformar URLs](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md)

## Entrega HTTP/2 de ativos do Dynamic Media {#http-delivery-of-dynamic-media-assets}

O AEM agora é compatível com a entrega de todo o conteúdo do Dynamic Media (imagens e vídeo) por HTTP/2. Ou seja, um URL publicado ou código incorporado para a imagem ou vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é então entregue por meio do protocolo HTTP/2. Esse método de entrega melhora a maneira como os navegadores e servidores se comunicam, permitindo uma melhor resposta e tempos de carregamento de todos os seus ativos do Dynamic Media.

Para saber mais, consulte [Perguntas frequentes sobre entrega de conteúdo HTTP/2](/help/assets/dynamic-media/http2faq.md).
