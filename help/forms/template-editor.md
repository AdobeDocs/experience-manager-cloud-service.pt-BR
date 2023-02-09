---
title: Como criar um modelo de formulário adaptável?
description: Crie modelos de formulário adaptável para definir a estrutura básica e o conteúdo inicial usando o Editor de modelos.
exl-id: a882cba2-c621-4ff7-a972-c504641b5639
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 1%

---

# Criar um modelo de formulário adaptável {#adaptive-form-templates}

Ao criar um formulário, você adiciona campos e componentes para definir a estrutura, o conteúdo e as ações do formulário no editor. Você adiciona campos e componentes na `guideRootPanel` do contêiner de formulário. Com o Editor de modelo, é possível criar um modelo que contenha a estrutura básica e o conteúdo inicial que os autores podem usar para criar formulários.

Por exemplo, você deseja que todos os autores de formulários tenham determinadas caixas de texto, botões de navegação e um botão Enviar em um formulário de inscrição. É possível criar um modelo com os componentes que os autores podem usar para criar um formulário consistente com outros formulários de inscrição. Quando os autores usam o modelo para criar um formulário adaptável, o novo formulário herda a estrutura e os componentes especificados no modelo. O Editor de modelos permite:

* Adicione componentes de cabeçalho e rodapé de um formulário na camada de estrutura.
* Forneça o conteúdo inicial do formulário.
* Especifique um tema, Enviar ações.

Você pode baixar e instalar [!DNL AEM Forms] pacote de conteúdo de referência de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) portal para importar temas e modelos de referência para o seu ambiente.

## Trabalhar com modelos {#working-with-templates}

Você pode acessar o editor de modelos no menu Ferramentas navegando até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Modelos]**. Aqui, os modelos são organizados em pastas habilitadas para modelos editáveis.

O Experience Manager fornece uma pasta global para organizar templates. No entanto, não está ativado por padrão. Você pode solicitar ao Administrador que ative a pasta global ou crie uma pasta para modelos. Para obter mais informações sobre como criar pastas, consulte [Pastas de modelo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors).

### Criação de um modelo {#create-template}

Depois de criar uma pasta, abra-a e execute as seguintes etapas para criar um template:

1. Toque **[!UICONTROL Criar]** na pasta que você criou.
1. Na seção Selecionar um tipo de modelo , selecione **[!UICONTROL Modelo de formulário adaptável]** e tocar **[!UICONTROL Próximo]**.

1. Na seção Detalhes do modelo , forneça um Título de modelo e toque em **[!UICONTROL Criar]**.
Você também pode fornecer uma descrição.

1. Toque **[!UICONTROL Concluído]** para retornar ao console ou toque em **[!UICONTROL Abrir]** para abrir o template no editor.

### Interface do usuário do editor de modelos {#template-editor-ui}

Ao abrir um modelo para edição, você pode ver os seguintes componentes do Editor de AEM:

* **Barra de ferramentas da página**
Contém as seguintes opções:

   * **Alternar painel lateral**: Permite mostrar ou ocultar a barra lateral.
   * **Informações da página**: Permite que você especifique informações como o tempo de publicação/cancelamento de publicação, miniaturas, bibliotecas do lado do cliente, política de página e biblioteca do lado do cliente de design de página.

   <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **Seletor de modo:** Permite alterar o modo.
Você pode escolher **[!UICONTROL Estrutura]** modo, **[!UICONTROL Conteúdo inicial]**, **[!UICONTROL Controle de layout]** modo. O modo Estrutura permite adicionar e personalizar o cabeçalho e o rodapé. O modo Conteúdo inicial permite personalizar o conteúdo do formulário.
   * **Visualizar:** Permite que você visualize a aparência do modelo ao publicá-lo. Você pode usar o Seletor de camada e a Visualização para alternar os modos de edição e visualização.
* **Barra lateral:** Fornece os navegadores de Conteúdo, Propriedades, Ativos e Componentes.
* **Barra de ferramentas do componente:** Ao selecionar um componente, você verá uma barra de ferramentas que permite personalizar o componente.
* **Página**: A área onde você adiciona conteúdo para criar o modelo.

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

### Edição de um modelo {#editing-a-template}

Um modelo de Formulário adaptável é criado usando duas camadas:

* Estrutura
* Conteúdo inicial

O seletor de camada está disponível ao lado da opção Visualização no canto superior direito da tela.

### Estrutura {#structure}

Ao selecionar a camada de estrutura no Editor de modelo, é possível ver os contêineres de layout acima e abaixo do Contêiner de formulário adaptável. Os autores podem usar esses contêineres de layout para cabeçalho e rodapé. Você pode adicionar, editar ou personalizar o cabeçalho e o rodapé. Arraste e solte o componente Cabeçalho do formulário adaptável no contêiner de layout acima do Contêiner do formulário adaptável para personalizar o cabeçalho do modelo. Arraste e solte o componente Rodapé do formulário adaptável no contêiner de layout abaixo do Contêiner de formulário adaptável para personalizar o rodapé do modelo.

![Contêiner de layout na camada de estrutura](assets/header-layer-selector.png)

