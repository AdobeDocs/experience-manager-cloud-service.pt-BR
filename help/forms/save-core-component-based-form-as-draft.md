---
title: Como salvar o formulário adaptável baseado em componente principal como um rascunho?
description: Saiba como salvar o formulário adaptável baseado em componentes principais como um rascunho e criar um portal do Forms e usar os componentes principais prontos para uso em uma página do AEM Sites.
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer, Admin
source-git-commit: 52b87073cad84705b5dc0c6530aff44d1e686609
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 1%

---


# Salvar o formulário adaptável baseado no componente principal como um rascunho {#save-af-form}

Salvar o formulário adaptável como um rascunho é um recurso essencial que melhora a eficiência e a precisão do usuário. Essa funcionalidade permite que os usuários salvem o progresso e retornem para concluir as tarefas posteriormente sem perder nenhuma informação inserida. Fornecer uma opção `save-as-draft` garante flexibilidade no gerenciamento de tempo, reduz o risco de perda de dados e mantém a precisão dos envios. Você pode salvar formulários como rascunhos para preenchê-los posteriormente.

## Considerações

* [Ativar os componentes principais adaptáveis do Forms para o seu ambiente.](/help/forms/enable-adaptive-forms-core-components.md)

* Verifique se o componente principal [está definido como versão 3.0.24 ou posterior](https://github.com/adobe/aem-core-forms-components) para usar este recurso.
* Verifique se você tem uma [conta de armazenamento do Azure e uma chave de acesso](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal) para autorizar o acesso à conta de armazenamento do Azure.

## Salvar um formulário adaptável como rascunho

A Integração de Dados do [!DNL Experience Manager Forms] (data-integration.md) fornece a configuração de armazenamento do [!DNL Azure] para integrar formulários com serviços de armazenamento do [!DNL Azure]. O Modelo de Dados de Formulário (FDM) pode ser usado para criar o Forms Adaptável que interage com o servidor [!DNL Azure] para habilitar fluxos de trabalho de negócios.

Para salvar o formulário como rascunho, verifique se você tem uma conta de armazenamento do Azure e uma chave de acesso para autorizar o acesso à conta de armazenamento [!DNL Azure]. Para salvar um formulário como rascunho, execute as seguintes etapas:

1. [Criar configuração de armazenamento do Azure](#create-azure-storage-configuration)
1. [Configurar o Conector de armazenamento unificado para o Forms Portal](#configure-usc-forms-portal)
1. [Criar regra para salvar um formulário adaptável como rascunho](#rule-to-save-adaptive-form-as-draft)


### 1. Criar configuração de armazenamento do Azure {#create-azure-storage-configuration}

Depois de ter uma conta de armazenamento do Azure e uma chave de acesso para autorizar o acesso à conta de armazenamento [!DNL Azure], execute as seguintes etapas para criar a configuração de Armazenamento do Azure:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Armazenamento do Azure]**.

   ![Seleção de Cartão de Armazenamento do Azure](/help/forms/assets/save-form-as-draft-azure-card.png)

1. Selecione uma pasta de configuração para criar a configuração e selecione **[!UICONTROL Criar]**.

   ![Selecionar pasta de configuração de armazenamento do Azure](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. Especifique um título para a configuração no campo **[!UICONTROL Título]**.
1. Especifique o nome da conta de armazenamento [!DNL Azure] nos campos **[!UICONTROL Conta de Armazenamento do Azure]** e **[!UICONTROL Chave de Acesso do Azure]**.

   ![Configuração de Armazenamento do Azure](/help/forms/assets/save-form-as-draft-azure-storage.png)

1. Clique em **Salvar**.

>[!NOTE]
>
> Você pode recuperar a **[!UICONTROL Conta de Armazenamento do Azure]** e a **[!UICONTROL Chave de Acesso do Azure]** no [Portal do Microsoft Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).


### 2. Configurar o Conector de armazenamento unificado para o Forms Portal {#configure-usc-forms-portal}

Depois de criar com êxito a Configuração de Armazenamento do Azure, configure o Conector de Armazenamento Unificado para o Forms Portal, usando as seguintes etapas:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Conector de Armazenamento Unificado]**.

   ![Armazenamento de conector unificado](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. Na seção **[!UICONTROL Portal do Forms]**, selecione **[!UICONTROL Azure]** na lista suspensa **[!UICONTROL Armazenamento]**.
1. Especifique o [caminho de configuração para a configuração de armazenamento do Azure](#create-azure-storage-configuration) no campo **[!UICONTROL Caminho de Configuração de Armazenamento]**.

   ![Configuração de armazenamento do conector unificado](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. Selecione **[!UICONTROL Salvar]** e **[!UICONTROL Publish]** para publicar a configuração.

### 3. Criar regras para salvar um Formulário adaptável como rascunho {#rule-to-save-adaptive-form-as-draft}

Para salvar um formulário como Rascunho, crie uma regra **Salvar Formulário** em um componente de formulário, como um botão. Quando o botão é clicado, a regra é acionada e o formulário é salvo como rascunho. Execute as seguintes etapas para criar a regra **Salvar formulário** em um componente de botão:

1. Na instância do Autor, abra um Formulário adaptável em um modo de edição.
1. No painel esquerdo, selecione ![ícone Componentes](assets/components_icon.png) e arraste o componente **[!UICONTROL Botão]** para o formulário.
1. Selecione o componente **[!UICONTROL Botão]** e selecione o ![ícone Configurar](assets/configure_icon.png).
1. Selecione o ícone **[!UICONTROL Editar Regras]** para abrir o Editor de Regras.
1. Selecione **[!UICONTROL Criar]** para configurar e criar a regra.
1. Na seção **[!UICONTROL Quando]**, selecione **está clicado** e na seção **[!UICONTROL Depois]**, selecione a opção **Salvar Formulário**.
1. Selecione **[!UICONTROL Concluído]** para salvar a regra.

![Criar regra para o botão](/help/forms/assets/save-form-as-drfat-create-rule.png)

Ao visualizar um formulário adaptável, preencha-o e clique no botão **Salvar formulário**, ele será salvo como rascunho para uso posterior.

## Componente Rascunhos e envios para listar rascunhos na página do AEM Sites

A AEM Forms fornece o componente de portal **Rascunhos e envios** pronto para uso para exibir formulários salvos em páginas do AEM Sites. O componente **Rascunhos e Envios** mostra formulários que são salvos como rascunhos para conclusão posterior, bem como formulários enviados. Este componente oferece uma experiência personalizada para qualquer usuário conectado, listando os rascunhos e envios relacionados ao Forms adaptável criado pelo usuário.

Você pode usar componentes prontos para uso do Forms Portal para listar rascunhos de formulário na página do AEM Sites. Execute as seguintes etapas para usar o componente de portal **Rascunhos e Envios**:

1. [Ativar Componente de Rascunhos e Envios do Forms Portal](#enable-component)
2. [Adicionar componente de Rascunhos e Envios na página do AEM Sites](#Add-drafts-submissions-component)
3. [Configurar o componente de rascunhos e envios](#configure-drafts-submissions-component)

### 1. Ativar rascunhos e envios para o Forms Portal Component{#enable-component}

Para habilitar o componente **[!UICONTROL Rascunhos e Envios]** na política de modelo, execute as seguintes etapas:

1. Abra a página do AEM Sites no modo **Editar**.
1. Vá para as **[!UICONTROL Informações da Página]** > **[!UICONTROL Editar Modelo]**
   ![Editar política de modelo](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Clique na **[!UICONTROL Política]** e marque a caixa de seleção **[!UICONTROL Rascunhos e Envios]** sob o **[Nome do Projeto do Arquétipo AEM] - Forms e Portal de Comunicações**.

   ![Seleção de Política](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. Clique em **[!UICONTROL Concluído]**.

Depois que um componente de portal é ativado, você pode usá-lo na instância de autor da sua página do AEM Sites.

### 2. Adicionar componente Rascunhos e Envios na página do AEM Sites{#Add-drafts-submissions-component}

Você pode criar e personalizar o Forms Portal em sites criados usando AEM adicionando e configurando os componentes do portal. Verifique se o [Componente Rascunhos e Envios está habilitado](#enable-component) antes de usá-los na página do AEM Sites.

Para adicionar um componente, arraste e solte o componente do painel de componentes **Rascunhos e Envios** no contêiner de layout da página ou selecione o ícone adicionar no contêiner de layout e adicione o componente da caixa de diálogo **[!UICONTROL Inserir novo componente]**.

![Adicionar rascunho e componente de envio](/help/forms/assets/save-form-as-draft-add-dns.png)

### 3. Configurar o componente Rascunhos e Envios {#configure-drafts-submissions-component}

O componente **Rascunhos e Envios** exibe formulários que são salvos como rascunho para conclusão posterior e formulários enviados. Para configurar **Rascunhos e Envios**, execute as seguintes etapas:
1. Selecione o componente de **Rascunhos e Envios**.
1. Clique no ![ícone Configurar](assets/configure_icon.png) e a caixa de diálogo será exibida.
1. Na caixa de diálogo **[!UICONTROL Rascunhos e Envios]**, especifique o seguinte:
   * **Título** Para identificar um componente em uma página do Sites e, por padrão, o título aparece na parte superior do componente.
   * **Tipo**: para indicar a listagem de formulários como rascunho ou formulários enviados.
   * **Layout**: para exibir formulários de rascunho de lista ou formulários enviados no formato de cartão ou lista.

   ![Propriedades dos componentes de Rascunho e Envio](/help/forms/assets/save-form-as-draft-dns-properties.png)

1. Clique em **Concluído**.

Quando **[!UICONTROL Selecionar tipo]** é selecionado como **Rascunho do Forms**, os formulários salvos como rascunhos são exibidos:
![Ícone Rascunhos](assets/drafts-component.png)

Quando **[!UICONTROL Selecionar Tipo]** é selecionado como **Forms Enviada**, os formulários enviados são exibidos:

![Ícone de envios](assets/submission-listing.png)

Você pode abrir o formulário clicando no respectivo formulário.

<!--

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

## Consulte também {#see-also}

{{see-also}}



<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)

-->
