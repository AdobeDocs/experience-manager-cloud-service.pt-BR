---
title: Baixar ativos da Content Hub
description: Saiba como baixar ativos no portal Content Hub
role: User
exl-id: 96d4ffba-4e3e-4496-9da2-6eb36be8331f
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---

# Baixar ativos na Content Hub {#download-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas de metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>documentação para desenvolvedores do AEM Assets</b></a>
        </td>
    </tr>
</table>

<!-- ![Download assets](assets/download-asset.jpg) -->
![Baixar ativos](assets/download-asset-genstudio.jpeg)

>[!AVAILABILITY]
>
>O guia do Content Hub agora está disponível no formato PDF. Baixe o guia inteiro e use o Assistente de IA da Adobe Acrobat para responder às suas consultas.
>
>[!BADGE PDF do Guia do Content Hub]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

O Content Hub permite baixar e compartilhar os ativos. A Interface do usuário do Content Hub exibe somente ativos aprovados. Esses ativos podem incluir imagens, vídeos ou qualquer outro conteúdo digital. O Content Hub melhora a acessibilidade e a adaptabilidade para uma distribuição eficiente de ativos.

É possível baixar um ou vários ativos e suas representações disponíveis usando o Content Hub.

Consulte [tipos de representações disponíveis no Content Hub](#types-of-renditions).

## Baixar um ativo e suas representações {#download-asset-renditions}

Para baixar um ativo e suas representações, execute as seguintes etapas:

1. Clique no ativo para exibir suas propriedades.

1. Clique em ![baixar](/help/assets/assets/download-icon.svg) para iniciar o processo de download. O painel Download lista todas as representações de ativos disponíveis.

   >[!NOTE]
   >
   * As representações serão exibidas somente se sua visibilidade for habilitada usando a Interface do Usuário [Configuração](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).
   * É possível baixar todas as [representações de corte estáticas, dinâmicas e inteligentes](#types-of-renditions) ao baixar um ativo.

1. Selecione uma ou mais representações e clique em **[!UICONTROL Baixar]**.

   ![Baixar representações de ativo único](/help/assets/assets/download-single-asset-renditions.png)


Se você estiver baixando um ativo licenciado, selecione **[!UICONTROL Eu li e aceitei os termos e condições mencionados acima]** e clique em **[!UICONTROL Baixar]**. Você também pode clicar em **[!UICONTROL termos e condições]** para exibir a licença do ativo. A visualização da licença é exibida somente se o ativo for aprovado usando o ambiente de criação do Assets as a Cloud Service. Para obter mais informações, consulte [Gerenciar ativos licenciados no Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

>[!NOTE]
>
Os usuários com acesso ao [Dynamic Media com recursos de API aberta](/help/assets/dynamic-media-open-apis-overview.md) podem exibir e baixar representações de corte dinâmico e inteligente.

## Baixar vários ativos e suas representações {#download-multiple-assets-renditions}

Para baixar vários ativos e suas representações, execute as seguintes etapas:

1. Selecione os ativos e clique em ![baixar](/help/assets/assets/download-icon.svg) **[!UICONTROL Baixar]**. A tela [!UICONTROL Baixar ativos] exibe uma lista de todos os ativos selecionados.
1. Clique em **[!UICONTROL Baixar]** para selecionar entre as várias opções de download para iniciar o download:

   * **Baixar [!UICONTROL Originais]**: selecione essa opção para baixar os ativos selecionados no formulário original.
   * **Baixar [!UICONTROL Somente representações estáticas]**: selecione essa opção para baixar todas as representações estáticas disponíveis dos ativos, exceto os ativos originais.
   * **Baixar [!UICONTROL Representações originais e estáticas]**: selecione essa opção para baixar as representações originais e estáticas dos ativos selecionados.

     ![Baixar várias representações](/help/assets/assets/download-multiple-renditions.png)

     >[!NOTE]
     >
     * As representações serão exibidas somente se sua visibilidade for habilitada usando a Interface do Usuário [Configuração](/help/assets/configure-content-hub-ui-options.md#renditions-content-hub).
     * Você só pode baixar [representações estáticas](#types-of-renditions) ao baixar vários ativos.

   Se algum dos ativos selecionados for um ativo licenciado, clique na licença do ativo no painel esquerdo para ver sua visualização, o que permite selecionar **[!UICONTROL Li e aceitei os termos e condições mencionados acima]** e depois clique em **[!UICONTROL Baixar]**. A visualização da licença é exibida somente se o ativo for aprovado usando o ambiente de criação do Assets as a Cloud Service. Para obter mais informações, consulte [Gerenciar ativos licenciados no Content Hub](/help/assets/manage-licensed-assets-on-content-hub.md).

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

As representações de ativos são diferentes representações do arquivo original de um ativo. Isso pode incluir miniaturas, versões otimizadas para a Web ou dispositivos móveis, arquivos com marcas d&#39;água ou protegidos por DRM ou até mesmo elementos dinâmicos, como cortes inteligentes. Eles não precisam corresponder ao tipo de arquivo original. Em vez disso, servem para representar o ativo em vários casos de uso.

Saiba mais sobre [exibir e gerenciar representações no Experience Manager Assets](/help/assets/renditions.md).

[!DNL Experience Manager Assets] dá suporte aos seguintes tipos de representações:

* [Representações estáticas](/help/assets/renditions.md#static-renditions): representações estáticas são versões pré-criadas de ativos digitais, normalmente geradas durante a assimilação ou modificação do ativo. Eles são otimizados para usos e plataformas específicas, como miniaturas da Web, formatos amigáveis para dispositivos móveis para designs responsivos ou arquivos de alta resolução para impressão, proporcionando uma experiência simplificada e consistente.

* [Representações dinâmicas](/help/assets/renditions.md#dynamic-renditions): as representações dinâmicas são versões personalizadas em tempo real de ativos para executar várias ações, como redimensionar imagens para diferentes resoluções de dispositivo ou recortar para ajustar várias taxas de proporção. Essas representações permitem oferecer experiências personalizadas e otimizadas para requisitos mais amplos. Representações dinâmicas de ativos são criadas no ambiente de autor [!DNL Adobe Experience Manager Assets].

* [Corte inteligente](/help/assets/dynamic-media/image-profiles.md#creating-image-profiles): o corte inteligente se concentra exclusivamente na parte essencial de um ativo durante o processo de corte. O Corte inteligente do Dynamic Media para aproveita a inteligência artificial fornecida pelo Adobe Sensei para rastrear o ponto de interesse, garantindo que nossos ativos tenham a melhor aparência em todos os tamanhos de tela. O recorte inteligente [!DNL Adobe Experience Manager] exibe a largura e a altura das representações de um ativo junto com o título. Veja mais em [usando o Recorte inteligente com o AEM Assets Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use).

  ![Tipos de representações](/help/assets/assets/renditions-types.png)


>[!NOTE]
> 
* O recurso de representações de corte dinâmico e inteligente está na fase inicial de Adoção. Para obter acesso ao recurso, [crie e envie um caso de Suporte ao Cliente da Adobe](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).
* Os clientes recém-integrados nos [serviços de API aberta do Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) devem revisar suas predefinições de imagens existentes para aprovação.



