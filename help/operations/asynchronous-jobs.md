---
title: Trabalhos assíncronos
description: O Adobe Experience Manager otimiza o desempenho ao concluir de forma assíncrona algumas tarefas que consomem muitos recursos como operações em segundo plano.
exl-id: 9c5c4604-1290-4dea-a14d-08f3ab3ef829
source-git-commit: 1a4c5e618adaef99d82a00e1118d1a0f8536fc14
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 64%

---

# Operações assíncronas {#asynchronous-operations}

Para reduzir o impacto negativo no desempenho, o Adobe Experience Manager processa de forma assíncrona determinadas operações de longa duração e operações que usam muitos recursos, como operações em segundo plano. O processamento assíncrono envolve enfileiramento de vários trabalhos e sua execução em série dependendo da disponibilidade dos recursos do sistema.

Essas operações incluem:

* Exclusão de muitos ativos
* Movimentação de muitos ativos ou ativos com muitas referências
* Exportação/importação de metadados de ativos em massa
* Busca de ativos acima do limite definido a partir de uma implantação remota do Experience Manager
* Implantação de Live Copy

Você pode visualizar o status de trabalhos assíncronos na **[!UICONTROL Operações em segundo plano]** painel em **Navegação global** > **Ferramentas** > **Geral** > **Tarefas**.

