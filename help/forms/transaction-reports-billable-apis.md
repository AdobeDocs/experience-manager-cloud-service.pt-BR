---
title: APIs de relatórios de transação faturáveis
description: Lista de todas as APIs contabilizadas como transações
feature: Adaptive Forms, Foundation Components
hide: true
hidefromtoc: true
source-git-commit: a1a87a27d73d7472ec02de37621123bbdd3876b4
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 4%

---

# APIs de relatórios de transação faturáveis {#transaction-reports-billable-apis}

O AEM Forms fornece várias APIs para enviar formulários, processar documentos e renderizar documentos. Algumas APIs são contabilizadas como transações e outras são livres para uso. Este documento fornece uma lista de todas as APIs que são contabilizadas como transações em um relatório de transações. Estes são alguns cenários comuns em que uma API faturável é usada:

* Envio de um formulário adaptável
* Conversão de um documento de um formato para outro
* Nivelamento de um documento PDF dinâmico
* Gerar um documento de registro (usando o serviço do Forms ou o serviço de saída)
* Mesclar um documento PDF interativo com outro documento PDF
* Usando a etapa atribuir tarefa e as etapas API de comunicação de fluxos de trabalho AEM

As APIs de faturamento não levam em conta o número de páginas, o comprimento de um documento ou formulário ou o formato final do documento renderizado. Um relatório de transações divide as transações em duas categorias: Forms Submetido e Documentos Renderizados.

* **Forms enviado:** Quando os dados são enviados de qualquer tipo de formulário criado com o AEM Forms e os dados são enviados para qualquer repositório ou banco de dados de armazenamento de dados, é considerado o envio do formulário. Por exemplo, o envio de um formulário adaptável ou de um conjunto de formulários é considerado um formulário enviado. Se um conjunto de formulários tiver cinco formulários e quando o conjunto for enviado, o serviço de relatório de transações o contará como cinco envios.

* **Documentos renderizados:** Gerar um documento combinando um modelo e dados, assinando ou certificando digitalmente um documento, usando APIs de serviços de documento faturáveis para serviços de documento ou convertendo um documento de um formato para outro são considerados documentos renderizados.

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_submission_graph_en"
>title="Rastreador de envios de formulários"
>abstract="Rastreie facilmente os envios de formulários com uma exibição consolidada para contagens totais ou mergulhe em detalhes específicos da instância. Use o gráfico de barras intuitivo para identificar tendências, comparar instâncias e tomar decisões informadas rapidamente."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_conversions_graph_en"
>title="Rastreador de conversões de formulário"
>abstract="Mantenha guias sobre as conversões de formulários facilmente por meio de um resumo das contagens totais ou explore os detalhes de cada instância do AEM Forms. O gráfico de barras de fácil leitura ajuda a detectar tendências, comparar instâncias e tomar decisões rápidas e conscientes."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formCreationAvgDuration_graph_en"
>title="Duração média para geração de formulário"
>abstract="O gráfico ilustra o tempo médio necessário para criar um formulário. Cada barra no gráfico representa um formulário específico, e a altura da barra indica a duração média da criação do formulário durante esse período. A análise deste gráfico ajuda os usuários a entender a eficiência e a velocidade da criação de formulários em diferentes períodos ou em diferentes contextos, permitindo insights sobre possíveis melhorias."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formPublishAvgDuration_en"
>title="Duração média para criação de formulário"
>abstract="O gráfico exibe o tempo médio necessário para criar e publicar um formulário, medido a partir do dia inicial em que o formulário foi aberto para edição. Cada barra corresponde a um intervalo de tempo específico para um formulário, com a altura da barra indicando o tempo médio desde o início do desenvolvimento do formulário até sua finalização e publicação."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_newForms_graph_en"
>title="Novo Forms Tracker"
>abstract="O gráfico fornece informações sobre o número ou a frequência de formulários recém-criados durante períodos específicos. Cada barra no gráfico representa uma unidade distinta de medida, como dias, semanas ou meses. A altura de cada barra indica a quantidade ou a frequência dos novos formulários criados durante esse intervalo específico."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_publishedForms_graph_en"
>title="Rastreador do Forms publicado"
>abstract="O gráfico fornece informações sobre o número ou a frequência de formulários publicados com êxito durante períodos específicos. Isso permite entender as tendências, padrões ou variações na publicação de formulários ao longo do tempo, auxiliando no monitoramento da produtividade, identificando períodos de pico de publicação ou avaliando o sucesso das alterações no processo de publicação do formulário."

