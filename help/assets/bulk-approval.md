---
title: Revisar ativos em pastas e coleções
description: Configure fluxos de trabalho de revisão para ativos em uma pasta ou coleção e compartilhe-os com revisores ou parceiros criativos para buscar feedback.
contentOwner: AG
feature: Collections, Collaboration
role: User
exl-id: 1e5bdd66-2707-4584-87ed-a0ff1bde3718
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 9%

---

# Revisar ativos em pastas e coleções {#review-folder-assets-and-collections}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/bulk-approval.html?lang=en) |
| AEM as a Cloud Service | Este artigo |

Usando o Adobe Experience Manager Assets, você pode definir fluxos de trabalho de revisão ad hoc para ativos que estão em uma pasta ou coleção. Você pode compartilhá-lo com revisores ou parceiros criativos para buscar seus comentários. Você pode associar um fluxo de trabalho de revisão a um projeto ou criar uma tarefa de revisão independente.

Depois que você compartilhar os ativos, os revisores podem aprová-los ou rejeitá-los. As notificações são enviadas em vários estágios do fluxo de trabalho para notificar os destinatários sobre a conclusão de várias tarefas. Por exemplo, quando você compartilha uma pasta ou coleção, o revisor recebe uma notificação de que uma pasta/coleção foi compartilhada para revisão.

Depois que o revisor concluir a revisão (aprovar ou rejeitar ativos), você receberá uma notificação de conclusão da revisão.

## Criando uma tarefa de revisão para pastas {#creating-a-review-task-for-folders}

1. Na interface do usuário do Assets, selecione a pasta para a qual deseja criar uma tarefa de revisão.
1. Na barra de ferramentas, selecione o **[!UICONTROL Criar tarefa de análise]** ícone para abrir o **[!UICONTROL Tarefa de análise]** página. Se não conseguir ver o ícone na barra de ferramentas, selecione **[!UICONTROL Mais]** e, em seguida, selecione o ícone.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Opcional) No **[!UICONTROL Projeto]** selecione o projeto ao qual deseja associar a tarefa de revisão. Por padrão, a variável **[!UICONTROL Nenhum]** for selecionada. Se não quiser associar nenhum projeto à tarefa de revisão, mantenha essa seleção.

   >[!NOTE]
   >
   >Somente os projetos para os quais você tem permissões de nível de Editor (ou superiores) ficam visíveis na **[!UICONTROL Projetos]** lista.

1. Informe um nome para a tarefa de revisão e selecione um aprovador na **[!UICONTROL Atribuir a]** lista.

   >[!NOTE]
   >
   >Os membros/grupos do projeto selecionado estão disponíveis como aprovadores na **[!UICONTROL Atribuir a]** lista.

1. Insira uma descrição, a prioridade da tarefa e a data de vencimento da tarefa de revisão.

   ![task_details](assets/task_details.png)

1. Na guia Advanced, insira um rótulo a ser usado para criar o URI.

   ![review_name](assets/review_name.png)

1. Selecionar **[!UICONTROL Enviar]** e selecione **[!UICONTROL Concluído]** para fechar a mensagem de confirmação. Uma notificação para a nova tarefa é enviada ao aprovador.
1. Efetue logon no [!DNL Experience Manager Assets] como Aprovador e navegue até a interface do usuário do Assets. Para aprovar ativos, selecione o **[!UICONTROL Notificação]** e selecione a tarefa de revisão na lista.

   ![notificação](assets/notification.png)

1. No **[!UICONTROL Tarefa de análise]** página, examine os detalhes da tarefa de revisão e selecione **[!UICONTROL Revisão]**.
1. No **[!UICONTROL Tarefa de análise]** selecione ativos e selecione a variável **[!UICONTROL Aprovar/Rejeitar]** ícone para aprovar ou rejeitar, conforme apropriado.

   ![review_task](assets/review_task.png)

1. Selecione o **[!UICONTROL Concluído]** ícone na barra de ferramentas. Na caixa de diálogo, insira um comentário e selecione  **[!UICONTROL Concluído]** para confirmar.
1. Navegue até a interface do usuário do Assets e abra a pasta. Os ícones de status de aprovação dos ativos aparecem nas exibições Cartão e Lista.

   **Exibição de cartão**

   ![chlimage_1-404](assets/chlimage_1-404.png)

   **Exibição de lista**

   ![review_status_listview](assets/review_status_listview.png)

## Criação de uma tarefa de revisão para coleções {#creating-a-review-task-for-collections}

1. Na página Coleções, selecione a coleção para a qual deseja criar uma tarefa de revisão.
1. Na barra de ferramentas, selecione o **[!UICONTROL Criar tarefa de análise]** ícone para abrir o **[!UICONTROL Tarefa de análise]** página. Se não conseguir ver o ícone na barra de ferramentas, selecione **[!UICONTROL Mais]** e, em seguida, selecione o ícone.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Opcional) No **[!UICONTROL Projeto]** selecione o projeto ao qual deseja associar a tarefa de revisão. Por padrão, a variável **[!UICONTROL Nenhum]** for selecionada. Se não quiser associar nenhum projeto à tarefa de revisão, mantenha essa seleção.

   >[!NOTE]
   >
   >Somente os projetos para os quais você tem permissões de nível de Editor (ou superiores) ficam visíveis na **[!UICONTROL Projetos]** lista.

1. Informe um nome para a tarefa de revisão e selecione um aprovador na **[!UICONTROL Atribuir a]** lista.

   >[!NOTE]
   >
   >Os membros/grupos do projeto selecionado estão disponíveis como aprovadores na **[!UICONTROL Atribuir a]** lista.

1. Insira uma descrição, a prioridade da tarefa e a data de vencimento da tarefa de revisão.

   ![task_details-collection](assets/task_details-collection.png)

1. Selecionar **[!UICONTROL Enviar]** e selecione **[!UICONTROL Concluído]** para fechar a mensagem de confirmação. Uma notificação para a nova tarefa é enviada ao aprovador.
1. Efetue logon no [!DNL Experience Manager Assets] como Aprovador e navegue até o console de Ativos. Para aprovar ativos, selecione o **[!UICONTROL Notificação]** e selecione a tarefa de revisão na lista.
1. No **[!UICONTROL Tarefa de análise]** página, examine os detalhes da tarefa de revisão e selecione **[!UICONTROL Revisão]**.
1. Todos os ativos na coleção estão visíveis na página de revisão. Selecione os ativos e selecione a variável **[!UICONTROL Aprovar/Rejeitar]** ícone para aprovar ou rejeitar ativos, conforme apropriado.

   ![review_task_collection](assets/review_task_collection.png)

1. Selecione o **[!UICONTROL Concluído]** ícone na barra de ferramentas. Na caixa de diálogo, insira um comentário e selecione **[!UICONTROL Concluído]** para confirmar.
1. Navegue até o console Coleções e abra a coleção. Os ícones de status de aprovação dos ativos aparecem nas exibições Cartão e Lista.

   **Exibição de cartão**

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   **Exibição de lista**

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar ativos no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
