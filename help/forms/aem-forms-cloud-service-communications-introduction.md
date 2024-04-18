---
title: O que são as APIs de comunicação as a Cloud Service do Forms?
description: Use APIs de comunicação para assinar, certificar ou proteger seus documentos, automatizar processos de geração de PDF e converter documentos PDF para outro formato.
Keywords: How to generate document?, Generate PDF document, Manipulation PDF documents, Assembling PDF documents, Validating PDF document, APIs used in encrypting or decrypting PDFs.
feature: Adaptive Forms, APIs
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: 126af719cfd2c9361d0e7768b3b65e1149b6a989
workflow-type: tm+mt
source-wordcount: '1988'
ht-degree: 54%

---

# Introdução às Comunicações as a Cloud Service do AEM Forms {#frequently-asked-questions}


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html) |
| AEM as a Cloud Service | Este artigo |

O recurso de comunicações ajuda você a criar documentos aprovados pela marca, personalizados e padronizados, como correspondências comerciais, demonstrativos, cartas de processamento de solicitações, avisos de benefícios, contas mensais ou kits de boas-vindas.

O recurso fornece APIs para gerar e manipular os documentos. Você pode gerar ou manipular um documento por demanda ou criar uma tarefa em lote para gerar vários documentos em intervalos definidos. As APIs de comunicações fornecem:

* recursos simplificados de geração de documentação por demanda e em lote.

* capacidade de combinar, reorganizar e validar documentos PDF por demanda.

* APIs HTTP para facilitar a integração com sistemas externos. Estão incluídas APIs separadas para operações por demanda (baixa latência) e em lote (operações de alto rendimento).

* um acesso seguro aos dados. As APIs de comunicações se conectam e acessam somente dados de repositórios de dados designados pelo cliente, tornando as comunicações altamente seguras.

![Um exemplo de demonstrativo de cartão de crédito](assets/statement.png)
Um demonstrativo de cartão de crédito pode ser criado usando APIs de comunicações. Este demonstrativo de exemplo usa o mesmo modelo, mas dados separados para cada cliente, dependendo de seu uso do cartão de crédito.

## Geração de documentos

