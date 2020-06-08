---
title: Adicionar seus ativos digitais ao Adobe Experience Manager
description: Adicione seus ativos digitais ao Adobe Experience Manager como um serviço em nuvem
translation-type: tm+mt
source-git-commit: 114bc678fc1c6e3570d6d2a29bc034feb68aa56d
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 3%

---


# Adicionar ativos digitais ao Adobe Experience Manager {#add-assets-to-experience-manager}

O Adobe Experience Manager enriquece o conteúdo binário dos arquivos digitais carregados com metadados avançados, tags inteligentes, execuções e outros serviços de Gerenciamento de ativos digitais (DAM). You can upload various types of files, such as images, documents, and raw image files, from your local folder or a network drive to Experience Manager Assets.

Vários métodos de upload são fornecidos. In addition to the most commonly used browser upload, other methods of adding assets to the Experience Manager repository exist, including desktop clients, like Adobe Asset Link or Experience Manager desktop app, upload and ingestion scripts that customers would create, and automated ingestion integrations added as AEM extensions.

We will focus on upload methods for end users here, and provide links to articles describing technical aspects of asset upload and ingestion using Experience Manager APIs and SDKs.

Embora você possa carregar e gerenciar qualquer arquivo binário no Experience Manager, os formatos de arquivo mais usados têm suporte para serviços adicionais, como extração de metadados ou geração de pré-visualização/execução. Refer to [supported file formats](file-format-support.md) for details.

