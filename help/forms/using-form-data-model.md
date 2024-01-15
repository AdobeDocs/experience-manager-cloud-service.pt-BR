---
title: Como podemos criar um modelo de dados de formulário para um formulário adaptável?
description: Saiba como criar Forms adaptável e fragmentos com base em um modelo de dados de formulário (FDM). Gere e edite dados de amostra para objetos de modelo de dados no FDM.
feature: Adaptive Forms, Form Data Model
role: Admin, User
level: Beginner, Intermediate
exl-id: 827ce457-6585-46fb-8e28-1d970a40d949
source-git-commit: 527c9944929c28a0ef7f3e617ef6185bfed0d536
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 2%

---

# Utilizar modelo de dados do formulário {#use-form-data-model}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/using-form-data-model.html) |
| AEM as a Cloud Service | Este artigo |


![integração de dados](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] a integração de dados permite usar fontes de dados de back-end diferentes para criar um Modelo de dados de formulário que você pode usar como esquema em vários Forms adaptáveis <!--and interactive communications--> fluxos de trabalho. Ele requer a configuração de fontes de dados e a criação do Modelo de dados de formulário com base nos objetos e serviços do modelo de dados disponíveis nas fontes de dados. Para obter mais informações, consulte o seguinte:

* [[!DNL Experience Manager Forms] Integração de dados](data-integration.md)
* [Configurar fontes de dados](configure-data-sources.md)
* [Criar modelo de dados de formulário](create-form-data-models.md)
* [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md)

Um modelo de dados de formulário é uma extensão do esquema JSON que você pode usar para:

* [Criar Forms adaptável e fragmentos](#create-af)
  <!--* [Create interactive communications and building blocks like text, list, and condition fragments](#create-ic)-->
* [Visualizar com dados de amostra](#preview-ic)
* [uso do serviço de modelo de dados de formulário](#prefill)
* [Gravar dados do Formulário adaptável enviados de volta nas fontes de dados](#write-af)
* [Chamar serviços usando regras do Formulário adaptável](#invoke-services)

## Criar Forms adaptável e fragmentos {#create-af}

Você pode criar [Forms adaptável](creating-adaptive-form.md) e fragmentos de formulário adaptável <!-- [Adaptive Form Fragments](adaptive-form-fragments.md) --> com base em um modelo de dados de formulário. Faça o seguinte para usar um modelo de dados de formulário ao criar um formulário adaptável ou um fragmento de formulário adaptável:

1. Na guia Modelo de formulário na tela Adicionar propriedades, selecione **[!UICONTROL Modelo de dados do formulário]** no **[!UICONTROL Selecionar de]** lista suspensa.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Selecionar para expandir **[!UICONTROL Selecionar modelo de dados do formulário]**. Todos os modelos de dados de formulário disponíveis estão listados.

   Selecione um do modelo de dados.

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**Somente fragmentos de formulário adaptável**) Você pode criar um fragmento de formulário adaptável com base em apenas um objeto de modelo de dados em um modelo de dados de formulário. Expandir **[!UICONTROL Definições do modelo de dados de formulário]** menu suspenso. Ele lista todos os objetos do modelo de dados no modelo de dados de formulário especificado. Selecione um objeto de modelo de dados na lista.

   ![create-af-3](assets/create-af-3.png)

   Depois que o formulário adaptável ou o fragmento de formulário adaptável baseado em um modelo de dados de formulário for criado, os objetos do modelo de dados de formulário aparecerão no **[!UICONTROL Fontes de dados]** do Navegador de conteúdo no editor de Formulário adaptável.

   >[!NOTE]
   >
   >Para um Fragmento de formulário adaptável, somente o objeto de modelo de dados selecionado no momento da criação e seus objetos de modelo de dados associados aparecem na guia Fontes de dados.

   ![data-model-objects-tab](assets/data-model-objects-tab.png)

   Você pode arrastar e soltar objetos de modelo de dados no Formulário adaptável ou fragmento para adicionar campos de formulário. Os campos de formulário adicionados retêm as propriedades de metadados e a vinculação com as propriedades do objeto de modelo de dados. O vínculo garante que os valores de campo sejam atualizados nas fontes de dados correspondentes no envio do formulário e preenchidos previamente quando o formulário for renderizado.

<!-- ## Create interactive communications {#create-ic}

You can create an interactive communication based on a Form Data Model that you can use to prefill interactive communication with data from configured data sources. In addition, the building blocks of an interactive communication, such as text, list, and condition document fragments can be based on a form data model.

You can choose a Form Data Model when creating an interactive communication or a document fragment. The following image shows the General tab of the Create Interactive Communication dialog.

![create-ic](assets/create-ic.png)

General tab of Create Interactive Communication dialog

For more information, see:

[Create an interactive communication](create-interactive-communication.md)

[Text in Interactive Communications](texts-interactive-communications.md)

[Conditions in Interactive Communications](conditions-interactive-communications.md)

[List fragments](lists.md) -->

## Visualizar com dados de amostra {#preview-ic}

O editor de modelo de dados de formulário permite gerar e editar dados de amostra para objetos de modelo de dados no modelo de dados de formulário. Você pode usar esses dados para visualizar e testar <!--interactive communications and--> Forms adaptável. Você deve gerar os dados de amostra antes de visualizar como descrito em [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md#sample).

<!--To preview an interactive communication with sample Form Data Model data:

1. On [!DNL  Experience Manager] author instance, navigate to **[!UICONTROL Forms > Forms & Documents]**.
1. Select an interactive communication and select **[!UICONTROL Preview]** in the toolbar to select **[!UICONTROL Web Channel]**, **[!UICONTROL Print Channel]**, or **[!UICONTROL Both Channels]** to preview the interactive communication.
1. In the Preview [*channel*] dialog, ensure that **[!UICONTROL Test Data of Form Data Model]** is selected and select **[!UICONTROL Preview]**.

The interactive communication opens with prefilled sample data.

![web-preview](assets/web-preview.png)-->

Para visualizar um formulário adaptável com dados de amostra, abra o formulário adaptável no modo de autor e selecione **[!UICONTROL Visualizar]**.

## Preencher previamente usando o serviço de modelo de dados de formulário {#prefill}

[!DNL Experience Manager Forms] O fornece o Serviço de preenchimento prévio do modelo de dados de formulário pronto para uso que você pode ativar para o Adaptive Forms <!--and interactive communications--> com base no modelo de dados do formulário. O serviço de preenchimento prévio consulta as fontes de dados para objetos de modelo de dados no Formulário adaptável <!--and interactive communication--> e, portanto, preenche os dados enquanto renderiza o formulário ou a comunicação.

Para habilitar o Serviço de preenchimento do modelo de dados de formulário para um formulário adaptável, abra as propriedades do Contêiner de formulário adaptável e selecione **[!UICONTROL Serviço de preenchimento do modelo de dados de formulário]** do **[!UICONTROL Preencher Serviço]** na opção Básico. Em seguida, salve as propriedades.

![serviço de preenchimento](assets/prefill-service.png)

<!--To configure Form Data Model prefill service in an interactive communication, you can select Form Data Model Prefill Service in the Prefill Service drop-down while creating it or later by modifying the properties.

![edit-ic-props](assets/edit-ic-props.png)

Edit Properties dialog for an interactive communication-->

## Gravar dados do Formulário adaptável enviado nas fontes de dados {#write-af}

Quando um usuário envia um formulário com base em um modelo de dados de formulário, você pode configurar o formulário para gravar dados enviados de um objeto de modelo de dados em suas fontes de dados. Para obter esse caso de uso, [!DNL Experience Manager Forms] fornecer [Ação de envio do modelo de dados de formulário](configuring-submit-actions.md), disponível pronto para uso somente para o Adaptive Forms com base em um modelo de dados de formulário. Ele grava dados enviados para um objeto de modelo de dados em sua fonte de dados.

Para configurar a Ação de envio do modelo de dados de formulário, abra as propriedades do Contêiner de formulário adaptável e selecione **[!UICONTROL Enviar usando modelo de dados do formulário]** no menu suspenso Enviar ação, na opção Envio. Em seguida, procure e selecione um objeto de modelo de dados na **[!UICONTROL Nome do objeto de modelo de dados a ser enviado]** menu suspenso. Salve as propriedades.

No envio do formulário, os dados do objeto de modelo de dados configurado são gravados na respectiva fonte de dados.

<!--![data-submission](assets/data-submission.png)-->

Você também pode enviar anexos de formulário para uma fonte de dados usando a propriedade de objeto de modelo de dados binários. Faça o seguinte para enviar anexos para uma origem de dados JDBC:

1. Adicione um objeto de modelo de dados que inclua uma propriedade binária ao modelo de dados de formulário.
1. No Formulário adaptável, arraste e solte a **[!UICONTROL Anexo de arquivo]** componente do navegador Componentes no Formulário adaptável.
1. Selecione para selecionar o componente adicionado e ![settings_icon](assets/configure-icon.svg) para abrir o navegador Propriedades do componente.
1. No campo Referência de vinculação, selecione ![foldersearch_18](assets/folder-search-icon.svg) e navegue para selecionar a propriedade binária adicionada no modelo de dados de formulário. Configure outras propriedades, conforme apropriado.

   Selecionar ![botão de seleção](assets/save_icon.svg) para salvar as propriedades. O campo de anexo agora está associado à propriedade binária do modelo de dados de formulário.

1. Na seção Envio das propriedades do Contêiner de formulário adaptável, ative **[!UICONTROL Enviar anexos do formulário]**. Ele envia o anexo no campo de propriedade binária para a fonte de dados no envio do formulário.

## Chamar serviços no Adaptive Forms usando regras {#invoke-services}

Em um Formulário adaptável baseado em um modelo de dados de formulário, você pode [criar regras](rule-editor.md) para chamar serviços configurados no modelo de dados de formulário. A variável **[!UICONTROL Chamar serviços]** A operação em uma regra lista todos os serviços disponíveis no Modelo de dados de formulário e permite selecionar campos de entrada e saída para o serviço. Você também pode usar a variável **[!UICONTROL Definir valor]** tipo de regra para chamar um serviço de Modelo de dados de formulário e definir o valor de um campo para a saída retornada pelo serviço.

Por exemplo, a regra a seguir chama um serviço get que usa a ID do Funcionário como entrada e os valores retornados são preenchidos nos campos ID do Dependente, Sobrenome, Nome e Gênero correspondentes no formulário.

![invoke-service](assets/invoke-service.png)

Além disso, você pode usar a variável `guidelib.dataIntegrationUtils.executeOperation` API para gravar um JavaScript no editor de código do editor de regras. <!-- For API details, see [API to invoke Form Data Model service](invoke-form-data-model-services.md).-->

### Chamar um modelo de dados de formulário usando funções personalizadas {#invoke-form-data-model-using-custom-functions}

Você pode [chamar um modelo de dados de formulário do editor de regras usando funções personalizadas](/help/forms/rule-editor.md#custom-functions-in-rule-editor-custom-functions). Para chamar o modelo de dados de formulário, adicione um modelo de dados de formulário ao incluo na lista de permissões. Para adicionar um modelo de dados de formulário a uma lista de permissões:

1. Acesse o console da Web do Experience Manager em `https://server:host/system/console/configMgr`.
1. Localizar **[!UICONTROL Lista de permissões no nível do formulário adaptável do modelo de dados de formulário para chamada de serviço - Fábrica de configuração]**.
1. Clique em ![ícone de adição](/help/forms/assets/Smock_Add_18_N.svg) ícone para adicionar a configuração.
1. Adicionar **[!UICONTROL Padrão do caminho de conteúdo]** para especificar a localização do Forms adaptável.  Por padrão, o valor é `/content/forms/af/(.*)` que inclui todo o Adaptive Forms. Você também pode especificar o caminho para um Formulário adaptável específico.
1. Adicionar **[!UICONTROL Padrão de caminho do modelo de dados de formulário]** para especificar o local do modelo de dados de formulário. Por padrão, o valor é `/content/dams/formsanddocuments-fdm/(.*)` que inclui todo o Modelo de dados do formulário. Você também pode especificar o caminho para um modelo de dados de formulário específico.
1. Salve as configurações.

A configuração adicionada é salva em **[!UICONTROL Lista de permissões no nível do formulário adaptável do modelo de dados de formulário para chamada de serviço - Fábrica de configuração]** opção.

>[!VIDEO](https://video.tv.adobe.com/v/3423977/adaptive-forms-custom-function-rule-editor)

>[!NOTE]
>
> Para chamar um modelo de dados de formulário do editor de regras usando funções personalizadas por meio de um projeto de arquétipo AEM:
>
>1. [Criar um arquivo de configuração](https://github.com/adobe/aem-core-forms-components/blob/master/it/config/src/main/content/jcr_root/apps/system/config/com.adobe.aemds.guide.factory.impl.AdaptiveFormFDMConfigurationFactoryImpl~core-components-it.cfg.json).
>1. Definir as propriedades getContentPathPattern e getFormDataModelPathPattern.
>1. Implante o projeto.
