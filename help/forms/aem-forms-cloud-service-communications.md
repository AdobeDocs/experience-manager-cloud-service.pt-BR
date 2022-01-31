---
title: AEM Forms as a Cloud Service - Comunicações
description: Mesclar dados automaticamente com modelos XDP e PDF ou gerar saída nos formatos PCL, ZPL e PostScript
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: ed46b0be25dabcea69be29e54000a4eab55e2836
workflow-type: tm+mt
source-wordcount: '2250'
ht-degree: 0%

---


# Usar APIs de comunicações as a Cloud Service do AEM Forms {#frequently-asked-questions}

**O recurso Comunicações está em beta.**

As APIs de comunicações ajudam a combinar modelos XDP, documentos PDF baseados em XDP e Acrobat Forms (AcroForm) com dados XML para gerar documentos impressos em vários formatos e permitir que você crie aplicativos que permitem:

- Gere documentos preenchendo arquivos de modelo com dados XML.

- Gere formulários em vários formatos, incluindo fluxos de PDF não interativos.

- Gere PDF de impressão a partir de PDF de formulário XFA.

- Gere documentos PDF, PostScript, PCL e ZPL em massa ao mesclar vários conjuntos de dados com modelos de origem.

Considere um cenário em que você tem um ou mais modelos e vários registros de dados XML para cada modelo. Você pode usar as APIs de comunicações para gerar um documento de impressão para cada registro. <!-- You can also combine the records into a single document. --> O resultado é um documento PDF não interativo. Um documento PDF não interativo não permite que os usuários insiram dados em seus campos.

O [Documentação de referência da API](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) O fornece informações detalhadas sobre todas as APIs, parâmetros, métodos de autenticação e vários serviços fornecidos pelas APIs. A documentação de referência da API também está disponível no formato .yaml. Você pode baixar o .yaml para [APIs em lote](assets/batch-api.yaml) ou [API.yaml não em lote](assets/non-batch-api.yaml) e faça upload no postman para verificar a funcionalidade de APIs.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

Upload do arquivo .yaml das APIs de comunicação no postman para verificar a funcionalidade das APIs.

>[!NOTE]
>
>Somente membros do grupo forms-users podem acessar APIs de comunicações.

## Ativar comunicações

Para ativar as Comunicações no seu ambiente as a Cloud Service do Forms:

1. Faça logon no Cloud Manager e abra a instância as a Cloud Service do AEM Forms.

1. Abra a opção Editar programa , vá para a guia Soluções e complementos e selecione o **[!UICONTROL Forms - Comunicações]** opção.

   <!-- ![Communications](assets\communications.png)

    If you have already enabled the **[!UICONTROL Forms - Digital Enrollment]** option, then select the **[!UICONTROL Forms - Communications Add-On]** option.  

    <!-- ![Addon](assets\add-on.png) -->

1. Clique em **[!UICONTROL Atualizar]**.

1. Execute o pipeline de build.

Depois que a pipeline de criação for bem-sucedida, as APIs de comunicação serão ativadas para seu ambiente.

## Uso das APIs de comunicações {#workflows}

Normalmente, você cria um modelo usando [Designer](use-forms-designer.md) e usar APIs de comunicações para:

- Converta esses modelos em vários formatos, incluindo PDF, PostScript, ZPL e PCL.
- Mesclar dados de formulário XML com um design de formulário para gerar um documento.
- Gere um documento sem mesclar dados de formulário XML no documento. No entanto, o fluxo de trabalho principal está mesclando dados no documento.

Em seguida, o documento de saída é armazenado em um arquivo. Você pode criar fluxos de trabalho personalizados para enviar o arquivo para uma impressora de rede, uma impressora local ou para um sistema de armazenamento para arquivamento. Um fluxo de trabalho típico e personalizado é semelhante ao seguinte:

![Fluxo de trabalho de comunicações](assets/communicaions-workflow.png)

### Criar documentos PDF {#create-pdf-documents}

Você pode usar o _generatePDFOutput_ API para criar um documento PDF baseado em um design de formulário e em dados de formulário XML. A saída é um documento PDF não interativo. Ou seja, os usuários não podem inserir ou modificar dados de formulário. Um fluxo de trabalho básico é unir dados de formulário XML a um design de formulário para criar um documento PDF. A ilustração a seguir mostra a união de um design de formulário e dados de formulário XML para produzir um documento PDF.

![Criar documentos PDF](assets/outPutPDF_popup.png)

### Criar documento PostScript (PS), PCL (Printer Command Language), ZPL (Zebra Printing Language) {#create-PS-PCL-ZPL-documents}

