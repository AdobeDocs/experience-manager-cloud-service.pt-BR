---
title: Baixar ativos da Content Hub
description: Saiba como baixar ativos no portal Content Hub
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 28424cb184d0378669498c78e571961227f6539a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Baixar ativos na Content Hub {#download-assets}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

<!-- ![Download assets](assets/download-asset.jpg) -->
![Baixar ativos](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>O guia do Content Hub agora está disponível no formato PDF. Baixe o guia inteiro e use o Assistente de IA da Adobe Acrobat para responder às suas consultas.
>
>[!BADGE PDF do Guia do Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

O Content Hub permite baixar e compartilhar os ativos. A Interface do usuário do Content Hub exibe somente ativos aprovados. Esses ativos podem incluir imagens, vídeos ou qualquer outro conteúdo digital. O Content Hub melhora a acessibilidade e a adaptabilidade para uma distribuição eficiente de ativos.

É possível baixar um ou vários ativos e suas representações disponíveis usando o Content Hub.

## Baixar um ativo e suas representações {#download-asset-renditions}

Para baixar um ativo e suas representações, execute as seguintes etapas:

1. Clique no ativo para exibir suas propriedades.

1. Clique em ![baixar](/help/assets/assets/download-icon.svg) para iniciar o processo de download. O painel Download lista todas as representações de ativos disponíveis (Original + outras representações).

   >[!NOTE]
   >
   As representações serão exibidas somente se sua visibilidade for habilitada usando a Interface do Usuário [Configuração](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).

1. Selecione as representações e clique em **[!UICONTROL Baixar]**.

   ![Baixar representações de ativo único](/help/assets/assets/download-single-asset-renditions.png)


Se você estiver baixando um ativo licenciado, selecione **[!UICONTROL Eu li e aceitei os termos e condições mencionados acima]** e clique em **[!UICONTROL Baixar]**. Você também pode clicar em **[!UICONTROL termos e condições]** para exibir a licença do ativo. A visualização da licença é exibida somente se o ativo for aprovado usando o ambiente de criação do Assets as a Cloud Service. Para obter mais informações, consulte [Gerenciar ativos licenciados no Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

## Baixar vários ativos e suas representações {#download-multiple-assets-renditions}

Para baixar vários ativos e suas representações, execute as seguintes etapas:

1. Selecione os ativos e clique em ![baixar](/help/assets/assets/download-icon.svg) **[!UICONTROL Baixar]**. A tela [!UICONTROL Baixar ativos] exibe uma lista de todos os ativos selecionados.
1. Clique em **[!UICONTROL Baixar]** para selecionar entre as várias opções de download para iniciar o download:

   * **Baixar [!UICONTROL Originais]**: selecione essa opção para baixar os ativos selecionados no formulário original.
   * **Baixar [!UICONTROL Somente representações]**: selecione essa opção para baixar todas as representações disponíveis dos ativos, exceto os originais.
   * **Baixar [!UICONTROL Originais e todas as representações]**: selecione essa opção para baixar as representações originais e dos ativos selecionados.

     ![Baixar várias representações](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     As representações serão exibidas somente se sua visibilidade for habilitada usando a Interface do Usuário [Configuração](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).

   Se algum dos ativos selecionados for um ativo licenciado, clique na licença do ativo no painel esquerdo para ver sua visualização, o que permite selecionar **[!UICONTROL Li e aceitei os termos e condições mencionados acima]** e depois clique em **[!UICONTROL Baixar]**. A visualização da licença é exibida somente se o ativo for aprovado usando o ambiente de criação do Assets as a Cloud Service. Para obter mais informações, consulte [Gerenciar ativos licenciados no Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

   ![baixar-várias-licenças](/help/assets/assets/download-multiple-license.png)

<!--1. On the Content Hub homepage, select the asset and click **Download**. The **Download assets** dialog box displays a license or list of licenses associated with the selected assets in the left pane. 
1. Click a license in the left pane to see its PDF in the middle pane and the associated assets with it in the right pane. The license PDF preview is displayed only if the license is approved in your Assets as a Cloud Service environment. [Approve the license PDFs](/help/assets/approve-assets-content-hub.md) of the selected assets to see their previews.
1. Optional: Click ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the dialog box.
1. Select **I have read and accept all the terms and conditions mentioned above.** 
1. Click **Download** to download the selected assets.-->

<!---This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the preview of the associated assets to the license in the right. Reviewed licenses are highlighted in light blue.


The dialog box that displays depends on whether the download list includes expired assets or only non-expired assets. <br/>
**Download expired assets dialog box:** This dialog box displays the expired assets' preview along with their expiry date in the left pane. The expired assets' count out of total selected displays in the right pane. Click **Proceed with all assets** to download expired assets with other assets (if present). The Download assets dialog box displays. See the [Download assets dialog box](#Download-asset-dialog-box) to proceed further.
    
    >[!NOTE]
    >
    >[Enable the download option for expired assets](/help/assets/configure-content-hub-ui-options.md#expired-assets-content-hub) to download them. Only expired assets that have enabled downloading are available for download.

   <a id="Download-asset-dialog-box"></a> **Download assets dialog box:** This dialog box displays the list of licenses associated with the selected assets in the left pane. Select a license to preview its terms and conditions (in pdf format) in the middle pane and the associated assets' preview and their count in the right pane. Reviewed licenses are highlighted in light blue.

    >[!NOTE]
    >
    > The **Download Asset dialog box** previews licensing terms and conditions only for approved licenses. [Approve the assets' licenses](/help/assets/approve-assets-content-hub.md) before downloading them to preview their licensing terms in the **Download Asset dialog box**.

1. Click  ![remove-icon](/help/assets/assets/remove-icon.svg) to remove a license from the download dialog box. 

1. Accept the terms and conditions and then click **Download** to download assets associated with the available licenses in the left pane.-->
<!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

<!---
### Download non-licensed Assets {#download-non-licensed-assets}

 To download non-licensed assets, select the assets and click ![download](/help/assets/assets/download-icon.svg) from the top rail.-->