Contêineres de layout na camada de estrutura

**A.** Contêiner de layout para o componente Cabeçalho **B.** Contêiner de layout para o componente Rodapé

Arraste e solte o componente Cabeçalho do formulário adaptável no contêiner de layout acima do Contêiner do formulário adaptável. Após adicionar o componente, é possível especificar suas propriedades que permitem adicionar um logotipo e fornecer seu título.

Da mesma forma, ao arrastar e soltar o componente de rodapé no contêiner de layout abaixo do Contêiner de formulário adaptável, é possível fornecer as informações de direitos autorais e os detalhes da empresa.

![Cabeçalho e rodapé adicionados na camada Estrutura](assets/header-and-footer.png)

Cabeçalho e rodapé adicionados na camada Estrutura

#### Bloquear/desbloquear componentes na camada de estrutura {#locking-unlocking-components-in-the-structure-layer}

Ao editar o modelo com a camada de estrutura selecionada, é possível desbloquear o cabeçalho e o rodapé do modelo. Se um componente estiver desbloqueado no modelo, os autores de formulário poderão editar o componente no Formulário adaptável que usa o modelo. Bloquear um componente impede que os autores de formulários o editem no Formulário adaptável. A opção Bloquear está disponível na barra de ferramentas do componente.

Por exemplo, você adiciona o componente de cabeçalho no modelo. Ao selecionar o componente, você pode ver uma opção de bloqueio na barra de ferramentas do componente. Normalmente, o cabeçalho inclui o nome e o logotipo da empresa e você não deseja que os autores de formulários alterem o logotipo e o cabeçalho em um modelo. Em um formulário adaptável criado usando o modelo com o componente de cabeçalho bloqueado, os autores de formulário não podem alterar o logotipo e o nome da empresa.

>[!NOTE]
>
>Bloquear ou desbloquear imagem ou logotipo no componente de cabeçalho, individualmente, não é recomendado. Você pode desbloquear o componente de cabeçalho.

### Conteúdo inicial {#initial-content}

Quando a opção Conteúdo inicial é selecionada, o Contêiner de formulário adaptável do modelo é aberto como um Formulário adaptável para edição. Assim como a criação de um formulário adaptável, você pode especificar as configurações iniciais, como selecionar um tema e enviar ações.

Os autores de formulários o usam como base para criar um formulário. A estrutura do fluxo de conteúdo é especificada na camada Conteúdo inicial do modelo. Para alternar para a edição do conteúdo inicial do modelo de formulário, antes de Visualizar na barra de ferramentas da página, toque em ![lista suspensa de tela](assets/canvas-drop-down.png) **>** **[!UICONTROL Conteúdo inicial]**.


Na camada Conteúdo inicial , crie o modelo de Formulário adaptável usado pelos autores como base. A criação de um modelo é semelhante à criação de um formulário. Você usa as opções disponíveis na Barra lateral. A barra lateral fornece navegadores de conteúdo, propriedades, ativos e componentes.

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>Ao selecionar Armazenar conteúdo ou Armazenar PDF como a Ação de envio, você obtém uma opção para especificar o Caminho de armazenamento. Se você especificar o caminho no modelo, todos os formulários criados a partir dele terão o mesmo caminho. Você pode especificar o caminho de armazenamento correto ou garantir que os autores de formulários o atualizem para impedir que os dados de cada formulário sejam armazenados no mesmo local.

#### Criação de um modelo de formulário adaptável com guias e painéis {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Por exemplo, você deseja criar um modelo com as seguintes guias:

* Informações gerais
* Informações profissionais

Você adicionou um logotipo, forneceu um título e adicionou um rodapé na camada da estrutura. Bloqueie o cabeçalho e o rodapé para impedir que os autores de formulários os editem quando usam o modelo para criar formulários.

Altere a camada de Estrutura para Conteúdo inicial e comece a adicionar conteúdo ao formulário. Para criar uma estrutura com guias, adicione um Painel filho no guia Painel raiz do contêiner de Formulário adaptável. Para adicionar um painel:

* Você pode adicionar um painel tocando no botão **[!UICONTROL +]** ao selecionar o botão **[!UICONTROL Arraste componentes aqui]** opção.

* Você pode arrastar e soltar o componente do painel do navegador de componentes na barra lateral.
* Você pode adicionar o painel filho da `guideRootPanel` na barra de ferramentas do componente.

Para criar as guias Informações gerais e Informações profissionais , adicione dois painéis no painel filho da `guideRootPanel`. Selecione os painéis e toque em ![cmppr](assets/configure-icon.svg) para abrir as propriedades na barra lateral. Altere os nomes dos elementos como `general-info` e `professional-info`e títulos como Informações gerais e Informações profissionais, respectivamente. Na barra lateral, toque em conteúdo para abrir o navegador de conteúdo. Na guia Objetos de formulário , selecione `guideRootPanel`. No editor, o guideRootPanel é selecionado. Toque ![cmppr](assets/configure-icon.svg) na barra de ferramentas do componente para abrir suas propriedades. No campo Layout do painel , selecione **[!UICONTROL Guias em cima]** e tocar **[!UICONTROL Concluído]**. A estrutura do modelo com guias é aplicada.

