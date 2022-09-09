---
title: Configurar o mapeamento de metadados de ativos entre o Workfront e a Experience Manager Assets
description: Mapeie os campos de metadados de ativos entre o Adobe Workfront e os aplicativos as a Cloud Service do Experience Manager. Como resultado do mapeamento de campos de metadados, ao enviar um ativo do Workfront para o Experience Manager Assets, você pode exibir os metadados do ativo mapeados no Experience Manager Assets.
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# Configurar o mapeamento de metadados de ativos entre o Adobe Workfront e a Experience Manager Assets {#asset-metadata-mapping-workfront-aem-assets}

Você pode mapear os campos de metadados de ativos entre aplicativos as a Cloud Service do Adobe Workfront e do Experience Manager. Como resultado do mapeamento de campos de metadados, ao enviar um ativo do Workfront para o Experience Manager Assets, você pode exibir os metadados do ativo mapeados no Experience Manager Assets.

Por exemplo, se você precisar manter os campos de metadados de uma imagem, como nome, descrição e o projeto ao qual ela pertence no Workfront ao enviar a imagem para a Experience Manager Assets, configure e mapeie esses campos para as propriedades do Experience Manager Assets.

**Caso de uso**

Uma imagem `add-users-workfront.png` existe no `Metadata Syncs` projeto no aplicativo Adobe Workfront. Você precisa enviar essa imagem para a Experience Manager Assets as a Cloud Service com os seguintes metadados:

* Nome do projeto

* Nome do documento

* Descrição do documento

## Pré-requisitos {#prerequisites}

* Um acesso de administrador aos aplicativos as a Cloud Service do Workfront e Experience Manager Assets.

