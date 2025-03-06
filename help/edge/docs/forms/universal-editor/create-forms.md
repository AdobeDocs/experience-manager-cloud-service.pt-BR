---
title: Como criar um Forms adaptável independente usando o Universal Editor?
description: Este artigo explica como criar o Forms adaptável usando o assistente de Criação de formulários na instância de autor do AEM e publicar formulários no AEM Edge Delivery Services.
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 12%

---

# Criar formulários independentes usando o Editor universal (WYSIWYG)

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email com o nome da sua organização GitHub e o nome do repositório do seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>

Este artigo o orienta pelo processo de criação de formulários independentes com o Editor universal, selecionando um modelo baseado em Edge Delivery Services no Assistente de criação de formulários. Você também pode publicar os formulários criados com o Universal Editor no AEM Edge Delivery Services.

<!--To publish forms to Edge Delivery Services, you must first establish a connection between your AEM environment and your GitHub repository. Once connected, you can author the forms using the Universal Editor, which follows a WYSIWYG (What You See Is What You Get) approach for a seamless and consistent user experience with Sites.-->

Antes de começar, saiba mais sobre o tipo de componentes do Forms disponíveis para você:

* O [Edge Delivery Services para AEM Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) é um conjunto de serviços combináveis que permite um ambiente de desenvolvimento rápido, em que os autores podem atualizar, publicar e iniciar novos formulários rapidamente usando o Universal Editor. O Editor universal simplifica a criação de formulários para os Serviços de entrega de borda da Adobe com uma interface visual do WYSIWYG amigável.

