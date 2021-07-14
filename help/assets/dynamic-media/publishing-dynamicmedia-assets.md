---
title: Publicar ativos do Dynamic Media
description: Saiba como publicar ativos do Dynamic Media.
contentOwner: Rick Brough
feature: Gerenciamento de ativos
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: a11529886d4b158c19a97ccbcb7d004cf814178d
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---

# Publicar ativos do Dynamic Media {#publishing-dynamic-media-assets}

Publique seus ativos do Dynamic Media selecionando os ativos que já carregou e selecionando **[!UICONTROL Publicar]** ou **[!UICONTROL Publicação rápida]**. Depois que os ativos da Dynamic Media forem publicados, eles estarão disponíveis para inclusão em uma página da Web por meio de um URL ou como meio de incorporar o código na página.

Você também pode publicar instantaneamente os ativos que você faz upload, sem nenhuma intervenção do usuário. Ou você pode publicar seletivamente esses ativos. Consulte [Configurar Dynamic Media](config-dm.md). Ou, você pode publicar ativos seletivamente no Dynamic Media ou no Adobe Experience Manager, mutuamente exclusivos entre si, usando **[!UICONTROL Publicação seletiva]** no nível da pasta. Consulte [Trabalhar com publicação seletiva no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

Na **[!UICONTROL Exibição de cartão]**, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda da data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

>[!NOTE]
>
>Se um ativo já tiver sido publicado, mova-o para outra pasta e republique-o de seu novo local, o local do ativo publicado original ainda estará disponível, juntamente com o ativo recém-republicado. O ativo publicado original, no entanto, é &quot;perdido&quot; para o Experience Manager e não pode ter a publicação cancelada. Portanto, como prática recomendada, cancele a publicação de ativos primeiro antes de movê-los para uma pasta diferente.

Se você pretende publicar ativos de vídeo imediatamente após codificá-los, verifique se a codificação foi feita. Quando os vídeos são codificados, o sistema informa que um fluxo de trabalho de processamento de vídeo está em andamento. Quando a codificação de vídeo estiver concluída, você poderá visualizar as representações de vídeo. Nesse momento, é seguro publicar os vídeos sem incorrer em erros de publicação.

Consulte também [Vincular URLs ao seu aplicativo Web](linking-urls-to-yourwebapplication.md).

Consulte também [Incorporar o visualizador de vídeo ou o visualizador de imagem do Dynamic Media em uma página da Web](embed-code.md).

>[!NOTE]
>
>* Os ativos devem ser publicados para usar o URL. Se os ativos não forem publicados, copiar e colar o URL em um navegador da Web não funcionará.
>* As predefinições de imagens e as predefinições do visualizador devem ser ativadas e publicadas para entrega ao vivo.

>



Para obter informações detalhadas sobre a publicação de um conjunto ou ativo, consulte [Publicação de ativos](/help/assets/manage-digital-assets.md).

## Entrega HTTP/2 de ativos do Dynamic Media {#http-delivery-of-dynamic-media-assets}

O Experience Manager agora é compatível com a entrega de todo o conteúdo do Dynamic Media (imagens e vídeo) por HTTP/2. Ou seja, um URL publicado ou código incorporado para a imagem ou vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é então entregue por meio do protocolo HTTP/2. Esse método de entrega melhora a maneira como os navegadores e servidores se comunicam, permitindo uma melhor resposta e tempos de carregamento de todos os seus ativos do Dynamic Media.

Consulte [Entrega HTTP/2 de conteúdo de perguntas frequentes](/help/assets/dynamic-media/http2faq.md).

<!--this md file used to reside under sites-administering-->
