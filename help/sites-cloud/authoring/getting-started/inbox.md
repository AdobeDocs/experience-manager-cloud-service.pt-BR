---
title: Sua caixa de entrada
description: Gerenciar suas tarefas com a caixa de entrada
exl-id: 37d0cf43-192f-4a50-b174-42d7dced3b63
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '913'
ht-degree: 100%

---

# Sua caixa de entrada {#your-inbox}

Você pode receber notificações de diversas áreas do AEM, incluindo fluxos de trabalho e projetos. Por exemplo, você pode receber notificações sobre:

* Tarefas:
   * Elas também podem ser criadas em vários pontos da interface do usuário do AEM, por exemplo, em **Projetos**.
   * Podem ser o produto de uma etapa de fluxo de trabalho **Criar tarefa** ou **Criar tarefa do projeto**.
* Fluxos de trabalhos:
   * Itens de trabalho que representam as ações que devem ser executadas no conteúdo da página
      * Estes são o produto de etapas do fluxo de trabalho **Participante.**
   * Itens de falha, para permitir que os administradores tentem novamente a etapa que falhou

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

## Abrir a Caixa de entrada   {#opening-the-inbox}

Para abrir a caixa de entrada de notificação do AEM:

1. Clique/toque no indicador na barra de ferramentas.

1. Selecione **Exibir todos**. A **Caixa de entrada do AEM** será aberta. A caixa de entrada mostra itens de fluxos de trabalho, projetos e tarefas.
1. A exibição padrão é [Exibição em lista](#inbox-list-view), mas você também pode alternar para [Exibição de calendário](#inbox-calendar-view). Isso é feito com o seletor de visualização (barra de ferramentas, parte superior direita).

   Para ambas as exibições você também pode definir [Configurações de exibição](#inbox-view-settings). As opções disponíveis dependem da exibição atual.

   ![Configurações de exibição da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>A caixa de entrada funciona como um console, portanto, use [Navegação global](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) ou [Pesquisar](/help/sites-cloud/authoring/getting-started/search.md) para navegar para outro local quando terminar.

### Caixa de entrada - exibição de lista {#inbox-list-view}

Essa exibição lista todos os itens, juntamente com informações relevantes:

![Exibição de lista da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### Caixa de entrada - Exibição de calendário {#inbox-calendar-view}

Esta exibição apresenta itens de acordo com sua posição no calendário:

![Exibição de calendário da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

É possível:

* Selecionar uma exibição específica: **Linha do tempo**, **Coluna**, **Lista**
* Especificar as tarefas a serem exibidas de acordo com **Agendamento**: **Todos**, **Planejado**, **Em andamento**, **Vencimento em breve**, **Vencido**
* Abra o detalhamento para obter mais informações sobre um item
* Selecione um intervalo de datas para focalizar na exibição:

![Intervalo de datas da exibição de calendário da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

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

   Você também pode delegar o calendário a outros usuários, além de solicitar a delegação de outros usuários e gerenciar as delegações.

   ![Configurações de delegação da exibição de lista da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## Realizar ação em um item {#taking-action-on-an-item}

>[!NOTE]
>
>Embora seja possível selecionar mais de um item, ações só podem ser executadas em um item de cada vez.

1. Para executar uma ação em um item, selecione a miniatura do item apropriado. Os ícones de ações aplicáveis a esse item serão mostrados na barra de ferramentas:

   ![Selecionar item da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   As ações são apropriadas ao item e incluem:

   * **Concluir** ação
   * **Delegar** um item
   * **Abrir** um item, dependendo do tipo de item, essa ação pode:

      * Mostrar as propriedades do item
      * Abrir um painel ou um assistente apropriado para uma futura ação
      * Abrir a documentação relacionada
   * **Recuar** para uma etapa anterior
   * Visualizar a carga de um fluxo de trabalho
   * Criar um projeto a partir do item

   >[!NOTE]
   >
   >Para obter mais informações, consulte:
   >
   >* Itens de fluxo de trabalho - [participar de fluxos de trabalho](/help/sites-cloud/authoring/workflows/participating.md)


2. Dependendo do item selecionado, uma ação será iniciada, por exemplo:

   * Uma caixa de diálogo apropriada para a ação será aberta
   * Um assistente de ação será iniciado
   * Uma página de documentação será aberta

   Por exemplo, **Delegar** abrirá uma caixa de diálogo:

   ![Delegar tarefa da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   Se uma caixa de diálogo, um assistente ou uma página de documentação tiver sido aberta, é possível:

   * Confirmar a ação apropriada, por exemplo, atribuir novamente.
   * Cancelar a ação
   * Selecione a seta para trás para retornar à caixa de entrada, por exemplo, se um assistente de ação ou uma página de documentação tiver sido aberta, você poderá retornar à Caixa de entrada.


## Criação de uma tarefa {#creating-a-task}

Na caixa de entrada, você pode criar tarefas:

1. Selecione **Criar**, **Tarefa**.
1. Preencha os campos necessários nas guias **Básicas** e **Avançadas** (somente o **Título** é obrigatório, todos os demais são opcionais):

   * **Básico**:

      * **Título**
      * **Projeto**
      * **Destinatário**
      * **Conteúdo**, semelhante a Carga, essa é uma referência da tarefa a um local no repositório
      * **Descrição**
      * **Prioridade da tarefa**
      * **Data inicial**
      * **Data de vencimento**

   ![Tarefa Adicionar caixa de entrada](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **Avançado**

      * **Nome**: isso será usado para formar o URL e, se estiver vazio, será baseado no **Título**.

   ![Opções avançadas da tarefa Adicionar caixa de entrada](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. Selecione **Enviar**.

## Criação de um projeto   {#creating-a-project}

Para determinadas tarefas, você pode criar um [Projeto](/help/sites-cloud/authoring/projects/overview.md) com base nessa tarefa:

1. Toque ou clique na miniatura para selecionar a tarefa apropriada.

   >[!NOTE]
   >
   >Somente tarefas criadas usando a opção **Criar** da **Caixa de entrada** podem ser usadas para criar um projeto.
   >
   >Itens de trabalho (de um fluxo de trabalho) não podem ser usados para criar um projeto.

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

   ![Pesquisa da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-search.png)

1. É possível filtrar os itens listados de acordo com uma variedade de critérios, muitos dos quais pode ser refinados. Por exemplo:

   ![Filtro de pesquisa da caixa de entrada](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >Com [Configurações de exibição](#inbox-view-settings) você também pode configurar a ordem de classificação ao usar a [Exibição de lista](#inbox-list-view).
