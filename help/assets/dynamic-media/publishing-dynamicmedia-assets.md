---
title: Publicar ativos do Dynamic Media
description: Saiba como publicar ativos do Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
source-git-commit: a11529886d4b158c19a97ccbcb7d004cf814178d
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---

# Publicar ativos do Dynamic Media {#publishing-dynamic-media-assets}

Publique seus ativos do Dynamic Media selecionando os ativos que você já carregou e selecionando **[!UICONTROL Publish]** ou **[!UICONTROL Publicação rápida]**. Depois que os ativos do Dynamic Media forem publicados, eles estarão disponíveis para inclusão em uma página da Web por meio de um URL ou por meio da incorporação de código na página.

Você também pode publicar instantaneamente os ativos que carregou, sem nenhuma intervenção do usuário. Ou você pode publicar seletivamente esses ativos. Consulte [Configurar Dynamic Media](config-dm.md). Ou você pode publicar seletivamente ativos no Dynamic Media ou no Adobe Experience Manager, mutuamente exclusivos entre si, usando **[!UICONTROL Publicação seletiva]** no nível da pasta. Consulte [Trabalhar com publicação seletiva no Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

No **[!UICONTROL Exibição de cartão]**, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda da data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

>[!NOTE]
>
>Se um ativo já tiver sido publicado, você o move para outra pasta e republica do novo local, o local do ativo original publicado ainda estará disponível, junto com o ativo recém-republicado. No entanto, o ativo original publicado é &quot;perdido&quot; para o Experience Manager e não pode ter a publicação desfeita. Portanto, como prática recomendada, cancele a publicação de ativos antes de movê-los para uma pasta diferente.

Se você pretende publicar ativos de vídeo imediatamente após codificá-los, certifique-se de que a codificação foi feita. Quando os vídeos estão sendo codificados, o sistema informa que um fluxo de trabalho de processamento de vídeo está em andamento. Quando a codificação do vídeo for concluída, você poderá pré-visualizar as representações do vídeo. Nesse ponto, é seguro publicar os vídeos sem incorrer em erros de publicação.

Consulte também [Vincular URLs ao aplicativo da Web](linking-urls-to-yourwebapplication.md).

Consulte também [Incorporação do visualizador de vídeo do Dynamic Media ou do visualizador de imagens em uma página da Web](embed-code.md).

>[!NOTE]
>
>* Os ativos devem ser publicados para usar o URL. Se os ativos não forem publicados, copiar e colar o URL em um navegador não funcionará.
>* As predefinições de imagem e do visualizador devem ser ativadas e publicadas para entrega em tempo real.
>


Para obter informações detalhadas sobre a publicação de um conjunto ou ativo, consulte [Publicar ativos](/help/assets/manage-digital-assets.md).

## Entrega HTTP/2 de ativos do Dynamic Media {#http-delivery-of-dynamic-media-assets}

O Experience Manager agora é compatível com a entrega de todo o conteúdo do Dynamic Media (imagens e vídeo) via HTTP/2. Ou seja, um URL publicado ou código incorporado para a imagem ou vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é entregue por meio do protocolo HTTP/2. Esse método de entrega melhora a maneira como os navegadores e servidores se comunicam, permitindo melhores tempos de resposta e carregamento de todos os ativos do Dynamic Media.

Consulte [Perguntas frequentes sobre entrega de conteúdo HTTP/2](/help/assets/dynamic-media/http2faq.md).

<!--this md file used to reside under sites-administering-->
