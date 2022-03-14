---
title: Como usar o Modelo de dados de formulário?
description: Saiba como criar Forms adaptável e Fragmentos de formulário adaptáveis com base em um modelo de dados de formulário. Saiba mais sobre como gerar e editar dados de amostra para objetos de modelo de dados no modelo de dados de formulário. Você pode usar esses dados para visualizar e testar o Adaptive Forms.
feature: Form Data Model
role: User
level: Beginner, Intermediate
exl-id: 827ce457-6585-46fb-8e28-1d970a40d949
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 1%

---

# Utilizar modelo de dados do formulário {#use-form-data-model}

![integração de dados](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] a integração de dados permite usar diferentes fontes de dados de backend para criar um Modelo de dados de formulário que pode ser usado como esquema em vários Forms adaptáveis <!--and interactive communications--> fluxos de trabalho. Ela requer a configuração de fontes de dados e a criação de um Modelo de Dados de Formulário com base em objetos e serviços de modelo de dados disponíveis em fontes de dados. Para obter mais informações, consulte:

* [[!DNL Experience Manager Forms] Integração de dados](data-integration.md)
* [Configurar fontes de dados](configure-data-sources.md)
* [Criar modelo de dados de formulário](create-form-data-models.md)
* [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md)

Um Modelo de dados de formulário é uma extensão de esquema JSON que pode ser usada para:

