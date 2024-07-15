---
title: Como importar e exportar ativos para  [!DNL AEM Forms]?
description: Saiba como usar o DocuSign com um formulário adaptável para coletar assinaturas eletrônicas.
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1313'
ht-degree: 0%

---


# Importar e exportar ativos {#importing-and-exporting-assets-to-aem-forms}

Você pode mover formulários, temas, modelos, fragmentos de documentos, temas e outros ativos entre diferentes instâncias do [!DNL AEM Forms]. Esse movimento é necessário ao migrar sistemas ou mover formulários de um servidor de desenvolvimento ou de preparo para um servidor de produção.

Para os ativos para os quais há suporte para carregamento e importação por meio da interface do usuário do [!DNL AEM Forms], o uso da interface do usuário do Forms é a maneira recomendada para exportação ou importação. Não é recomendado usar o Gerenciador de pacotes AEM para exportar ou importar esses ativos.

## Baixar ou carregar ativos da Forms e de documentos {#download-or-upload-forms-amp-documents-assets}

A interface de usuário do [!DNL AEM Forms] permite exportar ativos de uma instância do AEM baixando-os como um pacote de CRX AEM ou como arquivos binários. Você pode importar o pacote AEM CRX baixado ou o arquivo binário para outra instância do AEM.

Todos os ativos oferecem suporte para exportação e importação através da interface do usuário do [!DNL AEM Forms], exceto os modelos de Formulário adaptável e as políticas de conteúdo do Formulário adaptável. Portanto, ao exportar um Formulário Adaptável da interface do usuário do [!DNL AEM Forms], o modelo de Formulário Adaptável relacionado e as políticas de conteúdo não são exportados automaticamente como outros ativos relacionados.

Para esses tipos de ativos, você deve usar o Gerenciador de pacotes AEM para criar um pacote do CRX no servidor AEM de origem e instalar o pacote no servidor de destino. Para obter informações sobre como criar e instalar pacotes, consulte [Implantação no AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html).

### Baixar ativos da Forms e de documentos {#download-forms-amp-documents-assets}

Para baixar os ativos do Forms e do Documents:

1. Faça logon na instância [!DNL AEM Forms].
1. Selecione Experience Manager ![ícone do adobeexperiencemanager](assets/adobeexperiencemanager.png) > ícone de navegação ![bússola](assets/Smock_Compass_18_N.svg)> **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione os ativos de formulários e selecione o ícone **[!UICONTROL Baixar]**.
1. Em Baixar ativos, escolha uma das opções a seguir e selecione **[!UICONTROL Baixar]**.

   * **Baixar como Pacote do CRX:** Use a opção para baixar e mover todos os ativos selecionados e as dependências relacionadas de uma instância [!DNL AEM Forms] para outra. Ele baixa todos os ativos e pastas como pacote crx. Todos os ativos de formulário, incluindo os formulários criados em AEM (Fragmentos adaptáveis de Forms e Formulários adaptáveis), documentos PDF e recursos (XSDs, XFS, imagens) podem ser baixados como pacotes na interface do usuário do [!DNL AEM Forms].
A vantagem de baixar ativos como pacote é que ele também baixa ativos que foram usados pelo ativo selecionado para download. Por exemplo, se você tiver um formulário adaptável que usa um modelo de formulário, XSD e uma imagem. Ao selecionar esse Formulário adaptável e baixá-lo como pacote, o pacote baixado também conterá o modelo de formulário, o XSD e a imagem. Todas as propriedades de metadados (incluindo propriedades personalizadas) associadas ao ativo também são baixadas.

   * **Baixar ativos como arquivos binários:** Use a opção para baixar somente modelos de formulário (XDP), PDF forms (PDF), documento (PDF) e recursos (imagens, esquemas, folhas de estilos). É possível editar esses ativos com aplicativos externos. Ele baixa os ativos de formulários que têm binários, como XSDs, XDPs, imagens, PDF e XDPs como um arquivo .zip.
