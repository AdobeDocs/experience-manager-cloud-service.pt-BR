---
title: Considerações sobre problemas conhecidos e práticas recomendadas
description: Práticas recomendadas de comunicação, problemas conhecidos e limitações
exl-id: e95615dd-e494-40cd-9cdf-6e9761ca3b3e
source-git-commit: 4b76fbbb1b58324065b39d6928027759b0897246
workflow-type: tm+mt
source-wordcount: '1707'
ht-degree: 0%

---

# Considerações sobre problemas conhecidos e práticas recomendadas {#best-practices-known-issues-and-limitations}

Antes de começar a usar as APIs de comunicação, analise as seguintes considerações, problemas conhecidos e perguntas frequentes:

## Considerações  {#considerations-for-communications-apis}

### Dados de formulário {#form-data}

As APIs de comunicação aceitam um design de formulário que normalmente é criado no Designer e dados de formulário XML como entrada. Para preencher um documento com dados, um elemento XML deve existir nos dados de formulário XML para cada campo de formulário que você deseja preencher. O nome do elemento XML deve corresponder ao nome do campo. Um elemento XML será ignorado se não corresponder a um campo de formulário ou se o nome do elemento XML não corresponder ao nome do campo. Não é necessário corresponder à ordem em que os elementos XML são exibidos. O fator importante é que os elementos XML são especificados com valores correspondentes.

Considere o exemplo de formulário de aplicativo de empréstimo a seguir:

![Formulário de pedido de empréstimo](assets/loanFormData.png)

Para mesclar dados neste design de formulário, crie uma fonte de dados XML que corresponda ao formulário. O XML a seguir representa uma fonte de dados XML que corresponde ao exemplo de formulário de aplicativo de hipoteca.

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

### Tipos de documento suportados {#supported-document-types}

Para obter acesso total aos recursos de renderização das APIs de comunicações, é recomendável usar um arquivo XDP como entrada. Às vezes, um arquivo PDF pode ser usado. No entanto, o uso de um arquivo PDF como entrada tem as limitações:

Um documento PDF que não contém um fluxo XFA não pode ser renderizado como PostScript, PCL ou ZPL. As APIs de comunicação podem renderizar documentos PDF com fluxos XFA (ou seja, formulários criados no Designer) em formatos laser e de rótulo. Se o documento PDF for assinado, certificado ou contiver direitos de uso (aplicados pelo serviço AEM Forms Reader Extensions), ele não poderá ser renderizado nesses formatos de impressão.


### Áreas imprimíveis {#printable-areas}

A margem não imprimível padrão de 0,25 pol. não é exata para impressoras de etiquetas e varia de impressora para impressora e de tamanho de etiqueta para tamanho de etiqueta. No entanto, é recomendável manter ou reduzir a margem de 0,25 pol. No entanto, é recomendável não aumentar a margem não imprimível. Caso contrário, as informações na área imprimível não serão impressas corretamente.

Use sempre o arquivo XDC correto para a impressora. Por exemplo, evite escolher um arquivo XDC para uma impressora de 300 dpi e enviar o documento para uma impressora de 200 dpi.

### Scripts somente para formulários XFA (XDP/PDF) {#scripts}

Um design de formulário usado com as APIs de comunicações pode conter scripts executados no servidor. Certifique-se de que um design de formulário não contenha scripts que sejam executados no cliente. Para obter informações sobre como criar scripts de design de formulário, consulte [Ajuda do Designer](use-forms-designer.md).

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### Mapeamento de fontes {#font-mapping}

Para criar um formulário que use fontes residentes na impressora, escolha um nome de fonte no Designer que corresponda às fontes disponíveis na impressora. Uma lista de fontes compatíveis com PCL ou PostScript está localizada nos perfis de dispositivo correspondentes (arquivos XDC). Como alternativa, o mapeamento de fontes pode ser criado para mapear fontes não residentes na impressora para fontes residentes na impressora de um nome de fonte diferente. Por exemplo, em um cenário PostScript, as referências à fonte Arial® podem ser mapeadas para a fonte Helvetica® residente na impressora.

