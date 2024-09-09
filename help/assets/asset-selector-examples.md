---
title: Seletor de ativos para [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Exemplos para usar o Seletor de ativos para personalizar de acordo com o requisito.
role: Admin, User
exl-id: 7a393a96-f2a2-4a25-922c-577271cafc57
source-git-commit: 575980320c1dbd32f799bf9c2fddf3d6773c838a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 49%

---

# Exemplos de uso das propriedades do Seletor de ativos {#usage-examples}

Você pode definir o Seletor de ativos [propriedades](/help/assets/asset-selector-properties.md) no arquivo **index.html** para personalizar a exibição do Seletor de ativos no seu aplicativo.

## Exemplo 1: Seletor de ativos na exibição do painel

![rail-view-example](assets/rail-view-example-vanilla.png)

Se o valor do AssetSelector `rail` estiver definido como `false` ou não for mencionado nas propriedades, o Seletor de ativos é exibido na exibição Modal por padrão. A propriedade `acvConfig` permite algumas configurações detalhadas, como Arrastar e Soltar. Visite [habilitar ou desabilitar a ação de arrastar e soltar](asset-selector-customization.md#enable-disable-drag-and-drop) para entender o uso da propriedade `acvConfig`.

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

## Exemplo 2: popover de metadados

Use várias propriedades para definir os metadados de um ativo que deseja visualizar usando um ícone de informações. O popover de informações fornece a coleção de informações sobre o ativo ou a pasta, incluindo título, dimensões, data de modificação, local e descrição de um ativo. No exemplo abaixo, várias propriedades são usadas para exibir metadados de um ativo, por exemplo, a propriedade `repo:path` especifica o local de um ativo. <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)

## Exemplo 3: propriedade de filtro personalizado na exibição do painel

Além da pesquisa facetada, o Seletor de Assets permite personalizar vários atributos para refinar sua pesquisa do [!DNL Adobe Experience Manager] como um aplicativo do [!DNL Cloud Service]. Adicione o código a seguir para adicionar filtros de pesquisa personalizados em seu aplicativo. No exemplo abaixo, a pesquisa `Type Filter` que filtra o tipo de ativo entre Imagens, Documentos ou Vídeos ou o tipo de filtro adicionado para a pesquisa.

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->


>[!MORELIKETHIS]
>
>* [Personalizações do Seletor de ativos](/help/assets/asset-selector-customization.md)
>* [Carregamento do Seletor de ativos](/help/assets/asset-selector-upload.md)
>* [Propriedades do Seletor de ativos](/help/assets/asset-selector-properties.md)
>* [Integrar o Seletor de ativos ao Dynamic Media com recursos OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