* [Criar Forms adaptável e fragmentos](#create-af)

<!--* [Create interactive communications and building blocks like text, list, and condition fragments](#create-ic)-->
* [Visualizar com dados de amostra](#preview-ic)
* [usando o serviço Modelo de dados de formulário](#prefill)
* [Gravar dados do formulário adaptativo enviados de volta em fontes de dados](#write-af)
* [Chamar serviços usando regras de formulário adaptável](#invoke-services)

## Criar Forms adaptável e fragmentos {#create-af}

Você pode criar [Forms adaptável](creating-adaptive-form.md) e Fragmentos de formulário adaptáveis <!-- [Adaptive Form Fragments](adaptive-form-fragments.md) --> com base em um modelo de dados de formulário. Faça o seguinte para usar um Modelo de dados de formulário ao criar um Formulário adaptável ou Fragmento de formulário adaptável:

1. Na guia Modelo de formulário na tela Adicionar propriedades , selecione **[!UICONTROL Modelo de dados do formulário]** no **[!UICONTROL Selecionar de]** lista suspensa.

   ![create-af-1-1](assets/create-af-1-1.png)

1. Toque para expandir **[!UICONTROL Selecionar Modelo de Dados de Formulário]**. Todos os modelos de dados de formulário disponíveis são listados.

   Selecione um do modelo de dados.

   ![create-af-2-1](assets/create-af-2-1.png)

1. (**Somente fragmentos de formulário adaptáveis**) É possível criar um Fragmento de formulário adaptável com base em apenas um objeto de modelo de dados em um modelo de dados de formulário. Expandir **[!UICONTROL Definições do Modelo de dados de formulário]** lista suspensa. Ele lista todos os objetos de modelo de dados no modelo de dados de formulário especificado. Selecione um objeto de modelo de dados na lista.

   ![create-af-3](assets/create-af-3.png)

   Depois que o formulário adaptável ou o fragmento do formulário adaptável com base em um modelo de dados de formulário for criado, os objetos do Modelo de dados de formulário aparecerão na variável **[!UICONTROL Fontes de dados]** do navegador Conteúdo no editor de formulário adaptável.

   >[!NOTE]
   >
   >Para um Fragmento de formulário adaptável, somente o objeto de modelo de dados selecionado no momento da criação e seus objetos de modelo de dados associados aparecem na guia Fontes de dados.

   ![data-model-objects-tab](assets/data-model-objects-tab.png)

   É possível arrastar e soltar objetos de modelo de dados no Formulário adaptável ou no fragmento para adicionar campos de formulário. Os campos de formulário adicionados mantêm as propriedades de metadados e o vínculo com as propriedades de objetos do modelo de dados. O vínculo garante que os valores do campo sejam atualizados nas fontes de dados correspondentes no envio do formulário e pré-preenchidos no momento em que o formulário for renderizado.

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

O editor de Modelo de dados de formulário permite gerar e editar dados de amostra para objetos de modelo de dados no modelo de dados de formulário. Você pode usar esses dados para visualizar e testar <!--interactive communications and--> Forms adaptável. Você deve gerar os dados de amostra antes de visualizar conforme descrito em [Trabalhar com o modelo de dados de formulário](work-with-form-data-model.md#sample).

<!--To preview an interactive communication with sample Form Data Model data:

1. On [!DNL  Experience Manager] author instance, navigate to **[!UICONTROL Forms > Forms & Documents]**.
1. Select an interactive communication and tap **[!UICONTROL Preview]** in the toolbar to select **[!UICONTROL Web Channel]**, **[!UICONTROL Print Channel]**, or **[!UICONTROL Both Channels]** to preview the interactive communication.
1. In the Preview [*channel*] dialog, ensure that **[!UICONTROL Test Data of Form Data Model]** is selected and tap **[!UICONTROL Preview]**.

The interactive communication opens with prefilled sample data.

![web-preview](assets/web-preview.png)-->

Para visualizar um formulário adaptável com dados de amostra, abra o formulário adaptável no modo de criação e toque em **[!UICONTROL Visualizar]**.

## Preencher previamente usando o serviço do Modelo de dados de formulário {#prefill}

[!DNL Experience Manager Forms] fornece o serviço de preenchimento prévio do modelo de dados de formulário pronto para uso que você pode ativar para o Adaptive Forms <!--and interactive communications--> com base no modelo de dados de formulário. O serviço de preenchimento prévio consulta fontes de dados de objetos de modelo de dados no Formulário adaptável <!--and interactive communication--> e, portanto, preenche os dados ao renderizar o formulário ou a comunicação.

Para ativar o Serviço de preenchimento prévio do modelo de dados de formulário em um formulário adaptável, abra as propriedades do contêiner de formulário adaptável e selecione **[!UICONTROL Serviço de preenchimento prévio do modelo de dados de formulário]** do **[!UICONTROL Serviço de preenchimento prévio]** na opção Básico . Em seguida, salve as propriedades.

![serviço de preenchimento prévio](assets/prefill-service.png)

<!--To configure Form Data Model prefill service in an interactive communication, you can select Form Data Model Prefill Service in the Prefill Service drop-down while creating it or later by modifying the properties.

![edit-ic-props](assets/edit-ic-props.png)

Edit Properties dialog for an interactive communication-->

## Gravar dados enviados do formulário adaptativo em fontes de dados {#write-af}

Quando um usuário envia um formulário com base em um modelo de dados de formulário, é possível configurar o formulário para gravar dados enviados de um objeto de modelo de dados em suas fontes de dados. Para obter esse caso de uso, [!DNL Experience Manager Forms] fornecer [Ação de envio do modelo de dados de formulário](configuring-submit-actions.md), disponível somente para o Adaptive Forms baseado em um modelo de dados de formulário. Ele grava dados enviados para um objeto de modelo de dados em sua fonte de dados.

Para configurar a Ação de envio do modelo de dados de formulário, abra as propriedades do contêiner do formulário adaptável e selecione **[!UICONTROL Enviar usando o Modelo de dados de formulário]** no menu suspenso Enviar ação sob a opção Enviar. Em seguida, navegue e selecione um objeto de modelo de dados no **[!UICONTROL Nome do objeto de modelo de dados a ser enviado]** lista suspensa. Salve as propriedades.

No envio do formulário, os dados do objeto de modelo de dados configurado são gravados na respectiva fonte de dados.

<!--![data-submission](assets/data-submission.png)-->

Também é possível enviar anexos de formulário para uma fonte de dados usando a propriedade de objeto de modelo de dados binário. Faça o seguinte para enviar anexos a uma fonte de dados JDBC:

1. Adicione um objeto de modelo de dados que inclua uma propriedade binária ao modelo de dados de formulário.
1. No formulário adaptável, arraste e solte o **[!UICONTROL Anexo de arquivo]** do navegador Componentes até o Formulário adaptável.
1. Toque para selecionar o componente adicionado e toque em ![settings_icon](assets/configure-icon.svg) para abrir o navegador Propriedades do componente.
1. No campo Referência de associação, toque em ![foldersearch_18](assets/folder-search-icon.svg) e navegue para selecionar a propriedade binária adicionada no modelo de dados de formulário. Configure outras propriedades, conforme apropriado.

   Toque ![botão de seleção](assets/save_icon.svg) para salvar as propriedades. O campo de anexo agora está vinculado à propriedade binária do modelo de dados de formulário.

1. Na seção Envio das propriedades do Contêiner de formulário adaptável, ative **[!UICONTROL Enviar anexos de formulário]**. Ele envia o anexo no campo de propriedade binária para a fonte de dados no envio do formulário.

## Invocar serviços no Adaptive Forms usando regras {#invoke-services}

Em um formulário adaptável baseado em um modelo de dados de formulário, é possível [criar regras](rule-editor.md) para chamar os serviços configurados no modelo de dados de formulário. O **[!UICONTROL Invocar serviços]** em uma regra lista todos os serviços disponíveis no Modelo de dados de formulário e permite selecionar campos de entrada e saída para o serviço. Também é possível usar a variável **[!UICONTROL Definir valor]** tipo de regra para chamar um serviço de Modelo de dados de formulário e definir o valor de um campo para a saída retornada pelo serviço.

Por exemplo, a regra a seguir chama um serviço get que utiliza a ID do Funcionário como entrada e os valores retornados são preenchidos nos campos ID Dependente, Sobrenome, Nome e Gênero correspondentes no formulário.

![invoke-service](assets/invoke-service.png)

Além disso, você pode usar o `guidelib.dataIntegrationUtils.executeOperation` API para gravar um JavaScript no editor de códigos do editor de regras. <!-- For API details, see [API to invoke Form Data Model service](invoke-form-data-model-services.md).-->
