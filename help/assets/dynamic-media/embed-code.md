---
title: Incorporar o visualizador de vídeo ou imagem do Dynamic Media em uma página da Web
description: Saiba como incorporar vídeos ou ativos de imagem do Dynamic Media em uma página da Web.
feature: Asset Management
role: User
exl-id: 76335781-e39f-4aae-967f-5af8634d8f61
source-git-commit: 6933f053e11320d8201922723879983084c52209
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 21%

---

# Incorporar o vídeo do Dynamic Media, o visualizador de imagens ou o visualizador dimensional em uma página da Web {#embedding-the-video-or-image-viewer-on-a-web-page}

Use o recurso **[!UICONTROL Incorporar código]** quando quiser reproduzir o vídeo ou exibir um ativo incorporado em uma página da Web. Copie o código incorporado na área de transferência para poder colá-lo nuas páginas da Web. A edição do código não é permitida na caixa de diálogo **[!UICONTROL Incorporar código]**.

Você incorporar URLs somente se estiver _not_ usando o Adobe Experience Manager como WCM. Se estiver usando o Experience Manager como o WCM, [você adiciona os ativos diretamente na página](adding-dynamic-media-assets-to-pages.md).

Consulte [Vincular URLs ao seu aplicativo web](linking-urls-to-yourwebapplication.md).

Consulte [Fornecer imagens otimizadas para um site responsivo](responsive-site.md).

>[!NOTE]
>
>O código incorporado não está disponível para cópia até que você tenha publicado o ativo selecionado. Além disso, você também deve publicar a predefinição do visualizador ou a predefinição de imagem.
>
>Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).
>
>Consulte [Publicar predefinições do visualizador](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulte [Publicar predefinições da imagem](managing-image-presets.md#publishing-image-presets).

**Para incorporar o visualizador de vídeo ou imagem do Dynamic Media em uma página da Web:**

1. Navegue até o *publicado* vídeo ou ativo de imagem cujo código incorporado você deseja copiar.

   Lembre-se de que o código incorporado só está disponível para cópia *depois* que você *publicou* os ativos pela primeira vez. Além disso, a predefinição do visualizador ou da imagem também deve ser publicada.

   Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).

   Consulte [Publicar predefinições do visualizador](managing-viewer-presets.md#publishing-viewer-presets).

   Consulte [Publicar predefinições da imagem](managing-image-presets.md#publishing-image-presets).

1. No painel à esquerda, selecione a lista suspensa e selecione **[!UICONTROL Visualizadores]**.
1. No painel à esquerda, selecione um nome de predefinição do visualizador. A predefinição do visualizador é aplicada ao ativo.
1. Selecionar **[!UICONTROL Incorporar]**.
1. No **[!UICONTROL Código incorporado]** , copie o código inteiro para a área de transferência e selecione **[!UICONTROL Fechar]**.
1. Cole o código incorporado nas páginas da Web.

## Usar HTTP/2 para fornecer ativos da Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como os navegadores e servidores se comunicam. Ele oferece transferência mais rápida de informações e reduz a quantidade de poder de processamento necessário. A entrega de ativos do Dynamic Media agora pode ser feita via HTTP/2, o que oferece melhor resposta e tempo de carregamento.

Consulte [Entrega de conteúdo HTTP2](http2faq.md) para obter detalhes completos sobre a introdução ao HTTP/2 com sua conta do Dynamic Media.
