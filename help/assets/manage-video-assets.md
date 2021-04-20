---
title: Gerenciar ativos de vídeo
description: Carregue, visualize, anote e publique ativos de vídeo em [!DNL Adobe Experience Manager].
contentOwner: AG
feature: Asset Management,Publishing,Collaboration,Video
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 6%

---


# Gerenciar ativos de vídeo {#manage-video-assets}

O formato de vídeo é uma parte essencial dos ativos digitais de uma organização. [!DNL Adobe Experience Manager] O oferece ofertas e recursos maduros para gerenciar todo o ciclo de vida dos ativos de vídeo após sua criação.

Saiba como gerenciar e editar os ativos de vídeo em [!DNL Adobe Experience Manager Assets]. A codificação e a transcodificação de vídeo, por exemplo, a transcodificação FFmpeg, é possível usando Perfis de processamento e usando a integração [!DNL Dynamic Media]. Sem a licença [!DNL Dynamic Media], [!DNL Experience Manager] fornece suporte básico para vídeos, como transcodificação usando FFmpeg, extração de miniaturas de visualização para os formatos de arquivo compatíveis e pré-visualização na interface do usuário para formatos que são compatíveis com reprodução diretamente no navegador.

## Fazer upload e visualizar ativos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] gera visualizações para ativos de vídeo com a extensão MP4. Você pode visualizar as representações na interface do usuário [!DNL Assets].

1. Na pasta ou nas subpastas de ativos digitais, navegue até o local onde deseja adicionar ativos digitais.
1. Para fazer upload do ativo, clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Arquivos]**. Como alternativa, arraste um arquivo na interface do usuário do . Consulte [fazer upload de ativos](manage-digital-assets.md#uploading-assets) para obter detalhes.
1. Para visualizar um vídeo na exibição de cartão, clique na opção **[!UICONTROL Play]** ![play option](assets/do-not-localize/play.png) no ativo de vídeo. Você pode pausar ou reproduzir vídeo somente na exibição de cartão. As opções [!UICONTROL Play] e [!UICONTROL Pause] não estão disponíveis na exibição de lista.
1. Para visualizar o vídeo na página de detalhes do ativo, selecione **[!UICONTROL Editar]** no cartão. O vídeo é reproduzido no player de vídeo nativo do navegador. Você pode reproduzir, pausar, controlar o volume e aplicar zoom ao vídeo em tela cheia.

## Publicar ativos de vídeo {#publish-video-assets}

Após a publicação, é possível incluir os ativos de vídeo em uma página da Web como um URL ou incorporar diretamente os ativos. Para obter detalhes, consulte [publicar [!DNL Dynamic Media] ativos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Transcodificar usando o Perfil de processamento {#transcode-video}

[!DNL Experience Manager] O as a  [!DNL Cloud Service] permite fazer a transcodificação básica de arquivos de vídeo MP4 usando Perfis de processamento. A funcionalidade permite que você não apenas faça upload, mas também visualize e dimensione um arquivo de vídeo MP4.

![Criar perfil de processamento para transcodificação de vídeo em  [!DNL Experience Manager]](assets/video-processing-profile-for-mp4.png)

*Figura: Um perfil de processamento para transcodificação de vídeo no  [!DNL Experience Manager].*

Se você fornecer somente largura ou apenas altura e deixar o outro campo em branco, as representações manterão a proporção. O codec de vídeo H.264 está disponível para transcodificação.

Para processar ativos usando um perfil de processamento, adicione um perfil a uma pasta. Consulte [usar perfis de processamento para processar ativos](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

## Anotar ativos de vídeo {#annotate-video-assets}

1. No console [!DNL Assets], selecione **[!UICONTROL Editar]** no cartão de ativos para exibir a página de detalhes do ativo.
1. Para reproduzir o vídeo, clique em **[!UICONTROL Preview]**.
1. Para anotar o vídeo, clique em **[!UICONTROL Anotar]**. Uma anotação é adicionada no horário específico (quadro) do vídeo. Ao fazer anotações, você pode desenhar na tela e incluir um comentário com o desenho. Os comentários são salvos automaticamente. Para sair do assistente de anotação, clique em **[!UICONTROL Fechar]**.
1. Procure um ponto específico no vídeo, especifique o tempo em segundos no campo de **texto** e clique em **Pular**. Por exemplo, para pular os primeiros 20 segundos de vídeo, digite 20 no campo de texto.
1. Para exibi-la na linha do tempo, clique em uma anotação. Para excluir a anotação da linha do tempo, clique em **[!UICONTROL Excluir]**.

## Práticas recomendadas e limitações {#tips-limitations}

* Sem a licença [!DNL Dynamic Media], você só pode processar arquivos MP4 usando perfis de processamento.
* Ao transcodificar arquivos MP4 usando Perfis de processamento, as seguintes diretrizes e limitações se aplicam:

   * Os arquivos da Apple ProRes só podem transcodificar para uma resolução máxima de 1080p.
   * Se o arquivo de origem tiver uma taxa de bits > 200 Mbps, você só poderá transcodificar para uma resolução máxima de 1080p.
   * Se o fragmento de origem >=60 fps, o tamanho máximo do arquivo de origem que você pode usar é,

      * 400 MB para transcodificação 4k.
      * 800 MB para transcodificação de 1080p.
      * 8 GB para transcodificação de 720p.
   * O tamanho máximo de arquivo que você pode transcodificar para a resolução de 4 k é um arquivo MP4 de 2,55 GB com resolução de 4 k, taxa de bits de 12 Mbps e 23 fps.


>[!MORELIKETHIS]
>
>* [Documentação de vídeo do Dynamic Media](/help/assets/dynamic-media/video.md).
>* [Saiba mais sobre o uso, os tipos e a configuração de perfis](/help/assets/asset-microservices-configure-and-use.md) de processamento.

