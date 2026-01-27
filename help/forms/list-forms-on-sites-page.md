---
title: Como listar formulários em uma página do Adobe Experience Manager Sites usando o componente do Forms Portal?
description: Saiba como listar formulários em uma página do AEM Sites.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 37e3ddd9-b20d-4156-b52e-64e36c455184
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# Listar formulários na página Sites

Imagine um usuário visitando o site do banco em busca de um formulário de abertura de conta. O banco usa o componente Forms Portal para ajudar os usuários a encontrar rapidamente o formulário, inserindo palavras-chave específicas ou filtrando por categorias, como &quot;Novas contas&quot; ou &quot;Banco pessoal&quot;, e permite que os usuários localizem facilmente o formulário desejado sem ter que percorrer longas listas.

O componente **Pesquisa &amp; Lister** do Portal Forms permite exibir e listar formulários em uma página do Sites. Os usuários podem configurar e apresentar uma lista abrangente de formulários com base em critérios específicos para atender aos requisitos organizacionais. Os usuários anônimos podem visitar a página Sites para visualizar e navegar pelos formulários disponíveis. Os formulários listados podem ser classificados em ordem crescente ou decrescente usando a opção suspensa **Classificar por**, localizada no canto superior direito da tela.

![Ícone de Pesquisa e Lister](assets/search-and-lister-component.png)


## Listar formulários na página Sites

Para adicionar o componente de portal **Pesquisa e Listagem** à página Sites, execute as seguintes etapas:

1. Abra a página do AEM Sites no modo **Editar**.
1. Vá para as **[!UICONTROL Informações da Página]** > **[!UICONTROL Editar Modelo]**
   ![Editar política de modelo](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Clique na **[!UICONTROL Política]** e marque a caixa de seleção **[!UICONTROL Pesquisar e Listar]** em **[Nome do Projeto do Arquétipo do AEM] - Forms e Portal de Comunicações**.

   ![Seleção de Política](/help/forms/assets/search-lister-enable-policy.png)

1. Clique em **[!UICONTROL Concluído]**.
1. Agora, abra novamente a página do AEM Sites no modo de criação.
1. Localize a seção no editor de páginas que permite adicionar o componente Forms Portal.

1. Clique no ícone **Adicionar**. O ícone é um sinal de mais (+) que significa a opção de adicionar novos componentes.

   Clicar no ícone **Adicionar** exibe uma caixa de diálogo **Inserir novo componente** que exibe vários componentes para inserção.

   >[!NOTE]
   >
   > Como alternativa, você também pode arrastar e soltar o componente.

1. Navegue pelos componentes disponíveis na caixa de diálogo e selecione o componente desejado na lista. Por exemplo, selecione o componente **Pesquisa e Listagem** da lista para adicionar o componente do Forms Portal **Pesquisa e Listagem**.

   ![Componente de pesquisa e listagem](/help/forms/assets/add-search-lister.png)

Agora, configure as propriedades do componente **Pesquisa e Listagem**.

## Compreender as propriedades do componente de Pesquisa e Lister

Você pode personalizar facilmente as propriedades do componente **Pesquisa e Lister** usando a Caixa de Diálogo de Configuração para obter uma experiência perfeita para o usuário. Para configurar, selecione o componente e, em seguida, selecione o ![ícone Configurar](assets/configure_icon.png). A caixa de diálogo **[!UICONTROL Pesquisa e Lister]** é aberta.

### Guia Exibir

![Guia Exibição](/help/forms/assets/search-and-lister-display-tab.png)

1. Em **[!UICONTROL Título]**, especifique o título do componente de Pesquisa e Listagem. Um título indicativo permite que os usuários executem uma pesquisa rápida na lista de formulários.
1. Na lista **[!UICONTROL Layout]**, selecione o layout para representar os formulários no formato de cartão ou lista.
1. Selecione **[!UICONTROL Ocultar Pesquisa]** e **[!UICONTROL Ocultar Classificação]** para ocultar a pesquisa e a classificação por recursos.
1. Em **[!UICONTROL Dica de Ferramenta]**, forneça a dica de ferramenta que aparece quando você passa o mouse sobre o componente.

### Guia Ativo

![Guia Ativo](/help/forms/assets/search-and-lister-asset-tab.png)

1. Na guia **[!UICONTROL Pasta de ativos]**, especifique o local de onde os formulários são extraídos e listados na página.
1. Usando o **[!UICONTROL Adicionar outro local]**, você pode configurar vários locais de pastas.

### Guia Resultados

![Guia Exibição](/help/forms/assets/search-and-lister-result-tab.png)

Na guia **[!UICONTROL Resultados]**, configure o número máximo de formulários a serem exibidos por página. O padrão é oito formulários por página.

## Exibir formulários na página Sites usando o componente Pesquisa e listagem

Para exibir a lista de formulários, use o componente do Portal Forms do **Search &amp; Lister**. Visualize a página do AEM Sites para ver a lista de formulários da pasta **Assets** exibida na tela. Também é possível pesquisar por um formulário específico usando a barra de pesquisa.

![Ícone de Pesquisa e Lister](assets/search-and-lister-component.png)

<!--
## Configure Azure Storage for Adaptive Forms {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Azure] storage configuration to integrate forms with [!DNL Azure] storage services. The Form Data Model (FDM) can be used to create Adaptive Forms that interact with [!DNL Azure] server to enable business workflows.

### Create Azure Storage Configuration {#create-azure-storage-configuration}

Before executing these steps, ensure that you have an Azure storage account and an access key to authorize access to the [!DNL Azure] storage account.

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Cloud Services]** &gt; **[!UICONTROL Azure Storage]**.
1. Select a folder to create the configuration and select **[!UICONTROL Create]**.
1. Specify a title for the configuration in the **[!UICONTROL Title]** field.
1. Specify the name of the [!DNL Azure] storage account in the **[!UICONTROL Azure Storage Account]** field.

