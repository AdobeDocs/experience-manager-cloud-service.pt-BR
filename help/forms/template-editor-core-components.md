---
title: Como criar um modelo de formulário adaptável com os Componentes principais?
description: Crie modelos de formulário adaptável com base no componente principal para definir a estrutura básica e o conteúdo inicial usando o Editor de modelos.
feature: Adaptive Forms, Core Components
Keywords: form builder, build adaptive form template, adaptive form template core components, form template builder, build form template.
exl-id: c1c050d3-953e-4e56-a96b-d84f2ec05e5e
role: User, Developer
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 4%

---

# Criar um modelo de formulário adaptável com os Componentes principais {#adaptive-form-templates}

Ao criar um formulário, você adiciona campos e componentes para definir a estrutura do formulário, o conteúdo e as ações no editor. Você adiciona campos e componentes no `guideRootPanel` do contêiner de formulário. Com o Editor de modelos, você pode criar um modelo que contenha estrutura básica e conteúdo inicial que os autores possam usar para criar formulários.

Por exemplo, você deseja que todos os autores de formulários tenham determinadas caixas de texto, botões de navegação e um botão de envio em um formulário de inscrição. Você pode criar um modelo com os componentes que os autores podem usar para criar um formulário consistente com outros formulários de inscrição. Quando os autores usam o modelo para criar um Formulário adaptável, o novo formulário herda a estrutura, a estrutura e os componentes especificados no modelo. O Editor de modelos permite:

* Adicione componentes de cabeçalho e rodapé de um formulário na camada da estrutura.
* Forneça o conteúdo inicial para o formulário.
* Especifique um tema, Enviar ações.

<!--
You can download and install [!DNL AEM Forms] reference content package from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal to import reference themes and templates to your environment.
-->

## Pré-requisito

**Habilitar os Componentes principais adaptáveis do Forms para o seu ambiente**: quando você cria um programa, os Componentes principais adaptáveis do Forms já estão habilitados para o seu ambiente.Instale os componentes principais adaptáveis do Forms mais recentes para habilitar o ambiente do AEM Cloud Service.

>[!NOTE]
>
> Ao implantar o ambiente Forms as a Cloud Service com base no Arquétipo 45, os **modelos do Adaptive Forms (Componente principal)** e os temas baseados em componentes principais são adicionados ao seu ambiente.

## Trabalhar com modelo {#working-with-templates}

Você pode acessar o editor de modelos no menu Ferramentas navegando até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Modelos]**. Aqui, os modelos são organizados em pastas ativadas para modelos editáveis.

>[!NOTE]
>
> Você pode encontrar os modelos editáveis baseados nos componentes principais nas pastas específicas dos componentes principais.

O Experience Manager fornece uma pasta global para organizar modelos. No entanto, não está ativado por padrão. Você pode solicitar que o administrador ative a pasta global ou crie uma pasta para modelos. Para obter mais informações sobre como criar pastas, consulte [Pastas de Modelo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors).

## Criação de um modelo {#create-template}

Após criar uma pasta, abra-a e execute as seguintes etapas para criar um template:

1. Selecione **[!UICONTROL Criar]** dentro da pasta que você criou.
1. Na seção **[!UICONTROL Escolher um Tipo de Modelo]**, selecione o **[!UICONTROL modelo de Formulário Adaptável (Componente Principal)]** e selecione **[!UICONTROL Próximo]**.

1. Na seção **[!UICONTROL Detalhes do Modelo]**, forneça um **Título do Modelo** e selecione **[!UICONTROL Criar]**.
Você também pode fornecer uma descrição.

1. Selecione **[!UICONTROL Concluído]** para retornar ao console ou **[!UICONTROL Abrir]** para abrir o modelo no editor.

## Interface do editor de modelos {#template-editor-ui}

Ao abrir um modelo para edição, você pode ver os seguintes componentes do Editor do AEM:

* **Barra de ferramentas da página**
Contém as seguintes opções:

   * **Alternar Painel Lateral**: Permite mostrar ou ocultar a barra lateral.
   * **Informações da página**: permite especificar informações como hora de publicação/cancelamento de publicação, miniaturas, bibliotecas do lado do cliente, política da página e biblioteca do lado do cliente de design da página.
     <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **Seletor de modo:** permite alterar o modo. Você pode escolher o modo **[!UICONTROL Estrutura]**, **[!UICONTROL Conteúdo inicial]**, **[!UICONTROL Controle de layout]**. O modo Estrutura permite adicionar e personalizar o cabeçalho e o rodapé. O modo Conteúdo inicial permite personalizar o conteúdo do formulário.
   * **Visualizar:** permite que você visualize a aparência do modelo ao publicá-lo. Você pode usar o Seletor de camada e a Visualização para alternar entre os modos de edição e visualização.
