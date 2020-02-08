---
title: Sua Caixa de entrada
description: Gerenciar suas tarefas com a caixa de entrada
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Sua Caixa de entrada {#your-inbox}

Você pode receber notificações de várias áreas do AEM, incluindo fluxos de trabalho e projetos. Por exemplo, você pode receber notificações sobre:

* Tarefas:
   * These can also be created at various points within the AEM UI, for example, under **Projects**.
   * These can be the product of a workflow **Create Task** or **Create Project Task** step.
* Fluxos de trabalhos:
   * Itens de trabalho que representam ações que você precisa executar no conteúdo da página
      * These are the product of workflow **Participant** steps.
   * Itens com falha, para permitir que os administradores repitam a etapa com falha

Você recebe essas notificações em sua própria caixa de entrada, onde você pode visualizá-las e executar a ação necessária.

>[!NOTE]
>
>Para obter mais informações sobre os tipos de item, consulte também:
>
>* [Projetos](/help/sites-cloud/authoring/projects/overview.md)
>* [Projetos - trabalhar com tarefas](/help/sites-cloud/authoring/projects/tasks.md)
>* [Fluxos de trabalhos](/help/sites-cloud/authoring/workflows/overview.md)


## Caixa de entrada no cabeçalho {#inbox-in-the-header}

De qualquer um dos consoles, o número atual de itens em sua caixa de entrada é mostrado no cabeçalho. O indicador também pode ser aberto para fornecer acesso rápido às páginas que requerem ações ou acesso à caixa de entrada:

![Visão geral da caixa de entrada no cabeçalho](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
>
>Algumas ações também serão mostradas na [exibição de cartão do recurso apropriado](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view).

## Abrir a Caixa de entrada {#opening-the-inbox}

Para abrir a caixa de entrada de notificação do AEM:

1. Clique/toque no indicador na barra de ferramentas.

1. Selecione **Exibir todos**. A **Caixa de entrada do AEM** será aberta. A caixa de entrada mostra itens de fluxos de trabalho, projetos e tarefas.
1. A exibição padrão é a [Exibição de lista](#inbox-list-view), mas você também pode alternar para a [Visualização do calendário](#inbox-calendar-view). Isso é feito com o seletor de exibição (barra de ferramentas, canto superior direito).

   For both views you can also define [View Settings](#inbox-view-settings). The options available are dependent on the current view.

   ![Configurações de exibição da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>The Inbox operates as a console, so use [Global Navigation](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) or [Search](/help/sites-cloud/authoring/getting-started/search.md) to navigate to another location when you are finished.

### Caixa de entrada - exibição de lista {#inbox-list-view}

Esta exibição lista todos os itens, juntamente com as informações relevantes:

![Exibição da lista da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### Caixa de entrada - Exibição de calendário {#inbox-calendar-view}

Esta exibição apresenta itens de acordo com sua posição no calendário:

![Exibição de calendário da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

É possível:

* Select a specific view: **Timeline**, **Column**, **List**
* Specify the tasks to display according to **Schedule**: **All**, **Planned**, **In Progress**, **Due Soon**, **Past Due**
* Detalhar para obter informações mais detalhadas sobre um item
* Selecione um intervalo de datas para focalizar a exibição:

![Intervalo de datas da exibição do calendário da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### Caixa de entrada - configurações de exibição {#inbox-view-settings}

Para ambas as exibições (Lista e Calendário), você pode definir configurações:

* **Exibição de calendário**

   Para a **Exibição de calendário** é possível configurar:

   * **Agrupar por**
   * **Agendamento** ou **Nenhum**
   * **Tamanho do cartão**
   ![Configurações de exibição do calendário da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **Exibição de lista**

   Para a **Exibição de lista**, você pode configurar o mecanismo de classificação:

   * **Classificar por**
   * **Ordem de classificação**
   ![Configurações de exibição da lista da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

   Você também pode delegar seu calendário para outros usuários, além de solicitar delegação de outros usuários e gerenciar suas delegações.

   ![Configurações de delegação de exibição da lista de caixa de entrada](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## Realizar ação em um item {#taking-action-on-an-item}

1. Para executar uma ação em um item, selecione a miniatura do item apropriado. Os ícones de ações aplicáveis a esse item serão mostrados na barra de ferramentas:

   ![Selecionar item da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   As ações são apropriadas ao item e incluem:

   * **Ação completa**
   * **Delegar** um item
   * **Abra** um item, dependendo do tipo de item que esta ação pode:

      * Mostrar as propriedades do item
      * Abrir um painel ou assistente apropriado para outras ações
      * Abrir documentação relacionada
   * **Recuar** para uma etapa anterior
   * Visualizar a carga de um fluxo de trabalho
   * Criar um projeto a partir do item
   >[!NOTE]
   >
   >Para obter mais informações, consulte:
   >
   >* Itens de fluxo de trabalho - [ participar de fluxos de trabalho](/help/sites-cloud/authoring/workflows/participating.md)


1. Dependendo do item selecionado, uma ação será iniciada, por exemplo:

   * Uma caixa de diálogo apropriada para a ação será aberta
   * Um assistente de ação será iniciado
   * Uma página de documentação será aberta
   For example, **Delegate** will open a dialog:

   ![Delegar tarefa da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   Se uma caixa de diálogo, um assistente ou uma página de documentação tiver sido aberta, é possível:

   * Confirme a ação apropriada, por exemplo, reatribuir.
   * Cancelar a ação
   * Selecione a seta para trás para retornar à caixa de entrada; por exemplo, se um assistente de ação ou uma página de documentação tiver sido aberta, você poderá retornar à Caixa de entrada.


## Criação de uma tarefa {#creating-a-task}

Na caixa de entrada, você pode criar tarefas:

1. Selecione **Criar**, **Tarefa**.
1. Complete the necessary fields in the **Basic** and **Advanced** tabs (only the **Title** is mandatory, all others are optional):

   * **Básico**:

      * **Título**
      * **Projeto**
      * **Destinatário**
      * **Conteúdo**, semelhante à Carga, essa é uma referência da tarefa para um local no repositório
      * **Descrição**
      * **Prioridade da tarefa**
      * **Data inicial**
      * **Data de vencimento**
   ![Tarefa de adição da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **Avançado**

      * **Nome**: será usado para formar o URL e, se estiver em branco, será baseado no **Título**.
   ![Caixa de entrada adicionar opções avançadas de tarefa](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. Selecione **Enviar**.

## Criação de um projeto {#creating-a-project}

Para determinadas tarefas, você pode criar um [Projeto](/help/sites-cloud/authoring/projects/overview.md) com base nessa tarefa:

1. Toque ou clique na miniatura para selecionar a tarefa apropriada.

   >[!NOTE]
   >
   >Only tasks created using the **Create** option of the **Inbox** can be used to create a project.
   >
   >Os itens de trabalho (de um fluxo de trabalho) não podem ser usados para criar um projeto.

1. Selecione **Criar projeto** na barra de ferramentas para abrir o assistente.
1. Selecione o modelo apropriado e, em seguida, clique em **Avançar**.
1. Especifique as propriedades necessárias:

   * **Básico**

      * **Título**
      * **Descrição**
      * **Data inicial**
      * **Data de vencimento**
      * **Usuário** e função
   * **Avançado**

      * **Nome**
   >[!NOTE]
   >
   >Consulte [Criação de um projeto](/help/sites-cloud/authoring/projects/managing.md#creating-a-project) para obter as informações completas.

1. Selecione **Criar** para confirmar a ação.

## Filtrar itens na Caixa de entrada do AEM {#filtering-items-in-the-aem-inbox}

Você pode filtrar os itens listados:

1. Abra a **Caixa de entrada do AEM**.

1. Abra o seletor de filtro:

   ![Pesquisa na caixa de entrada](/help/sites-cloud/authoring/assets/inbox-search.png)

1. Você pode filtrar os itens listados de acordo com uma variedade de critérios, muitos dos quais podem ser refinados.Por exemplo:

   ![Filtro de pesquisa da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >Com [Configurações de exibição](#inbox-view-settings) você também pode configurar a ordem de classificação ao usar a [Exibição de lista](#inbox-list-view).