### Configure Unified Storage Connector for Forms Portal {#configure-usc-forms-portal}

Perform the following steps to configure Unified Storage Connector for AEM Workflows:

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Unified Storage Connector]**.
1. In the **[!UICONTROL Forms Portal]** section, select **[!UICONTROL Azure]** from the **[!UICONTROL Storage]** drop-down list.
1. Specify the [configuration path for the Azure storage configuration](#create-azure-storage-configuration) in the **[!UICONTROL Storage Configuration Path]** field.
1. Select **[!UICONTROL Publish]** and then select **[!UICONTROL Save]** to save the configuration.

## Enable Forms Portal Components {#enable-forms-portal-components}

To use any core component (including the out-of-the-box portal components) in an Adobe Experience Manager (AEM) site, you must create a proxy component and enable it for your site. For creating a proxy component and enabling portal components, see [Using Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components). 

Once a portal component is enabled, you can use it in the author instance of your sites page.

## Add and Configure Forms Portal Components {#configure-forms-portal-components}

You can create and customize Forms Portal on websites authored using AEM by adding and configuring the portal components. Ensure that the [components are enabled](#enable-forms-portal-components) before using them in the Forms Portal.

To add a component, either drag and drop the component from the Components pane to the layout container on the page, or select the add icon on the layout container and add the component from the [!UICONTROL Insert New Component] dialog.

### Configure Drafts & Submissions Component {#configure-drafts-submissions-component}

The Drafts & Submissions component displays forms that are saved as draft for completing later and submitted forms. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). In the [!UICONTROL Drafts and Submissions] dialog, specify the title to indicate the form listing as draft or submitted forms. Also select whether the component should list draft forms or submitted forms in card or list format.

![Drafts icon](assets/drafts-component.png)

![Submissions icon](assets/submission-listing.png)

### Configure Search & Lister Component {#configure-search-lister-component}

The Search & Lister component is used to list adaptive forms on a page and to implement search on the listed forms. 

![Search and Lister icon](assets/search-and-lister-component.png)

To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Search and Lister] dialog opens.

