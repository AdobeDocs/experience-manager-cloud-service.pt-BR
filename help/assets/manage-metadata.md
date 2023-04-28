---
title: Gerenciar metadados de ativos digitais
description: Saiba mais sobre os tipos de metadados e como [!DNL Adobe Experience Manager Assets] O ajuda a gerenciar metadados de ativos para permitir a categorização e a organização mais fáceis de ativos. [!DNL Experience Manager] possibilita organizar e processar ativos automaticamente com base em seus metadados.
contentOwner: AG
mini-toc-levels: 1
feature: Asset Management,Metadata
role: User,Architect,Admin
exl-id: 73a82bc2-1dda-4090-b7ee-29d1a632ba25
source-git-commit: 91af800c8b2f83e689e057f304a8e144ae4cc5ed
workflow-type: tm+mt
source-wordcount: '1981'
ht-degree: 8%

---

# Gerenciar metadados dos ativos digitais {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] mantém metadados para cada ativo. Ela facilita a categorização e a organização de ativos e ajuda as pessoas que estão procurando por um ativo específico. Com a capacidade de extrair metadados de arquivos carregados para o [!DNL Experience Manager Assets], o gerenciamento de metadados é integrado ao fluxo de trabalho criativo. Com a capacidade de manter e gerenciar metadados com seus ativos, você pode organizar e processar ativos automaticamente com base em seus metadados.

<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## Por que precisamos de metadados {#why-metadata}

Metadados significa dados sobre dados. Nesse sentido, os dados se referem ao seu ativo digital, digamos uma imagem. Os metadados são essenciais para um gerenciamento eficiente de ativos.

Metadados é a coleção de todos os dados disponíveis para um ativo, mas que não estão necessariamente contidos nessa imagem. Alguns exemplos de metadados são:

* Nome do ativo.
* Hora e data da última modificação.
* Tamanho do ativo como ele foi armazenado no repositório.
* Nome da pasta na qual ele está contido.
* Ativos relacionados ou tags aplicadas.

Estas são as propriedades básicas de metadados que [!DNL Experience Manager] O pode gerenciar para ativos, o que permite que os usuários vejam todos os ativos. Por exemplo, solicitar ativos por data de última modificação é útil ao tentar descobrir ativos adicionados ou modificados recentemente.

Você pode adicionar mais dados de alto nível aos ativos digitais, por exemplo:

* Tipo de ativo (é uma imagem, um vídeo, um clipe de áudio ou um documento?).
* Proprietário do ativo.
* Título do ativo.
* Descrição do ativo.
* Tags atribuídas a um ativo.

Mais metadados ajudam a categorizar ativos e são úteis à medida que a quantidade de informações digitais aumenta. É possível gerenciar algumas centenas de arquivos com base apenas nos nomes de arquivo. No entanto, essa abordagem não é escalável. Fica aquém do aumento do número de pessoas envolvidas e do número de ativos gerenciados.

Com a adição de metadados, o valor de um ativo digital cresce, porque o ativo se torna,

* Mais acessível — os sistemas e usuários podem encontrá-lo facilmente.
* Mais fácil de gerenciar — é possível encontrar ativos com o mesmo conjunto de propriedades mais facilmente e realizar alterações neles.
* Completo — o ativo carrega mais informações e contexto com mais metadados.

Por estas razões, [!DNL Assets] O fornece o meio certo para criar, gerenciar e trocar metadados para seus ativos digitais.

## Tipos de metadados {#types-of-metadata}

Os dois tipos básicos de metadados são metadados técnicos e descritivos.

Os metadados técnicos são úteis para aplicativos de software que lidam com ativos digitais e não devem ser mantidos manualmente. [!DNL Experience Manager Assets] e outros softwares determinam automaticamente os metadados técnicos e podem mudar quando o ativo é modificado. Os metadados técnicos disponíveis de um ativo dependem principalmente do tipo de arquivo do ativo. Alguns exemplos de metadados técnicos são:

* Tamanho de um arquivo.
* Dimension (altura e largura) de uma imagem.
* Taxa de bits de um arquivo de áudio ou vídeo.
* Resolução (nível de detalhes) de uma imagem.

