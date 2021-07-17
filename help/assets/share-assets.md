---
title: Distribuir e compartilhar ativos, pastas e coleções
description: Distribua seus ativos digitais usando métodos como compartilhar como um link, baixar e via [!DNL Brand Portal], [!DNL desktop app], and [!DNL Asset Link].
contentOwner: AG
feature: Gerenciamento de ativos, Colaboração, Distribuição de ativos
role: User,Admin
exl-id: 14e897cc-75c2-42bd-8563-1f5dd23642a0
source-git-commit: 568c25d77eb42f7d5fd3c84d71333e083759712d
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 2%

---

# Compartilhar e distribuir ativos gerenciados em [!DNL Experience Manager] {#share-assets-from-aem}

[!DNL Adobe Experience Manager Assets] permite compartilhar ativos, pastas e coleções com membros de sua organização e entidades externas, incluindo parceiros e fornecedores. Use os seguintes métodos para compartilhar ativos de [!DNL Experience Manager Assets] como um [!DNL Cloud Service]:

* [Compartilhar como um link](#sharelink).
* [Baixe ](/help/assets/download-assets-from-aem.md) ativos e compartilhe separadamente.
* Compartilhe usando [[!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html).
* Compartilhe usando [[!DNL Adobe Asset Link]](https://www.adobe.com/br/creativecloud/business/enterprise/adobe-asset-link.html).
* Compartilhe usando [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html).

## Compartilhar ativos como um link {#sharelink}

Para gerar o URL dos ativos que deseja compartilhar com os usuários, use a caixa de diálogo Compartilhamento de links . Os usuários com privilégios de administrador ou com permissões de leitura no local `/var/dam/share` podem visualizar os links compartilhados com eles. O compartilhamento de ativos por meio de um link é uma maneira conveniente de disponibilizar recursos para partes externas sem que elas precisem primeiro fazer logon em [!DNL Assets].

![Caixa de diálogo Compartilhamento de link](assets/link-share-dialog.png)

>[!NOTE]
>
>* Você precisa de permissão Editar ACL na pasta ou no ativo que deseja compartilhar como um link.
>* Antes de compartilhar um link com os usuários, [ative emails de saída](/help/implementing/developing/introduction/development-guidelines.md#sending-email). Caso contrário, ocorrerá um erro.


1. Na interface do usuário [!DNL Assets], selecione o ativo a ser compartilhado como um link.
1. Na barra de ferramentas, clique em **[!UICONTROL Compartilhar link]**. Um link de ativo é criado automaticamente no campo **[!UICONTROL Compartilhar link]**. Copie esse link e compartilhe-o com os usuários. O tempo de expiração padrão do link é de um dia.

   >[!NOTE]
   >
   >Se um ativo compartilhado for movido para um local diferente, seu link para de funcionar. Recrie o link e compartilhe-o com os usuários.

<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to Experience Manager Assets.

>[!NOTE]
>
>* You need Edit ACL permission on the folder or the asset that you want to share as a link.
>* Before you share a link with users, ensure that Day CQ Mail Service is configured. Otherwise, an error occurs.

1. In the Assets user interface, select the asset to share as a link.
1. From the toolbar, click/tap the **[!UICONTROL Share Link]**.

   An asset link is auto-created in the **[!UICONTROL Share Link]** field. Copy this link and share it with the users. The default expiration time for the link is one day.

   Alternatively, proceed to perform steps 3-7 of this procedure to add email recipients, configure the expiration time for the link, and send it from the dialog.

   >[!NOTE]
   >
   >If a shared asset is moved to a different location, its link stops working. Re-create the link and re-share with the users.

1. From the web console, open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against each:

    * local
    * author
    * publish

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single Experience Manager author instance. For publish, provide the URL for the publish instance.

1. In the email address box of the **[!UICONTROL Link Sharing]** dialog, type the email ID of the user you want to share the link with. You can also share the link with multiple users.

   If the user is a member of your organization, select the user's email ID from the suggested email IDs that appear in the list below the typing area. For an external user, type the complete email ID and then select it from the list.

   To enable emails to be sent out to users, configure the SMTP server details in [Day CQ Mail Service](/help/assets/configure-asset-sharing.md#configmailservice).

   >[!NOTE]
   >
   >If you enter an email ID of a user that is not a member of your organization, the words "External User" are prefixed with the email ID of the user.

1. In the **[!UICONTROL Subject]** box, enter a subject for the asset you want to share.
1. In the **[!UICONTROL Message]** box, enter an optional message.
1. In the **[!UICONTROL Expiration]** field, specify an expiration date and time for the link using the date picker. By default, the expiration date is set for a week from the date you share the link.
1. To let users download the original image along with the renditions, select **[!UICONTROL Allow download of original file]**.

   >[!NOTE]
   >
   >By default, users can only download the renditions of the asset that you share as a link.

1. Click **[!UICONTROL Share]**. A message confirms that the link is shared with the users through an email.
1. To view the shared asset, click/tap the link in the email that is sent to the user. The shared asset is displayed in the **[!UICONTROL Adobe Marketing Cloud]** page.

   To toggle to the list view, click/tap the layout icon in the toolbar.

1. To generate a preview of the asset, click/tap the shared asset. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click/tap **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click/tap **[!UICONTROL Parent Folder]** to return to the parent folder.

   >[!NOTE]
   >
   >Experience Manager supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## Baixar e compartilhar ativos {#download-and-share-assets}

Os usuários podem baixar os ativos necessários e compartilhá-los fora de [!DNL Experience Manager]. Para obter mais informações, consulte [como pesquisar ativos](/help/assets/search-assets.md), [como baixar ativos](/help/assets/download-assets-from-aem.md) e [como baixar coleções](manage-collections.md#download-a-collection)

## Compartilhar ativos com profissionais de criação {#share-with-creatives}

Os profissionais de marketing e os usuários de linha de negócios podem compartilhar facilmente os ativos aprovados com seus profissionais de criação usando o

* **Aplicativo** de desktop do Experience Manager: O aplicativo funciona no Windows e no Mac. Consulte [visão geral do aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html). Para saber como qualquer usuário autorizado de desktop pode acessar facilmente os ativos compartilhados, consulte [procurar, pesquisar e visualizar ativos](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Os usuários da área de trabalho podem criar ativos e compartilhá-los com seus equivalentes que são usuários do Experience Manager, por exemplo, ao fazer upload de novas imagens. Consulte [fazer upload de ativos usando o aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem).

* **Adobe Asset Link**: Os profissionais criativos podem pesquisar e usar ativos diretamente de dentro  [!DNL Adobe InDesign],  [!DNL Adobe Illustrator]e  [!DNL Adobe Photoshop].

## Configurar compartilhamento de ativos {#configure-sharing}

As diferentes opções para compartilhar os ativos exigem configuração específica e têm pré-requisitos específicos.

### Configurar compartilhamento de link de ativos {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Para gerar o URL dos ativos que deseja compartilhar com os usuários, use a caixa de diálogo Compartilhamento de links . Os usuários com privilégios de administrador ou com permissões de leitura no local `/var/dam/share` podem visualizar os links compartilhados com eles. O compartilhamento de ativos por meio de um link é uma maneira conveniente de disponibilizar recursos para partes externas sem que elas precisem primeiro fazer logon em [!DNL Assets].

>[!NOTE]
>
>Se você quiser compartilhar links da sua instância de Autor com entidades externas, certifique-se de expor apenas os seguintes URLs para solicitações `GET`. Bloqueie outros URLs para garantir que a instância do Autor seja segura.
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password

1. Click/tap **[!UICONTROL Save]**.
-->

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.
### Configure maximum data size {#maxdatasize}

When you download assets from the link shared using the Link Sharing feature, Experience Manager compresses the asset hierarchy from the repository and then returns the asset in a ZIP file. However, in the absence of limits to the amount of data that can be compressed in a ZIP file, huge amounts of data is subjected to compression, which causes out of memory errors in JVM. To secure the system from a potential denial of service attack due to this situation, you can configure the maximum size of the downloaded files. If uncompressed size of the asset exceeds the configured value, asset download requests are rejected. The default value is 100 MB.

1. Click/Tap the Experience Manager logo and then go to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the web console, locate the **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configuration.
1. Open the configuration in edit mode, and modify the value of the **[!UICONTROL Max Content Size (uncompressed)]** parameter.
1. Save the changes.
-->

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### Ativar ações da área de trabalho para usar com o aplicativo da área de trabalho {#desktop-actions}

Na interface do usuário [!DNL Assets] em um navegador, é possível explorar os locais do ativo ou fazer check-out e abrir o ativo para edição no aplicativo de desktop. Essas opções são chamadas de ações da área de trabalho e, para ativá-las, consulte [ativar ações da área de trabalho em [!DNL Assets] interface da Web](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2).

![Permitir que as ações da área de trabalho sejam usadas como atalho ao trabalhar com o aplicativo da área de trabalho](assets/enable_desktop_actions.png)

### Configurações para usar [!DNL Adobe Asset Link] {#configure-asset-link}

O Adobe Asset Link simplifica a colaboração entre criadores e profissionais de marketing no processo de criação de conteúdo. Ele se conecta [!DNL Adobe Experience Manager Assets] com [!DNL Creative Cloud] aplicativos de desktop [!DNL Adobe InDesign], [!DNL Adobe Photoshop] e [!DNL Adobe Illustrator]. O painel [!DNL Adobe Asset Link] permite que os criadores acessem e modifiquem o conteúdo armazenado em [!DNL Assets] sem deixar os aplicativos criativos com os quais estão mais familiarizados.

Consulte [como configurar [!DNL Assets] para usá-lo com [!DNL Adobe Asset Link]](https://helpx.adobe.com/br/enterprise/using/configure-aem-assets-for-asset-link.html).

## Práticas recomendadas e solução de problemas {#bestpractices}

* As pastas ou coleções de ativos que contêm um espaço em branco no nome podem não ser compartilhadas.
* Se os usuários não conseguirem baixar os ativos compartilhados, verifique com o administrador do Experience Manager quais são os [limites de download](#maxdatasize).
* Para que um usuário visualize um vídeo que é compartilhado usando o compartilhamento de link, o vídeo deve ter uma representação de vídeo estática disponível no local `/jcr:content/renditions` no nó do vídeo no repositório. A visualização não depende da disponibilidade de uma representação [!DNL Dynamic Media].
* Ao baixar um ativo de vídeo por meio do compartilhamento de link, as representações [!DNL Dynamic Media] não são incluídas no arquivo baixado.

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your Experience Manager administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!-- TBD: Add content or link about how to share using Brand Portal when it is available on [!DNL Cloud Service].
-->
