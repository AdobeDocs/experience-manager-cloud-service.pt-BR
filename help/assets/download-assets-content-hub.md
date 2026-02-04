---
title: Baixar ativos da Content Hub
description: Saiba como baixar um ou mais ativos e suas representações no portal do Content Hub.
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 655f84593adb1199bcfc21cb54071feb3c8523c5
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Baixar ativos da Content Hub {#download-assets}

O [!DNL Content Hub] permite que você baixe e compartilhe seus ativos. A Interface do Usuário do [!DNL Content Hub] exibe somente ativos aprovados. Esses ativos podem incluir imagens, vídeos ou qualquer outro conteúdo digital. O [!DNL Content Hub] aprimora a acessibilidade e a adaptabilidade para uma distribuição eficaz de ativos.

>[!VIDEO](https://video.tv.adobe.com/v/3433135/?learn=on){transcript=true}

Você pode baixar um ou vários ativos e suas representações disponíveis usando o [!DNL Content Hub].

Consulte os [tipos de representações disponíveis no Content Hub](#types-of-renditions).

## Baixar um ou mais ativos e suas representações {#download-asset-renditions}

Para baixar um ou mais ativos e suas representações, execute as seguintes etapas:

* Para baixar um único ativo e suas representações:
   1. Selecione ![baixar](/help/assets/assets/download-icon.svg), disponível no cartão de ativos, para visualizar o ativo e suas representações disponíveis.
   1. Selecione as representações disponíveis e clique na opção **[!UICONTROL Baixar]** na caixa de diálogo para baixar as representações selecionadas como um arquivo ZIP. Se a caixa de diálogo exibir uma licença de ativo (para ativo licenciado), aceite os termos e condições de licenciamento e clique em **[!UICONTROL Baixar]**.
      ![baixar um ativo](/help/assets/assets/download-an-asset-CH-from-asset-card.png)
Como alternativa, clique na miniatura do ativo e em ![baixar](/help/assets/assets/download-icon.svg) para selecionar e exibir as representações disponíveis na caixa de diálogo antes de baixá-las.

* Para baixar vários ativos e suas representações:
   1. Selecione os ativos, clique em ![baixar](/help/assets/assets/download-icon.svg) **[!UICONTROL Baixar]** e veja a lista de ativos selecionados na caixa de diálogo **[!UICONTROL Baixar ativos]**. Clique em ![desmarcar](/help/assets/assets/Close.svg) ao lado de um ativo para desmarcá-lo da lista.
   1. Selecione uma ou mais representações para baixá-las como um arquivo ZIP. Selecionar **[!UICONTROL Corte inteligente]** e **[!UICONTROL Representações estáticas]** baixa todas as representações estáticas e de corte inteligente disponíveis de cada ativo selecionado.
   1. Opcional: desmarque **[!UICONTROL Criar uma pasta separada para cada ativo]** para baixar os ativos selecionados e suas representações como uma hierarquia simples em uma pasta no arquivo zip. Por padrão, o [!DNL Content Hub] baixa os ativos selecionados e suas representações em pastas separadas dentro de um arquivo zip.

      >[!NOTE]
      >
      > * O Content Hub salva sua seleção (**[!UICONTROL Criar uma pasta separada para cada ativo]**) como sua preferência e a retém para downloads futuros.
      > * A opção **[!UICONTROL Criar uma pasta separada para cada ativo]** está disponível somente para usuários [!DNL Content Hub] autenticados. [!DNL Content Hub] permite que usuários públicos baixem ativos como ativos individuais.

   1. Clique em **[!UICONTROL Baixar]** para baixar os ativos selecionados e suas representações.
      ![baixar vários ativos](/help/assets/assets/bulk-asset-download-content-hub.png)

Você pode continuar usando o [!DNL Content Hub] enquanto o download está em andamento. O Content Hub não interrompe o fluxo de trabalho durante o processo de download.
![baixar vários ativos](/help/assets/assets/download-assets-notification-ch.png)
Se a caixa de diálogo **[!UICONTROL Baixar ativos]** exibir licenças de ativos, selecione cada licença no painel esquerdo (seção [!UICONTROL Documentos T&amp;C]) para visualizar a licença e exibir os ativos selecionados associados à licença no painel do meio da caixa de diálogo. Após examinar cada licença, selecione as execuções, clique em **[!UICONTROL Li e aceitei os termos e condições mencionados acima]** e selecione **[!UICONTROL Baixar]** para baixá-las.
![baixar vários ativos](/help/assets/assets/download-multiple-licensed-assets-CH.png)

>[!NOTE]
>
>* As representações serão exibidas somente se sua visibilidade for habilitada usando a Interface do Usuário [[!UICONTROL Configuração]](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).
>* Os usuários com acesso ao [[!DNL Dynamic Media with Open API capabilities]](/help/assets/dynamic-media-open-apis-overview.md) podem exibir e baixar representações de corte dinâmico e inteligente.
>* A visualização da licença é exibida somente se o ativo for aprovado usando o ambiente de criação do [!DNL Assets as a Cloud Service]. Para obter mais informações, consulte [Gerenciar ativos licenciados no Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

<!--

## Download an asset and its renditions {#download-asset-renditions} 

To download an asset and its renditions, execute the following steps: 

1. Click the asset to view its properties.

1. Click ![download](/help/assets/assets/download-icon.svg) to see the list of available asset renditions in the **[!UICONTROL Download]** panel.

   >[!NOTE]
   >
   >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
   >* You can download all [static, dynamic, and smart crop renditions](#types-of-renditions) while downloading an asset.

1. Select one or more renditions and click **[!UICONTROL Download]** to download the selected renditions as a zip file. 
While downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** before clicking **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

   ![Download single asset renditions](/help/assets/assets/download-single-asset-renditions.png)


If you are downloading a licensed asset, select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. You can also click **[!UICONTROL terms & conditions]** to view the asset license. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
> The users with access to [Dynamic Media with Open API capabilities](/help/assets/dynamic-media-open-apis-overview.md) can view and download dynamic and smart crop renditions.

## Download multiple assets and their renditions {#download-multiple-assets-renditions} 

To download multiple assets and their renditions, execute the following steps: 

1. Select the assets and click ![download](/help/assets/assets/download-icon.svg) **[!UICONTROL Download]**. The [!UICONTROL Download assets] screen displays listing all the selected assets. 
1. Click **[!UICONTROL Download]** to select from the various download options to begin download:

    * **Download [!UICONTROL Originals]**: Select this option to download the selected assets in the original form.
    * **Download [!UICONTROL Static Renditions only]**: Select this option to download all available static renditions of assets except the original assets.
    * **Download [!UICONTROL Originals & Static Renditions]**: Select this option to download both original and static renditions of the selected assets. 

      ![Download multiple renditions](/help/assets/assets/download-multiple-renditions.png)

      >[!NOTE]
      >
      >* The renditions display only if their visibility is enabled using the [Configuration](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub) User Interface.
      >* You can only download [static renditions](#types-of-renditions) while downloading multiple assets.

    If any of the selected asset is a licensed asset, click the license of the asset in left pane to see its preview, which enables you to select **[!UICONTROL I have read and accepted the terms & conditions mentioned above]** and then click **[!UICONTROL Download]**. The preview of the license displays only if the asset is approved using Assets as a Cloud Service authoring environment. For more information, see [Manage licensed assets on Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

    <!--![download-multiple-license](/help/assets/assets/download-multiple-license.png)-->

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

## Tipos de representações {#types-of-renditions}

As representações de ativos são diferentes representações do arquivo original de um ativo. Essas representações podem incluir miniaturas, versões otimizadas para Web ou dispositivos móveis, arquivos protegidos por marcas d&#39;água ou DRM ou até mesmo elementos dinâmicos, como cortes inteligentes. Eles não precisam corresponder ao tipo de arquivo original. Em vez disso, servem para representar o ativo em vários casos de uso.

Saiba mais sobre [exibir e gerenciar representações em [!DNL Experience Manager Assets]](/help/assets/renditions.md).

[!DNL Experience Manager Assets] dá suporte aos seguintes tipos de representações:

* [Representações estáticas](/help/assets/renditions.md#static-renditions): representações estáticas são versões pré-criadas de ativos digitais, normalmente geradas durante a assimilação ou modificação do ativo. Eles são otimizados para usos e plataformas específicas, como miniaturas da Web, formatos amigáveis para dispositivos móveis para designs responsivos ou arquivos de alta resolução para impressão, proporcionando uma experiência simplificada e consistente.

* [Representações dinâmicas](/help/assets/renditions.md#dynamic-renditions): as representações dinâmicas são versões personalizadas em tempo real de ativos para executar várias ações, como redimensionar imagens para diferentes resoluções de dispositivo ou recortar para ajustar várias taxas de proporção. Essas representações permitem oferecer experiências personalizadas e otimizadas para requisitos mais amplos. Representações dinâmicas de ativos são criadas no ambiente de autor [!DNL Adobe Experience Manager Assets]. Para obter informações sobre as etapas necessárias para habilitar representações dinâmicas, consulte [Habilitar representações dinâmicas](#enable-dynamic-media-renditions).

* [Corte inteligente](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles): o corte inteligente se concentra exclusivamente na parte essencial de um ativo durante o processo de corte. O Corte inteligente do Dynamic Media aproveita a inteligência artificial fornecida pelo Adobe AI para rastrear o ponto de interesse, garantindo que nossos ativos tenham melhor aparência em todos os tamanhos de tela. O recorte inteligente [!DNL Adobe Experience Manager] exibe a largura e a altura das representações de um ativo junto com o título. Veja mais em [usando o Recorte inteligente com o AEM Assets Dynamic Media](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

  As representações de Recorte inteligente são exibidas e estão disponíveis para download somente se você tiver acesso ao [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md). As representações de Recorte inteligente estão disponíveis somente para ativos de imagem.

  ![Tipos de representações](/help/assets/assets/renditions-types.png)

  >[!NOTE]
  > 
  > O painel Download exibe somente representações estáticas personalizadas. As miniaturas `cq5dam.*` padrão não são exibidas no Content Hub.

### Ativar representações dinâmicas {#enable-dynamic-media-renditions}

Para ativar representações dinâmicas:

1. Verifique se você tem acesso ao [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md).

   Depois de ter acesso ao Dynamic Media com recursos OpenAPI, todos os ativos marcados como `Approved` estarão disponíveis para entrega pública usando o Dynamic Media.

1. Defina o [destino de aprovação do ativo](/help/assets/approve-assets-content-hub.md#set-approval-target) como Content Hub para aprovar ativos somente para o Content Hub.

1. Habilite a opção de alternância **[!UICONTROL Habilitar disponibilidade de representações]**, disponível na guia **[!UICONTROL Representações]** da Interface do Usuário [Configuração](/help/assets/configure-content-hub-ui-options.md#access-configuration-options-content-hub).

1. Salve novamente as predefinições de imagem existentes para disponibilizá-las no Content Hub. Ela é aplicável somente se você tiver integrado recentemente ao Dynamic Media com OpenAPI.

   Para salvar novamente as predefinições de imagens existentes, navegue até Admin View e selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições de Imagens]**. Selecione uma predefinição, clique em **[!UICONTROL Editar]** e em **[!UICONTROL Salvar]**.



   >[!NOTE]
   > 
   > As representações dinâmicas estão disponíveis somente para ativos de imagem.



