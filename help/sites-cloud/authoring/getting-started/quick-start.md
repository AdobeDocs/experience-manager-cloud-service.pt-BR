---
title: Guia de início rápido para a criação de páginas
description: Um guia rápido de alto nível para começar a criar conteúdo de página
exl-id: d37c9b61-7382-4bf6-8b90-59726b871264
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 84%

---


# Guia de início rápido para a criação de páginas {#quick-guide-to-authoring-pages}

Este documento é um guia de início rápido de alto nível para as ações principais de criação de página no AEM. Este documento:

* Não é destinado a uma abordagem ampla.
* Fornece links para a documentação detalhada.

Para obter os detalhes completos sobre a criação com o AEM, consulte:

* [Conceitos de criação](/help/sites-cloud/authoring/getting-started/concepts.md)
* [Manuseio básico](/help/sites-cloud/authoring/getting-started/basic-handling.md)

{{edge-delivery-authoring}}

## Algumas dicas rápidas {#a-few-quick-hints}

Antes de começar o guia de início rápido, veja uma pequena coleção de dicas gerais que você deve considerar, dividida entre as áreas do sistema de criação.

### No console Sites {#sites-console}

* Botão Criar

   * Este botão está disponível em vários consoles, as opções apresentadas são sensíveis ao contexto, por isso podem variar de acordo com o cenário.

* Reordenação de páginas

   * Isso pode ser feito na [Exibição de lista](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view). As alterações são aplicadas e visíveis em outras exibições.

### Criação de página {#page-authoring}

* Links de navegação

   * **Os links não estão disponíveis para navegação** quando você estiver em modo **Editar**. Para navegar com links, é necessário [visualizar a página](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) usando:

      * [Modo de visualização](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode)
      * [Exibir como publicado](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)

* As versões não são iniciadas/criadas pelo editor de página. Agora isso é feito no console **Sites** (por meio da opção **Criar** ou da [Linha do Tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) de um recurso selecionado).

