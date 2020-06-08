---
title: Operações assíncronas
description: AEM Assets optimizes performance by asynchronously completing some resource-intensive tasks.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 9%

---


# Operações assíncronas {#asynchronous-operations}

To reduce adverse impact on performance, Adobe Experience Manger (AEM) Assets processes certain long-running and resource-intensive asset operations asynchronously.

These operations include:

* Deleting many assets
* Movimentação de muitos ativos ou ativos com muitas referências
* Exportar/importar metadados de ativos em massa.
* Fetching assets, that are above the threshold limit set, from a remote AEM deployment.

Asynchronous processing involves enqueuing multiple jobs and eventually running them in a serial manner subject to the availability of system resources.

Você pode visualização o status de trabalhos assíncronos na página Status **[!UICONTROL do trabalho]** assíncrono.

>[!NOTE]
>
>By default, jobs in AEM Assets run in parallel. If N is the number of CPU cores, N/2 jobs can run in parallel, by default. Para usar configurações personalizadas para a fila de trabalhos, modifique a configuração da Fila **padrão de operação** assíncrona do console da Web. For more information, see [Queue Configurations](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Monitoring the status of asynchronous operations {#monitoring-the-status-of-asynchronous-operations}

Whenever AEM Assets processes an operation asynchronously, you receive a notification at your inbox <!-- and through email -->.

Para visualização o status das operações assíncronas em detalhes, navegue até a página Status **[!UICONTROL do trabalho]** assíncrono.

1. Toque/clique no logotipo do AEM e acesse **[!UICONTROL Ativos]** > **[!UICONTROL Trabalhos]**.
1. Na página Status **[!UICONTROL do trabalho]** assíncrono, reveja os detalhes das operações.

   ![job_status](assets/job_status.png)

   Para verificar o progresso de uma operação específica, consulte o valor na coluna **[!UICONTROL Status]** . Dependendo do progresso, um dos seguintes status é exibido:

   **[!UICONTROL Ativo]**: A operação está sendo processada

   **[!UICONTROL Sucesso]**: A operação está concluída

   **[!UICONTROL Falha]** ou **[!UICONTROL erro]**: não foi possível processar a operação

   **[!UICONTROL Agendado]**: A operação está programada para processamento posterior

1. Para interromper uma operação ativa, selecione-a na lista e toque/clique no ícone **[!UICONTROL Parar]** na barra de ferramentas.

   ![stop_icon](assets/stop_icon.png)

1. Para visualização de detalhes adicionais, por exemplo, descrição e registros, selecione a operação e toque/clique no ícone **[!UICONTROL Abrir]** na barra de ferramentas.

   ![open_icon](assets/open_icon.png)

   The job details page is displayed.

   ![job_details](assets/job_details.png)

1. Para excluir a operação da lista, selecione **[!UICONTROL Excluir]** na barra de ferramentas. Para baixar os detalhes em um arquivo CSV, toque/clique no ícone **[!UICONTROL Download]** .

   >[!NOTE]
   >
   >Não é possível excluir um trabalho se seu status estiver ativo ou na fila.

## Expurgando trabalhos concluídos {#purging-completed-jobs}

Os ativos AEM executam um trabalho de limpeza todos os dias às 13:00 da manhã para excluir trabalhos assíncronos concluídos que têm mais de um dia.

Você pode modificar a programação para a ordem de produção de expurgação e a duração para a qual os detalhes das ordens de produção concluídas são retidos antes de serem deletados. Você também pode configurar o número máximo de trabalhos concluídos para os quais os detalhes são retidos a qualquer momento.

1. Toque/clique no logotipo do AEM e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. Abra o trabalho **[!UICONTROL Adobe CQ DAM Async Jobs para Expurgar agendado]** .
1. Especifique o número limite de dias após o qual as tarefas concluídas são excluídas e o número máximo de trabalhos para os quais os detalhes são mantidos no histórico.

   ![Configuração para agendar a remoção de trabalhos assíncronos](assets/configmgr_purge_asyncjobs.png)
   *Figura: Configuração para agendar a remoção de trabalhos assíncronos*

1. Salve as alterações.

## Configurar limites para processamento assíncrono {#configuring-thresholds-for-asynchronous-processing}

Você pode configurar o número limite de ativos ou referências para que os ativos AEM processem uma determinada operação de forma assíncrona.

### Configurar limites para operações de exclusão assíncronas {#configuring-thresholds-for-asynchronous-delete-operations}

If the number of assets or folders to be deleted exceed the threshold number, the delete operation is performed asynchronously.

1. Toque/clique no logotipo do AEM e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. From the web console, open the **[!UICONTROL Async Delete Operation Job Processing]** configuration.
1. In the **[!UICONTROL Threshold number of assets]** box, specify the threshold number of assets/folders for asynchronous processing of delete operations.

   ![delete_threshold](assets/delete_threshold.png)

1. Salve as alterações.

### Configuring thresholds for asynchronous move operations {#configuring-thresholds-for-asynchronous-move-operations}

If the number of assets/folders or references to be moved exceed the threshold number, the move operation is performed asynchronously.

1. Toque/clique no logotipo do AEM e acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. From the web console, open the **[!UICONTROL Async Move Operation Job Processing]** configuration.
1. In the **[!UICONTROL Threshold number of assets/references]** box, specify the threshold number of assets/folders or references for asynchronous processing of move operations.

   ![move_threshold](assets/move_threshold.png)

1. Salve as alterações.
