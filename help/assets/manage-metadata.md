---
title: Gerencie metadados de seus ativos digitais no [!DNL Adobe Experience Manager].
description: Saiba mais sobre os tipos de metadados e [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] como tornar possível organizar e processar ativos automaticamente com base em seus metadados.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 643d31998989e9ebe73e124313379fb64ec86cd5
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 5%

---


# Gerenciar metadados de seus ativos digitais {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] mantém metadados para cada ativo. Permite a categorização e organização mais fáceis de ativos e ajuda as pessoas que estão procurando um ativo específico. Com a capacidade de extrair metadados de arquivos carregados para [!DNL Experience Manager Assets], o gerenciamento de metadados se integra ao fluxo de trabalho criativo. Com a capacidade de manter e gerenciar metadados com seus ativos, você pode organizar e processar automaticamente ativos com base em seus metadados.

>[!MORELIKETHIS]
>
>* [Metadados XMP](xmp-metadata.md)
>* [How to edit or add metadata](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## Por que precisamos de metadados {#why-metadata}

Metadados significa dados sobre dados. Nesse sentido, os dados se referem ao seu ativo digital, digamos uma imagem. Metadata is critical for efficient asset management.

Metadados é a coleta de todos os dados disponíveis para um ativo, mas não necessariamente contidos nessa imagem. Some examples of metadata are:

* Nome do ativo.
* Hora e data da última modificação.
* Size of the asset as it was stored in the repository.
* Nome da pasta em que está contido.
* Ativos relacionados ou tags aplicadas.

As informações acima são as propriedades básicas de metadados que [!DNL Experience Manager] podem ser gerenciadas para ativos, o que permite que os usuários vejam todos os ativos. Por exemplo, ordenar ativos pela última data de modificação é útil ao tentar descobrir ativos adicionados recentemente.

Você pode adicionar mais dados de alto nível a ativos digitais, por exemplo:

* Tipo de ativo (é uma imagem, um vídeo, um clipe de áudio ou um documento?).
* Proprietário do ativo.
* Título do ativo.
* Descrição do ativo.
* Tags atribuídas a um ativo.

Mais metadados ajudam a categorizar ativos e são úteis à medida que a quantidade de informações digitais cresce. É possível gerenciar algumas centenas de arquivos com base apenas nos nomes dos arquivos. No entanto, essa abordagem não é escalável. Fica aquém quando o número de pessoas envolvidas e o número de ativos gerenciados aumenta.

Com a adição de metadados, o valor de um ativo digital cresce, pois o ativo se torna,

* Mais acessível - os sistemas e usuários podem encontrá-lo facilmente.
* Mais fácil de gerenciar - você pode encontrar ativos com o mesmo conjunto de propriedades mais facilmente e aplicar alterações a eles.
* Concluído - o ativo traz mais informações e contexto com mais metadados.

Por esses motivos, [!DNL Assets] fornece os meios certos de criar, gerenciar e trocar metadados para seus ativos digitais.

## Tipos de metadados {#types-of-metadata}

Os dois tipos básicos de metadados são metadados técnicos e metadados descritivos.

Os metadados técnicos são úteis para aplicativos de software que lidam com ativos digitais e não devem ser mantidos manualmente. [!DNL Experience Manager Assets] e outros softwares determinam automaticamente os metadados técnicos e os metadados podem mudar quando o ativo é modificado. Os metadados técnicos disponíveis de um ativo dependem em grande parte do tipo de arquivo do ativo. Alguns exemplos de metadados técnicos são:

* Tamanho de um arquivo.
* Dimensões (altura e largura) de uma imagem.
* Taxa de bits de um arquivo de áudio ou vídeo.
* Resolução (nível de detalhes) de uma imagem.

Metadados descritivos são metadados relacionados ao domínio do aplicativo, por exemplo, o negócio de onde um ativo vem. Metadados descritivos não podem ser determinados automaticamente. É criado manual ou semiautomaticamente. Por exemplo, uma câmera habilitada para GPS pode rastrear automaticamente a latitude e a longitude e adicionar geolocalização da imagem.

O custo da criação manual de informações descritivas de metadados é alto. Assim, os padrões são estabelecidos para facilitar a troca de metadados entre sistemas de software e organizações. [!DNL Experience Manager Assets] oferece suporte a todas as normas relevantes para o gerenciamento de metadados.

## Padrões de codificação {#encoding-standards}

Há várias maneiras de incorporar metadados em arquivos. Há suporte para uma seleção de padrões de codificação:

* XMP: usado por [!DNL Assets] para armazenar os metadados extraídos no repositório.
* ID3: para arquivos de áudio e vídeo.
* Exif: para arquivos de imagem.
* Outro/Legado: de [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]e assim por diante.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) é um padrão aberto usado por todos [!DNL Experience Manager Assets] o gerenciamento de metadados. A codificação padrão de metadados universais do oferta que pode ser incorporada em todos os formatos de arquivo. A Adobe e outras empresas oferecem suporte ao padrão XMP, pois fornece um modelo de conteúdo avançado. Os usuários do padrão XMP e do [!DNL Experience Manager Assets] têm uma plataforma poderosa para aproveitar. For more information, see [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Os dados armazenados nessas tags ID3 são exibidos quando você reproduz um arquivo de áudio digital em seu computador ou em um player MP3 portátil.

As tags ID3 foram projetadas para o formato de arquivo MP3. Informações adicionais sobre formatos:

* As tags ID3 funcionam em arquivos MP3 e mp3PRO.
* WAV não tem tags.
* O WMA tem tags proprietárias que não permitem a implementação de código aberto.
* Ogg Vorbis usa Comentários Xiph incorporados ao container Ogg.
* O AAC usa um formato de marcação proprietário.

### Exif {#exif}

O formato de arquivo de imagem permutável (Exif) é o formato de metadados mais popular usado na fotografia digital. Ele fornece uma maneira de incorporar um vocabulário fixo de propriedades de metadados em muitos formatos de arquivo, como JPEG, TIFF, RIFF e WAV. O Exif armazena metadados como pares de um nome de metadados e um valor de metadados. Esses pares de nome-valor de metadados também são chamados de tags, para não serem confundidos com a marcação em [!DNL Experience Manager]. As câmeras digitais modernas criam metadados Exif e softwares gráficos modernos suportam isso. O formato Exif é o menor denominador comum para o gerenciamento de metadados, especialmente para imagens.

Uma grande limitação do Exif é que alguns formatos de arquivo de imagem populares, como BMP, GIF ou PNG, não são compatíveis.

Os campos de metadados definidos pela Exif são tipicamente de natureza técnica e têm uso limitado para o gerenciamento descritivo de metadados. Por esse motivo, o [!DNL Experience Manager Assets] oferta mapeia as propriedades Exif em esquemas [de metadados](metadata-schemas.md) comuns e em XMP.

#### Outros metadados {#other-metadata}

Outros metadados que podem ser incorporados de arquivos incluem [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel]etc.

## Gerenciar metadados de seus ativos digitais {#manage-assets-metadata}

Os ativos do Enterprise Manager permitem que você edite os metadados de vários ativos simultaneamente para que possa propagar rapidamente alterações comuns de metadados para ativos em massa. Use a página [!UICONTROL Propriedades] para alterar as propriedades de metadados para um valor comum ou adicionar ou modificar tags. Para personalizar a página Propriedades de metadados, incluindo adicionar, modificar e excluir propriedades de metadados, use o editor de Schemas.

>[!NOTE]
>
>Os métodos de edição em massa funcionam para ativos disponíveis em uma pasta ou coleção. Para os ativos que estão disponíveis em pastas ou que correspondem a critérios comuns, é possível atualizar [em massa os metadados após a pesquisa](/help/assets/search-assets.md#metadataupdates).

1. Navegue até o local dos ativos que deseja editar.
1. Selecione os ativos para os quais deseja editar propriedades comuns.
1. Na barra de ferramentas, toque/clique em **[!UICONTROL Propriedades]** para abrir a página [!UICONTROL Propriedades] dos ativos selecionados.

   >[!NOTE]
   >
   >Quando você seleciona vários ativos, o formulário pai comum mais baixo é selecionado para os ativos. Em outras palavras, a página [!UICONTROL Propriedades] exibe apenas os campos de metadados comuns nas páginas [!UICONTROL Propriedades] de todos os ativos individuais.

1. Modifique as propriedades de metadados para ativos selecionados nas várias guias.
1. Para visualização do editor de metadados para um ativo específico, desmarque os ativos restantes na lista. Os campos do editor de metadados são preenchidos com os metadados do ativo específico.

   >[!NOTE]
   >
   >* Na página [!UICONTROL Propriedades] , é possível remover ativos da lista de ativos desmarcando-os. A lista do ativo tem todos os ativos selecionados por padrão. Os metadados dos ativos que você remove da lista não são atualizados.
   >* Na parte superior da lista de ativos, marque a caixa de seleção ao lado de **[!UICONTROL Título]** para alternar entre a seleção dos ativos e a limpeza da lista.


1. Para selecionar um schema de metadados diferente para os ativos, toque/clique em **[!UICONTROL Configurações]** na barra de ferramentas e selecione o schema desejado. Salve as alterações.
1. Para anexar os novos metadados aos existentes em campos que contêm vários valores, selecione o **[!UICONTROL Modo anexar]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Toque/clique em **[!UICONTROL Enviar]**.

   >[!CAUTION]
   >
   >Em campos de valor único, os novos metadados não são anexados ao valor existente no campo mesmo se você selecionar o **[!UICONTROL Modo anexar]**.

## Configurar limite para atualização de metadados em massa {#configlimit}

Para evitar uma situação semelhante ao DOS, o AEM limita o número de parâmetros suportados em uma solicitação Sling. Ao atualizar metadados de muitos ativos de uma só vez, você pode atingir o limite e os metadados não são atualizados para mais ativos. O AEM gera o seguinte aviso nos registros:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Para alterar o limite, acesse o Console da Web (**[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**) e altere o valor de **[!UICONTROL Parâmetros de POST máximo]** na configuração OSGi da **[!UICONTROL Manipulação de parâmetro da solicitação do Apache]**.

## Esquemas de metadados {#metadata-schemata}

Os schemas de metadados são conjuntos predefinidos de definições de propriedade de metadados que podem ser usados em vários aplicativos. As propriedades estão sempre associadas a um ativo, o que significa que as propriedades são &#39;sobre&#39; o recurso.

Você também pode projetar seus próprios esquemas de metadados se não houver nenhum que atenda às suas necessidades. Não duplicado informações existentes. Em uma organização, a separação de esquemas facilita o compartilhamento de metadados. [!DNL Experience Manager] fornece uma lista padrão dos esquemas de metadados mais populares. A lista ajuda você a iniciar rapidamente sua estratégia de metadados e a escolher rapidamente as propriedades de metadados de que você precisa.

Os esquemas de metadados suportados estão listados abaixo.

### Metadados padronizados {#standard-metadata}

* DC - [!DNL Dublin Core] é um conjunto importante e amplamente utilizado de metadados.
* DICOM - Digital Imaging and Communications in Medicine (Imagem digital e comunicações em medicina).
* `Iptc4xmpCore` e `iptc4xmpExt` - O International Press Communications Standard contém muitos metadados específicos para cada assunto.
* RDF - Estrutura de Descrição do Recurso - para metadados semânticos genéricos da Web.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Ingresso no Serviço Básico.

### Metadados específicos do aplicativo {#application-specific-metadata}

Os metadados específicos do aplicativo incluem metadados técnicos e descritivos. Se você usar esses metadados, outros aplicativos talvez não consigam usá-los. Por exemplo, um aplicativo de renderização de imagem diferente pode não conseguir acessar [!DNL Adobe Photoshop] metadados. Você pode criar uma etapa de fluxo de trabalho que altera uma propriedade específica do aplicativo para uma propriedade padrão.

* ACDSee - Metadados gerenciados pelo [!DNL ACDSee] programa. Consulte [www.acdsee.com/](https://www.acdsee.com/).
* Álbum - [!DNL Adobe Photoshop Album].
* CQ - Usado por [!DNL Experience Manager Assets].
* DAM - Usado por [!DNL Experience Manager Assets].
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html) é uma coleção de ferramentas para gerenciamento de metadados e arquivos para sistemas operacionais Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto e MP - Microsoft Photo.
* PDF e PDF/X.
* Photoshop e psAux - [!DNL Adobe Photoshop].

### Metadados do Gerenciamento de direitos digitais {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - Sistema [Universal de Licenciamento de](https://www.useplus.com)Imagens.
* PRISM - Requisitos de [publicação para metadados](https://www.idealliance.org/prism-metadata)padrão do setor.
* PRL - Idioma dos Direitos do PRISM.
* PUR - Direitos de uso do PRISM.
* `xmpPlus` - Integração da PLUS com a XMP.

### Metadados específicos da fotografia {#photography-specific-metadata}

* Exif - Informações técnicas da câmera, incluindo a posição GPS.
* CRS - [!DNL Camera Raw] schema.
* `iptc4xmpCore` e `iptc4xmpExt`.
* TIFF - metadados de imagem (não apenas para imagens TIFF).

### Metadados específicos para impressão {#print-specific-metadata}

* PDF e PDF/X - Adobe PDF e aplicativos de terceiros.
* PRISM - Requisitos de [publicação para metadados](https://www.prismstandard.org)padrão do setor.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - Metadados XMP para texto paginado.

### Metadados específicos de multimídia {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gerenciamento de mídia.

## workflows orientados por metadados {#metadata-driven-workflows}

A criação de workflows orientados por metadados ajuda a automatizar alguns processos, o que aumenta a eficiência. Em um fluxo de trabalho controlado por metadados, o sistema de gerenciamento de fluxo de trabalho lê o fluxo de trabalho e, como resultado, executa alguma ação predefinida. Por exemplo, algumas maneiras de usar workflows orientados por metadados:

* O fluxo de trabalho pode verificar se uma imagem tem um título ou não. Caso contrário, o sistema notifica para adicionar um título.
* O fluxo de trabalho pode verificar se um aviso de direitos autorais em um ativo permite distribuição ou não. Portanto, o sistema envia o ativo para um servidor ou outro.
* Um fluxo de trabalho pode verificar ativos sem metadados obrigatórios e predefinidos ou ativos com metadados *inválidos* .
