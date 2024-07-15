---
title: Como importar, exportar e organizar o Adaptive Forms ou PDF forms em uma instância do AEM Forms?
description: Saiba como migrar Forms adaptável, PDF forms, temas e outros ativos de suporte para e de instâncias AEM.
topic-tags: forms-manager
role: Admin, User
feature: Adaptive Forms
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: 6f547bd743932d45e45e0a3c47ff5eb2129cb664
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 3%

---



| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/manage-administer-aem-forms/import-export-forms-templates) |
| AEM as a Cloud Service | Este artigo |

# Importar ou exportar ativos adaptáveis do Forms e do AEM Forms {#importing-and-exporting-assets-to-aem-forms}

Você pode mover o Adaptive Forms e ativos relacionados, como temas do Formulário adaptável, Modelo de dados de formulário (FDM), modelos de Formulário adaptável, Fragmentos e PDF forms entre [!DNL AEM Forms] instâncias.

## Baixar o Forms adaptável, o PDF forms ou ativos relacionados {#download-forms-amp-documents-assets}

Para baixar formulários ou ativos relacionados:

1. Faça logon na instância do [!DNL Experience Manager Forms].
1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

   ![Selecionar Forms](/help/forms/assets/select-forms.png)

1. Selecione os ativos e clique no ícone **[!UICONTROL Download]** no painel superior.

   ![Baixar Forms](/help/forms/assets/download-form.png)

   Ao baixar o formulário, a caixa de diálogo **[!UICONTROL Baixar ativo(s)]** é exibida.

   ![Baixar ativos de formulários](/help/forms/assets/download-form-assets.png)

1. Clique em **[!UICONTROL Baixar]**.

Os ativos selecionados são baixados como um arquivo (arquivo .zip).

## Fazer upload de ativos adaptáveis do Forms, PDF forms ou relacionados {#upload-forms-amp-documents-assets}

Você pode fazer upload dos tipos de ativos compatíveis individualmente ou como um arquivo ZIP. Para um arquivo ZIP, os caminhos relativos de todos os ativos compatíveis são exibidos. Os ativos incompatíveis dentro do ZIP são ignorados e não são listados. No entanto, se o arquivo ZIP contiver somente os ativos incompatíveis, uma mensagem de erro será exibida em vez da caixa de diálogo pop-up.
Para carregar um formulário ou um ativo relacionado:

1. Faça logon na instância do [!DNL Experience Manager Forms].
1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

   ![Selecionar Forms](/help/forms/assets/select-forms.png)

1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Carregar arquivo]**. Uma caixa de diálogo é exibida.

   ![Carregar Forms](/help/forms/assets/form-upload.png)

1. Na caixa de diálogo, navegue e selecione o pacote ou o arquivo a ser importado. Você também pode selecionar outros tipos de arquivos compatíveis. Selecione **[!UICONTROL Abrir]**. A pasta ou o nome de arquivo selecionado não deve incluir caracteres especiais.

   Na caixa de diálogo, verifique os detalhes dos ativos sendo carregados e selecione **[!UICONTROL Carregar]**.

   Caso você carregue um ativo de formulários existente, o ativo é atualizado.

   >[!NOTE]
   >
   > Quando um nome entra em conflito com tipos de recursos diferentes, o upload de um pacote não substitui a hierarquia de pastas existente. Por exemplo, se você tiver um formulário adaptável chamado &#39;Treinamento&#39; no local `/content/dam/formsanddocuments` em um servidor. É possível baixar o formulário adaptável e carregá-lo em outro servidor. O segundo servidor também tem uma pasta com o nome &#39;Treinamento&#39; no mesmo local `/content/dam/formsanddocuments`. Falha no upload.

## Baixar um tema

Você pode exportar temas em [!DNL AEM Forms] que você pode usar em outros projetos ou instâncias. O AEM permite baixar temas como um arquivo zip, que pode ser carregado na instância.
Para baixar um tema:

1. Faça logon na sua instância de Autor do [!DNL Experience Manager Forms].
1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Temas]**.

   ![Selecionar tema](/help/forms/assets/select-theme.png)

1. Na página Temas, selecione o tema e clique no ícone **[!UICONTROL Baixar]** no painel superior.

   ![Baixar Tema](/help/forms/assets/download-theme.png)

   Ao baixar o tema, a caixa de diálogo **[!UICONTROL Baixar ativo(s)]** é exibida.

   ![Baixar ativos de tema](/help/forms/assets/download-theme-asset.png)

