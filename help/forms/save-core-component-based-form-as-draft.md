---
title: Como salvar o formulário adaptável baseado em componente principal como um rascunho?
description: Saiba como salvar o formulário adaptável baseado em componentes principais como um rascunho e criar um portal do Forms e usar os componentes principais prontos para uso em uma página do AEM Sites.
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer, Admin
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 1%

---

<span class="preview"> Este artigo apresenta conteúdo para o recurso de pré-lançamento do. O recurso de pré-lançamento pode ser acessado somente por meio de [canal de pré-lançamento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=pt-BR#new-features).

# Salvar o formulário adaptável baseado no componente principal como um rascunho {#save-af-form}

Salvar o formulário adaptável como um rascunho é um recurso essencial que melhora a eficiência e a precisão do usuário. Essa funcionalidade permite que os usuários salvem o progresso e retornem para concluir as tarefas posteriormente sem perder nenhuma informação inserida. Fornecer uma  `save-as-draft` A opção garante flexibilidade no gerenciamento de tempo, reduz o risco de perda de dados e mantém a precisão dos envios. Você pode salvar formulários como rascunhos para preenchê-los posteriormente.

## Considerações

* [Ativar os componentes principais adaptáveis do Forms para o seu ambiente.](/help/forms/enable-adaptive-forms-core-components.md)

* Certifique-se de que o [o componente principal está definido para a versão 3.0.24 ou posterior](https://github.com/adobe/aem-core-forms-components) para usar este recurso.
* Certifique-se de que você tenha um [Conta de armazenamento do Azure e uma chave de acesso](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal) para autorizar o acesso à conta de armazenamento do Azure.

## Salvar um formulário adaptável como rascunho

[!DNL Experience Manager Forms] A Integração de dados (data-integration.md) oferece [!DNL Azure] configuração de armazenamento para integrar formulários com o [!DNL Azure] serviços de armazenamento. O Modelo de dados de formulário (FDM) pode ser usado para criar o Forms adaptável que interage com o [!DNL Azure] servidor para habilitar workflows de negócios.

Para salvar o formulário como rascunho, verifique se você tem uma conta de armazenamento do Azure e uma chave de acesso para autorizar o acesso ao [!DNL Azure] conta de armazenamento. Para salvar um formulário como rascunho, execute as seguintes etapas:

1. [Criar configuração de armazenamento do Azure](#create-azure-storage-configuration)
1. [Configurar o Conector de armazenamento unificado para o Forms Portal](#configure-usc-forms-portal)
1. [Criar regra para salvar um formulário adaptável como rascunho](#rule-to-save-adaptive-form-as-draft)


### 1. Criar configuração de armazenamento do Azure {#create-azure-storage-configuration}

Uma vez, você tem uma conta de armazenamento do Azure e uma chave de acesso para autorizar o acesso ao [!DNL Azure] conta de armazenamento, execute as seguintes etapas para criar a configuração de Armazenamento do Azure:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Armazenamento do Azure]**.

   ![Seleção do Cartão de Armazenamento do Azure](/help/forms/assets/save-form-as-draft-azure-card.png)

1. Selecione uma pasta de configuração para criar a configuração e selecione **[!UICONTROL Criar]**.

   ![Selecionar pasta de configuração de armazenamento do Azure](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. Especifique um título para a configuração no campo **[!UICONTROL Título]** campo.
1. Especifique o nome do [!DNL Azure] conta de armazenamento na **[!UICONTROL Conta de armazenamento do Azure]** e **[!UICONTROL Chave de Acesso do Azure]** campos.

   ![Configuração de armazenamento do Azure](/help/forms/assets/save-form-as-draft-azure-storage.png)

1. Clique em **Salvar**.

>[!NOTE]
>
> Você pode recuperar a variável **[!UICONTROL Conta de armazenamento do Azure]** e **[!UICONTROL Chave de Acesso do Azure]** do [Portal do Microsoft Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).


### 2. Configurar o Conector de armazenamento unificado para o Forms Portal {#configure-usc-forms-portal}

Depois de criar com êxito a Configuração de Armazenamento do Azure, configure o Conector de Armazenamento Unificado para o Forms Portal, usando as seguintes etapas:

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Conector de armazenamento unificado]**.

   ![Armazenamento de conector unificado](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. No **[!UICONTROL Portal Forms]** , selecione **[!UICONTROL Azure]** do **[!UICONTROL Armazenamento]** lista suspensa.
1. Especifique a [caminho de configuração para a configuração de armazenamento do Azure](#create-azure-storage-configuration) no **[!UICONTROL Caminho de configuração de armazenamento]** campo.

   ![Configuração de armazenamento de conector unificado](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. Selecionar **[!UICONTROL Salvar]** e selecione **[!UICONTROL Publish]** para publicar a configuração.

### 3. Criar regras para salvar um Formulário adaptável como rascunho {#rule-to-save-adaptive-form-as-draft}

Para salvar um formulário como Rascunho, crie um **Salvar formulário** regra em um componente de formulário, como um botão. Quando o botão é clicado, a regra é acionada e o formulário é salvo como rascunho. Execute as seguintes etapas para criar **Salvar formulário** regra em um componente de botão:

1. Na instância do Autor, abra um Formulário adaptável em um modo de edição.
1. No painel esquerdo, selecione ![Ícone Componentes](assets/components_icon.png) e arraste o **[!UICONTROL Botão]** componente ao formulário.
1. Selecione o **[!UICONTROL Botão]** e selecione o ![Ícone Configurar](assets/configure_icon.png).
1. Selecione o **[!UICONTROL Editar regras]** ícone para abrir o Editor de regras.
1. Selecionar **[!UICONTROL Criar]** para configurar e criar a regra.
1. No **[!UICONTROL Quando]** , selecione **foi clicado** e no **[!UICONTROL Depois]** , selecione a **Salvar formulário** opção.
1. Selecionar **[!UICONTROL Concluído]** para salvar a regra.

![Criar regra para o botão](/help/forms/assets/save-form-as-drfat-create-rule.png)

Ao visualizar um Formulário adaptável, preencha-o e clique em **Salvar formulário** for salvo como rascunho para uso posterior.

## Componente Rascunhos e envios para listar rascunhos na página do AEM Sites

A AEM Forms fornece a **Rascunhos e envios** componente de portal pronto para uso para exibir formulários salvos em páginas do AEM Sites. A variável **Rascunhos e envios** O componente mostra formulários salvos como rascunhos para conclusão posterior, bem como formulários enviados. Este componente oferece uma experiência personalizada para qualquer usuário conectado, listando os rascunhos e envios relacionados ao Forms adaptável criado pelo usuário.

Você pode usar componentes prontos para uso do Forms Portal para listar rascunhos de formulário na página do AEM Sites. Execute as seguintes etapas para usar o **Rascunhos e envios** componente do portal:

1. [Ativar Componente de Rascunhos e Envios do Forms Portal](#enable-component)
2. [Adicionar componente de Rascunhos e Envios na página do AEM Sites](#Add-drafts-submissions-component)
3. [Configurar o componente de rascunhos e envios](#configure-drafts-submissions-component)

### 1. Ativar rascunhos e envios para o Forms Portal Component{#enable-component}

Para ativar o **[!UICONTROL Rascunhos e envios]** componente na política de modelo, execute as seguintes etapas:

1. Abra a página do AEM Sites em um **Editar** modo.
1. Vá para a **[!UICONTROL Informações da página]** > **[!UICONTROL Editar modelo]**
   ![Editar política de modelo](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Clique em **[!UICONTROL Política]** e selecione o **[!UICONTROL Rascunhos e envios]**  na caixa de seleção **[Nome do projeto do arquétipo AEM] - Forms e Portal de comunicações**.

   ![Seleção de política](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. Clique em **[!UICONTROL Concluído]**.

Depois que um componente de portal é ativado, você pode usá-lo na instância de autor da sua página do AEM Sites.

### 2. Adicionar componente Rascunhos e Envios na página do AEM Sites{#Add-drafts-submissions-component}

Você pode criar e personalizar o Forms Portal em sites criados usando AEM adicionando e configurando os componentes do portal. Certifique-se de que o [O componente Rascunhos e Envios está ativado](#enable-component) antes de usá-los na página do AEM Sites.

Para adicionar um componente, arraste e solte o componente da **Rascunhos e envios** painel de componentes ao contêiner de layout na página ou selecione o ícone adicionar no contêiner de layout e adicione o componente na **[!UICONTROL Inserir novo componente]** diálogo.

![Adicionar Componente de Rascunho e Submissão](/help/forms/assets/save-form-as-draft-add-dns.png)

### 3. Configurar o componente Rascunhos e Envios {#configure-drafts-submissions-component}

A variável **Rascunhos e envios** O componente exibe os formulários salvos como rascunho para preencher formulários e enviados posteriormente. Para configurar **Rascunhos e envios**, execute as seguintes etapas:
1. Selecione o **Rascunhos e envios** componente.
1. Clique em ![Ícone Configurar](assets/configure_icon.png) e a caixa de diálogo é exibida.
1. No **[!UICONTROL Rascunhos e envios]** especifique o seguinte:
   * **Título** Para identificar um componente em uma página de Sites e, por padrão, o título é exibido na parte superior do componente.
   * **Tipo**: Para indicar a listagem do form como forms preliminares ou submetidos.
   * **Layout**: para exibir a lista de formulários de rascunho ou formulários enviados no formato de cartão ou lista.

   ![Propriedades do componente de Rascunho e Submissão](/help/forms/assets/save-form-as-draft-dns-properties.png)

1. Clique em **Concluído**.

Quando **[!UICONTROL Selecionar tipo]** está selecionado como **Forms de rascunho**, os formulários salvos como rascunhos serão exibidos:
![Ícone Rascunhos](assets/drafts-component.png)

Quando **[!UICONTROL Selecionar tipo]** está selecionado como **Forms enviado**, os formulários enviados aparecem:

![Ícone Envios](assets/submission-listing.png)

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