Os metadados descritivos são metadados relacionados ao domínio do aplicativo, por exemplo, o negócio de onde um ativo vem. Metadados descritivos não podem ser determinados automaticamente. Ele é criado manual ou semiautomaticamente. Por exemplo, uma câmera ativada por GPS pode rastrear automaticamente a latitude e a longitude e adicionar geotag à imagem.

O custo de criar manualmente informações de metadados descritivos é alto. Assim, os padrões são estabelecidos para facilitar a troca de metadados entre sistemas e organizações de software. [!DNL Experience Manager Assets] O suporta todas as normas relevantes para a gestão de metadados.

## Metadados e última modificação {#last-modification}

A última data modificada de um ativo reflete a última vez que o arquivo original de um ativo é modificado. Como resultado, a data de modificação e o usuário só são alterados quando:

* Uma nova versão do ativo é carregada
* Um ativo é reprocessado

A última data de modificação e o usuário não muda:

* Quando um ativo é movido ou renomeado
* Quando um ativo é finalizado, há check-in ou versão
* Quando um ativo é publicado ou não
* Em atualizações de metadados
* Atualizações de referência ou coleção

## Padrões de codificação {#encoding-standards}

Há várias maneiras de incorporar metadados em arquivos. Há suporte para uma seleção de padrões de codificação:

