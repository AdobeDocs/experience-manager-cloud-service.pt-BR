---
title: Referências do desenvolvedor para [!DNL Assets]
description: "[!DNL Assets] O conteúdo de referência de APIs e desenvolvedores permite gerenciar ativos, incluindo arquivos binários, metadados, representações, comentários e [!DNL Content Fragments]."
contentOwner: AG
feature: APIs,Assets HTTP API
role: Developer,Architect,Admin
exl-id: c75ff177-b74e-436b-9e29-86e257be87fb
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1899'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager Assets] casos de uso do desenvolvedor, APIs e material de referência {#assets-cloud-service-apis}

O artigo contém recomendações, materiais de referência e recursos para desenvolvedores de [!DNL Assets] como [!DNL Cloud Service]. Ele inclui um novo módulo de upload de ativos, uma referência de API e informações sobre o suporte fornecido em workflows de pós-processamento.

## [!DNL Experience Manager Assets] APIs e operações {#use-cases-and-apis}

[!DNL Assets] como [!DNL Cloud Service] O fornece várias APIs para interagir programaticamente com ativos digitais. Cada API suporta casos de uso específicos, conforme mencionado na tabela abaixo. O [!DNL Assets] interface do usuário, [!DNL Experience Manager] aplicativo de desktop e [!DNL Adobe Asset Link] dar suporte a todas ou algumas das operações.

>[!CAUTION]
>
>Algumas APIs continuam a existir, mas não têm suporte ativo (denotado com um ×). Na medida do possível, não use essas APIs.

| Nível de suporte | Descrição |
| ------------- | --------------------------- |
| ✓ | Compatível |
| × | Não suportado. Não utilizar. |
| - | Não disponível |

