---
title: Uma introdução às Comunicações as a Cloud Service do Forms
description: Mesclar dados automaticamente com modelos XDP e PDF ou gerar saída nos formatos PCL, ZPL e PostScript
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: 0673aa4f2f0ad2f0a5205bf929de3f26aea0d879
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 1%

---

# Usar as comunicações as a Cloud Service do AEM Forms {#frequently-asked-questions}

**O recurso Comunicações as a Cloud Service do AEM Forms está em beta.**

O recurso de comunicações ajuda você a criar documentos orientados à marca, personalizados e padronizados, como correspondências comerciais, demonstrativos, cartas de processamento de solicitações, avisos de benefícios, contas mensais ou kits de boas-vindas.


Você pode gerar um documento sob demanda ou criar um trabalho em lote para gerar vários documentos em intervalos definidos. As APIs de comunicação fornecem:

* recursos de geração de documentação em lote e sob demanda simplificados

* fornecer APIs HTTP para facilitar a integração com sistemas existentes

* um acesso seguro aos dados. As APIs de comunicações se conectam e acessam somente dados de repositórios de dados designados pelo cliente, não fazem cópias locais de dados, tornando as Comunicações altamente seguras.

* APIs separadas para operações de baixa latência e alta throughput que tornam a geração de documentos uma tarefa eficiente.

![Um exemplo de demonstrativo de cartão de crédito](assets/statement.png)

## Como funciona?