Se uma fonte estiver instalada em um computador cliente, ela estará disponível na lista suspensa no Designer. Se a fonte não estiver instalada, será necessário especificar o nome da fonte manualmente. A opção &quot;Substituir permanentemente fontes indisponíveis&quot; no Designer pode estar desativada. Caso contrário, quando o arquivo XDP é salvo no Designer, o nome da fonte de substituição é gravado no arquivo XDP. Isso significa que a fonte residente na impressora não é usada.

Existem dois tipos de fontes OpenType®. Um tipo é uma fonte TrueType OpenType® suportada por PCL. O outro é o CFF OpenType®. A saída de PDF e PostScript suporta fontes Type-1, TrueType e OpenType® incorporadas. A saída PCL suporta fontes TrueType incorporadas.

As fontes Type-1 e OpenType® não estão incorporadas na saída PCL. O conteúdo formatado com as fontes Type-1 e OpenType® é rasterizado e gerado como uma imagem bitmap que pode ser grande e de geração mais lenta.

As fontes baixadas ou incorporadas são substituídas automaticamente ao gerar saída PostScript, PCL ou PDF. Isso significa que somente o subconjunto dos glifos de fonte necessários para renderizar corretamente o documento gerado é incluído na saída gerada.

### Trabalhar com arquivos de perfil de dispositivo (arquivo XDC) {#working-with-xdc-files}

Um perfil de dispositivo (arquivo XDC) é um arquivo de descrição da impressora no formato XML. Esse arquivo permite que as APIs de comunicações emitam documentos como formatos de impressora a laser ou de etiqueta. As APIs de comunicação usam os arquivos XDC, incluindo o seguinte:

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

Você pode usar os arquivos XDC fornecidos para gerar documentos de impressão ou modificá-los de acordo com sua necessidade.
<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

Esses arquivos são arquivos XDC de referência que oferecem suporte a recursos de impressoras específicas, como fontes residentes, bandejas de papel e grampeador. O objetivo dessa referência é ajudá-lo a entender como configurar suas próprias impressoras usando perfis de dispositivo. A referência também é um ponto de partida para impressoras semelhantes na mesma linha de produtos.

### Trabalhar com o arquivo de configuração XCI {#working-with-xci-files}

As APIs de comunicações usam um arquivo de configuração XCI para executar tarefas, como controlar se a saída é um painel único ou paginada. Embora esse arquivo contenha configurações que podem ser definidas, não é típico modificar esse valor. <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

Você pode passar um arquivo XCI modificado ao usar uma API de comunicações. Ao fazer isso, crie uma cópia do arquivo padrão, altere apenas os valores que exigem modificação para atender aos requisitos comerciais e use o arquivo XCI modificado.

As APIs de comunicações começam com o arquivo XCI padrão (ou o arquivo modificado). Em seguida, ele aplica valores especificados usando as APIs de comunicações. Esses valores substituem as configurações XCI.

A tabela a seguir especifica as opções de XCI.

