---
title: Guia de início rápido para a criação de páginas
description: Um guia rápido e de alto nível para começar a criar conteúdo de página
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Quick Start Guide to Authoring Pages {#quick-guide-to-authoring-pages}

Este documento é um guia de início rápido de alto nível para as ações principais de criação de página no AEM. Este documento:

* Não se destina a uma cobertura abrangente.
* Fornece links para a documentação detalhada.

Para obter os detalhes completos sobre a criação com o AEM, consulte:

* [Conceitos de criação](/help/sites-cloud/authoring/getting-started/concepts.md)
* [Manuseio básico](/help/sites-cloud/authoring/getting-started/basic-handling.md)

## Algumas dicas rápidas {#a-few-quick-hints}

Antes de começar o guia de início rápido, veja uma pequena coleção de dicas gerais que você deve considerar, divididas entre as áreas do sistema de criação.

### No console Sites {#sites-console}

* Botão Criar

   * Este botão está disponível em vários consoles, as opções apresentadas são sensíveis ao contexto, por isso podem variar de acordo com o cenário.

* Reordenar páginas

   * This can be done in [List View](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view). The changes will be applied and be visible in other views.

### Criação de página {#page-authoring}

* Links de navegação

   * **Os links não estão disponíveis para navegação** quando você estiver no modo de **Edição**. Para navegar pelos links, é necessário [Visualizar a página](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) usando:

      * [Modo de visualização](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)
      * [Exibir como publicado](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)

* Versions are not started/created from the page editor. This is now done from the **Sites** console (via either **Create** or [Timeline](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) for a selected resource).

>[!NOTE]
>
>Há vários atalhos do teclado que podem facilitar a experiência de criação.
>
>* [Atalhos de teclado ao editar páginas](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
>* [Atalhos de teclado para os consoles](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)


### Encontrar a sua página {#finding-your-page}

Há vários aspectos para localizar uma página; você pode navegar e/ou pesquisar:

1. Abra o console **Sites** (usando a opção **Sites** na [Navegação global](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) - isso é acionado (menu suspenso) ao selecionar o link do Adobe Experience Manager (parte superior esquerda).

1. Navegue para baixo na árvore, tocando/clicando na página apropriada. A forma como os recursos da página são apresentados depende da exibição usada ([Cartão, Lista ou Coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)):

   ![Exibir lista suspensa de seleção](/help/sites-cloud/authoring/assets/views.png)

1. Navigate up the tree using [the breadcrumb in the header](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header), which allows you to return to the selected location:

   ![Lista suspensa](/help/sites-cloud/authoring/assets/breadcrumb.png)

1. Você também pode [Pesquisar](/help/sites-cloud/authoring/getting-started/search.md) por uma página. Selecione sua página nos resultados mostrados.

   ![Campo de pesquisa](/help/sites-cloud/authoring/assets/search.png)

### Criar uma nova página {#creating-a-new-page}

Para [criar uma nova página](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page):

1. [Navegue até o local](#finding-your-page) onde deseja criar a nova página.
1. Use o ícone **Criar** e selecione **Página** na lista:

   ![Botão Criar](/help/sites-cloud/authoring/assets/create.png)

1. Isso abrirá o assistente que vai guiá-lo na coleta das informações necessárias ao [criar sua nova página](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page). Siga as instruções na tela.

### Selecionar sua página para mais ações {#selecting-your-page-for-further-action}

Você pode selecionar uma página para executar ações. A seleção de uma página atualizará automaticamente a barra de ferramentas para que as ações pertinentes a esse recurso sejam mostradas.

A forma de selecionar uma página dependerá da exibição usada no console:

1. Visualização de coluna:

   * Toque/clique na miniatura do recurso desejado - a miniatura será sobreposta com uma marca de verificação para mostrar que a opção foi selecionada.

1. Exibição de lista:

   * Toque/clique na miniatura do recurso desejado - a miniatura será sobreposta com uma marca de verificação para mostrar que a opção foi selecionada.

1. Exibição de cartão:

   * Enter selection mode by [selecting the required resource](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources). A forma como você faz isso depende do seu dispositivo:

      * Em um dispositivo móvel: toque e segure o cartão
      * Em um dispositivo de desktop: use a ação [](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) rápida representada pelo ícone de marca de verificação:
   * O cartão será sobreposto como uma marca de verificação para mostrar que a página foi selecionada.
   ![Cartão exemplo](/help/sites-cloud/authoring/assets/card.png)

### Ações rápidas (apenas a exibição de cartão/área de trabalho) {#quick-actions-card-view-desktop-only}

As [ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) estão disponíveis:

1. [Navegue até a página](#finding-your-page) que deseja realizar a ação.
1. Passe o ponteiro do mouse sobre o cartão que representa o recurso desejado. As ações rápidas serão exibidas:

   ![Ações do cartão](/help/sites-cloud/authoring/assets/card-actions.png)

### Editar o seu conteúdo da página {#editing-your-page-content}

Para editar sua página:

1. [Navegue até a página](#finding-your-page) que deseja editar.
1. [Abra a página para edição](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing) usando o ícone Editar (lápis):

   ![Botão Editar](/help/sites-cloud/authoring/assets/edit.png)

   Essa opção pode ser acessada com:

   * [Ações rápidas (somente exibição de cartão/área de trabalho)](#quick-actions-card-view-desktop-only) para o recurso apropriado.
   * A barra de ferramenta quando a sua [página é selecionada](#selecting-your-page-for-further-action).

1. Quando o editor for aberto, é possível:

   * [Adicione um novo componente à sua página](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component) :

      * Abrir o painel lateral
      * Selecting the components tab (the [components browser](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser))
      * Arrastar o componente necessário para a página.
      O painel lateral pode ser aberto (ou fechado) com:

      ![Botão de alternância do painel lateral](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

   * [Edite o conteúdo de um componente existente](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) na página:

      * Abra a barra de ferramentas do componente com um toque ou clique. Use o ícone **Editar** (lápis) para abrir a caixa de diálogo.
      * Abra o editor no local para o componente com a opção de tocar e segurar ou dê um clique duplo lento. As ações disponíveis serão exibidas (para alguns componentes isso será uma seleção limitada).
      * Para visualizar todas as ações disponíveis entre no modo de tela cheia usando:

         ![Botão de tela cheia](/help/sites-cloud/authoring/assets/full-screen.png)
   * [Configurar as propriedades de um componente existente](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-edit-dialog)

      * Abra a barra de ferramentas do componente com um toque ou clique. Use o ícone **Configurar** (chave) para abrir a caixa de diálogo.
   * [Mover um componente](/help/sites-cloud/authoring/fundamentals/editing-content.md#moving-a-component):

      * Arraste o componente desejado para sua nova localização.
      * Open the component toolbar with either tap or click. Use the **Cut** then **Paste** icons where required.
   * [Copiar (e Colar)](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) um componente:

      * Open the component toolbar with either tap or click. Use the **Copy** then **Paste** icons as required.
   >[!NOTE]
   >
   >Você pode **Colar** os componentes na mesma página ou em uma diferente. Ao colar em uma página diferente que já foi aberta antes da operação de cortar/copiar, essa página precisará de uma atualização. 

   * [Excluir](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) um componente:

      * Open the component toolbar with either tap or click, then use the **Delete** icon.
   * [Adicionar anotações](/help/sites-cloud/authoring/fundamentals/annotations.md#annotations) à página:

      * Selecione o modo **Anotar** (ícone de balão). Adicione anotações usando o ícone **Adicionar anotação** (mais). Saia do modo de anotação usando o X na parte superior direita.

         ![Botão Anotações](/help/sites-cloud/authoring/assets/annotations.png)
   * [Visualizar uma página](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) (para verificar como ela será exibida no ambiente de publicação)

      * Selecione **Visualização** na barra de ferramentas.
   * Retornar para o modo de edição (ou selecionar outro modo), usando o seletor suspenso **Editar**.
   >[!NOTE]
   >
   >Para navegar usando os links no conteúdo, você deve usar o [Modo de visualização](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode).

### Editar as propriedades da página {#editing-the-page-properties}

Existem dois métodos (principais) [para editar as propriedades da página](/help/sites-cloud/authoring/fundamentals/page-properties.md):

* No console **Sites**:

   1. [Navegue até a página](#finding-your-page) que deseja publicar.
   1. Selecione o ícone **Propriedade** por meio de:

      * [Ações rápidas (apenas exibição de cartão/área de trabalho)](#quick-actions-card-view-desktop-only) para o recurso apropriado.
      * A barra de ferramenta quando a sua [página é selecionada](#selecting-your-page-for-further-action).
      ![Botão Propriedades](/help/sites-cloud/authoring/assets/properties.png)

   1. As propriedades da página serão exibidas. É possível fazer atualizações conforme necessário, em seguida, usar a opção Salvar para continuar


* Ao [editar a sua página](#editing-your-page-content):

   1. Abra o menu **Informações da página**.
   1. Selecione **Abrir propriedades** para abrir a caixa de diálogo para editar as propriedades.

      ![Botão Informações da página](/help/sites-cloud/authoring/assets/page-information.png)

### Publicar sua página (ou desfazer a publicação) {#publishing-your-page-or-unpublishing}

Existem dois métodos principais [para publicar a sua página](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) (e também de desfazer a publicação):

* No console **Sites**:

   1. [Navegue até a página](#finding-your-page) que deseja publicar.
   1. Select the **Quick Publish** icon from either:

      * [Ações rápidas (apenas exibição de cartão/área de trabalho)](#quick-actions-card-view-desktop-only) para o recurso apropriado.
      * A barra de ferramentas quando a sua [página é selecionada](#selecting-your-page-for-further-action) (também fornece o acesso à opção [Publicar mais tarde](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)).
      ![Botão Publicação rápida](/help/sites-cloud/authoring/assets/quick-publish.png)


* Ao [editar a sua página](#editing-your-page-content):

   1. Abra o menu **Informações da página**.
   1. Selecione **Publicar página**. 

* O cancelamento da publicação de uma página no console só pode ser feito por meio da opção **Gerenciar publicação**, que está disponível somente na barra de ferramentas (não por meio das ações rápidas).

   ![Botão Gerenciar publicação](/help/sites-cloud/authoring/assets/manage-publication.png)

   A opção **Cancelar publicação da página** ainda está disponível por meio do menu **Informações da página** no editor.

   Consulte [Publicação de páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) para obter mais informações.

### Mover, copiar e colar ou excluir sua página {#move-copy-and-paste-or-delete-your-page}

Essas ações podem ser acionadas por:

1. [Navegue até a página](#finding-your-page) que deseja mover, copiar e colar ou excluir.
1. Selecione o ícone para copiar (e, em seguida, colar), mover ou excluir, conforme desejado, usando:

   * As [Ações rápidas (apenas a exibição de cartão/área de trabalho) ](#quick-actions-card-view-desktop-only) do recurso desejado.
   * A barra de ferramenta quando a sua [página é selecionada](#selecting-your-page-for-further-action).
   Em seguida, depende da sua ação:

   * Copiar:

      * Em seguida, será necessário navegar até o novo local e colar.
   * Mover:

      * Isso abrirá o assistente para coletar as informações necessárias para mover a página. Siga as instruções na tela.
   * Exclua:

      * Você receberá uma solicitação para confirmar a ação.
   >[!NOTE]
   >
   >A opção Excluir não está disponível como uma Ação rápida.

### Bloquear sua página (em seguida, desbloquear) {#locking-your-page-then-unlocking}

[Bloquear uma página](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) impede que outros autores trabalhem nela junto com você. O ícone/botão Bloquear (e Desbloquear) pode ser encontrado dentre as seguintes opções:

* A barra de ferramenta quando a sua [página é selecionada](#selecting-your-page-for-further-action).
* O [menu suspenso Informações da página](#editing-the-page-properties) ao editar uma página.
* A barra de ferramentas da página ao editar uma página (quando a página estiver bloqueada)

Por exemplo, o ícone de bloqueio tem a seguinte aparência:

![Botão Bloquear](/help/sites-cloud/authoring/assets/lock.png)

### Acessar as referências da página {#accessing-page-references}

[O acesso rápido às referências ](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) para/de uma página estão disponíveis no Trilho de referências.

1. Selecione a **Referências** usando o ícone da barra de ferramentas (antes ou depois de [selecionar a página](#selecting-your-page-for-further-action)): 

   ![Opção de exibição Referências](/help/sites-cloud/authoring/assets/references.png)

   Uma lista de tipos de referência será exibida:

   ![Exibição de referências](/help/sites-cloud/authoring/assets/references-list.png)

1. Toque/clique no tipo de referência desejado para mostrar mais detalhes e (conforme o caso) realizar novas ações.

### Criar uma versão da sua página {#creating-a-version-of-your-page}

Para criar uma [versão](/help/sites-cloud/authoring/features/page-versions.md) da página:

1. Para abrir o painel Linha do tempo, selecione **[Linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)**usando o ícone da barra de ferramentas (antes ou depois de[selecionar a página](#selecting-your-page-for-further-action)):

   ![Opção de exibição Linha do tempo](/help/sites-cloud/authoring/assets/timeline.png)

1. Tap/click on the ellipsis at the bottom right of the Timeline column to reveal extra buttons, including **Save as Version**.

   ![Exibição da linha do tempo](/help/sites-cloud/authoring/assets/timeline-view.png)

1. Selecione **Salvar como versão**, em seguida, **Criar**.

### Restaurar/comparar uma versão da sua página {#restoring-comparing-a-version-of-your-page}

O mesmo mecanismo básico é usado ao restaurar e/ou comparar as versões da sua página:

1. Selecione a **[Linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)**usando o ícone da barra de ferramentas (antes ou depois de[selecionar a página](#selecting-your-page-for-further-action)):

   ![Opção de exibição Linha do tempo](/help/sites-cloud/authoring/assets/timeline.png)

   Se uma versão da sua página já foi salva, ela será listada na Linha do tempo.

1. Toque/clique na versão que você deseja restaurar - essa opção exibirá botões de ação adicionais:

   * **Reverter para essa versão**

      * A versão será restaurada.
   * **Mostrar diferenças**

      * A página será aberta com as diferenças (entre as duas versões) destacadas.