As APIs de geração de documentos de comunicações ajudam a combinar um modelo (XFA ou PDF) com dados do cliente (XML) para gerar documentos em formatos de PDF e impressão, como formatos PS, PCL, DPL, IPL e ZPL. Essas APIs utilizam modelos PDF e XFA com [Dados XML](communications-known-issues-limitations.md#form-data) para gerar um único documento por demanda ou vários documentos usando um trabalho em lote.

Normalmente, você cria um modelo usando o [Designer](use-forms-designer.md) e usa as APIs de comunicações para mesclar dados com o modelo. Seu aplicativo pode enviar o documento de saída para uma impressora de rede, uma impressora local ou para um sistema de armazenamento para arquivamento. Um fluxo de trabalho típico personalizado e pronto para uso é semelhante ao seguinte:

![Fluxo de trabalho de geração de documentos de comunicações](assets/communicaions-workflow.png)

Dependendo do caso de uso, também é possível disponibilizar esses documentos para download através do seu site ou de um servidor de armazenamento.

Alguns exemplos de APIs de geração de documentos são:

### Criar documentos PDF {#create-pdf-documents}

Você pode usar as APIs de geração de documentos para criar um documento PDF baseado em um design de formulário e dados de formulário XML. A saída é um documento PDF não interativo. Ou seja, os usuários não podem inserir ou modificar os dados do formulário. Um fluxo de trabalho básico é mesclar dados de formulário XML a um design de formulário para criar um documento PDF. A ilustração a seguir mostra a mesclagem de um design de formulário e dados de formulário XML para produzir um documento PDF.

![Criar documentos PDF](assets/outPutPDF_popup.png)
Figura: Fluxo de trabalho típico para criar um documento PDF

### Criar documento PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) {#create-PS-PCL-ZPL-documents}

Você pode usar APIs de geração de documentos para criar documentos PostScript (PS), Printer Command Language (PCL) e Zebra Printing Language (ZPL) baseados em um design de formulário XDP ou documento PDF. Essas APIs ajudam a mesclar um design de formulário com dados de formulário para gerar um documento. Você pode salvar o documento em um arquivo e desenvolver um processo personalizado para enviá-lo a uma impressora.

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that con tains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### Processamento de dados em lote para criar vários documentos {#processing-batch-data-to-create-multiple-documents}

Você pode usar APIs de geração de documentos para criar documentos separados para cada registro em uma fonte de dados em lote XML. Você pode gerar documentos em massa e em modo assíncrono. Você pode configurar vários parâmetros para a conversão e iniciar o processo em lote.

![Criar documentos PDF](assets/ou_OutputBatchMany_popup.png)

<!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. 

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use document generation APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form. -->

## Manipulação de documento

As APIs de manipulação de documentos de comunicação ajudam a combinar, reorganizar e validar documentos PDF. Normalmente, você cria um DDX e o envia para APIs de manipulação de documentos para montar ou reorganizar um documento. O [Documento DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) fornece instruções sobre como usar os documentos de origem para produzir um conjunto de documentos necessários. A documentação de referência DDX fornece informações detalhadas sobre todas as operações permitidas. Alguns exemplos de manipulação de documentos:

### Montar documentos PDF

Você pode usar as APIs de manipulação de documentos para montar dois ou mais documentos PDF ou XDP em um único documento PDF ou Portfólio de PDF. Estas são algumas das maneiras de montar documentos PDF:

* Montar um documento PDF simples
* Criar um Portifolio de PDF
* Compilar documentos criptografados
* Montar documentos usando a numeração de Bates
* Nivelar e reunir documentos

![Montagem de um documento PDF simples a partir de vários documentos de PDF](assets/as_document_assembly.png)
Figura: Montagem de um documento PDF simples a partir de vários documentos de PDF

### Desmontar documentos PDF

Você pode usar as APIs de manipulação de documentos para desmontar um documento do PDF. As APIs podem extrair páginas do documento de origem ou dividir um documento de origem com base em marcadores. Normalmente, essa tarefa é útil se o documento PDF foi criado originalmente de muitos documentos individuais, como uma coleção de declarações.

* Extrair páginas de um documento de origem
* Dividir um documento de origem com base em marcadores

![Dividir um documento de origem com base em marcadores de vários documentos](assets/as_intro_pdfsfrombookmarks.png)
Figura: Dividir um documento de origem com base em marcadores de vários documentos

### Converter e validar documentos compatíveis com PDF/A

Você pode usar as APIs de manipulação de documentos para converter um documento PDF em um documento compatível com PDF/A e determinar se um documento PDF é compatível com PDF/A. PDF/A é um formato de arquivo destinado à preservação do conteúdo do documento a longo prazo. As fontes são incorporadas no documento e o arquivo é descompactado. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Além disso, um documento PDF/A não contém conteúdo de áudio e vídeo.

>[!NOTE]
>
> O AEM Forms oferece uma variedade de fontes integradas que se integram perfeitamente com arquivos PDF. Para ver a lista de fontes suportadas, [clique aqui](/help/forms/supported-out-of-the-box-fonts.md).

<!-- 

## Document utilities

Document utilities synchronous APIs helps you convert documents between PDF and XDP file formats, and query information about a PDF document. For example, you can determine whether a PDF document contains comments or attachments. 

### Retrieve PDF document properties

You can [query a PDF document](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Extraction/) for the following information:

* Is a PDF Document: Check whether the source document is a PDF document.
* Is a fillable form: Check whether the source PDF document is a fillable form.
* Form Type: Retrieve the form type of the document.
* Check for Attachments: Check whether the source PDF document has any attachments.
* Check for Comments: Check whether the source PDF document has any review comments.
* Is a PDF Package: Check whether the document is a PDF package.
* Get the PDF Version: Retrieve the [version of the PDF document](https://en.wikipedia.org/wiki/History_of_PDF).
* Recommended Acrobat Version: Retrieve the required version of Acrobat (Reader) to open the PDF document.
* Is an XFA Document: Check whether the source PDF document is an XFA-based PDF document.
* Is Shell PDF: Check whether the source PDF document is shell PDF. A shell PDF contains only an XFA stream, font and image resources, and one page that is either blank or contains a warning that the document must be opened using Acrobat or Adobe Reader. The shell PDF is used with PDF transformation to optimize delivery of PDFForm transformations only.
* Get the XFA Version: Retrieve the [XFA Version for an XFA-based PDF document](https://en.wikipedia.org/wiki/XFA#XFA_versions).

### Convert PDF Documents into XDP Documents

The [PDF to XDP API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Conversion) converts a PDF document to an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the dictionary. -->

## Document Assurance {#doc-assurance}

O serviço DocAssurance inclui as APIs de Assinatura e Criptografia:

### APIs de assinatura

As APIs de assinatura permitem que sua organização proteja a segurança e a privacidade dos documentos do Adobe PDF que distribui e recebe. <!--This service uses digital signatures and certification to ensure that only intended recipients can alter documents. --> Os recursos de segurança são aplicados ao próprio documento; o documento permanece seguro e controlado durante todo o ciclo de vida. O documento permanece seguro além do firewall, quando é baixado offline e quando é enviado de volta à sua organização. Você pode realizar as seguintes tarefas usando as APIs de assinatura:

* Adicione um campo de assinatura visível a um documento PDF.
* Adicione um campo de assinatura invisível a um documento PDF.
* Assine o campo de assinatura especificado em um documento PDF.
* Certificar um documento PDF

### APIs de criptografia

As APIs de criptografia permitem criptografar e descriptografar documentos. Quando um documento é criptografado, seu conteúdo fica ilegível. Um usuário autorizado pode descriptografar o documento para obter acesso ao conteúdo. Se um documento PDF for criptografado com uma senha, o usuário deverá especificar a senha aberta para que o documento possa ser visualizado no Adobe Reader ou no Adobe Acrobat. <!-- Likewise, if a PDF document is encrypted with a certificate, the user must decrypt the PDF document with the public key that corresponds to the certificate (private key) that was used to encrypt the PDF document.-->

Você pode realizar essas tarefas usando as APIs de criptografia:

* Criptografar um documento PDF com uma senha.
* Remova a criptografia baseada em senha de um documento PDF.
* Recupere o tipo de segurança aplicada a um documento PDF.
* Retorne o tipo de segurança aplicado a um documento PDF.

As APIs de assinatura e as APIs de criptografia são [APIs síncronas](#types-of-communications-apis-types).

### APIs de direitos de uso

<span class="preview"> O recurso Direitos de uso está no Programa de adoção antecipada. Você pode escrever para aem-forms-ea@adobe.com a partir de sua ID de e-mail oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso. </span>

O recurso Direitos de uso permite que sua organização compartilhe facilmente documentos PDF interativos, estendendo a funcionalidade do Adobe Reader com direitos de uso adicionais. O serviço funciona com o Adobe Reader 7.0 ou posterior e adiciona direitos de uso a um documento PDF. Essa ação ativa recursos que geralmente não estão disponíveis quando um documento PDF é aberto usando o Adobe Reader, como adicionar comentários a um documento, preencher formulários e salvar o documento.

Quando os documentos PDF têm os direitos de uso apropriados adicionados, os recipients podem fazer as seguintes atividades no Adobe Reader:

* Preencha os documentos e formulários do PDF on-line ou off-line, permitindo que os recipients salvem cópias localmente para seus registros e ainda mantenham as informações adicionadas intactas.
* Salve os documentos de PDF em um disco rígido local para reter o documento original e quaisquer comentários, dados ou anexos adicionais.
* Anexe arquivos e clipes de mídia a documentos do PDF.
* Assine, certifique e autentique documentos PDF aplicando assinaturas digitais usando tecnologias de infraestrutura de chave pública (PKI) padrão do setor.
* Envie eletronicamente documentos de PDF concluídos ou anotados.
* Use documentos e formulários do PDF como um front-end de desenvolvimento intuitivo para bancos de dados internos e serviços da Web.
* Compartilhe documentos do PDF com outras pessoas para que os revisores possam adicionar comentários usando ferramentas de marcação intuitivas. Essas ferramentas incluem notas adesivas eletrônicas, carimbos, destaques e tachado de texto. As mesmas funções estão disponíveis no Acrobat.
* Suporte à decodificação Forms com código de barras.

Esses recursos de direitos de uso especiais são ativados automaticamente quando um documento de PDF habilitado para direitos é aberto no Adobe Reader. Quando o usuário terminar de trabalhar com um documento habilitado para direitos, essas funções serão novamente desabilitadas no Adobe Reader. Eles permanecem desativados até que o usuário receba outro documento PDF com direitos ativados.

#### Ativar ou desativar direitos de uso

Os vários recursos de direitos de uso para estender os serviços do PDF Reader são:

* **Decodificação de códigos de barras**: Para decodificar códigos de barras dentro do documento PDF.

* **Comentários**: Para comentar offline no documento PDF.

* **Comentários online**: Para comentar on-line no documento PDF.

* **Assinatura digital**: Para adicionar assinaturas digitais a um documento PDF.

* **Campos do formulário dinâmico**: para adicionar campos de formulário a um documento PDF.

* **Páginas do formulário dinâmico**: Para adicionar páginas de formulário a um documento PDF.

* **Arquivos incorporados**: Para incorporar arquivos em um documento PDF.

* **Importação de dados do formulário**: para importar dados de formulário para um documento PDF.

* **Exportação de dados do formulário**: para importar dados de formulário para um documento PDF.

* **Preenchimento de formulário**: para preencher campos de formulário em um documento PDF.

* **Forms Online**: para acessar um serviço Web ou banco de dados de um documento PDF.

* **Enviar autônomo**: para enviar dados de formulário off-line de um documento PDF.

#### Extrair direitos de uso

Ajuda a recuperar os direitos de uso ativados ou desativados em um documento do PDF para extensibilidade do Adobe Acrobat Reader.

#### Outros recursos

* **Mensagem**: a mensagem exibida no Adobe Acrobat Reader ao abrir um documento PDF com um ou mais direitos de uso aplicados.
* **Desbloquear senha**: A senha necessária para abrir um documento de PDF criptografado. Normalmente, essa é a senha para abrir o documento, mas se o documento PDF também estiver protegido por uma senha de permissões, ele poderá ser usado para abri-lo.

A variável [Documentação de referência da API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/) O fornece informações detalhadas sobre todos os parâmetros, métodos de autenticação e vários serviços fornecidos por APIs. A documentação de referência da API também está disponível no formato .yaml. Você pode baixar o arquivo .yaml e carregá-lo no Postman para verificar a funcionalidade das APIs.

## Tipos de APIs de Comunicação {#types}

As Comunicações fornecem APIs HTTP para geração de documentos sob demanda e em lote:

* **[APIs síncronas](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** são adequadas para cenários sob demanda, baixa latência e geração de documento de registro único. Essas APIs são mais adequadas para casos de uso baseados em ações do usuário. Por exemplo, gerar um documento depois que um usuário conclui o preenchimento de um formulário.

* **[APIs em lote (APIs assíncronas)](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** são adequadas para cenários programados, de alta taxa de transferência e de geração de vários documentos. Essas APIs geram documentos em lotes. Por exemplo, contas telefônicas, demonstrativos de cartão de crédito e demonstrativos de benefícios gerados todo mês.

## Integração

O recurso de Comunicações está disponível como um módulo independente e complementar para usuários do Forms as a Cloud Service. Você pode entrar em contato com a equipe de vendas da Adobe ou com seu representante da Adobe para solicitar acesso ao serviço. A Adobe habilita o acesso para sua organização e fornece os privilégios necessários à pessoa designada como administrador em sua organização. O administrador pode conceder acesso aos desenvolvedores do Forms as a Cloud Service (usuários) de sua organização para usar as APIs.

Após a integração, para ativar o recurso de Comunicações no ambiente do Forms as a Cloud Service:

1. Faça logon no Cloud Manager e abra a instância do AEM Forms as a Cloud Service.

1. Abra a opção Editar programa, vá para a guia Soluções e complementos e selecione a opção **[!UICONTROL Forms - Comunicações]**.

   ![Comunicações](assets/communications.png)

   Se você já tiver ativado a variável **[!UICONTROL Forms - Inscrição digital]**, selecione a opção **[!UICONTROL Forms - complemento Comunicações]**.

   ![Complementos](assets/add-on.png)

1. Clique em **[!UICONTROL Atualizar]**.

1. Execute o pipeline de build. Depois que o pipeline do build for bem-sucedido, as APIs de Comunicações são ativadas para o seu ambiente.

>[!NOTE]
>
> Para ativar e configurar APIs de manipulação de documentos, adicione a seguinte regra à [Configuração do Dispatcher](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service lets you generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

  * Generate documents by populating template files (PDF and XDP) with XML data.
  * Generate output forms in various formats, including non-interactive PDF print streams.

Consider a scenario where you have one or more templates and multiple records of XML data for each template. You can use Communications APIs to generate a print document for each record.  You can also combine the records into a single document.  The result is a non-interactive PDF document. A non-interactive PDF document does not let users enter data into its fields.

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as REST endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example, ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document.  

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

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on an XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->

## Consulte também {#see-also}

* [Processamento de comunicação - APIs síncronas](/help/forms/aem-forms-cloud-service-communications.md)
* [Processamento de comunicação - APIs em lote](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [Arquitetura as a Cloud Service do AEM Forms para APIs de Forms adaptável e comunicação](/help/forms/aem-forms-cloud-service-architecture.md)
