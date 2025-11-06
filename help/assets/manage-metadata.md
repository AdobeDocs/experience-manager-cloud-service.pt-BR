---
title: Gerenciar metadados de ativos digitais
description: Saiba mais sobre os tipos de metadados e como o [!DNL Adobe Experience Manager Assets] ajuda a gerenciar metadados de ativos para facilitar a categorização e a organização de ativos.O  [!DNL Experience Manager] permite organizar e processar ativos automaticamente com base em seus metadados.
contentOwner: AG
mini-toc-levels: 1
feature: Asset Management, Metadata
role: User, Developer, Admin
exl-id: 73a82bc2-1dda-4090-b7ee-29d1a632ba25
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 8%

---

# Gerencie metadados de seus ativos digitais {#managing-metadata-for-digital-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/metadata.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

[!DNL Adobe Experience Manager Assets] mantém metadados para cada ativo. Ele facilita a categorização e a organização de ativos e ajuda as pessoas que estão procurando um ativo específico. Com a capacidade de extrair metadados de arquivos carregados para o [!DNL Experience Manager Assets], o gerenciamento de metadados integra-se ao fluxo de trabalho criativo. Com a capacidade de manter e gerenciar metadados com seus ativos, você pode organizar e processar ativos automaticamente com base nos metadados.

<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## Por que precisamos de metadados {#why-metadata}

Metadados são dados sobre dados. A este respeito, os dados se referem ao seu ativo digital, digamos uma imagem. Os metadados são essenciais para o gerenciamento eficiente de ativos.

Os metadados são a coleção de todos os dados disponíveis para um ativo, mas que não estão necessariamente contidos nessa imagem. Alguns exemplos de metadados são:

* Nome do ativo.
* Hora e data da última modificação.
* Tamanho do ativo conforme foi armazenado no repositório.
* Nome da pasta na qual ele está contido.
* Ativos relacionados ou tags aplicadas.

As propriedades de metadados básicas que [!DNL Experience Manager] pode gerenciar para ativos, o que permite que os usuários vejam todos os ativos. Por exemplo, solicitar ativos pela última data de modificação é útil ao tentar descobrir ativos adicionados ou modificados recentemente.

Você pode adicionar mais dados de alto nível aos ativos digitais, por exemplo:

* Tipo de ativo (é uma imagem, um vídeo, um clipe de áudio ou um documento?)
* Proprietário do ativo.
* Título do ativo.
* Descrição do ativo.
* Tags atribuídas a um ativo.

Mais metadados ajudam a categorizar os ativos e são úteis à medida que a quantidade de informações digitais cresce. É possível gerenciar algumas centenas de arquivos com base apenas nos nomes de arquivo. No entanto, essa abordagem não é escalável. Ela é limitada quando o número de pessoas envolvidas e o número de ativos gerenciados aumentam.

Com a adição de metadados, o valor de um ativo digital cresce, porque o ativo se torna,

* Mais acessível — os sistemas e usuários podem encontrá-lo facilmente.
* Mais fácil de gerenciar — é possível encontrar ativos com o mesmo conjunto de propriedades mais facilmente e realizar alterações neles.
* Completo — o ativo carrega mais informações e contexto com mais metadados.

Por esses motivos, o [!DNL Assets] fornece o meio certo de criar, gerenciar e trocar metadados para os seus ativos digitais.

## Tipos de metadados {#types-of-metadata}

Os metadados são classificados como Técnicos, Informativos e Administrativos.

### Metadados técnicos

Os metadados técnicos se concentram nos aspectos técnicos dos ativos digitais, fornecendo informações cruciais relacionadas com:

* Tamanho do arquivo
* Formato
* Resolução
* Dimensões
* Modo de cores

Esse tipo de metadados ajuda os usuários a entender e usar ativos digitais com eficiência.

### Metadados informativos

Os metadados informativos fornecem informações descritivas para aprimorar a compreensão do conteúdo, auxiliando na descoberta e pesquisa de conteúdo. Inclui palavras-chave, legendas e descrições. <br>Por exemplo, ao gerenciar um vídeo no Experience Manager Assets, podemos incluir os seguintes metadados informativos:

* **Palavras-chave**: marketing, lançamento de produto, promoção
* **Legenda**: apresentando nosso produto mais recente com excelentes recursos
* **Descrição**: uma visão geral detalhada do conteúdo do vídeo.

### Metadados administrativos

