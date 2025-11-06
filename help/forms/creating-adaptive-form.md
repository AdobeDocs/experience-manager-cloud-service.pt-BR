---
title: 'Construtor de formulários: criar formulários com componentes de base'
description: Saiba como usar o construtor de formulários do AEM Forms para criar formulários adaptáveis com componentes de base. Perfeito para criadores de formulários que mantêm formulários existentes ou que trabalham com integrações herdadas.
keywords: construtor de formulários, componentes de base, criar formulários, criador de formulários, formulários adaptáveis, criar formulários, AEM forms, criador de formulários
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 59%

---

# Construtor de formulários: criar formulários com componentes de base {#creating-an-adaptive-form}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |


>[!NOTE]
>
> A Adobe recomenda usar os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base.

O construtor de formulários do AEM Forms permite criar formulários envolventes, responsivos, dinâmicos e adaptáveis. Quer você seja um criador de formulários que mantém formulários com base em bases existentes ou precise criar formulários rapidamente com componentes estabelecidos, o AEM Forms fornece um assistente simples. O assistente fornece uma navegação rápida por guias para selecionar facilmente modelos pré-configurados, estilos, campos e opções de envio.

Antes de começar, saiba mais sobre o tipo de componentes do Forms disponíveis para você:

* [Os Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) são componentes de captura de dados padronizados. Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital. Um desenvolvedor pode personalizar e estilizar facilmente esses componentes. A Adobe recomenda usar esses componentes modernos e extensíveis para desenvolver o Adaptive Forms.

* [Os componentes adaptáveis do Forms Foundation](creating-adaptive-form.md) são componentes de captura de dados clássicos (antigos). Você pode continuar usando-os para editar seus componentes fundamentais já existentes com base no formulário adaptável. Se você estiver criando novos formulários, a Adobe recomenda usar os [Componentes principais do Forms Adaptive](creating-adaptive-form-core-components.md) para criar um Forms Adaptável.



<!-- 

You can choose to create an Adaptive Form based on a form model or schema or without a form model. It is important to carefully choose the form model that not only suits your requirements but extends your existing infrastructural investments and assets. You get to choose from the following options to create an Adaptive Form: 

-->

![Assistente para criar um formulário adaptável](/help/release-notes/assets/wizard.png)

<!-- 

Adaptive Forms allow you to create forms that are engaging, responsive, dynamic, and adaptive. [!DNL AEM Forms] provides an intuitive wizard and out-of-the-box components to create Adaptive Forms. You can choose to create an Adaptive Form based on a form model or schema or without a form model. It is important to carefully choose the form model that not only suits your requirements but extends your existing infrastructural investments and assets. You get to choose from the following options to create an Adaptive Form:

* **Using a form data model**
  [Data integration](data-integration.md) lets you integrate entities and services from disparate data sources in to a Form Data Model that you can use to create Adaptive Forms. Choose Form Data Model if the Adaptive Form you are creating involves fetching and write data from and to multiple data source.

  <!--  * **Using an XDP Form Template**
   It is an ideal form model if you have investments in XFA-based or XDP forms. It provides a direct way to convert your XFA-based forms into Adaptive Forms. Any existing XFA rules are retained in the associated Adaptive Forms. The resulting Adaptive Forms support XFA constructs, such as validations, events, properties, and patterns. 

* **Using an XML Schema Definition (XSD) or a JSON Schema**
   XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate the schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available for use in the Data Model Objects tab of the Content browser when authoring Adaptive Forms.

* **Using none or without a form model**
   Adaptive Forms created with this option do not use any form model. The data XML generated from such forms has flat structure with fields and corresponding values. -->

## Pré-requisitos

Você precisará do seguinte para criar um formulário adaptável:

* **Permissões**: adicione seus usuários ao [!DNL forms-users] para fornecer-lhes permissões para criar Formulários adaptáveis. Para obter uma lista detalhada de grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