Você pode usar as APIs de Comunicações para criar o documento PostScript (PS), PCL (Printer Command Language) e ZPL (Zebra Printing Language) que são baseados em um design de formulário XDP ou documento PDF. O _generatePrintedOutput_ A API mescla um design de formulário com dados de formulário para gerar um documento. Você pode salvar o documento em um arquivo e desenvolver um processo personalizado para enviá-lo a uma impressora.

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### Processamento de dados em lote para criar vários documentos {#processing-batch-data-to-create-multiple-documents}

Você pode criar documentos separados para cada registro dentro de uma fonte de dados em lote XML. Você pode gerar documentos em massa e em modo assíncrono. Você pode configurar vários parâmetros para a conversão e iniciar o processo em lote. <!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. -->

### Nivelar documentos interativos do PDF {#flatten-interactive-pdf-documents}

Você pode usar as APIs de comunicações para transformar um documento PDF interativo (por exemplo, um formulário) em um documento PDF não interativo. Um documento PDF interativo permite que os usuários insiram ou modifiquem dados localizados nos campos do documento PDF. O processo de transformação de um documento PDF interativo em um documento PDF não interativo é chamado de nivelamento. Quando um documento PDF é nivelado, um usuário não pode modificar os dados localizados nos campos do documento. Um motivo para nivelar um documento PDF é garantir que os dados não possam ser modificados.

Você pode nivelar os seguintes tipos de documentos PDF:

- Documentos de PDF interativos criados no Designer (que contêm fluxos XFA).

- Acrobat PDF forms

Se você tentar nivelar um documento PDF não interativo, ocorrerá uma exceção.

### Manter Estado do Formulário {#retain-form-state}

Um documento PDF interativo contém vários elementos que constituem um formulário. Esses elementos podem incluir campos (para aceitar ou exibir dados), botões (para acionar eventos) e scripts (comandos para executar uma ação específica). Clicar em um botão pode acionar um evento que altera o estado de um campo. Por exemplo, escolher uma opção de gênero pode alterar a cor de um campo ou a aparência do formulário. Este é um exemplo de um evento manual que faz com que o estado do formulário mude.

Quando esse documento PDF interativo é nivelado usando as APIs de Comunicação, o estado do formulário não é mantido. Para garantir que o estado do formulário seja mantido mesmo depois que o formulário for achatado, defina o valor booleano _keepFormState_ como Verdadeiro para salvar e manter o estado do formulário.

### Considerações para APIs de comunicações {#considerations-for-communications-apis}

#### Dados do formulário {#form-data}

As APIs de comunicações aceitam um design de formulário que normalmente é criado no Designer e dados de formulário XML como entrada. Para preencher um documento com dados, um elemento XML deve existir nos dados do formulário XML para cada campo de formulário que você deseja preencher. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML é ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos. O fator importante é que os elementos XML são especificados com valores correspondentes.

Considere o seguinte exemplo de formulário de pedido de empréstimo:

![Formulário de pedido de empréstimo](assets/loanFormData.png)

Para unir dados neste design de formulário, crie uma fonte de dados XML que corresponda ao formulário. O XML a seguir representa uma fonte de dados XML que corresponde ao formulário de aplicativo de hipoteca de exemplo.

