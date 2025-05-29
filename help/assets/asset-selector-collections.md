---
title: Coleções do seletor de ativos
description: Trabalhar com coleções do seletor de ativos.
role: Admin,User
exl-id: 1687e7d5-eb7e-4eb7-8747-e5dc6afacd5b
source-git-commit: 08fc43bc8edeea91bfeb01f053d435e136658e7f
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 7%

---

# Coleções do seletor de ativos {#asset-selector-collections}

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
            <a href="/help/assets/search-best-practices.md"><b>Práticas recomendadas de pesquisa</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas para metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de conteúdo</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos da OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentação do AEM Assets para desenvolvedores</b></a>
        </td>
    </tr>
</table>

Uma coleção é um conjunto de ativos, pastas ou outras coleções no Seletor de ativos. Use coleções para compartilhar ativos entre usuários. Diferente de pastas, uma coleção pode incluir ativos de locais diferentes.

As coleções de microfront-end no Seletor de ativos estão disponíveis imediatamente no modo somente leitura. Ele busca ativos e coleções diretamente do repositório do [!DNL Experience Manager Assets] ao qual você tem acesso.

>[!NOTE]
>
>Verifique se você tem permissões para acessar uma [!DNL Experience Manager Assets] [imsOrg](/help/assets/asset-selector-properties.md) e Coleções.

As coleções de microfront-end no Seletor de ativos estão disponíveis imediatamente no modo somente leitura. Ele busca ativos e coleções diretamente do repositório do Experience Manager Assets ao qual você tem acesso e herda as propriedades de pastas públicas e privadas do repositório do Experience Manager Assets. Veja mais sobre [a criação de uma coleção pública ou privada no modo de exibição do Assets](/help/assets/manage-collections-assets-view.md#create-collection).

É possível exibir Coleções no Seletor de ativos na exibição do painel e na exibição modal.

![Coleções na exibição de painel](assets/collections-rail-modal-view.png)

<!--
Additionally, you can [customize](/help/assets/asset-selector-customization.md) the `featureSet` property to enable or disable collections in Asset Selector. See [enable or disable Collections tab](#enable-disable-collections-tab).-->

Além disso, também é possível personalizar a seleção de ativos na guia Coleções. Para fazer isso, você pode personalizá-lo usando o `handleSelection`. Consulte [manipulação de seleção de Assets usando Esquema de Objeto](/help/assets/asset-selector-customization.md#handling-selection).

## Exibir coleções {#view-collections}

O Seletor de ativos permite exibir coleções em uma exibição de lista ![1} ou em uma exibição de grade ![3}. ](assets/do-not-localize/list-view.png)](assets/do-not-localize/grid-view.png) Consulte [tipos de exibição no Seletor de ativos](overview-asset-selector.md#types-of-view).

## Arraste e solte ativos na coleção {#collection-drag-and-drop}

Você pode arrastar e soltar um ativo em Coleções diretamente da exibição [!DNL Assets as a Cloud Service] no ambiente de Autor. Para fazer isso, arraste o ativo da guia Assets para a área de trabalho Coleções do aplicativo Seletor de ativos para criar aplicativos avançados.

>[!NOTE]
>
>* O arrastar e soltar de um ativo é possível somente na exibição do painel.
>* Você pode arrastar e soltar somente arquivos (ativos) e não as pastas.

Por outro lado, você também pode [habilitar ou desabilitar o arrastar e soltar ativos nas coleções](asset-selector-customization.md#enable-disable-drag-and-drop) diretamente.

## Desabilitar seleção de ativo em Coleções {#disable-selection-collection}

Desativar seleção é usado para ocultar ou desativar a seleção de ativos ou pastas. Ela oculta a caixa de seleção de seleção do cartão ou ativo, impedindo-o de ser selecionado. Consulte [desabilitar seleção](/help/assets/asset-selector-customization.md#disable-selection).

## Habilitar ou desabilitar a guia Coleções {#enable-disable-collections-tab}

O Seletor de ativos permite personalizar os componentes de acordo com os requisitos e a usabilidade. Para habilitar ou desabilitar a guia Coleções no Seletor de Ativos, você pode usar a propriedade `featureSet` da seguinte maneira:

* **Habilitar guia Coleções** Para habilitar a guia Coleções, você precisa fornecer `collections` como valor para a matriz. Por padrão, a guia Coleções é ativada imediatamente para todos os usuários. Por exemplo, `featureSet:["collections"]`
* **Guia Desabilitar Coleções**: para desabilitar a guia de coleções, é preciso fornecer uma matriz vazia como seu valor. Por exemplo, `featureSet:[ ]`

>[!MORELIKETHIS]
>
>* [Personalizações do Seletor de ativos](/help/assets/asset-selector-customization.md)
>* [Integrar o Seletor de ativos a vários aplicativos](/help/assets/integrate-asset-selector.md)
>* [Propriedades do Seletor de ativos](/help/assets/asset-selector-properties.md)