Não é possível baixar Forms adaptável, fragmentos de formulário adaptável e temas, com a opção **[!UICONTROL Baixar ativos como arquivos binários]**. Para baixar esses ativos, você deve usar a opção **[!UICONTROL Baixar como Pacote do CRX]**.

   Os ativos selecionados são baixados como um arquivo (arquivo .zip).

   >[!NOTE]
   >
   >O pacote AEM e os arquivos binários são baixados como um arquivo (arquivo .zip). Os modelos dos ativos não são baixados junto com os ativos. É necessário exportar os modelos de ativos separadamente.

### Upload de ativos {#upload-forms-amp-documents-assets}

Para fazer upload de ativos do Forms e do Documents:

1. Faça logon na instância [!DNL AEM Forms].
1. Selecione Experience Manager ![ícone do adobeexperiencemanager](assets/adobeexperiencemanager.png) > ícone de navegação ![bússola](assets/Smock_Compass_18_N.svg)> **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione **Criar** >**Carregar Arquivo**. Uma caixa de diálogo Carregar formulários ou pacote é exibida.
1. Na caixa de diálogo, navegue e selecione o pacote ou o arquivo a ser importado. Você também pode selecionar o documento PDF, XSDs, imagens, folhas de estilos e formulários XDP. Selecione **[!UICONTROL Abrir]**. A pasta ou o nome de arquivo selecionado não deve incluir caracteres especiais.

   Na caixa de diálogo, verifique os detalhes dos ativos sendo carregados e selecione **[!UICONTROL Carregar]**.

   Caso você carregue um ativo de formulários existente, o ativo é atualizado.

   >[!NOTE]
   >
   >O carregamento de um pacote não substitui a hierarquia de pastas existente. Por exemplo, se você tiver um formulário adaptável chamado &quot;Treinamento&quot; no local /content/dam/formsanddocuments em um servidor. Você baixou o Formulário adaptável e carregou o formulário em outro servidor. O segundo servidor também tem uma pasta com o nome &#39;Training&#39; no mesmo local /content/dam/formsanddocuments. Falha no upload.

## Download ou upload de um tema {#downloading-or-uploading-a-theme}

Com [!DNL AEM Forms], você pode criar, baixar ou carregar temas. Um tema é criado como outros ativos, como formulários, documentos e cartas. É possível criar um tema, baixá-lo e carregá-lo em uma instância separada para reutilizá-lo. Para obter mais informações sobre temas, consulte [Temas](themes.md) em [!DNL AEM Forms].

### Download de um tema {#downloading-a-theme}

Você pode exportar temas em [!DNL AEM Forms] que você pode usar em outros projetos ou instâncias. O AEM permite baixar temas como um arquivo zip, que você pode carregar na instância.

Para baixar um tema:

1. Faça logon na instância [!DNL AEM Forms].
1. Selecione Experience Manager ![ícone do adobeexperiencemanager](assets/adobeexperiencemanager.png) > ícone de navegação ![bússola](assets/Smock_Compass_18_N.svg)> **[!UICONTROL Forms]** > **[!UICONTROL Temas]**.
1. Selecione o tema e selecione **[!UICONTROL Baixar]**. O tema é baixado como um arquivo (arquivo .zip).

### Carregamento de um tema {#uploading-a-theme}

Você pode usar temas criados com predefinições de estilo em seu projeto. Você pode importar pacotes de temas que outras pessoas criam carregando-os no seu projeto.

Para fazer upload de um tema:

1. No Experience Manager, navegue até **[!UICONTROL Forms]** > **[!UICONTROL Temas do Forms]**.
1. Na página Temas, clique em **[!UICONTROL Criar Forms]** > **[!UICONTROL Carregar Arquivo Forms]**.
1. No prompt do Upload de arquivo, procure e selecione um pacote de tema no computador e clique em **[!UICONTROL Upload do Forms]**. O tema é carregado.

<!--

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

### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

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
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator.
-->

## Exportar um aplicativo de fluxo de trabalho {#export-a-workflow-application}

Você pode usar o gerenciador de pacotes AEM para exportar aplicativos de workflow. O procedimento é conforme listado abaixo:

1. Abra o gerenciador de pacotes [!DNL AEM Forms].
1. Clique em **[!UICONTROL Criar Pacote]**. A caixa de diálogo **[!UICONTROL Novo Pacote]** é exibida.
1. Especifique o nome, a versão e o grupo do pacote. Clique em **[!UICONTROL OK]**.
1. Clique em **[!UICONTROL Editar]** e abra a guia **[!UICONTROL Filtros]**. Clique em **[!UICONTROL Adicionar filtro]**. Especifique o caminho do aplicativo de workflow. Por exemplo, /etc/fd/dashboard/startpoints/homemortgage. Clique em **[!UICONTROL Adicionar regra]**.

1. Abra a guia **[!UICONTROL Avançado]**. Selecione **[!UICONTROL Mesclar]** ou **[!UICONTROL Substituir]** no campo Manuseio de ACL. Clique em **[!UICONTROL Salvar]**.
1. Clique em **[!UICONTROL Build]** para criar o pacote.

   Depois que o pacote for criado, é possível baixá-lo e importá-lo para o outro servidor. O aplicativo de workflow aparece no servidor onde o pacote é carregado.

   >[!NOTE]
   >
   >Para que o aplicativo de fluxo de trabalho funcione corretamente, exporte também o formulário adaptável correspondente e o modelo de fluxo de trabalho com o aplicativo de trabalho.

## Pastas e organização de ativos {#folders-and-organizing-assets}

A interface de usuário do [!DNL AEM Forms] usa pastas para organizar ativos. Essas pastas são usadas para organizar ativos criados na interface do usuário do [!DNL AEM Forms]. Você pode renomear, criar subpastas e armazenar ativos e documentos nessas pastas. Organizar documentos e ativos em uma pasta permite agrupar os arquivos para facilitar o gerenciamento. Você pode selecionar uma pasta e escolher baixá-la ou excluí-la.

Para criar uma pasta, conclua as seguintes etapas:

### Criar uma pasta {#create-a-folder}

1. Faça logon na interface de usuário do [!DNL AEM Forms] em `https://<server>:<port>/aem/forms.html`.
1. Navegue até o local em que deseja criar uma pasta.
1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Pasta]**.
1. Insira os seguintes detalhes:

   * **Título:** Nome para exibição da pasta
   * **Nome:** *(Obrigatório)* O nome do nó no qual você deseja armazenar a pasta no repositório

   >[!NOTE]
   >
   >Por padrão, o valor do campo de nome é preenchido automaticamente a partir do título. O nome só pode conter caracteres alfanuméricos ou os caracteres especiais de hífen (-) e sublinhado (_). Quaisquer outros caracteres especiais inseridos no título são substituídos automaticamente por um hífen e você será solicitado a confirmar o novo nome. Você pode optar por continuar com o nome sugerido ou fazer mais edições.

1. Uma nova pasta com o título definido é exibida no local atual na lista de ativos.

   Se existir uma pasta com o nome especificado, o envio falha com um erro. Você pode exibir a mensagem de erro passando o cursor do mouse sobre o ícone de erro ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) que aparece ao lado do campo de nome.

   Você pode selecionar a pasta criada para entrar na pasta e criar ativos ou pastas dentro dela. Além disso, você pode selecionar uma pasta e optar por colocá-la na fila para download, excluí-la ou editar seu nome.

<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets and letters to quickly create a assets and letters with similar properties, content, and inherited assets. You can copy and paste data dictionaries, document fragments, and letters.

Complete the following steps to create copies of assets and letters:

1. In the relevant Assets or Letters page, select one or more assets/letters. The UI displays the Copy icon.
1. Select Copy. The UI displays the Paste icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Select Paste. The Paste dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If necessary, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Select Paste. New copies of the copied assets are created.

## Search {#search-forms}

[!DNL AEM Forms] UI lets you search your content. Using the top bar, you can select Search **[A]** to search your content for resources such as assets and documents.

When you search for assets, [!DNL AEM Forms] displays the side panel. You can also select ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also lets you save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also lets you save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](/help/sites-authoring/search.md).

-->

>[!MORELIKETHIS]
>
>* [Importar modelos de formulário de exportação](/help/forms/import-export-forms-templates.md)
>* [Usar temas nos Componentes Principais do Formulário Adaptável](/help/forms/using-themes-in-core-components.md)