* XMP: usado por [!DNL Assets] para armazenar os metadados extraídos no repositório.
* ID3: para arquivos de áudio e vídeo.
* Exif: para arquivos de imagem.
* Outro/Legado: from [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]e assim por diante.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) é uma norma aberta usada por [!DNL Experience Manager Assets] para toda a gestão de metadados. O padrão oferece codificação de metadados universais que podem ser incorporados em todos os formatos de arquivo. O Adobe e outras empresas oferecem suporte XMP padrão, pois fornece um modelo de conteúdo avançado. Usuários XMP padrão e de [!DNL Experience Manager Assets] tenha uma plataforma poderosa para desenvolver. Para obter mais informações, consulte [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Os dados armazenados nessas tags ID3 são exibidos quando você reproduz um arquivo de áudio digital em seu computador ou em um player MP3 portátil.

As tags ID3 foram projetadas para o formato de arquivo MP3. Informações adicionais sobre formatos:

* As tags ID3 funcionam em arquivos MP3 e mp3PRO.
* O WAV não tem tags.
* O WMA tem tags proprietárias que não permitem implementação de código aberto.
* O Ogg Vorbis usa Comentários Xiph incorporados no contêiner Ogg.
* O AAC usa um formato de marcação proprietário.

### Exif {#exif}

O formato de arquivo de imagem permutável (Exif) é o formato de metadados mais popular usado em fotografia digital. Ele fornece uma maneira de incorporar um vocabulário fixo de propriedades de metadados em muitos formatos de arquivo, como JPEG, TIFF, RIFF e WAV. O Exif armazena metadados como pares de um nome de metadados e um valor de metadados. Esses pares nome-valor-metadados também são chamados de tags, não devem ser confundidos com a marcação em [!DNL Experience Manager]. Câmeras digitais modernas criam metadados Exif e softwares gráficos modernos suportam isso. O formato Exif é o menor denominador comum para o gerenciamento de metadados, especialmente para imagens.

Uma grande limitação do Exif é que alguns formatos de arquivo de imagem populares, como BMP, GIF ou PNG, não o suportam.

Os campos de metadados definidos pela Exif normalmente têm natureza técnica e são de uso limitado para o gerenciamento de metadados descritivos. Por isso, [!DNL Experience Manager Assets] O oferece mapeamento das propriedades Exif em [esquemas de metadados comuns](metadata-schemas.md) e no XMP.

#### Outros metadados {#other-metadata}

Outros metadados que podem ser incorporados de arquivos incluem [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]e assim por diante.

## Gerenciar metadados dos ativos digitais {#manage-assets-metadata}

O Enterprise Manager Assets permite editar os metadados de vários ativos simultaneamente, para que você possa propagar rapidamente alterações de metadados comuns a ativos em massa. Use o [!UICONTROL Propriedades] para alterar as propriedades dos metadados para um valor comum ou adicionar ou modificar tags. Para personalizar a página Propriedades dos metadados, incluindo adicionar, modificar e excluir propriedades dos metadados, use o Editor de esquemas.

>[!NOTE]
>
>Os métodos de edição em massa funcionam para ativos disponíveis em uma pasta ou coleção. Para os ativos que estão disponíveis em pastas ou que correspondem a um critério comum, é possível [atualização em massa dos metadados após a pesquisa](/help/assets/search-assets.md#metadata-updates).

1. Navegue até o local dos ativos que deseja editar.
1. Selecione os ativos para os quais deseja editar propriedades comuns.
1. Na barra de ferramentas, toque/clique **[!UICONTROL Propriedades]** para abrir o [!UICONTROL Propriedades] para os ativos selecionados.

   >[!NOTE]
   >
   >Ao selecionar vários ativos, o formulário pai comum mais baixo é selecionado para os ativos. Em outras palavras, a variável [!UICONTROL Propriedades] A página exibe somente campos de metadados comuns em [!UICONTROL Propriedades] páginas de todos os ativos individuais.

1. Modifique as propriedades de metadados para ativos selecionados nas várias guias.
1. Para exibir o editor de metadados para um ativo específico, cancele a seleção dos ativos restantes na lista. Os campos do editor de metadados são preenchidos com os metadados do ativo específico.

   >[!NOTE]
   >
   >* No [!UICONTROL Propriedades] você pode remover ativos da lista de ativos cancelando a seleção. A lista de ativos tem todos os ativos selecionados por padrão. Os metadados dos ativos que você remove da lista não são atualizados.
   >* Na parte superior da lista de ativos, marque a caixa de seleção ao lado de **[!UICONTROL Título]** para alternar entre selecionar os ativos e limpar a lista.


1. Para selecionar um esquema de metadados diferente para os ativos, toque/clique **[!UICONTROL Configurações]** na barra de ferramentas e selecione o schema desejado. Salve as alterações.
1. Para anexar os novos metadados aos existentes em campos que contêm vários valores, selecione o **[!UICONTROL Modo anexar]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Toque/clique em **[!UICONTROL Enviar]**.

   >[!CAUTION]
   >
   >Em campos de valor único, os novos metadados não são anexados ao valor existente no campo mesmo se você selecionar o **[!UICONTROL Modo anexar]**.

## Metadados personalizados usando o perfil de processamento {#metadata-compute-service}

Ativos como [!DNL Cloud Service] podem gerar metadados personalizados para um ativo usando serviços nativos em nuvem. Configure um perfil de processamento para gerar metadados personalizados. Consulte [como usar o perfil de processamento](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

![Representação de metadados no perfil de processamento](assets/processing-profile-metadata.png)

>[!TIP]
>
>Somente um perfil de processamento pode ser aplicado a uma pasta. Para aplicar vários processos a ativos em uma pasta, adicione mais opções a um único perfil de processamento. Por exemplo, um único perfil pode gerar representações, transcodificar ativos, gerar metadados personalizados e assim por diante. Você pode aplicar filtros de tipo MIME para cada tarefa para que a tarefa apropriada seja acionada para o formato de arquivo necessário.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Configure limit for bulk metadata update {#configlimit}

To prevent DOS-like situation, [!DNL Experience Manager] limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. [!DNL Experience Manager] generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access Web Console ( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**) and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.
-->

## Esquemas de metadados {#metadata-schemata}

Os esquemas de metadados são conjuntos predefinidos de definições de propriedades de metadados que podem ser usadas em vários aplicativos. As propriedades são sempre associadas a um ativo, o que significa que as propriedades são &quot;sobre&quot; o recurso.

Você também pode criar seus próprios esquemas de metadados se não existir nenhum que atenda às suas necessidades. Não duplique as informações existentes. Em uma organização, separar esquemas facilita o compartilhamento de metadados. [!DNL Experience Manager] O fornece uma lista padrão dos esquemas de metadados mais populares. A lista ajuda você a iniciar rapidamente sua estratégia de metadados e escolher rapidamente as propriedades de metadados necessárias.

Os esquemas de metadados compatíveis estão listados abaixo.

### Metadados padrão {#standard-metadata}

* DC - [!DNL Dublin Core] O é um conjunto de metadados importante e amplamente usado.
* DICOM - Digital Imaging and Communications in Medicine (Imagem digital e comunicações em medicina).
* `Iptc4xmpCore` e `iptc4xmpExt` - O International Press Communications Standard contém muitos metadados específicos de assunto.
* RDF - Estrutura de Descrição do Recurso - para metadados semanticos da Web genéricos.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Bilhete básico de trabalho.

### Metadados específicos do aplicativo {#application-specific-metadata}

Os metadados específicos do aplicativo incluem metadados técnicos e descritivos. Se você usar esses metadados, outros aplicativos talvez não consigam usá-los. Por exemplo, um aplicativo de renderização de imagem diferente pode não ser capaz de acessar [!DNL Adobe Photoshop] metadados. Você pode criar uma etapa de fluxo de trabalho que altera uma propriedade específica do aplicativo para uma propriedade padrão.

* ACDSee - Metadados gerenciados pelo [!DNL ACDSee] programa. Consulte [www.acdsee.com/](https://www.acdsee.com/).
* Álbum - [!DNL Adobe Photoshop Album].
* CQ - Usado por [!DNL Experience Manager Assets].
* DAM - Usado por [!DNL Experience Manager Assets].
* DEX - [Explorador de descrição do Optima SC](https://www.optimasc.com/products/dex/index.html) é uma coleção de ferramentas para metadados e gerenciamento de arquivos para sistemas operacionais Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto e MP - Foto do Microsoft.
* PDF e PDF/X.
* Photoshop e psAux - [!DNL Adobe Photoshop].

### Metadados de Digital Rights Management {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* MAIS - [Sistema Universal de Licenciamento de Imagens](https://www.useplus.com).
* PRISMO - [Requisitos de publicação para metadados padrão do setor](https://www.idealliance.org/prism-metadata).
* PRL - Linguagem de direitos PRISM.
* PUR - Direitos de uso do PRISM.
* `xmpPlus` - Integração da PLUS com a XMP.

### Metadados específicos da fotografia {#photography-specific-metadata}

* Exif - Informações técnicas da câmera, incluindo a posição GPS.
* CRS - [!DNL Camera Raw] esquema.
* `iptc4xmpCore` e `iptc4xmpExt`.
* TIFF - metadados de imagem (não apenas para imagens TIFF).

### Metadados específicos para impressão {#print-specific-metadata}

* PDF e PDF/X - Adobe PDF e aplicativos de terceiros.
* PRISMO - [Requisitos de publicação para metadados padrão do setor](https://www.idealliance.org/prism-metadata).
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - XMP metadados para texto paginado.

### Metadados específicos de multimídia {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gerenciamento de mídia.

## Fluxos de trabalho orientados por metadados {#metadata-driven-workflows}

A criação de fluxos de trabalho orientados por metadados ajuda a automatizar alguns processos, o que melhora a eficiência. Em um fluxo de trabalho orientado por metadados, o sistema de gerenciamento de fluxo de trabalho lê o fluxo de trabalho e, como resultado, executa alguma ação predefinida. Por exemplo, algumas das maneiras de usar workflows orientados por metadados:

* O fluxo de trabalho pode verificar se uma imagem tem um título ou não. Caso contrário, o sistema notifica para adicionar um título.
* O workflow pode verificar se um aviso de copyright em um ativo permite distribuição ou não. Assim, o sistema envia o ativo para um servidor ou outro.
* Um fluxo de trabalho pode verificar ativos sem metadados obrigatórios predefinidos ou ativos com *inválido* metadados.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Metadados XMP](xmp-metadata.md)
>* [Como editar ou adicionar metadados](meta-edit.md)