>[!NOTE]
>
>Há vários atalhos de teclado que podem facilitar a experiência de criação.
>
>* [Atalhos de teclado ao editar páginas](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
>* [Atalhos de teclado para Consoles](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

### Encontrar a sua página {#finding-your-page}

Há vários aspectos para localizar uma página. Você pode navegar e/ou pesquisar:

1. Abra o console do **Sites** (usando a opção **Sites** no painel de [Navegação global](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation)) - isso é acionado (menu suspenso) ao selecionar o link do Adobe Experience Manager (parte superior esquerda).

1. Navegue para baixo na árvore, tocando/clicando na página apropriada. A forma como os recursos da página são apresentados depende da exibição usada ([Cartão, Lista ou Coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)):

   ![Exibir lista suspensa de seleção](/help/sites-cloud/authoring/assets/views.png)

1. Navegue até a árvore usando [a navegação estrutural no cabeçalho](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header), que permite retornar ao local selecionado:

   ![Lista suspensa de navegação estrutural](/help/sites-cloud/authoring/assets/breadcrumb.png)

1. Você também pode [Pesquisar](/help/sites-cloud/authoring/getting-started/search.md) por uma página. É possível selecionar sua página a partir dos resultados mostrados.

   ![Campo Pesquisa](/help/sites-cloud/authoring/assets/search.png)

### Criar uma nova página {#creating-a-new-page}

Para [criar uma página](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page):

1. [Navegue até o local onde deseja criar a nova página.](#finding-your-page)
1. Use o ícone **Criar** e selecione **Página** na lista:

   ![Botão Criar](/help/sites-cloud/authoring/assets/create.png)

1. Isso abrirá o assistente que guiará você pela coleta das informações necessárias ao [criar sua nova página](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page). Siga as instruções na tela.

### Selecionar sua página para mais ações   {#selecting-your-page-for-further-action}

Você pode selecionar uma página para poder agir nela. Selecionar uma página atualizará automaticamente a barra de ferramentas para que as ações relevantes para esse recurso sejam exibidas.

Como selecionar uma página depende da exibição usada no console:

1. Exibição de coluna:

   * Selecione a miniatura do recurso desejado - a miniatura é sobreposta com uma marca de verificação para mostrar que ela foi selecionada.

1. Exibição de lista:

   * Selecione a miniatura do recurso desejado - a miniatura é sobreposta com uma marca de verificação para mostrar que ela foi selecionada.

1. Exibição de cartão:

   * Entre no modo de seleção, [selecionando o recurso desejado](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources). A forma como você faz isso depende do dispositivo:

      * Em um dispositivo móvel: toque e segure o cartão
      * Em um dispositivo de desktop: use a [ação rápida](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) representada pelo ícone de marca de verificação:

   * O cartão será sobreposto com uma marca de verificação para mostrar que a página foi selecionada.

   ![Exemplo de cartão](/help/sites-cloud/authoring/assets/card.png)

### Ações rápidas (apenas a exibição de cartão/desktop) {#quick-actions-card-view-desktop-only}

As [ações rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) estão disponíveis:

1. [Navegue até a página](#finding-your-page) você deseja agir.
1. Passe o mouse sobre o cartão que representa o recurso desejado. As ações rápidas serão exibidas:

   ![Ações do cartão](/help/sites-cloud/authoring/assets/card-actions.png)

### Editar o seu conteúdo da página {#editing-your-page-content}

Para editar sua página:

1. [Navegue até a página](#finding-your-page) que deseja editar.
1. [Abra a página para edição](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing) usando o ícone Editar (lápis):

   ![Botão Editar](/help/sites-cloud/authoring/assets/edit.png)

   Essa opção pode ser acessada com:

   * As [Ações rápidas (apenas a exibição de cartão/área de trabalho)](#quick-actions-card-view-desktop-only) do recurso adequado.
   * A barra de ferramenta quando a sua [página é selecionada](#selecting-your-page-for-further-action).

1. Quando o editor for aberto, será possível:

   * [Adicionar um novo componente para a página](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component) ao:

      * Abrir o painel lateral
      * Selecionar a guia componentes (o [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser))
      * Arrastar o componente desejado para a página.

     O painel lateral pode ser aberto (ou fechado) com:

     ![Botão Ativar/desativar painel lateral](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

   * [Editar o conteúdo de um componente existente](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) na página:

      * Abra a barra de ferramentas do componente com os botões Selecionar. Use o ícone de **Editar** (lápis) para abrir a caixa de diálogo.
      * Abra o editor local do componente clicando e segurando ou com um clique duplo e lento. As ações disponíveis serão exibidas (para alguns componentes, será uma seleção limitada).
      * Para ver todas as ações disponíveis, entre no modo de tela cheia utilizando:

        ![Botão de tela cheia](/help/sites-cloud/authoring/assets/full-screen.png)

   * [Configurar as propriedades de um componente existente](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-edit-dialog)

      * Abra a barra de ferramentas do componente com os botões Selecionar. Use o ícone de **Configurar** (chave inglesa) para abrir a caixa de diálogo.

   * [Mover um componente](/help/sites-cloud/authoring/fundamentals/editing-content.md#moving-a-component):

      * Arrastando o componente desejado para o novo local.
      * Abra a barra de ferramentas do componente com os botões Selecionar. Use o **Recortar** depois **Colar** ícones, quando necessário.

   * [Copiar (e Colar)](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) um componente:

      * Abra a barra de ferramentas do componente com os botões Selecionar. Use o **Copiar** depois **Colar** ícones, conforme necessário.

   >[!NOTE]
   >
   >Você pode **Colar** os componentes na mesma página ou em uma diferente. Ao colar em uma página diferente que já foi aberta antes da operação de cortar/copiar, essa página precisa ser atualizada.

   * [Excluir](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) um componente:

      * Abra a barra de ferramentas do componente com selecione e, em seguida, use o **Excluir** ícone.

   * [Adicionar anotações](/help/sites-cloud/authoring/fundamentals/annotations.md#annotations) à página:

      * Selecione o modo **Anotar** (ícone de balão de fala). Adicione anotações usando o ícone de **Adicionar anotação** (mais). Saia do modo de anotação usando o X na parte superior direita.

        ![Botão Anotações](/help/sites-cloud/authoring/assets/annotations.png)

   * [Visualizar uma página](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) (para ver como ela aparecerá no ambiente de publicação)

      * Selecione **Visualizar** na barra de ferramentas.

   * Retorne ao modo de edição (ou selecione outro modo) usando o seletor suspenso **Editar**.

   >[!NOTE]
   >
   >Para navegar usando links no conteúdo, é necessário usar o [Modo de visualização](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode).

### Editar as propriedades da página   {#editing-the-page-properties}

Existem dois métodos (principais) de [editar propriedades da página](/help/sites-cloud/authoring/fundamentals/page-properties.md):

* No console **Sites**:

   1. [Navegue até a página](#finding-your-page) que deseja publicar.
   1. Selecione o ícone de **Propriedades**:

      * As [Ações rápidas (apenas a exibição de cartão/área de trabalho)](#quick-actions-card-view-desktop-only) do recurso adequado.
      * A barra de ferramenta quando a sua [página é selecionada](#selecting-your-page-for-further-action).

      ![Botão Propriedades](/help/sites-cloud/authoring/assets/properties.png)

   1. As propriedades da página serão exibidas. É possível fazer atualizações conforme necessário, em seguida, usar a opção Salvar para continuar

* Ao [editar sua página](#editing-your-page-content):

   1. Abra o menu de **Informações da página**.
   1. Selecione **Abrir propriedades** para abrir a caixa de diálogo para editar as propriedades.

      ![Botão Informações da página](/help/sites-cloud/authoring/assets/page-information.png)

### Publicar sua página (ou desfazer a publicação) {#publishing-your-page-or-unpublishing}

Existem dois métodos principais de [publicar sua página](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) (e também de desfazer a publicação):

* No console **Sites**:

   1. [Navegue até a página](#finding-your-page) que deseja publicar.
   1. Selecione o ícone **Publicação rápida** por meio de:

      * As [Ações rápidas (apenas a exibição de cartão/área de trabalho)](#quick-actions-card-view-desktop-only) do recurso adequado.
      * A barra de ferramentas quando a sua [página é selecionada](#selecting-your-page-for-further-action) (também fornece o acesso à opção [Publicar mais tarde](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)).

      ![Botão Publicação rápida](/help/sites-cloud/authoring/assets/quick-publish.png)

* Ao [editar sua página](#editing-your-page-content):

   1. Abra o menu de **Informações da página**.
   1. Selecione **Publicar página**.

* Desfazer a publicação de uma página do console só pode ser feito por meio da opção **Gerenciar publicação**, que está disponível somente na barra de ferramentas (não pelas ações rápidas).

  ![Botão Gerenciar publicação](/help/sites-cloud/authoring/assets/manage-publication.png)

  A opção **Cancelar publicação da página** ainda está disponível por meio do menu **Informações da página** no editor.

  Consulte [Publicar páginas](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages) para obter mais informações.

### Mover, copiar e colar ou excluir sua página   {#move-copy-and-paste-or-delete-your-page}

Essas ações podem ser acionadas por:

1. [Navegue até a página](#finding-your-page) que deseja mover, copiar e colar ou excluir.
1. Selecione o ícone copiar (e colar), mover ou excluir, conforme necessário, usando:

   * As [Ações rápidas (apenas a exibição de cartão/área de trabalho)](#quick-actions-card-view-desktop-only) do recurso desejado.
   * A barra de ferramenta quando a sua [página é selecionada](#selecting-your-page-for-further-action).

   Em seguida, depende da sua ação:

   * [Copiar](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#copying-and-pasting-a-page):

      * Em seguida, será necessário navegar até o novo local e colar.

   * [Mover](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#moving-or-renaming-a-page):

      * O assistente é aberto para coletar as informações necessárias para mover a página. Siga as instruções na tela.

   * [Excluir](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#deleting-a-page):

      * Você receberá uma solicitação para confirmar a ação.

   >[!NOTE]
   >
   >A opção Excluir não está disponível como uma Ação rápida.

### Bloquear sua página (em seguida, desbloquear) {#locking-your-page-then-unlocking}

[Bloquear uma página](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) impede que outros autores trabalhem nela enquanto você estiver trabalhando. O ícone/botão Bloquear (e Desbloquear) pode ser encontrado:

* A barra de ferramenta quando a sua [página é selecionada](#selecting-your-page-for-further-action).
* O [menu suspenso Informações da Página](#editing-the-page-properties) ao editar uma página.
* A barra de ferramentas da página ao editar uma página (quando a página estiver bloqueada)

Por exemplo, o ícone de bloqueio tem a seguinte aparência:

![Botão Bloquear](/help/sites-cloud/authoring/assets/lock.png)

### Acessar as referências da página {#accessing-page-references}

[O acesso rápido às referências](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) para/de uma página estão disponíveis no Trilho de referências.

1. Selecione a **Referências** usando o ícone da barra de ferramentas (antes ou depois de [selecionar a página](#selecting-your-page-for-further-action)): 

   ![Opção Exibir referências](/help/sites-cloud/authoring/assets/references.png)

   Uma lista de tipos de referência será exibida:

   ![Exibir referências](/help/sites-cloud/authoring/assets/references-list.png)

1. Selecione o tipo de referência necessário para mostrar mais detalhes e (quando apropriado) executar outras ações.

### Criar uma versão da sua página   {#creating-a-version-of-your-page}

Para criar uma [versão](/help/sites-cloud/authoring/features/page-versions.md) da página:

1. Para abrir o painel Linha do tempo, selecione **[Linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** usando o ícone da barra de ferramentas (antes ou depois de [selecionar a página](#selecting-your-page-for-further-action)): 

   ![Opção Exibir linha do tempo](/help/sites-cloud/authoring/assets/timeline.png)

1. Selecione as reticências na parte inferior direita da coluna Linha do tempo para exibir os botões extras, incluindo **Salvar como versão**.

   ![Exibir linha do tempo](/help/sites-cloud/authoring/assets/timeline-view.png)

1. Selecione **Salvar como versão**, em seguida, **Criar**.

### Restaurar/comparar uma versão da sua página {#restoring-comparing-a-version-of-your-page}

O mesmo mecanismo básico é usado ao restaurar e/ou comparar as versões da sua página:

1. Selecione a **[Linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)** usando o ícone da barra de ferramentas (antes ou depois de [selecionar a página](#selecting-your-page-for-further-action)): 

   ![Opção Exibir linha do tempo](/help/sites-cloud/authoring/assets/timeline.png)

   Se uma versão da sua página já foi salva, ela será listada na Linha do tempo.

1. Selecione a versão que deseja restaurar - isso revelará botões de ação adicionais:

   * **Reverter para essa versão**

      * A versão foi restaurada.

   * **Exibir diferenças**

      * A página será aberta com as diferenças (entre as duas versões) destacadas.
