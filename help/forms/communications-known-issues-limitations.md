---
title: 'Problemas conhecidos '
description: Práticas recomendadas de comunicações, problemas conhecidos e limitações
source-git-commit: c38a34519822449ff2577a9474b1294d5d45d3ae
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 0%

---


# Considerações sobre problemas conhecidos e práticas recomendadas {#best-practices-known-issues-and-limitations}

Antes de começar a usar as APIs de comunicação, analise as considerações a seguir, os problemas conhecidos e as perguntas frequentes:

## Considerações  {#considerations-for-communications-apis}

### Dados do formulário {#form-data}

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

### Tipos de documento suportados {#supported-document-types}

Para obter acesso completo aos recursos de renderização das APIs de Comunicação, é recomendável usar um arquivo XDP como entrada. Às vezes, um arquivo PDF pode ser usado. No entanto, usar um arquivo PDF como entrada tem as limitações:

Um documento PDF que não contém um fluxo XFA não pode ser renderizado como PostScript, PCL ou ZPL. As APIs de comunicações podem renderizar documentos PDF com fluxos XFA (ou seja, formulários criados no Designer) em formatos de laser e rótulo. Se o documento do PDF for assinado, certificado ou contiver direitos de uso (aplicados usando o serviço AEM Forms Reader Extensions), ele não poderá ser renderizado para esses formatos de impressão.


### Áreas para impressão {#printable-areas}

A margem padrão não imprimível de 0,25 polegadas não é exata para impressoras de etiquetas e varia de impressora para impressora e do tamanho do rótulo para tamanho do rótulo, no entanto, é recomendável manter a margem de 0,25 polegadas ou reduzi-la. No entanto, é recomendável não aumentar a margem não imprimível. Caso contrário, as informações na área de impressão não serão impressas corretamente.

Sempre verifique se você usa o arquivo XDC correto para a impressora. Por exemplo, evite escolher um arquivo XDC para uma impressora de 300 dpi e envie o documento para uma impressora de 200 dpi.

### Scripts somente para formulários XFA (XDP/PDF) {#scripts}

Um design de formulário usado com as APIs de comunicações pode conter scripts executados no servidor. Certifique-se de que um design de formulário não contenha scripts executados no cliente. Para obter informações sobre como criar scripts de design de formulário, consulte [Ajuda do Designer](use-forms-designer.md).

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

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
<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

Esses arquivos são arquivos XDC de referência que oferecem suporte aos recursos de impressoras específicas, como fontes residentes, bandejas de papel e grampeador. A finalidade dessa referência é ajudar você a entender como configurar suas próprias impressoras usando perfis de dispositivo. As referências são também um ponto de partida para impressoras semelhantes na mesma linha de produtos.

### Trabalhar com o arquivo de configuração XCI {#working-with-xci-files}

As APIs de comunicações usam um arquivo de configuração XCI para executar tarefas, como controlar se a saída é um único painel ou paginada. Embora esse arquivo contenha configurações que podem ser definidas, não é normal modificar esse valor. <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

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


## Problemas conhecidos

* Você pode usar um tipo de renderização específico (PDF, IMPRESSÃO) apenas uma vez na lista de opções de impressão. Por exemplo, você não pode ter duas opções de IMPRESSÃO, cada uma especificando um tipo de renderização PCL.

* Para uma configuração de lote, apenas uma instância da combinação de valores de OutputType(PDF, PRINT) e RenderType(PostScript, PCL, IPL, ZPL, etc.) é permitido.

## Práticas recomendadas    

* O Adobe recomenda hospedar arquivos de dados no armazenamento do contêiner de blob na região de nuvem usada pelo AEM Cloud Service.

## Perguntas frequentes {#faq}

**Posso usar uma pasta monitorada ou outros mecanismos de armazenamento para armazenar entrada e saída?**

No momento, você pode usar o Armazenamento do Microsoft Azure para salvar dados de entrada e documentos gerados. O armazenamento do Microsoft Azure fornece várias opções para [automatizar operações de movimentação de dados](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Uma conta de armazenamento do Microsoft Azure está incluída na licença do Experience Manager Forms Cloud Service?**

A conta de armazenamento do Microsoft Azure é independente da licença do Experience Manager Forms Cloud Service.

**As APIs do Communication armazenam dados nos servidores do Experience Manager Forms Cloud Service?**

Os dados de entrada e saída são salvos somente no Armazenamento do Microsoft Azure.

**As APIs de comunicação estão disponíveis apenas para o Experience Manager Forms Cloud Service? Posso obter funcionalidade semelhante no ambiente local?**

Você pode usar o serviço AEM Forms Output para combinar um modelo (XFA ou PDF) com dados do cliente para gerar documentos nos formatos PDF, PS, PCL e ZPL.

Em comparação com o ambiente local, o Cloud Service oferece benefícios adicionais de dimensionamento automático e economia de custos.

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**Posso executar várias operações em lote simultaneamente?**
Sim, você pode executar várias operações em lote de maneira semelhante. Sempre use pastas de origem e de destino diferentes para cada operação para evitar conflitos.