#### Adição de conteúdo em guias {#adding-content-in-tabs}

Depois de adicionar painéis e estruturá-los como guias, é possível adicionar campos dentro das guias. Ao selecionar uma guia no editor, é possível ver a variável **[!UICONTROL Arraste componentes aqui]** opção. Você pode arrastar e soltar componentes como caixas de texto, itens de lista e botões. Você pode arrastar e soltar componentes do navegador de componentes na barra lateral.

Cada componente tem propriedades que aprimoram a captura e a manipulação de dados. Por exemplo, é possível ativar a variável **[!UICONTROL Campo obrigatório]** de um componente. Seus autores podem especificar uma mensagem que seus clientes veem ao ignorar o preenchimento de um campo obrigatório. Especifique a mensagem em **[!UICONTROL Mensagem de campo necessária]** propriedade.

No modelo de exemplo, os campos Nome, Número de telefone e Data de nascimento são adicionados na guia Informações gerais . Na guia Informações profissionais , são adicionados o tipo de emprego atualmente empregado, os campos de qualificação educacional .

Depois de adicionar campos, é possível adicionar botões, como Enviar e Redefinir.

### Ativação do template {#enabling-the-template}

Ao criar um modelo, ele é adicionado como rascunho. Ative o modelo para usá-lo na criação do Adaptive Forms. Para ativar um template:

1. Navegar para **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Modelos]** e abra a pasta na qual você criou o template.

1. O modelo criado é marcado como Rascunho.
1. Selecione o modelo e toque em **[!UICONTROL Habilitar]** na barra de ferramentas.
Ao criar um formulário adaptável, você pode ver o modelo listado quando for solicitado a escolher um modelo.

## Importação ou exportação de um template {#importing-or-exporting-a-template}

Um formulário funciona com seu modelo. Quando você faz o download de um formulário adaptável criado usando um modelo personalizado, o modelo não é baixado. Ao importar o formulário em um [!DNL AEM Forms] , ele é importado sem seu template. Se um formulário for importado, mas seu modelo não estiver disponível, o formulário não será renderizado. Você pode empacotar o modelo personalizado de `/conf` nó no `https://<server>:<port>/crx/packmgr`e importe-o no [!DNL AEM Forms] instância em que deseja fazer upload do formulário. Você também pode [Crie um modelo usando o AEM Arqueype e implante-o na sua instância do Cloud Services](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites).

>[!NOTE]
>
> * Você pode associar um [!UICONTROL Esquema do modelo de dados de formulário] para um modelo de Formulário adaptável em um editor de modelos. Consulte [Criação de um formulário adaptável](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model) para obter mais informações.
> * Você também pode configurar o [!UICONTROL Documento de registro] diretamente do editor de formulário adaptável ou do editor de modelo de formulário adaptável. Para obter mais informações, consulte [Gerar documento de registro para Forms adaptável](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform).



## Criação de um formulário adaptável usando o modelo {#creating-an-adaptive-form-using-the-template}

Depois de criar e ativar um modelo, ele estará disponível no gerenciador de formulários ao criar um Formulário adaptável. Para usar um modelo e criar um formulário adaptável, consulte [Criação de um formulário adaptável](creating-adaptive-form.md).


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
    * To show or hide out of the box Adaptive Form templates that were added in AEM 6.0 Forms or AEM 6.1 Forms releases but are now deprecated, check or uncheck the **Include AEM 6.0 AF Templates** option. If this option is checked, in order to take effect, it requires the **Include Out of the box AF and AD Templates** configuration to be enabled.

1. Click **Save**. The display options for the out of the box templates are changed. -->

## Salvar um formulário adaptável como modelo {#saving-adaptive-form-as-template}

Também é possível salvar um formulário adaptável como um modelo para uso futuro. Para salvar um formulário adaptável como um modelo:

1. Selecione um formulário adaptável para salvá-lo como um modelo.
1. Clique em **[!UICONTROL Salvar como modelo]**. Uma caixa de diálogo é exibida.
1. Especificar **[!UICONTROL Título]** (campo obrigatório), **[!UICONTROL Localização]** (campo obrigatório) e **[!UICONTROL Descrição]** (campo opcional) para o modelo.
1. Clique em **[!UICONTROL Criar]**.

   ![Salvar como formulário como modelo](/help/forms/assets/saveformastemplate.png)



>[!NOTE]
>
>Para usar a mesma política de contêiner do Formulário adaptativo de origem, é recomendável salvar o modelo na mesma pasta do Formulário adaptável de origem. Nesse caso, o modelo é salvo em qualquer outra pasta, diferente do modelo criado, e usa uma política de contêiner padrão.

## Recomendações {#recommendations}

* Ao modificar as propriedades do formulário no editor de modelo, não use a propriedade BindReference.
* Se quiser adicionar um ponto de interrupção, crie-o ao criar um modelo de Formulário adaptável.
Para obter mais informações sobre pontos de interrupção, consulte [Layout responsivo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/responsive-layout.html#authoring).
