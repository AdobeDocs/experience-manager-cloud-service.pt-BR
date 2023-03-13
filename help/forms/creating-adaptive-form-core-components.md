---
title: Como criar um formulário adaptável?
description: Saiba como criar um Formulário adaptável usando o [!DNL Experience Manager Forms]. Os Forms adaptáveis são formulários de HTML5 responsivos que simplificam a coleta e o processamento de informações. Saiba mais sobre como criar um Formulário adaptável com base em um Modelo de dados de formulário e um esquema XML ou JSON.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
source-git-commit: ae208e9ac35c3c464d9beeaa3bc2bddc0ecf52bb
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 1%

---


# Criar um formulário adaptável (componentes principais) {#creating-an-adaptive-form-core-components}

Formulários adaptáveis fornecem uma experiência envolvente, responsiva, dinâmica e adaptável. O AEM Forms fornece um assistente prático para que o usuário empresarial crie rapidamente o Adaptive Forms. O assistente fornece uma navegação rápida por guias para selecionar facilmente o modelo pré-configurado, o estilo, os campos e as opções de envio para criar um Formulário adaptável.

Antes de começar, saiba mais sobre o tipo de componentes do Forms disponíveis para você:

* [Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en): Esses são componentes de captura de dados padronizados. Esses componentes fornecem recursos de personalização, tempo de desenvolvimento reduzido e custos de manutenção mais baixos para suas experiências de inscrição digital. Um desenvolvedor pode personalizar e estilizar facilmente esses componentes. A Adobe recomenda aproveitar esses componentes modernos e extensíveis para desenvolver o Adaptive Forms.

* [Componentes adaptáveis do Forms Foundation](creating-adaptive-form.md): esses são componentes clássicos (antigos) da captura de dados. Você pode continuar a usá-los para editar seus componentes de base existentes com base no Formulário adaptável. Se você estiver criando novos formulários, o Adobe recomenda usar  [Componentes principais adaptáveis do Forms](creating-adaptive-form-core-components.md) para criar uma Forms adaptável.

![Assistente para criar um formulário adaptável](/help/release-notes/assets/wizard.png)


## Pré-requisitos

Você precisa do seguinte para criar um Formulário adaptável:

* **Ativar os Componentes principais adaptáveis do Forms para o seu ambiente**: ao criar um novo programa, os Componentes principais adaptáveis do Forms já estão habilitados para o seu ambiente. Se você tiver um ambiente as a Cloud Service do Forms com base no Archetype 39 ou anterior, [Ativar os Componentes principais adaptáveis do Forms para o seu ambiente](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). Ao ativar os Componentes principais para seu ambiente, a variável **Forms adaptável (componente principal)** o modelo e o tema da tela são adicionados ao seu ambiente.

* **Um modelo de formulário adaptável**: um modelo fornece uma estrutura básica e define a aparência (layouts e estilos) de um Formulário adaptável. Ele tem componentes pré-formatados que contêm determinadas propriedades e estrutura de conteúdo. Também fornece as opções para definir um tema e uma ação de envio. O tema define a aparência e a aparência, e a ação de envio define a ação a ser executada no envio de um Formulário adaptável. Por exemplo, enviar os dados coletados para uma fonte de dados. O serviço de nuvem fornece um modelo OOTB, chamado em branco:

   * A variável `blank` O modelo de está incluído em todos os novos programas do AEM Forms as a Cloud Service.
   * É possível instalar o pacote de referência, por meio do Gerenciador de pacotes, para adicionar o `blank` para o seu programa AEM Forms as a Cloud Service.
   * Também é possível [criar um novo modelo do Forms adaptável (Componentes principais)](template-editor.md) do zero.

* **Um tema de formulário adaptável**: um tema contém detalhes de estilo para os componentes e painéis. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência, alinhamento e tamanho. Quando você aplica um tema, o estilo especificado é refletido nos componentes correspondentes.  A variável `Canvas` O modelo de está incluído em todos os novos programas do AEM Forms as a Cloud Service.

   <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Permissões**: adicionar usuários ao [!DNL forms-users] grupo. Os membros da [!DNL forms-users] grupo tem permissões para criar um Formulário adaptável. Para obter uma lista detalhada de grupos de usuários específicos dos formulários, consulte [Grupos e permissões](forms-groups-privileges-tasks.md).


## Criar um formulário adaptável (componentes principais) {#create-an-adaptive-form-core-components}

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

Agora, você pode arrastar e soltar os Componentes principais do Adaptive Forms no contêiner do Adaptive Forms para projetar e criar o formulário.

## Componentes principais do Forms adaptável disponíveis

Os Componentes principais adaptáveis do Forms são componentes de captura de dados padronizados. Esses componentes fornecem recursos de personalização, ajudam a reduzir o tempo de desenvolvimento e os custos de manutenção das suas experiências de inscrição digital. [Documentação dos Componentes principais do Forms adaptável](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en) A tem uma lista detalhada dos componentes disponíveis, juntamente com informações detalhadas sobre os recursos de cada componente. Você também pode visitar [https://aemcomponents.dev/](https://aemcomponents.dev/) para ver os componentes principais disponíveis em ação.

## Editar propriedades do modelo de formulário de um formulário adaptável {#edit-form-model}

1. Selecione o Formulário adaptável e toque em ![Informações da página](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Abrir propriedades]**. A página Propriedades do formulário é aberta.

1. Vá para a **[!UICONTROL Modelo de formulário]** e escolha um modelo de formulário. Se o Formulário adaptável não tiver um modelo de formulário, você terá a liberdade de escolher um esquema JSON ou um modelo de dados de formulário. Por outro lado, se o formulário adaptável já estiver baseado em um modelo de formulário, você terá a opção de alternar para outro modelo de formulário do mesmo tipo. Por exemplo, se o formulário estiver usando um esquema JSON, você poderá alternar facilmente para outro esquema JSON e, de forma semelhante, se o formulário estiver usando um Modelo de dados de formulário, você poderá alternar para outro Modelo de dados de formulário.

1. Toque **[!UICONTROL Salvar]** para salvar as propriedades.