| Opção XCI | Descrição |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config/present/pdf/creator | Identifica o criador do documento usando a entrada Criador no dicionário de Informações do Documento. Para obter informações sobre esse dicionário, consulte o Guia de referência de PDF. |
| config/present/pdf/producer | Identifica o produtor do documento usando a entrada Produtor no dicionário de Informações do documento. Para obter informações sobre esse dicionário, consulte o Guia de referência de PDF. |
| config/present/layout | Controla se a saída é um painel único ou paginada. |
| config/present/pdf/compression/level | Especifica o grau de compactação a ser usado ao gerar um documento PDF. |
| config/present/pdf/scriptModel | Controla se informações específicas de XFA são incluídas no documento PDF de saída. |
| config/present/common/data/adjustData | Controla se o aplicativo XFA ajusta os dados após a mesclagem. |
| config/present/pdf/renderPolicy | Controla se a geração do conteúdo da página é feita no servidor ou adiada para o cliente. |
| configuração/presente/comum/local | Especifica a localidade padrão usada no documento de saída. |
| config/present/destination | Quando contido por um elemento presente, especifica o formato de saída. Quando contido por um elemento openAction, especifica a ação a ser executada ao abrir o documento em um cliente interativo. |
| config/present/output/type | Especifica o tipo de compactação a ser aplicado a um arquivo ou o tipo de saída a ser produzido. |
| config/present/common/temp/uri | Especifica o URI do formulário. |
| config/present/common/template/base | Fornece um local base para URIs no design do formulário. Quando este elemento estiver ausente ou vazio, o local do design do formulário será usado como base. |
| config/present/common/log/to | Controla o local onde os dados de log ou de saída são gravados. |
| config/present/output/to | Controla o local onde os dados de log ou de saída são gravados. |
| config/present/script/currentPage | Especifica a página inicial quando o documento é aberto. |
| config/present/script/exclude | Informa ao servidor da AEM Forms/APIs de comunicações quais eventos devem ser ignorados. |
| config/present/pdf/linearized | Controla se o documento de PDF de saída está linearizado. |
| config/present/script/runScripts | Controla qual conjunto de scripts o AEM Forms executa. |
| config/present/pdf/tagged | Controla a inclusão de tags no documento de PDF de saída. As tags, no contexto de PDF, são informações adicionais incluídas em um documento para expor a estrutura lógica do documento. As tags auxiliam na acessibilidade e na reformatação. Por exemplo, um número de página pode ser marcado como um artefato para que um leitor de tela não o enuncie no meio do texto. Embora as tags tornem um documento mais útil, elas também aumentam o tamanho do documento e o tempo de processamento para criá-lo. |
| config/present/pdf/version | Especifica a versão do documento de PDF a ser gerada. |


## Problemas conhecidos

* Você pode usar um tipo de renderização específico (PDF, PRINT) apenas uma vez na lista de opções de impressão. Por exemplo, você não pode ter duas opções PRINT, cada uma especificando um tipo de renderização PCL.

* Para uma configuração em lote, somente uma instância de combinação de valores de OutputType(PDF, PRINT) e RenderType(PostScript, PCL, IPL, ZPL etc.) é permitido.

* Para APIs assíncronas (Processamento em lote), o nível de registro padrão é definido como 2. Você pode usar um XCI personalizado para alterar o nível de registro para 1.

* Quando o XCI padrão é configurado, ele inclui o caminho até a representação original. Por exemplo `/content/dam/formsanddocuments/default.xci/jcr:content/renditions/original`



## Práticas recomendadas    

* A Adobe recomenda hospedar arquivos de dados no armazenamento de contêiner de blob na região da nuvem usada pelo AEM Cloud Service.

## Perguntas frequentes {#faq}

**Posso usar uma pasta monitorada ou outros mecanismos de armazenamento para armazenar entrada e saída?**

No momento, você pode usar o Armazenamento do Microsoft Azure para salvar dados de entrada e documentos gerados. O armazenamento do Microsoft Azure fornece várias opções para [automatizar operações de movimentação de dados](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Uma conta de Armazenamento do Microsoft Azure está incluída na licença do Cloud Service da Experience Manager Forms?**

A conta de Armazenamento do Microsoft Azure é independente da licença Cloud Service do Experience Manager Forms.

**As APIs de comunicação armazenam dados nos servidores Experience Manager Forms Cloud Service?**

Os dados de entrada e saída são salvos somente no Armazenamento do Microsoft Azure.

**As APIs de comunicação estão disponíveis apenas para o Experience Manager Forms Cloud Service? É possível obter funcionalidade semelhante no ambiente local?**

Você pode usar o serviço AEM Forms Output para combinar um modelo (XFA ou PDF) com os dados do cliente para gerar documentos nos formatos PDF, PS, PCL e ZPL.

Em comparação com o ambiente local, o Cloud Service oferece benefícios adicionais de dimensionamento automático e economia.

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**Posso executar várias operações em lote simultaneamente?**
Sim, você pode executar várias operações em lote simultaneamente. Sempre use pastas de origem e destino diferentes para cada operação para evitar conflitos.