<!-- 
>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formFragments_graph_en"
>title="Form Fragments Tracker"
>abstract="This graph helps you see how many form fragments people use in their forms. It gives you a sense of how popular or common these reusable parts are in form building."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_avgFormPerFragments_graph_en"
>title="Average Duration for Form Fragments Creation"
>abstract= "The graph displays the average time taken to create a form fragment, measured from the initial day the form fragment was opened for editing. Each bar corresponds to a specific time frame for a form fragment, with the bar height indicating the average time taken from the start of form fragment development to its finalization and publication."


<!-- 

>[!NOTE]
>
>Transaction Reports UI displays three categories: Forms Submitted, Documents Rendered, and Documents Processed. Both Documents Rendered and Documents Processed are accounted as Documents Rendered.
-->


<!--

## Billable Document Services APIs {#billable-document-services-apis}

### Generate PDF Service {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Distiller Service {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## APIs de serviços de documento faturáveis {#billable-document-services-apis}

### Gerar serviço de PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#section/Before-you-start" target="_blank">createPDF</a></td>
   <td>Gera um documento PDF a partir de um modelo e mescla os dados a ele.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePrintedOutput/post" target="_blank">exportPDF</a></td>
   <td>Converte arquivo XDP ou documento PDF em tipos de arquivos compatíveis.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

### Serviço de saída {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutput" target="_blank">generatePDFOutput</a></td>
   <td>Mescla dados e modelos para criar um documento PDF.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutputOptions" target="_blank">generatePDFOutput (PDFOutputOptions)</a></td>
   <td>Mescla dados e modelos para criar um documento PDF.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePDFOutputBatch</a></td>
   <td>Mescla dados e modelos para criar um conjunto de documentos PDF.</td>
   <td>Documentos processados</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutput" target="_blank">generatePrintedOutput</a></td>
   <td>Converte documentos XDP e PDF em formatos de arquivo PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions" target="_blank">generatePrintedOutput (OpçõesDeSaídaImpressas)</a></td>
   <td>Converte documentos XDP e PDF em formatos de arquivo PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Converte um conjunto de documentos XDP e PDF em um conjunto de formatos de arquivo PostScript (PS), Printer Command Language (PCL) e ZPL. </td>
   <td>Documentos processados</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
 </tbody>
</table>

### Serviço DocAssurance {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/docassurance/#tag/DocAssurance" target="_blank">secureDocument</a><br /> </td>
   <td>Essa API permite que você proteja seu documento. Você pode usar a API para assinar, certificar, estender o leitor ou criptografar um documento PDF.</td>
   <td>Documentos processados</td>
   <td>Somente assinar e certificar a operação do secureDocument são cobrados.</td>
  </tr>
 </tbody>
</table>

### Serviço de documento de registro (DOR) {#document-of-record-dor-forms-service-and-output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://opensource.adobe.com/aem-forms-af-runtime/api/#tag/Generate-DoR/operation/generateDoR" target="_blank">renderizar</a></td>
   <td>Chama o método de renderização especificado para gerar um documento de registro usando os parâmetros fornecidos.</td>
   <td>Documentos processados usando o serviço do Forms</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed using Output Service</td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

<!--

### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Convert PDF Service {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Converts a PDF document to a list of image documents. Supported image formats are JPEG, JPEG2K, PNG, and TIFF.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Converts a Flat PDF file to PostScript format using the options specified in the option spec.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Barcoded Forms Service {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
   <td>Decodes all the barcodes in a Document object and returns an org.w3c.dom.Document object that contains data that was retrieved from the barcode.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

