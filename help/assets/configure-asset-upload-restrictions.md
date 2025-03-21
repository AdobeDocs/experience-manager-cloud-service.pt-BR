---
title: Configurar restrições de upload de ativos
description: Configure o Adobe Experience Manager Assets para restringir os tipos de ativos que os usuários podem carregar com base no tipo MIME. Ele ajuda a impedir uploads acidentais de formato indesejado e arquivos mal-intencionados.
exl-id: 094c31f3-f2e9-4b44-9995-c76fb78ca458
feature: Upload, Asset Ingestion
role: User, Admin, Developer
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 10%

---

# Configurar restrições de upload de ativos {#configure-asset-upload-restrictions}

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

Você pode configurar o Adobe Experience Manager Assets para restringir os tipos de ativos que os usuários podem carregar com base no tipo MIME.

>[!IMPORTANT]
>
>Por padrão, o Experience Manager Assets permite que os usuários façam upload de ativos de todos os tipos MIME. No entanto, você pode definir as configurações para impedir que os usuários façam upload de arquivos apenas de tipos MIME específicos.

## Pré-requisitos {#prerequisites-asset-upload-restrictions}

É necessário ter privilégios de administrador para configurar restrições de upload de ativos.

## Aplicar restrições a uploads de ativos {#apply-restrictions-asset-uploadsssssss}

Para configurar o [!DNL Experience Manager] para impedir que usuários carreguem arquivos de tipos MIME específicos:

1. Navegue até **[!UICONTROL Ferramentas > Assets > Configurações do Assets]**.

1. Clique em **[!UICONTROL Restrições de Carregamento]**.

1. Clique em **[!UICONTROL Adicionar]** para definir os tipos MIME permitidos.

1. Especifique o tipo MIME na caixa de texto. Você pode clicar em **[!UICONTROL Adicionar]** novamente para especificar mais tipos MIME permitidos. Você também pode clicar no ![ícone excluir](assets/delete-icon.svg) para excluir qualquer tipo MIME da lista.

1. Clique em **[!UICONTROL Salvar]**.

**Exemplo 1: permitir o carregamento de todas as imagens e arquivos PDF para o Experience Manager Assets**

Para permitir o upload de imagens em todos os formatos e arquivos PDF para o Experience Manager Assets, faça as seguintes configurações:

![Restrições de upload de ativos](assets/asset-upload-restrictions.png)

`image/*` como tipo MIME permite o carregamento de imagens em todos os formatos. `application/pdf` como tipo MIME permite o carregamento de arquivos PDF para o Experience Manager Assets.

Se você tentar fazer upload de um arquivo que não está incluído na lista de tipos MIME permitidos, o Experience Manager Assets exibirá a seguinte mensagem de erro:

![Arquivos restritos](assets/asset-upload-restricted-files.png)

`Screen Recording 2022-08-31 at 3.36.09 PM.mov` refere-se a um nome de arquivo que não está incluído nos tipos MIME permitidos.

**Exemplo 2: Permitir carregamento de formatos de imagem específicos para o Experience Manager Assets**

Para adicionar formatos de imagem específicos aos tipos MIME permitidos e restringir o upload de todos os outros formatos de ativo, faça as seguintes configurações:

![Restrições de ativos](assets/asset-restrictions.png)

Com base nas configurações representadas na imagem, você pode fazer upload de imagens nos formatos .JPG, .PNG e .GIF no Experience Manager Assets.

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
