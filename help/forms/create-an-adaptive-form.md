---
title: Como criar um formulário adaptável?
description: Saiba como usar o construtor de formulários do AEM Forms para criar formulários adaptáveis responsivos para dispositivos móveis. Perfeito para criadores e desenvolvedores de formulários que precisam de formulários que se adaptam perfeitamente em todos os dispositivos.
keywords: form builder, criador de formulário, criar formulários, criador de formulário, formulários adaptáveis, formulários responsivos, formulários HTML5, criar formulários, formulários AEM
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
exl-id: 6f1c3fe7-b61e-47ce-b565-15b4904db092
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '2703'
ht-degree: 72%

---

# Guia de introdução ao Construtor de formulários {#creating-an-adaptive-form}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

O construtor de formulários do AEM Forms permite criar formulários envolventes, responsivos, dinâmicos e adaptáveis. Quer você seja um criador de formulários que cria formulários profissionais ou precise criar formulários responsivos rapidamente, o AEM Forms fornece um assistente amigável. O assistente fornece uma navegação rápida por guias para selecionar facilmente modelos pré-configurados, estilos, campos e opções de envio.

![Assistente para criar um formulário adaptável](/help/release-notes/assets/wizard.png){width="100%" align="center"}

Antes de começar, saiba mais sobre o tipo de componentes do Forms disponíveis para você:

* [Componentes principais de formulários adaptáveis](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR): Esses são componentes de captura de dados padronizados. Esses componentes oferecem recursos de personalização, redução do tempo de desenvolvimento e dos custos de manutenção para suas experiências de inscrição digital. Um desenvolvedor pode personalizar e estilizar facilmente esses componentes. Você pode visitar [https://aemcomponents.dev/](https://aemcomponents.dev/) para ver os componentes principais disponíveis em ação **A Adobe recomenda o uso desses componentes modernos e extensíveis para desenvolver formulários adaptáveis**.

* [Componentes de fundamentais de formulários adaptáveis](creating-adaptive-form.md): esses são componentes clássicos (antigos) de captura de dados. Você pode continuar usando-os para editar seus componentes fundamentais já existentes com base no formulário adaptável. Se estiver criando novos formulários, o Adobe recomenda usar os [Componentes principais para criar formulários adaptáveis](#create-an-adaptive-form-core-components).

>[!BEGINTABS]

>[!TAB Criação de formulários adaptáveis com componentes principais (recomendado)]

Você precisará do seguinte para criar um formulário adaptável:

* **Habilitar os Componentes principais adaptáveis do Forms para o seu ambiente**: quando você cria um programa, os Componentes principais adaptáveis do Forms já estão habilitados para o seu ambiente. Instale os componentes principais adaptáveis do Forms mais recentes até o momento para ativar o ambiente do AEM Cloud Service. Ao habilitar os componentes principais no seu ambiente, o modelo **Formulários adaptáveis (Componente principal)** e o tema da tela são adicionados ao seu ambiente. Se sua versão do SDK do AEM for anterior à 2023.02.0, [certifique-se de que`prerelease` o sinalizador esteja habilitado em seu ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=pt-BR#new-features), pois os componentes principais dos formulários adaptáveis faziam parte do pré-lançamento antes da versão 2023.02.0.

* **Um modelo de formulário adaptável**: um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um formulário adaptável. Ele tem componentes pré-formatados que contêm determinadas propriedades e estrutura de conteúdo. Também fornece as opções para definir um tema e uma ação de envio. O tema define a aparência, e a ação de envio define a ação a ser executada no envio de um formulário adaptável. Por exemplo, enviar os dados coletados para uma fonte de dados. O serviço de nuvem fornece um modelo OOTB, chamado de em branco:

   * O modelo `blank` está incluído em todos os novos programas do AEM Forms as a Cloud Service.
   * É possível instalar o pacote de referência, por meio do Gerenciador de pacotes, para adicionar o modelo `blank` para o seu programa do AEM Forms as a Cloud Service.
   * Você também pode [criar um modelo Adaptive Forms (Componentes principais)](template-editor.md) do zero.

* **Um tema de formulários adaptáveis**: um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Ao aplicar um tema, o estilo especificado é refletido nos componentes correspondentes.  O modelo `Canvas` está incluído em todos os novos programas do AEM Forms as a Cloud Service.
  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create an Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Permissões**: adicionar usuários ao grupo [!DNL forms-users]. Os membros do grupo [!DNL forms-users] tem permissões para criar formulários adaptáveis. Para obter uma lista detalhada de grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).


## Criar um formulário adaptável {#create-an-adaptive-form-core-components}

1. Faça logon na Instância de criação do [!DNL Experience Manager Forms]. Pode ser uma instância da nuvem ou uma instância de desenvolvimento local.

1. Insira suas credenciais na página de logon do Experience Manager. Depois de fazer logon, no canto superior esquerdo, selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O Assistente será aberto. Na guia Origem, selecione um modelo:

   ![Modelo dos componentes principais](/help/forms/assets/core-components-template.png){width="100%" align="center"}

   Ao selecionar um modelo, o tema e a ação de envio especificados no modelo são selecionados automaticamente e o botão **[!UICONTROL Criar]** será habilitado. Você pode ir para as guias **[!UICONTROL Estilo]** ou **[!UICONTROL Envio]** para selecionar um tema ou uma ação de envio diferente. Se o modelo selecionado não especificar um tema, o botão criar permanecerá desabilitado. É possível ir para a guia **[!UICONTROL Estilos]** para selecionar um tema manualmente.

   >[!NOTE]
   >
   >
   > Se você não tiver o modelo **Formulários adaptáveis (componente principal)** em seu ambiente, [Habilite os Componentes principais dos formulários adaptáveis para o seu ambiente](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). Ao habilitar os componentes principais no seu ambiente, o modelo **Formulários adaptáveis (Componente principal)** será adicionado ao seu ambiente.

1. Na guia **[!UICONTROL Estilo]**, selecione um tema:

   * Quando o modelo selecionado especifica um tema, ele é selecionado automaticamente no assistente. Você também pode escolher um tema diferente da guia de Estilo.

   * Se o modelo selecionado não especificar um tema, será possível usar a guia de Estilo para escolher um tema. O botão **[!UICONTROL Criar]** só será habilitado depois que um tema for selecionado.

1. (Opcional) Na guia Dados, selecione um modelo de dados:

   * **Modelo de dados de formulário**: o [Modelo de Dados de Formulário(FDM)](data-integration.md) permite integrar entidades e serviços de fontes de dados diferentes em um Formulário adaptável. Escolha Modelo de dados de formulário (FDM) se o Formulário adaptável que você está criando envolver a busca e a gravação de dados de e para várias fontes de dados.

   * **Esquema JSON**: [Esquema JSON](adaptive-form-json-schema-form-model.md) nosso formulário adaptável baseado em componentes principais permite a integração perfeita com o sistema back-end da sua organização, fornecendo a capacidade de associar um esquema JSON, que representa a estrutura dos dados que estão sendo produzidos ou consumidos. Essa associação permite que os autores adicionem conteúdo dinamicamente ao Formulário adaptável usando os elementos do esquema. Os elementos do esquema são facilmente acessíveis na guia Objetos do modelo de dados do navegador de conteúdo durante o processo de criação e todos os campos são adicionados automaticamente a qualquer formulário adaptável criado.

   Por padrão, todos os campos do esquema JSON associado são selecionados e convertidos automaticamente nos componentes de Formulários adaptáveis correspondentes, simplificando o processo de criação. O assistente oferece a conveniência adicional de permitir a escolha seletiva de quais campos devem ser incluídos no Formulário adaptável usando caixas de seleção.

1. Na guia **[!UICONTROL Envio]**, selecione uma ação de envio:

   * Ao selecionar um modelo, a ação de envio especificada no modelo é selecionada automaticamente. É possível selecionar uma ação de envio diferente na guia Envio. A guia **[!UICONTROL Envio]** exibe todas as ações de envio disponíveis.

   * Quando o modelo selecionado não especificar uma ação de envio, você poderá usar a guia **[!UICONTROL Envio]** para selecionar uma

1. (Opcional) Na guia **[!UICONTROL Entrega]**, é possível especificar uma data de publicação ou cancelamento da publicação para um Formulário adaptável.

1. Selecione **[!UICONTROL Criar]**. Uma caixa de diálogo para especificar o título, o nome e o local para salvar o Formulário adaptável será exibida:

   * **[!UICONTROL Título]** especifica o nome de exibição do formulário. O título ajuda a identificar o formulário na interface do usuário do [!DNL Experience Manager Forms].
   * **[!UICONTROL Nome:]** especifica o nome do formulário. Um nó com o nome especificado será criado no repositório. Ao começar a digitar um título, o valor do campo de nome é gerado automaticamente. É possível alterar o valor sugerido. O campo de nome pode incluir apenas caracteres alfanuméricos, hifens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.
   * **[!UICONTROL Caminho:]** especifica o local no qual o Formulário adaptável deverá ser salvo. É possível salvar o formulário adaptável diretamente em `/content/dam/formsanddocuments` ou criar uma pasta como `/content/dam/formsanddocuments/adaptiveforms` para salvar um Formulário adaptável. Certifique-se de criar a pasta antes de usá-la no caminho. O campo **[!UICONTROL Caminho]** não cria uma pasta automaticamente.

1. Selecione **[!UICONTROL Criar]**. Um Formulário adaptável será criado e aberto no editor de Formulários adaptáveis. O editor exibirá o conteúdo disponível no modelo.  Com base no tipo de Formulário adaptável, os elementos de formulário presentes no esquema JSON do <!--XFA form template, XML schema or --> associado ou no Modelo de Dados de Formulário (FDM) são exibidos na guia **[!UICONTROL Objetos do Modelo de Dados]** do **[!UICONTROL Navegador de Conteúdo]** na barra lateral.

Agora, é possível arrastar e soltar os [Componentes principais dos formulários adaptáveis](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR#components) ou elementos de esquema para criar o Formulário adaptável.


## Editar propriedades do modelo de formulário de um formulário adaptável {#edit-form-model-core-components-based-adaptive-forms}

1. Selecione o Formulário adaptável e selecione ![Informações da página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Abrir propriedades]**. A página Propriedades do formulário será aberta.

1. Vá para a guia **[!UICONTROL Modelo de formulário]** e escolha um modelo de formulário. Se o Formulário adaptável não tiver um modelo de formulário, você terá a liberdade de escolher um esquema JSON ou um modelo de dados de formulário (FDM). Por outro lado, se o formulário adaptável já estiver baseado em um modelo de formulário, você terá a opção de alternar para outro modelo de formulário do mesmo tipo. Por exemplo, se o formulário estiver usando um esquema JSON, você poderá alternar facilmente para outro esquema JSON e, de forma semelhante, se o formulário estiver usando um Modelo de dados de formulário (FDM), será possível alternar para outro Modelo de dados de formulário (FDM).

1. Selecione **[!UICONTROL Salvar]** para salvar as propriedades.

>[!TAB Criação de Formulários adaptáveis com componentes fundamentais]

Você precisará do seguinte para criar um formulário adaptável:

* **Permissões**: adicione seus usuários ao [!DNL forms-users] para fornecer-lhes permissões para criar Formulários adaptáveis. Para obter uma lista detalhada de grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

* **Um tema de formulário adaptável**: um tema contém os detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Ao aplicar um tema, o estilo especificado é refletido nos componentes correspondentes. Você pode [criar um tema](themes.md) ou [importar um tema existente](import-export-forms-templates.md#uploading-a-theme). Também é possível pode implantar o [arquétipo mais recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=pt-BR#create-project) para alguns temas de amostra.

* **Um modelo de formulário adaptável**: um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um Formulário adaptável. Ele tem componentes pré-formatados que contêm determinadas propriedades e estrutura de conteúdo. Também fornece as opções para definir um tema e uma ação de envio. O tema define a aparência, e a ação de envio define a ação a ser executada no envio de um formulário adaptável. Por exemplo, enviar os dados coletados para uma fonte de dados. Os serviços na nuvem oferecem suporte a dois tipos de modelos:

   * **Modelo editável**: você pode [criar um](template-editor.md) ou [importar um modelo editável existente](migrate-to-forms-as-a-cloud-service.md). Você também pode implantar o [arquétipo mais recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=pt-BR#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20are%20Java-based%20integration%20tests.) para obter alguns modelos editáveis de amostra.

   * **Modelo estático**: esses são modelos herdados e são recomendados apenas para clientes que estão migrando do Adobe Managed Services (AMS) e de instalações locais do AEM Forms (AEM Forms 6.5 ou anterior). Eles permitem continuar usando seu investimento já existente em modelos estáticos. Ao criar um Formulário adaptável, use um Modelo editável.


## Criar um formulário adaptável {#create-an-adaptive-form-foundation-components}

1. Acessar a Instância de criação do [!DNL Experience Manager Forms]. Pode ser uma instância da nuvem ou uma instância de desenvolvimento local.

1. Insira suas credenciais na página de logon do Experience Manager.

   Depois de fazer logon, no canto superior esquerdo, selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O Assistente será aberto.
1. Na guia Origem, selecione um modelo:

   * Ao selecionar um modelo Editável, um tema e uma ação de envio especificados no modelo são selecionados automaticamente e o botão **[!UICONTROL Criar]** será habilitado. Você pode ir para as guias **[!UICONTROL Estilo]** ou **[!UICONTROL Envio]** para selecionar um tema ou uma ação de envio diferente. Se o modelo Editável selecionado não especificar um tema, o botão Criar permanecerá desabilitado. É possível ir para a guia **[!UICONTROL Estilos]** para selecionar um tema manualmente.

     >[!NOTE]
     >
     > Você também pode criar um modelo de [!UICONTROL Documento do registro] usando o editor de Formulários adaptáveis. Para obter mais informações, consulte [Suporte a documento de registro no editor de formulário adaptável](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

   * Ao selecionar um modelo estático, as opções de dados, estilo, envio, entrega e visualização não estarão disponíveis. Ao criar um Formulário adaptável, é recomendável usar um Modelo editável.

1. Na guia **[!UICONTROL Estilo]**, selecione um tema:

   * Quando o modelo selecionado especifica um tema, ele é selecionado automaticamente no assistente. Você também pode escolher um tema diferente da guia de Estilo.
   * Se o modelo selecionado não especificar um tema, será possível usar a guia de Estilo para escolher um tema. O botão **[!UICONTROL Criar]** só será habilitado depois que um tema for selecionado.

1. (Opcional) Na guia **[!UICONTROL Dados]**, selecione um modelo de dados:

   * **Modelo de dados de formulário**: o [Modelo de Dados de Formulário (FDM)](data-integration.md) permite integrar entidades e serviços de diferentes fontes de dados a um Formulário adaptável. Escolha Modelo de dados de formulário (FDM) se o Formulário adaptável que você está criando envolver a busca e a gravação de dados de e para várias fontes de dados.

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

## Create an adaptive form based on XML or JSON schema {#create-an-adaptive-form-based-on-xml-or-json-schema}

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
>You can also change the schema for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model2). -->

## Editar propriedades do modelo de formulário de um formulário adaptável {#edit-form-model-foundation-components}

É possível alterar o modelo de formulário para um Formulário adaptável (baseado em JSON ou Modelo de dados de formulário (FDM)). Não é possível alterar de um modelo de formulário para outro.

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

![FDM-Schema-Support](/help/forms/assets/fdmsupport.png){width="100%" align="center"}

>[!NOTE]
>
> Você também pode salvar um formulário adaptável como modelo. Para obter mais informações, consulte [Criação de um modelo usando um formulário adaptável](/help/forms/template-editor.md#saving-an-adaptive-form-as-template-saving-adaptive-form-as-template).

>[!ENDTABS]


## Próximas etapas

* [Use o Adobe Sign com o Forms](working-with-adobe-sign.md)
* [Use o Google reCaptcha com o Forms](captcha-adaptive-forms.md)
* [Adicione uma seção repetível a um formulário](create-forms-repeatable-sections.md)
* [Preencha previamente os campos de um formulário](prepopulate-adaptive-form-fields.md)

>[!MORELIKETHIS]
>
>* [Criar um Formulário Adaptável](/help/forms/creating-adaptive-form-core-components.md)