### Serviço de Assembler {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX">invocar</a></td>
   <td>Executa o DDX nos documentos de entrada fornecidos e retorna um objeto contendo os documentos resultantes</td>
   <td>Documentos processados</td>
   <td>As seguintes operações não são contabilizadas como transações:
    <ul>
     <li>Criação de pacotes ou portfólio</li>
     <li>Compilação de vários XDPs </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX" target="_blank">invocar</a></td>
   <td>Executa o DDX nos documentos de entrada fornecidos e retorna um objeto contendo os documentos resultantes</td>
   <td>Documentos processados</td>
   <td>Todos os formatos de arquivo de entrada compatíveis com os serviços PDF Generator, Forms e Output, o serviço Assembler é compatível com todos esses formatos como formatos de arquivo de saída. </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA">toPDFA</a></td>
   <td>Converta um documento especificado em PDF/A usando as opções especificadas.</td>
   <td>Documentos processados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

O uso da API de chamada é contado como uma transação, quando você executa uma ou mais das seguintes operações:

1. Conversão de formatos sem PDF para formatos PDF. <!--For instance, the conversion from XDP format to PDF format, catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. Conversão do formato PDF para o formato PDF/A.
1. Conversão do formato PDF para formatos não PDF. Os exemplos englobam a transformação do formato PDF para o formato Imagem ou a conversão do formato PDF para Texto.


>[!NOTE]
>
>* A API de chamada do serviço do montador pode chamar internamente uma API faturável de outro serviço, dependendo da entrada. Portanto, a API invoke pode ser contabilizada como nenhuma, uma única ou várias transações. O número de transações contadas depende da entrada e das APIs internas chamadas.
>* Um único documento de PDF produzido usando o serviço de montagem pode ser contabilizado como nenhuma, uma única ou várias transações. O número de transações contadas depende do código fornecido.
>

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. In order for a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## APIs de captura de dados faturáveis {#billable-data-capture-apis}

Todos os eventos de envio de formulários adaptáveis são contabilizados como transações. Por padrão, o envio de um Formulário de PDF não é contabilizado como uma transação. Usar o fornecido [API do gravador de transações](record-transaction-custom-implementation.md) para registrar um envio de PDF forms como uma transação.

### Adaptive Forms {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Descrição</td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Envio de um formulário adaptável</td>
   <td>Envia um formulário adaptável para a ação de envio configurada. </td>
   <td>Formulários enviados</td>
   <td>
    <ul>
     <li>Os envios bem-sucedidos levam em conta uma ou duas transações. O número de transações contadas depende do tipo de ação de envio usado para envio. Por exemplo, o envio de PDF por meio de ações de envio de email contabiliza duas contagens de transações. Uma transação para envio de formulário e outra para PDF gerado usando o serviço de Documento de registro (DOR). </li>
     <li>O uso do formulário adaptável em um formulário adaptável (conjunto de formulários de formulário adaptável) contabiliza apenas uma transação. É possível ter qualquer número de formulários adaptáveis em um formulário adaptável.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

<!--

### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Form set {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting a form set</td>
   <td>Submits form set to the submit URL configured in the form set.</td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
     <li>Every form in an HTML5 Forms form set accounts as a separate transaction. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

## Fluxos de trabalho do AEM faturáveis centrados no formulário {#billable--form-centric-aem-workflows}

As etapas Atribuir tarefa e serviços de documento dos Fluxos de trabalho do AEM centrados no formulário são contabilizadas como transações. Se uma etapa do fluxo de trabalho contabilizar uma transação e o fluxo de trabalho não for concluído, a contagem da transação não será revertida.

<!--
Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.
-->


<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->

### Fluxos de trabalho do AEM centrados em formulários {#form-centric-aem-workflows}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Categoria do relatório de transações</td>
   <td>Informações adicionais</td>
  </tr>
  <tr>
   <td>Submetendo uma etapa Atribuir Tarefa</td>
   <td>Formulários enviados</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Envio de um ponto de partida de aplicativo de fluxo de trabalho </td>
   <td>Formulários enviados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Registrando APIs faturáveis como transações para código personalizado {#recording-billable-apis-as-transactions-for-custom-code}

Ações como enviar um Formulário PDF, usar a interface do usuário do agente para visualizar uma comunicação interativa, usar o envio de formulários não padrão e implementações personalizadas não são contabilizadas como transações. O AEM Forms fornece uma API para registrar ações como transações. Você pode chamar a API de suas implementações personalizadas para [registrar uma transação](/help/forms/record-transaction-custom-implementation.md).

## Artigos relacionados {#related-articles}

* [Registrar uma transação para implementações personalizadas](/help/forms/record-transaction-custom-implementation.md)
