---
title: Gerenciar predefinições de imagem
description: Saiba mais sobre predefinições de imagens e como criar, modificar e gerenciar predefinições de imagens.
contentOwner: Rick Brough
feature: Image Presets,Viewers,Renditions
role: User
exl-id: a53f40ab-0e27-45f8-9142-781c077a04cc
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '3587'
ht-degree: 8%

---

# Gerenciar predefinições de imagem{#managing-image-presets}

As Predefinições de imagem permitem que o Adobe Experience Manager Assets forneça imagens dinamicamente em diferentes tamanhos, formatos ou com outras propriedades de imagem geradas dinamicamente. Cada predefinição de imagem representa uma coleção predefinida de comandos de dimensionamento e formatação para a exibição de imagens. Ao criar uma Predefinição de imagem, você escolhe um tamanho para a entrega da imagem. Você também escolhe comandos de formatação para que a aparência da imagem seja otimizada quando ela for entregue para visualização.

Os administradores podem criar predefinições para exportar ativos. Os usuários podem escolher uma predefinição ao exportar imagens, o que também reformata imagens para as especificações especificadas pelo administrador.

Também é possível criar predefinições de imagens responsivas. Se você aplicar uma predefinição de imagem responsiva aos seus ativos, eles mudam dependendo do dispositivo ou tamanho da tela em que são exibidos. É possível configurar predefinições de imagens para usar CMYK no espaço de cores, além de RGB ou Cinza.

Esta seção descreve como criar, modificar e gerenciar predefinições de imagens. É possível aplicar uma predefinição de imagem a uma imagem sempre que ela for visualizada. Consulte [Aplicar predefinições de imagem](/help/assets/dynamic-media/image-presets.md).

>[!NOTE]
>
>A geração de imagens inteligentes funciona com suas predefinições de imagens existentes e usa inteligência nos últimos milissegundos do delivery para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede. Consulte [Smart Imaging](/help/assets/dynamic-media/imaging-faq.md) para obter mais informações.

## Saiba mais sobre predefinições de imagem {#understanding-image-presets}

Como uma macro, uma Predefinição de imagem é uma coleção predefinida de comandos de dimensionamento e formatação salvos com um nome. Para entender como as Predefinições de imagem funcionam, suponha que seu site exija que cada imagem do produto seja exibida em tamanhos, formatos e taxas de compactação diferentes para entrega de desktops e dispositivos móveis.

Você pode criar duas predefinições de imagem: uma com 500 x 500 pixels para a versão para desktop e 150 x 150 pixels para a versão móvel. Você cria duas Predefinições de Imagem, uma chamada `Enlarge` para exibir imagens a 500x500 pixels e outra chamada `Thumbnail` para exibir imagens a 150 x 150 pixels. Para fornecer imagens no tamanho `Enlarge` e `Thumbnail`, o Experience Manager encontra a definição da Predefinição Ampliar Imagem e da Predefinição Miniatura de Imagem. Em seguida, o Experience Manager gera dinamicamente uma imagem com as especificações de tamanho e formatação de cada Predefinição de imagem.

Imagens com tamanho reduzido quando entregues dinamicamente podem perder nitidez e detalhes. Por esse motivo, cada Predefinição de imagem contém controles de formatação para otimizar uma imagem quando ela é entregue em um tamanho específico. Esses controles garantem que suas imagens sejam nítidas e claras quando forem entregues ao seu site ou aplicativo.

Os administradores podem criar Predefinições de imagem. Para criar uma predefinição de imagem, inicie do zero ou inicie a partir de uma predefinição existente e salve-a com um novo nome.

## Gerenciar predefinições de imagem {#managing-image-presets-1}

Para gerenciar as predefinições de imagem no Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global e, em seguida, selecione o ícone Ferramentas e navegue até **[!UICONTROL Assets]** > **[!UICONTROL Predefinições de Imagem]**.

![6_5_ferramentas-ativos-imagens-predefinições](assets/6_5_tools-assets-imagepresets.png)

