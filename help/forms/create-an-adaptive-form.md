---
title: Como criar um Formulário adaptável?
description: Saiba como criar Forms adaptável responsivo para dispositivos móveis com nosso tutorial passo a passo. Esses formulários se adaptam perfeitamente em todos os dispositivos, garantindo uma experiência perfeita.
keywords: Forms adaptável, Forms móvel, Forms responsivo, HTML5 Forms
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2780'
ht-degree: 4%

---


# Criar um Formulário adaptável {#creating-an-adaptive-form}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html) |
| AEM as a Cloud Service | Este artigo |

O Forms adaptável permite criar formulários envolventes, responsivos, dinâmicos e adaptáveis. O AEM Forms fornece um assistente prático para que as empresas possam criar rapidamente o Adaptive Forms. O assistente fornece uma navegação rápida por guias para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um Formulário adaptável.

![Assistente para criar um formulário adaptável](/help/release-notes/assets/wizard.png){width="100%" align="center"}

Antes de começar, saiba mais sobre o tipo de componentes do Forms disponíveis para você:

* [Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR): Esses são componentes de captura de dados padronizados. Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital. Um desenvolvedor pode personalizar e estilizar facilmente esses componentes. Você pode visitar [https://aemcomponents.dev/](https://aemcomponents.dev/) para ver os componentes principais disponíveis em ação **A Adobe recomenda o uso desses componentes modernos e extensíveis para desenvolver o Adaptive Forms**.

* [Componentes adaptáveis do Forms Foundation](creating-adaptive-form.md): esses são componentes clássicos (antigos) da captura de dados. Você pode continuar a usá-los para editar seus componentes de base existentes com base no Formulário adaptável. Se você estiver criando novos formulários, o Adobe recomenda usar  [Componentes principais do Forms adaptável para criar um Forms adaptável](#create-an-adaptive-form-core-components).

>[!BEGINTABS]

>[!TAB Criar Forms adaptável com componentes principais (recomendado)]

Você precisa do seguinte para criar um Formulário adaptável:

* **Ativar os Componentes principais adaptáveis do Forms para o seu ambiente**: ao criar um novo programa, os Componentes principais adaptáveis do Forms já estão habilitados para o seu ambiente. Se você tiver um ambiente as a Cloud Service do Forms com base no Archetype 39 ou anterior, [Ativar os Componentes principais adaptáveis do Forms para o seu ambiente](enable-adaptive-forms-core-components.md). Ao habilitar os componentes principais no seu ambiente, o modelo **Formulários adaptáveis (Componente principal)** e o tema da tela são adicionados ao seu ambiente. Se sua versão do SDK do AEM for anterior à 2023.02.0, [certifique-se de que`prerelease` o sinalizador esteja habilitado em seu ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=pt-BR#new-features), pois os componentes principais dos formulários adaptáveis faziam parte do pré-lançamento antes da versão 2023.02.0.

* **Um modelo de formulário adaptável**: um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um Formulário adaptável. Ele tem componentes pré-formatados que contêm determinadas propriedades e estrutura de conteúdo. Também fornece as opções para definir um tema e uma ação de envio. O tema define a aparência e a aparência, e a ação de envio define a ação a ser executada no envio de um Formulário adaptável. Por exemplo, enviar os dados coletados para uma fonte de dados. O serviço de nuvem fornece um modelo OOTB, chamado em branco:

   * A variável `blank` O modelo de está incluído em todos os novos programas do AEM Forms as a Cloud Service.
   * É possível instalar o pacote de referência, por meio do Gerenciador de pacotes, para adicionar o `blank` para o seu programa AEM Forms as a Cloud Service.
   * Também é possível [criar um novo modelo do Forms adaptável (Componentes principais)](template-editor.md) do zero.

* **Um tema de formulário adaptável**: um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica um tema, o estilo especificado é refletido nos componentes correspondentes.  A variável `Canvas` O modelo de está incluído em todos os novos programas do AEM Forms as a Cloud Service.
  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Permissões**: adicionar usuários ao [!DNL forms-users] grupo. Os membros da [!DNL forms-users] grupo tem permissões para criar um Formulário adaptável. Para obter uma lista detalhada de grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).


## Criar um Formulário adaptável {#create-an-adaptive-form-core-components}

1. Faça logon no [!DNL Experience Manager Forms] Instância do autor. Pode ser uma instância da nuvem ou uma instância de desenvolvimento local.

1. Insira suas credenciais na página de logon do Experience Manager. Depois de fazer logon, no canto superior esquerdo, toque em **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.

1. Toque **[!UICONTROL Criar]**  > **[!UICONTROL Forms adaptável]**. O Assistente é aberto. Na guia Origem, selecione um modelo:

   ![Modelo dos Componentes principais](/help/forms/assets/core-components-template.png){width="100%" align="center"}

   Ao selecionar um modelo, um tema e uma ação de envio especificados no modelo são selecionados automaticamente e a variável **[!UICONTROL Criar]** for ativado. Você pode ir para o **[!UICONTROL Estilo]** ou **[!UICONTROL Envio]** para selecionar um tema ou uma ação de envio diferente. Se o modelo selecionado não especificar um tema, o botão criar permanecerá desativado. Você pode ir para o **[!UICONTROL Estilos]** para selecionar um tema manualmente.

   >[!NOTE]
   >
   >
   > Se você não tiver, **Forms adaptável (componente principal)** no seu ambiente, [Ativar os Componentes principais adaptáveis do Forms para o seu ambiente](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). Ao ativar os Componentes principais para seu ambiente, a variável **Forms adaptável (componente principal)** O modelo é adicionado ao seu ambiente.

1. No **[!UICONTROL Estilo]** selecione um tema:

   * Quando o modelo selecionado especifica um tema, ele é selecionado automaticamente no assistente. Você também pode escolher um tema diferente da guia Style.

   * Se o modelo selecionado não especificar um tema, você poderá usar a guia Estilo para escolher um tema. A variável **[!UICONTROL Criar]** O botão só é ativado depois que um tema é selecionado.

1. (Opcional) Na guia Dados, selecione um modelo de dados:

   * **Modelo de dados do formulário**: A [Modelo de dados do formulário](data-integration.md) O permite integrar entidades e serviços de diferentes fontes de dados a um Formulário adaptável. Escolha Modelo de dados de formulário se o formulário adaptável que você está criando envolver a busca e gravação de dados de e para várias fontes de dados.

   * **Esquema JSON**: [Esquema JSON](adaptive-form-json-schema-form-model.md) Nosso formulário adaptável baseado em componentes principais permite uma integração perfeita com o sistema de back-end de sua organização, fornecendo a capacidade de associar um esquema JSON, que representa a estrutura dos dados que estão sendo produzidos ou consumidos. Essa associação permite que os autores adicionem conteúdo dinamicamente ao Formulário adaptável usando os elementos do esquema. Os elementos do esquema são facilmente acessíveis na guia Objetos do modelo de dados do navegador de conteúdo durante o processo de criação e todos os campos são adicionados automaticamente a qualquer formulário adaptável recém-criado.

   Por padrão, todos os campos do esquema JSON associado são selecionados e convertidos automaticamente em componentes de Formulário adaptável correspondentes, simplificando o processo de criação. O assistente oferece a conveniência adicional de permitir que você escolha seletivamente quais campos devem ser incluídos no Formulário adaptável usando caixas de seleção.

1. No **[!UICONTROL Envio]** selecione uma ação de envio:

   * Ao selecionar um modelo, a ação de envio especificada no modelo é selecionada automaticamente. Você pode selecionar uma ação de envio diferente na guia Envio. A variável **[!UICONTROL Envio]** exibe todas as ações de envio disponíveis.

   * Quando o modelo selecionado não especificar uma ação de envio, você poderá usar o **[!UICONTROL Envio]** para selecionar uma ação de envio

1. (Opcional) Na **[!UICONTROL Entrega]** , é possível especificar uma data de publicação ou cancelamento da publicação para um Formulário adaptável.

1. Toque **[!UICONTROL Criar]**. Uma caixa de diálogo para especificar o título, o nome e o local para salvar o Formulário adaptável é exibida:

   * **[!UICONTROL Título]** Especifica o nome de exibição do formulário. O título ajuda a identificar o formulário na variável [!DNL Experience Manager Forms] interface do usuário.
   * **[!UICONTROL Nome:]** Especifica o nome do formulário. Um nó com o nome especificado é criado no repositório. Quando você começa a digitar um título, o valor do campo de nome é gerado automaticamente. Você pode alterar o valor sugerido. O campo de nome pode incluir apenas caracteres alfanuméricos, hifens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.
   * **[!UICONTROL Caminho:]** Especifica o local no qual o Formulário adaptável deve ser salvo. É possível salvar o formulário adaptável diretamente em `/content/dam/formsanddocuments` ou criar uma pasta como `/content/dam/formsanddocuments/adaptiveforms` para salvar um Formulário adaptável. Certifique-se de criar a pasta antes de usá-la no caminho. A variável **[!UICONTROL Caminho]** não cria uma pasta automaticamente.

1. Toque **[!UICONTROL Criar]**. Um Formulário adaptável é criado e aberto no editor do Forms adaptável. O editor exibe o conteúdo disponível no modelo.  Com base no tipo de Formulário adaptável, os elementos de formulário presentes no <!--XFA form template, XML schema or --> O esquema JSON ou o modelo de dados de formulário são exibidos no **[!UICONTROL Objetos do modelo de dados]** guia do **[!UICONTROL Navegador de conteúdo]** na barra lateral.

Agora, você pode arrastar e soltar a variável [Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#components) ou elementos de esquema para criar o Formulário adaptável.


## Editar propriedades do modelo de formulário de um formulário adaptável {#edit-form-model-core-components-based-adaptive-forms}

1. Selecione o Formulário adaptável e toque em ![Informações da página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Abrir propriedades]**. A página Propriedades do formulário é aberta.

1. Vá para a **[!UICONTROL Modelo de formulário]** e escolha um modelo de formulário. Se o Formulário adaptável não tiver um modelo de formulário, você terá a liberdade de escolher um esquema JSON ou um modelo de dados de formulário. Por outro lado, se o formulário adaptável já estiver baseado em um modelo de formulário, você terá a opção de alternar para outro modelo de formulário do mesmo tipo. Por exemplo, se o formulário estiver usando um esquema JSON, você poderá alternar facilmente para outro esquema JSON e, de forma semelhante, se o formulário estiver usando um Modelo de dados de formulário, você poderá alternar para outro Modelo de dados de formulário.

1. Toque **[!UICONTROL Salvar]** para salvar as propriedades.

>[!TAB Criar Forms adaptável com componentes de base]

Você precisa do seguinte para criar um Formulário adaptável:

* **Permissões**: adicionar usuários ao [!DNL forms-users] para fornecer a eles permissões para criar um Formulário adaptável. Para obter uma lista detalhada de grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

* **Um tema de formulário adaptável**: um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica um tema, o estilo especificado é refletido nos componentes correspondentes. Você pode [criar um novo tema](themes.md) ou [importar um tema existente](import-export-forms-templates.md#uploading-a-theme). Você também pode implantar o [arquétipo mais recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html#create-project) para alguns temas de amostra.

* **Um modelo de formulário adaptável**: um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um Formulário adaptável. Ele tem componentes pré-formatados que contêm determinadas propriedades e estrutura de conteúdo. Também fornece as opções para definir um tema e uma ação de envio. O tema define a aparência e a aparência, e a ação de envio define a ação a ser executada no envio de um Formulário adaptável. Por exemplo, enviar os dados coletados para uma fonte de dados. O Cloud Service oferece suporte a dois tipos de modelos:

   * **Modelo editável**: é possível [criar um novo](template-editor.md) ou [importar um modelo editável existente](migrate-to-forms-as-a-cloud-service.md). Você também pode implantar o [arquétipo mais recente](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#:~:text=The%20AEM%20Archetype%20is%20made%20up%20of%20modules%3A,and%20request%20filters.%20it.tests%3A%20are%20integration%20based%20Java.) para obter alguns modelos editáveis de amostra.

   * **Modelo estático**: esses são modelos herdados e são recomendados apenas para clientes que estão migrando do Adobe Managed Services (AMS) e de instalações locais do AEM Forms AEM (6.5 Forms ou anterior). Eles permitem que você continue a usar seu investimento existente em modelos estáticos. Ao criar um novo Formulário adaptável, é recomendável usar um Modelo editável.


## Criar um Formulário adaptável {#create-an-adaptive-form-foundation-components}

1. Access [!DNL Experience Manager Forms] Instância do autor. Pode ser uma instância da nuvem ou uma instância de desenvolvimento local.

1. Insira suas credenciais na página de logon do Experience Manager.

   Depois de fazer logon, no canto superior esquerdo, toque em **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.

1. Toque **[!UICONTROL Criar]**  > **[!UICONTROL Forms adaptável]**. O Assistente é aberto.
1. Na guia Origem, selecione um modelo:

   * Ao selecionar um modelo Editável, um tema e uma ação de envio especificados no modelo são selecionados automaticamente e a variável **[!UICONTROL Criar]** for ativado. Você pode ir para o **[!UICONTROL Estilo]** ou **[!UICONTROL Envio]** para selecionar um tema ou uma ação de envio diferente. Se o modelo Editável selecionado não especificar um tema, o botão Criar permanecerá desativado. Você pode ir para o **[!UICONTROL Estilos]** para selecionar um tema manualmente.

     >[!NOTE]
     >
     > Você também pode criar [!UICONTROL Documento do registro] usando um editor Forms adaptável. Para obter mais informações, consulte [Suporte a documento de registro no editor de formulário adaptável](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

   * Ao selecionar um modelo estático, as opções de dados, estilo, envio, entrega e visualização não estão disponíveis. Ao criar um novo Formulário adaptável, é recomendável usar um Modelo editável.

1. No **[!UICONTROL Estilo]** selecione um tema:

   * Quando o modelo selecionado especifica um tema, ele é selecionado automaticamente no assistente. Você também pode escolher um tema diferente da guia Style.
   * Se o modelo selecionado não especificar um tema, você poderá usar a guia Estilo para escolher um tema. A variável **[!UICONTROL Criar]** O botão só é ativado depois que um tema é selecionado.

1. (Opcional) Na **[!UICONTROL Dados]** selecione um modelo de dados:

   * **Modelo de dados do formulário**: A [Modelo de dados do formulário](data-integration.md) O permite integrar entidades e serviços de diferentes fontes de dados a um Formulário adaptável. Escolha Modelo de dados de formulário se o formulário adaptável que você está criando envolver a busca e gravação de dados de e para várias fontes de dados.

   * **Esquema JSON**: [Esquema JSON](adaptive-form-json-schema-form-model.md) representa a estrutura em que os dados são produzidos ou consumidos pelo sistema de back-end em sua organização. Você pode associar o esquema a um formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao formulário adaptável. Os elementos do esquema estão disponíveis para uso na guia Objetos do modelo de dados do navegador de conteúdo ao criar o Adaptive Forms, e todos os campos também são adicionados ao Formulário adaptável recém-criado.

   Por padrão, todos os campos do modelo de dados são selecionados. Ao criar o Formulário adaptável, todos os campos de modelo de dados selecionados são convertidos em componentes de Formulário adaptável correspondentes. O assistente fornece caixas de seleção para selecionar apenas os campos que devem ser incluídos no Formulário adaptável.

   <!-- 
   
   If your JSON schema contains a fragment, the fragment is considered a single unit. You can select or deselect a complete fragment and all the fields of the fragment are selected or deselected accordingly. 
   
   -->

1. No **[!UICONTROL Envio]** selecione uma ação de envio:

   * Ao selecionar um modelo, a ação de envio especificada no modelo é selecionada automaticamente. Você pode selecionar uma ação de envio diferente na guia Envio. A variável **[!UICONTROL Envio]** exibe todas as ações de envio disponíveis.

   * Quando o modelo selecionado não especificar uma ação de envio, você poderá usar o **[!UICONTROL Envio]** para selecionar uma ação de envio

1. (Opcional) Na guia Delivery, é possível especificar uma data de publicação ou cancelamento de publicação para um Formulário adaptável.

1. Toque **[!UICONTROL Criar]**. Uma caixa de diálogo para especificar o título, o nome e o local para salvar o Formulário adaptável é exibida:

   * **[!UICONTROL Título]** Especifica o nome de exibição do formulário. O título ajuda a identificar o formulário na variável [!DNL Experience Manager Forms] interface do usuário.
   * **[!UICONTROL Nome:]** Especifica o nome do formulário. Um nó com o nome especificado é criado no repositório. Quando você começa a digitar um título, o valor do campo de nome é gerado automaticamente. Você pode alterar o valor sugerido. O campo de nome pode incluir apenas caracteres alfanuméricos, hifens e sublinhados. Todas as entradas inválidas são substituídas por um hífen.
   * **[!UICONTROL Caminho:]** Especifica o local no qual o Formulário adaptável deve ser salvo. É possível salvar o formulário adaptável diretamente em `/content/dam/formsanddocuments` ou criar uma pasta como `/content/dam/formsanddocuments/adaptiveforms` para salvar um Formulário adaptável. Certifique-se de criar a pasta antes de usá-la no caminho. A variável **[!UICONTROL Caminho:]** não cria uma pasta automaticamente.

1. Toque **[!UICONTROL Criar]**. Um Formulário adaptável é criado e aberto no editor do Forms adaptável. O editor exibe o conteúdo disponível no modelo. Ele também exibe a barra lateral para personalizar o formulário recém-criado de acordo com as necessidades.

   Com base no tipo de Formulário adaptável, os elementos de formulário presentes no <!--XFA form template, XML schema or --> O esquema JSON ou o modelo de dados de formulário são exibidos no **[!UICONTROL Objetos do modelo de dados]** guia do **[!UICONTROL Navegador de conteúdo]** na barra lateral. Você também pode arrastar e soltar esses elementos para criar o Formulário adaptável.

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
>You can also change the schema for an Adaptive Form. For detailed steps, see [Edit Form Model properties of an Adaptive Form](#edit-form-model2). -->

## Editar propriedades do modelo de formulário de um formulário adaptável {#edit-form-model-foundation-components}

Você pode alterar o modelo de formulário para um Formulário adaptável (com base em JSON ou Modelo de dados de formulário). Não é possível alterar de um modelo de formulário para outro.

1. Selecione o Formulário adaptável e toque no **Propriedades** ícone.
1. Abra o **[!UICONTROL Modelo de formulário]** e siga um destes procedimentos.

   * Se o formulário adaptável não tiver um modelo de formulário, você poderá escolher outro modelo de formulário e selecionar <!-- a form template, --> Esquema XML, JSON ou modelo de dados de formulário.
   * Se o formulário adaptável for baseado em um modelo de formulário, você poderá escolher outro <!-- form template, --> Esquema XML, JSON ou Modelo de dados de formulário para o mesmo modelo de formulário.

1. Toque **[!UICONTROL Salvar]** para salvar as propriedades.

Também é possível modificar as propriedades do modelo de formulário pelo editor de formulário adaptável ou pelo editor de modelo de formulário adaptável.

1. Selecione o **[!UICONTROL Contêiner de formulário adaptável (raiz)]** componente.
1. Clique em ![Ícone Configurar](/help/forms/assets/configure-icon.svg) ícone para abrir o **[!UICONTROL Propriedades]** do contêiner do Formulário adaptável.
1. Selecione o **[!UICONTROL Modelo de dados]** e siga um destes procedimentos:

   * Se o formulário adaptável não tiver um modelo de formulário, você poderá escolher um modelo de formulário e selecionar <!-- a form template, --> Esquema XML, JSON ou modelo de dados de formulário.
   * Se o formulário adaptável for baseado em um modelo de formulário, não será possível alterar o modelo de formulário. Você pode escolher outro <!-- form template, --> Esquema XML, JSON ou Modelo de dados de formulário para o mesmo modelo de formulário conforme aplicável.
1. Toque ![Salvar](/help/forms/assets/check-button.png) para salvar as propriedades.

![FDM-Schema-Support](/help/forms/assets/fdmsupport.png){width="100%" align="center"}

>[!NOTE]
>
> Você também pode salvar um Formulário adaptável como um modelo. Para obter mais informações, consulte [Criar um modelo usando um Formulário adaptável](/help/forms/template-editor.md#saving-an-adaptive-form-as-template-saving-adaptive-form-as-template).

>[!ENDTABS]


## Próximas etapas

* [Usar o Adobe Sign com o Forms](working-with-adobe-sign.md)
* [Usar o Google reCaptcha no com o Forms](captcha-adaptive-forms.md)
* [Adicionar seção repetível a um formulário](create-forms-repeatable-sections.md)
* [Preencher previamente os campos de um formulário](prepopulate-adaptive-form-fields.md)

>[!MORELIKETHIS]
>
>* [Criar um formulário adaptável na página do AEM Sites ou Fragmento de experiência](create-or-add-an-adaptive-form-to-aem-sites-page.md)
>* [Criar um tema Forms adaptável personalizado](using-themes-in-core-components.md)
>* [Configurar ações de envio para um formulário](configuring-submit-actions.md)
>* [Componentes principais do Forms adaptável disponíveis](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#components)
