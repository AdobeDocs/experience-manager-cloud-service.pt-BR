---
title: Incorporação do visualizador de vídeo ou imagem do Dynamic Media em uma página da Web
description: Saiba como incorporar ativos de vídeo ou imagem do Dynamic Media em uma página da Web.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 76335781-e39f-4aae-967f-5af8634d8f61
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 21%

---

# Incorpore o Vídeo do Dynamic Media, o Visualizador de imagens ou o Visualizador dimensional em uma página da Web {#embedding-the-video-or-image-viewer-on-a-web-page}

Use o recurso **[!UICONTROL Incorporar código]** quando quiser reproduzir o vídeo ou exibir um ativo incorporado em uma página da Web. Copie o código incorporado na área de transferência para poder colá-lo nuas páginas da Web. A edição do código não é permitida na caixa de diálogo **[!UICONTROL Incorporar código]**.

Você incorpora URLs somente se estiver _não_ usando o Adobe Experience Manager como o WCM. Se estiver usando o Experience Manager como o WCM, [você adiciona os ativos diretamente na página](adding-dynamic-media-assets-to-pages.md).

Consulte [Vincular URLs ao aplicativo web](linking-urls-to-yourwebapplication.md).

Consulte [Entregar imagens otimizadas para um site responsivo](responsive-site.md).

>[!NOTE]
>
>O código incorporado não está disponível para cópia até que você tenha publicado o ativo selecionado. Além disso, você também deve publicar a predefinição do visualizador ou a predefinição da imagem.
>
>Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).
>
>Consulte [Publicar predefinições do visualizador](managing-viewer-presets.md#publishing-viewer-presets).
>
>Consulte [Publicar predefinições da imagem](managing-image-presets.md#publishing-image-presets).

**Para incorporar o visualizador de vídeo ou imagem do Dynamic Media em uma página da Web:**

1. Navegue até a *publicado* ativo de vídeo ou imagem cujo código incorporado você deseja copiar.

   Lembre-se de que o código incorporado só está disponível para cópia *depois* que você *publicou* os ativos pela primeira vez. Além disso, a predefinição do visualizador ou da imagem também deve ser publicada.

   Consulte [Publicar ativos](publishing-dynamicmedia-assets.md).

   Consulte [Publicar predefinições do visualizador](managing-viewer-presets.md#publishing-viewer-presets).

   Consulte [Publicar predefinições da imagem](managing-image-presets.md#publishing-image-presets).

1. No painel à esquerda, selecione a lista suspensa e **[!UICONTROL Visualizadores]**.
1. No painel à esquerda, selecione um nome de predefinição do visualizador. A predefinição do visualizador é aplicada ao ativo.
1. Selecionar **[!UICONTROL Incorporar]**.
1. No **[!UICONTROL Código de inserção]** , copie o código inteiro para a área de transferência e selecione **[!UICONTROL Fechar]**.
1. Cole o código incorporado nas páginas da Web.

## Usar HTTP/2 para entregar seus ativos do Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 é o novo protocolo da Web atualizado que melhora a maneira como navegadores e servidores se comunicam. Ele possibilita a transferência mais rápida de informações e reduz a quantidade necessária de poder de processamento. A entrega de ativos do Dynamic Media agora pode ser por HTTP/2, o que fornece melhores tempos de resposta e carregamento.

Consulte [Entrega de conteúdo HTTP2](http2faq.md) para obter detalhes completos sobre a introdução ao uso de HTTP/2 com sua conta da Dynamic Media.