You can also choose to have additional processing done on the uploaded assets. Vários perfis de processamento de ativos podem ser configurados na pasta, na qual os ativos são carregados, para adicionar metadados específicos, representações ou serviços de processamento de imagens. See [Additional processing](#additional-processing) below for more information.

>[!NOTE]
>
> Experience Manager as a Cloud Service leverages a new way of uploading assets - direct binary upload. Por padrão, ele é suportado pelos recursos e clientes prontos para uso do produto, como a interface do usuário do AEM, o Adobe Asset Link, o aplicativo de desktop do AEM e, portanto, transparente para os usuários finais.
>
> Upload code that is customized or extended by customers technical teams needs to use the new upload APIs and protocols.

## Upload assets {#upload-assets}

Para carregar um arquivo (ou vários arquivos), você pode selecioná-los na área de trabalho e arrastar e soltar na interface do usuário (navegador da Web) na pasta de destino. Como alternativa, você pode iniciar o upload a partir da interface do usuário.

1. Na interface do usuário do Assets, navegue até o local onde deseja adicionar ativos digitais.
1. Para fazer upload dos ativos, execute um dos procedimentos a seguir:

   * Na barra de ferramentas, toque no ícone **[!UICONTROL Criar]** . Then, on the menu, then tap **[!UICONTROL Files]**. You can rename the file in the presented dialog if needed.
   * Em um navegador compatível com HTML5, arraste os ativos diretamente na interface do usuário dos Ativos. A caixa de diálogo para renomear o arquivo não é exibida.
   ![create_menu](assets/create_menu.png)

   To select multiple files, press the Ctrl or Command key and select the assets in the file picker dialog. When using an iPad, you can select only one file at a time.

<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#

   You can pause the uploading of large assets (greater than 500 MB) and resume it later from the same page. Tap the **[!UICONTROL Pause]** icon beside progress bar that appears when an upload starts.

   ![chlimage_1-211](assets/chlimage_1-211.png)

   The size above which an asset is considered a large asset is configurable. For example, you can configure the system to consider assets above 1000 MB (instead of 500 MB) as large assets. In this case, **[!UICONTROL Pause]** appears on the progress bar when assets of size greater than 1000 MB are uploaded.

   The Pause button does not show if a file greater than 1000 MB is uploaded with a file less than 1000 MB. However, if you cancel the less than 1000 MB file upload, the **[!UICONTROL Pause]** button appears.

   To modify the size limit, configure the `chunkUploadMinFileSize` property of the `fileupload`node in the CRX repository.

   When you click the **[!UICONTROL Pause]** icon, it toggles to a **[!UICONTROL Play]** icon. To resume uploading, click the **[!UICONTROL Play]** icon.

   ![chlimage_1-212](assets/chlimage_1-212.png)
-->

1. Para cancelar um upload em andamento, clique em Fechar (`X`) ao lado da barra de progresso. When you cancel the upload operation, AEM Assets deletes the partially uploaded portion of the asset.

   If you cancel the upload operation before the files are uploaded, AEM Assets stops uploading the current file and refreshes the content. No entanto, os arquivos que já foram carregados não são excluídos.


<!-- #ENGCHECK do we support pausing? I couldn't get pause to show with 1.5GB upload.... If not, this should be removed#
   The ability to resume uploading is especially helpful in low-bandwidth scenarios and network glitches, where it takes a long time to upload a large asset. You can pause the upload operation and continue later when the situation improves. When you resume, uploading starts from the point where you paused it.
-->

<!-- #ENGCHECK assuming this is not relevant? remove after confirming#
   During the upload operation, AEM saves the portions of the asset being uploaded as chunks of data in the CRX repository. When the upload completes, AEM consolidates these chunks into a single block of data in the repository.

   To configure the cleanup task for the unfinished chunk upload jobs, go to `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`.
-->


1. A caixa de diálogo de andamento do upload nos ativos AEM exibe a contagem de arquivos carregados com êxito e os arquivos que não foram carregados.

Além disso, a interface do usuário Ativos exibe o ativo mais recente que você carregou ou a pasta que criou primeiro.

>[!NOTE]
>
> Para fazer upload de hierarquias de pastas aninhadas para o AEM, consulte o upload [em massa de ativos](#bulk-upload).

<!-- #ENGCHECK I'm assuming this is no longer relevant.... If yes, this should be removed#

### Serial uploads {#serialuploads}

Uploading numerous assets in bulk consumes significant I/O resources, which may adversely impact the performance of your AEM Assets instance. In particular, if you have a slow internet connection, the time to upload drastically increases due to a spike in disk I/O. Moreover, your web browser may introduce additional restrictions to the number of POST requests AEM Assets can handle for concurrent asset uploads. As a result, the upload operation fails or terminate prematurely. In other words, AEM assets may miss some files while ingesting a bunch of files or altogether fail to ingest any file.

To overcome this situation, AEM Assets ingests one asset at a time (serial upload) during a bulk upload operation, instead of the concurrently ingesting all the assets.

Serial uploading of assets is enabled by default. To disable the feature and allow concurrent uploading, overlay the `fileupload` node in Crx-de and set the value of the `parallelUploads` property to `true`.

### Streamed uploads {#streamed-uploads}

If you upload many assets to AEM, the I/O requests to server increase drastically, which reduces the upload efficiency and can even cause some upload task to time out. AEM Assets supports streamed uploading of assets. Streamed uploading reduces the disk I/O during the upload operation by avoiding asset storage in a temporary folder on the server before copying it to the repository. Instead, the data is transferred directly to the repository. This way, the time to upload large assets and the possibility of timeouts is reduced. Streamed upload is enabled by default in AEM Assets.

>[!NOTE]
>
>Streaming upload is disabled for AEM running on JEE server with servlet-api version lower than 3.1.
-->

### Manuseio de uploads quando o ativo já existe {#handling-upload-existing-file}

Se você fizer upload de um ativo com o mesmo nome de um ativo já disponível no local em que você está fazendo upload do ativo, uma caixa de diálogo de aviso será exibida.

Você pode optar por substituir um ativo existente, criar outra versão ou manter ambos renomeando o novo ativo que é carregado. Se você substituir um ativo existente, os metadados do ativo e quaisquer modificações anteriores (por exemplo, anotações, recortes e assim por diante) que você fez no ativo existente serão excluídos. If you choose to keep both assets, the new asset is renamed with the number `1` appended to its name.

>[!NOTE]
>
>Quando você seleciona **[!UICONTROL Substituir]** na caixa de diálogo Conflito [!UICONTROL de] nomes, a ID do ativo é regenerada para o novo ativo. Essa ID é diferente da ID do ativo anterior.
>
>Se o Asset Insights estiver habilitado para rastrear impressões/cliques com o Adobe Analytics, a ID de ativo regenerada invalida os dados capturados para o ativo no Analytics.

To retain the duplicate asset in AEM Assets, tap/click **[!UICONTROL Keep]**. Para excluir o ativo de duplicado carregado, toque/clique em **[!UICONTROL Excluir]**.

### Tratamento de nomes de arquivos e caracteres proibidos {#filename-handling}

AEM Assets prevents you from uploading assets with the forbidden characters in their filenames. If you try to upload an asset with file name containing a disallowed character or more, AEM Assets displays a warning message and stops the upload until you remove these characters or upload with an allowed name.

Para adequar-se a convenções de nomenclatura de arquivos específicas para sua organização, a caixa de diálogo [!UICONTROL Carregar ativos] permite especificar nomes longos para os arquivos carregados.

No entanto, os seguintes caracteres (lista separada por espaços de) não são suportados:

* asset file name must not contain `* / : [ \\ ] | # % { } ? &`
* o nome da pasta de ativos não deve conter `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

## Upload em massa de ativos {#bulk-upload}

Para carregar um número maior de arquivos, especialmente se eles existirem em uma hierarquia de pastas aninhadas no disco, as seguintes abordagens podem ser usadas:

* Use a custom upload script or tool that leverages [asset upload APIs](developer-reference-material-apis.md#asset-upload-technical). Such a custom tool can add additional handling of assets (for example, translate metadata or rename files), if required.
* Use o aplicativo [de desktop do](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) Experience Manager para fazer upload das hierarquias de pastas aninhadas.

>[!NOTE]
>
> Bulk upload as a part of content migration from other systems when setting up and deploying to Experience Manager requires careful planning, consideration, and choice of tools. Consulte o guia [de](/help/implementing/deploying/overview.md) implantação para obter orientação sobre as abordagens de migração de conteúdo.

## Upload assets using desktop clients {#upload-assets-desktop-clients}

In addition to web browser user interface, Experience Manager supports other clients on desktop. They also provide upload experience without the need to go to the web browser.

* [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) provides access to assets from AEM in Adobe Photoshop, Adobe Illustrator, and Adobe InDesign desktop applications. Você pode fazer upload do documento aberto no momento para o AEM diretamente da interface do usuário do Adobe Asset Link nesses aplicativos de desktop.
* [O aplicativo](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) de desktop Experience Manager simplifica o trabalho com ativos no desktop, independentemente do tipo de arquivo ou do aplicativo nativo que os manipula. É particularmente útil fazer upload de arquivos nas hierarquias de pastas aninhadas a partir do sistema de arquivos local, já que o upload do navegador suporta apenas o upload de listas de arquivos simples.

## Processamento adicional {#additional-processing}

In order to have additional processing done on the uploaded assets, you can use asset processing profiles profiles  on the folder, into which assets are uploaded. Eles estão disponíveis na caixa de diálogo **[!UICONTROL Propriedades]** da pasta.

![assets-folder-properties](assets/assets-folder-properties.png)

Os seguintes perfis estão disponíveis:

* [perfis](metadata-profiles.md) de metadados permitem aplicar propriedades de metadados padrão a ativos carregados nessa pasta
* [Processing profiles](asset-microservices-configure-and-use.md#processing-profiles) allow you to apply rendition processing and generate renditions in addition to the default ones

Additionally, if Dynamic Media is enabled in your environment:

* Os [perfis de imagem](dynamic-media/image-profiles.md) permitem aplicar cortes específicos (**[!UICONTROL Corte inteligente]** e corte de pixels) e configuração de nitidez aos ativos carregados
* [Video profiles](dynamic-media/video-profiles.md) allow you to apply specific video encoding profiles (resolution, format, parameters)

>[!NOTE]
>
> O corte do Dynamic Media e outras operações em ativos não são destrutivas, ou seja, não alteram o original carregado, mas fornecem parâmetros para o corte ou transformação de mídia a ser feito ao entregar os ativos

For folders that have a processing profile assigned, the profile name appears on the thumbnail in the card view. In the list view, the profile name appears in the **[!UICONTROL Processing Profile]** column.

## Upload or ingest assets using APIs {#upload-using-apis}

Detalhes técnicos das APIs e protocolo de upload, além de links para SDK de código aberto e clientes de amostra, são fornecidos na seção de upload [](developer-reference-material-apis.md#asset-upload-technical) de ativos da referência do desenvolvedor.

>[!MORELIKETHIS]
>
>* [Aplicativo de desktop do Adobe Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html)
>* [Adobe Asset Link](https://www.adobe.com/br/creativecloud/business/enterprise/adobe-asset-link.html)
>* [Documentação do Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)
>* [Referência técnica para upload de ativos](developer-reference-material-apis.md#asset-upload-technical)