Os metadados administrativos tratam dos aspectos gerenciais dos ativos digitais. Ele garante o controle de acesso, a conformidade e o gerenciamento do ciclo de vida geral dos ativos no sistema de gerenciamento de ativos digitais. Inclui informações relacionadas com:

* Propriedade do ativo
* Direitos de uso
* Permissões
* Outros detalhes administrativos

Esse tipo de metadados garante o gerenciamento eficaz de ativos, o controle de acesso e a conformidade.

<!-- Learn more about [metadata best practices](metadata-best-practices.md) to manage your digital assets effectively. -->

<!-- The two basic types of metadata are technical metadata and descriptive metadata.

Technical metadata is useful for software applications that are dealing with digital assets and should not be maintained manually. [!DNL Experience Manager Assets] and other software automatically determine technical metadata and the metadata may change when the asset is modified. The available technical metadata of an asset depends largely on the file type of the asset. Some examples of technical metadata are:

* Size of a file.
* Dimensions (height and width) of an image.
* Bit rate of an audio or video file.
* Resolution (level of detail) of an image.

Descriptive metadata is metadata concerned with the application domain, for example, the business that an asset is coming from. Descriptive metadata cannot be determined automatically. It is created manually or semi-automatically. For example, a GPS-enabled camera can automatically track the latitude and longitude and add geotag the image.

The cost of manually creating descriptive metadata information is high. So, standards are established to ease the exchange of metadata across software systems and organizations. [!DNL Experience Manager Assets] supports all relevant standards for metadata management. -->

## Metadados e última modificação {#last-modification}

A data da última modificação de um ativo reflete a última vez que o arquivo original de um ativo é modificado. Como resultado, a data de modificação e o usuário só mudam quando:

* Uma nova versão do ativo é carregada
* Um ativo é reprocessado

A data da última modificação e o usuário não mudam:

* Quando um ativo é movido ou renomeado
* Quando é feito o check-out, check-in ou versão de um ativo
* Quando um ativo é publicado ou não
* Em atualizações de metadados
* Atualizações de referência ou coleção

## Padrões de codificação {#encoding-standards}

Há várias maneiras de incorporar metadados em arquivos. Uma seleção de padrões de codificação é compatível:

* XMP: usado por [!DNL Assets] para armazenar os metadados extraídos no repositório.
* ID3: para arquivos de áudio e vídeo.
* Exif: para arquivos de imagem.
* Outro/Herdado: de [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel] e assim por diante.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) é um padrão aberto usado por [!DNL Experience Manager Assets] para todo o gerenciamento de metadados. O padrão oferece codificação de metadados universais que pode ser incorporada em todos os formatos de arquivo. A Adobe e outras empresas oferecem suporte ao padrão XMP, pois ele fornece um modelo de conteúdo avançado. Os usuários do XMP Standard e do [!DNL Experience Manager Assets] têm uma plataforma eficiente com base na qual compilar. Para obter mais informações, consulte [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Os dados armazenados nessas tags de ID3 são exibidos ao reproduzir um arquivo de áudio digital no computador ou em um MP3 player portátil.

As tags ID3 foram criadas para o formato de arquivo MP3. Informações adicionais sobre formatos:

* As tags ID3 funcionam em arquivos MP3 e mp3PRO.
* O WAV não tem tags.
* O WMA tem tags proprietárias que não permitem a implementação de código aberto.
* Ogg Vorbis usa comentários Xiph incorporados no contêiner Ogg.
* A AAC usa um formato de marcação proprietário.

### Exif {#exif}

O formato de arquivo de imagem intercambiável (Exif) é o formato de metadados mais popular usado em fotografias digitais. Ele fornece uma maneira de incorporar um vocabulário fixo de propriedades de metadados em muitos formatos de arquivo, como JPEG, TIFF, RIFF e WAV. O Exif armazena metadados como pares de um nome de metadados e um valor de metadados. Esses pares de nome-valor de metadados também são chamados de marcas, para não serem confundidos com a marcação em [!DNL Experience Manager]. Câmeras digitais modernas criam metadados Exif e software de gráficos modernos suportam isso. O formato Exif é o menor denominador comum para o gerenciamento de metadados, especialmente para imagens.

Uma limitação importante do Exif é que alguns formatos de arquivo de imagem populares, como BMP, GIF ou PNG, não são compatíveis.

Os campos de metadados definidos pelo Exif são normalmente de natureza técnica e de uso limitado para a gestão de metadados descritivos. Por este motivo, [!DNL Experience Manager Assets] oferece o mapeamento de propriedades Exif em [esquema de metadados comuns](metadata-schemas.md) e em XMP.

#### Outros metadados {#other-metadata}

Outros metadados que podem ser inseridos de arquivos incluem [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel] e assim por diante.

## Gerencie metadados de seus ativos digitais {#manage-assets-metadata}

O Enterprise Manager Assets permite que você edite os metadados de vários ativos simultaneamente para que possa propagar rapidamente alterações de metadados comuns em ativos em massa. Use a página [!UICONTROL Propriedades] para alterar propriedades de metadados para um valor comum ou adicionar ou modificar marcas. Para personalizar a página Propriedades dos metadados, incluindo adição, modificação e exclusão de propriedades dos metadados, use o Editor de esquemas.

>[!NOTE]
>
>Os métodos de edição em massa funcionam para ativos disponíveis em uma pasta ou coleção. Para os ativos que estão disponíveis em pastas ou correspondem a um critério comum, é possível [atualizar os metadados em massa após a pesquisa](/help/assets/search-assets.md#metadata-updates).

1. Navegue até o local dos ativos que deseja editar.
1. Selecione os ativos para os quais deseja editar propriedades comuns.
1. Na barra de ferramentas, selecione **[!UICONTROL Propriedades]** para abrir a página [!UICONTROL Propriedades] dos ativos selecionados.

   >[!NOTE]
   >
   >Quando você seleciona vários ativos, o formulário principal comum mais baixo é selecionado para os ativos. Em outras palavras, a página [!UICONTROL Propriedades] exibe somente campos de metadados que são comuns nas páginas [!UICONTROL Propriedades] de todos os ativos individuais.

1. Modifique as propriedades de metadados dos ativos selecionados nas várias guias.
1. Para exibir o editor de metadados de um ativo específico, cancele a seleção dos ativos restantes na lista. Os campos do editor de metadados são preenchidos com os metadados do ativo específico.

   >[!NOTE]
   >
   >* Na página [!UICONTROL Propriedades], é possível remover ativos da lista de ativos, cancelando a seleção. A lista de ativos tem todos os ativos selecionados por padrão. Os metadados dos ativos removidos da lista não são atualizados.
   >* Na parte superior da lista de ativos, marque a caixa de seleção ao lado de **[!UICONTROL Título]** para alternar entre selecionar os ativos e limpar a lista.

1. Para selecionar um esquema de metadados diferente para os ativos, selecione **[!UICONTROL Configurações]** na barra de ferramentas e selecione o esquema desejado. Salve as alterações.
1. Para anexar os novos metadados aos existentes em campos que contêm vários valores, selecione o **[!UICONTROL Modo anexar]**. Se você não selecionar essa opção, os novos metadados substituirão os existentes nos campos. Selecione **[!UICONTROL Enviar]**.

   >[!CAUTION]
   >
   >Em campos de valor único, os novos metadados não são anexados ao valor existente no campo mesmo se você selecionar o **[!UICONTROL Modo anexar]**.

## Metadados personalizados usando o perfil de processamento {#metadata-compute-service}

O Assets as a [!DNL Cloud Service] pode gerar metadados personalizados para um ativo usando serviços nativos em nuvem. Configure um perfil de processamento para gerar metadados personalizados. Consulte [como usar o perfil de processamento](/help/assets/asset-microservices-configure-and-use.md#use-profiles).

![Representação de metadados no perfil de processamento](assets/processing-profile-metadata.png)

>[!TIP]
>
>Somente um perfil de processamento pode ser aplicado a uma pasta. Para aplicar vários processamentos a ativos em uma pasta, adicione mais opções a um único perfil de processamento. Por exemplo, um único perfil pode gerar representações, transcodificar ativos, gerar metadados personalizados e assim por diante. É possível aplicar filtros do tipo MIME para cada tarefa para que a tarefa apropriada seja acionada para o formato de arquivo necessário.

<!-- TBD: Commenting as Web Console is not available. Document the appropriate OSGi config method if available in CS.

## Configure limit for bulk metadata update {#configlimit}

To prevent DOS-like situation, [!DNL Experience Manager] limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. [!DNL Experience Manager] generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access Web Console ( **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**) and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.
-->

## Esquema de metadados {#metadata-schemata}

Os esquemas de metadados são conjuntos predefinidos de definições de propriedades de metadados que podem ser usadas em vários aplicativos. As propriedades são sempre associadas a um ativo, o que significa que as propriedades são &quot;sobre&quot; o recurso.

Você também pode projetar seu próprio esquema de metadados se não houver nenhum que atenda às suas necessidades. Não duplique as informações existentes. Em uma organização, a separação de esquemas facilita o compartilhamento de metadados. [!DNL Experience Manager] fornece uma lista padrão dos esquemas de metadados mais populares. A lista ajuda você a iniciar rapidamente sua estratégia de metadados e escolher rapidamente as propriedades de metadados necessárias.

Os esquemas de metadados compatíveis estão listados abaixo.

### Metadados padrão {#standard-metadata}

* DC - [!DNL Dublin Core] é um conjunto de metadados importante e amplamente usado.
* DICOM - Imagem Digital e Comunicações em Medicina.
* `Iptc4xmpCore` e `iptc4xmpExt` - O International Press Communications Standard contém muitos metadados específicos de assunto.
* RDF - Estrutura de descrição do recurso - para metadados web semânticos genéricos.
* XMP - [!DNL Extensible Metadata Platform].
* `xmpBJ` - Tíquetes de Trabalho Básicos.

### Metadados específicos do aplicativo {#application-specific-metadata}

Os metadados específicos do aplicativo incluem metadados técnicos e descritivos. Se você usar esses metadados, outros aplicativos talvez não consigam usá-los. Por exemplo, um aplicativo de renderização de imagem diferente talvez não possa acessar os metadados de [!DNL Adobe Photoshop]. Você pode criar uma etapa de fluxo de trabalho que altere uma propriedade específica do aplicativo para uma propriedade padrão.

* ACDSee - Metadados gerenciados pelo programa [!DNL ACDSee]. Consulte [www.acdsee.com/](https://www.acdsee.com/).
* Álbum - [!DNL Adobe Photoshop Album].
* CQ - Usado por [!DNL Experience Manager Assets].
* DAM - Usado por [!DNL Experience Manager Assets].
* DEX - [O explorador de Descrição Optima SC](https://www.optimasc.com/products/dex/index.html) é uma coleção de ferramentas para gerenciamento de metadados e arquivos de sistemas operacionais Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto e MP - Microsoft Photo.
* PDF e PDF/X.
* Photoshop e psAux - [!DNL Adobe Photoshop].

### Metadados do Digital Rights Management {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [Sistema Universal de Licenciamento de Imagens](https://www.useplus.com).
<!--THIS LINK IS 404 WITH NO SUITABLE REPLACEMENT * PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata). -->
* PRL - Idioma de direitos PRISM.
* PUR - Direitos de Uso do PRISM.
* `xmpPlus` - Integração do PLUS com o XMP.

### Metadados específicos de fotografia {#photography-specific-metadata}

* Exif - Informações técnicas da câmera, incluindo a posição GPS.
* CRS - Esquema [!DNL Camera Raw].
* `iptc4xmpCore` e `iptc4xmpExt`.
* TIFF - metadados de imagem (não apenas para imagens TIFF).

### Metadados específicos de impressão {#print-specific-metadata}

* PDF e PDF/X - aplicativos da Adobe PDF e de terceiros.
<!--THIS LINK IS 404 WITH NO SUITABLE REPLACEMENT * PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata). -->
* XMP - [!DNL Extensible Metadata Platform].
* `xmpPG` - Metadados do XMP para texto paginado.

### Metadados específicos de multimídia {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gerenciamento de mídia.

## Fluxos de trabalho orientados por metadados {#metadata-driven-workflows}

A criação de workflows orientados por metadados ajuda você a automatizar alguns processos, o que melhora a eficiência. Em um fluxo de trabalho orientado por metadados, o sistema de gerenciamento de fluxos de trabalho lê o fluxo de trabalho e, como resultado, executa alguma ação predefinida. Por exemplo, algumas das maneiras de usar workflows orientados por metadados:

* O fluxo de trabalho pode verificar se uma imagem tem ou não um título. Caso contrário, o sistema notificará a adição de um título.
* O fluxo de trabalho pode verificar se um aviso de copyright em um ativo permite a distribuição ou não. Assim, o sistema envia o ativo para um servidor ou para o outro.
* Um fluxo de trabalho pode verificar ativos sem metadados obrigatórios predefinidos ou ativos com *metadados* inválidos.

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
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Metadados XMP](xmp-metadata.md)
>* [Como editar ou adicionar metadados](meta-edit.md)
