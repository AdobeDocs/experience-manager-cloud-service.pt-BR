---
title: Incorporação do visualizador de vídeo ou imagem do Dynamic Media em uma página da Web
description: Saiba como incorporar vídeos ou imagens do Dynamic Media em uma página da Web
translation-type: tm+mt
source-git-commit: 7dae5c0ed82687415719cd2d72f98028cf0a8e64
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 22%

---


# Incorporar o vídeo de Dynamic Media, o visualizador de imagens ou o visualizador de dimensões em uma página da Web {#embedding-the-video-or-image-viewer-on-a-web-page}

Use o recurso **[!UICONTROL Incorporar código]** quando quiser reproduzir o vídeo ou exibir um ativo incorporado em uma página da Web. Copie o código incorporado na área de transferência para poder colá-lo nuas páginas da Web. A edição do código não é permitida na caixa de diálogo **[!UICONTROL Incorporar código]**.

Você incorpora URLs somente se _não_ estiver usando o AEM como seu WCM. Se você estiver usando o AEM como seu WCM, [adicione os ativos diretamente na sua página.](adding-dynamic-media-assets-to-pages.md)

See [Linking URLs to your Web Application.](linking-urls-to-yourwebapplication.md)

See [Delivering Optimized Images for a Responsive Site.](responsive-site.md)

>[!NOTE]
>
>O código incorporado não está disponível para cópia até que você tenha publicado o ativo selecionado. Além disso, você também deve publicar a predefinição do visualizador ou a predefinição da imagem.
>
>Consulte [Publicação de ativos](publishing-dynamicmedia-assets.md).
>
>See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).
>
>See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

**Para incorporar o visualizador de vídeo ou imagem do Dynamic Media em uma página da Web**

1. Navegue até o vídeo *publicado* ou ativo de imagem cujo código incorporado você deseja copiar.

   Lembre-se de que o código incorporado só está disponível para cópia *depois* que você *publicou* os ativos pela primeira vez. Além disso, a predefinição do visualizador ou da imagem também deve ser publicada.

   Consulte [Publicação de ativos.](publishing-dynamicmedia-assets.md)

   See [Publishing Viewer Presets](managing-viewer-presets.md#publishing-viewer-presets).

   See [Publishing Image Presets](managing-image-presets.md#publishing-image-presets).

1. No painel esquerdo, selecione o menu suspenso e toque em **[!UICONTROL Visualizadores]**.
1. No painel esquerdo, toque no nome predefinido do visualizador. A predefinição do visualizador é aplicada ao ativo.
1. Toque em **[!UICONTROL Incorporar]**.
1. Na caixa de diálogo **[!UICONTROL Incorporar código]** , copie o código inteiro para a área de transferência e toque em **[!UICONTROL Fechar]**.
1. Cole o código incorporado em suas páginas da Web.

## Usar HTTP/2 para fornecer seus ativos de Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como os navegadores e servidores se comunicam. Fornece transferência de informações mais rápida e reduz a quantidade de poder de processamento necessário. O Delivery de ativos de Dynamic Media agora pode estar acima de HTTP/2, o que oferece melhor resposta e tempo de carregamento.

Consulte Delivery [HTTP2 de conteúdo](http2faq.md) para obter detalhes completos sobre como começar a usar HTTP/2 com sua conta de Dynamic Media.
