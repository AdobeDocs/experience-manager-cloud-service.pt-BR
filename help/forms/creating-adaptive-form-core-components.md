---
title: 'Construtor de formulários: criar formulários com componentes principais'
description: Saiba como usar o construtor de formulários do AEM Forms para criar formulários adaptáveis com componentes principais. Perfeito para criadores de formulários que precisam de formulários HTML5 responsivos que simplificam a coleta e o processamento de informações.
keywords: construtor de formulários, componentes principais, criar formulários, criador de formulários, formulários adaptáveis, criar formulários, formulários do AEM, formulários responsivos
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2445'
ht-degree: 40%

---

# Construtor de formulários: criar formulários com componentes principais {#creating-an-adaptive-form-core-components}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-an-adaptive-form-core-components.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |


O construtor de formulários do AEM Forms permite criar formulários envolventes, responsivos, dinâmicos e adaptáveis. Quer você seja um criador de formulários que cria formulários profissionais ou precise criar formulários responsivos rapidamente, o AEM Forms fornece um assistente amigável. O assistente fornece uma navegação rápida por guias para selecionar facilmente modelos pré-configurados, estilos, campos e opções de envio.

Antes de começar, saiba mais sobre o tipo de componentes do Forms disponíveis para você:

* [Componentes principais de formulários adaptáveis](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR): Esses são componentes de captura de dados padronizados. Esses componentes oferecem recursos de personalização, redução do tempo de desenvolvimento e dos custos de manutenção para suas experiências de inscrição digital. Um desenvolvedor pode personalizar e estilizar facilmente esses componentes. A Adobe recomenda usar esses componentes modernos e extensíveis para desenvolver o Adaptive Forms.

* [Componentes de fundamentais de formulários adaptáveis](creating-adaptive-form.md): esses são componentes clássicos (antigos) de captura de dados. Você pode continuar usando-os para editar seus componentes fundamentais já existentes com base no formulário adaptável. Se você estiver criando novos formulários, a Adobe recomenda usar os [Componentes principais do Forms Adaptive](creating-adaptive-form-core-components.md) para criar um Forms Adaptável.

![Assistente para criar um formulário adaptável](/help/release-notes/assets/wizard.png)

## Aplicabilidade e casos de uso

### Seguros

## O AEM Forms pode ser usado para processos de seguro internos e voltados para o cliente?

Sim. O AEM Forms oferece suporte a formulários digitais voltados para o cliente, bem como a processos internos, conduzidos por funcionários ou agentes, como revisões, aprovações e captura assistida de dados.

## O AEM Forms pode ser usado para envio de solicitações de seguro?

Sim. O AEM Forms oferece suporte a formulários adaptáveis em várias etapas que permitem aos segurados enviar solicitações de seguro digitalmente, incluindo a captura de dados estruturados e a documentação de apoio.

## O AEM Forms oferece suporte a solicitações de seguro móvel?

Sim. O AEM Forms oferece suporte a formulários responsivos e compatíveis com dispositivos móveis, permitindo que clientes e agentes enviem informações de seguro de dispositivos móveis.

## Pré-requisitos

Você precisará do seguinte para criar um formulário adaptável:


* **Habilitar os Componentes principais adaptáveis do Forms para o seu ambiente**: quando você cria um programa, os Componentes principais adaptáveis do Forms já estão habilitados para o seu ambiente.  Instale os componentes principais adaptáveis do Forms mais recentes até o momento para ativar o ambiente do AEM Cloud Service. Ao habilitar os Componentes principais para seu ambiente, os modelos e temas do **Forms adaptável (Componente principal)** são adicionados ao seu ambiente. Se sua versão do SDK do AEM for anterior à 2023.02.0, [certifique-se de que`prerelease` o sinalizador esteja habilitado em seu ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=pt-BR#new-features), pois os componentes principais dos formulários adaptáveis faziam parte do pré-lançamento antes da versão 2023.02.0.

* **Um modelo de formulário adaptável**: um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um formulário adaptável. Ele tem componentes pré-formatados que contêm determinadas propriedades e estrutura de conteúdo. Também fornece as opções para definir um tema e uma ação de envio. O tema define a aparência, e a ação de envio define a ação a ser executada no envio de um formulário adaptável. Por exemplo, enviar os dados coletados para uma fonte de dados. O serviço de nuvem fornece um modelo OOTB, chamado de em branco:

   * O modelo `blank` está incluído em todos os novos programas do AEM Forms as a Cloud Service.
   * É possível instalar o pacote de referência, por meio do Gerenciador de pacotes, para adicionar o modelo `blank` para o seu programa do AEM Forms as a Cloud Service.
   * Você também pode [criar um modelo Adaptive Forms (Componentes principais)](/help/forms/template-editor-core-components.md) do zero.
   * Você também pode implantar [modelos de amostra](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=pt-BR) em seu ambiente. Isso o ajuda a começar a criar formulários rapidamente.

* **Um tema de formulários adaptáveis**: um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Ao aplicar um tema, o estilo especificado é refletido nos componentes correspondentes.  O modelo `Canvas` é incluído em todos os novos programas do AEM Forms as a Cloud Service. Você também pode implantar [temas de amostra](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=pt-BR) em seu ambiente. Isso o ajuda a começar a estilizar seus formulários e a fornecer uma estrutura básica para criar ou personalizar um tema de acordo com os requisitos da empresa.

  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create an Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Permissões**: adicionar usuários ao grupo [!DNL forms-users]. Os membros do grupo [!DNL forms-users] tem permissões para criar formulários adaptáveis. Para obter uma lista detalhada de grupos de usuários específicos de formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=pt-BR) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## Criar um formulário adaptável  {#create-an-adaptive-form-core-components}

1. Faça logon na Instância de criação do [!DNL Experience Manager Forms]. Pode ser uma instância da nuvem ou uma instância de desenvolvimento local.

1. Insira suas credenciais na página de logon do Experience Manager. Depois de fazer logon, no canto superior esquerdo, selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.

1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O Assistente será aberto. Na guia Origem, selecione um modelo:

   ![Modelo dos componentes principais](/help/forms/assets/core-components-template.png)

   Ao selecionar um modelo, o tema e a ação de envio especificados no modelo são selecionados automaticamente e o botão **[!UICONTROL Criar]** será habilitado. Você pode ir para as guias **[!UICONTROL Estilo]** ou **[!UICONTROL Envio]** para selecionar um tema ou uma ação de envio diferente. Se o modelo selecionado não especificar um tema, o botão criar permanecerá desabilitado. É possível ir para a guia **[!UICONTROL Estilos]** para selecionar um tema manualmente.

   >[!NOTE]
   >
   >
   > Se você não tiver o modelo **Formulários adaptáveis (componente principal)** em seu ambiente, [Habilite os Componentes principais dos formulários adaptáveis para o seu ambiente](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). Ao habilitar os componentes principais no seu ambiente, o modelo **Formulários adaptáveis (Componente principal)** será adicionado ao seu ambiente.

1. Na guia **[!UICONTROL Estilo]**, selecione um tema:

   * Quando o modelo selecionado especifica um tema, ele é selecionado automaticamente no assistente. Você também pode escolher um tema diferente da guia de Estilo.

   * Se o modelo selecionado não especificar um tema, será possível usar a guia de Estilo para escolher um tema. O botão **[!UICONTROL Criar]** só será habilitado depois que um tema for selecionado.

1. (Opcional) Na guia Dados, selecione um modelo de dados:

   * **Modelo de dados de formulário (FDM)**: o [Modelo de Dados de Formulário](data-integration.md) permite integrar entidades e serviços de diferentes fontes de dados a um Formulário adaptável. Escolha Modelo de dados de formulário (FDM) se o Formulário adaptável que você está criando envolver a busca e a gravação de dados de e para várias fontes de dados.

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