1. Clique em **[!UICONTROL Baixar]**.

Os ativos selecionados são baixados como um arquivo (arquivo .zip).

## Carregar um tema {#uploading-a-theme}

Você pode carregar e usar temas que outras pessoas criam em seus formulários.
Para fazer upload de um tema:

1. Faça logon na instância do [!DNL Experience Manager Forms].
1. No Experience Manager, navegue até **[!UICONTROL Forms]** > **[!UICONTROL Temas]**.

   ![Selecionar tema](/help/forms/assets/select-theme.png)

1. Na página Temas, clique em **[!UICONTROL Criar]** > **[!UICONTROL Carregar Arquivo]**.

   ![Carregar Tema](/help/forms/assets/theme-upload.png)

1. Procure e selecione um pacote de tema no computador e clique em **[!UICONTROL Carregar]**. O tema carregado fica disponível na página Temas.

## Usar pastas para organizar o Forms adaptável, PDF forms e ativos relacionados  {#folders-and-organizing-assets}

Você pode usar pastas para organizar e organizar ativos. Organizar documentos e ativos em uma pasta permite agrupar os arquivos para facilitar o gerenciamento. Você pode selecionar uma pasta e escolher baixá-la ou excluí-la.

### Criar uma pasta {#create-a-folder}

Para criar uma pasta:

1. Faça logon na instância do [!DNL Experience Manager Forms].
1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

   ![Selecionar formulário](/help/forms/assets/select-forms.png)

1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Pasta]**.

   ![Criar pasta](/help/forms/assets/create-folder.png)

   A caixa de diálogo **[!UICONTROL Adicionar pasta]** é exibida.
1. Insira o **[!UICONTROL Título]**. O **[!UICONTROL Nome]** é preenchido automaticamente à medida que você digita o **[!UICONTROL Título]**.

   ![Adicionar pasta](/help/forms/assets/add-folder.png)

1. Clique em **[!UICONTROL Criar]**.

   >[!NOTE]
   >
   >Por padrão, o valor do campo de nome é preenchido automaticamente a partir do título. O nome só pode conter caracteres alfanuméricos ou os caracteres especiais de hífen (-) e sublinhado (_). Quaisquer outros caracteres especiais inseridos no título são substituídos automaticamente por um hífen e você será solicitado a confirmar o novo nome. Você pode optar por continuar com o nome sugerido ou fazer mais edições.

Uma nova pasta com o título definido é exibida no local atual na lista de ativos.

Se existir uma pasta com o nome especificado, o envio falha com um erro. Você pode exibir a mensagem de erro passando o cursor do mouse sobre o ícone de erro ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) que aparece ao lado do campo de nome.

Você pode selecionar a pasta criada para entrar na pasta e criar ativos ou pastas dentro dela. Além disso, você pode selecionar uma pasta e optar por colocá-la na fila para download, excluí-la ou editar seu nome.

### Criar cópias de um ou mais ativos {#create-copies-of-one-or-more-assets-or-letters}

Você pode usar um ativo existente para criar rapidamente um ativo com propriedades, conteúdo e ativos herdados semelhantes.

Para criar cópias de ativos:

1. Faça logon na instância do [!DNL Experience Manager Forms].
1. Na página de ativos relevantes, selecione um ou mais ativos. A interface exibe o ícone **[!UICONTROL Copiar]**.
1. Selecione **[!UICONTROL Copiar]**. A interface exibe o ícone ![Colar](/help/forms/assets/Smock_Paste_18_N.svg).

   ![Copiar ativo](/help/forms/assets/copy-asset.png)

   Você também pode escolher ir/navegar dentro de uma pasta antes de colar. Pastas diferentes podem conter ativos com os mesmos nomes. Para obter mais informações sobre pastas, consulte [Pastas e organização de ativos](#folders-and-organizing-assets).
1. Selecione **[!UICONTROL Colar]**.

   ![Colar ativo](/help/forms/assets/paste-asset.png)

1. A caixa de diálogo **[!UICONTROL Colar]** é exibida. O sistema gera automaticamente nomes e títulos para as novas cópias de ativos, mas você pode editar os títulos e nomes dos ativos.

   Se você copiar e colar os ativos no mesmo local, um sufixo &quot;-CopyXX&quot; será adicionado ao nome existente do `asset`. Se não houver título para o ativo copiado, o campo de título gerado automaticamente permanecerá em branco.

   ![Colar ativo em novo local](/help/forms/assets/paste-click-asset.png)

   Se necessário, edite o **[!UICONTROL Título]** com o qual deseja salvar a cópia do ativo. O **[!UICONTROL Nome]** é preenchido automaticamente à medida que você digita o **[!UICONTROL Título]**.
1. Selecione **[!UICONTROL Colar]**. Novas cópias dos ativos copiados são criadas.

## Pesquisar {#search-forms}

Quando você tem um grande número de ativos, pesquisar o ativo certo é demorado. Você pode executar uma pesquisa baseada em texto para um ativo específico na página do ativo.

Para pesquisar o ativo:

1. Faça logon na instância do [!DNL Experience Manager Forms].
1. Clique no ![ícone de pesquisa](assets/folder-search-icon.svg) ícone de pesquisa.

   ![Formulário de pesquisa](/help/forms/assets/search-form.png)

1. Insira o nome do ativo que deseja pesquisar na barra de pesquisa.

1. Uma lista de ativos relacionados é exibida. Selecione o ativo desejado na lista de ativos exibida.

   ![Pesquisar ativos](/help/forms/assets/search-bar.png)

Para obter mais informações e instruções sobre como usar a pesquisa, consulte [Pesquisar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=pt-BR).

<!--
## Export or create a package {#export-a-workflow-application}

You can use packages to install new content, install new functionality, transfer content between instances, and back up content.
To export or create a package:

1. Log in to your [!DNL Experience Manager Forms] instance.
1. Navigate to **[!UICONTROL Tools]** ![hammer](assets/hammer.png) &gt; **[!UICONTROL Deployment]** &gt; **[!UICONTROL Packages]**.

   ![Package Manager](/help/forms/assets/package-manager.png)

1. Click **[!UICONTROL Create Package]**.

   ![Create package](/help/forms/assets/create-package.png)   
   
   When **[!UICONTROL Create Package]** is clicked, the **[!UICONTROL New Package]** dialog box appears.
1. Specify the package name, version, and group for the package. 
   
   ![New package](/help/forms/assets/new-package.png)  

   * **Package Name** - Select a descriptive name to help you identify the contents of the package.

   * **Version** - It is a textual field to indicate a version. This is appended to the package name to form the name of the zip file.

   * **Group** - This is the target group (or folder) name. Groups help you organize your packages. A folder is created for the group if it does not already exist. If you leave the group name blank, it creates the package in the main package list.

1. Click **[!UICONTROL OK]**.

   Once the package is created, it appears at the top of the list of packages.

1. Click **[!UICONTROL Edit]**.
   
   ![Edit Package](/help/forms/assets/edit-package.png)
    
1. Open the **[!UICONTROL Filters]** tab.
   
   ![Open filter tab](/help/forms/assets/add-filter-package.png)
   
1.  Click **[!UICONTROL Add Filter]**. 
   
      ![Add filter](/help/forms/assets/add-filter.png)

      You can specify the path of the package. You can also add rules and other validations for the package.

      ![Add path](/help/forms/assets/add-path.png)

1. Click **[!UICONTROL Save]** after you are finished editing the settings.
1. Click **[!UICONTROL Build]** to create the package.
    
     ![Build path](/help/forms/assets/build-package.png)

   After the package is built, you can download the package and import it to the other server. The workflow application appears on the server where the package is uploaded.

   >[!NOTE]
   >
   >For the workflow application to work properly, also export the corresponding Adaptive Form and workflow model with the work application.

   Once a package is uploaded to AEM, you can modify its settings. You can also download or delete the package.

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, select and select the assets you want to export to a single package, and then select Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Select **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Select Resolve. Or skip to the next step. Even if you do not select resolve, the dependencies are still exported.
1. To download the .cmp file, select **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Select **Adobe Experience Manager** in the Global Navigation bar.
1. Select tools ( ![tools](assets/tools.png)) and then select **Forms**.
1. Select **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Select **Export** and, in the confirm message, select **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Select the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

<!-- ### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, select **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Select **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator. -->

## Consulte também {#see-also}

{{see-also}}
