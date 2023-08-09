---
title: Como criar um Formulário adaptável
description: Saiba como criar um Formulário adaptável usando o [!DNL Experience Manager Forms]. Os Forms adaptáveis são formulários de HTML5 responsivos que simplificam a coleta e o processamento de informações. Saiba mais sobre como criar um Formulário adaptável com base em um Modelo de dados de formulário e um esquema XML ou JSON.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 6d9ebc5410f6ffce0f0c7c7f4e9302b30e82b70b
workflow-type: tm+mt
source-wordcount: '2342'
ht-degree: 6%

---

# Criar um Formulário adaptável {#creating-an-adaptive-form-core-components}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-an-adaptive-form-core-components.html) |
| AEM as a Cloud Service | Este artigo |


O Forms adaptável permite criar formulários envolventes, responsivos, dinâmicos e adaptáveis. O AEM Forms fornece um assistente prático para que as empresas possam criar rapidamente o Adaptive Forms. O assistente fornece uma navegação rápida por guias para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um Formulário adaptável.

Antes de começar, saiba mais sobre o tipo de componentes do Forms disponíveis para você:

* [Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR): Esses são componentes de captura de dados padronizados. Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital. Um desenvolvedor pode personalizar e estilizar facilmente esses componentes. A Adobe recomenda aproveitar esses componentes modernos e extensíveis para desenvolver o Adaptive Forms.

* [Componentes adaptáveis do Forms Foundation](creating-adaptive-form.md): esses são componentes clássicos (antigos) da captura de dados. Você pode continuar a usá-los para editar seus componentes de base existentes com base no Formulário adaptável. Se você estiver criando novos formulários, o Adobe recomenda usar  [Componentes principais adaptáveis do Forms](creating-adaptive-form-core-components.md) para criar uma Forms adaptável.

![Assistente para criar um formulário adaptável](/help/release-notes/assets/wizard.png)


## Pré-requisitos

Você precisa do seguinte para criar um Formulário adaptável:

* **Ativar os Componentes principais adaptáveis do Forms para o seu ambiente**: ao criar um novo programa, os Componentes principais adaptáveis do Forms já estão habilitados para o seu ambiente. Se você tiver um ambiente do Forms as a Cloud Service baseado no arquétipo 39 ou anterior, [habilite os componentes principais dos formulários adaptáveis no seu ambiente](enable-adaptive-forms-core-components.md). Ao habilitar os componentes principais no seu ambiente, o modelo **Formulários adaptáveis (Componente principal)** e o tema da tela são adicionados ao seu ambiente. Se sua versão do SDK do AEM for anterior à 2023.02.0, [certifique-se de que`prerelease` o sinalizador esteja habilitado em seu ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=pt-BR#new-features), pois os componentes principais dos formulários adaptáveis faziam parte do pré-lançamento antes da versão 2023.02.0.

* **Um modelo de formulário adaptável**: um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um Formulário adaptável. Ele tem componentes pré-formatados que contêm determinadas propriedades e estrutura de conteúdo. Também fornece as opções para definir um tema e uma ação de envio. O tema define a aparência e a aparência, e a ação de envio define a ação a ser executada no envio de um Formulário adaptável. Por exemplo, enviar os dados coletados para uma fonte de dados. O serviço de nuvem fornece um modelo OOTB, chamado em branco:

   * A variável `blank` O modelo de está incluído em todos os novos programas do AEM Forms as a Cloud Service.
   * É possível instalar o pacote de referência, por meio do Gerenciador de pacotes, para adicionar o `blank` para o seu programa AEM Forms as a Cloud Service.
   * Também é possível [criar um novo modelo do Forms adaptável (Componentes principais)](template-editor.md) do zero.
   * Também é possível implantar [modelos de amostra](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) ao seu ambiente. Isso o ajuda a começar a criar formulários rapidamente.

* **Um tema de formulário adaptável**: um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica um tema, o estilo especificado é refletido nos componentes correspondentes.  A variável `Canvas` O modelo de está incluído em todos os novos programas do AEM Forms as a Cloud Service. Também é possível implantar [temas de amostra](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) ao seu ambiente. Isso o ajuda a começar a estilizar seus formulários e a fornecer uma estrutura básica para criar ou personalizar um tema de acordo com os requisitos da empresa.

  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Permissões**: adicionar usuários ao [!DNL forms-users] grupo. Os membros da [!DNL forms-users] grupo tem permissões para criar um Formulário adaptável. Para obter uma lista detalhada de grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## Criar um Formulário adaptável  {#create-an-adaptive-form-core-components}

1. Faça logon no [!DNL Experience Manager Forms] Instância do autor. Pode ser uma instância da nuvem ou uma instância de desenvolvimento local.

1. Insira suas credenciais na página de logon do Experience Manager. Depois de fazer logon, no canto superior esquerdo, toque em **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.

1. Toque **[!UICONTROL Criar]**  > **[!UICONTROL Forms adaptável]**. O Assistente é aberto. Na guia Origem, selecione um modelo:

   ![Modelo dos Componentes principais](/help/forms/assets/core-components-template.png)

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

1. Toque **[!UICONTROL Criar]**. Um Formulário adaptável é criado e aberto no editor do Forms adaptável. O editor exibe o conteúdo disponível no modelo.  Com base no tipo de Formulário adaptável, os elementos de formulário presentes no <!--XFA form template, XML schema or --> O esquema JSON ou o modelo de dados de formulário são exibidos no **[!UICONTROL Objetos do modelo de dados]** guia do **[!UICONTROL Navegador de conteúdo]** na barra lateral. Você também pode arrastar e soltar esses elementos para criar o Formulário adaptável.

Agora, você pode arrastar e soltar a variável [Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-br) para o contêiner Adaptive Forms para projetar e criar o formulário. Você também pode visitar [https://aemcomponents.dev/](https://aemcomponents.dev/) para ver os componentes principais disponíveis em ação.

## Configurar a ação enviar para um formulário adaptável {#configure-submit-action-for-form}

Uma ação enviar permite escolher o destino dos dados capturados por meio de um formulário adaptável. É acionado quando um usuário clica no botão Enviar em um Formulário adaptável. Os formulários adaptáveis incluem algumas ações de envio prontas para uso. Você também pode estender ações de envio padrão para criar sua própria ação de envio personalizada. Para configurar uma Ação de envio para o formulário:

1. Abra o Navegador de conteúdo e selecione a variável **[!UICONTROL Contêiner do guia]** componente do seu Formulário adaptável.
1. Clique nas propriedades do Container do guia ![Propriedades do guia](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável é aberta.

1. Clique em  **[!UICONTROL Envio]** guia.

   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável para configurar uma ação de envio](/help/forms/assets/adaptive-forms-submit-message.png)

1. Selecionar e configurar um **[!UICONTROL Enviar ação]**, com base nas suas necessidades. Para obter informações detalhadas sobre Ações de Envio, consulte [Ação de envio do formulário adaptável](/help/forms/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Redirecionar o usuário para uma página ou mostrar uma mensagem de agradecimento no envio do formulário

No envio de um formulário, você pode redirecionar o usuário para outra página da Web ou uma mensagem. Para redirecionar o usuário ou configurar a mensagem de agradecimento:

1. Abra o Navegador de conteúdo e selecione a variável **[!UICONTROL Contêiner do guia]** componente do seu Formulário adaptável.
1. Clique nas propriedades do Container do guia ![Propriedades do guia](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Abra o **[!UICONTROL Envio]** guia.

   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner do formulário adaptável para configurar uma página de redirecionamento ou mensagem de agradecimento](/help/forms/assets/adaptive-forms-redirect-message.png)

   * Para configurar um URL de redirecionamento, para na opção Enviar, selecione o **[!UICONTROL Redirecionar para URL]** e procure e selecione uma página do AEM Sites ou forneça o URL de uma página externa.

   * Para configurar uma mensagem personalizada ou de agradecimento, para na opção Enviar, selecione o **[!UICONTROL Mostrar mensagem]** e forneça uma mensagem na caixa de diálogo **[!UICONTROL Conteúdo da mensagem]** caixa. É uma caixa de rich text, você pode usar a opção de tela cheia para exibir todos os itens de rich text disponíveis.

## Configurar um esquema ou modelo de dados de formulário para um formulário adaptável{#configure-schema-or-data-model-for-form}

Você pode usar o Modelo de dados de formulário para conectar um formulário a uma Fonte de dados para enviar e receber dados com base nas ações do usuário. Você também pode conectar um formulário a um esquema JSON para receber os dados enviados em um formato predefinido. Com base no requisito, conecte seu formulário a um esquema JSON ou modelo de dados de formulário:

* [Crie um esquema JSON e faça upload para o seu ambiente](/help/forms/adaptive-form-json-schema-form-model.md)
* [Criar um modelo de dados de formulário](/help/forms/create-form-data-models.md)

### Configurar um esquema JSON ou um modelo de dados de formulário para o formulário

Para configurar um Esquema JSON ou um Modelo de dados de formulário para seu formulário:

1. Abra o Navegador de conteúdo e selecione a variável **[!UICONTROL Contêiner do guia]** componente do seu Formulário adaptável.
1. Clique nas propriedades do Container do guia ![Propriedades do guia](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Abra o **[!UICONTROL Modelo de dados]** guia.

   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável para configurar um esquema JSON ou um modelo de dados de formulário](/help/forms/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Selecione e configure um esquema JSON ou um modelo de dados de formulário, com base em seus requisitos:

   * Ao selecionar a variável **[!UICONTROL Modelo de formulário]** , use o **[!UICONTROL Selecionar modelo de dados do formulário]** opção para selecionar um modelo de dados de formulário pré-configurado.
   * Ao selecionar a variável **[!UICONTROL Esquema]** , use o **[!UICONTROL Esquema]** opção para selecionar um esquema JSON para o formulário.

1. Clique em **[!UICONTROL Concluído]**.

## Configurar um serviço de preenchimento  {#configure-prefill-service-for-form}

Você pode usar o serviço de preenchimento prévio para preencher automaticamente os campos de um Formulário adaptável usando dados existentes. Quando um usuário abre um formulário, os valores desses campos são preenchidos previamente. É possível:

* [Criar um serviço de preenchimento prévio personalizado](/help/forms/prepopulate-adaptive-form-fields.md)
* [Usar o serviço de preenchimento do modelo de dados de formulário](#fdm-prefill-service)

### Usar o serviço de preenchimento do modelo de dados de formulário para preencher previamente os campos de um formulário adaptável {#fdm-prefill-service}

Você pode usar o serviço de preenchimento do modelo de dados de formulário para preencher previamente os campos de um formulário adaptável usando um modelo de dados de formulário ou um serviço de preenchimento prévio personalizado. O serviço de Preenchimento do modelo de dados de formulário usa o [Obter serviço do modelo de dados de formulário configurado](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) para recuperar dados. Para usar o serviço de Preenchimento de modelo de dados de formulário para um Formulário adaptável:

1. Abra o Navegador de conteúdo e selecione a variável **[!UICONTROL Contêiner do guia]** componente do seu Formulário adaptável.
1. Clique nas propriedades do Container do guia ![Propriedades do guia](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique nas propriedades do Contêiner de formulário adaptável ![Propriedades do contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável para configurar os Modelos de dados é aberta.
   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner do formulário adaptável para configurar uma página de redirecionamento ou mensagem de agradecimento](/help/forms/assets/adaptive-forms-container-prefill-service.png)
1. Selecionar um modelo de dados do formulário. Abra o **[!UICONTROL Básico]** guia. No serviço de preenchimento, selecione **[!UICONTROL Serviço de preenchimento do modelo de dados de formulário]**.
1. Clique em **[!UICONTROL Concluído]**. O formulário adaptável agora está configurado para usar o Preenchimento prévio do modelo de dados de formulário. Agora você pode, use o [editor de regras](rule-editor.md) para criar regras para preencher previamente os campos do formulário.

## Editar propriedades do modelo de formulário de um formulário adaptável {#edit-form-model}

1. Selecione o Formulário adaptável e toque em ![Informações da página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Abrir propriedades]**. A página Propriedades do formulário é aberta.

1. Vá para a **[!UICONTROL Modelo de formulário]** e escolha um modelo de formulário. Se o Formulário adaptável não tiver um modelo de formulário, você terá a liberdade de escolher um esquema JSON ou um modelo de dados de formulário. Por outro lado, se o formulário adaptável já estiver baseado em um modelo de formulário, você terá a opção de alternar para outro modelo de formulário do mesmo tipo. Por exemplo, se o formulário estiver usando um esquema JSON, você poderá alternar facilmente para outro esquema JSON e, de forma semelhante, se o formulário estiver usando um Modelo de dados de formulário, você poderá alternar para outro Modelo de dados de formulário.

1. Toque **[!UICONTROL Salvar]** para salvar as propriedades.


## Ver próximo

* [Criar estilo ou temas para seus formulários](using-themes-in-core-components.md)
* [Adicionar comportamento dinâmico a formulários usando o editor de regras](rule-editor.md)
* [Definir layout de formulários para diferentes tamanhos de tela e tipos de dispositivo](/help/sites-cloud/authoring/features/responsive-layout.md)
* [Modelos de temas de amostra e modelos de dados de formulário](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)


## Artigo relacionado {#related-article}

* [Criar um formulário adaptável independente baseado nos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=pt-BR)
