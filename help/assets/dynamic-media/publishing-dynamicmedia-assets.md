---
title: Publicação de ativos de mídia dinâmica
description: Como publicar ativos de mídia dinâmica
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: b65ce0af6281f60272322744f0e6f81b7eb6b96a
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 3%

---


# Publicando ativos de mídia dinâmica {#publishing-dynamic-media-assets}

Você publica seus ativos de Mídia dinâmica selecionando os ativos que já carregou e tocando em **[!UICONTROL Publicar]** ou **[!UICONTROL Publicação rápida]**. Depois que seus ativos de Mídia dinâmica forem publicados, eles estarão disponíveis para você incluir em uma página da Web por meio de um URL ou da incorporação de código na página.

Você também pode publicar instantaneamente ativos que você carrega, sem nenhuma intervenção do usuário. Ou você pode publicar seletivamente esses ativos. Consulte [Configuração do Dynamic Media.](config-dm.md) Ou você pode publicar seletivamente ativos no Dynamic Media ou AEM, mutuamente exclusivos entre si, usando  **[!UICONTROL Publicação seletiva no]** nível de pasta. Consulte [Trabalhando com publicação seletiva no Dynamic Media.](/help/assets/dynamic-media/selective-publishing.md)

Na **[!UICONTROL Visualização de cartão]**, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda da data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

>[!NOTE]
>
>Se um ativo já estiver publicado, você usará AEM para mover o ativo para outra pasta e republicar de seu novo local, o local original do ativo publicado ainda estará disponível, juntamente com o ativo recém-publicado. O ativo publicado original, no entanto, é &quot;perdido&quot; para AEM e não pode ser despublicado. Portanto, como prática recomendada, cancele a publicação de ativos primeiro antes de movê-los para uma pasta diferente.

Se você pretende publicar ativos de vídeo imediatamente após a codificação, certifique-se de que a codificação esteja concluída. Quando os vídeos ainda estão sendo codificados, o sistema permite que você saiba que um fluxo de trabalho de processamento de vídeo está em andamento. Quando a codificação de vídeo estiver concluída, você poderá pré-visualização as execuções de vídeo. Nesse ponto, é seguro publicar os vídeos sem incorrer em erros de publicação.

Consulte também [Vincular URLs à sua Aplicação web.](linking-urls-to-yourwebapplication.md)

Consulte também [Incorporar o visualizador de Vídeo de Mídia Dinâmica ou o Visualizador de Imagem em uma página da Web.](embed-code.md)

>[!NOTE]
>
>* Os ativos devem ser publicados para usar o URL. Se os ativos não forem publicados, copiar e colar o URL em um navegador da Web não funcionará.
>* As predefinições de imagens e as predefinições do visualizador devem ser ativadas e publicadas para o delivery ao vivo.

>



Para obter informações detalhadas sobre como publicar um conjunto ou ativo, consulte [Publicar ativos.](/help/assets/manage-digital-assets.md)

## DELIVERY HTTP/2 de ativos de Dynamic Media {#http-delivery-of-dynamic-media-assets}

AEM agora suporta o delivery de todo o conteúdo de Dynamic Media (imagens e vídeo) por HTTP/2. Ou seja, um URL publicado ou um código incorporado para a imagem ou o vídeo está disponível para ser integrado a qualquer aplicativo que aceite um ativo hospedado. Esse ativo publicado é então entregue por meio do protocolo HTTP/2. Este método de delivery melhora a maneira como os navegadores e servidores se comunicam, permitindo uma melhor resposta e tempos de carregamento de todos os seus ativos de Dynamic Media.

Consulte [delivery HTTP/2 de conteúdo com perguntas frequentes](/help/assets/dynamic-media/http2faq.md) para saber mais.
<!--this md file used to reside under sites-administering-->
