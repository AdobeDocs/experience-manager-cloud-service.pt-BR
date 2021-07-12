---
title: Administração de instâncias do fluxo de trabalho
description: Saiba como administrar instâncias de fluxo de trabalho
feature: Administração
role: Admin
exl-id: d2adb5e8-3f0e-4a3b-b7d0-dbbc5450e45f
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 1%

---

# Administração de instâncias do fluxo de trabalho {#administering-workflow-instances}

O console Fluxo de trabalho fornece várias ferramentas para administrar instâncias do fluxo de trabalho, para garantir que elas estejam em execução conforme esperado.

Há vários consoles disponíveis para administrar seus fluxos de trabalho. Use o [navegação global](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) para abrir o painel **Ferramentas** e selecione **Fluxo de trabalho**:

* **Modelos**: Gerenciar definições de fluxo de trabalho
* **Instâncias**: Exibir e gerenciar a execução de instâncias de fluxo de trabalho
* **Iniciadores**: Gerenciar como os workflows devem ser iniciados
* **Arquivar**: Exibir o histórico de fluxos de trabalho concluídos com êxito
* **Falhas**: Exibir o histórico de fluxos de trabalho concluídos com erros
* **Atribuição** automática: Configurar workflows de atribuição automática para modelos

## Monitorar o status de instâncias de fluxo de trabalho {#monitoring-the-status-of-workflow-instances}

1. Usando Navegação, selecione **Ferramentas**, em seguida **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho que estão em andamento.

   ![wf-97](/help/sites-cloud/administering/assets/wf-97.png)


## Pesquisar instâncias do fluxo de trabalho {#search-workflow-instances}

1. Usando Navegação, selecione **Ferramentas**, em seguida **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho que estão em andamento. No painel superior, no canto esquerdo, selecione **Filters**. Como alternativa, você pode usar os pressionamentos de tecla alt+1. A seguinte caixa de diálogo é exibida:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. Na caixa de diálogo Filtro , selecione os critérios de pesquisa do fluxo de trabalho. Você pode pesquisar com base nessas entradas:

   * Caminho da carga: Selecionar um caminho específico
   * Modelo de fluxo de trabalho: Selecionar um modelo de fluxo de trabalho
   * Destinatário: Selecionar um Destinatário do fluxo de trabalho
   * Tipo: Tarefa, item de fluxo de trabalho ou falha de fluxo de trabalho
   * Status da tarefa: Ativo, concluído ou encerrado
   * Onde Estou: Proprietário E Destinatário, somente Proprietário, Somente Destinatário
   * Data de início: Data inicial antes ou depois de uma data especificada
   * Data final: Data final antes ou depois de uma data especificada
   * Data de Vencimento: Data de vencimento antes ou depois de uma data especificada
   * Data de atualização: Data atualizada antes ou depois de uma data especificada

## Suspensão, retomada e Encerramento de uma Instância de Fluxo de Trabalho {#suspending-resuming-and-terminating-a-workflow-instance}

1. Usando Navegação, selecione **Ferramentas**, em seguida **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho que estão em andamento.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Selecione um item específico e use **Terminar**, **Suspender** ou **Retomar**, conforme apropriado; é necessária confirmação e/ou mais pormenores:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

## Visualização de fluxos de trabalho arquivados {#viewing-archived-workflows}

1. Usando Navegação, selecione **Ferramentas**, em seguida **Fluxo de trabalho**.

1. Selecione **Arquivar** para exibir a lista de instâncias de fluxo de trabalho concluídas com êxito.

   ![wf-98](/help/sites-cloud/administering/assets/wf-98.png)

   >[!NOTE]
   >O status abort é considerado como uma terminação bem-sucedida, pois ocorre como resultado da ação do usuário; por exemplo:
   >
   >* uso da ação **Terminar**
   >* quando uma página, que está sujeita a um fluxo de trabalho, é (forçar) excluída, o fluxo de trabalho será encerrado


