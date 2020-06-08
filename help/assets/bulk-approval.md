---
title: Revisar ativos em pastas e coleções
description: Configure workflows de revisão para ativos em uma pasta ou coleção e compartilhe-os com revisores ou parceiros criativos para obter feedback.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 24%

---


# Revisar ativos em pastas e coleções {#review-folder-assets-and-collections}

Usando os ativos Adobe Experience Manager (AEM), você pode definir workflows de revisão ad hoc para ativos que estão em uma pasta ou em uma coleção. Você pode compartilhá-lo com revisores ou parceiros criativos para buscar seus comentários. Você pode associar um fluxo de trabalho de revisão a um projeto ou criar uma tarefa de revisão independente.

Depois de compartilhar os ativos, os revisores podem aprová-los ou rejeitá-los. As notificações são enviadas em vários estágios do fluxo de trabalho para notificar recipient pretendidos sobre a conclusão de várias tarefas. Por exemplo, quando você compartilha uma pasta ou coleção, o revisor recebe uma notificação de que uma pasta/coleção foi compartilhada para revisão.

Depois que o revisor concluir a revisão (aprova ou rejeita ativos), você receberá uma notificação de conclusão da revisão.

## Criação de uma tarefa de revisão para pastas {#creating-a-review-task-for-folders}

1. Na interface do usuário Ativos, selecione a pasta para a qual deseja criar uma tarefa de revisão.
1. Na barra de ferramentas, toque/clique no ícone **[!UICONTROL Criar tarefa de revisão]** para abrir a página **[!UICONTROL Verificar tarefa]**. Se não conseguir ver o ícone na barra de ferramentas, toque/clique em **[!UICONTROL Mais]** e selecione o ícone.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Opcional) Na lista **[!UICONTROL Projeto]** , selecione o projeto ao qual deseja associar a tarefa de revisão. Por padrão, a opção **[!UICONTROL Nenhum]** está selecionada. Se você não quiser associar qualquer projeto à tarefa de revisão, mantenha essa seleção.

   >[!NOTE]
   >
   >Somente os projetos para os quais você tem permissões no nível do Editor (ou superior) estão visíveis na lista **[!UICONTROL Projetos]** .

1. Insira um nome para a tarefa de revisão e selecione um aprovador na lista **[!UICONTROL Atribuir]** .

   >[!NOTE]
   >
   >Os membros/grupos do projeto selecionado estão disponíveis como aprovadores na lista **[!UICONTROL Atribuir]** .

1. Informe uma descrição, a prioridade da tarefa e a data de vencimento da tarefa de revisão.

   ![tarefa_details](assets/task_details.png)

1. Na guia Avançado, digite um rótulo a ser usado para criar o URI.

   ![review_name](assets/review_name.png)

1. Toque/clique em **[!UICONTROL Enviar]** e em **[!UICONTROL Concluído]** para fechar a mensagem de confirmação. Uma notificação para a nova tarefa é enviada ao aprovador.
1. Faça logon nos ativos AEM como aprovador e navegue até a interface do usuário dos ativos. Para aprovar ativos, clique/toque no ícone **[!UICONTROL Notificações]** e selecione a tarefa de revisão na lista.

   ![notificação](assets/notification.png)

1. Na página **[!UICONTROL Tarefa de revisão]**, examine os detalhes da tarefa de revisão e toque/clique em **[!UICONTROL Revisar]**.
1. Na página **[!UICONTROL Revisar tarefa]**, selecione os ativos e toque/clique no ícone **[!UICONTROL Aprovar/Rejeitar]** para aprovar ou rejeitar, conforme apropriado.

   ![review_tarefa](assets/review_task.png)

1. Toque/clique no ícone **[!UICONTROL Concluído]** na barra de ferramentas. Na caixa de diálogo, digite um comentário e toque/clique em **[!UICONTROL Concluir]** para confirmar.
1. Navegue até a interface do usuário Ativos e abra a pasta. Os ícones de status de aprovação dos ativos são exibidos nas visualizações Cartão e Lista.

   **Exibição de cartão**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **Exibição de lista**

   ![review_status_listview](assets/review_status_listview.png)

## Criação de uma tarefa de revisão para coleções {#creating-a-review-task-for-collections}

1. Na página Coleções, selecione a coleção para a qual deseja criar uma tarefa de revisão.
1. Na barra de ferramentas, toque/clique no ícone **[!UICONTROL Criar tarefa de revisão]** para abrir a página **[!UICONTROL Verificar tarefa]**. Se não conseguir ver o ícone na barra de ferramentas, toque/clique em **[!UICONTROL Mais]** e selecione o ícone.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Opcional) Na lista **[!UICONTROL Projeto]** , selecione o projeto ao qual deseja associar a tarefa de revisão. Por padrão, a opção **[!UICONTROL Nenhum]** está selecionada. Se você não quiser associar qualquer projeto à tarefa de revisão, mantenha essa seleção.

   >[!NOTE]
   >
   >Somente os projetos para os quais você tem permissões no nível do Editor (ou superior) estão visíveis na lista **[!UICONTROL Projetos]** .

1. Insira um nome para a tarefa de revisão e selecione um aprovador na lista **[!UICONTROL Atribuir]** .

   >[!NOTE]
   >
   >Os membros/grupos do projeto selecionado estão disponíveis como aprovadores na lista **[!UICONTROL Atribuir]** .

1. Informe uma descrição, a prioridade da tarefa e a data de vencimento da tarefa de revisão.

   ![tarefa_details-collection](assets/task_details-collection.png)

1. Toque/clique em **[!UICONTROL Enviar]** e em **[!UICONTROL Concluído]** para fechar a mensagem de confirmação. Uma notificação para a nova tarefa é enviada ao aprovador.
1. Faça logon nos ativos AEM como aprovador e navegue até o console Ativos. Para aprovar ativos, toque/clique no ícone **[!UICONTROL Notificações]** e selecione a tarefa de revisão na lista.
1. Na página **[!UICONTROL Tarefa de revisão]**, examine os detalhes da tarefa de revisão e toque/clique em **[!UICONTROL Revisar]**.
1. Todos os ativos na coleção estão visíveis na página de revisão. Selecione os ativos e toque/clique no ícone **[!UICONTROL Aprovar/Rejeitar]** para aprovar ou rejeitar ativos, conforme apropriado.

   ![review_tarefa_collection](assets/review_task_collection.png)

1. Toque/clique no ícone **[!UICONTROL Concluído]** na barra de ferramentas. Na caixa de diálogo, digite um comentário e toque/clique em **[!UICONTROL Concluir]** para confirmar.
1. Navegue até o console Coleções e abra a coleção. Os ícones de status de aprovação dos ativos são exibidos nas visualizações Cartão e Lista.

   **Exibição de cartão**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **Exibição de lista**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

