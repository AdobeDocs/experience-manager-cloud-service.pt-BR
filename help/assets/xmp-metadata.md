---
title: Metadados XMP
description: Saiba mais sobre o padrão de metadados do XMP (Extensible Metadata Platform) para gerenciamento de metadados. Ele é usado pelo Experience Manager como um formato padronizado para criação, processamento e intercâmbio de metadados.
contentOwner: AG
feature: Metadata
role: Admin, User
exl-id: fd9af408-d2a3-4c7a-9423-c4b69166f873
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 16%

---

# Metadados XMP {#xmp-metadata}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar o Dynamic Media Prime e o Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Pesquisar Práticas Recomendadas</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas de metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>documentação para desenvolvedores do AEM Assets</b></a>
        </td>
    </tr>
</table>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

XMP (Extensible Metadata Platform) é o padrão de metadados usado pelo Experience Manager Assets para todo o gerenciamento de metadados. O XMP fornece um formato padrão para a criação, o processamento e o intercâmbio de metadados para uma grande variedade de aplicativos.

Além de oferecer codificação de metadados universal que pode ser incorporada em todos os formatos de arquivo, o XMP fornece um [modelo de conteúdo](#xmp-core-concepts) avançado e tem [suporte do Adobe](#advantages-of-xmp) e de outras empresas, para que os usuários do XMP em combinação com o [!DNL Assets] tenham uma plataforma eficiente com base na qual possam trabalhar.

## Visão geral e ecossistema do XMP {#xmp-ecosystem}

[!DNL Assets] nativamente oferece suporte ao padrão de metadados XMP. O XMP é um padrão para processar e armazenar metadados padronizados e proprietários em ativos digitais. O XMP foi projetado para ser o padrão comum que permite que vários aplicativos funcionem efetivamente com metadados.

Os profissionais de produção, por exemplo, usam o suporte XMP integrado nos aplicativos da Adobe para transmitir informações em vários formatos de arquivo. O repositório do [!DNL Assets] extrai os metadados do XMP e os usa para gerenciar o ciclo de vida do conteúdo e oferece a capacidade de criar workflows de automação.

A XMP padroniza como os metadados são definidos, criados e processados fornecendo um modelo de dados, um modelo de armazenamento e esquemas. Todos esses conceitos são abordados nesta seção.

Todos os metadados herdados do EXIF, ID3 ou Microsoft Office são traduzidos automaticamente para o XMP, que pode ser estendido para oferecer suporte ao esquema de metadados específico do cliente, como catálogos de produtos.

Os metadados no XMP consistem em um conjunto de propriedades. Essas propriedades são sempre associadas a uma entidade específica chamada de recurso; ou seja, as propriedades são &quot;sobre&quot; o recurso. No caso do XMP, o recurso é sempre o ativo.

O XMP define um modelo de [metadados](https://pt.wikipedia.org/wiki/Metadados) que pode ser usado com qualquer conjunto definido de itens de metadados. O XMP também define [esquemas](https://en.wikipedia.org/wiki/XML_schema) específicos de propriedades básicas úteis para gravar o histórico de um recurso à medida que ele passa por várias etapas de processamento, de ser fotografado, [digitalizado](https://pt.wikipedia.org/wiki/Digitalizador) ou criado como texto, até etapas de edição de fotos (como [recorte](https://en.wikipedia.org/wiki/Cropping_%28image%29) ou ajuste de cor), para montagem em uma imagem final. O XMP permite que cada programa de software ou dispositivo ao longo do caminho adicione suas próprias informações a um recurso digital, que pode ser retido no arquivo digital final.

O XMP geralmente é serializado e armazenado usando um subconjunto do [W3C](https://pt.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://pt.wikipedia.org/wiki/Resource_Description_Framework) (RDF), que por sua vez é expresso em [XML](https://pt.wikipedia.org/wiki/XML).

### Vantagens do XMP {#advantages-of-xmp}

O XMP tem as seguintes vantagens em relação a outros padrões e esquemas de codificação:

* Os metadados baseados em XMP são muito eficientes e refinados.
* O XMP permite que você tenha vários valores para uma propriedade.
* O XMP tem codificação padronizada, que permite trocar metadados facilmente.
* O XMP é extensível. Você pode adicionar mais informações aos seus ativos.

O padrão XMP foi projetado para ser extensível, permitindo adicionar tipos personalizados de metadados aos dados do XMP. O EXIF, por outro lado, não - ele tem uma lista fixa de propriedades que não podem ser estendidas.

>[!NOTE]
>
>O XMP geralmente não permite que tipos de dados binários sejam incorporados. Para transportar dados binários no XMP, por exemplo, imagens em miniatura, eles devem ser codificados em um formato compatível com XML, como `Base64`.

### Conceitos principais do XMP {#xmp-core-concepts}

**Namespaces e esquemas**

Um esquema do XMP é um conjunto de nomes de propriedades em um namespace XML comum que inclui
o tipo de dados e as informações descritivas. Um esquema do XMP é identificado por seu URI de namespace XML. O uso de namespaces impede conflitos entre propriedades em esquemas diferentes que têm o mesmo nome, mas um significado diferente.

Por exemplo, a propriedade **Creator** em dois esquemas criados de forma independente pode significar a pessoa que criou o ativo ou pode significar o aplicativo que criou o ativo (por exemplo, Adobe Photoshop).

**Propriedades e valores do XMP**

O XMP pode incluir propriedades de um ou mais esquemas. Por exemplo, um subconjunto típico usado por muitos aplicativos do Adobe pode incluir o seguinte:

* Esquema principal de Dublin: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* Esquema básico do XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* Esquema de gerenciamento de direitos do XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* Esquema de gerenciamento de mídia do XMP: `xmpMM:DocumentID`

**Alternativas de idioma**

O XMP oferece a capacidade de adicionar uma propriedade `xml:lang` às propriedades de texto para especificar o idioma do texto.

## Writeback XMP para representações {#xmp-writeback-to-renditions}

Esse recurso de write-back do XMP em [!DNL Adobe Experience Manager Assets] replica as alterações de metadados nas representações do ativo original.
Quando você altera os metadados de um ativo a partir do [!DNL Assets] ou ao carregar o ativo, as alterações são inicialmente armazenadas no nó de metadados na hierarquia do ativo. O recurso de write-back permite propagar as alterações de metadados para todas as representações ou representações específicas do ativo. O recurso grava somente as propriedades de metadados que usam o namespace `jcr`, ou seja, uma propriedade chamada `dc:title` é gravada, mas uma propriedade chamada `mytitle` não.

Por exemplo, considere um cenário em que você modifica a propriedade [!UICONTROL Title] do ativo intitulado `Classic Leather` para `Nylon`.

![metadados](assets/metadata.png)

Nesse caso, [!DNL Assets] salva as alterações na propriedade **[!UICONTROL Title]** no parâmetro `dc:title` para os metadados de ativos armazenados na hierarquia de ativos.

![metadados armazenados no nó do ativo no repositório](assets/metadata_stored.png)

>[!IMPORTANT]
>
>O recurso de write-back não está habilitado por padrão em [!DNL Assets]. Veja como [habilitar write-back de metadados](#enable-xmp-writeback). O MSM para ativos digitais não funciona com o write-back de metadados habilitado. No write-back, a herança é interrompida.

### Habilitar write-back do XMP {#enable-xmp-writeback}

O fluxo de trabalho [!UICONTROL Writeback de metadados DAM] é usado para write-back de metadados de um ativo. Para ativar o write-back, siga um dos três métodos a seguir:

* Use Iniciadores.
* Inicie manualmente o fluxo de trabalho `DAM MetaData Writeback`.
* Configure o workflow para fazer parte do pós-processamento.

Para usar Iniciadores, siga estas etapas:

1. Como administrador, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Iniciadores]**.
1. Selecione o [!UICONTROL Iniciador] para o qual a coluna **[!UICONTROL Fluxo de Trabalho]** exibe o **[!UICONTROL Writeback de Metadados DAM]**. Clique em **[!UICONTROL Propriedades]** na barra de ferramentas.

   ![Selecione o iniciador de write-back de metadados do DAM para modificar suas propriedades e ativá-lo](assets/launcher-properties-metadata-writeback1.png)

1. Selecione **[!UICONTROL Ativar]** na página **[!UICONTROL Propriedades do inicializador]**. Clique em **[!UICONTROL Salvar e fechar]**.

Para aplicar manualmente o fluxo de trabalho a um ativo apenas uma vez, aplique o fluxo de trabalho [!UICONTROL Writeback de metadados DAM] a partir do painel esquerdo.

Para aplicar o fluxo de trabalho a todos os ativos carregados, adicione o fluxo de trabalho a um perfil de pós-processamento.

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Select the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, select the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then select **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
-->

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