* **Um tema de formulários adaptáveis**: um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Ao aplicar um tema, o estilo especificado é refletido nos componentes correspondentes. Você pode [criar um tema](themes.md) ou [importar um tema existente](import-export-forms-templates.md#uploading-a-theme). Também é possível pode implantar o [arquétipo mais recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=pt-BR#create-project) para alguns temas de amostra.

* **Um modelo de formulário adaptável**: um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um Formulário adaptável. Ele tem componentes pré-formatados que contêm determinadas propriedades e estrutura de conteúdo. Também fornece as opções para definir um tema e uma ação de envio. O tema define a aparência, e a ação de envio define a ação a ser executada no envio de um formulário adaptável. Por exemplo, enviar os dados coletados para uma fonte de dados. Os serviços na nuvem oferecem suporte a dois tipos de modelos:

   * **Modelo editável**: você pode [criar um](template-editor.md) ou [importar um modelo editável existente](migrate-to-forms-as-a-cloud-service.md). Você também pode implantar o [arquétipo mais recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=pt-BR#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20are%20Java-based%20integration%20tests.) para obter alguns modelos editáveis de amostra.

   * **Modelo estático**: esses são modelos herdados e são recomendados apenas para clientes que estão migrando do Adobe Managed Services (AMS) e de instalações locais do AEM Forms (AEM Forms 6.5 ou anterior). Eles permitem continuar usando seu investimento já existente em modelos estáticos. Ao criar um Formulário adaptável, use um Modelo editável.



## Criar um formulário adaptável (componentes de base) {#create-an-adaptive-form-foundation-components}

1. Acessar a Instância de criação do [!DNL Experience Manager Forms]. Pode ser uma instância da nuvem ou uma instância de desenvolvimento local.

1. Insira suas credenciais na página de logon do Experience Manager.

   Depois de fazer logon, no canto superior esquerdo, selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O Assistente será aberto.
1. Na guia Origem, selecione um modelo:

   * Ao selecionar um modelo Editável, um tema e uma ação de envio especificados no modelo são selecionados automaticamente e o botão **[!UICONTROL Criar]** será habilitado. Você pode ir para as guias **[!UICONTROL Estilo]** ou **[!UICONTROL Envio]** para selecionar um tema ou uma ação de envio diferente. Se o modelo Editável selecionado não especificar um tema, o botão Criar permanecerá desabilitado. É possível ir para a guia **[!UICONTROL Estilos]** para selecionar um tema manualmente.

     >[!NOTE]
     >
     > Você também pode criar um modelo de [!UICONTROL Documento do registro] usando o editor de Formulários adaptáveis. Para obter mais informações, consulte [Suporte a documento de registro no editor de formulário adaptável](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

   * Ao selecionar um modelo estático, as opções de dados, estilo, envio, entrega e visualização não estarão disponíveis. Ao criar um Formulário adaptável, use um Modelo editável.

1. Na guia **[!UICONTROL Estilo]**, selecione um tema:

   * Quando o modelo selecionado especifica um tema, ele é selecionado automaticamente no assistente. Você também pode escolher um tema diferente da guia de Estilo.
   * Se o modelo selecionado não especificar um tema, será possível usar a guia de Estilo para escolher um tema. O botão **[!UICONTROL Criar]** só será habilitado depois que um tema for selecionado.

1. (Opcional) Na guia **[!UICONTROL Dados]**, selecione um modelo de dados:

   * **Modelo de dados de formulário**: um [Modelo de dados de formulário](data-integration.md) permite integrar entidades e serviços de diferentes fontes de dados a um formulário adaptável. Escolha Modelo de dados de formulário (FDM) se o Formulário adaptável que você está criando envolver a busca e a gravação de dados de e para várias fontes de dados.

   * **Esquema JSON**: o [Esquema JSON](adaptive-form-json-schema-form-model.md) representa a estrutura na qual os dados são produzidos ou consumidos pelo sistema back-end em sua organização. É possível associar o esquema a um formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao formulário adaptável. Os elementos do esquema estão disponíveis para uso na guia Objetos do modelo de dados do navegador de conteúdo ao criar o Adaptive Forms e todos os campos também são adicionados ao Formulário adaptável criado.

   Por padrão, todos os campos do modelo de dados são selecionados. Ao criar o formulário adaptável, todos os campos de modelo de dados selecionados são convertidos nos componentes de formulários adaptáveis correspondentes. O assistente fornecerá caixas de seleção para selecionar apenas os campos que devem ser incluídos no formulário adaptável.

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. Na guia **[!UICONTROL Envio]**, selecione uma ação de envio:

   * Ao selecionar um modelo, a ação de envio especificada no modelo é selecionada automaticamente. É possível selecionar uma ação de envio diferente na guia Envio. A guia **[!UICONTROL Envio]** exibe todas as ações de envio disponíveis.

   * Quando o modelo selecionado não especificar uma ação de envio, você poderá usar a guia **[!UICONTROL Envio]** para selecionar uma

1. (Opcional) Na guia Entrega, é possível especificar uma data de publicação ou cancelamento de publicação para um Formulário adaptável.

1. Selecione **[!UICONTROL Criar]**. Uma caixa de diálogo para especificar o título, o nome e o local para salvar o Formulário adaptável será exibida:

   * **[!UICONTROL Título]** especifica o nome de exibição do formulário. O título ajuda a identificar o formulário na interface do usuário do [!DNL Experience Manager Forms].
   * **[!UICONTROL Nome:]** especifica o nome do formulário. Um nó com o nome especificado será criado no repositório. Ao começar a digitar um título, o valor do campo de nome é gerado automaticamente. É possível alterar o valor sugerido. O campo de nome pode incluir apenas caracteres alfanuméricos, hifens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.
   * **[!UICONTROL Caminho:]** especifica o local no qual o Formulário adaptável deverá ser salvo. É possível salvar o formulário adaptável diretamente em `/content/dam/formsanddocuments` ou criar uma pasta como `/content/dam/formsanddocuments/adaptiveforms` para salvar um Formulário adaptável. Certifique-se de criar a pasta antes de usá-la no caminho. O campo **[!UICONTROL Caminho:]** não cria uma pasta automaticamente.

1. Selecione **[!UICONTROL Criar]**. Um Formulário adaptável será criado e aberto no editor de Formulários adaptáveis. O editor exibirá o conteúdo disponível no modelo. Ele também exibe a barra lateral para personalizar o formulário criado de acordo com as necessidades.

   Com base no tipo de Formulário adaptável, os elementos de formulário presentes no esquema JSON do <!--XFA form template, XML schema or --> associado ou no Modelo de Dados de Formulário (FDM) são exibidos na guia **[!UICONTROL Objetos do Modelo de Dados]** do **[!UICONTROL Navegador de Conteúdo]** na barra lateral. Também é possível arrastar e soltar esses elementos para criar seu formulário adaptável.

<!-- ## Create an Adaptive Form based on a Form Data Model {#fdm}

[Data integration](data-integration.md) lets you integrate multiple data sources and bring their entities and services together to create a form data model. It is an extension of JSON schema. You can use a Form Data Model to create an Adaptive Form. The entities or data model objects configured in a Form Data Model are available as data model objects for form authoring. They are bound to respective data sources and used to prefill a form and write submitted data back to the respective data sources. You can also call services configured in a Form Data Model using Adaptive Form rules.

To use a Form Data Model for creating an Adaptive Form:

1. In Form Model tab on Add Properties screen, select **[!UICONTROL Form Data Model]** in the **[!UICONTROL Select From]** drop-down list.

   ![Create an Adaptive Form](assets/create-af-1-1.png)

1. Select to expand **[!UICONTROL Select Form Data Model]**. All available form data models are listed.Select a from data model.

>[!NOTE]
>
>You can also change the Form Data Model for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model).

## Build an adaptive form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate a schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available in the Data Model Object tab of the content browser for authoring Adaptive Forms. You can drag-drop the schema elements to build the form.

See the following documents to understand how to design XML or JSON schema for authoring Adaptive Forms.

* [Creating Adaptive Forms using XML schema](adaptive-form-xml-schema-form-model.md)
* [Creating Adaptive Forms using JSON schema](adaptive-form-json-schema-form-model.md)

Do the following to use XML or JSON schema as form model for an Adaptive Form:

1. On the **[!UICONTROL Add Properties]** step of Adaptive Form creation page, select on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Select **[!UICONTROL Select Schema]** and do one of the following:

    * **[!UICONTROL Upload from disk]** - Select this option and select Upload Schema Definition to browse and upload an XML schema or JSON schema from your file system. The uploaded schema file resides with the form and is not accessible to other Adaptive Forms.
    * **[!UICONTROL Search in repository]** - Select this option to select from the list of schema definition files available in the repository. Select the XML or JSON schema file as form model. The selected schema is associated with the form by reference and is accessible for use in other Adaptive Forms.

      Ensure that the JSON schema filename ends with **.schema.json**. For example: mySchema.schema.json

   ![Selecting XML or JSON schema](assets/upload-schema.png)
**Figure:** *Selecting XML or JSON schema*

1. (For XML schema only) After you select or upload an XML Schema, specify a root element of the selected XSD file to map with the Adaptive Form.

   ![Selecting XSD root element](assets/xsd-root-element.png)
**Figure:** *Selecting XSD root element*

>[!NOTE]
>
>You can also change the schema for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model). -->

## Editar propriedades do modelo de formulário de um formulário adaptável {#edit-form-model}

Você pode alterar o modelo de formulário para um formulário adaptável (com base em JSON ou Modelo de dados de formulário). Não é possível alterar de um modelo de formulário para outro.

1. Selecione o Formulário adaptável e o ícone **Propriedades**.
1. Abra a guia **[!UICONTROL Modelo de Formulário]** e siga um destes procedimentos.

   * Se o formulário adaptável não tiver um modelo de formulário, você poderá escolher outro modelo de formulário e selecionar o esquema XML ou JSON do <!-- a form template, --> ou o modelo de dados de formulário (FDM).
   * Se o formulário adaptável for baseado em um modelo de formulário, você poderá escolher outro esquema XML ou JSON do <!-- form template, --> ou o Modelo de dados de formulário (FDM) para o mesmo modelo de formulário.

1. Selecione **[!UICONTROL Salvar]** para salvar as propriedades.

Você também pode modificar as propriedades do modelo de formulário no Criador de formulários adaptáveis ou no Criador de modelos de formulários adaptáveis.

1. Selecione o componente **[!UICONTROL Container de Formulário Adaptável (raiz)]**.
1. Clique no ![Ícone de Configurar](/help/forms/assets/configure-icon.svg) para abrir as **[!UICONTROL Propriedades]** do container do formulário adaptável.
1. Selecione a guia **[!UICONTROL Modelo de Dados]** e siga um destes procedimentos:

   * Se o formulário adaptável não tiver um modelo de formulário, você poderá escolher um modelo de formulário e selecionar o esquema XML ou JSON do <!-- a form template, --> ou o modelo de dados de formulário (FDM).
   * Se o formulário adaptável for baseado em um modelo de formulário, não será possível alterar o modelo de formulário. Você pode escolher outro esquema XML ou JSON <!-- form template, --> ou o Modelo de dados de formulário (FDM) para o mesmo modelo de formulário aplicável.
1. Selecione ![Salvar](/help/forms/assets/check-button.png) para salvar as propriedades.

![FDM-Schema-Support](/help/forms/assets/fdmsupport.png)

>[!NOTE]
>
> Você também pode salvar um Formulário adaptável como um modelo. Para obter mais informações, consulte [Criação de um modelo usando um formulário adaptável](/help/forms/template-editor.md#saving-an-adaptive-form-as-template-saving-adaptive-form-as-template).

## Como renomear um formulário adaptável do AEM? {#rename-an-AEM-Adaptive-Form}

Para renomear um formulário adaptável, execute as seguintes etapas:

1. Selecione um formulário adaptável na interface do usuário do AEM Forms.
1. Clique nas **Propriedades** localizadas no painel superior.
1. Altere o nome do formulário na guia **Título**, conforme mostrado na imagem abaixo.
1. Clique em **Salvar e fechar**.

![Renomear um Formulário adaptável do AEM](/help/forms/assets/change-af-name.png)

## Consulte também: {#see-also}

{{see-also}}
