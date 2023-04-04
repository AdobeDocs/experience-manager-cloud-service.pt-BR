---
title: Como criar um formulário adaptável?
description: Saiba como criar um formulário adaptável usando [!DNL Experience Manager Forms]. O Adaptive Forms são formulários HTML5 responsivos que simplificam a coleta e o processamento de informações. Saiba mais sobre como criar um formulário adaptável com base em um Modelo de dados de formulário e esquema XML ou JSON.
feature: Adaptive Forms
role: User, Developer
level: Beginner
exl-id: 38ca5eea-793b-420b-ae60-3a0bd83caf00
source-git-commit: a1830db797a88e43e17d73a2e8cbc979084f6328
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 4%

---

# Criar um formulário adaptável (componentes básicos) {#creating-an-adaptive-form}


Formulários adaptáveis fornecem uma experiência envolvente, responsiva, dinâmica e adaptável. O AEM Forms fornece um assistente para usuários empresariais para criar rapidamente o Adaptive Forms. O assistente tem uma navegação de guia rápida para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um formulário adaptável.

Antes de começar, saiba mais sobre o tipo de componentes do Forms disponíveis para você:

* [Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) são componentes padronizados de captura de dados. Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital. Um desenvolvedor pode personalizar e criar estilos facilmente para esses componentes. O Adobe recomenda o aproveitamento desses componentes modernos e extensíveis para desenvolver o Adaptive Forms.

* [Componentes básicos adaptáveis do Forms](creating-adaptive-form.md) são componentes de captura de dados clássicos (antigos). Você pode continuar a usá-los para editar os componentes de base existentes, com base no Formulário adaptável. Se você estiver criando novos formulários, o Adobe recomenda usar  [Componentes principais adaptáveis do Forms](creating-adaptive-form-core-components.md) para criar um Forms adaptável.



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
   XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate the schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema will be available for use in the Data Model Objects tab of the Content browser when authoring Adaptive Forms.

* **Using none or without a form model**
   Adaptive Forms created with this option don't use any form model. The data XML generated from such forms has flat structure with fields and corresponding values. -->

## Pré-requisitos

Você precisa do seguinte para criar um formulário adaptável:

* **Permissões**: Adicione seus usuários a [!DNL forms-users] para fornecer permissões para criar um formulário adaptável. Para obter uma lista detalhada dos grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

