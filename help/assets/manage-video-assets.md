---
title: Gerencie ativos de vídeo no [!DNL Adobe Experience Manager].
description: Faça upload, pré-visualização, anote e publique ativos de vídeo em [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: d6a0848547a6dcbb058576827d3cacbc8045ae79
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 6%

---


# Gerenciar ativos de vídeo {#manage-video-assets}

O formato de vídeo é uma parte essencial dos ativos digitais de uma organização. [!DNL Adobe Experience Manager] O oferta amadurece as ofertas e os recursos para gerenciar todo o ciclo de vida de seus ativos de vídeo após sua criação.

Saiba como gerenciar e editar os ativos de vídeo em [!DNL Adobe Experience Manager Assets]. A codificação e a transcodificação de vídeo, por exemplo, a transcodificação FFmpeg, é possível usando Perfis de processamento e usando a [!DNL Dynamic Media] integração. Sem [!DNL Dynamic Media] licença, [!DNL Experience Manager] fornece suporte básico para vídeos, como transcodificação usando FFmpeg, extração de miniaturas de pré-visualização para os formatos de arquivo suportados e pré-visualização na interface do usuário para formatos que são suportados para reprodução diretamente no navegador.

## Fazer upload e pré-visualização de ativos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] gera pré-visualizações para ativos de vídeo com a extensão MP4. Você pode pré-visualização as execuções na interface do [!DNL Assets] usuário.

1. Na pasta ou subpastas de ativos digitais, navegue até o local onde deseja adicionar ativos digitais.
1. Para carregar o ativo, clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Arquivos]**. Como alternativa, arraste um arquivo na interface do usuário. Consulte [fazer upload de ativos](manage-digital-assets.md#uploading-assets) para obter detalhes.
1. Para pré-visualização de um vídeo na visualização da placa, clique na opção **[!UICONTROL Reproduzir]** ![reprodução](assets/do-not-localize/play.png) no ativo de vídeo. Você pode pausar ou reproduzir vídeo apenas na visualização do cartão. As opções [!UICONTROL Reproduzir] e [!UICONTROL Pausar] não estão disponíveis na visualização da lista.
1. Para pré-visualização do vídeo na página de detalhes do ativo, selecione **[!UICONTROL Editar]** no cartão. O vídeo é reproduzido no player de vídeo nativo do navegador. Você pode reproduzir, pausar, controlar o volume e aplicar zoom no vídeo em tela cheia.

## Publicar ativos de vídeo {#publish-video-assets}

Após a publicação, você pode incluir os ativos de vídeo em uma página da Web como um URL ou incorporar diretamente os ativos. Para obter detalhes, consulte [publicar ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)de Mídia dinâmica.

## Transcodificação usando o Perfil de processamento {#transcode-video}

[!DNL Experience Manager] como um Cloud Service, você pode fazer a transcodificação básica de arquivos de vídeo MP4 usando Perfis de processamento. A funcionalidade permite que você não apenas carregue, mas também pré-visualização e dimensione um arquivo de vídeo MP4.

![Criar Perfil de processamento para transcodificação de vídeo no Experience Manager](assets/video-processing-profile-for-mp4.png)

*Figura: Um Perfil de processamento para transcodificação de vídeo no[!DNL Experience Manager].*

Se você fornecer apenas largura ou somente altura e deixar o outro campo em branco, as renderizações manterão a proporção. Atualmente, apenas o codec h264 está disponível para transcodificação.

Para processar ativos usando um perfil de processamento, adicione um perfil a uma pasta. Consulte [usar perfis de processamento para processar ativos](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Anotar ativos de vídeo {#annotate-video-assets}

1. No [!DNL Assets] console, selecione **[!UICONTROL Editar]** no cartão do ativo para exibir a página de detalhes do ativo.
1. Para reproduzir o vídeo, clique em **[!UICONTROL Pré-visualização]**.
1. Para anotar o vídeo, clique em **[!UICONTROL Anotar]**. Uma anotação é adicionada no horário específico (quadro) do vídeo. Ao anotar, você pode desenhar na tela e incluir um comentário com o desenho. Os comentários são salvos automaticamente. Para sair do assistente de anotações, clique em **[!UICONTROL Fechar]**.
1. Procure um ponto específico no vídeo, especifique o tempo em segundos no campo de **texto** e clique em **Pular**. Por exemplo, para pular os primeiros 20 segundos de vídeo, digite 20 no campo de texto.
1. Para visualização na linha do tempo, clique em uma anotação. Para excluir a anotação da linha do tempo, clique em **[!UICONTROL Excluir]**.

## Práticas recomendadas e limitações {#tips-limitations}

* Sem a licença do Dynamic Media, você só pode processar arquivos MP4 usando perfis de processamento.
* Para transcodificação básica usando

>[!MORELIKETHIS]
>
>* [Documentação](/help/assets/dynamic-media/video.md)de vídeo do Dynamic Media.
>* [Saiba mais sobre o uso, os tipos e a configuração de perfis](/help/assets/asset-microservices-configure-and-use.md)de processamento.