1. Selecione um item específico e **Abrir Histórico** para ver mais detalhes:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Correção de falhas na instância do fluxo de trabalho {#fixing-workflow-instance-failures}

Quando um workflow falha, o AEM fornece o console **Falhas** para permitir que você investigue e tome as medidas apropriadas quando a causa original tiver sido tratada:

* **Falha em**
DetalhesAbre uma janela para mostrar a 
**Mensagem** de falha,  **** empilhar pilha  **de falhas**.

* **Open**
HistoryMostra detalhes do histórico do fluxo de trabalho.

* **Repetir** StepExecuta a instância do componente Etapa do Script novamente. Use o comando Repetir etapa após corrigir a causa do erro original. Por exemplo, tente novamente a etapa depois de corrigir um erro no script que a Etapa do processo executa.
* **** TerminateEncerra o workflow se o erro tiver causado uma situação inreconciliável para o workflow. Por exemplo, o workflow pode depender de condições ambientais, como informações no repositório que não são mais válidas para a instância do workflow.
* **Encerrar e** Tentar novamenteSemelhante a  **** Terminar, exceto que uma nova instância de fluxo de trabalho é iniciada usando a carga, o título e a descrição originais.

Para investigar falhas e, em seguida, retomar ou encerrar o fluxo de trabalho depois, use as seguintes etapas:

1. Usando Navegação, selecione **Ferramentas**, em seguida **Fluxo de trabalho**.

1. Selecione **Falhas** para exibir a lista de instâncias de fluxo de trabalho que não foram concluídas com êxito.
1. Selecione um item específico e, em seguida, a ação apropriada:

   ![wf-47](/help/sites-cloud/administering/assets/wf-47.png)

## Limpeza regular de instâncias de fluxo de trabalho {#regular-purging-of-workflow-instances}

Minimizar o número de instâncias de fluxo de trabalho aumenta o desempenho do mecanismo de fluxo de trabalho, para que você possa limpar regularmente as instâncias de fluxo de trabalho concluídas ou em execução do repositório.

Configure **Adobe Granite Workflow Purge Configuration** para limpar instâncias de fluxo de trabalho de acordo com sua idade e status. Você também pode limpar instâncias de fluxo de trabalho de todos os modelos ou de um modelo específico.

Você também pode criar várias configurações do serviço para limpar instâncias de fluxo de trabalho que satisfaçam critérios diferentes. Por exemplo, crie uma configuração que limpe as instâncias de um modelo de fluxo de trabalho específico quando elas estiverem em execução por muito mais tempo do que o tempo esperado. Crie outra configuração que elimine todos os workflows concluídos após um determinado número de dias para minimizar o tamanho do repositório.

Para configurar o serviço, você pode configurar os Arquivos de Configuração do OSGi, consulte [Arquivos de configuração do OSGi](/help/implementing/deploying/configuring-osgi.md). A tabela a seguir descreve as propriedades necessárias para qualquer método.

>[!NOTE]
>Para adicionar a configuração ao repositório, o PID do serviço é:
>`com.adobe.granite.workflow.purge.Scheduler`
>Como o serviço é um serviço de fábrica, o nome do nó `sling:OsgiConfig` requer um sufixo identificador, por exemplo:
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>Nome da propriedade (Console da Web)</th>
   <th>Nome da Propriedade OSGi</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Nome da tarefa</td>
   <td>scheduledpurge.name</td>
   <td>Um nome descritivo para a limpeza agendada.</td>
  </tr>
  <tr>
   <td>Status do fluxo de trabalho</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>O status das instâncias do fluxo de trabalho a serem removidas. Os seguintes valores são válidos:</p>
    <ul>
     <li>CONCLUÍDO: As instâncias de fluxo de trabalho concluídas são removidas.</li>
     <li>EM EXECUÇÃO: A execução de instâncias de fluxo de trabalho é eliminada.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelos a serem limpos</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>A ID dos modelos de fluxo de trabalho a serem limpos. A ID é o caminho para o nó do modelo, por exemplo:<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> Especifique nenhum valor para limpar instâncias de todos os modelos de fluxo de trabalho.</p> <p>Para especificar vários modelos, clique no botão + no Console da Web. </p> </td>
  </tr>
  <tr>
   <td>Idade do fluxo de trabalho</td>
   <td>scheduledpurge.daysold</td>
   <td>A idade das instâncias do fluxo de trabalho a serem removidas, em dias.</td>
  </tr>
 </tbody>
</table>

## Configuração do tamanho máximo da caixa de entrada {#setting-the-maximum-size-of-the-inbox}

Você pode definir o tamanho máximo da caixa de entrada configurando o **Adobe Granite Workflow Service**, consulte [adicionar uma configuração OSGi ao repositório](/help/implementing/deploying/configuring-osgi.md). A tabela a seguir descreve a propriedade configurada.

>[!NOTE]
>Para adicionar a configuração ao repositório, o PID do serviço é:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nome da propriedade (Console da Web) | Nome da Propriedade OSGi |
|---|---|
| Tamanho máximo da consulta da caixa de entrada | granite.workflow.inboxQuerySize |
