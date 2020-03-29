---
title: Compartilhar ativos, pastas e coleções como um link
description: Este artigo descreve como compartilhar ativos, pastas e coleções nos ativos do Experience Manager como um hiperlink.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 68b2214a4c8941365120bdef670e89b4c9058966

---


# Compartilhar e distribuir ativos gerenciados no Experience Manager {#share-assets-from-aem}

Os ativos Adobe Experience Manager (AEM) permitem que você compartilhe ativos, pastas e coleções com membros de sua organização e entidades externas, incluindo parceiros e fornecedores. Use os seguintes métodos para compartilhar ativos dos Ativos do Experience Manager como um Serviço em nuvem:

* Compartilhar como um link.
* Baixe ativos e compartilhe separadamente.
* Compartilhe por meio do aplicativo de desktop do AEM.
* Compartilhe por meio do Adobe Asset Link.
* (Funcionalidade futura) Compartilhe usando o Brand Portal.

## Compartilhar ativos como um link {#sharelink}

Para gerar o URL dos ativos que deseja compartilhar com os usuários, use a caixa de diálogo Compartilhamento de links. Os usuários com privilégios de administrador ou com permissões de leitura no `/var/dam/share` local podem visualização os links compartilhados com eles. Compartilhar ativos por meio de um link é uma maneira conveniente de disponibilizar recursos para terceiros sem que eles precisem primeiro fazer logon nos ativos AEM.

>[!NOTE]
>
>* Você precisa da permissão Editar ACL na pasta ou no ativo que deseja compartilhar como um link.
>* Antes de compartilhar um link com os usuários, verifique se o Day CQ Mail Service está configurado. Caso contrário, ocorrerá um erro.


1. Na interface do usuário Ativos, selecione o ativo a ser compartilhado como um link.
1. Na barra de ferramentas, clique/toque em **[!UICONTROL Compartilhar link]**. Um link de ativo é criado automaticamente no campo **[!UICONTROL Compartilhar link]** . Copie este link e compartilhe-o com os usuários. A hora de expiração padrão do link é um dia.

   >[!NOTE]
   >
   >Se um ativo compartilhado for movido para um local diferente, seu link para de funcionar. Recriar o link e compartilhar novamente com os usuários.

<!--
## Share assets as a link {#sharelink}

To generate the URL for assets you want to share with users, use the Link Sharing dialog. Users with administrator privileges or with read permissions at `/var/dam/share` location are able to view the links shared with them. Sharing assets through a link is a convenient way of making resources available to external parties without them having to first log in to AEM Assets.

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

   For the local and author properties, provide the URL for the local and author instance respectively. Both local and author properties have the same value if you run a single AEM author instance. For publish, provide the URL for the publish instance.

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
   >AEM supports generating the preview of assets of these MIME types: JPG, PNG, GIF, BMP, INDD, PDF, and PPT. You can only download the assets of the other MIME types.

1. To download the shared asset, click/tap **[!UICONTROL Select]** from the toolbar, click/tap the asset, and then click/tap **[!UICONTROL Download]** from the toolbar.
1. To view the assets you shared as links, go to the Assets user interface and click/tap the GlobalNav icon. Choose **[!UICONTROL Navigation]** from the list to display the Navigation pane.
1. From the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.
1. To un-share an asset, select it and tap/click **[!UICONTROL Unshare]** from the toolbar.

A message confirms that you unshared the asset. In addition, the entry for the asset is removed from the list.
-->

## Baixar e compartilhar ativos {#download-and-share-assets}