* Uma integração entre [Aplicativos as a Cloud Service da Workfront e da Experience Manager Assets](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## Configurar mapeamento de metadados no Workfront {#set-up-metadata-mapping}

Para definir o mapeamento de metadados para os campos Nome do projeto, Nome do documento e Descrição do documento no Workfront:

1. Clique no ícone do Menu principal ![Mostrar Menu](assets/show-menu.svg) disponível no canto superior direito do aplicativo Adobe Workfront, em seguida, clique em **[!UICONTROL Configuração]**.

1. Selecionar **[!UICONTROL Documentos]** no painel esquerdo e selecione **[!UICONTROL Experience Manager Assets]**.

1. Selecione a integração do Experience Manager Assets e clique em **[!UICONTROL Editar]**.

1. Clique em **[!UICONTROL Metadados]**. No **[!UICONTROL Ativos]** , mapeie a [!UICONTROL Projeto] > [!UICONTROL Nome] O campo Workfront para `wm:projectName` Campo Experience Manager Assets . Se não encontrar a correspondência exata, o Adobe recomenda procurar a melhor correspondência para mapear o campo Workfront e Experience Manager Assets. É possível evitar o mapeamento de campos de diferentes tipos de dados. Por exemplo, mapear um campo Workfront de data para um campo Ativos de descrição.
1. Mapeie o [!UICONTROL Documento] > [!UICONTROL Nome] O campo Workfront para `wm:documentName` Campo Experience Manager Assets .

   ![Mapeamento no Workfront](assets/workfront-metadata-mapping.png)

1. Mapeie o [!UICONTROL Documento] > [!UICONTROL Descrição] O campo Workfront para `dc:description` Campo Experience Manager Assets .

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## Enviar a imagem do Workfront para o Experience Manager Assets {#send-image-workfront-assets}

Para enviar a imagem do Workfront para o Experience Manager Assets:

1. Clique no ícone do Menu principal ![Mostrar Menu](assets/show-menu.svg) disponível no canto superior direito do aplicativo Adobe Workfront, em seguida, clique em **[!UICONTROL Projetos]**.

1. Clique em **[!UICONTROL Novo projeto]** para criar um novo projeto.

1. Clique em **[!UICONTROL Documentos]** disponível no painel esquerdo, arraste e selecione a imagem que precisa ser enviada para a Experience Manager Assets.

1. Clique em **[!UICONTROL Enviar para]** e escolha o nome da integração do Experience Manager Assets Essentials.

   ![Enviar para AEM](assets/send-to-aem.png)

1. Escolha a pasta de destino do ativo e clique em **[!UICONTROL Selecionar pasta]**.

1. Clique em **[!UICONTROL Salvar]**.

## Configurar o mapeamento de metadados de ativos no Experience Manager as a Cloud Service {#metadata-mapping-aem}

Depois [configuração do mapeamento de metadados de ativos no Adobe Workfront](#set-up-metadata-mapping), você deve usar o mesmo mapeamento no aplicativo as a Cloud Service do Experience Manager Assets para exibir os resultados de metadados apropriados para a imagem.

O mapeamento de metadados é executado usando Esquemas de metadados no Experience Manager Assets. É possível editar um formulário de esquema de metadados recém-adicionado ou existente. O formulário de esquema de metadados inclui guias e itens de formulário em guias. Você pode mapear/configurar esses itens de formulário em um campo dentro de um nó de metadados no repositório CRX. É possível adicionar guias ou itens de formulário ao formulário de esquema de metadados. Para obter mais informações, consulte [Esquemas de metadados](metadata-schemas.md).

Para configurar o mapeamento de metadados usando um novo formulário de metadados no Experience Manager Assets as a Cloud Service:

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**.

1. Clique em **[!UICONTROL Criar]** na barra de ferramentas. Na caixa de diálogo , forneça o título do formulário de esquema e clique em **[!UICONTROL Criar]** para concluir o processo de criação do formulário.

1. Selecione o formulário de esquema e clique em **[!UICONTROL Editar]**.

1. (Opcional) No Editor de formulário de esquema de metadados, clique em `+` para criar uma nova guia para os campos do Workfront.

1. Clique no botão **[!UICONTROL Criar formulário]** e arraste a **[!UICONTROL Texto de linha única]** ao formulário. Clique no componente no formulário. No **[!UICONTROL Criar formulário]** guia :

   1. Especificar `Project Name` no **[!UICONTROL Rótulo do campo]** campo.

   1. Especificar `./jcr:content/metadata/wm:projectName` no **[!UICONTROL Mapear para propriedade]** campo. Como diretriz, use o seguinte modelo para definir os mapeamentos de campo nos Ativos do Experience Manager:
      `./jcr:content/metadata/<mapping defined for the field in workfront>`.

      Ao configurar mapeamentos no Workfront, você mapeou `wm:projectName` Campo Experience Manager Assets para Projeto > Nomear Workfront .

      `wm` refere-se ao nome do namespace e `projectName` refere-se ao título da propriedade. Use o `namespace:propertyTitle` para definir mapeamentos de campo de metadados.

      ![Enviar para AEM](assets/metadata-schema-mapping.png)

1. Clique no botão **[!UICONTROL Criar formulário]** e arraste a **[!UICONTROL Texto de linha única]** ao formulário. Clique no componente no formulário. No **[!UICONTROL Criar formulário]** guia :

   1. Especificar `Document Name` no **[!UICONTROL Rótulo do campo]** campo.

   1. Especificar `./jcr:content/metadata/wm:documentName` no **[!UICONTROL Mapear para propriedade]** campo.
Ao configurar mapeamentos no Workfront, você mapeou `wm:documentName` Campo Experience Manager Assets para Documento > Nomear Workfront.

1. Clique no botão **[!UICONTROL Criar formulário]** e arraste a **[!UICONTROL Texto de várias linhas]** ao formulário. Clique no componente no formulário. No **[!UICONTROL Criar formulário]** guia :

   1. Especificar `Document Description` no **[!UICONTROL Rótulo do campo]** campo.

   1. Especificar `./jcr:content/metadata/dc:description` no **[!UICONTROL Mapear para propriedade]** campo.
Ao configurar mapeamentos no Workfront, você mapeou `dc:description` Campo Experience Manager Assets para Documento > Descrição do campo Workfront.

1. Clique em **[!UICONTROL Salvar]** para salvar as alterações.

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## Aplicar configurações de metadados à pasta de imagem {#apply-metadata-settings-image-folder}

Depois de definir as configurações de metadados no aplicativo Experience Manager as a Cloud Service, aplique essas configurações ao [pasta que contém a imagem enviada do aplicativo Workfront](#send-image-workfront-assets).

Para aplicar configurações de metadados à pasta de imagem:

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**.

1. Selecione o esquema de metadados na lista disponível e clique em **[!UICONTROL Aplicar às pastas]**.

1. Selecione a pasta de destino para a qual [a imagem é enviada do aplicativo Adobe Workfront](#send-image-workfront-assets) e clique em **[!UICONTROL Aplicar]**.

Você pode navegar até a imagem no Experience Manager Assets e exibir os metadados associados à imagem. Selecione a imagem e clique **[!UICONTROL Propriedades]** para exibir os metadados da imagem.