Comunicações utilizam [Templates PDF e XFA](#supported-document-types) com [Dados XML](#form-data) para gerar um único documento sob demanda ou vários documentos usando um trabalho em lote em um intervalo definido.

Uma API de comunicações ajuda a combinar um modelo (XFA ou PDF) com os dados do cliente ([Dados XML](#form-data)) para gerar documentos em Formatos de PDF e impressão, como PS, PCL, DPL, IPL e ZPL.

Normalmente, você cria um modelo usando o Designer e usa as APIs de Comunicações para unir dados ao modelo. Seu aplicativo pode enviar o documento de saída para uma impressora de rede, uma impressora local ou para um sistema de armazenamento para arquivamento. Um fluxo de trabalho típico e personalizado é semelhante ao seguinte:

![Fluxo de trabalho de comunicações](assets/communicaions-workflow.png)

Dependendo do caso de uso, também é possível disponibilizar esses documentos para download através do seu site ou de um servidor de armazenamento.

## APIs de comunicação

As comunicações fornecem APIs HTTP para geração de documentos sob demanda e em lote:

* **APIs síncronas** são adequados para cenários sob demanda, baixa latência e geração de documento de registro único. Essas APIs são mais adequadas para casos de uso baseados em ações do usuário. Por exemplo, gerar um documento depois que um usuário conclui o preenchimento de um formulário.

* **APIs em lote (APIs assíncronas)** são adequados para cenários programados, de alta taxa de transferência e de geração de vários documentos. Essas APIs geram documentos em lotes. Por exemplo, contas telefônicas, demonstrativos de cartão de crédito e demonstrativos de benefícios gerados todo mês.

## Integração

As comunicações estão disponíveis como um módulo independente e complementar para o usuário as a Cloud Service do Forms. Você pode entrar em contato com a equipe de vendas do Adobe ou com seu representante de Adobe para solicitar acesso.

A Adobe habilita o acesso para sua organização e fornece os privilégios necessários à pessoa designada como administrador em sua organização. O administrador pode conceder acesso aos desenvolvedores (usuários) da AEM Forms de sua organização para usar as APIs.

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

## Considerações {#considerations-for-communications-apis}

Antes de começar a gerar documentos usando APIs de comunicação, analise as seguintes considerações:

### Dados do formulário {#form-data}

As APIs de comunicações aceitam um design de formulário que normalmente é criado no Designer e dados de formulário XML como entrada. Para preencher um documento com dados, um elemento XML deve existir nos dados do formulário XML para cada campo de formulário que você deseja preencher. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML é ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos. O fator importante é que os elementos XML são especificados com valores correspondentes.

Considere o seguinte exemplo de formulário de pedido de empréstimo:

![Formulário de pedido de empréstimo](assets/loanFormData.png)

Para unir dados neste design de formulário, crie uma fonte de dados XML que corresponda ao formulário. O XML a seguir representa uma fonte de dados XML que corresponde ao formulário de aplicativo de hipoteca de exemplo.

```XML
<?xml version="1.0" encoding="UTF-8" ?>
* <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
* <xfa:data>
* <data>
    * <Layer>
        <closeDate>1/26/2007</closeDate>
        <lastName>Johnson</lastName>
        <firstName>Jerry</firstName>
        <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
        <city>New York</city>
        <zipCode>00501</zipCode>
        <state>NY</state>
        <dateBirth>26/08/1973</dateBirth>
        <middleInitials>D</middleInitials>
        <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
        <phoneNumber>5555550000</phoneNumber>
    </Layer>
    * <Mortgage>
        <mortgageAmount>295000.00</mortgageAmount>
        <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
        <purchasePrice>300000</purchasePrice>
        <downPayment>5000</downPayment>
        <term>25</term>
        <interestRate>5.00</interestRate>
    </Mortgage>
</data>
</xfa:data>
</xfa:datasets>
```

### Tipos de documento suportados {#supported-document-types}

Para obter acesso completo aos recursos de renderização das APIs de Comunicação, é recomendável usar um arquivo XDP como entrada. Às vezes, um arquivo PDF pode ser usado. No entanto, usar um arquivo PDF como entrada tem as seguintes limitações:

Um documento PDF que não contém um fluxo XFA não pode ser renderizado como PostScript, PCL ou ZPL. As APIs de comunicações podem renderizar documentos PDF com fluxos XFA (ou seja, formulários criados no Designer) em formatos de laser e rótulo. Se o documento do PDF for assinado, certificado ou contiver direitos de uso (aplicados usando o serviço AEM Forms Reader Extensions), ele não poderá ser renderizado para esses formatos de impressão.

&lt;!-* * Opções de tempo de execução como PDF e PDF marcado não são suportadas para formulários Acrobat. Eles são válidos para PDF forms que contêm fluxos XFA; no entanto, esses formulários não podem ser assinados ou certificados.

### Suporte por email {#email-support}

Para obter a funcionalidade de email, você pode criar um processo em Fluxos de trabalho do Experience Manager que usa a Etapa de email. Um workflow representa um processo de negócios que você está automatizando. —>

### Áreas para impressão {#printable-areas}

A margem não imprimível padrão de 0,25 polegadas não é exata para impressoras de etiquetas e varia de impressora para impressora e do tamanho do rótulo para tamanho do rótulo. É recomendável manter a margem de 0,25 polegadas ou reduzi-la. No entanto, é recomendável não aumentar a margem não imprimível. Caso contrário, as informações na área de impressão não serão impressas corretamente.

Sempre verifique se você usa o arquivo XDC correto para a impressora. Por exemplo, evite escolher um arquivo XDC para uma impressora de 300 dpi e envie o documento para uma impressora de 200 dpi.

### Scripts {#scripts}

Um design de formulário usado com as APIs de comunicações pode conter scripts executados no servidor. Certifique-se de que um design de formulário não contenha scripts executados no cliente. Para obter informações sobre como criar scripts de design de formulário, consulte a Ajuda do Designer.

&lt;!-* #### Trabalhando com fontes Considerações do documento para Trabalhar com fontes>> —>

### Mapeamento de fonte {#font-mapping}

Para projetar um formulário que use fontes residentes na impressora, escolha um nome de fonte no Designer que corresponda às fontes disponíveis na impressora. Uma lista de fontes compatíveis com PCL ou PostScript está localizada nos perfis de dispositivo correspondentes (arquivos XDC). Como alternativa, o mapeamento de fontes pode ser criado para mapear fontes não residentes em impressoras para fontes residentes em impressoras de um nome de fonte diferente. Por exemplo, em um cenário PostScript, as referências à fonte Arial® podem ser mapeadas para a fonte Helvetica® residente na impressora.

Se uma fonte estiver instalada em um computador cliente, ela estará disponível na lista suspensa no Designer. Se a fonte não estiver instalada, é necessário especificar o nome da fonte manualmente. A opção &quot;Substituir permanentemente fontes indisponíveis&quot; no Designer pode estar desativada. Caso contrário, quando o arquivo XDP é salvo no Designer, o nome da fonte de substituição é gravado no arquivo XDP. Significa que a fonte residente na impressora não é usada.

Existem dois tipos de fontes OpenType®. Um tipo é uma fonte TrueType OpenType® compatível com PCL. O outro é o OpenType CFF®. A saída PDF e PostScript suporta fontes incorporadas Type-1, TrueType e OpenType®. A saída PCL suporta fontes TrueType incorporadas.

As fontes Tipo-1 e OpenType® não são incorporadas na saída PCL. O conteúdo formatado com fontes Tipo-1 e OpenType® é rasterizado e gerado como uma imagem de bitmap que pode ser grande e mais lenta para gerar.

Fontes baixadas ou incorporadas são substituídas automaticamente ao gerar saída PostScript, PCL ou PDF. Significa que apenas o subconjunto dos glifos de fonte necessários para renderizar corretamente o documento gerado é incluído na saída gerada.

### Trabalhar com arquivos de perfil de dispositivo (arquivo XDC) {#working-with-xdc-files}

Um perfil de dispositivo (arquivo XDC) é um arquivo de descrição de impressora no formato XML. Esse arquivo permite que as APIs de comunicações enviem documentos como formatos de impressora laser ou de etiqueta. As APIs de comunicações usam os arquivos XDC, incluindo o seguinte:

* hppcl5c.xdc

* hppcl5e.xdc

* ps_plain_level3.xdc

* ps_plain.xdc

* zpl300.xdc

* zpl600.xdc

* zpl300.xdc

* ipl300.xdc

* ipl400.xdc

* tpcl600.xdc

* dpl300.xdc

* dpl406.xdc

* dpl600.xdc

Você pode usar os arquivos XDC fornecidos para gerar documentos de impressão ou modificá-los de acordo com seu requisito.
&lt;!-* Não é necessário modificar esses arquivos para criar documentos. No entanto, você pode modificá-las para atender aos requisitos de sua empresa. —>

Esses arquivos são arquivos XDC de referência que oferecem suporte aos recursos de impressoras específicas, como fontes residentes, bandejas de papel e grampeador. A finalidade dessa referência é ajudar você a entender como configurar suas próprias impressoras usando perfis de dispositivo. As referências são também um ponto de partida para impressoras semelhantes na mesma linha de produtos.

### Trabalhar com o arquivo de configuração XCI {#working-with-xci-files}

As APIs de comunicações usam um arquivo de configuração XCI para executar tarefas, como controlar se a saída é um único painel ou paginada. Embora esse arquivo contenha configurações que podem ser definidas, não é normal modificar esse valor. &lt;!-* O arquivo default.xci está localizado na pasta svcdata\XMLFormService. —>

Você pode passar um arquivo XCI modificado usando uma API de comunicações. Ao fazer isso, crie uma cópia do arquivo padrão, altere somente os valores que exigem modificação para atender às suas necessidades de negócios e use o arquivo XCI modificado.

As APIs de comunicações começam com o arquivo XCI padrão (ou o arquivo modificado). Em seguida, ele aplica valores especificados pelas APIs de comunicações. Esses valores substituem as configurações XCI.

A tabela a seguir especifica as opções de XCI.

| Opção XCI | Descrição |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config/presente/pdf/criador | Identifica o criador do documento usando a entrada Creator no dicionário Informações do documento. Para obter informações sobre este dicionário, consulte o Guia de referência de PDF. |
| config/presente/pdf/produtor | Identifica o produtor do documento utilizando a menção Produtor no dicionário Informações do Documento. Para obter informações sobre este dicionário, consulte o Guia de referência de PDF. |
| configuração/presente/layout | Controla se a saída é um único painel ou paginado. |
| config/presente/pdf/compression/level | Especifica o grau de compactação a ser usado ao gerar um documento PDF. |
| config/present/pdf/scriptModel | Controla se informações específicas de XFA são incluídas no documento PDF de saída. |
| config/present/common/data/adaptData | Controla se o aplicativo XFA ajusta os dados após a mesclagem. |
| config/present/pdf/renderPolicy | Controla se a geração de conteúdo da página é feita no servidor ou adiada para o cliente. |
| config/present/common/locale | Especifica o local padrão usado no documento de saída. |
| config/presente/destino | Quando contido por um elemento presente, especifica o formato de saída. Quando contido por um elemento openAction , especifica a ação a ser executada ao abrir o documento em um cliente interativo. |
| config/present/output/type | Especifica o tipo de compactação a ser aplicado a um arquivo ou o tipo de saída a ser produzido. |
| config/presente/common/temp/uri | Especifica o URI do formulário. |
| config/presente/common/template/base | Fornece um local básico para URIs no design de formulário. Quando esse elemento está ausente ou vazio, o local do design de formulário é usado como base. |
| config/presente/common/log/to | Controla o local onde os dados de log ou de saída são gravados. |
| config/present/output/to | Controla o local onde os dados de log ou de saída são gravados. |
| config/present/script/currentPage | Especifica a página inicial quando o documento é aberto. |
| config/present/script/exclude | Informa às APIs do AEM Forms server/Communications quais eventos devem ser ignorados. |
| config/presente/pdf/linearized | Controla se o documento PDF de saída é linearizado. |
| config/present/script/runScripts | Controla qual conjunto de scripts é executado pelo AEM Forms. |
| config/present/pdf/tagged | Controla a inclusão de tags no documento PDF de saída. As tags, no contexto do PDF, são informações adicionais incluídas em um documento para expor a estrutura lógica do documento. As tags ajudam a acessibilidade e a reformatação. Por exemplo, um número de página pode ser marcado como um artefato, de modo que um leitor de tela não o enuncie no meio do texto. Embora as tags tornem um documento mais útil, elas também aumentam o tamanho do documento e o tempo de processamento para criá-lo. |
| config/presente/pdf/version | Especifica a versão do documento PDF a ser gerado. |