* **Um tema de formulário adaptável**: Um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de plano de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica um tema, o estilo especificado reflete nos componentes correspondentes. Você pode [criar um novo tema](themes.md) ou [importar um tema existente](import-export-forms-templates.md#uploading-a-theme). Você também pode implantar o [arquétipo mais recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html#create-project) para alguns temas de amostra.

* **Um modelo de formulário adaptável**: Um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um formulário adaptável. Ele tem componentes pré-formatados contendo determinadas propriedades e estrutura de conteúdo. Também fornece as opções para definir um tema e uma ação de envio. O tema define a ação de aparência e envio define a ação a ser executada no envio de um formulário adaptável. Por exemplo, enviar os dados coletados para uma fonte de dados. O serviço em nuvem oferece suporte a dois tipos de modelos:

   * **Modelo editável**: Você pode [criar um novo](template-editor.md) ou [importar um template editável existente](migrate-to-forms-as-a-cloud-service.md). Você também pode implantar o [arquétipo mais recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20são%20integração%20baseada em Java%20testes.) para obter algumas amostras de modelos editáveis.

   * **Modelo estático**: Esses são modelos herdados e são recomendados apenas para clientes que estão migrando do Adobe Managed Services (AMS) e instalações locais do AEM Forms (AEM 6.5 Forms ou anterior). Isso permite que você continue aproveitando seu investimento existente em modelos estáticos. Quando você cria um novo formulário adaptável, é recomendável usar um modelo editável.



## Criar um formulário adaptável (componentes básicos) {#create-an-adaptive-form-foundation-components}

1. Acesso [!DNL Experience Manager Forms] Instância do autor. Pode ser uma instância do Cloud ou uma instância de desenvolvimento local.

1. Insira suas credenciais na página de logon do Experience Manager.

   Depois de fazer logon, no canto superior esquerdo, toque em **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.

1. Toque **[!UICONTROL Criar]**  > **[!UICONTROL Forms adaptável]**. O Assistente é aberto.
1. Na guia Source , selecione um template:

   * Ao selecionar um modelo editável, um tema e uma ação de envio especificada no modelo são selecionados automaticamente e o **[!UICONTROL Criar]** estiver ativado. Você pode ir para o **[!UICONTROL Estilo]** ou **[!UICONTROL Submissão]** guias para selecionar um tema diferente ou enviar uma ação. Se o modelo Editável selecionado não especificar um tema, o botão criar permanecerá desativado. Você pode ir para o **[!UICONTROL Estilos]** para selecionar manualmente um tema.

      >[!NOTE]
      >
      > Você também pode criar [!UICONTROL Documento de registro] usando um editor adaptável do Forms. Para obter mais informações, consulte [Suporte para documento de registro no editor de formulário adaptável](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

   * Quando você seleciona um template estático, as opções de dados, estilo, envio, delivery e visualização não estão disponíveis. Quando você cria um novo formulário adaptável, é recomendável usar um modelo editável.

1. No **[!UICONTROL Estilo]** selecione um tema:

   * Quando o template selecionado especifica um tema, o tema é selecionado automaticamente no assistente. Também é possível escolher um tema diferente na guia Style .
   * Se o modelo selecionado não especificar um tema, você pode usar a guia Style para escolher um tema. O **[!UICONTROL Criar]** é ativado somente depois que um tema é selecionado.

1. (Opcional) Na seção **[!UICONTROL Dados]** selecione um modelo de dados:

   * **Modelo de dados do formulário**: A [Modelo de dados do formulário](data-integration.md) O permite integrar entidades e serviços de diferentes fontes de dados a um Formulário adaptável. Escolha Modelo de dados de formulário se o Formulário adaptável que você está criando envolver a busca e gravação de dados de e para várias fontes de dados.

   * **Esquema JSON**: [Esquema JSON](adaptive-form-json-schema-form-model.md) representa a estrutura na qual os dados são produzidos ou consumidos pelo sistema de back-end em sua organização. Você pode associar o esquema a um formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao formulário adaptável. Os elementos do esquema estão disponíveis para uso na guia Objetos do modelo de dados do navegador Conteúdo ao criar o Adaptive Forms e todos os campos também são adicionados ao Formulário adaptável recém-criado.

   Por padrão, todos os campos do modelo de dados são selecionados. Quando você cria o Formulário adaptativo, todos os campos do modelo de dados selecionados são convertidos em componentes do Formulário adaptável correspondentes. O assistente fornece caixas de seleção para selecionar apenas os campos que devem ser incluídos no formulário adaptável.

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. No **[!UICONTROL Submissão]** selecione uma ação enviar:

   * Quando você seleciona um modelo, a ação de envio especificada no modelo é selecionada automaticamente. Você pode selecionar uma ação de envio diferente da guia Enviar. O **[!UICONTROL Submissão]** exibe todas as ações de envio disponíveis.

   * Quando o modelo selecionado não especifica uma ação de envio, você pode usar a variável **[!UICONTROL Submissão]** para selecionar uma ação enviar

1. (Opcional) Na guia Delivery , é possível especificar uma data de publicação ou de cancelamento da publicação para um Formulário adaptável.

1. Toque **[!UICONTROL Criar]**. Uma caixa de diálogo para especificar o título, o nome e o local para salvar o Formulário adaptativo é exibida:

   * **[!UICONTROL Título]** Especifica o nome de exibição do formulário. O título ajuda a identificar o formulário no [!DNL Experience Manager Forms] interface do usuário.
   * **[!UICONTROL Nome:]** Especifica o nome do formulário. Um nó com o nome especificado é criado no repositório. À medida que você começa a digitar um título, o valor do campo de nome é gerado automaticamente. Você pode alterar o valor sugerido. O campo de nome pode incluir somente caracteres alfanuméricos, hifens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.
   * **[!UICONTROL Caminho:]** Especifica o local em que o formulário adaptativo deve ser salvo. Você pode salvar o formulário adaptável diretamente em `/content/dam/formsanddocuments` ou criar uma pasta como `/content/dam/formsanddocuments/adaptiveforms` para salvar um formulário adaptável. Certifique-se de criar a pasta antes de usá-la no caminho. O **[!UICONTROL Caminho:]** não cria uma pasta automaticamente.

1. Toque **[!UICONTROL Criar]**. Um formulário adaptável é criado e aberto no editor do Adaptive Forms. O editor exibe o conteúdo disponível no template. Também exibe a barra lateral para personalizar o formulário recém-criado de acordo com as necessidades.

   Com base no tipo de formulário adaptável, os elementos de formulário presentes no <!--XFA form template, XML schema or --> O esquema JSON ou o Modelo de dados de formulário são exibidos no **[!UICONTROL Objetos do modelo de dados]** da guia **[!UICONTROL Navegador de conteúdo]** na barra lateral. Também é possível arrastar e soltar esses elementos para criar o Formulário adaptável.

<!-- ## Create an Adaptive Form based on a Form Data Model {#fdm}

[Data integration](data-integration.md) lets you integrate multiple data sources and bring their entities and services together to create a form data model. It is an extension of JSON schema. You can use a Form Data Model to create an Adaptive Form. The entities or data model objects configured in a Form Data Model are available as data model objects for form authoring. They are bound to respective data sources and used to prefill a form and write submitted data back to the respective data sources. You can also call services configured in a Form Data Model using Adaptive Form rules.

To use a Form Data Model for creating an Adaptive Form:

1. In Form Model tab on Add Properties screen, select **[!UICONTROL Form Data Model]** in the **[!UICONTROL Select From]** drop-down list.

   ![Create an Adaptive Form](assets/create-af-1-1.png)

1. Tap to expand **[!UICONTROL Select Form Data Model]**. All available form data models are listed.Select a from data model.

>[!NOTE]
>
>You can also change the Form Data Model for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model).

## Create an Adaptive Form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML and JSON schemas represent the structure in which data is produced or consumed by the back-end system in your organization. You can associate a schema to an Adaptive Form and use its elements to add dynamic content to the Adaptive Form. The elements of the schema are available in the Data Model Object tab of the content browser for authoring Adaptive Forms. You can drag-drop the schema elements to build the form.

See the following documents to understand how to design XML or JSON schema for authoring Adaptive Forms.

* [Creating Adaptive Forms using XML schema](adaptive-form-xml-schema-form-model.md)
* [Creating Adaptive Forms using JSON schema](adaptive-form-json-schema-form-model.md)

Do the following to use XML or JSON schema as form model for an Adaptive Form:

1. On the **[!UICONTROL Add Properties]** step of Adaptive Form creation page, tap on the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, select **[!UICONTROL Schema]** from the **[!UICONTROL Select From]** drop-down field.

1. Tap **[!UICONTROL Select Schema]** and do one of the following:

    * **[!UICONTROL Upload from disk]** - Select this option and tap Upload Schema Definition to browse and upload an XML schema or JSON schema from your file system. The uploaded schema file resides with the form and is not accessible to other Adaptive Forms.
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

## Editar as propriedades do Modelo de formulário de um formulário adaptável {#edit-form-model}

É possível alterar o modelo de formulário para um Formulário adaptável (baseado em JSON ou no Modelo de dados de formulário). Não é possível alterar de um modelo de formulário para outro.

1. Selecione o formulário adaptável e toque no **Propriedades** ícone .
1. Abra o **[!UICONTROL Modelo de formulário]** e faça o seguinte.

   * Se o formulário adaptável não tiver um modelo de formulário, é possível escolher outro modelo de formulário e, consequentemente, selecionar <!-- a form template, --> Esquema XML ou JSON ou modelo de dados de formulário.
   * Se o formulário adaptável for baseado em um modelo de formulário, você poderá escolher outro <!-- form template, --> Esquema XML ou JSON ou Modelo de dados de formulário para o mesmo modelo de formulário.

1. Toque **[!UICONTROL Salvar]** para salvar as propriedades.

Também é possível modificar as propriedades do modelo de formulário no editor de formulário adaptável ou no editor de modelo de formulário adaptável.

1. Selecione o **[!UICONTROL Contêiner de formulário adaptável (raiz)]** componente.
1. Clique em ![Ícone Configurar](/help/forms/assets/configure-icon.svg) ícone para abrir o **[!UICONTROL Propriedades]** do contêiner de Formulário adaptável.
1. Selecione o **[!UICONTROL Modelo de dados]** e faça o seguinte:

   * Se o formulário adaptável não tiver um modelo de formulário, é possível escolher um modelo de formulário e, consequentemente, selecionar <!-- a form template, --> Esquema XML ou JSON ou modelo de dados de formulário.
   * Se o formulário adaptável for baseado em um modelo de formulário, não será possível alterar o modelo de formulário. Você pode escolher outro <!-- form template, --> Esquema XML ou JSON ou Modelo de dados de formulário para o mesmo modelo de formulário aplicável.
1. Toque ![Salvar](/help/forms/assets/check-button.png) para salvar as propriedades.

![FDM-Schema-Support](/help/forms/assets/fdmsupport.png)

>[!NOTE]
>
> Também é possível salvar um Formulário adaptativo como modelo. Para obter mais informações, consulte [Criar um modelo usando um formulário adaptável](/help/forms/template-editor.md#saving-an-adaptive-form-as-template-saving-adaptive-form-as-template).