>[!NOTE]
>
>Todas as predefinições de imagens criadas também estão disponíveis como representações dinâmicas ao pré-visualizar ou fornecer ativos.
>
>Você precisa *não* publicar predefinições de imagens, pois as predefinições de imagens são publicadas automaticamente.
>
>Consulte [Predefinições de imagem do Publish](#publishing-image-presets).

>[!NOTE]
>
>O sistema mostra várias representações quando você seleciona **[!UICONTROL Representações]** na Exibição de detalhes de um ativo. É possível aumentar ou diminuir o número de predefinições de imagens exibidas. Consulte [Aumentar o número de predefinições de imagens exibidas](#increasing-or-decreasing-the-number-of-image-presets-that-display).

### Formatos de arquivo Adobe Illustrator (AI), PostScript® (EPS) e PDF {#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats}

Se sua intenção for oferecer suporte à assimilação de arquivos AI, EPS e PDF para que você possa gerar representações dinâmicas desses formatos de arquivo, revise as informações a seguir antes de criar predefinições de imagem.

O formato de arquivo do Adobe Illustrator é uma variante do PDF. As principais diferenças, no contexto do Experience Manager Assets, são as seguintes:

* Os documentos do Adobe Illustrator consistem em uma única página com várias camadas. Cada camada é extraída como um subativo PNG no ativo principal do Illustrator.
* Os documentos PDF consistem em uma ou mais páginas. Cada página é extraída como um único subativo de PDF de página no documento principal de PDF de várias páginas.

Os subativos são criados pelo componente `Create Sub Asset process` dentro do fluxo de trabalho `DAM Update Asset` geral. Para ver este componente do processo no fluxo de trabalho, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]** > **[!UICONTROL Ativo de atualização do DAM]** > **[!UICONTROL Editar]**.

<!-- See also [Viewing pages of a multi-page file](/help/assets/manage-linked-subassets.md#view-pages-of-a-multi-page-file). -->

É possível exibir os subativos ou as páginas ao abrir o ativo, selecionar o menu Conteúdo e selecionar **[!UICONTROL Subativos]** ou **[!UICONTROL Páginas]**. Os subativos são ativos reais. Ou seja, as páginas de PDF são extraídas pelo componente de fluxo de trabalho `Create Sub Asset`. Eles são armazenados como `page1.pdf`, `page2.pdf` e assim por diante, abaixo do ativo principal. Após serem armazenados, o fluxo de trabalho `DAM Update Asset` os processa.

Para usar o Dynamic Media para visualizar e gerar representações dinâmicas para arquivos AI, EPS ou PDF, as seguintes etapas de processamento são necessárias:

1. No fluxo de trabalho `DAM Update Asset`, o componente de processo `Rasterize PDF/AI Image Preview Rendition` rasteriza a primeira página do ativo original, usando a resolução configurada, em uma representação `cqdam.preview.png`.

1. A representação `cqdam.preview.png` é otimizada em um PTIFF pelo componente de processo `Dynamic Media Process Image Assets` no fluxo de trabalho.

>[!NOTE]
>
>No fluxo de trabalho do ativo de atualização do DAM, a etapa de **[!UICONTROL Miniaturas do EPS]** gera miniaturas para arquivos EPS.

#### Propriedades de metadados de ativos do PDF/AI/EPS {#pdf-ai-eps-asset-metadata-properties}

| **Propriedade de metadados** | **Descrição** |
|---|---|
| dam:Physicalwidthininch | Largura do documento em polegadas. |
| dam:Physicalheightinpolegadas | Altura do documento em polegadas. |

Você acessa `Rasterize PDF/AI Image Preview Rendition` opções do componente do processo por meio do fluxo de trabalho `DAM Update Asset`.

Selecione Adobe Experience Manager no canto superior esquerdo, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**. Na página Modelos de fluxo de trabalho, selecione **[!UICONTROL Ativo de atualização do DAM]** e, na barra de ferramentas, selecione **[!UICONTROL Editar]**. Na página de fluxo de trabalho Atualizar ativo do DAM, selecione duas vezes o componente do processo `Rasterize PDF/AI Image Preview Rendition` para abrir sua caixa de diálogo Propriedades da etapa.

#### Opções de Rasterizar representação da exibição de imagens do PDF/AI {#rasterize-pdf-ai-image-preview-rendition-options}

![Argumentos para rasterizar o fluxo de trabalho do PDF ou da IA](assets/rasterize_pdf_ai_image_preview.png)

Argumentos para rasterizar o fluxo de trabalho do PDF ou da IA

| Argumento do processo | Configuração padrão | Descrição |
|---|---|---|
| Tipos de mime | application/pdf<br>application/postscript<br>application/illustrator | Lista de tipos MIME de documentos que são considerados documentos PDF ou Illustrator. |
| Largura máxima | 2048 | Largura máxima da representação de visualização gerada, em pixels. |
| Altura máxima | 2048 | Altura máxima da representação de visualização gerada, em pixels. |
| Resolução | 72 | Resolução para rasterizar a primeira página, em ppi (pixels por polegada). |

Usando os argumentos de processo padrão, a primeira página de um documento PDF/AI é rasterizada em 72 ppi e a imagem de visualização gerada é dimensionada em 2048 x 2048 pixels. Para uma implantação típica, é possível aumentar a resolução para um mínimo de 150 ppi ou mais. Por exemplo, um documento tamanho carta EUA a 300 ppi requer no máximo 2550 x 3300 pixels de largura e altura, respectivamente.

Largura máxima e Altura máxima limitam a resolução na qual rasterizar. Por exemplo, se os máximos não forem alterados e a Resolução for definida como 300 ppi, um documento Carta dos EUA será rasterizado em 186 ppi. Ou seja, o documento tem 1581 x 2046 pixels.

O componente do processo `Rasterize PDF/AI Image Preview Rendition` tem um máximo definido para garantir que ele não crie imagens muito grandes na memória. Essas imagens grandes podem estourar a memória fornecida para a JVM (Java™ Virtual Machine). É necessário tomar cuidado para fornecer à JVM memória suficiente para gerenciar o número configurado de workflows paralelos, com cada um tendo o potencial de criar uma imagem no tamanho máximo configurado.

### formato de arquivo InDesign (INDD) {#indesign-indd-file-format}

Se você pretende suportar a assimilação de arquivos INDD para gerar uma representação dinâmica desse formato de arquivo, revise as informações a seguir antes de criar predefinições de imagem.

Para arquivos de InDesign, os sub-ativos são extraídos somente se o Adobe InDesign Server estiver integrado ao Experience Manager. Os ativos referenciados são vinculados com base em seus metadados. O InDesign Server não é necessário para vinculação. No entanto, os ativos referenciados devem estar presentes no Experience Manager antes que os arquivos de InDesign sejam processados para que os links sejam criados entre os arquivos de InDesign e os ativos referenciados.

<!-- See [Integrate Experience Manager Assets with InDesign Server](/help/assets/indesign.md). -->

O componente do processo de Extração de Mídia no fluxo de trabalho `DAM Update Asset` executa vários Scripts de Extensão pré-configurados para processar arquivos de InDesign.

![Os caminhos do ExtendScript nos argumentos do processo de Extração de Mídia](/help/assets/dynamic-media/assets/6_5_mediaextractionprocess.png)

Os caminhos do ExtendScript nos argumentos do componente do processo de Extração de mídia no fluxo de trabalho Atualizar ativo do DAM.

Os seguintes scripts são usados pela integração do Dynamic Media:


| Nome do ExtendScript | Padrão | Descrição |
|---|---|---|
| ThumbnailExport.jsx | Sim | Gera uma representação de 300 PPI `thumbnail.jpg` que é otimizada e transformada em uma representação PTIFF pelo componente de processo `Dynamic Media Process Image Assets`. |
| JPEGPagesExport.jsx | Sim | Gera um subativo de JPEG de 300 PPI para cada página. O subativo JPEG é um ativo real armazenado no ativo InDesign. Ele também é otimizado e transformado em um PTIFF pelo fluxo de trabalho `DAM Update Asset`. |
| PDFPagesExport.jsx | Não | Gera um subativo PDF para cada página. O subativo PDF é processado conforme descrito anteriormente. Como o PDF contém apenas uma página, nenhum subativo é gerado. |

### Configurar tamanho da miniatura da imagem {#configuring-image-thumbnail-size}

Você pode definir o tamanho das miniaturas definindo essas configurações no fluxo de trabalho **[!UICONTROL Ativo de atualização DAM]**. Há duas etapas no fluxo de trabalho nas quais você pode configurar o tamanho da miniatura de ativos de imagem. Uma (**[!UICONTROL Dynamic Media Process Image Assets]**) é usada para ativos de imagem dinâmicos. O outro (**[!UICONTROL Miniaturas de Processo]**) é usado para geração de miniaturas estáticas ou quando todos os outros processos não conseguem gerar miniaturas. Independentemente disso, *ambos* devem ter as mesmas configurações.

Com a etapa **[!UICONTROL Ativos de imagem de processo do Dynamic Media]**, as miniaturas são geradas pelo servidor de imagem e essa configuração é independente da configuração aplicada à etapa **[!UICONTROL Processar miniaturas]**. Gerar miniaturas por meio da etapa **[!UICONTROL Processar miniaturas]** é a maneira mais lenta e intensiva de memória para criar miniaturas.

O dimensionamento de miniatura é definido no seguinte formato: **[!UICONTROL largura:height:centro]**, por exemplo, `80:80:false`. A largura e a altura determinam o tamanho da miniatura em pixels. O valor central é falso ou verdadeiro. Se definido como true, indica que a imagem em miniatura tem exatamente o tamanho fornecido na configuração. Se a imagem redimensionada for menor, ela será centralizada na miniatura.

>[!NOTE]
>
>* Os tamanhos de miniatura de arquivos do EPS são configurados na etapa **[!UICONTROL Miniaturas do EPS]**, na guia **[!UICONTROL Argumentos]**, em Miniaturas.
>
>* Os tamanhos de miniatura de vídeos são configurados na etapa **[!UICONTROL Miniaturas de FFmpeg]**, na guia **[!UICONTROL Processo]** em **[!UICONTROL Argumentos]**.
>

**Para configurar o tamanho da miniatura da imagem:**

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]** > **[!UICONTROL Ativo de atualização do DAM]** > **[!UICONTROL Editar]**.
1. Selecione a etapa **[!UICONTROL Dynamic Media Process Image Assets]** e selecione a guia **[!UICONTROL Miniaturas]**. Altere o tamanho da miniatura, conforme necessário, e selecione **[!UICONTROL OK]**.

   ![6_5_dynamicmediaprocessimageassets-thumbnailstab](assets/6_5_dynamicmediaprocessimageassets-thumbnailstab.png)

1. Selecione a etapa **[!UICONTROL Processar miniaturas]** e selecione a guia **[!UICONTROL Miniaturas]**. Altere o tamanho da miniatura, conforme necessário, e selecione **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Os valores no argumento de miniaturas da etapa **[!UICONTROL Processar miniaturas]** devem corresponder ao argumento de miniaturas na etapa **[!UICONTROL Ativos de imagem do processo do Dynamic Media]**.

1. Selecione **[!UICONTROL Salvar]** para salvar as alterações no fluxo de trabalho.

### Aumentar ou diminuir o número de predefinições de imagens exibidas {#increasing-or-decreasing-the-number-of-image-presets-that-display}

As predefinições de imagem criadas estão disponíveis como representações dinâmicas ao visualizar ativos. O Experience Manager mostra várias representações dinâmicas ao visualizar um ativo de **[!UICONTROL Exibição detalhada > Representações]**. É possível aumentar ou diminuir o limite de representações exibidas.

**Para aumentar ou diminuir o número de predefinições de imagens exibidas:**

1. Navegue até CRXDE Lite ([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. Navegue até o nó da listagem de predefinições de imagens em `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist`

   ![aumento_diminuição_enumeraçãobimberopredefiniçõesdeexibição](assets/increase_decreasethenumberofimagepresetsthatdisplay.png)

1. Na propriedade **[!UICONTROL limit]**, altere o **[!UICONTROL Value]**, que é definido como 15 por padrão, para o número desejado.
1. Navegar até a fonte de dados de predefinição de imagem em `/libs/dam/gui/coral/content/commons/sidepanels/imagepresetsdetail/imgagepresetslist/datasource`

   ![chlimage_1-495](assets/chlimage_1-495.png)

1. Na propriedade limit, altere o número para o número desejado, por exemplo, `{empty requestPathInfo.selectors[1] ? "20" : requestPathInfo.selectors[1]}`
1. Selecione **[!UICONTROL Salvar tudo]**.

### Criar predefinições de imagem {#creating-image-presets}

Crie predefinições de imagens para aplicar configurações de forma consistente nas imagens ao visualizar ou publicar.

>[!NOTE]
>
>Se estiver usando o Internet Explorer 9, a criação de uma predefinição não aparecerá na lista de predefinições imediatamente após salvar. Para contornar esse problema, desabilite o cache do IE9.

Se sua intenção for oferecer suporte à assimilação de arquivos AI, PDF e EPS para que você possa gerar a representação dinâmica desses formatos de arquivo, revise as informações a seguir antes de criar predefinições de imagem.

Consulte [formatos de arquivo do Adobe Illustrator (AI), PostScript® (EPS) e PDF](#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats).

Se você pretende suportar a assimilação de arquivos INDD para gerar uma representação dinâmica desse formato de arquivo, revise as informações a seguir antes de criar predefinições de imagem.

Consulte o [formato de arquivo INDD (InDesign)](#indesign-indd-file-format).

**Para criar predefinições de imagem:**

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições de imagem]**.
1. Selecione **[!UICONTROL Criar]**.

   ![chlimage_1-496](assets/chlimage_1-496.png)

   >[!NOTE]
   >
   >Para tornar essa predefinição de imagem responsiva, apague os valores nos campos **[!UICONTROL largura]** e **[!UICONTROL altura]** e deixe-os em branco.

1. Na janela **[!UICONTROL Editar Predefinição de Imagem]**, insira valores nas guias **[!UICONTROL Básico]** e **[!UICONTROL Avançado]** conforme apropriado, incluindo um nome. As opções são descritas em [Opções de predefinição de imagem](#image-preset-options). As predefinições aparecem no painel à esquerda e podem ser usadas junto com outros ativos.

   ![6_5_imagepreset-edit](assets/6_5_imagepreset-edit.png)

1. Selecione **[!UICONTROL Salvar]**.

### Criação de uma predefinição de imagem responsiva {#creating-a-responsive-image-preset}

Para criar uma predefinição de imagem responsiva, execute as etapas em [Criar predefinições de imagem](#creating-image-presets). Ao inserir a altura e a largura na janela **[!UICONTROL Editar predefinição de imagem]**, apague os valores e deixe-os em branco.

Deixá-los em branco informa ao Experience Manager que essa predefinição de imagem é responsiva. Você pode ajustar os outros valores conforme apropriado.

>[!NOTE]
>
>O ativo deve ser publicado para ver os botões **[!UICONTROL URL]** e **[!UICONTROL RESS]** ao aplicar uma predefinição de imagem a um ativo.
>
>![chlimage_1-79](assets/chlimage_1-498.png)
>
>As predefinições de imagem e os ativos de imagem são publicados automaticamente.

### Opções de predefinição de imagem {#image-preset-options}

Ao criar ou editar predefinições de imagens, você tem as opções descritas nesta seção. Além disso, a Adobe recomenda que estas opções de &quot;práticas recomendadas&quot; comecem:

* **[!UICONTROL Formato]** (guia **[!UICONTROL Básico]**) - Selecione **[!UICONTROL JPEG]** ou outro formato que atenda aos seus requisitos. Todos os navegadores da Web são compatíveis com o formato de imagem JPEG; ele oferece um bom equilíbrio entre arquivos pequenos e qualidade de imagem. No entanto, as imagens no formato JPEG usam um esquema de compactação com perdas que pode apresentar artefatos de imagem indesejados se a configuração de compactação for muito baixa. Por esse motivo, a Adobe recomenda definir a qualidade de compactação como 75. Essa configuração oferece um bom equilíbrio entre a qualidade da imagem e o tamanho pequeno de arquivo.

* **[!UICONTROL Ativar nitidez simples]** - Não selecione **[!UICONTROL Ativar nitidez simples]** (este filtro de nitidez oferece menos controle do que as configurações Tirar nitidez da máscara).

* **[!UICONTROL Nitidez: Modo De Reamostragem]** - Selecione **[!UICONTROL Sharp2]**.

#### Opções da guia Básico {#basic-tab-options}

| Texto | Descrição |
| --- | --- |
| **Nome** | Insira um nome descritivo sem espaços em branco. Para ajudar os usuários a identificarem essa predefinição de imagem, inclua a especificação do tamanho da imagem no nome. |
| **Largura e Altura** | Insira, em pixels, o tamanho da imagem. A largura e a altura devem ser maiores que 0 pixels. Se um dos valores for 0, nenhuma predefinição será criada. Se ambos os valores estiverem em branco, uma predefinição de imagem responsiva será criada. |
| **Formato** | Escolha um formato no menu.<br>Escolher **JPEG** oferece as seguintes outras opções:<br>· **Qualidade** - A escala de qualidade JPEG é de 1 a 100. A escala fica visível quando você arrasta o controle deslizante.<br>· **Habilitar redução de resolução de crominância de JPG** - Como o olho é menos sensível a informações de cores de alta frequência do que a luminosidade de alta frequência, as imagens de JPEG dividem as informações da imagem em componentes de luminosidade e cor. Quando uma imagem de JPEG é compactada, o componente de luminosidade fica com a resolução total, enquanto os componentes de cor ficam com uma resolução mais baixa para calcular a média de grupos de pixels. A redução da resolução reduz o volume de dados pela metade ou em um terço com quase nenhum impacto na qualidade aparente. A redução da resolução não é aplicável a imagens em tons de cinza. Essa técnica reduz a quantidade de compactação útil para imagens com alto contraste (por exemplo, imagens com texto sobreposto).<br><br>Escolher **GIF** ou **GIF com alpha** fornece estas opções adicionais de **Quantização de Cores de GIF**:<br>· **Tipo** - Selecionar **Adaptável** (padrão), **Web** ou **Macintosh**. Se você selecionar **GIF com Alpha**, a opção Macintosh não estará disponível.<br>· **Pontilhamento** - Selecionar **Difuso** ou **Desativado**.<br>· **Número de Cores** - Insira um número de 2 a 256.<br>· **Lista de Cores** - Insira uma lista separada por vírgulas. Por exemplo, para branco, cinza e preto, digite `000000,888888,ffffff`.<br><br>Escolher **PDF**, **TIFF** ou **TIFF com alpha** fornece esta opção adicional:<br>· **Compactação** - Selecione um algoritmo de compactação. As opções de algoritmo para PDF são **None**, **Zip** e **Jpeg**; para TIFF, são **None**, **LZW**, **Jpeg** e **Zip**; e para TIFF com Alpha são **None**, **LZW** e **Zip**.<br><br>Escolher **PNG**, **PNG com Alpha** ou **EPS** não fornece opções adicionais. |
| **Nitidez** | Selecione **Habilitar Nitidez Simples** para aplicar um filtro de nitidez básico à imagem depois de todo o dimensionamento. A nitidez pode ajudar a compensar o desfoque que pode ocorrer ao exibir uma imagem de tamanho diferente. |

#### Opções da guia Avançadas {#advanced-tab-options}

<table>
 <tbody>
  <tr>
   <td><strong>Texto</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td><strong>Espaço de cor</strong></td>
   <td>Selecione <strong>RGB, CMYK</strong> ou <strong>Tons de cinza</strong> para o espaço de cores.</td>
  </tr>
  <tr>
   <td><strong>Perfil de cor</strong></td>
   <td>Selecione o perfil de espaço de cores de saída no qual você deseja converter o ativo se ele for diferente do perfil de trabalho.</td>
  </tr>
  <tr>
   <td><strong>Renderizar recuo</strong></td>
   <td>Você pode substituir a tentativa de renderização padrão. As tentativas de renderização determinam o que acontece com as cores que não podem ser reproduzidas no perfil de cores de destino (fora do gamut). A intenção de renderização é ignorada se não for compatível com o perfil ICC.
    <ul>
     <li>Selecione <strong>Perceptivo</strong> para compactar o gamut total de um espaço de cores em outro espaço de cores quando uma ou mais cores da imagem original estiverem fora do gamut do espaço de cores de destino.</li>
     <li>Selecione <strong>Colorimétrica relativa</strong> quando uma cor no espaço de cores atual estiver fora do gamut no espaço de cores de destino. E, você deseja mapeá-lo para a cor mais próxima possível dentro do gamut do espaço de cores de destino, sem afetar outras cores. </li>
     <li>Selecione <strong>Saturação</strong> se desejar reproduzir a saturação de cores da imagem original ao converter para o espaço de cores de destino. </li>
     <li>Selecione <strong>Colorimétrica Absoluta</strong> para combinar exatamente as cores sem nenhum ajuste para o ponto branco ou para o ponto preto, o que alteraria o brilho da imagem.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Compensação de pontos pretos</strong></td>
   <td>Selecione essa opção se o perfil de saída suportar esse recurso. A compensação de Blackpoint é ignorada se não for compatível com o perfil ICC especificado.</td>
  </tr>
  <tr>
   <td><strong>Pontilhamento</strong></td>
   <td>Selecione essa opção para possivelmente evitar ou reduzir artefatos de banda de cores. </td>
  </tr>
  <tr>
   <td><strong>Tipo de nitidez</strong></td>
   <td><p>Selecione <strong>Nenhum</strong>, <strong>Nitidez</strong> ou <strong>Tirar nitidez da máscara</strong>. </p>
    <ul>
     <li>Selecione <strong>Nenhum</strong> se desejar desabilitar a nitidez.</li>
     <li>Selecione <strong>Nitidez </strong>para aplicar um filtro de nitidez básico à imagem depois de todo o dimensionamento. A nitidez pode ajudar a compensar o desfoque que pode ocorrer ao exibir uma imagem de tamanho diferente. </li>
     <li>Selecione <strong> Tirar nitidez da máscara</strong> se desejar ajustar um efeito de filtro de nitidez na imagem final com resolução reduzida. É possível controlar a intensidade do efeito, o raio do efeito (medido em pixels) e um limite de contraste que é ignorado. Esse efeito usa as mesmas opções do filtro "Tirar nitidez da máscara" do Photoshop.</li>
    </ul> <p>Em <strong>Tirar nitidez da máscara</strong>, você tem as seguintes opções:</p>
    <ul>
     <li><strong>Quantidade</strong> - Controla a quantidade de contraste aplicada aos pixels de borda. O valor padrão do número real é 1,0. Para imagens de alta resolução, é possível aumentá-las para até 5,0. Pense na Quantidade como uma medida da intensidade do filtro.</li>
     <li><strong>Raio</strong> - Determina o número de pixels em torno dos pixels de borda que afetam a nitidez. Para imagens de alta resolução, digite um número real de 1 a 2. Um valor baixo aplica nitidez apenas aos pixels da borda; um valor alto aplica nitidez a uma faixa mais ampla de pixels. O valor correto depende do tamanho da imagem.</li>
     <li><strong>Limite</strong> - Determina o intervalo de contraste que deve ser ignorado quando o filtro Tirar nitidez da máscara for aplicado. Em outras palavras, essa opção determina o quão diferentes os pixels com nitidez devem ser da área ao redor antes de serem considerados pixels de borda e de serem nitidez. Para evitar a introdução de ruídos, experimente valores inteiros de 2 a 20. </li>
     <li><strong>Aplicar a</strong> - Determina se a desnitidez se aplica a cada cor ou brilho.</li>
    </ul>
    <div>
      A nitidez é descrita em
     <a href="https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html#dynamic-media">Usando nitidez de imagem com vídeo do Experience Manager Dynamic Media</a>, no tópico da Ajuda online <a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/using/master-files/sharpening-image.html#master-files">Nitidez de imagem</a> e em <a href="https://experienceleague.adobe.com/docs/dynamic-media-classic/assets/s7_sharpening_images.pdf">Práticas recomendadas para nitidez de imagens no PDF baixável do Dynamic Media Classic</a>.
    </div> </td>
  </tr>
  <tr>
   <td><strong>Modo de nova amostra</strong></td>
   <td>Selecione uma opção de <strong>Modo de reamostragem</strong>. Essas opções deixam a imagem mais nítida quando a resolução é reduzida:
    <ul>
     <li><strong>Bilinear</strong> - O método mais rápido de reamostragem. Alguns artefatos de suavização são visíveis.</li>
     <li><strong>Bi-Cubic</strong> - aumenta o uso do CPU, mas produz imagens mais nítidas com menos artefatos de suavização visíveis.</li>
     <li><strong>Sharp2</strong> - Pode produzir resultados ligeiramente mais nítidos do que o Bi-Cubic, mas com um custo de CPU ainda maior.</li>
     <li><strong>Bi-Sharp</strong> - Seleciona o reamostragem padrão do Photoshop para reduzir o tamanho da imagem, que é chamado de <strong>bicubic sharper</strong> no Adobe Photoshop.</li>
     <li><strong>Cada Cor</strong> e <strong>Brilho</strong> - cada método pode ser baseado em cor ou brilho. Por padrão, <strong>cada Cor</strong> está selecionada.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Resolução de impressão</strong></td>
   <td>Selecione uma resolução para imprimir esta imagem; o padrão é 72 pixels.</td>
  </tr>
  <tr>
   <td><strong>Modificador de imagem</strong></td>
   <td><p>Além das configurações de imagem comuns disponíveis na interface, o Dynamic Media oferece suporte a várias modificações de imagem avançadas que você pode especificar no campo <strong>Modificadores de imagem</strong>. Estes parâmetros são definidos na <a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/syntax-and-features/image-serving-http/c-command-overview.html">referência de comando do Protocolo do Servidor de Imagens</a>.</p> <p>Importante: a seguinte funcionalidade listada na API não é compatível:</p>
    <ul>
     <li>Modelos básicos e comandos de renderização de texto: <code>text= textAngle= textAttr= textFlowPath= textFlowXPath= textPath=</code> e <code>textPs=</code></li>
     <li>Comandos de localização: <code>locale=</code> e <code>req=xlate</code></li>
     <li><code>req=set</code> não está disponível para uso geral.</li>
     <li><code>req=mbrset</code></li>
     <li><code>req=saveToFile</code></li>
     <li><code>req=targets</code></li>
     <li><code>template=</code></li>
     <li>Serviços Dynamic Media não essenciais: SVG, renderização de imagem e Web-to-Print</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Definir opções de predefinição de imagem com modificadores de imagem {#defining-image-preset-options-with-image-modifiers}

Além das opções disponíveis nas guias Básico e Avançado, é possível definir modificadores de imagem para oferecer mais opções ao definir predefinições de imagens. A Renderização de Imagens depende da API de Renderização de Imagens do Dynamic Media e é definida em detalhes na [Referência do Protocolo HTTP](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-rendering-api/http-protocol-reference/c-ir-introduction.html#image-rendering-api).

A seguir estão alguns exemplos básicos do que você pode fazer com modificadores de imagem.

>[!NOTE]
>
>Alguns modificadores de imagem [ não podem ser usados em Experience Manager](#advanced-tab-options).

* [op_invert](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-invert.html) - Inverte cada componente de cor para um efeito de imagem negativo.

  ```xml {.line-numbers}
  &op_invert=1
  ```

  ![6_5_imagepreset-edit-invert](assets/6_5_imagepreset-edit-invert.png)

* [op_blur](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-blur.html) - Aplica um filtro de desfoque à imagem.

  ```xml {.line-numbers}
  &op_blur=7
  ```

  ![6_5_imagepreset-edit-blur](assets/6_5_imagepreset-edit-blur.png)

* Comandos combinados - op_blur e op-invert

  ```xml {.line-numbers}
  &op_invert=1&op_blur=7
  ```

  ![chlimage_1-80](assets/chlimage_1-501.png)

* [op_brightness](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-op-brightness.html) - Diminui ou aumenta o brilho.

  ```xml {.line-numbers}
  &op_brightness=58
  ```

  ![6_5_imagepreset-edit-brightness](assets/6_5_imagepreset-edit-brightness.png)

* [opac](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-opac.html) - Ajusta a opacidade da imagem. Permite diminuir a opacidade do primeiro plano.

  ```xml {.line-numbers}
  opac=29
  ```

  ![6_5_imagepreset-edit-opacity](assets/6_5_imagepreset-edit-opacity.png)

### Editar predefinições de imagem {#modifying-image-presets}

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Predefinições de imagem]**.

   ![6_5_imagepreset-editpreset](assets/6_5_imagepreset-editpreset.png)

1. Selecione uma predefinição e, em seguida, **[!UICONTROL Editar]**. A janela **[!UICONTROL Editar predefinição de imagem]** é aberta.
1. Faça alterações e selecione **[!UICONTROL Salvar]** para salvar as alterações ou **[!UICONTROL Cancelar]** para cancelar as alterações.

### Predefinições de imagem do Publish {#publishing-image-presets}

As predefinições de imagem são publicadas automaticamente.

### Excluir predefinições de imagem {#deleting-image-presets}

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global e selecione o ícone Ferramentas.
1. Navegue até **[!UICONTROL Assets]** > **[!UICONTROL Predefinições de imagem]**.
1. Selecione uma predefinição e, em seguida, **[!UICONTROL Excluir]**. O Dynamic Media confirma que você deseja excluí-lo. Selecione **[!UICONTROL Excluir]** para remover ou selecione **[!UICONTROL Cancelar]** para retornar às Predefinições de Imagem.