| Caso de uso | [aem-upload](https://github.com/adobe/aem-upload) | [Experience Manager / Sling / JCR](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) APIs Java | [Serviço Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) | [[!DNL Assets] API HTTP](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html#create-an-asset) | Sling [GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) / [POST](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html) servlets | [GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=pt-BR) |
| ----------------|:---:|:---:|:---:|:---:|:---:|:---:|
| **Binário original** |  |  |  |  |  |  |
| Criar original | ✓ | × | - | × | × | - |
| Ler original | - | × | ✓ | ✓ | ✓ | - |
| Atualizar original | ✓ | × | ✓ | × | × | - |
| Excluir original | - | ✓ | - | ✓ | ✓ | - |
| Copiar original | - | ✓ | - | ✓ | ✓ | - |
| Mover original | - | ✓ | - | ✓ | ✓ | - |
| **Metadados** |  |  |  |  |  |  |
| Criar metadados | - | ✓ | ✓ | ✓ | ✓ | - |
| Ler metadados | - | ✓ | - | ✓ | ✓ | - |
| Atualizar metadados | - | ✓ | ✓ | ✓ | ✓ | - |
| Excluir metadados | - | ✓ | ✓ | ✓ | ✓ | - |
| Copiar metadados | - | ✓ | - | ✓ | ✓ | - |
| Mover metadados | - | ✓ | - | ✓ | ✓ | - |
| **Fragmentos de conteúdo (CF)** |  |  |  |  |  |  |
| Criar CF | - | ✓ | - | ✓ | - | - |
| Ler CF | - | ✓ | - | ✓ | - | ✓ |
| Atualizar CF | - | ✓ | - | ✓ | - | - |
| Excluir CF | - | ✓ | - | ✓ | - | - |
| Copiar CF | - | ✓ | - | ✓ | - | - |
| Mover CF | - | ✓ | - | ✓ | - | - |
| **Versões** |  |  |  |  |  |  |
| Criar versão | ✓ | ✓ | - | - | - | - |
| Ler versão | - | ✓ | - | - | - | - |
| Excluir versão | - | ✓ | - | - | - | - |
| **Pastas** |  |  |  |  |  |  |
| Criar pasta | ✓ | ✓ | - | ✓ | - | - |
| Ler pasta | - | ✓ | - | ✓ | - | - |
| Excluir pasta | ✓ | ✓ | - | ✓ | - | - |
| Copiar pasta | ✓ | ✓ | - | ✓ | - | - |
| Mover pasta | ✓ | ✓ | - | ✓ | - | - |

## Upload de ativo {#asset-upload}

Em [!DNL Experience Manager] como [!DNL Cloud Service], é possível fazer upload direto dos ativos para o armazenamento na nuvem usando a API HTTP. As etapas para fazer upload de um arquivo binário estão abaixo. Execute essas etapas em um aplicativo externo e não na [!DNL Experience Manager] JVM.

1. [Enviar uma solicitação HTTP](#initiate-upload). Ele informa [!DNL Experience Manage]Ou implantação de sua intenção de fazer upload de um novo binário.
1. [PUT do conteúdo do binário](#upload-binary) a um ou mais URI fornecidos pelo pedido de início.
1. [Enviar uma solicitação HTTP](#complete-upload) para informar ao servidor que o conteúdo do binário foi carregado com êxito.

![Visão geral do protocolo de upload binário direto](assets/add-assets-technical.png)

>[!IMPORTANT]
Execute as etapas acima em um aplicativo externo e não no [!DNL Experience Manager] JVM.

A abordagem oferece uma manipulação escalável e mais eficiente dos uploads de ativos. As diferenças em comparação com [!DNL Experience Manager] 6.5 são:

* Os binários não passam [!DNL Experience Manager], que agora simplesmente coordena o processo de upload com o armazenamento em nuvem binário configurado para a implantação.
* O armazenamento em nuvem binário funciona com uma Rede de entrega de conteúdo (CDN) ou rede de borda. Um CDN seleciona um ponto de extremidade de upload mais próximo de um cliente. Quando os dados viajam uma distância menor até um terminal próximo, o desempenho de upload e a experiência do usuário melhoram, especialmente para equipes distribuídas geograficamente.

>[!NOTE]
Consulte o código de cliente para implementar essa abordagem no código aberto [biblioteca de upload do aem](https://github.com/adobe/aem-upload).
[!IMPORTANT]
Em determinadas circunstâncias, as alterações podem não se propagar totalmente entre as solicitações para o Experience Manager devido à natureza eventualmente consistente do armazenamento no Cloud Service. Isso leva a 404 respostas para iniciar ou concluir chamadas de upload devido às criações de pasta necessárias não terem sido propagadas. Os clientes devem esperar respostas 404 e lidar com elas implementando uma nova tentativa com uma estratégia de recuo.

### Iniciar upload {#initiate-upload}

Envie uma solicitação HTTP POST para a pasta desejada. Os ativos são criados ou atualizados nesta pasta. Incluir o seletor `.initiateUpload.json` para indicar que a solicitação é iniciar o upload de um arquivo binário. Por exemplo, o caminho para a pasta onde o ativo deve ser criado é `/assets/folder`. A solicitação POST é `POST https://[aem_server]:[port]/content/dam/assets/folder.initiateUpload.json`.

O tipo de conteúdo do corpo da solicitação deve ser `application/x-www-form-urlencoded` dados do formulário, contendo os seguintes campos:

* `(string) fileName`: Obrigatório. O nome do ativo como ele aparece em [!DNL Experience Manager].
* `(number) fileSize`: Obrigatório. O tamanho do arquivo, em bytes, do ativo que está sendo carregado.

Uma única solicitação pode ser usada para iniciar uploads para vários binários, desde que cada binário contenha os campos necessários. Se bem-sucedida, a solicitação responde com um `201` código de status e um corpo contendo dados JSON no seguinte formato:

```json
{
    "completeURI": "(string)",
    "folderPath": "(string)",
    "files": [
        {
            "fileName": "(string)",
            "mimeType": "(string)",
            "uploadToken": "(string)",
            "uploadURIs": [
                "(string)"
            ],
            "minPartSize": (number),
            "maxPartSize": (number)
        }
    ]
}
```

* `completeURI` (string): Chame esse URI quando o binário terminar o upload. O URI pode ser um URI absoluto ou relativo, e os clientes devem ser capazes de lidar com ambos. Ou seja, o valor pode ser `"https://[aem_server]:[port]/content/dam.completeUpload.json"` ou `"/content/dam.completeUpload.json"` Consulte [upload completo](#complete-upload).
* `folderPath` (string): Caminho completo para a pasta na qual o binário é carregado.
* `(files)` (matriz): Uma lista de elementos cujo comprimento e ordem correspondem ao comprimento e à ordem da lista de informações binárias fornecidas na solicitação de inicialização.
* `fileName` (string): O nome do binário correspondente, conforme fornecido na solicitação de inicialização. Esse valor deve ser incluído na solicitação completa.
* `mimeType` (string): O tipo mime do binário correspondente, conforme fornecido na solicitação de inicialização. Esse valor deve ser incluído na solicitação completa.
* `uploadToken` (string): Um token de upload para o binário correspondente. Esse valor deve ser incluído na solicitação completa.
* `uploadURIs` (matriz): Uma lista de strings cujos valores são URIs completos para as quais o conteúdo do binário deve ser carregado (consulte [Upload binário](#upload-binary)).
* `minPartSize` (número): O comprimento mínimo, em bytes, dos dados que podem ser fornecidos a qualquer uma das `uploadURIs`, se houver mais de um URI.
* `maxPartSize` (número): O comprimento máximo, em bytes, dos dados que podem ser fornecidos a qualquer uma das `uploadURIs`, se houver mais de um URI.

### Upload binário {#upload-binary}

A saída de iniciar um upload inclui um ou mais valores de URI de upload. Se mais de um URI for fornecido, o cliente poderá dividir o binário em partes e fazer solicitações de PUT de cada parte aos URIs de upload fornecidos, em ordem. Se você optar por dividir o binário em partes, siga as seguintes diretrizes:

* Cada parte, com exceção do último, deve ter um tamanho maior ou igual a `minPartSize`.
* Cada parte deve ter um tamanho inferior ou igual a `maxPartSize`.
* Se o tamanho do seu binário exceder `maxPartSize`, divida o binário em partes para carregá-lo.
* Não é necessário usar todos os URIs.

Se o tamanho do seu binário for menor ou igual a `maxPartSize`, em vez disso, você pode fazer upload de todo o binário para um único URI de upload. Se mais de um URI de upload for fornecido, use o primeiro e ignore o restante. Não é necessário usar todos os URIs.

Os nós de borda CDN ajudam a acelerar o upload solicitado de binários.

A maneira mais fácil de fazer isso é usar o valor de `maxPartSize` como seu tamanho de peça. O contrato da API garante que haja URIs de upload suficientes para carregar seu binário se você usar esse valor como tamanho de peça. Para fazer isso, divida o binário em partes do tamanho `maxPartSize`, usando um URI para cada parte, em ordem. A parte final pode ser de qualquer tamanho menor ou igual a `maxPartSize`. Por exemplo, suponha que o tamanho total do binário seja de 20.000 bytes, a variável `minPartSize` é de 5.000 bytes, `maxPartSize` é de 8.000 bytes e o número de URIs de upload é de 5. Execute as seguintes etapas:

* Faça upload dos primeiros 8.000 bytes do binário usando o primeiro URI de upload.
* Faça upload dos segundos 8.000 bytes do binário usando o segundo URI de upload.
* Faça upload dos últimos 4.000 bytes do binário usando o terceiro URI de upload. Uma vez que esta é a parte final, não é necessário que seja superior a `minPartSize`.
* Não é necessário usar os dois últimos URIs de upload. Você pode ignorá-los.

Um erro comum é calcular o tamanho da peça com base no número de URIs de upload fornecidos pela API. O contrato da API não garante que essa abordagem funcione e pode realmente resultar em tamanhos de partes fora do intervalo entre `minPartSize` e `maxPartSize`. Isso pode resultar em falhas de upload binário.

Novamente, a maneira mais fácil e segura é simplesmente usar partes de tamanho igual a `maxPartSize`.

Se o upload for bem-sucedido, o servidor responderá a cada solicitação com uma `201` código de status.

>[!NOTE]
Para obter mais informações sobre o algoritmo de carregamento, consulte o [documentação de recursos oficiais](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload) e [Documentação da API](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/api/binary/BinaryUpload.html) no projeto Apache Jackrabbit Oak.

### Carregamento completo {#complete-upload}

Depois que todas as partes de um arquivo binário forem carregadas, envie uma solicitação POST HTTP para o URI completo fornecido pelos dados de início. O tipo de conteúdo do corpo da solicitação deve ser `application/x-www-form-urlencoded` dados do formulário, contendo os seguintes campos.

| Campos | Tipo | Obrigatório ou não | Descrição |
|---|---|---|---|
| `fileName` | String | Obrigatório | O nome do ativo, conforme fornecido pelos dados de início. |
| `mimeType` | String | Obrigatório | O tipo de conteúdo HTTP do binário, como foi fornecido pelos dados de início. |
| `uploadToken` | String | Obrigatório | Faça upload do token para o binário, conforme fornecido pelos dados de início. |
| `createVersion` | Booleano | Opcional | If `True` e um ativo com o nome especificado existe, então [!DNL Experience Manager] cria uma nova versão do ativo. |
| `versionLabel` | String | Opcional | Se uma nova versão for criada, o rótulo associado à nova versão de um ativo . |
| `versionComment` | String | Opcional | Se uma nova versão for criada, os comentários associados à versão. |
| `replace` | Booleano | Opcional | If `True` e existe um ativo com o nome especificado, [!DNL Experience Manager] exclui o ativo e depois o recria. |
| `uploadDuration` | Número | Opcional | O tempo total, em milissegundos, para o upload do arquivo em sua totalidade. Se especificado, a duração do upload é incluída nos arquivos de log do sistema para análise da taxa de transferência. |
| `fileSize` | Número | Opcional | O tamanho, em bytes, do arquivo. Se especificado, o tamanho do arquivo é incluído nos arquivos de log do sistema para análise da taxa de transferência. |

>[!NOTE]
Se o ativo existir e nem `createVersion` nor `replace` for especificado, [!DNL Experience Manager] atualiza a versão atual do ativo com o novo binário.

Como o processo de inicialização, os dados completos da solicitação podem conter informações para mais de um arquivo.

O processo de upload de um binário não é feito até que o URL completo seja chamado para o arquivo. Um ativo é processado após a conclusão do processo de upload. O processamento não é iniciado mesmo se o arquivo binário do ativo for carregado completamente, mas o processo de upload não estiver concluído. Se o upload for bem-sucedido, o servidor responderá com uma `200` código de status.

### Biblioteca de upload de código aberto {#open-source-upload-library}

Para saber mais sobre os algoritmos de upload ou para criar seus próprios scripts e ferramentas de upload, o Adobe oferece bibliotecas e ferramentas de código aberto:

* [Biblioteca de upload de aem de código aberto](https://github.com/adobe/aem-upload).
* [Ferramenta de linha de comando de código aberto](https://github.com/adobe/aio-cli-plugin-aem).

>[!NOTE]
A biblioteca do aem-upload e a ferramenta de linha de comando usam o [biblioteca node-httptransfer](https://github.com/adobe/node-httptransfer/)

### APIs de upload de ativos obsoletos {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

O novo método de upload é suportado somente para [!DNL Adobe Experience Manager] como [!DNL Cloud Service]. As APIs de [!DNL Adobe Experience Manager] 6.5 estão obsoletas. Os métodos relacionados ao upload ou atualização de ativos ou representações (qualquer upload binário) estão obsoletos nas seguintes APIs:

* [API HTTP Experience Manager Assets](mac-api-assets.md)
* `AssetManager` API Java, como `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Biblioteca de upload de aem de código aberto](https://github.com/adobe/aem-upload).
* [Ferramenta de linha de comando de código aberto](https://github.com/adobe/aio-cli-plugin-aem).
* [Documentação do Apache Jackrabbit Oak para upload direto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html#Upload).


## Fluxos de trabalho de processamento e pós-processamento de ativos {#post-processing-workflows}

Em [!DNL Experience Manager], o processamento de ativos é baseado em **[!UICONTROL Processando perfis]** configuração que usa [microsserviços de ativos](asset-microservices-configure-and-use.md#get-started-using-asset-microservices). O processamento não requer extensões de desenvolvedor.

Para configuração de fluxo de trabalho de pós-processamento, use os fluxos de trabalho padrão com extensões com etapas personalizadas.

## Suporte a etapas do fluxo de trabalho no fluxo de trabalho de pós-processamento {#post-processing-workflows-steps}

Se você atualizar de uma versão anterior de [!DNL Experience Manager], é possível usar os microsserviços de ativos para processar ativos. Os microsserviços de ativos nativos em nuvem são mais simples de configurar e usar. Algumas etapas do fluxo de trabalho usadas na [!UICONTROL Ativo de atualização DAM] não há suporte para fluxo de trabalho na versão anterior. Para obter mais informações sobre as classes compatíveis, consulte a [Referência da API Java ou Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html).

Os seguintes modelos de fluxo de trabalho técnicos são substituídos por microsserviços de ativos ou o suporte não está disponível:

* `com.day.cq.dam.cameraraw.process.CameraRawHandlingProcess`
* `com.day.cq.dam.core.process.CommandLineProcess`
* `com.day.cq.dam.pdfrasterizer.process.PdfRasterizerHandlingProcess`
* `com.day.cq.dam.core.process.AddPropertyWorkflowProcess`
* `com.day.cq.dam.core.process.CreateSubAssetsProcess`
* `com.day.cq.dam.core.process.DownloadAssetProcess`
* `com.day.cq.dam.word.process.ExtractImagesProcess`
* `com.day.cq.dam.word.process.ExtractPlainProcess`
* `com.day.cq.dam.ids.impl.process.IDSJobProcess`
* `com.day.cq.dam.indd.process.INDDMediaExtractProcess`
* `com.day.cq.dam.indd.process.INDDPageExtractProcess`
* `com.day.cq.dam.core.impl.lightbox.LightboxUpdateAssetProcess`
* `com.day.cq.dam.pim.impl.sourcing.upload.process.ProductAssetsUploadProcess`
* `com.day.cq.dam.core.process.SendDownloadAssetEmailProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.switchengine.process.SwitchEngineHandlingProcess`
* `com.day.cq.dam.core.process.GateKeeperProcess`
* `com.day.cq.dam.s7dam.common.process.DMEncodeVideoWorkflowCompletedProcess`
* `com.day.cq.dam.core.process.DeleteImagePreviewProcess`
* `com.day.cq.dam.video.FFMpegTranscodeProcess`
* `com.day.cq.dam.core.process.ThumbnailProcess`
* `com.day.cq.dam.video.FFMpegThumbnailProcess`
* `com.day.cq.dam.core.process.CreateWebEnabledImageProcess`
* `com.day.cq.dam.core.process.CreatePdfPreviewProcess`
* `com.day.cq.dam.s7dam.common.process.VideoUserUploadedThumbnailProcess`
* `com.day.cq.dam.s7dam.common.process.VideoThumbnailDownloadProcess`
* `com.day.cq.dam.s7dam.common.process.VideoProxyServiceProcess`
* `com.day.cq.dam.scene7.impl.process.Scene7UploadProcess`
* `com.day.cq.dam.s7dam.common.process.S7VideoThumbnailProcess`
* `com.day.cq.dam.core.process.MetadataProcessorProcess`
* `com.day.cq.dam.core.process.AssetOffloadingProcess`
* `com.adobe.cq.dam.dm.process.workflow.DMImageProcess`

<!-- Commenting the previous list documented at the time of GA. Replacing it with the updated list via cqdoc-18231.

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
-->

<!-- PPTX source: slide in add-assets.md - overview of direct binary upload section of
https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)

>[!MORELIKETHIS]
* [[!DNL Experience Cloud] as a [!DNL Cloud Service] SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md).

