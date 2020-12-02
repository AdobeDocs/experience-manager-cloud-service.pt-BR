---
title: Administração de instâncias de fluxo de trabalho
description: Saiba como administrar instâncias de fluxo de trabalho
translation-type: tm+mt
source-git-commit: c19079b1be36c4e87962491f263ddf97ab98f831
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---


# Administração de instâncias de fluxo de trabalho {#administering-workflow-instances}

O console de fluxo de trabalho fornece várias ferramentas para administrar instâncias de fluxo de trabalho para garantir que elas estejam sendo executadas conforme esperado.

Vários consoles estão disponíveis para administrar seus workflows. Use a [navegação global](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) para abrir o painel **Ferramentas** e selecione **Fluxo de trabalho**:

* **Modelos**: Gerenciar definições de fluxo de trabalho
* **Instâncias**: Visualização e gerenciamento de instâncias de fluxo de trabalho em execução
* **Iniciadores**: Gerenciar como os workflows devem ser iniciados
* **Arquivo**: Histórico de visualizações concluídos com êxito
* **Falhas**: Histórico de visualizações que foram concluídos com erros
* **Atribuição** automática: Configurar a atribuição automática de workflows a modelos

## Monitorando o Status das Instâncias de Fluxo de Trabalho {#monitoring-the-status-of-workflow-instances}

1. Usando Navegação, selecione **Ferramentas**, em seguida **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em andamento.

   ![wf-97](/help/sites-cloud/administering/assets/wf-97.png)


## Instâncias do Fluxo de Trabalho de Pesquisa {#search-workflow-instances}

1. Usando Navegação, selecione **Ferramentas**, em seguida **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em andamento. No painel superior, no canto esquerdo, selecione **Filtros**. Como alternativa, você pode usar os pressionamentos de teclas alt+1. A seguinte caixa de diálogo é exibida:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. Na caixa de diálogo Filtro, selecione os critérios de pesquisa do fluxo de trabalho. Você pode pesquisar com base nessas entradas:

   * Caminho da carga: Selecione um caminho específico
   * Modelo de fluxo de trabalho: Selecionar um modelo de fluxo de trabalho
   * Destinatário: Selecionar um Destinatário do fluxo de trabalho
   * Tipo: Tarefa, item de fluxo de trabalho ou falha de fluxo de trabalho
   * Status da tarefa: Ativo, concluído ou finalizado
   * Onde estou: Proprietário E Destinatário, somente Proprietário, Somente Destinatário
   * Data do start: Data do start antes ou depois de uma data especificada
   * Data final: Data final antes ou depois de uma data especificada
   * Data de Vencimento: Data de vencimento antes ou depois de uma data especificada
   * Data de atualização: Data de atualização antes ou depois de uma data especificada

## Suspendendo, Retomando e Encerrando uma Instância de Fluxo de Trabalho {#suspending-resuming-and-terminating-a-workflow-instance}

1. Usando Navegação, selecione **Ferramentas**, em seguida **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em andamento.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Selecione um item específico e use **Terminar**, **Suspender** ou **Retomar**, conforme apropriado; a confirmação e/ou outros detalhes são necessários:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

## Exibindo Workflows Arquivados {#viewing-archived-workflows}

1. Usando Navegação, selecione **Ferramentas**, em seguida **Fluxo de trabalho**.

1. Selecione **Arquivar** para exibir a lista de instâncias de fluxo de trabalho concluídas com êxito.

   ![wf-98](/help/sites-cloud/administering/assets/wf-98.png)

   >[!NOTE]
   >O status de anulação é considerado como uma terminação bem-sucedida, pois ocorre como resultado da ação do usuário; por exemplo:
   >
   >* uso da ação **Terminar**
   >* quando uma página sujeita a um fluxo de trabalho é (forçar) excluída, o fluxo de trabalho será encerrado


