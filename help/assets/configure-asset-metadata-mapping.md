---
title: Configurar o mapeamento de metadados de ativos entre o Workfront e o Experience Manager Assets
description: Mapeie os campos de metadados de ativos entre os aplicativos Adobe Workfront e Experience Manager as a Cloud Service. Como resultado do mapeamento de campos de metadados, ao enviar um ativo do Workfront para o Experience Manager Assets, você pode visualizar os metadados do ativo mapeados no Experience Manager Assets.
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
feature: Metadata, Workfront Integrations and Apps
role: User, Admin
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 4%

---

# Configurar o mapeamento de metadados de ativos entre o Adobe Workfront e o Experience Manager Assets {#asset-metadata-mapping-workfront-aem-assets}

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

Você pode mapear os campos de metadados de ativos entre os aplicativos Adobe Workfront e Experience Manager as a Cloud Service. Como resultado do mapeamento de campos de metadados, ao enviar um ativo do Workfront para o Experience Manager Assets, você pode visualizar os metadados do ativo mapeados no Experience Manager Assets.

Por exemplo, se você precisar manter os campos de metadados de uma imagem, como nome, descrição e o projeto ao qual ela pertence no Workfront, ao enviar a imagem para o Experience Manager Assets, configure e mapeie esses campos para as propriedades do Experience Manager Assets.

**Caso de uso**

Uma imagem `add-users-workfront.png` existe no projeto `Metadata Syncs` no aplicativo Adobe Workfront. Você precisa enviar essa imagem para o Experience Manager Assets as a Cloud Service com os seguintes metadados:

* Nome do projeto

* Nome do documento

* Descrição do documento

## Pré-requisitos {#prerequisites}

* Um acesso de administrador aos aplicativos Workfront e Experience Manager Assets as a Cloud Service.