* **Barra Lateral:** fornece os navegadores de Conteúdo, Propriedades, Assets e Componentes.
* **Barra de ferramentas do componente:** ao selecionar um componente, você verá uma barra de ferramentas que permite personalizar o componente.
* **Página**: a área onde você adiciona conteúdo para criar o modelo.

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

## Edição de um modelo {#editing-a-template}

Os diferentes modos para selecionar e editar o aspecto apropriado do modelo são:

* [Estrutura](#structure)
* [Conteúdo inicial](#initial-content)
* [Layout](#layout)

O seletor de camadas está disponível ao lado da opção Visualizar, no canto superior direito da tela.

### Estrutura {#structure}

Quando você seleciona a camada de estrutura no Editor de modelo, ela ajuda a predefinir o conteúdo que não pode ser alterado ao criar o Forms adaptável associado ao modelo.

<!-- you can see the layout containers above and below the Adaptive Form Container. Authors can use these layout containers for header and footer. -->


![Contêiner de layout na camada da estrutura](/help/forms/assets/header-layer-selector-core-component.png)

<!--

**A. Layout container for Header component**
Drag-drop the Adaptive Form Header component in the layout container above the Adaptive Form Container. After you add the component, you can specify its properties that let you add a logo and provide its title.
**B. Adaptive Form Container component**
Drag-drop the Adaptive Form components in the Adaptive Form Container. You can specify the design and arrangement of fields and components in the template editor. After you add the components, you can specify its properties.
**C. Layout container for Footer component**
Similarly, when you drag-drop the footer component in the layout container below the Adaptive Form Container, you can provide the copyright information and company details. 
You can add, edit, or customize the header and footer. Drag-drop the Adaptive Form Header and Footer component to customize the template. Drag-drop the Adaptive Form components in the Adaptive Form Container. You can specify the design and arrangement of fields and components in the template editor. 


Header and footer are added in the Initial Content layer.
-->

#### Bloquear/desbloquear componentes na camada da estrutura {#locking-unlocking-components-in-the-structure-layer}

Ao editar o modelo com a camada de estrutura selecionada, é possível desbloquear o cabeçalho e o rodapé do modelo. Se um componente estiver desbloqueado no modelo, os autores do formulário poderão editar o componente no Formulário adaptável que usa o modelo. Bloquear um componente impede que os autores do formulário o editem no Formulário adaptável. A opção Bloquear está disponível na barra de ferramentas do componente.

Por exemplo, você adiciona o componente de cabeçalho no modelo. Ao selecionar o componente, você pode ver uma opção de bloqueio na barra de ferramentas do componente. Normalmente, o cabeçalho inclui o nome da empresa e o logotipo, e você não deseja que os autores de formulários alterem o logotipo e o cabeçalho em um modelo. Em um formulário adaptável criado usando o modelo com o componente de cabeçalho bloqueado, os autores de formulário não podem alterar o logotipo e o nome da empresa.

>[!NOTE]
>
>Não é recomendado bloquear ou desbloquear a imagem ou o logotipo no componente de cabeçalho, individualmente. Você pode desbloquear o componente de cabeçalho.

### Conteúdo inicial {#initial-content}

Quando a opção Conteúdo inicial estiver selecionada, o Contêiner de formulário adaptável do modelo será aberto como um Formulário adaptável para edição. Ele permite criar um conteúdo predefinido que pode ser alterado ao criar o Forms adaptável associado ao modelo. Assim como a criação de um Formulário adaptável, você pode especificar configurações iniciais, como selecionar um tema e Enviar ações.

Os autores de formulários o usam como base para criar um formulário. A estrutura do fluxo de conteúdo é especificada na camada Conteúdo inicial do modelo. Para alternar para a edição do conteúdo inicial do modelo de formulário, antes de Visualizar na barra de ferramentas da página, selecione ![tela suspensa](assets/canvas-drop-down.png) **>** **[!UICONTROL Conteúdo inicial]**.

![Cabeçalho e rodapé adicionados à camada Conteúdo Inicial](assets/header-and-footer.png)

Na camada Conteúdo inicial, crie o modelo de Formulário adaptável que seus autores usam como base. A criação de um modelo é semelhante à criação de um formulário. As opções disponíveis na Barra lateral são usadas. A barra lateral fornece conteúdo, propriedades, ativos e componentes nos navegadores.

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>Ao selecionar Armazenar conteúdo ou Armazenar PDF como a Ação enviar, você obtém uma opção para especificar o Caminho de armazenamento. Se você especificar o caminho no modelo, todos os formulários criados a partir dele terão o mesmo caminho. Você pode especificar o caminho de armazenamento correto ou garantir que os autores do formulário o atualizem para impedir que os dados de cada formulário sejam armazenados no mesmo local.

### Layout {#layout}

Ao editar um modelo, é possível definir o layout, isso usa o layout responsivo padrão. O layout ajuda a gerenciar a largura de um componente com base na largura do dispositivo para facilitar um design responsivo de formulário adaptável.

![Contêiner de layout na camada da estrutura](/help/forms/assets/layout-template-core-component.png)

Consulte o artigo [noções básicas sobre layout responsivo](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/responsive-layout-feature-video-understand.html?lang=en) para obter mais informações.

## Habilitação do modelo {#enabling-the-template}

Ao criar um modelo, ele é adicionado como um rascunho. Ative o modelo para usá-lo na criação do Forms adaptável. Para ativar um modelo:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Modelos]** e abra a pasta na qual você criou o modelo.
O modelo criado está marcado como Rascunho.
1. Selecione o modelo e selecione **[!UICONTROL Habilitar]** na barra de ferramentas.
Ao criar um Formulário adaptável, você pode ver o modelo listado quando é solicitado a escolher um modelo.

## Importação ou exportação de um template {#importing-or-exporting-a-template}

Um formulário funciona com seu modelo. Ao baixar um Formulário adaptável criado usando um modelo personalizado, o modelo não é baixado. Quando você importa o formulário em uma instância do [!DNL AEM Forms] diferente, ele é importado sem seu modelo. Se um formulário for importado, mas seu template não estiver disponível, o formulário não será renderizado. Você pode empacotar o modelo personalizado do nó `/conf` em `https://<server>:<port>/crx/packmgr` e colocá-lo na porta na instância [!DNL AEM Forms] para onde deseja carregar o formulário. Você também pode [Criar um modelo usando o Arquétipo do AEM e implantá-lo na sua instância do Cloud Services](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites).

>[!NOTE]
>
> * Você também pode configurar o modelo [!UICONTROL Documento de registro] diretamente do Construtor de formulários adaptáveis ou do Construtor de modelos de formulários adaptáveis. Para obter mais informações, consulte [Gerar documento de registro para Forms adaptável](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).

## Associar um esquema do modelo de dados de formulário a um modelo {#associating-form-data-model-schema-in-template}

Os autores podem associar um [!UICONTROL Esquema de modelo de dados de formulário] a um modelo de formulário adaptável no editor de modelos. Ele permite que os autores selecionem um esquema no editor de modelos. Quando você associa um esquema a um modelo e um autor de formulário cria um formulário com base no modelo, o esquema é pré-selecionado para o formulário. Ele ajuda os autores de formulários a regular o uso do esquema e também economiza tempo para os autores de formulários. Para selecionar um esquema de modelo de dados de formulário no editor de modelo:

1. Selecione o **[!UICONTROL Navegador de Conteúdo]**, localizado no lado esquerdo.
1. Vá para o contêiner de formulário **[!UICONTROL Configuração]**.
1. Selecione **[!UICONTROL Modelo de Dados]**.
1. Escolha o modelo de dados de formulário (FDM) por meio do **[!UICONTROL Selecione Modelo de Dados de Formulário]** e salve a configuração.

![Associação-no-Forms-do-Modelo-de-Dados-de-Formulário](/help/forms/assets/select-form-data-model-img-core-component.png)

<!--

## Creating an Adaptive Form template with tabs and panels {#creating-an-adaptive-form-template-with-tabs-and-panels-nbs}

For example, you want to create a template with the following tabs:

* General Information
* Professional Information

You have added a logo, provided a title, and added a footer in the structure layer. Lock the header and footer to stop form authors from editing them when they use the template to create forms.

Change the layer from **Structure** to **Initial Content**, and start adding content to the form. To create a tabbed structure, add a child Panel in the guideRootPanel of the Adaptive Form container. To add a panel:

* You can add a panel by tapping the **[!UICONTROL +]** button when you select the **[!UICONTROL Drag components here]** option.

* You can drag-drop the panel component from the components browser in the sidebar.
* You can add child panel of the `guideRootPanel` from the component toolbar.

To create the General Information and Professional Information tabs, add two panels in the child panel of the `guideRootPanel`. Select the panels and select ![cmppr](assets/configure-icon.svg) to open the properties in the sidebar. Change the element names as `general-info` and `professional-info`, and titles as General Information and Professional Information respectively. In the sidebar, select content to open the content browser. In the Form Objects tab, select `guideRootPanel`. In the editor, the guideRootPanel is selected. Select ![cmppr](assets/configure-icon.svg) in the component toolbar to open its properties. In the Panel Layout field, select **[!UICONTROL Tabs on Top]** and select **[!UICONTROL Done]**. The tabbed template structure is applied.

### Adding content in tabs {#adding-content-in-tabs}

After you add panels and structure them as tabs, you can add fields inside the tabs. When you select a tab in the editor, you can see the **[!UICONTROL Drag components here]** option. You can drag-drop components such as text-boxes, list items, and buttons. You can drag-drop components from the components browser in the sidebar.

Each component has properties that enhance data capturing and manipulation. For example, you can enable the **[!UICONTROL Required field]** property of a component. Your authors can specify a message that your customers see when they skip filling a required field. Specify the message in **[!UICONTROL Required Field Message]** property.

In the example template, Name, Phone number, and Date of birth fields are added in the General Information tab. In the Professional Information tab, Currently employed, employment type, Educational qualification fields are added.

After you have added fields, you can add buttons such as Submit and Reset.
-->

### Adicionar propriedades personalizadas aos Componentes de formulário adaptável usando a política de modelo

As propriedades personalizadas permitem associar atributos personalizados (pares de chave e valor) a um componente principal de formulário adaptável usando o modelo de formulário. As propriedades personalizadas são refletidas na seção **[!UICONTROL properties]** da representação headless do componente. Isso permite criar um comportamento de formulário dinâmico que se adapta de acordo com os valores de atributos personalizados. Por exemplo, desenvolvedores(as) podem criar várias representações de um componente de formulário headless para plataformas móveis, de desktop ou da web, melhorando significativamente a experiência de usuário em uma grande variedade de dispositivos.

As etapas para adicionar propriedades personalizadas aos campos do componente principal do Formulário adaptável são:

1. [Adicionar um nome de grupo personalizado na política de um editor de modelo](#add-a-custom-group-name)
1. [Selecione um nome de grupo personalizado na caixa de diálogo de edição de um componente do Formulário adaptável](#select-a-custom-group-name)

#### Adicionar um nome de grupo personalizado na política do editor de modelo {#add-a-custom-group-name}

1. Vá para **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Modelos]**.
1. Selecione o modelo com base nos Componentes principais e abra-o em um modo de edição.
1. Clique no ícone **[!UICONTROL Política]** ![Política](/help/forms/assets/Smock_FeedManagement_18_N.svg) de um campo Componente principal do formulário adaptável no qual as propriedades personalizadas precisam ser definidas. A caixa de diálogo **[!UICONTROL Campo de Formulário Adaptável]** é exibida.
1. Selecione a guia **[!UICONTROL Propriedades Personalizadas]**.
1. Especifique o **[!UICONTROL Título da Política]** na seção **[!UICONTROL Política]**.
1. Especifique o **[!UICONTROL Nome do grupo]** e adicione o par de valor-chave associado a um grupo específico. O nome do grupo é visível para os autores do formulário na caixa de diálogo de edição de um componente. Se você selecionar o nome do grupo, cada par de valor-chave associado será aplicável a um componente.
1. Clique em **[Concluído]**.

![Adicionando o nome do grupo de propriedades personalizadas no editor de modelo](/help/forms/assets/custom-properties-core-component.png)

Quando você adiciona pelo menos um grupo de propriedades personalizadas usando a política de modelo, a guia **[!UICONTROL Avançado]** fica visível na caixa de diálogo Editar de um componente principal correspondente.

#### Selecione um nome de grupo personalizado na caixa de diálogo de edição de um componente principal {#select-a-custom-group-name}

1. Abra um Formulário adaptável em um modo de edição.
1. Selecione o componente cujas propriedades personalizadas foram definidas no editor de modelo e selecione ![settings_icon](assets/configure-icon.svg) para abrir a caixa de diálogo de edição do componente.
1. Selecione a guia **[!UICONTROL Avançado]**.
1. Selecione o nome do grupo de propriedades personalizadas no menu suspenso **[!UICONTROL Selecionar propriedade personalizada]**. Todos os nomes de grupos personalizados definidos são preenchidos automaticamente na lista suspensa.
1. Selecione **[!UICONTROL Concluído]** para salvar as propriedades.

![selecionar nome do grupo de propriedades personalizadas](/help/forms/assets/select-custom-properties-group-name.png)

>[!NOTE]
>
> * A caixa de seleção **[!UICONTROL Propriedades Personalizadas Adicionais]** permite adicionar dinamicamente propriedades personalizadas específicas do componente, além daquelas fornecidas na política de modelo. A propriedade personalizada do componente específico tem prioridade sobre a propriedade personalizada definida na política do modelo quando os valores do nome da chave correspondem.

## Criação de um formulário adaptável usando o modelo {#creating-an-adaptive-form-using-the-template}

Depois de criar e ativar um modelo, ele fica disponível no gerenciador de formulários quando você cria um Formulário adaptável. Para usar um modelo e criar um Formulário adaptável, consulte [Criação de um Formulário adaptável com base nos Componentes principais](/help/forms/creating-adaptive-form-core-components.md).
<!--
## Change display option of out of the box templates  {#change-display-option-of-out-of-the-box-templates}

You can create custom templates for Adaptive Forms to define basic structure and initial content. [!DNL AEM Forms] also provides a set of out of the box template for Adaptive Forms. You can choose to show or hide the templates.

Perform the following steps to show and hide templates:

1. Log in to [!DNL AEM Forms] author instance and navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   >[!NOTE]
   >
   >The URL of AEM web console is https://'[server]:[port]'/system/console/configMgr

1. Locate and open the **FormsManager Configuration** settings:

    * To show or hide out of the box Adaptive Forms template, check or uncheck the **Include Out of the box AF and AD Templates** option.
    * To show or hide out of the box Adaptive Form templates that were added in AEM 6.0 Forms or AEM 6.1 Forms releases but are now deprecated, check or uncheck the **Include AEM 6.0 AF Templates** option. If this option is checked, and you want it to take effect, it requires the **Include Out of the box AF and AD Templates** configuration to be enabled.

1. Click **Save**. The display options for the out of the box templates are changed. 

## Save an Adaptive Form as a template {#saving-adaptive-form-as-template}

You can also save an Adaptive Form as a template for future use. To save a Adaptive Form as a template:

1. Select an Adaptive Form to save it as a template.
1. Click **[!UICONTROL Save as Template]**. A dialog box appears.
1. Specify **[!UICONTROL Title]** (mandatory field), **[!UICONTROL Location]** (mandatory field) and **[!UICONTROL Description]** (optional field) for the template. 
1. Click **[!UICONTROL Create]**.

   ![Save as Form as Template](/help/forms/assets/saveformastemplate.png)



>[!NOTE]
>
>To use the same container policy as of the source Adaptive Form, it is recommended to save the template in the same folder as of the source Adaptive Form. In case, the template is saved in any other folder, than the created template uses a default container policy.
-->

## Práticas recomendadas {#best-practices}

* Crie modelos usando os componentes baseados nos Componentes principais, por exemplo, Texto de formulário adaptável, Contêiner de formulário adaptável e muito mais. Para obter informações sobre os Componentes principais adaptáveis do Forms, [clique aqui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR).
* Limitar o número de modelos para corresponder aos tipos de formulário fundamentalmente diferentes disponíveis nos sites
* Forneça a flexibilidade e os recursos de configuração necessários para seus componentes personalizados usados em um modelo.

<!--
## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Create an Adaptive Form (core components)](/help/forms/creating-adaptive-form-core-components.md)

-->

## Consulte também {#see-also}

{{see-also}}

* [Criar estilo ou temas para seus formulários](using-themes-in-core-components.md)
* [Criar um formulário adaptável (componentes principais)](/help/forms/creating-adaptive-form-core-components.md)

