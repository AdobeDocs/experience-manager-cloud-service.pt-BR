---
title: Referências do desenvolvedor para [!DNL Assets]
description: As APIs do [!DNL Assets] e o conteúdo de referência do desenvolvedor permitem gerenciar ativos, incluindo arquivos binários, metadados, representações, comentários e [!DNL Content Fragments].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8b1cc8af67c6d12d7e222e12ac4ff77e32ec7e0e
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 1%

---


# [!DNL Assets] APIs e material de referência do desenvolvedor {#assets-cloud-service-apis}

O artigo contém material de referência e recursos para desenvolvedores de [!DNL Assets] um Cloud Service. Inclui novo método de upload, referência de API e informações sobre o suporte fornecido em workflows de pós-processamento.

## Carregamento de ativos {#asset-upload-technical}

[!DNL Experience Manager] como Cloud Service, fornece um novo método para carregar ativos no repositório. Os usuários podem carregar diretamente os ativos no armazenamento da nuvem usando a API HTTP. As etapas para carregar um arquivo binário são:

1. [Envie uma solicitação](#initiate-upload)HTTP. Ele informa [!DNL Experience Manage]ou implanta sua intenção de fazer upload de um novo binário.
1. [POST o conteúdo do binário](#upload-binary) para um ou mais URIs fornecidos pelo pedido de início.
1. [Envie uma solicitação](#complete-upload) HTTP para informar ao servidor que o conteúdo do binário foi carregado com êxito.

![Visão geral do protocolo de carregamento binário direto](assets/add-assets-technical.png)

A abordagem oferece uma manipulação escalável e mais eficiente dos uploads de ativos. As diferenças em comparação com [!DNL Experience Manager] 6.5 são:

* Os binários não passam [!DNL Experience Manager], o que agora é simplesmente coordenar o processo de upload com o armazenamento da nuvem binária configurado para a implantação.
* O armazenamento de nuvem binário funciona com uma rede Content Delivery Network (CDN) ou Edge. Um CDN seleciona um ponto de extremidade de carregamento mais próximo de um cliente. Quando os dados percorrem uma distância menor para um terminal próximo, o desempenho do upload e a experiência do usuário melhoram, especialmente para equipes distribuídas geograficamente.

>[!NOTE]
>
>Consulte o código do cliente para implementar essa abordagem na biblioteca [de upload do](https://github.com/adobe/aem-upload)aem de código aberto.

### Iniciar carregamento {#initiate-upload}

Envie uma solicitação POST HTTP para a pasta desejada. Os ativos são criados ou atualizados nesta pasta. Inclua o seletor `.initiateUpload.json` para indicar que a solicitação é iniciar o upload de um arquivo binário. Por exemplo, o caminho para a pasta onde o ativo deve ser criado é `/assets/folder`. A solicitação de POST é `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

O tipo de conteúdo do corpo da solicitação deve ser dados de `application/x-www-form-urlencoded` formulário, contendo os seguintes campos:

* `(string) fileName`: Obrigatório. O nome do ativo como ele aparece em [!DNL Experience Manager].
* `(number) fileSize`: Obrigatório. O tamanho do arquivo, em bytes, do ativo que está sendo carregado.

Uma única solicitação pode ser usada para iniciar uploads para vários binários, desde que cada binário contenha os campos obrigatórios. Se bem-sucedida, a solicitação responderá com um código de `201` status e um corpo contendo dados JSON no seguinte formato:

```json
{
    "completeURI": "(string)",
    "folderPath": (string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ]
        }
    ]
}
```

* `completeURI` (string): Chame esse URI quando o binário terminar de carregar. O URI pode ser um URI absoluto ou relativo, e os clientes devem ser capazes de lidar com ele. Ou seja, o valor pode ser `"https://author.acme.com/content/dam.completeUpload.json"` ou `"/content/dam.completeUpload.json"` Ver upload [](#complete-upload)concluído.
* `folderPath` (string): Caminho completo para a pasta na qual o binário é carregado.
* `(files)` (matriz): Uma lista de elementos cujo comprimento e ordem correspondem ao comprimento e à ordem da lista de informações binárias fornecidas na solicitação de início.
* `fileName` (string): O nome do binário correspondente, conforme fornecido na solicitação de início. Esse valor deve ser incluído na solicitação completa.
* `mimeType` (string): O tipo mime do binário correspondente, conforme fornecido na solicitação de início. Esse valor deve ser incluído na solicitação completa.
* `uploadToken` (string): Um token de carregamento para o binário correspondente. Esse valor deve ser incluído na solicitação completa.
* `uploadURIs` (matriz): Uma lista de strings cujos valores são URIs completos para os quais o conteúdo do binário deve ser carregado (consulte [Carregar binário](#upload-binary)).
* `minPartSize` (número): O comprimento mínimo, em bytes, dos dados que podem ser fornecidos a qualquer um dos uploadURIs, se houver mais de um URI.
* `maxPartSize` (número): O comprimento máximo, em bytes, dos dados que podem ser fornecidos a qualquer um dos uploadURIs, se houver mais de um URI.

### Carregar binário {#upload-binary}

A saída de iniciar um upload inclui um ou mais valores de URI de upload. Se mais de um URI for fornecido, o cliente dividirá o binário em partes e fará uma solicitação POST de cada parte para cada URI, em ordem. Use todos os URIs. Certifique-se de que o tamanho de cada peça esteja dentro dos tamanhos mínimo e máximo especificados na resposta de início. Os nós de borda CDN ajudam a acelerar o carregamento solicitado de binários.

Um método potencial para fazer isso é calcular o tamanho da peça com base no número de URIs de upload fornecidos pela API. Por exemplo, suponha que o tamanho total do binário seja de 20.000 bytes e que o número de URIs de upload seja de 2. Em seguida, siga estas etapas:

* Calcule o tamanho da peça dividindo o tamanho total pelo número de URIs: 20.000 / 2 = 10.000.
* Intervalo de POST byte de 0 a 9.999 do binário para o primeiro URI na lista de URIs de upload.
* Intervalo de POST 10.000 - 19.999 do binário para o segundo URI na lista de URIs de upload.

Se o upload for bem-sucedido, o servidor responderá a cada solicitação com um código de `201` status.

### Carregamento completo {#complete-upload}

Depois que todas as partes de um arquivo binário forem carregadas, envie uma solicitação POST HTTP para o URI completo fornecido pelos dados de início. O tipo de conteúdo do corpo da solicitação deve ser dados de `application/x-www-form-urlencoded` formulário, contendo os seguintes campos.

| Fields | Tipo | Obrigatório ou não | Descrição |
|---|---|---|---|
| `fileName` | Sequência de caracteres | Obrigatório | O nome do ativo, conforme fornecido pelos dados de início. |
| `mimeType` | Sequência de caracteres | Obrigatório | O tipo de conteúdo HTTP do binário, conforme fornecido pelos dados de iniciação. |
| `uploadToken` | Sequência de caracteres | Obrigatório | Faça upload do token para o binário, conforme fornecido pelos dados de início. |
| `createVersion` | Booleano | Opcional | Se `True` e um ativo com o nome especificado existir, então [!DNL Experience Manager] cria uma nova versão do ativo. |
| `versionLabel` | Sequência de caracteres | Opcional | Se uma nova versão for criada, o rótulo associado à nova versão de um ativo. |
| `versionComment` | Sequência de caracteres | Opcional | Se uma nova versão for criada, os comentários associados à versão. |
| `replace` | Booleano | Opcional | Se `True` e um ativo com o nome especificado existir, [!DNL Experience Manager] exclui o ativo e, em seguida, o recria. |

>!![NOTE]
Se o ativo existir e nem `createVersion` nem `replace` for especificado, então [!DNL Experience Manager] atualiza a versão atual do ativo com o novo binário.

Como o processo de inicialização, os dados de solicitação completos podem conter informações para mais de um arquivo.

O processo de carregamento de um binário não é feito até que o URL completo seja chamado para o arquivo. Um ativo é processado após a conclusão do processo de upload. O processamento não start mesmo se o arquivo binário do ativo for carregado completamente, mas o processo de upload não estiver concluído.

Se bem-sucedido, o servidor responde com um código de `200` status.

### Biblioteca de upload de código aberto {#open-source-upload-library}

Para saber mais sobre os algoritmos de upload ou para criar seus próprios scripts e ferramentas de upload, o Adobe oferece bibliotecas e ferramentas de código aberto:

* [Biblioteca](https://github.com/adobe/aem-upload)de upload de aem de código aberto.
* [Ferramenta](https://github.com/adobe/aio-cli-plugin-aem)de linha de comando de código aberto.

### APIs de upload de ativos obsoletos {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

O novo método de upload é suportado somente para [!DNL Adobe Experience Manager] um Cloud Service. As APIs da versão [!DNL Adobe Experience Manager] 6.5 estão obsoletas. Os métodos relacionados ao upload ou atualização de ativos ou execuções (qualquer upload binário) estão obsoletos nas seguintes APIs:

* [API HTTP do Experience Manager Assets](mac-api-assets.md)
* `AssetManager` API Java, como `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Biblioteca](https://github.com/adobe/aem-upload)de upload de aem de código aberto.
* [Ferramenta](https://github.com/adobe/aio-cli-plugin-aem)de linha de comando de código aberto.


## Processamento de ativos e workflows pós-processamento {#post-processing-workflows}

Em [!DNL Experience Manager]geral, o processamento de ativos é baseado na configuração **[!UICONTROL Processando Perfis]** que usa [os microserviços](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)de ativos. O processamento não requer extensões de desenvolvedor.

Para a configuração do fluxo de trabalho de pós-processamento, use os workflows padrão com extensões com etapas personalizadas.

## Suporte às etapas do fluxo de trabalho no fluxo de trabalho de pós-processamento {#post-processing-workflows-steps}

Os clientes que atualizam de versões anteriores do [!DNL Experience Manager] podem usar os microserviços de ativos para processar ativos. Os microserviços de ativos nativos na nuvem são muito mais simples de configurar e usar. Algumas etapas do fluxo de trabalho usadas no fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM na versão anterior não são suportadas.

[!DNL Experience Manager] como Cloud Service, suporte as seguintes etapas do fluxo de trabalho:

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

Os seguintes modelos de fluxo de trabalho técnico são substituídos por microserviços de ativos ou o suporte não está disponível:

* `com.day.cq.dam.core.impl.process.DamMetadataWritebackWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.XMPWritebackProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.ScheduledPublishBPProcess`
* `com.day.cq.dam.core.process.ScheduledUnPublishBPProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.core.impl.process.SendTransientWorkflowCompletedEmailProcess`

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of 
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

>[!MORELIKETHIS]
* [O Experience Cloud como um SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)Cloud Service.

