---
title: Metadados XMP
description: Saiba mais sobre o padrão de metadados XMP (Extensible Metadata Platform) para gerenciamento de metadados. É usado pelo AEM como um formato padronizado para criação, processamento e intercâmbio de metadados.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Metadados XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) é o padrão de metadados usado pelo AEM Assets para todo o gerenciamento de metadados. O XMP fornece um formato padrão para a criação, o processamento e o intercâmbio de metadados para uma grande variedade de aplicativos.

Além de oferecer a codificação de metadados universais que pode ser incorporada em todos os formatos de arquivo, o XMP fornece um modelo [de](#xmp-core-concepts) conteúdo avançado e é [suportado pela Adobe](#advantages-of-xmp) e por outras empresas, para que os usuários do XMP em combinação com os ativos AEM tenham uma plataforma poderosa para desenvolver.

## Visão geral e ecossistema do XMP {#xmp-ecosystem}

Os ativos AEM oferecem suporte nativo ao padrão de metadados XMP. O XMP é um padrão para processamento e armazenamento de metadados padronizados e proprietários em ativos digitais. O XMP é projetado para ser o padrão comum que permite que vários aplicativos funcionem com metadados de forma eficaz.

Os profissionais de produção, por exemplo, usam o suporte XMP integrado nos aplicativos da Adobe para transmitir informações em vários formatos de arquivo. O repositório do AEM Assets extrai os metadados XMP e os usa para gerenciar o ciclo de vida do conteúdo e oferece a capacidade de criar fluxos de trabalho de automação.

O XMP padroniza como os metadados são definidos, criados e processados fornecendo um modelo de dados, um modelo de armazenamento e esquemas. Todos estes conceitos são abordados nesta seção.

Todos os metadados herdados do EXIF, ID3 ou Microsoft Office são convertidos automaticamente para XMP, que pode ser estendido para suportar o esquema de metadados específico do cliente, como catálogos de produtos.

Os metadados no XMP consistem em um conjunto de propriedades. Estas propriedades estão sempre associadas a uma entidade específica designada por recurso; ou seja, as propriedades são &quot;sobre&quot; o recurso. No caso do XMP, o recurso é sempre o ativo.

O XMP define um modelo de [metadados](https://en.wikipedia.org/wiki/Metadata) que pode ser usado com qualquer conjunto definido de itens de metadados. O XMP também define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos para propriedades básicas úteis para gravar o histórico de um recurso à medida que ele passa por várias etapas de processamento, de ser fotografado, [digitalizado](https://en.wikipedia.org/wiki/Image_scanner)ou criado como texto, através de etapas de edição de fotos (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) ou ajuste de cor), para montagem em uma imagem final. O XMP permite que cada programa de software ou dispositivo ao longo do caminho adicione suas próprias informações a um recurso digital, que pode ser retido no arquivo digital final.

O XMP é mais comumente serializado e armazenado usando um subconjunto do [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que por sua vez é expresso em [XML](https://en.wikipedia.org/wiki/XML).

### Vantagens do XMP {#advantages-of-xmp}

O XMP tem as seguintes vantagens em relação a outros padrões e esquemas de codificação:

* Metadados baseados em XMP são muito potentes e de granulação fina.
* O XMP permite que você tenha vários valores para uma propriedade.
* O XMP tem codificação padronizada, que permite a troca fácil de metadados.
* XMP é extensível. Você pode adicionar informações adicionais aos ativos.

O padrão XMP foi projetado para ser extensível, permitindo que você adicione tipos personalizados de metadados aos dados XMP. EXIF, por outro lado, não - tem uma lista fixa de propriedades que não podem ser estendidas.

>[!NOTE]
>
>O XMP geralmente não permite a incorporação de tipos de dados binários. Para carregar dados binários no XMP, por exemplo, imagens em miniatura, eles devem ser codificados em um formato compatível com XML, como `Base64`.

### Conceitos principais do XMP {#xmp-core-concepts}

**Namespaces e esquemas**

Um esquema XMP é um conjunto de nomes de propriedades em um namespace XML comum que inclui o tipo de dados e as informações descritivas. Um esquema XMP é identificado pelo URI do namespace XML. O uso de namespaces evita conflitos entre propriedades em esquemas diferentes que tenham o mesmo nome, mas um significado diferente.

Por exemplo, a propriedade **Creator** em dois esquemas projetados independentemente pode significar a pessoa que criou o ativo ou o aplicativo que criou o ativo (por exemplo, Adobe Photoshop).

**Propriedades e valores XMP**

XMP pode incluir propriedades de um ou mais esquemas. Por exemplo, um subconjunto típico usado por muitos aplicativos Adobe pode incluir o seguinte:

* Esquema principal de Dublin: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* Esquema básico XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* Esquema de gerenciamento de direitos XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* Esquema de gerenciamento de mídia XMP: `xmpMM:DocumentID`

**Alternativas linguísticas**

O XMP oferece a capacidade de adicionar uma `xml:lang` propriedade às propriedades de texto para especificar o idioma do texto.

## Write-back de XMP a execuções {#xmp-writeback-to-renditions}

Esse recurso de gravação XMP nos ativos Adobe Experience Manager (AEM) replica as alterações nos metadados do ativo nas representações do ativo.

Quando você altera os metadados de um ativo dos ativos AEM ou durante o upload do ativo, as alterações são armazenadas inicialmente no nó do ativo no CRXDE.

O recurso de write-back XMP propaga as alterações de metadados para todas as execuções ou representações específicas do ativo.

Considere um cenário em que você modifica a propriedade [!UICONTROL Título] do ativo com título `Classic Leather` para `Nylon`.

![metadata](assets/metadata.png)

Nesse caso, os ativos AEM salvam as alterações na propriedade **[!UICONTROL Title]** no `dc:title` parâmetro para os metadados do ativo armazenados na hierarquia do ativo.

![metadata_storage](assets/metadata_stored.png)

No entanto, os ativos AEM não propagam automaticamente quaisquer alterações de metadados nas representações de um ativo.

O recurso de write-back XMP permite que você propague as alterações de metadados para todas as representações ou representações específicas do ativo. No entanto, as alterações não são armazenadas no nó de metadados na hierarquia do ativo. Em vez disso, esse recurso incorpora as alterações nos arquivos binários das execuções.

### Ativar gravação XMP {#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

Para permitir que as alterações de metadados sejam propagadas para as representações do ativo ao carregá-lo, modifique a configuração do **[!UICONTROL Adobe CQ DAM Rendition Maker]** no Configuration Manager.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração do **[!UICONTROL Adobe CQ DAM Rendition Maker]** .
1. Selecione a opção **[!UICONTROL Propagar XMP]** e salve as alterações.

### Habilitar gravação XMP para execuções específicas {#enable-xmp-writeback-for-specific-renditions}

Para permitir que o recurso de gravação XMP propague alterações de metadados para selecionar execuções, especifique essas execuções para a etapa de fluxo de trabalho do Processo  de gravação XMP do fluxo de trabalho WriteBack de metadados DAM. Por padrão, essa etapa é configurada com a representação original.

Para que o recurso de gravação XMP propague metadados para as miniaturas de execução 140.100.png e 319.319.png, execute estas etapas.

1. Toque/clique no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos, abra o modelo de fluxo de trabalho Writeback **[!UICONTROL de metadados]** DAM.
1. Na página de propriedades Writeback **[!UICONTROL de metadados]** DAM, abra a etapa Processo **[!UICONTROL de Writeback de]** XMP.
1. Na caixa de diálogo Propriedades **[!UICONTROL da]** etapa, toque/clique na guia **[!UICONTROL Processo]** .
1. Na caixa **[!UICONTROL Argumentos]** , adicione `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`e toque/clique em **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Salve as alterações.
1. Para regenerar as execuções de Pirâmide TIFF (PTIFF) para imagens de Dynamic Media com os novos atributos, adicione a etapa Ativos **** de imagem do processo de Dynamic Media ao fluxo de trabalho de gravação de metadados DAM. As execuções PTIFF são criadas e armazenadas apenas localmente em uma implementação do Dynamic Media Hybrid.

1. Salve o fluxo de trabalho.

As alterações de metadados são propagadas para as representações representações thumbnail.140.100.png e thumbnail.319.319.png do ativo, e não para as outras.

<!--
>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).
-->

### Filtrar metadados XMP {#filtering-xmp-metadata}

Os ativos AEM oferecem suporte à filtragem de listas negras e de listas brancas de propriedades/nós para metadados XMP que são lidos de binários de ativos e armazenados no JCR quando os ativos são ingeridos.

A filtragem da lista negra permite importar todas as propriedades de metadados XMP, exceto as propriedades especificadas para exclusão. No entanto, para tipos de ativos, como arquivos INDD que têm quantidades enormes de metadados XMP (por exemplo, 1000 nós com 10.000 propriedades), os nomes dos nós a serem filtrados nem sempre são conhecidos antecipadamente. Se a filtragem da lista negra permitir a importação de um grande número de ativos com diversos metadados XMP, a instância/cluster do AEM poderá enfrentar problemas de estabilidade, por exemplo, filas de observação obstruídas.

A filtragem da lista de permissões dos metadados XMP resolve esse problema ao permitir que você defina as propriedades XMP a serem importadas. Dessa forma, outras propriedades XMP/desconhecidas são ignoradas. Você pode adicionar algumas dessas propriedades ao filtro da lista negra para compatibilidade com versões anteriores.

>[!NOTE]
>
>A filtragem funciona somente para as propriedades derivadas de fontes XMP em binários de ativos. Para as propriedades derivadas de fontes não XMP, como formatos EXIF e IPTC, a filtragem não funciona. Por exemplo, a data de criação do ativo é armazenada em uma propriedade chamada `CreateDate` em EXIF TIFF. O AEM relata esse valor no campo de metadados chamado `exif:DateTimeOriginal`. Como a fonte é uma fonte não XMP, a filtragem não funciona nessa propriedade.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração **[!UICONTROL Adobe CQ DAM XmpFilter]** .
1. Para aplicar a filtragem de lista de permissões, selecione **[!UICONTROL Aplicar lista de permissões às propriedades]** XMP e especifique as propriedades a serem importadas na caixa de filtragem **** XML da lista de permissões para XMP.

1. Para filtrar as propriedades XMP proibidas após a aplicação da filtragem de lista branca, especifique-as na caixa de filtragem **** XML da lista negra Nomes XML para XMP.

   >[!NOTE]
   >
   >A opção **[!UICONTROL Aplicar lista negra a propriedades]** XMP está selecionada por padrão. Em outras palavras, a filtragem da lista negra é ativada por padrão. Para desativar a filtragem da lista negra, desmarque a opção **[!UICONTROL Aplicar lista negra às propriedades]** XMP.

1. Salve as alterações.

>[!MORELIKETHIS]
>
>* [Especificação XMP da Adobe](https://www.adobe.com/devnet/xmp.html)