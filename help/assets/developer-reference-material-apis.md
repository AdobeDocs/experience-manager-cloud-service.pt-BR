---
title: 'APIs de ativos para gerenciamento de ativos digitais no Adobe Experience Manager como Cloud Service '
description: As APIs de ativos permitem operações básicas de criação-leitura-atualização-exclusão (CRUD) para gerenciar ativos, incluindo binários, metadados, representações, comentários e Fragmentos de conteúdo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 1%

---


# Ativos como APIs de Cloud Service {#assets-cloud-service-apis}

<!-- 
Give a list of and overview of all reference information available.
* New upload method
* Javadocs
* Assets HTTP API documented at [https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html](https://helpx.adobe.com/experience-manager/6-5/assets/using/mac-api-assets.html)

-->

## Carregamento de ativos {#asset-upload-technical}

O Experience Manager como um serviço em nuvem fornece uma nova maneira de fazer upload de ativos no repositório - fazer upload binário direto para o armazenamento da nuvem binária. Esta seção fornece uma visão geral técnica.

### Visão geral do upload binário direto {#overview-binary-upload}

O algoritmo de alto nível para carregar um binário é:

1. Envie uma solicitação HTTP informando o AEM sobre a intenção de carregar um novo binário.
1. Publique o conteúdo do binário em um ou mais URIs fornecidos pelo pedido de início.
1. Envie uma solicitação HTTP para informar ao servidor que o conteúdo do binário foi carregado com êxito.

![Visão geral do protocolo de carregamento binário direto](assets/add-assets-technical.png)

As diferenças importantes comparadas às versões anteriores do AEM incluem:

* Os binários não passam pelo AEM, que agora está apenas coordenando o processo de upload com o armazenamento da nuvem binária configurado para a implantação
* O armazenamento em nuvem binário é fornecido por uma Rede de Delivery de Conteúdo (CDN, Edge Network), que aproxima o terminal de upload do cliente, ajudando, assim, a melhorar o desempenho de upload e a experiência do usuário, especialmente para equipes distribuídas que carregam ativos

Essa abordagem deve proporcionar uma manipulação mais escalável e eficiente dos uploads de ativos.

>[!NOTE]
>
>Para revisar o código do cliente que implementa essa abordagem, consulte a biblioteca de [upload do aem de código aberto](https://github.com/adobe/aem-upload)

### Iniciar carregamento {#initiate-upload}

A primeira etapa é enviar uma solicitação HTTP POST para a pasta onde o ativo deve ser criado ou atualizado; inclua o seletor `.initiateUpload.json` para indicar que a solicitação deve iniciar um upload binário. Por exemplo, o caminho para a pasta onde o ativo deve ser criado é `/assets/folder`:

```
POST https://[aem_server]/content/dam/assets/folder.initiateUpload.json
```

O tipo de conteúdo do corpo da solicitação deve ser dados de `application/x-www-form-urlencoded` formulário, contendo os seguintes campos:

* `(string) fileName`: Obrigatório. O nome do ativo como ele será exibido na instância.
* `(number) fileSize`: Obrigatório. O comprimento total, em bytes, do binário a ser carregado.

Uma única solicitação pode ser usada para iniciar uploads para vários binários, desde que cada binário contenha os campos obrigatórios. Se bem-sucedida, a solicitação responderá com um código de `201` status e um corpo contendo dados JSON no seguinte formato:

```
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
* `folderPath` (string): Caminho completo para a pasta onde o binário está sendo carregado.
* `(files)` (matriz): Uma lista de elementos cujo comprimento e ordem corresponderão ao comprimento e à ordem da lista de informações binárias fornecidas na solicitação inicial.
* `fileName` (string): O nome do binário correspondente, conforme fornecido na solicitação de início. Esse valor deve ser incluído na solicitação completa.
* `mimeType` (string): O tipo mime do binário correspondente, conforme fornecido na solicitação de início. Esse valor deve ser incluído na solicitação completa.
* `uploadToken` (string): Um token de carregamento para o binário correspondente. Esse valor deve ser incluído na solicitação completa.
* `uploadURIs` (matriz): Uma lista de strings cujos valores são URIs completos para os quais o conteúdo do binário deve ser carregado (consulte [Carregar binário](#upload-binary)).
* `minPartSize` (número): O comprimento mínimo, em bytes, dos dados que podem ser fornecidos a qualquer um dos uploadURIs, se houver mais de um URI.
* `maxPartSize` (número): O comprimento máximo, em bytes, dos dados que podem ser fornecidos a qualquer um dos uploadURIs, se houver mais de um URI.

### Carregar binário {#upload-binary}

A saída do início de um upload incluirá um ou mais valores de URI de upload. Se mais de um URI for fornecido, é responsabilidade do cliente &quot;dividir&quot; o binário em partes e executar o POST em cada parte, em ordem, para cada URI, em ordem. Todos os URIs devem ser usados e cada parte deve ser maior que o tamanho mínimo e menor que o tamanho máximo especificado na resposta de início. Essas solicitações serão encaminhadas por nós de borda CDN para acelerar o upload de binários.

Uma maneira potencial de fazer isso é calcular o tamanho da peça com base no número de URIs de upload fornecidos pela API. Exemplo, considerando que o tamanho total do binário é de 20.000 bytes e o número de URIs de upload é de 2:

* Calcule o tamanho da peça dividindo o tamanho total pelo número de URIs: 20.000 / 2 = 10.000
* Intervalo de bytes POST de 0 a 9.999 do binário para o primeiro URI na lista de URIs de upload
* Intervalo de bytes POST 10.000 - 19.999 do binário para o segundo URI na lista de URIs de upload

Se bem-sucedido, o servidor responde a cada solicitação com um código de `201` status.

### Carregamento completo {#complete-upload}

Depois que todas as partes de um arquivo binário forem carregadas, envie uma solicitação HTTP POST para o URI completo fornecido pelos dados de início. O tipo de conteúdo do corpo da solicitação deve ser dados de `application/x-www-form-urlencoded` formulário, contendo os seguintes campos.

| Fields | Tipo | Obrigatório ou não | Descrição |
|---|---|---|---|
| `fileName` | Sequência de caracteres | Obrigatório | O nome do ativo, conforme fornecido pelos dados de início. |
| `mimeType` | Sequência de caracteres | Obrigatório | O tipo de conteúdo HTTP do binário, conforme fornecido pelos dados de iniciação. |
| `uploadToken` | Sequência de caracteres | Obrigatório | Faça upload do token para o binário, conforme fornecido pelos dados de início. |
| `createVersion` | Booleano | Opcional | Se `True` e um ativo com o nome especificado já existir, o Experience Manager criará uma nova versão do ativo. |
| `versionLabel` | Sequência de caracteres | Opcional | Se uma nova versão for criada, o rótulo associado à nova versão de um ativo. |
| `versionComment` | Sequência de caracteres | Opcional | Se uma nova versão for criada, os comentários associados à versão. |
| `replace` | Booleano | Opcional | Se `True` e um ativo com o nome especificado já existir, o Experience Manager excluirá o ativo e, em seguida, recriá-lo. |

>!![NOTE]
Se o ativo já existir e nem `createVersion` nem `replace` for especificado, o Experience Manager atualizará a versão atual do ativo com o novo binário.

Como o processo de inicialização, os dados de solicitação completos podem conter informações para mais de um arquivo.

O processo de carregamento de um binário não é feito até que o URL completo seja chamado para o arquivo. Mesmo se o binário de um arquivo for carregado na totalidade, o ativo não será processado pela instância até que o processo de upload seja concluído.

Se bem-sucedido, o servidor responde com um código de `200` status.

### Biblioteca de upload de código aberto {#open-source-upload-library}

Para saber mais sobre os algoritmos de upload ou para criar seus próprios scripts e ferramentas de upload, a Adobe fornece bibliotecas e ferramentas de código aberto como pontos de partida:

* [Biblioteca aem-upload de código aberto](https://github.com/adobe/aem-upload)
* [Ferramenta de linha de comando open-source](https://github.com/adobe/aio-cli-plugin-aem)

### APIs de upload de ativos obsoletos {#deprecated-asset-upload-api}

<!-- #ENGCHECK review / update the list of deprecated APIs below. -->

Somente as novas APIs de carregamento são suportadas para Adobe Experience Manager como Cloud Service. As APIs do Adobe Experience Manager 6.5 estão obsoletas. Os métodos relacionados ao upload ou atualização de ativos ou execuções (qualquer upload binário) estão obsoletos nas seguintes APIs:

* [API HTTP do AEM Assets](mac-api-assets.md)
* `AssetManager` API Java, como `AssetManager.createAsset(..)`

>[!MORELIKETHIS]
* [Biblioteca](https://github.com/adobe/aem-upload)de upload de aem de código aberto.
* [Ferramenta](https://github.com/adobe/aio-cli-plugin-aem)de linha de comando de código aberto.


## Processamento de ativos e workflows pós-processamento {#post-processing-workflows}

No Experience Manager, o processamento de ativos é baseado na configuração de Perfis **[!UICONTROL de]** processamento que usa os [microserviços](asset-microservices-configure-and-use.md#get-started-using-asset-microservices)de ativos. O processamento não requer extensões de desenvolvedor.

Para a configuração do fluxo de trabalho de pós-processamento, use os workflows padrão com extensões com etapas personalizadas.

## Suporte às etapas do fluxo de trabalho no fluxo de trabalho de pós-processamento {#post-processing-workflows-steps}

Os clientes que atualizam para o Experience Manager como Cloud Service das versões anteriores do Experience Manager podem usar os microserviços de ativos para o processamento de ativos. Os microserviços de ativos nativos na nuvem são muito mais simples de configurar e usar. Algumas etapas do fluxo de trabalho usadas no fluxo de trabalho do Ativo [!UICONTROL de atualização do] DAM na versão anterior não são suportadas.

As etapas de fluxo de trabalho a seguir são suportadas no Experience Manager como um Cloud Service.

* `com.day.cq.dam.similaritysearch.internal.workflow.process.AutoTagAssetProcess`
* `com.day.cq.dam.core.impl.process.CreateAssetLanguageCopyProcess`
* `com.day.cq.wcm.workflow.process.CreateVersionProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.StartTrainingProcess`
* `com.day.cq.dam.similaritysearch.internal.workflow.smarttags.TransferTrainingDataProcess`
* `com.day.cq.dam.core.impl.process.TranslateAssetLanguageCopyProcess`
* `com.day.cq.dam.core.impl.process.UpdateAssetLanguageCopyProcess`
* `com.adobe.cq.workflow.replication.impl.ReplicationWorkflowProcess`
* `com.day.cq.dam.core.impl.process.DamUpdateAssetWorkflowCompletedProcess`

Os seguintes modelos de fluxo de trabalho técnico são substituídos por microserviços de ativos ou o suporte não está disponível.

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
