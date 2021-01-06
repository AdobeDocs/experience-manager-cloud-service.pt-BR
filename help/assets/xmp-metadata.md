---
title: Metadados XMP
description: Saiba mais sobre o padrão de metadados XMP (Plataforma de metadados extensível) para gerenciamento de metadados. É usado pelo AEM como um formato padronizado para criação, processamento e intercâmbio de metadados.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8110259a910c891a5bcf7507cfa9897603a45c91
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 18%

---


# Metadados XMP {#xmp-metadata}

XMP (Plataforma de metadados extensível) é o padrão de metadados usado pela AEM Assets para todo o gerenciamento de metadados. XMP fornece um formato padrão para a criação, o processamento e o intercâmbio de metadados para uma grande variedade de aplicativos.

Além de oferecer codificação de metadados universais que podem ser incorporados em todos os formatos de arquivo, XMP fornece um [modelo de conteúdo](#xmp-core-concepts) rico e é [suportado pelo Adobe](#advantages-of-xmp) e outras empresas, para que os usuários de XMP em combinação com a AEM Assets tenham uma plataforma poderosa para desenvolver.

## Visão geral XMP e ecossistema {#xmp-ecosystem}

A AEM Assets oferece suporte nativo ao padrão de metadados XMP. XMP é um padrão para processamento e armazenamento de metadados padronizados e proprietários em ativos digitais. XMP é projetado para ser o padrão comum que permite que vários aplicativos trabalhem com metadados de forma eficaz.

Os profissionais de produção, por exemplo, usam o suporte integrado XMP nos aplicativos Adobe para transmitir informações em vários formatos de arquivo. O repositório da AEM Assets extrai os metadados XMP e os usa para gerenciar o ciclo de vida do conteúdo e oferta a capacidade de criar workflows de automação.

XMP padroniza como os metadados são definidos, criados e processados fornecendo um modelo de dados, um modelo de armazenamento e schemas. Todos estes conceitos são abordados nesta seção.

Todos os metadados herdados do EXIF, ID3 ou Microsoft Office são traduzidos automaticamente para XMP, que podem ser estendidos para suportar schemas de metadados específicos do cliente, como catálogos de produtos.

Os metadados no XMP consistem em um conjunto de propriedades. Estas propriedades estão sempre associadas a uma entidade específica designada por recurso; ou seja, as propriedades são &quot;sobre&quot; o recurso. No caso de XMP, o recurso é sempre o ativo.

O XMP define um modelo de [metadados](https://pt.wikipedia.org/wiki/Metadados) que pode ser usado com qualquer conjunto definido de itens de metadados. O XMP também define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos de propriedades básicas úteis para gravar o histórico de um recurso à medida que ele passa por várias etapas de processamento, de ser fotografado, [digitalizado](https://pt.wikipedia.org/wiki/Digitalizador) ou criado como texto, até etapas de edição de fotos (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) ou ajuste de cor), para montagem em uma imagem final. O XMP permite que cada programa de software ou dispositivo ao longo do caminho adicione suas próprias informações a um recurso digital, que pode ser retido no arquivo digital final.

O XMP geralmente é serializado e armazenado usando um subconjunto do [W3C](https://pt.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://pt.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que por sua vez é expresso em [XML](https://pt.wikipedia.org/wiki/XML).

### Vantagens do XMP {#advantages-of-xmp}

XMP tem as seguintes vantagens sobre outros padrões e esquemas de codificação:

* Metadados baseados em XMP são muito potentes e de granulação fina.
* XMP permite que você tenha vários valores para uma propriedade.
* XMP tem codificação padronizada, que permite a troca fácil de metadados.
* XMP é extensível. Você pode adicionar informações adicionais aos ativos.

O padrão XMP foi projetado para ser extensível, permitindo que você adicione tipos personalizados de metadados aos dados XMP. O EXIF, por outro lado, não - tem uma lista fixa de propriedades que não podem ser estendidas.

>[!NOTE]
>
>XMP geralmente não permite a incorporação de tipos de dados binários. Para carregar dados binários em XMP, por exemplo, imagens em miniatura, eles devem ser codificados em um formato compatível com XML, como `Base64`.

### XMP principais conceitos {#xmp-core-concepts}

**Namespaces e esquemas**

Um schema XMP é um conjunto de nomes de propriedade em uma namespace XML comum que inclui
o tipo de dados e as informações descritivas. Um schema XMP é identificado por seu URI de namespace XML. O uso do namespace evita conflitos entre propriedades em schemas diferentes que tenham o mesmo nome, mas um significado diferente.

Por exemplo, a propriedade **Creator** em dois schemas projetados de forma independente pode significar a pessoa que criou o ativo ou o aplicativo que criou o ativo (por exemplo, Adobe Photoshop).

**Propriedades e valores XMP**

XMP pode incluir propriedades de um ou mais schemas. Por exemplo, um subconjunto típico usado por muitos aplicativos Adobe pode incluir o seguinte:

* Schema principal de Dublin: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* XMP schema básico: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* schema de gerenciamento de direitos XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* schema de gerenciamento de mídia XMP: `xmpMM:DocumentID`

**Alternativas linguísticas**

XMP oferta a capacidade de adicionar uma propriedade `xml:lang` às propriedades de texto para especificar o idioma do texto.

## Write-back de XMP a execuções {#xmp-writeback-to-renditions}

Esse recurso de gravação XMP no Adobe Experience Manager (AEM) Assets replica as alterações nos metadados do ativo nas representações do ativo.

Quando você altera os metadados de um ativo no AEM Assets ou durante o upload do ativo, as alterações são armazenadas inicialmente no nó do ativo no CRXDE.

O recurso de write-back XMP propaga as alterações nos metadados para todas as execuções ou para as execuções específicas do ativo.

Considere um cenário em que você modifica a propriedade [!UICONTROL Title] do ativo intitulado `Classic Leather` para `Nylon`.

![metadata](assets/metadata.png)

Nesse caso, o AEM Assets salva as alterações na propriedade **[!UICONTROL Title]** no parâmetro `dc:title` para os metadados de ativos armazenados na hierarquia de ativos.

![metadata_storage](assets/metadata_stored.png)

No entanto, a AEM Assets não propaga automaticamente quaisquer alterações de metadados nas representações de um ativo.

O recurso de write-back XMP permite que você propague as alterações de metadados para todas as representações ou representações específicas do ativo. No entanto, as alterações não são armazenadas no nó de metadados na hierarquia do ativo. Em vez disso, esse recurso incorpora as alterações nos arquivos binários das execuções.

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}
-->

<!-- asgupta, Engg: Need attention here to update the configuration manager changes. -->

<!-- 
To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Tap/click the AEM logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, tap/click the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then tap/click **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
-->

>[!MORELIKETHIS]
>
>* [Especificação XMP por Adobe](https://www.adobe.com/devnet/xmp.html)