>[!NOTE]
>
>Por padrão, os trabalhos assíncronos são executados em paralelo. Se o número de núcleos da CPU for *`n`*, podem ser executados *`n/2`* trabalhos em paralelo, por padrão. Para usar configurações personalizadas para a fila de trabalhos, modifique a **[!UICONTROL Configuração da fila padrão da operação assíncrona]** e a **Configuração da movimentação e implantação de página de operação assíncrona** no console da web.
>
>Para obter mais informações, consulte [Configurações de fila](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Monitorar o status de operações assíncronas {#monitor-the-status-of-asynchronous-operations}

Sempre que o AEM processar uma operação de modo assíncrono, você receberá uma notificação na sua [caixa de entrada](/help/sites-cloud/authoring/inbox.md) e por email (se ativada essa opção).

Para visualizar o status das operações assíncronas em detalhes, navegue até o **[!UICONTROL Operações em segundo plano]** página.

1. Na interface do Experience Manager, selecione **Navegação global** > **Ferramentas** > **Geral** > **Tarefas**.

1. No **[!UICONTROL Operações em segundo plano]** verifique os detalhes das operações.

   ![Status e detalhes de operações assíncronas](assets/async-operation-status.png)

   Para determinar o progresso de uma operação específica, consulte o valor na coluna **[!UICONTROL Status]**. Dependendo do progresso, será exibido um dos seguintes status:

   * **[!UICONTROL Ativo]**: a operação está sendo processada

   * **[!UICONTROL Sucesso]**: a operação foi concluída

   * **[!UICONTROL Falha]** ou **[!UICONTROL Erro]**: não foi possível processar a operação

   * **[!UICONTROL Agendado]**: a operação está programada para ser processada mais tarde

1. Para interromper uma operação ativa, selecione-a na lista e clique em **[!UICONTROL Parar]** na barra de ferramentas.

   ![stop_icon](assets/async-stop-icon.png)

1. Para exibir detalhes adicionais, por exemplo, descrição e logs, selecione a operação e clique em **[!UICONTROL Abertura]** na barra de ferramentas.

   ![open_icon](assets/async-open-icon.png)

   A página de detalhes do trabalho é exibida.

   ![job_details](assets/async-job-details.png)

1. Para excluir a operação da lista, selecione **[!UICONTROL Excluir]** na barra de ferramentas. Para baixar os detalhes em um arquivo CSV, clique em **[!UICONTROL Baixar]**.

   >[!NOTE]
   >
   >Não é possível excluir um trabalho se o seu status for **Ativo** ou **Em fila**.

## Configuração de opções de processamento de trabalho assíncrono {#configure}

Há várias opções sobre trabalhos assíncronos que podem ser configuradas. Os exemplos a seguir mostram como isso pode ser feito usando o gerenciador de configurações em um sistema de desenvolvimento local.

>[!NOTE]
>
>[Configurações do OSGi](/help/implementing/deploying/configuring-osgi.md#creating-osgi-configurations) são considerados conteúdo mutável e qualquer uma dessas configurações deve ser implantada como um pacote de conteúdo para um ambiente de produção.

### Limpar trabalhos concluídos {#purging-completed-jobs}

O AEM executa um trabalho de limpeza todos os dias à 1h para excluir trabalhos assíncronos concluídos há mais de um dia.

Você pode modificar a programação da limpeza e a duração da retenção dos detalhes dos trabalhos concluídos, antes da sua exclusão. Você também pode configurar, a qualquer momento, o número máximo de trabalhos concluídos cujos detalhes serão retidos.

1. Faça logon no console da Web AEM do AEM do SDK do em `https://<host>:<port>/system/console` como o usuário administrador.
1. Navegue até **OSGi** > **Configuração**
1. Abra o **[!UICONTROL Trabalho agendado de limpeza de trabalhos assíncronos no Adobe Granite]**.
1. Especifique:
   * O limite de dias após o qual os trabalhos concluídos são excluídos.
   * O número máximo de trabalhos cujos detalhes são mantidos no histórico.
   * A expressão CRON que define quando a limpeza deve ser feita.

   ![Configuração para agendar a limpeza de trabalhos assíncronos](assets/async-purge-job.png)

1. Salve as alterações.

### Configurar operações assíncronas de exclusão de ativos {#configuring-synchronous-delete-operations}

Se o número de ativos ou pastas que serão excluídos exceder o limite, a operação de exclusão será feita de modo assíncrono.

1. Faça logon no console da Web AEM do AEM do SDK do em `https://<host>:<port>/system/console` como o usuário administrador.
1. Navegue até **OSGi** > **Configuração**
1. No console da Web, abra a **[!UICONTROL Configuração da fila padrão de processo assíncrono.]**
1. Na caixa **[!UICONTROL Limite de ativos]**, especifique o limite de ativos/pastas para o processamento assíncrono de operações de exclusão.

   ![Limite de exclusão de ativos](assets/async-delete-threshold.png)

1. Marque a opção **Habilitar notificação por email** para receber notificações por email sobre o status do trabalho. por exemplo, sucesso, falha.
1. Salve as alterações.

### Configurar operações assíncronas de movimentação de ativos {#configuring-asynchronous-move-operations}

Se o número de ativos/pastas ou referências que serão movidos exceder o limite, a operação de movimentação será feita de modo assíncrono.

1. Faça logon no console da Web AEM do AEM do SDK do em `https://<host>:<port>/system/console` como o usuário administrador.
1. Navegue até **OSGi** > **Configuração**
1. No console da Web, abra a **[!UICONTROL Configuração do processamento assíncrono da operação de movimentação.]**
1. Na caixa **[!UICONTROL Limite de ativos/referências]**, especifique o limite de ativos/pastas ou referências para o processamento assíncrono de operações de movimentação.

   ![Limite de movimentação do ativo](assets/async-move-threshold.png)

1. Marque a opção **Habilitar notificação por email** para receber notificações por email sobre o status do trabalho. Por exemplo, sucesso, falha.
1. Salve as alterações.

### Configurar operações assíncronas do MSM {#configuring-asynchronous-msm-operations}

1. Faça logon no console da Web AEM do AEM do SDK do em `https://<host>:<port>/system/console` como o usuário administrador.
1. Navegue até **OSGi** > **Configuração**
1. No console da Web, abra a **[!UICONTROL Configuração do processamento assíncrono da operação de movimentação de página.]**
1. Marque a opção **Habilitar notificação por email** para receber notificações por email sobre o status do trabalho. Por exemplo, sucesso, falha.

   ![Configuração do MSM](assets/async-msm.png)

1. Salve as alterações.

>[!MORELIKETHIS]
>
>* [Gerenciamento de páginas](/help/sites-cloud/authoring/sites-console/managing-pages.md)
>* [Importar e exportar metadados de ativos em massa](/help/assets/metadata-import-export.md).
>* [Usar ativos conectados para compartilhar ativos DAM de implantações remotas](/help/assets/use-assets-across-connected-assets-instances.md).
