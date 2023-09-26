---
title: Editar conteúdo da página
description: Depois que a página é criada, é possível editar o conteúdo para fazer as atualizações necessárias
exl-id: 8af0f621-14e8-4605-a51a-a3be21f19092
source-git-commit: 53d4e22805774c0b994ee2bba429c19506639014
workflow-type: tm+mt
source-wordcount: '2983'
ht-degree: 97%

---


# Editar conteúdo da página{#editing-page-content}

Assim que a página for criada (nova ou como parte de um lançamento ou uma live copy), você pode editar o conteúdo para fazer as atualizações necessárias.

O conteúdo é adicionado usando [componentes](/help/sites-cloud/authoring/features/components-console.md) (apropriado ao tipo de conteúdo) que podem ser arrastados para a página. Estes podem então ser editados no local, movidos ou excluídos. 

>[!NOTE]
>
>Sua conta precisa dos direitos de acesso apropriados e das permissões para editar páginas.
>
>Caso encontre algum problema, sugerimos que você entre em contato com o administrador do sistema.
<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to edit pages.
-->

>[!NOTE]
>
>Se a página e/ou o modelo foi configurado corretamente, é possível usar o [layout responsivo](/help/sites-cloud/authoring/features/responsive-layout.md) durante a edição.

>[!TIP]
>
>Quando estiver no modo de **Edição**, os links em seu conteúdo ficam visíveis, mas **não ficam acessíveis**. Use o [modo de Visualização](#previewing-pages) se você deseja navegar usando os links no seu conteúdo.

{{edge-delivery-authoring}}

## Barra de ferramentas da página {#page-toolbar}

A barra de ferramentas da página oferece acesso à funcionalidade adequada, dependendo da configuração da página.

![Barra de ferramentas da página](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

A barra de ferramentas oferece acesso a várias opções. Dependendo do contexto e da configuração atual, algumas opções podem não estar disponíveis.

* **Ativar/desativar painel lateral**

  Isso abre/fecha o painel lateral, que contém o [Navegador de ativos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser), [Navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) e [Árvore de conteúdo](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree).

  ![Ativar/desativar painel lateral](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **Informações da página**

  Fornece acesso ao menu [Informações da página](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) incluindo detalhes da página e ações que podem ser tomadas na página, incluindo visualização e edição de informações da página, visualização de propriedades da página e publicação/cancelamento da publicação da página.

  ![Botão Informações da página](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **Emulador**

  Ativa a [barra de ferramentas do emulador](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate), que é usada para emular a aparência da página em outro dispositivo. Isso é alternado automaticamente no modo de layout.

  ![Tecla Emulador](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

  Abre o [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md). Disponível somente no modo de Visualização.

  ![Botão ContextHub](/help/sites-cloud/authoring/assets/context-hub.png)

* **Título da página**

  Isso é puramente informativo.

  ![Título da página](/help/sites-cloud/authoring/assets/page-title.png)

* **Seletor de modo**

  Exibe o atual [modo](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) e permite selecionar outro modo, como editar, layout, timewarp ou direcionamento.

  ![Botão Seletor de modo](/help/sites-cloud/authoring/assets/mode-selector.png)

* **Visualizar**

  Habilita [modo de visualização](#preview-mode). Isso exibe a página como ela será exibida quando publicada.

  ![Botão Visualizar](/help/sites-cloud/authoring/assets/preview.png)

* **Anotar**

  Permite adicionar [anotações](/help/sites-cloud/authoring/fundamentals/annotations.md) à página ao revisar uma página. Após a primeira anotação, o ícone alternará para um número que indica o número de anotações na página.

  ![Botão Anotar](/help/sites-cloud/authoring/assets/annotations.png)

### Notificação de status {#status-notification}

Se uma página é parte de um [fluxo de trabalho](/help/sites-cloud/authoring/workflows/overview.md) ou de vários fluxos de trabalho, essas informações serão exibidas em uma barra de notificação na parte superior da tela ao editar a página.

![Notificação do fluxo de trabalho](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>A barra de status só é visível para contas de usuário com os privilégios apropriados.

A notificação lista o fluxo de trabalho que está sendo executado na página. Se o usuário estiver envolvido na etapa atual do fluxo de trabalho, as opções para [afetar o status do fluxo de trabalho](/help/sites-cloud/authoring/workflows/participating.md) e obter mais informações sobre ele também estarão disponíveis, como:

* **Concluir** - abre a caixa de diálogo **Concluir item de trabalho**
* **Delegar** - abre a caixa de diálogo **Concluir item de trabalho**
* **Exibir detalhes** - abre a janela **Detalhes** do fluxo de trabalho

Concluir e delegar etapas do fluxo de trabalho por meio da barra de notificação funciona da mesma maneira como ao [participar de fluxos de trabalho](/help/sites-cloud/authoring/workflows/participating.md) por meio da caixa de entrada de Notificações.

Se a página estiver sujeita a vários fluxos de trabalho, o número de fluxos de trabalho será exibido na extremidade direita da notificação, junto a botões de seta para permitir que você navegue pelos fluxos de trabalho.

![Várias notificações do fluxo de trabalho](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## Espaço reservado do componente {#component-placeholder}

O espaço reservado do componente é um indicador para mostrar onde um componente será posicionado ao soltá-lo, acima do componente sobre o qual você está passando o mouse.

* Ao adicionar um novo componente à página (arrastando-o a partir do navegador de componentes):

  ![Espaço reservado ao adicionar um novo componente a uma página](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* Ao mover um componente existente:

  ![Espaço reservado ao mover um componente existente em uma página](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## Inserir um componente {#inserting-a-component}

### Inserir um componente do navegador de componentes {#inserting-a-component-from-the-components-browser}

É possível adicionar um novo componente, usando o [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). O [espaço reservado do componente](#component-placeholder) mostra onde o componente está posicionado:

1. Certifique-se de que a página está no modo de [**edição**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. Abra o [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
1. Arraste o componente para a [posição desejada](#component-placeholder).
1. [Editar](#edit-content) o componente.

>[!NOTE]
>
>Em um dispositivo móvel, o navegador de componentes preencherá a tela inteira. Depois de começar a arrastar um componente, o navegador será fechado para mostrar a página novamente, para que você possa colocá-lo.

### Inserir um componente do Sistema de parágrafos {#inserting-a-component-from-the-paragraph-system}

É possível adicionar um novo componente, usando a caixa **Arraste componentes aqui**:

1. Certifique-se de que a página está no modo de [**edição**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. Há duas maneiras de selecionar e adicionar um novo componente a partir do sistema de parágrafos:

   * Selecione a opção **Inserir componente** (+) seja na barra de ferramentas de um componente já existente ou na caixa **Arraste componentes aqui**.

     ![Inserir um componente](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * Se você estiver em um dispositivo de desktop, clique duas vezes na caixa **Arraste componentes aqui**.

   * A caixa de diálogo **Inserir novo componente** será aberta para permitir que você selecione o componente desejado: 

     ![Caixa de diálogo Inserir novo componente](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. O componente selecionado será adicionado à parte inferior da página. [Edite-o](#edit-content), conforme necessário.

### Inserir um componente usando o Navegador de ativos   {#inserting-a-component-using-the-assets-browser}

Também é possível adicionar um novo componente à página arrastando um ativo do [navegador de ativos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser). Isso criará automaticamente um novo componente do tipo apropriado (e que contém o ativo).

Esse comportamento pode ser configurado para a instalação. Consulte Configuração de um sistema de parágrafo para que a arrastar um ativo crie uma instância de componente para obter mais detalhes. <!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

Para criar um componente arrastando um dos tipos de ativos acima:

1. Certifique-se de que a página está no modo de [**edição**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes).
1. Abra o [navegador de ativos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
1. Arraste o ativo desejado para a posição desejada. O [espaço reservado do componente](#component-placeholder) mostra onde ele será posicionado.

   Um componente, apropriado para o tipo de ativo, será criado nesse local e conterá o ativo selecionado.

1. [Edite](#edit-content) o componente, se necessário.

>[!NOTE]
>
>Em um dispositivo móvel, o navegador de ativos preencherá a tela inteira. Depois de começar a arrastar um ativo, o navegador será fechado para mostrar a página novamente, para que você possa colocá-lo.

Se, durante a navegação pelos ativos, você perceber que precisa fazer uma alteração rápida em um, é possível iniciar o [editor de ativos](/help/assets/manage-digital-assets.md) diretamente do navegador, clicando no ícone de edição ao lado do nome do ativo.

![Botão Editar ativos](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## Component Toolbar {#component-toolbar}

Selecionar um componente abrirá a barra de ferramentas. Isto proporciona acesso a várias ações que podem ser executadas no componente.

As ações de fato disponíveis para o usuário serão mostradas conforme apropriado e nem todas elas estarão descritas aqui.

![Component Toolbar](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **Editar**

  [Dependendo do tipo de componente](/help/sites-cloud/authoring/fundamentals/components.md), isso permite a [edição do conteúdo do componente](#edit-content). Frequentemente, é fornecida uma barra de ferramentas.

  ![Botão Editar](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **Configurar**

  [Dependendo do tipo de componente](/help/sites-cloud/authoring/fundamentals/components.md), isso permite a edição e a configuração das propriedades do componente. Frequentemente uma caixa de diálogo é aberta.

  ![Botão Configurar](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **Copiar**

  Isso copiará o componente para a área de transferência. Após a ação de colagem, o componente original permanecerá.

  ![Botão Copiar](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **Recortar**

  Isso copiará o componente para a área de transferência. Após a ação de colagem, o componente original é removido.

  ![Botão Cortar](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **Excluir**

  Isso irá excluir o componente da página após a sua confirmação.

  ![Botão Excluir](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **Inserir componente**

  Isso abrirá a caixa de diálogo para [adicionar um novo componente](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system).

  ![Botão Inserir](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **Colar**

  Isso colará o componente da área de transferência na página. A permanência do original dependerá se ele foi copiado ou recortado.

   * É possível colar para a mesma página para outra.
   * O item colado será posicionado acima do item onde você usou a ação de colagem.
   * A ação Colar só será exibida se houver conteúdo na área de transferência.

  ![Botão Colar](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

  >[!NOTE]
  >
  >Se você colar em uma página diferente que já estava aberta antes da operação de recortar/copiar, será necessário atualizar a página para ver o conteúdo colado.

* **Grupo**

  Isso permite selecionar vários componentes de uma só vez. O mesmo pode ser alcançado em um desktop por um **Ctrl+Clique** ou **Command+Clique**.

  ![Botão Agrupar](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **Pai**

  Permite selecionar o componente principal do componente selecionado.

  ![Botão Pai](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **Layout**

  Isso permite modificar o [layout](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) do componente selecionado. Isso se aplica somente ao componente selecionado e não ativa o [Modo de layout](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) para a página inteira.

  ![Botão Layout](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **Converta em uma variação de fragmento de experiência**

  Isso permite criar um novo [fragmento de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) do componente selecionado ou adicione-o a um fragmento de experiência existente.

  ![Botão Converter para fragmento de experiência](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## Editar conteúdo {#edit-content}

Existem dois métodos de adição e/ou edição do conteúdo dos componentes:

* Abra a [caixa de diálogo do componente para edição](#component-edit-dialog).
* [Arraste e solte um ativo](#drag-and-drop-assets-into-component) do navegador de ativos para adicionar conteúdo diretamente.

### Caixa de diálogo de edição de componente   {#component-edit-dialog}

Abra um componente para editar o conteúdo usando o ícone de [Editar (lápis) da barra de ferramentas do componente](#component-toolbar).

As opções de edição exatas dependerão do componente. Para alguns componentes, [todas as ações só estarão disponíveis no modo de tela cheia](#edit-content-full-screen-mode). Por exemplo:

* Componente de texto

  ![Barra de ferramentas do componente de texto](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* Componente de imagem

  ![Barra de ferramentas do componente de imagem](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

  >[!NOTE]
  >
  >A edição não funciona em um componente de imagem vazio.
  >
  >Você deve arrastar ou fazer upload de uma imagem para o componente antes de começar a editá-la.

* Componente de imagem - tela cheia

  [Entrar no modo de tela cheia](#edit-content-full-screen-mode) para o componente de imagem permite mais espaço para editar a imagem, bem como mostrar opções de edição adicionais como **Inicializar mapa** e **Redefinir zoom**. Além disso, a tela cheia permite selecionar predefinições de corte.

  ![Modo de tela cheia do Componente de imagem](/help/sites-cloud/authoring/assets/editing-image-component-full-screen.png)

* Componentes construídos a partir de mais de um componente básico exigem que você confirme primeiro qual o conjunto de opções de edição deseja:

### Arraste e solte ativos no componente {#drag-and-drop-assets-into-component}

Para tipos de componentes específicos (como imagens), você pode arrastar e soltar os ativos do navegador de ativos diretamente no componente para atualizar o conteúdo.

## Editar conteúdo no modo de tela cheia {#edit-content-full-screen-mode}

Para todos os componentes, o modo de tela cheia pode ser acessado com (e fechado de):

![Botão de tela cheia](/help/sites-cloud/authoring/assets/editing-full-screen.png)

Por exemplo, o componente de **Texto:**

![Componente de texto em tela cheia](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>Para alguns componentes, o modo de tela cheia terá mais opções disponíveis do que o editor básico no local.

## Mover um componente {#moving-a-component}

Para mover um componente de parágrafo:

1. Selecione o parágrafo a ser movido com o toque e segure ou com o clique e segure.
1. Arraste o parágrafo para o novo local. AEM indicará onde o parágrafo pode ser colocado. Solte-o no local desejado.

   ![Mover um componente](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. Seu parágrafo foi movido.

>[!TIP]
>
>Também é possível usar [Cortar e colar](#component-toolbar) para mover um componente.

## Editar layout de componente {#edit-component-layout}

Em vez de repetidamente alternar entre os modos de edição e de [layout](/help/sites-cloud/authoring/features/responsive-layout.md) para ajustar um componente, você pode selecionar a ação **Layout** referente a um componente para alterar o layout do componente e poupar tempo, uma vez que não é preciso sair do modo de edição.

1. Quando estiver no modo de **Edição** do console de sites, selecionar um componente revela a barra de ferramentas do componente.

   ![A barra de ferramentas do componente de um componente de página](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   Clique ou toque na ação **Layout** para definir o layout do componente.

   ![O botão Layout da barra de ferramentas do componente](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. Depois que a ação Layout for selecionada:

   * As alças de redimensionamento do componente são exibidas.
   * A barra de ferramentas do emulador é mostrada na parte superior da tela.
   * As ações de Layout em vez das ações de edição padrão são exibidas na barra de ferramentas do componente.

   ![Um componente no modo de layout](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   Agora é possível modificar o layout do componente da mesma maneira que você faria no [modo de layout](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode).

1. Após fazer as alterações necessárias no layout, clique no botão **Fechar** no menu de ação de componente para concluir a modificação do layout do componente. A barra de ferramentas do componente retornará ao seu estado normal de edição.

   ![A barra de ferramentas do componente de um componente de página](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>O escopo da ação Layout é limitada ao componente selecionado. Por exemplo, se estiver editando o layout de um componente e, em seguida, clicar em outro componente, a barra de ferramentas de edição padrão (não a barra de ferramentas do layout) será exibida para o componente recém-selecionado, e as alças de redimensionamento, bem como a barra de ferramentas do emulador desaparecerão.
>
>Se precisar editar o layout geral da página, afetando vários componentes, alterne para o [modo de layout](/help/sites-cloud/authoring/features/responsive-layout.md).

## Componentes herdados {#inherited-components}

Herança é o mecanismo em que o conteúdo pode ser automaticamente enviado de um componente para outro. Componentes herdados podem ser o resultado de vários cenários, incluindo:

* [Gerenciamento de vários sites](/help/sites-cloud/administering/msm/overview.md)
* [Lançamentos](/help/sites-cloud/authoring/launches/overview.md) (quando com base na live copy).

Você pode cancelar (e depois reativar) a herança. Dependendo do componente, esta opção pode estar disponível na barra de ferramentas do componente, se o componente estiver em uma página que faz parte de uma live copy ou lançamento (com base em uma live copy).

![Uma barra de ferramentas do componente que mostra a relação de herança](/help/sites-cloud/authoring/assets/editing-component-toolbar-inheritance.png)

Por exemplo:

* Cancelar herança

  ![Botão Cancelar herança](/help/sites-cloud/authoring/assets/editing-cancel-inheritance.png)

* Reativar herança (se a herança já estiver cancelada)

  ![Botão Reativar herança](/help/sites-cloud/authoring/assets/editing-reenable-inheritance.png)

* A ação de implantação também está disponível no blueprint ou na origem de Live Copy

  ![Botão Implantação](/help/sites-cloud/authoring/assets/editing-rollout.png)

## Editar o modelo da página {#editing-the-page-template}

Você pode alternar facilmente para o [editor de modelo](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors), selecionando **Editar modelo** no menu [Informações da página](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information).

É possível ver em qual modelo a página é baseada ao selecionar a página na [Exibição de coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) ou na [Exibição de lista](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view).

## Status da Live Copy   {#live-copy-status}

O [Modo de página Status da Live Copy](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) permite ter uma visão geral rápida do status da live copy e de quais componentes são, ou não, herdados:

* Borda verde: herdada
* Borda rosa: a herança foi cancelada

Por exemplo:

![Exemplo de status da live copy exibida](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## Adicionar anotações {#adding-annotations}

As [anotações](/help/sites-cloud/authoring/fundamentals/annotations.md) permitem que revisores e outros autores forneçam feedback sobre o seu conteúdo. Eles são usados com frequência para fins de revisão e validação.

## Visualizar páginas   {#previewing-pages}

Existem duas opções para a visualização de uma página:

* [Modo de visualização](#preview-mode) - uma visualização rápida, no local
* [Exibir como publicado](#view-as-published) - uma visualização completa que abre a página em uma nova guia

>[!TIP]
>
>* Os links no conteúdo estarão visíveis, mas não poderão ser acessados no modo Editar.
>* Use qualquer uma das opções de visualização, caso deseje navegar usando os links.
>* Use o [atalho de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` para alternar entre a visualização e o último modo selecionado.

>[!NOTE]
>
>O cookie do Modo de WCM está definido para ambas as opções de visualização.

### Modo de visualização {#preview-mode}

Ao editar o conteúdo, é possível visualizar a página usando o [modo](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) de visualização. Este modo:

* Oculta vários mecanismos de edição para fornecer uma visualização rápida de como a página aparecerá na publicação.
* Permite usar links para navegar.
* **Não** atualiza o conteúdo da página.

Ao criar, o modo de visualização está disponível usando o ícone na parte superior direita do editor de página:

![Botão Visualizar](/help/sites-cloud/authoring/assets/preview.png)

### Exibir como publicado {#view-as-published}

A opção **Exibir como publicado** está disponível no menu [Informações da página](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information). Isso abre a página em uma nova guia, atualiza o conteúdo e mostra a página exatamente como ela aparecerá no ambiente de publicação.

## Bloquear uma página   {#locking-a-page}

O AEM permite que você bloqueie uma página, para que ninguém mais possa editar o conteúdo. Esse bloqueio é útil quando você está fazendo várias edições em uma página específica ou quando precisa congelar uma página por um curto período.

Uma página pode ser bloqueada a partir do:

* Console do **Sites**

   1. Selecione a página com o [modo de seleção](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
   1. Selecione o ícone de bloqueio.

      ![Botão Bloquear](/help/sites-cloud/authoring/assets/lock.png)

* **Editor de página**

   1. Selecione o ícone de **Informações da página** para abrir o menu.
   1. Selecione a opção **Bloquear página**.

Uma vez bloqueadas, as informações de exibição do console são atualizadas e, ao editar, um símbolo de cadeado é apresentado na barra de ferramentas.

![Exemplo de uma página bloqueada](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>O bloqueio de uma página pode ser executado quando se representa um usuário. No entanto, uma página bloqueada dessa maneira só pode ser desbloqueada (por clientes) usando o usuário que foi representado.
>
>Páginas não podem ser desbloqueadas representando o usuário que as bloqueou.
>
>Se o usuário que bloqueou a página não estiver disponível para desbloqueá-la, entre em contato com o Suporte ao cliente para avaliar as opções para remover o bloqueio.

## Desbloquear uma página {#unlocking-a-page}

Desbloquear uma página é muito semelhante a [bloquear uma página](#locking-a-page). Uma vez bloqueada, as opções de bloqueio são substituídas por ações de desbloqueio.

O menu de Informações da página lista **Desbloquear** como uma opção, e o ícone Bloquear no console de sites é substituído pelo ícone **Desbloquear**.

![Botão Desbloquear](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>O bloqueio de uma página pode ser executado quando se representa um usuário. No entanto, uma página bloqueada dessa maneira só pode ser desbloqueada (por clientes) usando o usuário que foi representado.
>
>Páginas não podem ser desbloqueadas representando o usuário que as bloqueou.
>
>Se o usuário que bloqueou a página não estiver disponível para desbloqueá-la, entre em contato com o Suporte ao cliente para avaliar as opções para remover o bloqueio.

<!--
>[!CAUTION]
>
>Locking a page can be performed when impersonating a user. However a page locked in this way can only then be unlocked by the user who was impersonated, or by a user with admin rights (a member of AEM Administrator IMS profile).
>
>Pages cannot be unlocked by impersonating the user who locked the page.
-->

<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## Desfazer e refazer edições de página {#undoing-and-redoing-page-edits}

Os ícones a seguir permitem desfazer ou refazer uma ação. Os seguintes itens são mostrados na barra de ferramentas, quando apropriado: 

![Os botões Desfazer e Refazer](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* O [atalho de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Z` também pode ser usado para desfazer ações de edições em páginas.
>* O atalho de teclado `Ctrl-Y` também pode ser usado para refazer ações de edições em páginas.

>[!NOTE]
>
>Consulte [Desfazer e refazer edições de página - A teoria](#undoing-and-redoing-page-edits-the-theory) para obter todos os detalhes do que é possível fazer ao desfazer e refazer edições de página.

## Desfazer e refazer edições de página - a teoria {#undoing-and-redoing-page-edits-the-theory}

O AEM armazena um histórico de ações que você executa e a sequência na qual as executou, para que você possa desfazer várias ações na ordem em que as executou ou refazê-las pra reaplicar uma ou mais ações, se necessário.

Se um elemento na página de conteúdo estiver selecionado (po exemplo, como um componente de texto), o comando de desfazer e refazer será aplicado ao item selecionado.

O comportamento dos comandos desfazer e refazer é semelhante ao de outros softwares. Use os comandos para restaurar o estado recente da sua página da Web, conforme você decide sobre o conteúdo. Por exemplo, caso mova um parágrafo de texto para um local diferente na página, você pode usar o comando desfazer para mover o parágrafo de volta. Se você decidir que a posição anterior era melhor, use o comando Refazer para “desfazer a ação de desfazer”.

Por exemplo, você pode:

* Refazer ações desde que não tenha feito nenhuma edição da página desde que usou o comando desfazer.
* Desfazer no máximo 20 ações de edição (configuração padrão).
* Usar os [Atalhos de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) para desfazer e refazer.

É possível desfazer ou refazer os seguintes tipos de alterações de página:

* Adição, edição, remoção e movimentação de parágrafos
* Edição no local do conteúdo do parágrafo
* Cópia, recorte e colagem de itens em uma página

>[!NOTE]
>
>* Permissões especiais são necessárias para desfazer e refazer as alterações nos arquivos e imagens.
>* O histórico de alterações em arquivos e imagens dura no mínimo dez horas. Além desse período, no entanto, a ação de desfazer as alterações não é garantida. Seu administrador pode alterar o tempo padrão de dez horas.
>* O administrador do sistema pode configurar vários aspectos dos recursos desfazer/refazer de acordo com os requisitos de sua ocorrência.
<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
