---
title: Gerenciar ativos de vídeo
description: Carregue, pré-visualização, anote e publique ativos de vídeo em [!DNL Adobe Experience Manager].
contentOwner: AG
translation-type: tm+mt
source-git-commit: deab2183447e64e8a98f3072ceab2ef2216c4528
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 6%

---


# Gerenciar ativos de vídeo {#manage-video-assets}

O formato de vídeo é uma parte essencial dos ativos digitais de uma organização. [!DNL Adobe Experience Manager] O oferta amadurece as ofertas e os recursos para gerenciar todo o ciclo de vida de seus ativos de vídeo após sua criação.

Saiba como gerenciar e editar os ativos de vídeo em [!DNL Adobe Experience Manager Assets]. A codificação e transcodificação de vídeo, por exemplo, a transcodificação FFmpeg, é possível usando Perfis de processamento e usando a integração [!DNL Dynamic Media]. Sem a licença [!DNL Dynamic Media], [!DNL Experience Manager] oferece suporte básico para vídeos, como transcodificação usando FFmpeg, extração de miniaturas de pré-visualização para os formatos de arquivo suportados e pré-visualização na interface do usuário para formatos que são suportados para reprodução diretamente no navegador.

## Carregar e pré-visualização ativos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] gera pré-visualizações para ativos de vídeo com a extensão MP4. Você pode pré-visualização as execuções na interface do usuário [!DNL Assets].

1. Na pasta ou subpastas de ativos digitais, navegue até o local onde deseja adicionar ativos digitais.
1. Para fazer upload do ativo, clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Arquivos]**. Como alternativa, arraste um arquivo na interface do usuário. Consulte [fazer upload de ativos](manage-digital-assets.md#uploading-assets) para obter detalhes.
1. Para pré-visualização de um vídeo na visualização da placa, clique na opção **[!UICONTROL Reproduzir]** ![opção de reprodução](assets/do-not-localize/play.png) no ativo de vídeo. Você pode pausar ou reproduzir vídeo apenas na visualização do cartão. As opções [!UICONTROL Reproduzir] e [!UICONTROL Pausar] não estão disponíveis na visualização de lista.
1. Para pré-visualização do vídeo na página de detalhes do ativo, selecione **[!UICONTROL Editar]** no cartão. O vídeo é reproduzido no player de vídeo nativo do navegador. Você pode reproduzir, pausar, controlar o volume e aplicar zoom no vídeo em tela cheia.

## Publicar ativos de vídeo {#publish-video-assets}

Após a publicação, você pode incluir os ativos de vídeo em uma página da Web como um URL ou incorporar diretamente os ativos. Para obter detalhes, consulte [publish [!DNL Dynamic Media] assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Transcodificação usando o Perfil de processamento {#transcode-video}

[!DNL Experience Manager] como um recurso,  [!DNL Cloud Service] permite a transcodificação básica de arquivos de vídeo MP4 usando Perfis de processamento. A funcionalidade permite que você não apenas carregue, mas também pré-visualização e dimensione um arquivo de vídeo MP4.

![Criar Perfil de processamento para transcodificação de vídeo em  [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: Um Perfil de processamento para transcodificação de vídeo no  [!DNL Experience Manager].*

Se você fornecer apenas largura ou somente altura e deixar o outro campo em branco, as renderizações manterão a proporção. O codec de vídeo H.264 está disponível para transcodificação.

Para processar ativos usando um perfil de processamento, adicione um perfil a uma pasta. Consulte [utilizar perfis de processamento para processar ativos](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Anotar ativos de vídeo {#annotate-video-assets}

1. No console [!DNL Assets], selecione **[!UICONTROL Editar]** no cartão de ativos para exibir a página de detalhes do ativo.
1. Para reproduzir o vídeo, clique em **[!UICONTROL Pré-visualização]**.
1. Para anotar o vídeo, clique em **[!UICONTROL Anotar]**. Uma anotação é adicionada no horário específico (quadro) do vídeo. Ao anotar, você pode desenhar na tela e incluir um comentário com o desenho. Os comentários são salvos automaticamente. Para sair do assistente de anotações, clique em **[!UICONTROL Fechar]**.
1. Procure um ponto específico no vídeo, especifique o tempo em segundos no campo de **texto** e clique em **Pular**. Por exemplo, para pular os primeiros 20 segundos de vídeo, digite 20 no campo de texto.
1. Para visualização na linha do tempo, clique em uma anotação. Para excluir a anotação da linha do tempo, clique em **[!UICONTROL Excluir]**.

## Práticas recomendadas e limitações {#tips-limitations}

* Sem a licença [!DNL Dynamic Media], você só pode processar arquivos MP4 usando perfis de processamento.
* Ao transcodificar arquivos MP4 usando Perfis de processamento, as seguintes diretrizes e limitações se aplicam:

   * Os arquivos do Apple ProRes só podem transcodificar para uma resolução máxima de 1080p.
   * Se o arquivo de origem tiver uma taxa de bits >200 Mbps, você só poderá transcodificar para uma resolução máxima de 1080p.
   * Se a taxa de quadros de origem >=60 fps, o tamanho máximo do arquivo de origem que você pode usar é,

      * 400 MB para transcodificação de 4k.
      * 800 MB para transcodificação de 1080p.
      * 8 GB para transcodificação de 720p.
   * O tamanho máximo de arquivo que você pode transcodificar para resolução 4k é um arquivo MP4 de 2,55 GB com resolução de 4k, taxa de bits de 12 Mbps e 23 fps.


>[!MORELIKETHIS]
>
>* [Documentação](/help/assets/dynamic-media/video.md) de vídeo do Dynamic Media.
>* [Saiba mais sobre o uso, os tipos e a configuração de perfis](/help/assets/asset-microservices-configure-and-use.md) de processamento.