1. Selecione **[!UICONTROL Criar]**. Um Formulário adaptável será criado e aberto no editor de Formulários adaptáveis. O editor exibirá o conteúdo disponível no modelo.  Com base no tipo de Formulário adaptável, os elementos de formulário presentes no esquema JSON do <!--XFA form template, XML schema or --> associado ou no Modelo de Dados de Formulário (FDM) são exibidos na guia **[!UICONTROL Objetos do Modelo de Dados]** do **[!UICONTROL Navegador de Conteúdo]** na barra lateral. Também é possível arrastar e soltar esses elementos para criar seu formulário adaptável.

Agora você pode arrastar e soltar os [Componentes principais do Forms adaptável](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) no contêiner do Adaptive Forms para criar o formulário. Você também pode visitar [https://aemcomponents.dev/](https://aemcomponents.dev/) para ver os componentes principais disponíveis em ação.

>[!NOTE]
>
> Você também pode [criar o Adaptive Forms usando modelos de formulário XFA (arquivos *.XDP)](/help/forms/create-adaptive-form-using-xfa-templates.md). Ela permite economizar tempo, reutilizando campos de arquivos XDP diretamente no Adaptive Forms.

## Configurar a ação de envio para um formulário adaptável {#configure-submit-action-for-form}

Uma ação enviar permite escolher o destino dos dados capturados por meio de um formulário adaptável. É acionado quando um usuário clica no botão Enviar em um Formulário adaptável. Os formulários adaptáveis incluem algumas ações de envio prontas para uso. Você também pode estender ações de envio padrão para criar sua própria ação de envio personalizada. Para configurar uma Ação de envio para o formulário:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.

1. Clique na guia **[!UICONTROL Envio]**.

   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável para configurar uma ação de envio](/help/forms/assets/adaptive-forms-submit-message.png)

1. Selecione e configure uma **[!UICONTROL Ação de envio]**, com base em suas necessidades. Para obter informações detalhadas sobre Ações de Envio, consulte [Ação de Envio do Formulário Adaptável](/help/forms/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Redirecionar o usuário para uma página ou mostrar uma mensagem de agradecimento no envio do formulário

No envio de um formulário, você pode redirecionar o usuário para outra página da Web ou uma mensagem. Para redirecionar o usuário ou configurar a mensagem de agradecimento:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Abra a guia **[!UICONTROL Envio]**.

   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável e configurar uma página de redirecionamento ou mensagem de agradecimento](/help/forms/assets/adaptive-forms-redirect-message.png)

   * Para configurar uma URL de Redirecionamento, para a opção Enviar, selecione a opção **[!UICONTROL Redirecionar para URL]** e procure e selecione uma página do AEM Sites ou forneça a URL de uma página externa.

   * Para configurar uma mensagem personalizada ou de agradecimento, para a opção Enviar, selecione a opção **[!UICONTROL Mostrar Mensagem]** e forneça uma mensagem na caixa **[!UICONTROL Conteúdo da Mensagem]**. É uma caixa de rich text, você pode usar a opção de tela cheia para exibir todos os itens de rich text disponíveis.

## Configurar um esquema ou modelo de dados de formulário (FDM) para um formulário adaptável{#configure-schema-or-data-model-for-form}

Você pode usar o Modelo de dados de formulário (FDM) para conectar um formulário a um Source de dados para enviar e receber dados com base nas ações do usuário. Também é possível conectar um formulário a um esquema JSON para receber os dados enviados em um formato predefinido. Com base no requisito, conecte seu formulário a um esquema JSON ou Modelo de dados de formulário (FDM):

* [Criar um esquema JSON e carregar para o seu ambiente](/help/forms/adaptive-form-json-schema-form-model.md)
* [Criar um Modelo de Dados de Formulário (FDM)](/help/forms/create-form-data-models.md)

### Configure um esquema JSON ou um modelo de dados de formulário (FDM) para o seu formulário