* Uma integração entre os [aplicativos Workfront e Experience Manager Assets as a Cloud Service](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## Configurar o mapeamento de metadados no Workfront {#set-up-metadata-mapping}

Para definir o mapeamento de metadados para os campos Nome do projeto, Nome do documento e Descrição do documento no Workfront:

1. Clique no ícone Menu Principal ![Mostrar Menu](assets/show-menu.svg), disponível no canto superior direito do aplicativo Adobe Workfront, e clique em **[!UICONTROL Instalação]**.

1. Selecione **[!UICONTROL Documentos]** no painel esquerdo e selecione **[!UICONTROL Experience Manager Assets]**.

1. Selecione a integração do Experience Manager Assets e clique em **[!UICONTROL Editar]**.

1. Clique em **[!UICONTROL Metadados]**. Na guia **[!UICONTROL Assets]**, mapeie o campo de Workfront [!UICONTROL Projeto] > [!UICONTROL Nome] para o campo de Experience Manager Assets `wm:projectName`. Se você não encontrar a correspondência exata, a Adobe recomenda procurar a melhor correspondência para mapear o campo do Workfront e do Experience Manager Assets. Você pode evitar o mapeamento de campos de diferentes tipos de dados. Por exemplo, mapear um campo de Workfront de data para um campo de Assets de descrição.
1. Mapeie o campo Workfront [!UICONTROL Documento] > [!UICONTROL Nome] para o campo Experience Manager Assets `wm:documentName`.

   ![Mapeamento no Workfront](assets/workfront-metadata-mapping.png)

1. Mapeie o campo Workfront [!UICONTROL Documento] > [!UICONTROL Descrição] para o campo Experience Manager Assets `dc:description`.

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## Enviar a imagem do Workfront para o Experience Manager Assets {#send-image-workfront-assets}

Para enviar a imagem do Workfront para o Experience Manager Assets:

1. Clique no ícone Menu Principal ![Mostrar Menu](assets/show-menu.svg), disponível no canto superior direito do aplicativo Adobe Workfront, e clique em **[!UICONTROL Projetos]**.

1. Clique em **[!UICONTROL Novo projeto]** para criar um projeto.

1. Clique na opção **[!UICONTROL Documentos]**, disponível no painel esquerdo, arraste e selecione a imagem que você precisa enviar para o Experience Manager Assets.

1. Clique em **[!UICONTROL Enviar para]** e escolha o nome da integração do Experience Manager Assets Essentials.

   ![Enviar para o AEM](assets/send-to-aem.png)

1. Escolha a pasta de destino para o ativo e clique em **[!UICONTROL Selecionar pasta]**.

1. Clique em **[!UICONTROL Salvar]**.

## Configurar o mapeamento de metadados de ativos no Experience Manager as a Cloud Service {#metadata-mapping-aem}

Depois de [configurar o mapeamento de metadados de ativos no Adobe Workfront](#set-up-metadata-mapping), você deve usar o mesmo mapeamento no aplicativo Experience Manager Assets as a Cloud Service para exibir os resultados de metadados apropriados para a imagem.

O mapeamento de metadados é executado usando Esquemas de metadados no Experience Manager Assets. Você pode editar um formulário de esquema de metadados recém-adicionado ou existente. O formulário de esquema de metadados inclui guias e itens de formulário em guias. Você pode mapear/configurar esses itens de formulário para um campo em um nó de metadados no repositório do CRX. Você pode adicionar guias ou itens de formulário ao formulário de esquema de metadados. Para obter mais informações, consulte [Esquemas de metadados](metadata-schemas.md).

Para configurar o mapeamento de metadados usando um novo formulário de metadados no Experience Manager Assets as a Cloud Service:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de Metadados]**.

1. Clique em **[!UICONTROL Criar]** na barra de ferramentas. Na caixa de diálogo, forneça o título do formulário de esquema e clique em **[!UICONTROL Criar]** para concluir o processo de criação do formulário.

1. Selecione o formulário de esquema e clique em **[!UICONTROL Editar]**.

1. (Opcional) No Editor de Formulário de Esquema de Metadados, clique em `+` para criar uma guia para os campos do Workfront.

1. Clique na guia **[!UICONTROL Criar Formulário]** e arraste o componente **[!UICONTROL Texto de Linha Única]** para o formulário. Clique no componente no formulário. Na guia **[!UICONTROL Criar Formulário]**:

   1. Especifique `Project Name` no campo **[!UICONTROL Rótulo do campo]**.

   1. Especifique `./jcr:content/metadata/wm:projectName` no campo **[!UICONTROL Mapear para propriedade]**. Como diretriz, use o seguinte modelo para definir os mapeamentos de campo no Experience Manager Assets:
      `./jcr:content/metadata/<mapping defined for the field in workfront>`.

      Ao configurar mapeamentos no Workfront, você mapeou o campo do Experience Manager Assets `wm:projectName` para o campo Projeto > Nomear Workfront.

      `wm` refere-se ao nome do namespace e `projectName` ao título da propriedade. Use o formato `namespace:propertyTitle` para definir mapeamentos de campos de metadados.

      ![Enviar para o AEM](assets/metadata-schema-mapping.png)

1. Clique na guia **[!UICONTROL Criar Formulário]** e arraste o componente **[!UICONTROL Texto de Linha Única]** para o formulário. Clique no componente no formulário. Na guia **[!UICONTROL Criar Formulário]**:

   1. Especifique `Document Name` no campo **[!UICONTROL Rótulo do campo]**.

   1. Especifique `./jcr:content/metadata/wm:documentName` no campo **[!UICONTROL Mapear para propriedade]**.
Ao configurar mapeamentos no Workfront, você mapeou o campo do Experience Manager Assets `wm:documentName` para o campo Documento > Nomear Workfront.

1. Clique na guia **[!UICONTROL Criar Formulário]** e arraste o componente **[!UICONTROL Texto de Várias Linhas]** para o formulário. Clique no componente no formulário. Na guia **[!UICONTROL Criar Formulário]**:

   1. Especifique `Document Description` no campo **[!UICONTROL Rótulo do campo]**.

   1. Especifique `./jcr:content/metadata/dc:description` no campo **[!UICONTROL Mapear para propriedade]**.
Ao configurar mapeamentos no Workfront, você mapeou o campo do Experience Manager Assets `dc:description` para o campo Documento > Descrição do Workfront.

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## Aplicar configurações de metadados à pasta de imagens {#apply-metadata-settings-image-folder}

Depois de definir as configurações de metadados no aplicativo Experience Manager as a Cloud Service, aplique essas configurações à pasta [que contém a imagem enviada do aplicativo Workfront](#send-image-workfront-assets).

Para aplicar configurações de metadados à pasta de imagens:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de Metadados]**.

1. Selecione o esquema de metadados na lista disponível e clique em **[!UICONTROL Aplicar às Pastas]**.

1. Selecione a pasta de destino para a qual [a imagem é enviada do aplicativo Adobe Workfront](#send-image-workfront-assets) e clique em **[!UICONTROL Aplicar]**.

Você pode navegar até a imagem no Experience Manager Assets e visualizar os metadados associados à imagem. Selecione a imagem e clique em **[!UICONTROL Propriedades]** para exibir os metadados da imagem.

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