1. In the [!UICONTROL Display] tab, configure the following:
    * In **[!UICONTROL Title]**, specify the title for the Search & Lister component. An indicative title enables the users perform quick search across the list of forms.
    * From the **[!UICONTROL Layout]** list, select the layout to represent the forms in card or list format.
    * Select **[!UICONTROL Hide Search]** and **[!UICONTROL Hide Sorting]** to hide the search and sort by features.
    * In **[!UICONTROL Tooltip]**, provide the tooltip that appears when you hover over the component. 
1. In the [!UICONTROL Asset Folder] tab, specify the location from where the forms are pulled and listed on the page. You can configure multiple folder locations.
1. In the [!UICONTROL Results] tab, configure the maximum number of forms to display per page. The default is eight forms per page.

### Configure Link Component {#configure-link-component}

The link component enables you to provide links to an adaptive form on the page. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Edit Link Component] dialog opens.

1. In the [!UICONTROL Display] tab, provide the link caption and tooltip to ease identification of the forms represented by the link.
1. In the [!UICONTROL Asset Info] tab, specify the repository path where the asset is stored. 
1. In the [!UICONTROL Query Params] tab, specify the additional parameters in the key-value pair format. When the link is clicked, these additional parameters and passed along with the form.

## Configure Asynchronous Form Submission Using Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

You can configure to submit an adaptive form only when all the recipients have completed the signing ceremony. Follow the steps below to configure the setting using Adobe Sign.

1. In the author instance, open an Adaptive Form in the edit mode.
1. From the left pane, select the Properties icon and expand the **[!UICONTROL ELECTRONIC SIGNTATURE]** option.
1. Select **[!UICONTROL Enable Adobe Sign]**. Various configuration options display. 
1. In the [!UICONTROL Submit the form] section, select the **[!UICONTROL after every recipient completes signing ceremony]** option to configure the Submit Form action, where the form is first sent to all the recipients for signing. Once all the recipients have signed the form, only then the form is submitted. 

## Save Adaptive Forms As Drafts {#save-adaptive-forms-as-drafts}

You can save forms as Drafts for completing them later. There are two ways in which a form is saved as a draft:

* Create a "Save Form" rule on a form component, for example, a button. On clicking the button, the rule triggers and the form are saved a draft.
* Enable Auto-Save feature, which saves the form as per the specified event or after a configured interval of time.

### Create Rules to Save an Adaptive Form as Draft {#rule-to-save-adaptive-form-as-draft}

To create a "Save Form" rule on a form component, for example, a button, follow the steps below:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select ![Components icon](assets/components_icon.png) and drag the [!UICONTROL Button] component to the form.
1. Select the [!UICONTROL Button] component and then select the ![Configure icon](assets/configure_icon.png). 
1. Select the [!UICONTROL Edit Rules] icon to open the Rule Editor. 
1. Select **[!UICONTROL Create]** to configure and create the rule.
1. In the [!UICONTROL When] section, select "is clicked" and in the [!UICONTROL Then] section, select the "Save Form" options.
1. Select **[!UICONTROL Done]** to save the rule.

### Enable Auto-save {#enable-auto-save}

You can configure the auto-save feature for an adaptive form as follows:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select the ![Properties icon](assets/configure_icon.png) and expand the [!UICONTROL AUTO-SAVE] option.
1. Select the **[!UICONTROL Enable]** check box to enable auto-save of the form. You can configure the following:
* By default, the [!UICONTROL Adaptive Form Event] is set to "true", which implies that the form is auto-saved after every event.
* In [!UICONTROL Trigger], configure to trigger auto-save based on the occurrence of an event or after a specific interval of time.
-->


## Próximas etapas

No próximo artigo, vamos aprender [como salvar formulários como rascunhos e listá-los em uma página do Sites usando o componente Rascunhos e envios do Forms Portal](/help/forms/save-core-component-based-form-as-draft.md).

## Artigos relacionados

{{forms-portal-see-also}}

## Consulte também {#see-also}

{{see-also}}
