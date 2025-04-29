---
title: Como criar formulários independentes com base nos Componentes principais ou modelos do Edge Delivery Services e publicá-los no Edge Delivery Services
description: Este artigo explica como criar o Forms adaptável selecionando um modelo baseado em Componente principal ou baseado em Edge Delivery Services no Assistente de criação de formulário. Você também pode publicar os formulários no AEM Edge Delivery Services.
feature: Edge Delivery Services
role: User
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: c68e98cfe442d0b5a928fde596e193073d5cac21
workflow-type: tm+mt
source-wordcount: '1644'
ht-degree: 0%

---


# Da criação à publicação: AEM Forms no Edge Delivery Services

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email com o nome da sua organização GitHub e o nome do repositório do seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>

O Adobe Experience Manager (AEM) permite criar formulários envolventes, responsivos e dinâmicos. Ele oferece vários métodos de criação, cada um adequado a diferentes requisitos e níveis de conhecimento do usuário&#x200B;

Este artigo se concentra na abordagem em que os formulários são criados no ambiente do AEM e publicados por meio do Edge Delivery Services. O Forms criado com o uso de modelos baseados em Componentes principais pode ser publicado no AEM e no Edge Delivery Services, oferecendo flexibilidade na implantação. Por outro lado, os formulários criados usando modelos baseados no Edge Delivery Services só podem ser publicados no Edge Delivery Services.&#x200B;

![Criar e publicar o formulário adaptável](/help/edge/docs/forms/universal-editor/assets/author-publish-af.png){width=50% align=center}

## Vantagens de criar formulários no AEM e publicar usando o Edge Delivery Services:

* **Preservação de fluxos de trabalho existentes do AEM**: as organizações podem continuar usando seus fluxos de trabalho e estruturas de governança estabelecidos do AEM, garantindo consistência e controle sobre a criação de conteúdo.&#x200B;

* **Desempenho aprimorado**: a publicação por meio do Edge Delivery Services resulta em tempos de renderização mais rápidos, melhorando a experiência do usuário e reduzindo o tempo de carregamento da página.&#x200B;

* **SEO aprimorado**: o Edge Delivery Services foi projetado para fornecer conteúdo com pontuações altas no Google Lighthouse, o que pode resultar em uma melhor otimização do mecanismo de pesquisa e maior visibilidade.&#x200B;

* **Opções de implantação flexíveis**: o Forms criado com os Componentes principais pode ser publicado no AEM e no Edge Delivery Services, oferecendo flexibilidade nas estratégias de implantação.&#x200B;

## Antes de começar

Antes de começar a criar formulários no AEM e publicá-los por meio do Edge Delivery Services, verifique se os seguintes pré-requisitos foram atendidos:

* Verifique se você tem um Repositório GitHub configurado para o Edge Delivery Services.
   * Se você não tiver um repositório, [novo projeto do AEM pré-configurado com o Bloco de Forms Adaptável](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block).
   * Se você tiver um repositório, adicione o bloco adaptável do Forms ao seu repositório existente. Instruções detalhadas estão disponíveis na [Introdução ao Edge Delivery Services para AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project).
* Estabeleça uma conexão entre seu ambiente AEM e o repositório GitHub. [Como fazer?](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)

Um diagrama de fluxo de decisão para orientar a configuração e a publicação do Forms adaptável:

![Fluxo De Trabalho Do Repositório Github](/help/forms/assets/repo-workflow.png){width=auto}

## Criação de formulários no AEM e sua publicação no Edge Delivery Services

Siga estas etapas para criar formulários no AEM e publicá-los no Edge Delivery Services:

[1. Escolha um modelo e crie o formulário](#choose-a-template-and-create-the-form)

[2. Crie o formulário](#author-the-form)

[3. Publicar um formulário](#publish-a-form)

### Escolha um modelo e crie o formulário

É possível criar formulários em uma instância do AEM para publicação no Edge Delivery Services usando:

>[!BEGINTABS]

>[!TAB modelo baseado em Edge Delivery Services]

Execute as seguintes etapas para escolher o modelo e criar o formulário:

1. Faça logon na instância de autor do AEM Forms as a Cloud Service.
1. Selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O Assistente será aberto.
1. Na guia **Source**, selecione um **modelo baseado no Edge Delivery Services**:

   ![Criar EDS Forms](/help/edge/assets/create-eds-forms.png)

   Quando você seleciona um **modelo baseado em Edge Delivery Services**, o botão **[!UICONTROL Criar]** é habilitado.
1. (Opcional) Nas guias **[!UICONTROL Source de Dados]** ou **[!UICONTROL Envio]**, você pode selecionar uma fonte de dados ou uma ação de envio.
1. (Opcional) Na guia **[!UICONTROL Entrega]**, você pode especificar uma data de publicação ou cancelamento da publicação para um formulário.
1. Clique em **[!UICONTROL Criar]** e o assistente **Criar formulário** será exibido:

   1. Especifique o **Nome** e o **Título**.
   1. Especifique a **URL do GitHub**. Por exemplo, se o repositório GitHub for nomeado como `edsforms`, ele estiver localizado na conta `wkndforms`, a URL será:
      `https://github.com/wkndforms/edsforms`

   ![Criar assistente de formulário](/help/edge/assets/create-form-wizard.png)

   Ao clicar em **[!UICONTROL Criar]**, o formulário é aberto no Editor Universal para criação.

   ![crie o formulário](/help/edge/assets/author-form.png)
1. Clique em **[!UICONTROL Criar]** para criar o formulário. Agora, você pode [criar o formulário usando o Editor Universal](#author-the-form).

>[!TAB Modelo baseado em Componente Principal]

Execute as seguintes etapas para escolher o modelo e criar o formulário:

1. Faça logon na instância de autor do AEM Forms as a Cloud Service.
1. Selecione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Forms Adaptável]**. O Assistente será aberto.
1. Na guia **Source**, selecione um **modelo baseado em Componente Principal** e um **tema**. O botão **[!UICONTROL Criar]** está habilitado.:

![Modelo baseado no Componente principal](/help/forms/assets/core-component-based-template.png)

1. (Opcional) Nas guias **[!UICONTROL Source de Dados]** ou **[!UICONTROL Envio]**, você pode selecionar uma fonte de dados ou uma ação de envio.
1. (Opcional) Na guia **[!UICONTROL Entrega]**, você pode especificar uma data de publicação ou cancelamento da publicação para um formulário.
1. Clique em **[!UICONTROL Criar]** e o assistente **Criar formulário** será exibido para:
   1. Especifique o **Nome** e o **Título**.
   2. Especifique o local no campo **Caminho** onde o Formulário adaptável deve ser salvo.

   ![Criar Assistente de Formulário](/help/forms/assets/create-cc-form.png)

   Ao clicar em **[!UICONTROL Criar]**, o formulário é aberto no Editor de Formulário Adaptável para criação.

   ![Editor de formulário adaptável](/help/forms/assets/af-editor-form.png)

1. Clique em **[!UICONTROL Criar]** para criar o formulário. Agora, você pode [criar o formulário usando o Editor de Formulário Adaptável](#author-the-form).

>[!ENDTABS]

### Criar o formulário

Os formulários criados com o modelo baseado em Edge Delivery Services são abertos no [Editor Universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) para criação. No entanto, os formulários criados usando o modelo baseado nos Componentes principais são abertos no Editor de formulários adaptáveis para criação.

Execute as seguintes etapas para criar formulários usando o Editor universal para modelo baseado em Edge Delivery Services ou usando o Editor de formulário adaptável para modelo baseado em Componente principal:

>[!BEGINTABS]

>[!TAB modelo baseado em Edge Delivery Services]


1. Abra o navegador Conteúdo e navegue até o componente **[!UICONTROL Formulário adaptável]** na **Árvore de conteúdo**.

   ![árvore de conteúdo](/help/edge/assets/content-tree.png)

1. Clique no ícone **[!UICONTROL Adicionar]** e adicione os componentes desejados da lista **Componentes de Formulários Adaptáveis**.
   ![adicionar componente](/help/edge/assets/add-component.png)

   A captura de tela abaixo exibe o `Registration Form` criado no Editor Universal:

   ![contate-nos pelo formulário](/help/edge/assets/contact-us.png)

>[!NOTE]
>
> Para obter instruções detalhadas sobre como criar um Formulário adaptável usando o Universal Editor, [clique aqui](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

Agora você pode [configurar e personalizar as ações de envio para formulários](/help/edge/docs/forms/universal-editor/submit-action.md).

>[!TAB Modelo baseado em Componente Principal]

1. Clique em **[!UICONTROL Inserir componente]** na seção **Arraste componentes aqui**.

   ![Arraste componentes aqui](/help/forms/assets/drag-components-af-editor.png)

1. Adicione os componentes desejados da lista **Componentes de formulários adaptáveis**.

   ![Adicionar componentes](/help/forms/assets/add-component-af.png)

A captura de tela abaixo exibe o `Enrollment Form` criado no Editor de Formulário Adaptável:

![Editor de formulário adaptável](/help/forms/assets/af-editor-form.png)

>[!NOTE]
>
> Para obter orientações detalhadas sobre como criar um Formulário adaptável com base no modelo dos Componentes principais, [clique aqui](/help/forms/creating-adaptive-form-core-components.md).

Agora você pode [configurar as ações de envio para formulários](/help/forms/configure-submit-actions-core-components.md).

>[!ENDTABS]

### Publicar o formulário

Para publicar um Formulário adaptável no Edge Delivery Services, você precisa [criar uma Configuração do Edge Delivery Services em uma instância do AEM](#create-an-edge-delivery-services-configuration).

#### Criar uma configuração do Edge Delivery Services

Execute as seguintes etapas para criar a Configuração do Edge Delivery Services:

>[!BEGINTABS]
>[!TAB Para formulários criados usando o modelo baseado em Edge Delivery Services]


A configuração do Edge Delivery Services para formulários com base no modelo baseado em Edge Delivery Services é criada automaticamente no contêiner de configuração do formulário.

![Configuração do Edge Delivery Services](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB Para formulários criados usando o modelo baseado no Componente Principal]

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração do Edge Delivery Services]** na instância de autor do AEM Forms as a Cloud Service.

   ![Selecionar configuração do Edge Delivery Services](/help/edge/assets/select-eds-conf.png)

1. Selecione a pasta que corresponde ao nome do formulário. Por exemplo, se o formulário for chamado de `enrollment-form`, escolha a pasta `forms/enrollment-form` e clique em **[!UICONTROL Criar]** > **[!UICONTROL Configuração]**:

   ![Configuração do Edge Delivery Services](/help/forms/assets/create-eds-conf.png)

1. Clique em **[!UICONTROL Configuração do Edge Delivery Services]** e em **[!UICONTROL Propriedades]** para abrir as propriedades:

   ![Configuração criada automaticamente](/help/forms/assets/eds-conf.png)

   A tela Edge Delivery Services Configuration (Configuração do) é exibida.

1. Especifique o seguinte na Configuração do Edge Delivery Services:

   * **Organização**: especifique seu nome de organização do GitHub.

   * **Nome do site**: especifique seu nome de repositório do GitHub.
   * **Ramificação**: especifique o nome da ramificação. Deixe a caixa de texto vazia se estiver usando a ramificação principal.
   * **(Opcional) Host Edge**: deixe a opção Host Edge como está. O formulário é publicado nos ambientes de visualização (.page) e live (.live).
   * **(Opcional) Token de Autenticação do Site**: use o Token de Autenticação do Site para autenticar com segurança as solicitações entre a instância do AEM e a Edge Delivery Services.

1. Clique em **[!UICONTROL Salvar e fechar]**. A configuração é criada.

>[!ENDTABS]

#### Acessar o formulário no Edge Delivery Services

Para acessar o formulário no Edge Delivery Services, é obrigatório publicá-lo. Execute as seguintes etapas para publicar o formulário:

>[!BEGINTABS]
>[!TAB No Editor Universal]

1. Publique o formulário clicando no botão **[!UICONTROL Publicar]** no canto superior direito do Editor Universal.

![formulário de publicação](/help/edge/assets/publish-form.png)

>[!NOTE]
>
> Consulte o artigo [Publicar e implantar](/help/edge/docs/forms/universal-editor/publish-forms.md) para saber como publicar um formulário no Edge Delivery Services.

>[!TAB No Editor de Formulário Adaptável]

1. No console Experience Manager Forms, navegue até a pasta principal e selecione um formulário que deseja publicar.

1. Clique na opção **[!UICONTROL Publicar]** da barra de ferramentas e veja todos os ativos de referência que seriam publicados com o formulário.

![Publicar formulário no Editor de formulário adaptável](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> Consulte o artigo [Gerenciar publicação no Experience Manager Forms](/help/forms/manage-publication.md) para saber como publicar um formulário no Editor de formulário adaptável.

>[!ENDTABS]

* **Versão Preparada (para teste)**: a versão preparada exibe a versão não publicada e funcional do formulário para fins de teste. Use o seguinte formato de URL para visualizar o formulário antes que ele entre em vigor:

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`



* **Versão ao Vivo (formulário publicado)**:   A versão ao vivo exibe a versão publicada mais recentemente do formulário, acessível aos usuários finais. Use o seguinte formato de URL para acessar a versão publicada e em tempo real do formulário:

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  A estrutura do URL permanece a mesma para as versões preparadas e ativas. No entanto, o conteúdo exibido é diferente com base no contexto.

As capturas de tela abaixo comparam URLs de formulário preparadas e ativas e visualizações visuais para formulários criados usando modelos baseados em Edge Delivery Services e Componentes principais:

>[!BEGINTABS]
>[!TAB Acessando formulários criados com o Modelo baseado em Edge Delivery Services]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
    <thead>
    <tr>
      <th style="width: 20%;"><strong>Versão</strong></th>
      <th style="width: 80%;"><strong>Imagem</strong></th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td>Versão Preparada</td>
      <td><img src="/help/forms/assets/registration-form-staged-version.png" alt="Versão preparada do formulário de registro" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>Versão ao vivo</td>
      <td><img src="/help/forms/assets/registration-form-live-version.png" alt="Versão ao vivo do formulário de registro" style="width: 100%; height: auto;" /></td>
    </tr>
    </tbody>
  </table>

>[!TAB Acessando formulários criados com o Modelo baseado em Componente Principal]

<table border="1" style="width: 100%; border-collapse: collapse; text-align: left;">
  <thead>
    <tr>
      <th style="width: 20%;"><strong>Versão</strong></th>
      <th style="width: 80%;"><strong>Imagem</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Versão Preparada</td>
      <td><img src="/help/forms/assets/enrollment-form-staged-version.png" alt="Versão preparada do formulário de inscrição" style="width: 100%; height: auto;" /></td>
    </tr>
    <tr>
      <td>Versão ao vivo</td>
      <td><img src="/help/forms/assets/enrollment-form-live-version.png" alt="Versão ao vivo do formulário de inscrição" style="width: 100%; height: auto;" /></td>
    </tr>
  </tbody>
  </table>

>[!ENDTABS]

## Resolução de problemas

Está tendo problemas para carregar o formulário? Estes são alguns problemas comuns e como corrigi-los:

* **URL do formulário**: verifique se a URL do seu formulário não inclui a extensão &quot;.html&quot; no final. O Edge Deliver Service não exige essa extensão.

* **URL do Autor do AEM** L: verifique se a URL do Autor do AEM listada no arquivo `fstab.yaml` está formatada corretamente. Ele deve incluir os seguintes detalhes:

   * O proprietário correto do GitHub
   * O nome correto do repositório
   * A ramificação específica que você está usando para o Edge Delivery Services

## Começar a criar formulários

{{universal-editor-see-also}}

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.

### Managing a form

You can perform several operations on form using the AEM Forms user interface.

1. Login into your AEM Forms as a Cloud Service author instance.
1. Select **[!UICONTROL Adobe Experience Manager]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Forms & Documents]**.

1. Select a form and the toolbar displays the following operations you can perform on the selected form.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operation</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p>Edit</p> </td>
   <td><p>Opens the form in edit mode.<br /> <br /> </p> </td>
  </tr>
    <tr>
   <td><p>Properties</p> </td>
   <td><p>Provides options to modify the properties of the form.<br /> <br /> </p> </td>
  </tr>
  <td><p>Copy</p> </td>
   <td><p> Provides options to copy the form  and paste it at the desired location. <br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>Preview</p> </td>
   <td><p>Provides options to preview the form as HTML or perform a custom preview by merging data from an XML file with the form. <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Downloads the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Start Review/Manage Review</p> </td>
   <td><p>Allows initiating and managing a review of the selected form.<br /> <br /> </p> </td>
  </tr>
  <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publish / Unpublish</p> </td>
   <td><p>Publishes / unpublishes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Delete</p> </td>
   <td><p>Deletes the selected form.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Compare</p> </td>
   <td><p>Compares two different form for previewing purposes.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table> 


## How Edge Delivery Services Forms Work?

Users can author Edge Delivery Services Forms using document-based authoring tools such as Google Drive, SharePoint, or the Universal Editor (WYSIWYG authoring), while leveraging the basic styling, behaviour and components available in the GitHub repository. Once authored, Edge Delivery Services Forms can send data to any platform using the Forms Submission Service.

![How Edge Delivery Services Forms works](/help/edge/docs/forms/assets/eds-forms-working.png)

### Key components of Edge Delivery Services Forms

The key components of Edge Delivery Servies Forms are:

* **GitHub Repository**: The GitHub repository serves as a boilerplate for creating Edge Delivery Services Forms. The forms leverage basic styling and functionality from the repository and allow users to add customizations and custom components to the Edge Delivery Services Forms.

* **Form Authoring**: Edge Delivery Services Forms support two types of authoring: WYSIWYG and document-based authoring. Document-based authoring enables users to create forms using familiar tools like Google Docs and Microsoft Office. WYSIWYG authoring allows users to design forms visually using the Universal Editor, making it easy for non-technical users to create and manage forms. Universal Editor offers an intuitive form creation experience and provides access to numerous form capabilities.

* **Forms Submission Service**: The Forms Submission Service allows you to store data from forms submissions on any platform, such as OneDrive, SharePoint, or Google Sheets, making it easy to access and manage form data within your preferred system.-->
