---
title: Uma introdução às Comunicações as a Cloud Service do Forms
description: Mesclar dados automaticamente com modelos XDP e PDF ou gerar saída nos formatos PCL, ZPL e PostScript
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: 22018450f6d4383f3df6a9f5382a0ad6b4058480
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 2%

---

# Usar as comunicações as a Cloud Service do AEM Forms {#frequently-asked-questions}

O recurso de comunicações ajuda você a criar documentos aprovados pela marca, personalizados e padronizados, como correspondências comerciais, demonstrativos, cartas de processamento de solicitações, avisos de benefícios, contas mensais ou kits de boas-vindas.

O recurso fornece APIs para gerar e manipular os documentos. Você pode gerar ou manipular um documento sob demanda ou criar um trabalho em lote para gerar vários documentos em intervalos definidos. As APIs de comunicações fornecem:

* recursos simplificados de geração de documentação sob demanda e em lote.

* capacidade de combinar, reorganizar e validar documentos PDF sob demanda.

* APIs HTTP para facilitar a integração com sistemas externos. Estão incluídas APIs separadas para operações sob demanda (baixa latência) e em lote (operações de alta throughput).

* um acesso seguro aos dados. As APIs de comunicações se conectam e acessam somente dados de repositórios de dados designados pelo cliente, tornando as Comunicações altamente seguras.

![Um exemplo de demonstrativo de cartão de crédito](assets/statement.png)
Uma declaração de cartão de crédito pode ser criada usando APIs de comunicações. Esta declaração de exemplo usa o mesmo modelo, mas dados separados para cada cliente, dependendo de seu uso do cartão de crédito.

## Geração de documentos

