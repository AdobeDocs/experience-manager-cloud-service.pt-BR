---
title: Referências do desenvolvedor para [!DNL Assets]
description: '[!DNL Assets] APIs and developer reference content lets you manage assets, including binary files, metadata, renditions, comments, and [!DNL Content Fragments].'
contentOwner: AG
feature: APIs,API HTTP de ativos
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager Assets] casos de uso do desenvolvedor, APIs e material de referência {#assets-cloud-service-apis}

O artigo contém recomendações, materiais de referência e recursos para desenvolvedores de [!DNL Assets] como um [!DNL Cloud Service]. Ele inclui um novo módulo de upload de ativos, uma referência de API e informações sobre o suporte fornecido em workflows de pós-processamento.

## [!DNL Experience Manager Assets] APIs e operações {#use-cases-and-apis}

[!DNL Assets] o as a  [!DNL Cloud Service] fornece várias APIs para interagir programaticamente com ativos digitais. Cada API suporta casos de uso específicos, conforme mencionado na tabela abaixo. A interface do usuário [!DNL Assets], [!DNL Experience Manager] aplicativo de desktop e [!DNL Adobe Asset Link] são compatíveis com todas ou algumas das operações.

>[!CAUTION]
>
>Algumas APIs continuam a existir, mas não têm suporte ativo (denotado com um ×). Na medida do possível, não use essas APIs.

| Nível de suporte | Descrição |
| ------------- | --------------------------- |
| Instantâneo | Compatível |
| × | Não suportado. Não utilizar. |
| - | Não disponível |

| Caso de uso | [aem-upload](https://github.com/adobe/aem-upload) | [AEM / Sling / APIs ](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/index.html) JCRJava | [Serviço Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] API HTTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Servlets Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html) _(Visualização)_ |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **Binário original** |  |  |  |  |  |  |
| Criar original | Instantâneo | × | - | × | × | - |
| Ler original | - | × | Instantâneo | Instantâneo | Instantâneo | - |
| Atualizar original | Instantâneo | × | Instantâneo | × | × | - |
| Excluir original | - | Instantâneo | - | Instantâneo | Instantâneo | - |
| Copiar original | - | Instantâneo | - | Instantâneo | Instantâneo | - |
| Mover original | - | Instantâneo | - | Instantâneo | Instantâneo | - |
| **Metadados** |  |  |  |  |  |  |
| Criar metadados | - | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - |
| Ler metadados | - | Instantâneo | - | Instantâneo | Instantâneo | - |
| Atualizar metadados | - | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - |
| Excluir metadados | - | Instantâneo | Instantâneo | Instantâneo | Instantâneo | - |
| Copiar metadados | - | Instantâneo | - | Instantâneo | Instantâneo | - |
| Mover metadados | - | Instantâneo | - | Instantâneo | Instantâneo | - |
| **Fragmentos de conteúdo (CF)** |  |  |  |  |  |  |
| Criar CF | - | Instantâneo | - | Instantâneo | - | - |
| Ler CF | - | Instantâneo | - | Instantâneo | - | Instantâneo |
| Atualizar CF | - | Instantâneo | - | Instantâneo | - | - |
| Excluir CF | - | Instantâneo | - | Instantâneo | - | - |
| Copiar CF | - | Instantâneo | - | Instantâneo | - | - |
| Mover CF | - | Instantâneo | - | Instantâneo | - | - |
| **Versões** |  |  |  |  |  |  |
| Criar versão | Instantâneo | Instantâneo | - | - | - | - |
| Ler versão | - | Instantâneo | - | - | - | - |
| Excluir versão | - | Instantâneo | - | - | - | - |
| **Pastas** |  |  |  |  |  |  |
| Criar pasta | Instantâneo | Instantâneo | - | Instantâneo | - | - |
| Ler pasta | - | Instantâneo | - | Instantâneo | - | - |
| Excluir pasta | Instantâneo | Instantâneo | - | Instantâneo | - | - |
| Copiar pasta | Instantâneo | Instantâneo | - | Instantâneo | - | - |
| Mover pasta | Instantâneo | Instantâneo | - | Instantâneo | - | - |

## Upload de ativo {#asset-upload}

Em [!DNL Experience Manager] como um [!DNL Cloud Service], é possível fazer upload direto dos ativos para o armazenamento na nuvem usando a API HTTP. As etapas para fazer upload de um arquivo binário estão abaixo. Execute essas etapas em um aplicativo externo e não na JVM [!DNL Experience Manager].

1. [Envie uma solicitação](#initiate-upload) HTTP. Ele informa [!DNL Experience Manage]ou a implantação de sua intenção de fazer upload de um novo binário.
1. [POST do conteúdo do binário para um ou mais URIs fornecidos pelo pedido de início. ](#upload-binary) 
1. [Envie uma ](#complete-upload) solicitação HTTP para informar ao servidor que o conteúdo do binário foi carregado com êxito.

![Visão geral do protocolo de upload binário direto](assets/add-assets-technical.png)

>[!IMPORTANT]
Execute as etapas acima em um aplicativo externo e não na JVM [!DNL Experience Manager].

A abordagem oferece uma manipulação escalável e mais eficiente dos uploads de ativos. As diferenças em comparação com [!DNL Experience Manager] 6.5 são:

* Os binários não passam por [!DNL Experience Manager], que agora simplesmente coordena o processo de upload com o armazenamento em nuvem binário configurado para a implantação.
* O armazenamento em nuvem binário funciona com uma Rede de entrega de conteúdo (CDN) ou rede de borda. Um CDN seleciona um ponto de extremidade de upload mais próximo de um cliente. Quando os dados viajam uma distância menor até um terminal próximo, o desempenho de upload e a experiência do usuário melhoram, especialmente para equipes distribuídas geograficamente.

>[!NOTE]
Consulte o código de cliente para implementar essa abordagem no [biblioteca aem-upload](https://github.com/adobe/aem-upload) de código aberto.

### Iniciar upload {#initiate-upload}

Envie uma solicitação HTTP POST para a pasta desejada. Os ativos são criados ou atualizados nesta pasta. Inclua o seletor `.initiateUpload.json` para indicar que a solicitação é iniciar o upload de um arquivo binário. Por exemplo, o caminho para a pasta onde o ativo deve ser criado é `/assets/folder`. A solicitação de POST é `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

O tipo de conteúdo do corpo da solicitação deve ser `application/x-www-form-urlencoded` dados do formulário, contendo os seguintes campos:

* `(string) fileName`: Obrigatório. O nome do ativo como ele aparece em [!DNL Experience Manager].
* `(number) fileSize`: Obrigatório. O tamanho do arquivo, em bytes, do ativo que está sendo carregado.

Uma única solicitação pode ser usada para iniciar uploads para vários binários, desde que cada binário contenha os campos necessários. Se bem-sucedida, a solicitação responde com um código de status `201` e um corpo contendo dados JSON no seguinte formato:

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

* `completeURI` (string): Chame esse URI quando o binário terminar o upload. O URI pode ser um URI absoluto ou relativo, e os clientes devem ser capazes de lidar com ambos. Ou seja, o valor pode ser `"https://author.acme.com/content/dam.completeUpload.json"` ou `"/content/dam.completeUpload.json"` Consulte [concluir o upload](#complete-upload).
* `folderPath` (string): Caminho completo para a pasta na qual o binário é carregado.
* `(files)` (matriz): Uma lista de elementos cujo comprimento e ordem correspondem ao comprimento e à ordem da lista de informações binárias fornecidas na solicitação de inicialização.
* `fileName` (string): O nome do binário correspondente, conforme fornecido na solicitação de inicialização. Esse valor deve ser incluído na solicitação completa.
* `mimeType` (string): O tipo mime do binário correspondente, conforme fornecido na solicitação de inicialização. Esse valor deve ser incluído na solicitação completa.
* `uploadToken` (string): Um token de upload para o binário correspondente. Esse valor deve ser incluído na solicitação completa.
* `uploadURIs` (matriz): Uma lista de strings cujos valores são URIs completos para as quais o conteúdo do binário deve ser carregado (consulte  [Upload binário](#upload-binary)).
* `minPartSize` (número): O comprimento mínimo, em bytes, dos dados que podem ser fornecidos a qualquer um dos  `uploadURIs`, se houver mais de um URI.
* `maxPartSize` (número): O comprimento máximo, em bytes, dos dados que podem ser fornecidos a qualquer um dos  `uploadURIs`, se houver mais de um URI.

### Upload binário {#upload-binary}

A saída de iniciar um upload inclui um ou mais valores de URI de upload. Se mais de um URI for fornecido, o cliente dividirá o binário em partes e fará a solicitação POST de cada parte para cada URI, em ordem. Use todos os URIs. Certifique-se de que o tamanho de cada parte esteja dentro dos tamanhos mínimo e máximo especificados na resposta de inicialização. Os nós de borda CDN ajudam a acelerar o upload solicitado de binários.

Um possível método para fazer isso é calcular o tamanho da peça com base no número de URIs de upload fornecidos pela API. Por exemplo, suponha que o tamanho total do binário seja de 20.000 bytes e o número de URIs de upload seja 2. Siga estas etapas:

* Calcule o tamanho da peça dividindo o tamanho total pelo número de URIs: 20.000 / 2 = 10.000.
* Intervalo de POST byte 0-9.999 do binário para o primeiro URI na lista de URIs de upload.
* Intervalo de POST byte 10.000 - 19.999 do binário para o segundo URI na lista de URIs de upload.

Se o upload for bem-sucedido, o servidor responderá a cada solicitação com um código de status `201`.

### Carregamento completo {#complete-upload}

Depois que todas as partes de um arquivo binário forem carregadas, envie uma solicitação POST HTTP para o URI completo fornecido pelos dados de início. O tipo de conteúdo do corpo da solicitação deve ser `application/x-www-form-urlencoded` dados do formulário, contendo os seguintes campos.

| Fields | Tipo | Obrigatório ou não | Descrição |
|---|---|---|---|
| `fileName` | Sequência de caracteres | Obrigatório | O nome do ativo, conforme fornecido pelos dados de início. |
| `mimeType` | Sequência de caracteres | Obrigatório | O tipo de conteúdo HTTP do binário, como foi fornecido pelos dados de início. |
| `uploadToken` | Sequência de caracteres | Obrigatório | Faça upload do token para o binário, conforme fornecido pelos dados de início. |
| `createVersion` | Booleano | Opcional | Se `True` e um ativo com o nome especificado existir, [!DNL Experience Manager] criará uma nova versão do ativo. |
| `versionLabel` | Sequência de caracteres | Opcional | Se uma nova versão for criada, o rótulo associado à nova versão de um ativo . |
| `versionComment` | Sequência de caracteres | Opcional | Se uma nova versão for criada, os comentários associados à versão. |
| `replace` | Booleano | Opcional | Se `True` e um ativo com o nome especificado existir, [!DNL Experience Manager] o excluirá e o recriará. |

>[!NOTE]
Se o ativo existir e nenhum `createVersion` ou `replace` for especificado, [!DNL Experience Manager] atualizará a versão atual do ativo com o novo binário.

Como o processo de inicialização, os dados completos da solicitação podem conter informações para mais de um arquivo.

O processo de upload de um binário não é feito até que o URL completo seja chamado para o arquivo. Um ativo é processado após a conclusão do processo de upload. O processamento não é iniciado mesmo se o arquivo binário do ativo for carregado completamente, mas o processo de upload não estiver concluído.

Se bem-sucedido, o servidor responde com um código de status `200`.

### Biblioteca de upload de código aberto {#open-source-upload-library}

Para saber mais sobre os algoritmos de upload ou para criar seus próprios scripts e ferramentas de upload, o Adobe oferece bibliotecas e ferramentas de código aberto:

* [Biblioteca de upload do aem de código aberto](https://github.com/adobe/aem-upload).
* [Ferramenta de linha de comando de código aberto](https://github.com/adobe/aio-cli-plugin-aem).

### APIs de upload de ativos obsoletos {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

O novo método de upload é compatível somente para [!DNL Adobe Experience Manager] como um [!DNL Cloud Service]. As APIs de [!DNL Adobe Experience Manager] 6.5 estão obsoletas. Os métodos relacionados ao upload ou atualização de ativos ou representações (qualquer upload binário) estão obsoletos nas seguintes APIs:

* [API HTTP do Experience Manager Assets](mac-api-assets.md)
* `AssetManager` API Java, como  `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Biblioteca de upload do aem de código aberto](https://github.com/adobe/aem-upload).
* [Ferramenta de linha de comando de código aberto](https://github.com/adobe/aio-cli-plugin-aem).


## Fluxos de trabalho de processamento e pós-processamento de ativos {#post-processing-workflows}

Em [!DNL Experience Manager], o processamento de ativos é baseado na configuração **[!UICONTROL Processando Perfis]** que usa [microsserviços de ativos](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). O processamento não requer extensões de desenvolvedor.

Para configuração de fluxo de trabalho de pós-processamento, use os fluxos de trabalho padrão com extensões com etapas personalizadas.

## Suporte a etapas do fluxo de trabalho no fluxo de trabalho de pós-processamento {#post-processing-workflows-steps}

Os clientes que atualizam de versões anteriores do [!DNL Experience Manager] podem usar os microsserviços de ativos para processar ativos. Os microsserviços de ativos nativos em nuvem são muito mais simples de configurar e usar. Algumas etapas do fluxo de trabalho usadas no fluxo de trabalho [!UICONTROL Ativo de atualização DAM] na versão anterior não são suportadas.

[!DNL Experience Manager] como  [!DNL Cloud Service] suporte para as seguintes etapas do fluxo de trabalho:

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

Os seguintes modelos de fluxo de trabalho técnicos são substituídos por microsserviços de ativos ou o suporte não está disponível:

* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
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
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