* [Componentes principais de formulários adaptáveis](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR): Esses são componentes de captura de dados padronizados. Esses componentes oferecem recursos de personalização, redução do tempo de desenvolvimento e dos custos de manutenção para suas experiências de inscrição digital. Um desenvolvedor pode personalizar e estilizar facilmente esses componentes. Você pode visitar [https://aemcomponents.dev/](https://aemcomponents.dev/) para ver os componentes principais disponíveis em ação **A Adobe recomenda o uso desses componentes modernos e extensíveis para desenvolver formulários adaptáveis**.

* [Componentes de fundamentais de formulários adaptáveis](/help/forms/creating-adaptive-form.md): esses são componentes clássicos (antigos) de captura de dados. Você pode continuar usando-os para editar seus componentes fundamentais já existentes com base no formulário adaptável. Se estiver criando novos formulários, o Adobe recomenda usar os [Componentes principais para criar formulários adaptáveis](#create-an-adaptive-form-core-components).

O AEM Forms fornece um bloco, conhecido como Bloco adaptável do Forms, para ajudar você a criar facilmente o Edge Delivery Services Forms para capturar e armazenar dados. Você pode [criar um novo Projeto do AEM pré-configurado com o Bloco de Forms Adaptável](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) ou [adicionar o Bloco de Forms Adaptável a um Projeto de Site do AEM existente](#add-adaptive-forms-block-to-your-existing-aem-project).

![Fluxo De Trabalho Do Repositório Github](/help/edge/assets/repo-workflow.png)

## Pré-requisitos

* [Configure seu repositório GitHub](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) para estabelecer uma conexão entre seu ambiente AEM e o repositório GitHub.
* Se você já estiver usando o Edge Delivery Services, adicione a versão mais recente do [bloco adaptável do Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) ao seu repositório GitHub.
* A instância do Autor do AEM Forms inclui um modelo com base no Edge Delivery Services. Verifique se a [versão mais recente dos Componentes principais](https://github.com/adobe/aem-core-forms-components) está instalada em seu ambiente.
* Mantenha o URL da instância do autor do AEM Forms as a Cloud Service e do Repositório GitHub acessíveis.

## Criar um formulário adaptável usando o Editor universal

Com o Editor universal, você pode criar facilmente formulários independentes responsivos e interativos usando componentes prontos, como campos de texto, caixas de seleção e botões de opção. Ele oferece recursos avançados, como regras dinâmicas, integração de dados sem problemas e opções de personalização, permitindo criar formulários de acordo com seus requisitos exatos.

>[!NOTE]
>
> Você também pode [criar um formulário no Site do AEM usando o modelo de Site do Edge Delivery Services no Universal Editor e publicá-lo no Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project).

Para criar um formulário adaptável independente usando o Universal Editor, execute as seguintes etapas:

1. **Criar um formulário adaptável na instância de autor do AEM Forms**

   1. Acesse a instância do autor do AEM Forms as a Cloud Service.
   1. Selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O Assistente será aberto.
   1. Na guia **Source**, selecione um modelo de formulário baseado no Edge Delivery Services:

      ![Criar EDS Forms](/help/edge/assets/create-eds-forms.png)

   1. Clique em **[!UICONTROL Criar]** e o assistente **Criar formulário** será exibido.
   1. Especifique a **URL do GitHub**. Por exemplo, se o repositório GitHub for nomeado como `edsforms`, ele estiver localizado na conta `wkndforms`, a URL será:
      `https://github.com/wkndforms/edsforms`
   1. Clique em **[!UICONTROL Criar]**.

      ![Criar assistente de formulário](/help/edge/assets/create-form-wizard.png)

      Assim que você clicar em **[!UICONTROL Criar]**, o formulário será aberto no editor universal para criação.

      ![crie o formulário](/help/edge/assets/author-form.png)

      <!-- >[!NOTE]
        >
        > The Edge Delivery Services configuration for the forms based on Edge Delivery Services template is created automatically at the form's configuration container.-->

      Ao clicar em **[!UICONTROL Criar]**, o formulário é aberto no Editor Universal para criação.

1. **Criar o formulário no Editor Universal**

   1. Abra o navegador Conteúdo e navegue até o componente **[!UICONTROL Formulário adaptável]** na **Árvore de conteúdo**.

      ![árvore de conteúdo](/help/edge/assets/content-tree.png)

   1. Clique no ícone **[!UICONTROL Adicionar]** e adicione os componentes desejados da lista **Componentes de Formulários Adaptáveis**.

      ![adicionar componente](/help/edge/assets/add-component.png)

   1. Selecione o componente de Formulário adaptável adicionado e atualize suas propriedades usando **[!UICONTROL Propriedades]**.

      ![abrir propriedades](/help/edge/assets/component-properties.png)

      A captura de tela abaixo exibe o formulário `Registration Form` simples criado no Editor Universal:

      ![contate-nos pelo formulário](/help/edge/assets/contact-us.png)

      Agora você pode [configurar e personalizar as Ações de Envio de Formulário](/help/edge/docs/forms/universal-editor/submit-action.md).


<!--
## **Edge Delivery Services configuration of form**



   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Edge Delivery Services Configuration]** on your AEM Forms as a Cloud Service author instance.

        ![Select Edge Delivery Services Configuration](/help/edge/assets/select-eds-conf.png)
   1. Select the folder that matches the form's name. For example, if your form is called 'registration-form' choose the folder `forms/registration-form` and selct the configuration and publish the configuration:

        ![Edge Delivery Services Configuration](/help/edge/assets/aem-instance-eds-configuration.png)

   1. Click **[!UICONTROL Properties]** to see the configuration.   
        ![Automatically created configuration](/help/edge/assets/aem-forms-create-configuration-github.png)

        You can leave the Edge Host option as it is. The form would be published to both preview (.page) and live (.live) environments. 

   1. Click **[!UICONTROL Save and Close]**. The configuration is saved. -->

## Publicar o formulário

Agora publique o formulário independente no Edge Delivery Services clicando no botão **[!UICONTROL Publicar]** no canto superior direito do Editor Universal.

![formulário de publicação](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> Consulte o artigo [Publicar e implantar](/help/edge/docs/forms/universal-editor/publish-forms.md) para saber como publicar um formulário no Edge Delivery Services.

Veja como acessar o formulário no Edge Delivery Services:

* **Versão Preparada (para teste)**: a versão preparada exibe a versão não publicada e funcional do formulário para fins de teste. Use o seguinte formato de URL para visualizar o formulário antes que ele entre em vigor:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  Por exemplo, se o repositório do seu projeto for chamado de &quot;edsforms&quot;, estiver localizado na conta &quot;wkndforms&quot; e estiver usando a ramificação &quot;main&quot; e o formulário como &quot;Registration Form&quot;, o URL da versão preparada será semelhante ao seguinte:
  `https://main--edsforms--wkndforms.aem.page/content/forms/af/registration-form`

* **Versão ao Vivo (formulário publicado)**:   A versão ao vivo exibe a versão publicada mais recentemente do formulário, acessível aos usuários finais. Use o seguinte formato de URL para acessar a versão publicada e em tempo real do formulário:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  Por exemplo, se o repositório do seu projeto for chamado de &quot;edsforms&quot;, estiver localizado na conta &quot;wkndforms&quot; e estiver usando a ramificação &quot;main&quot; e o formulário como &quot;Registration Form&quot;, o URL da versão preparada será semelhante ao seguinte:
  `https://main--edsforms--wkndforms.aem.live/content/forms/af/registration-form`

A estrutura do URL permanece a mesma para as versões preparadas e ativas. No entanto, o conteúdo exibido é diferente com base no contexto:

![Exibir formulário publicado](/help/edge/assets/eds-view-publish-form.png)

## Resolução de problemas

Está tendo problemas para carregar o formulário? Estes são alguns problemas comuns e como corrigi-los:

* **URL do formulário**: verifique se a URL do seu formulário não inclui a extensão &quot;.html&quot; no final. O Edge Deliver Service não exige essa extensão.

* **URL do Autor do AEM** L: verifique se a URL do Autor do AEM listada no arquivo `fstab.yaml` está formatada corretamente. Ele deve incluir os seguintes detalhes:

   * O proprietário correto do GitHub
   * O nome correto do repositório
   * A ramificação específica que você está usando para o Edge Delivery Services

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## Começar a criar formulários

{{universal-editor-see-also}}