Para configurar um Esquema JSON ou um Modelo de dados de formulário (FDM) para seu formulário:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Abra a guia **[!UICONTROL Modelo de Dados]**.

   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável para configurar um esquema JSON ou um modelo de dados de formulário (FDM)](/help/forms/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Selecione e configure um Esquema JSON ou um Modelo de dados de formulário (FDM), com base em seus requisitos:

   * Ao selecionar a opção **[!UICONTROL Modelo de formulário]**, use a opção **[!UICONTROL Selecionar modelo de dados de formulário]** para selecionar um modelo de dados de formulário (FDM) pré-configurado.
   * Ao selecionar a opção **[!UICONTROL Esquema]**, use a opção **[!UICONTROL Esquema]** para selecionar um esquema JSON para o formulário.

1. Clique em **[!UICONTROL Concluído]**.

## Configurar um serviço de preenchimento  {#configure-prefill-service-for-form}

Você pode usar o serviço de preenchimento prévio para preencher automaticamente os campos de um Formulário adaptável usando dados existentes. Quando um usuário abre um formulário, os valores desses campos são preenchidos previamente. É possível:

* [Criar um serviço de preenchimento prévio personalizado](/help/forms/prepopulate-adaptive-form-fields.md)
* [Usar o serviço de preenchimento do modelo de dados de formulário](#fdm-prefill-service)

### Usar o serviço de preenchimento do modelo de dados de formulário para preencher previamente os campos de um formulário adaptável {#fdm-prefill-service}

Você pode usar o serviço de preenchimento do modelo de dados de formulário para preencher previamente os campos de um formulário adaptável usando um modelo de dados de formulário ou um serviço de preenchimento prévio personalizado. O serviço de Preenchimento de Modelo de Dados de Formulário usa o [Obter Serviço do Modelo de Dados de Formulário](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) configurado para recuperar dados. Para usar o serviço de Preenchimento de modelo de dados de formulário para um Formulário adaptável:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique no ícone de propriedades do Contêiner de formulário adaptável ![propriedades do Contêiner de formulário adaptável](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável para configurar os Modelos de dados é aberta.
   ![Clique no ícone de chave inglesa para abrir a caixa de diálogo Contêiner de formulário adaptável e configurar uma página de redirecionamento ou mensagem de agradecimento](/help/forms/assets/adaptive-forms-container-prefill-service.png)
1. Selecione um modelo de dados de formulário (FDM). Abra a guia **[!UICONTROL Básico]**. No serviço de preenchimento, selecione **[!UICONTROL Serviço de Preenchimento de Modelo de Dados de Formulário]**.
1. Clique em **[!UICONTROL Concluído]**. O formulário adaptável agora está configurado para usar o Preenchimento prévio do modelo de dados de formulário. Agora você pode usar o [editor de regras](rule-editor.md) para criar regras e preencher previamente os campos do formulário.

## Editar propriedades do modelo de formulário de um formulário adaptável {#edit-form-model}

1. Selecione o Formulário adaptável e selecione ![Informações da página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Abrir propriedades]**. A página Propriedades do formulário será aberta.

1. Vá para a guia **[!UICONTROL Modelo de formulário]** e escolha um modelo de formulário. Se o Formulário adaptável não tiver um modelo de formulário, você terá a liberdade de escolher um esquema JSON ou um modelo de dados de formulário (FDM). Por outro lado, se o formulário adaptável já estiver baseado em um modelo de formulário, você terá a opção de alternar para outro modelo de formulário do mesmo tipo. Por exemplo, se o formulário estiver usando um esquema JSON, você poderá alternar facilmente para outro esquema JSON e, de forma semelhante, se o formulário estiver usando um Modelo de dados de formulário (FDM), será possível alternar para outro Modelo de dados de formulário (FDM).

1. Selecione **[!UICONTROL Salvar]** para salvar as propriedades.


## Como renomear um formulário adaptável do AEM? {#rename-an-AEM-Adaptive-Form}

Para renomear um formulário adaptável, execute as seguintes etapas:

1. Selecione um formulário adaptável na interface do usuário do AEM Forms.
1. Clique nas **Propriedades** localizadas no painel superior.
1. Altere o nome do formulário na guia **Título**, conforme mostrado na imagem abaixo.
1. Clique em **Salvar e fechar**.

![Renomear um Formulário adaptável do AEM](/help/forms/assets/change-af-name.png)



