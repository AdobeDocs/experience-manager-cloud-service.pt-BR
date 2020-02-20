---
title: Publicação de ativos de mídia dinâmica
description: Como publicar ativos de mídia dinâmica
translation-type: tm+mt
source-git-commit: 218afb360ec3a13f2f4562a703ca3184083fa7f6

---


# Publishing Dynamic Media Assets {#publishing-dynamic-media-assets}

Você publica seus ativos de Mídia dinâmica selecionando os ativos e tocando em **[!UICONTROL Publicar]**. Depois que seus ativos de mídia dinâmica forem publicados, eles estarão disponíveis para você para inclusão em uma página da Web via URL ou por meio da incorporação.

Você também pode publicar instantaneamente ativos que você carrega, sem nenhuma intervenção do usuário. See [Configuring Dynamic Media](config-dm.md).

Na exibição **[!UICONTROL de]** cartão, um pequeno ícone de globo aparece logo abaixo do nome de um ativo para indicar que ele foi publicado. Na Exibição **[!UICONTROL de]** lista, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

>[!NOTE]
>
>Se um ativo já tiver sido publicado, você usará o AEM para mover o ativo para outra pasta e republicar de seu novo local, o local original do ativo publicado ainda estará disponível, juntamente com o ativo recém-publicado. O ativo publicado original, no entanto, é &quot;perdido&quot; para o AEM e não pode ser despublicado. Portanto, como prática recomendada, cancele a publicação de ativos primeiro antes de movê-los para uma pasta diferente.

Se você pretende publicar ativos de vídeo imediatamente após a codificação, certifique-se de que a codificação esteja concluída. Quando os vídeos ainda estão sendo codificados, o sistema permite que você saiba que um fluxo de trabalho de processamento de vídeo está em andamento. Quando a codificação de vídeo estiver concluída, você deverá visualizar as execuções de vídeo. Nesse ponto, é seguro publicar os vídeos sem incorrer em erros de publicação.

See also [Linking URLs to your Web Application](linking-urls-to-yourwebapplication.md).

Consulte também [Incorporação do visualizador de vídeo em uma página da Web.](embed-code.md)

>[!NOTE]
>
>* Os ativos devem ser publicados para usar o URL. Se os ativos não forem publicados, copiar e colar o URL em um navegador da Web não funcionará.
>* As predefinições de imagens e as predefinições do visualizador devem ser ativadas e publicadas para entrega ao vivo.
>



Para obter informações detalhadas sobre a publicação de um conjunto ou ativo, consulte [Publicação de ativos.](/help/assets/manage-digital-assets.md)

## Entrega HTTP/2 de ativos do Dynamic Media {#http-delivery-of-dynamic-media-assets}

O AEM agora oferece suporte à entrega de todo o conteúdo de Dynamic Media (imagens e vídeo) por HTTP/2. Ou seja, um URL publicado ou um código incorporado para a imagem ou o vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é então entregue por meio do protocolo HTTP/2. Esse método de entrega melhora a maneira como os navegadores e servidores se comunicam, permitindo uma melhor resposta e tempos de carregamento de todos os ativos do Dynamic Media.

Consulte a entrega de conteúdo [HTTP/2 com perguntas](/help/assets/dynamic-media/http2faq.md) frequentes para saber mais.
<!--this md file used to reside under sites-administering-->