1. Selecione um item específico e **Abrir histórico** para ver mais detalhes:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Corrigindo Falhas de Instância de Fluxo de Trabalho {#fixing-workflow-instance-failures}

Quando um fluxo de trabalho falha, AEM fornece o console **Failures** para permitir que você investigue e execute a ação apropriada assim que a causa original for tratada:

* **Detalhes**
da falhaAbre uma janela para mostrar a variável 
**Mensagem** de falha,  **** Stepand  **Failure Stack**.

* **Abrir**
históricoMostra detalhes do histórico de fluxo de trabalho.

* **Repetir** StepExecuta a instância do componente Etapa de script novamente. Use o comando Repetir etapa depois de corrigir a causa do erro original. Por exemplo, repita a etapa depois de corrigir um bug no script que a Etapa do processo executa.
* **** TerminarEncerra o fluxo de trabalho se o erro tiver causado uma situação inconciliável para o fluxo de trabalho. Por exemplo, o fluxo de trabalho pode depender de condições ambientais, como informações no repositório que não são mais válidas para a instância do fluxo de trabalho.
* **Encerrar e** Tentar novamenteSemelhante ao  **** Encerrar, exceto que uma nova instância do fluxo de trabalho é iniciada usando a carga, o título e a descrição originais.

Para investigar falhas, retome ou encerre o fluxo de trabalho depois, use as seguintes etapas:

1. Usando Navegação, selecione **Ferramentas**, em seguida **Fluxo de trabalho**.

1. Selecione **Falhas** para exibir a lista de instâncias de fluxo de trabalho que não foram concluídas com êxito.
1. Selecione um item específico e, em seguida, a ação apropriada:

   ![wf-47](/help/sites-cloud/administering/assets/wf-47.png)

## Expurgação Regular de Instâncias de Fluxo de Trabalho {#regular-purging-of-workflow-instances}

Minimizar o número de instâncias do fluxo de trabalho aumenta o desempenho do motor de workflow, para que você possa expurgar regularmente as instâncias do fluxo de trabalho concluídas ou em execução do repositório.

Configure **Configuração de Expurgação de Fluxo de Trabalho do Adobe Granite** para expurgar instâncias de fluxo de trabalho de acordo com sua idade e status. Você também pode expurgar instâncias de fluxo de trabalho de todos os modelos ou de um modelo específico.

Você também pode criar várias configurações do serviço para expurgar instâncias de fluxo de trabalho que atendam a critérios diferentes. Por exemplo, crie uma configuração que elimine as instâncias de um modelo de fluxo de trabalho específico quando elas estiverem em execução por muito mais tempo do que o esperado. Crie outra configuração que elimine todos os workflows concluídos após um determinado número de dias para minimizar o tamanho do repositório.

Para configurar o serviço, você pode configurar os Arquivos de configuração do OSGi, consulte [Arquivos de configuração do OSGi](/help/implementing/deploying/configuring-osgi.md). A tabela a seguir descreve as propriedades necessárias para qualquer um dos métodos.

>[!NOTE]
>Para adicionar a configuração ao repositório, o PID do serviço é:
>`com.adobe.granite.workflow.purge.Scheduler`
>Como o serviço é um serviço de fábrica, o nome do nó `sling:OsgiConfig` requer um sufixo de identificador, por exemplo:
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>Nome da propriedade (Console da Web)</th>
   <th>Nome da propriedade OSGi</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Nome da tarefa</td>
   <td>scheduledpurge.name</td>
   <td>Um nome descritivo para a expurgação programada.</td>
  </tr>
  <tr>
   <td>Status do fluxo de trabalho</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>O status das instâncias do fluxo de trabalho a serem expurgadas. Os seguintes valores são válidos:</p>
    <ul>
     <li>CONCLUÍDO: As instâncias de fluxo de trabalho concluídas são removidas.</li>
     <li>EM EXECUÇÃO: A execução de instâncias de fluxo de trabalho é removida.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelos a Serem Expurgados</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>A ID dos modelos de fluxo de trabalho a serem expurgados. A ID é o caminho para o nó do modelo, por exemplo:<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> Não especifique nenhum valor para expurgar instâncias de todos os modelos de fluxo de trabalho.</p> <p>Para especificar vários modelos, clique no botão + no Console da Web. </p> </td>
  </tr>
  <tr>
   <td>Idade do fluxo de trabalho</td>
   <td>scheduledpurge.daysold</td>
   <td>A idade das instâncias do fluxo de trabalho a serem expurgadas, em dias.</td>
  </tr>
 </tbody>
</table>

## Configuração do Tamanho Máximo da Caixa de Entrada {#setting-the-maximum-size-of-the-inbox}

Você pode definir o tamanho máximo da caixa de entrada configurando o **Adobe Granite Workflow Service**, consulte [adicionar uma configuração OSGi ao repositório](/help/implementing/deploying/configuring-osgi.md). A tabela a seguir descreve a propriedade que você configura.

>[!NOTE]
>Para adicionar a configuração ao repositório, o PID do serviço é:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nome da propriedade (Console da Web) | Nome da propriedade OSGi |
|---|---|
| Tamanho Máximo do Query da Caixa de Entrada | granite.workflow.inboxQuerySize |