As APIs de geração de documentos de comunicações ajudam a combinar um modelo (XFA ou PDF) com dados do cliente (XML) para gerar documentos em Formatos de PDF e impressão, como formatos PS, PCL, DPL, IPL e ZPL. Essas APIs utilizam modelos PDF e XFA com [Dados XML](communications-known-issues-limitations.md#form-data) para gerar um único documento sob demanda ou vários documentos usando um trabalho em lote.

Normalmente, você cria um modelo usando [Designer](use-forms-designer.md) e use as APIs de comunicações para mesclar dados com o modelo. Seu aplicativo pode enviar o documento de saída para uma impressora de rede, uma impressora local ou para um sistema de armazenamento para arquivamento. Um fluxo de trabalho típico e personalizado é semelhante ao seguinte:

![Fluxo de trabalho de geração de documentos de comunicações](assets/communicaions-workflow.png)

Dependendo do caso de uso, também é possível disponibilizar esses documentos para download através do seu site ou de um servidor de armazenamento.

Alguns exemplos de APIs de geração de documentos são:

### Criar documentos PDF {#create-pdf-documents}

Você pode usar as APIs de geração de documentos para criar um documento PDF baseado em um design de formulário e dados de formulário XML. A saída é um documento PDF não interativo. Ou seja, os usuários não podem inserir ou modificar os dados do formulário. Um fluxo de trabalho básico é unir dados de formulário XML a um design de formulário para criar um documento PDF. A ilustração a seguir mostra a mesclagem de um design de formulário e dados de formulário XML para produzir um documento PDF.

![Criar documentos PDF](assets/outPutPDF_popup.png)
Figura: Fluxo de trabalho típico para criar um documento PDF

### Criar documento PostScript (PS), PCL (Printer Command Language), ZPL (Zebra Printing Language) {#create-PS-PCL-ZPL-documents}

Você pode usar APIs de geração de documentos para criar documentos PostScript (PS), PCL (Printer Command Language) e ZPL (Zebra Printing Language) baseados em um design de formulário XDP ou documento PDF. Essas APIs ajudam a mesclar um design de formulário com dados de formulário para gerar um documento. Você pode salvar o documento em um arquivo e desenvolver um processo personalizado para enviá-lo a uma impressora.

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that con tains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### Processamento de dados em lote para criar vários documentos {#processing-batch-data-to-create-multiple-documents}

Você pode usar APIs de geração de documentos para criar documentos separados para cada registro em uma fonte de dados em lote XML. Você pode gerar documentos em massa e em modo assíncrono. Você pode configurar vários parâmetros para a conversão e iniciar o processo em lote.

![Criar documentos PDF](assets/ou_OutputBatchMany_popup.png)

<!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. 

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use document generation APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document’s fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form. -->

## Manipulação de documento

As APIs de manipulação de documentos de comunicações ajudam a combinar, reorganizar e validar documentos do PDF. Normalmente, você cria um DDX e o envia para APIs de manipulação de documentos para montar ou reorganizar um documento. O [Documento DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) O fornece instruções sobre como usar os documentos de origem para produzir um conjunto de documentos necessários. A documentação de referência DDX fornece informações detalhadas sobre todas as operações suportadas. Alguns exemplos de manipulação de documentos são:

### Montar documentos PDF

Você pode usar as APIs de manipulação de documentos para montar dois ou mais documentos PDF ou XDP em um único documento PDF ou Portfolio PDF. Estas são algumas das maneiras de montar documentos do PDF:

* Montar um documento PDF simples
* Criar um Portfolio de PDF
* Compilar documentos criptografados
* Montar documentos usando a numeração de Bates
* Nivelar e reunir documentos

![Montagem de um documento PDF simples a partir de vários documentos de PDF](assets/as_document_assembly.png)
Figura: Montagem de um documento PDF simples a partir de vários documentos de PDF

### Desmontar documentos PDF

Você pode usar as APIs de manipulação de documentos para desmontar um documento do PDF. As APIs podem extrair páginas do documento de origem ou dividir um documento de origem com base em marcadores. Normalmente, essa tarefa é útil se o documento PDF foi criado originalmente de muitos documentos individuais, como uma coleção de declarações.

* Extrair páginas de um documento de origem
* Dividir um documento de origem com base em marcadores

![Dividir um documento de origem com base em marcadores em vários documentos](assets/as_intro_pdfsfrombookmarks.png)
Figura: Dividir um documento de origem com base em marcadores em vários documentos

### Converter e validar documentos PDF e de conformidade

Você pode usar as APIs de manipulação de documentos para converter um documento PDF em um documento compatível com PDF/A e determinar se um documento PDF é compatível com PDF/A. PDF/A é um formato de arquivo destinado à preservação de longo prazo do conteúdo do documento. As fontes são incorporadas no documento e o arquivo é descompactado. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo.

## Tipos de APIs de comunicação

As comunicações fornecem APIs HTTP para geração de documentos sob demanda e em lote:

* **[APIs síncronas](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/)** são adequados para cenários sob demanda, baixa latência e geração de documento de registro único. Essas APIs são mais adequadas para casos de uso baseados em ações do usuário. Por exemplo, gerar um documento depois que um usuário conclui o preenchimento de um formulário.

* **[APIs em lote (APIs assíncronas)](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/)** são adequados para cenários programados, de alta taxa de transferência e de geração de vários documentos. Essas APIs geram documentos em lotes. Por exemplo, contas telefônicas, demonstrativos de cartão de crédito e demonstrativos de benefícios gerados todo mês.

## Integração

O recurso de comunicações está disponível como um módulo independente e complementar para usuários as a Cloud Service da Forms. Você pode entrar em contato com a equipe de vendas do Adobe ou com seu representante de Adobe para solicitar acesso. A Adobe habilita o acesso para sua organização e fornece os privilégios necessários à pessoa designada como administrador em sua organização. O administrador pode conceder acesso aos desenvolvedores as a Cloud Service (usuários) da Forms de sua organização para usar as APIs.

Após a integração, para ativar o recurso de Comunicações no ambiente as a Cloud Service do Forms:

1. Faça logon no Cloud Manager e abra a instância do AEM Forms as a Cloud Service.

1. Abra a opção Editar programa , vá para a guia Soluções e complementos e selecione o **[!UICONTROL Forms - Comunicações]** opção.

   ![Comunicações](assets/communications.png)

   Se você já tiver ativado a variável **[!UICONTROL Forms - Inscrição digital]** , em seguida, selecione a **[!UICONTROL Forms - Suplemento de comunicações]** opção.

   ![Addon](assets/add-on.png)

1. Clique em **[!UICONTROL Atualizar]**.

1. Execute o pipeline de build. Depois que o pipeline de criação for bem-sucedido, as APIs de comunicações serão ativadas para seu ambiente.

>[!NOTE]
>
> Para ativar e configurar APIs de manipulação de documentos, adicione a seguinte regra a [Configuração do Dispatcher](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service allows you to generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

  * Generate documents by populating template files (PDF and XDP) with XML data.
  * Generate output forms in various formats, including non-interactive PDF print streams.

Consider a scenario where you have one or more templates and multiple records of XML data for each template. You can use Communications APIs to generate a print document for each record.  You can also combine the records into a single document.  The result is a non-interactive PDF document. A non-interactive PDF document does not let users enter data into its fields.

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as REST endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document.  

The [API reference documentation](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) provides detailed information about all the parameters, authentication methods, and various services provided by APIs. The API reference documentation is also available in the .yaml format. You can download the .yaml for [Batch APIs](assets/batch-api.yaml) or [non-Batch API.yaml](assets/non-batch-api.yaml) file and upload it to postman to check functionality of APIs.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

Uploading Communication APIs .yaml file to postman to check functionality of APIs.

## Using the Communications APIs {#workflows}

Typically, you create a template using [Designer](use-forms-designer.md) and use communications APIs ( generatePDFOutput and generatePrintedOutput) to:

* Convert these templates to various formats, including PDF, PostScript, ZPL, and PCL.
* Merge XML form data with a form design to generate a document.
* Generate a document without merging XML form data into the document. However, the primary workflow is merging data into the document.

Then, the output document is stored to a file. You can design custom workflows to send the file to a network printer, a local printer, or to a storage system for archival. A typical out of the box and custom workflows look like the following:

![Communications Workflow](assets/communicaions-workflow.png)

### Create PDF documents {#create-pdf-documents}

You can use the _generatePDFOutput_ API to create PDF document that is based on a form design and XML form data. The output is a non-interactive PDF document. That is, users cannot enter or modify form data. A basic workflow is to merge XML form data with a form design to create a PDF document. The following illustration shows the merging of a form design and XML form data to produce a PDF document.

![Create PDF Documents](assets/outPutPDF_popup.png)

### Create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) document {#create-PS-PCL-ZPL-documents}

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on a XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document’s fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->
