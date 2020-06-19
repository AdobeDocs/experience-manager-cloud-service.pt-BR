---
title: Metadados XMP
description: Saiba mais sobre o padrão de metadados XMP (Extensible Metadata Platform) para gerenciamento de metadados. É usado pelo AEM como um formato padronizado para criação, processamento e intercâmbio de metadados.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0c915b32d676ff225cbe276be075d3ae1a865f11
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 21%

---


# Metadados XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) é o padrão de metadados usado pelos AEM Assets para todo o gerenciamento de metadados. O XMP fornece um formato padrão para a criação, o processamento e o intercâmbio de metadados para uma grande variedade de aplicativos.

Além de oferecer codificação de metadados universais que podem ser incorporados em todos os formatos de arquivo, o XMP fornece um modelo [de](#xmp-core-concepts) conteúdo avançado e é [suportado pela Adobe](#advantages-of-xmp) e outras empresas, para que os usuários do XMP em combinação com AEM Assets tenham uma plataforma poderosa para desenvolver.

## Visão geral e ecossistema do XMP {#xmp-ecosystem}

AEM Assets oferecem suporte nativo ao padrão de metadados XMP. O XMP é um padrão para processamento e armazenamento de metadados padronizados e proprietários em ativos digitais. O XMP é projetado para ser o padrão comum que permite que vários aplicativos funcionem com metadados de forma eficaz.

Os profissionais de produção, por exemplo, usam o suporte XMP integrado nos aplicativos da Adobe para transmitir informações em vários formatos de arquivo. O repositório AEM Assets extrai os metadados XMP e os usa para gerenciar o ciclo de vida do conteúdo e oferta a capacidade de criar workflows de automação.

O XMP padroniza como os metadados são definidos, criados e processados fornecendo um modelo de dados, um modelo de armazenamento e schemas. Todos estes conceitos são abordados nesta seção.

Todos os metadados herdados do EXIF, ID3 ou Microsoft Office são automaticamente traduzidos para XMP, que pode ser estendido para suportar schemas de metadados específicos do cliente, como catálogos de produtos.

Os metadados no XMP consistem em um conjunto de propriedades. Estas propriedades estão sempre associadas a uma entidade específica designada por recurso; ou seja, as propriedades são &quot;sobre&quot; o recurso. No caso do XMP, o recurso é sempre o ativo.

O XMP define um modelo de [metadados](https://pt.wikipedia.org/wiki/Metadados) que pode ser usado com qualquer conjunto definido de itens de metadados. O XMP também define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos de propriedades básicas úteis para gravar o histórico de um recurso à medida que ele passa por várias etapas de processamento, de ser fotografado, [digitalizado](https://pt.wikipedia.org/wiki/Digitalizador) ou criado como texto, até etapas de edição de fotos (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) ou ajuste de cor), para montagem em uma imagem final. O XMP permite que cada programa de software ou dispositivo ao longo do caminho adicione suas próprias informações a um recurso digital, que pode ser retido no arquivo digital final.

O XMP geralmente é serializado e armazenado usando um subconjunto do [W3C](https://pt.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://pt.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que por sua vez é expresso em [XML](https://pt.wikipedia.org/wiki/XML).

### Vantagens do XMP {#advantages-of-xmp}

O XMP tem as seguintes vantagens em relação a outros padrões e esquemas de codificação:

* Metadados baseados em XMP são muito potentes e de granulação fina.
* O XMP permite que você tenha vários valores para uma propriedade.
* O XMP tem codificação padronizada, que permite a troca fácil de metadados.
* XMP é extensível. Você pode adicionar informações adicionais aos ativos.

O padrão XMP foi projetado para ser extensível, permitindo que você adicione tipos personalizados de metadados aos dados XMP. O EXIF, por outro lado, não - tem uma lista fixa de propriedades que não podem ser estendidas.

>[!NOTE]
>
>O XMP geralmente não permite a incorporação de tipos de dados binários. Para carregar dados binários no XMP, por exemplo, imagens em miniatura, eles devem ser codificados em um formato compatível com XML, como `Base64`.

### Conceitos principais do XMP {#xmp-core-concepts}

**Namespaces e esquemas**

Um schema XMP é um conjunto de nomes de propriedade em uma namespace XML comum que inclui o tipo de dados e as informações descritivas. Um schema XMP é identificado pelo URI da namespace XML. O uso do namespace evita conflitos entre propriedades em schemas diferentes que tenham o mesmo nome, mas um significado diferente.

Por exemplo, a propriedade **Creator** em dois schemas projetados de forma independente pode significar a pessoa que criou o ativo ou o aplicativo que criou o ativo (por exemplo, Adobe Photoshop).

**Propriedades e valores XMP**

XMP pode incluir propriedades de um ou mais schemas. Por exemplo, um subconjunto típico usado por muitos aplicativos Adobe pode incluir o seguinte:

* schema principal de Dublin: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* schema básico XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* schema de gerenciamento de direitos XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* schema de gerenciamento de mídia XMP: `xmpMM:DocumentID`

**Alternativas linguísticas**

O XMP oferta a capacidade de adicionar uma `xml:lang` propriedade às propriedades do texto para especificar o idioma do texto.

## Write-back de XMP a execuções {#xmp-writeback-to-renditions}

Esse recurso de gravação XMP nos ativos Adobe Experience Manager (AEM) replica as alterações nos metadados do ativo nas representações do ativo.

Quando você altera os metadados de um ativo de dentro dos AEM Assets ou durante o upload do ativo, as alterações são armazenadas inicialmente no nó do ativo no CRXDE.

O recurso de write-back XMP propaga as alterações de metadados para todas as execuções ou representações específicas do ativo.

Considere um cenário em que você modifica a propriedade [!UICONTROL Título] do ativo com título `Classic Leather` para `Nylon`.

![metadata](assets/metadata.png)

Nesse caso, os AEM Assets salvam as alterações na propriedade **[!UICONTROL Title]** no `dc:title` parâmetro para os metadados do ativo armazenados na hierarquia do ativo.

![metadata_storage](assets/metadata_stored.png)

No entanto, os AEM Assets não propagam automaticamente quaisquer alterações de metadados nas representações de um ativo.

O recurso de write-back XMP permite que você propague as alterações de metadados para todas as representações ou representações específicas do ativo. No entanto, as alterações não são armazenadas no nó de metadados na hierarquia do ativo. Em vez disso, esse recurso incorpora as alterações nos arquivos binários das execuções.

### Ativar gravação XMP {#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

Para permitir que as alterações de metadados sejam propagadas para as representações do ativo ao carregá-lo, modifique a configuração do **[!UICONTROL Adobe CQ DAM Rendition Maker]** no Configuration Manager.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração do **[!UICONTROL Adobe CQ DAM Rendition Maker]** .
1. Selecione a opção **[!UICONTROL Propagar XMP]** e salve as alterações.

### Habilitar write-back XMP para execuções específicas {#enable-xmp-writeback-for-specific-renditions}

Para permitir que o recurso de gravação XMP propague alterações de metadados para selecionar execuções, especifique essas execuções para a etapa de fluxo de trabalho do Processo  de gravação XMP do fluxo de trabalho WriteBack de metadados DAM. Por padrão, essa etapa é configurada com a representação original.

Para que o recurso de gravação XMP propague metadados para as miniaturas de execução 140.100.png e 319.319.png, execute estas etapas.

1. Toque/clique no logotipo do AEM e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos, abra o modelo de fluxo de trabalho Writeback **[!UICONTROL de metadados]** DAM.
1. Na página de propriedades **[!UICONTROL DAM Metadata Writeback]**, abra a etapa **[!UICONTROL Processo de Writeback XMP]**.
1. Na caixa de diálogo **[!UICONTROL Propriedades da etapa]**, toque/clique na guia **[!UICONTROL Processo]**.
1. Na caixa **[!UICONTROL Argumentos]** , adicione `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`e toque/clique em **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Salve as alterações.
1. Para regenerar as representações de Pyramid TIFF (PTIFF) de imagens do Dynamic Media com os novos atributos, adicione a etapa **[!UICONTROL Ativos de imagem do processo do Dynamic Media]** ao fluxo de trabalho de gravação de metadados do DAM. As representações PTIFF são criadas e armazenadas apenas localmente em uma implementação híbrida do Dynamic Media.

1. Salve o fluxo de trabalho.

As alterações de metadados são propagadas para as representações representações thumbnail.140.100.png e thumbnail.319.319.png do ativo, e não para as outras.

>[!MORELIKETHIS]
>
>* [Especificação XMP da Adobe](https://www.adobe.com/devnet/xmp.html)