Os usuários podem baixar alguns ativos e compartilhá-los fora do Experience Manager. Para obter mais informações, consulte [como pesquisar ativos](/help/assets/search-assets.md), [como baixar ativos](/help/assets/download-assets-from-aem.md)e [como baixar coleções](manage-collections.md#download-a-collection)

## Compartilhar ativos com profissionais de criação {#share-with-creatives}

Os profissionais de marketing e os usuários de linha de negócios podem facilmente compartilhar ativos aprovados com seus profissionais criativos usando,

* **Aplicativo** para desktop AEM: O aplicativo funciona no Windows e no Mac. Consulte Visão geral [do aplicativo para](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html)desktop. Para saber como qualquer usuário autorizado do desktop pode acessar facilmente os ativos compartilhados, consulte [procurar, pesquisar e pré-visualização dos ativos](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets). Os usuários da área de trabalho podem criar ativos e compartilhá-los de volta com seus colegas que são usuários do AEM, por exemplo, fazendo upload de novas imagens. Consulte [fazer upload de ativos usando o aplicativo](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)para desktop.

* **Link** do ativo da Adobe: Os profissionais criativos podem pesquisar e usar ativos diretamente do Adobe InDesign, Adobe Illustrator e Adobe Photoshop.

## Configurar compartilhamento de ativos {#configure-sharing}

As diferentes opções para compartilhar os ativos exigem configuração específica e têm pré-requisitos específicos.

### Configurar compartilhamento de links de ativos {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Para gerar o URL dos ativos que deseja compartilhar com os usuários, use a caixa de diálogo Compartilhamento de links. Os usuários com privilégios de administrador ou com permissões de leitura no `/var/dam/share` local podem visualização os links compartilhados com eles. Compartilhar ativos por meio de um link é uma maneira conveniente de disponibilizar recursos para terceiros sem que eles precisem primeiro fazer logon nos ativos AEM.

>[!NOTE]
>
>Se você quiser compartilhar links da instância do autor de AEM com entidades externas, certifique-se de expor apenas os seguintes URLs para `GET` solicitações. Bloqueie outros URLs para garantir que sua instância de autor de AEM esteja segura.
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


<!--
## Configure Day CQ mail service {#configmailservice}

Before you can share assets as links, configure the email service.

1. Click or tap the AEM logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.
1. From the list of services, locate **[!UICONTROL Day CQ Mail Service]**.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

    * SMTP server host name: email server host name
    * SMTP server port: email server port
    * SMTP user: email server user name
    * SMTP password: email server password

1. Click/tap **[!UICONTROL Save]**.
-->

### Configurar tamanho máximo de dados {#maxdatasize}

Quando você baixa ativos do link compartilhado usando o recurso Compartilhamento de link, o AEM compacta a hierarquia de ativos do repositório e retorna o ativo em um arquivo ZIP. No entanto, na ausência de limites para a quantidade de dados que pode ser compactada em um arquivo ZIP, grandes quantidades de dados são submetidas à compactação, o que causa erros de memória esgotada no JVM. Para proteger o sistema de um possível ataque de negação de serviço devido a essa situação, é possível configurar o tamanho máximo dos arquivos baixados. Se o tamanho descompactado do ativo exceder o valor configurado, as solicitações de download do ativo serão rejeitadas. O valor padrão é 100 MB.

1. Clique/toque no logotipo do AEM e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. No console da Web, localize a configuração do Servlet **[!UICONTROL Adhoc de Compartilhamento de ativos Ad hoc do]** Day CQ DAM.
1. Open the configuration in edit mode, and modify the value of the **[!UICONTROL Max Content Size (uncompressed)]** parameter.
1. Salve as alterações.

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->

### Ativar ações de área de trabalho para usar com o aplicativo de área de trabalho {#desktop-actions}

Na interface do usuário Ativos em um navegador, você pode explorar os locais dos ativos ou fazer check-out e abrir o ativo para edição no aplicativo de desktop. Essas opções são chamadas de ações da área de trabalho e, para ativá-las, consulte [Ativar ações da área de trabalho na interface](https://docs.adobe.com/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2)da Web do AEM.

![Ativar ações da área de trabalho para usar como atalho ao trabalhar com o aplicativo da área de trabalho](assets/enable_desktop_actions.png)

### Configurações para usar o Adobe Asset Link {#configure-asset-link}

O Adobe Asset Link simplifica a colaboração entre criadores e comerciantes no processo de criação de conteúdo. Ele conecta os ativos Adobe Experience Manager (AEM) aos aplicativos de desktop da Creative Cloud, Adobe InDesign, Adobe Photoshop e Adobe Illustrator. O painel Adobe Asset Link permite que os criadores acessem e modifiquem o conteúdo armazenado nos ativos AEM sem deixar os aplicativos criativos com os quais estão mais familiarizados.

Consulte [como configurar o AEM para usar com o Adobe Asset Link](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html).

## Best practices and troubleshooting {#bestpractices}

* Pastas de ativos ou coleções que contêm um espaço em branco em seu nome podem não ser compartilhadas.
* Se os usuários não puderem baixar os ativos compartilhados, verifique com o administrador do AEM quais são os limites [de](#maxdatasize) download.

<!--
* If you cannot send email with links to shared assets or if the other users cannot receive your email, check with your AEM administrator if the [email service](/help/assets/configure-asset-sharing.md#configmailservice) is configured or not. 
* If you cannot share assets using link sharing functionality, ensure that you have the appropriate permissions. See [share assets](#sharelink).
-->

<!--
Add content or link about how to share using Brand Portal when it is available on Cloud Service.
-->