```XML
<?xml version="1.0" encoding="UTF-8" ?>
- <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
- <xfa:data>
- <data>
    - <Layer>
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
    - <Mortgage>
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

#### Tipos de documento suportados {#supported-document-types}

Para obter acesso completo aos recursos de renderização das APIs de Comunicação, é recomendável usar um arquivo XDP como entrada. Em alguns casos, um arquivo PDF pode ser usado. No entanto, usar um arquivo PDF como entrada tem as seguintes limitações:

- Um documento PDF que não contém um fluxo XFA não pode ser renderizado como PostScript, PCL ou ZPL. As APIs de comunicações podem renderizar documentos PDF com fluxos XFA (ou seja, formulários criados no Designer) em formatos de laser e rótulo. Se o documento do PDF for assinado, certificado ou contiver direitos de uso (aplicados usando o serviço AEM Forms Reader Extensions), ele não poderá ser renderizado para esses formatos de impressão.

<!-- * Run-time options such as PDF version and tagged PDF are not supported for Acrobat forms. They are valid for PDF forms that contain XFA streams; however, these forms cannot be signed or certified. 

#### Email support {#email-support}

For email functionality, you can create a process in AEM Workflows that uses the Email Step. A workflow represents a business process that you are automating. -->

#### Áreas para impressão {#printable-areas}

A margem não imprimível padrão de 0,25 polegadas não é exata para impressoras de etiquetas e varia de impressora para impressora e do tamanho do rótulo para tamanho do rótulo. É recomendável manter a margem de 0,25 polegadas ou reduzi-la. No entanto, é recomendável não aumentar a margem não imprimível. Caso contrário, as informações na área de impressão não serão impressas corretamente.

Sempre verifique se você usa o arquivo XDC correto para a impressora. Por exemplo, evite escolher um arquivo XDC para uma impressora de 300 dpi e envie o documento para uma impressora de 200 dpi.

#### Scripts {#scripts}

Um design de formulário usado com as APIs de comunicações pode conter scripts executados no servidor. Certifique-se de que um design de formulário não contenha scripts executados no cliente. Para obter informações sobre como criar scripts de design de formulário, consulte a Ajuda do Designer.

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

#### Mapeamento de fonte {#font-mapping}

Se uma fonte estiver instalada em um computador cliente, ela estará disponível na lista suspensa no Designer. Se a fonte não estiver instalada, é necessário especificar o nome da fonte manualmente. A opção &quot;Substituir permanentemente fontes indisponíveis&quot; no Designer pode estar desativada. Caso contrário, quando o arquivo XDP é salvo no Designer, o nome da fonte de substituição é gravado no arquivo XDP. Isso significa que a fonte residente na impressora não é usada.

Para projetar um formulário que use fontes residentes na impressora, escolha um nome de fonte no Designer que corresponda às fontes disponíveis na impressora. Uma lista de fontes compatíveis com PCL ou PostScript está localizada nos perfis de dispositivo correspondentes (arquivos XDC). Como alternativa, o mapeamento de fontes pode ser criado para mapear fontes não residentes em impressoras para fontes residentes em impressoras de um nome de fonte diferente. Por exemplo, em um cenário PostScript, as referências à fonte Arial® podem ser mapeadas para a fonte Helvetica® residente na impressora.

Existem dois tipos de fontes OpenType®. Um tipo é uma fonte TrueType OpenType® compatível com PCL. O outro é o OpenType CFF®. A saída PDF e PostScript suporta fontes incorporadas Type-1, TrueType e OpenType®. A saída PCL suporta fontes TrueType incorporadas.

As fontes Tipo-1 e OpenType® não são incorporadas na saída PCL. O conteúdo formatado com fontes Tipo-1 e OpenType® é rasterizado e gerado como uma imagem de bitmap que pode ser grande e mais lenta para gerar.

Fontes baixadas ou incorporadas são substituídas automaticamente ao gerar saída PostScript, PCL ou PDF. Isso significa que somente o subconjunto dos glifos de fonte necessários para renderizar corretamente o documento gerado é incluído na saída gerada.

#### Trabalhar com arquivos de perfil de dispositivo (arquivo XDC) {#working-with-xdc-files}

Um perfil de dispositivo (arquivo XDC) é um arquivo de descrição de impressora no formato XML. Esse arquivo permite que as APIs de comunicações enviem documentos como formatos de impressora laser ou de etiqueta. As APIs de comunicações usam os arquivos XDC, incluindo estes:

- hppcl5c.xdc

- hppcl5e.xdc

- ps_plain_level3.xdc

- ps_plain.xdc

- zpl300.xdc

- zpl600.xdc

- zpl300.xdc

- ipl300.xdc

- ipl400.xdc

- tpcl600.xdc

- dpl300.xdc

- dpl406.xdc

- dpl600.xdc

Não é necessário modificar esses arquivos para criar documentos. No entanto, você pode modificá-las para atender aos requisitos de sua empresa.

Esses arquivos são arquivos XDC de amostra que oferecem suporte aos recursos de impressoras específicas, como fontes residentes, bandejas de papel e grampeadores. O objetivo dessas amostras é ajudar você a entender como configurar suas próprias impressoras usando perfis de dispositivo. As amostras também são um ponto de partida para impressoras semelhantes na mesma linha de produtos.

#### Trabalhar com o arquivo de configuração XCI {#working-with-xci-files}

As APIs de comunicações usam um arquivo de configuração XCI para executar tarefas, como controlar se a saída é um único painel ou paginada. Embora esse arquivo contenha configurações que podem ser definidas, não é normal modificar esse valor. <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

Você pode passar um arquivo XCI modificado usando uma API de comunicações. Ao fazer isso, crie uma cópia do arquivo padrão, altere somente os valores que exigem modificação para atender às suas necessidades de negócios e use o arquivo XCI modificado.

As APIs de comunicações começam com o arquivo XCI padrão (ou o arquivo modificado). Em seguida, ele aplica valores especificados pelas APIs de comunicações. Esses valores substituem as configurações XCI.

A tabela a seguir especifica as opções de XCI.

| Opção XCI | Descrição |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
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

<!-- Using API

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as HTTP endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document. -->
