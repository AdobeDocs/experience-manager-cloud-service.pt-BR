---
title: Administração de instâncias do fluxo de trabalho
description: Saiba como administrar instâncias de fluxo de trabalho usando o console de fluxo de trabalho
feature: Administering
role: Admin
exl-id: d2adb5e8-3f0e-4a3b-b7d0-dbbc5450e45f
solution: Experience Manager Sites
source-git-commit: 372d8969b1939e9a24d7910a1678a17c0dc9f9fd
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 90%

---

# Administração de instâncias do fluxo de trabalho {#administering-workflow-instances}

O console do fluxo de trabalho fornece várias ferramentas para administrar instâncias do fluxo de trabalho e garantir que elas estejam em execução conforme esperado.

Há vários consoles disponíveis para administrar seus fluxos de trabalho. Use a [navegação global](/help/sites-cloud/authoring/basic-handling.md#global-navigation) para abrir o painel **Ferramentas** e selecione **Fluxo de trabalho**:

* **Modelos**: gerenciar definições de fluxo de trabalho
* **Instâncias**: exibir e gerenciar instâncias de fluxos de trabalho em execução
* **Iniciadores**: gerenciar o modo como os fluxos de trabalho devem ser inicializados
* **Arquivo**: exibir o histórico de fluxos de trabalho que foram concluídos com sucesso
* **Falhas**: exibir o histórico de fluxos de trabalho que foram concluídos com erros
* **Atribuição automática**: configurar a atribuição automática de fluxos de trabalho aos modelos

## Monitorar o status de instâncias de fluxo de trabalho {#monitoring-the-status-of-workflow-instances}

1. Usando a navegação, selecione **Ferramentas** e, em seguida, **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em execução.
1. No painel superior, no canto direito, as instâncias de fluxo de trabalho mostram os **fluxos de trabalho em execução**, o **status** e **detalhes**.
1. **Fluxos de trabalho em execução** mostra o número de fluxos de trabalho em execução e o status deles. por exemplo, nas imagens fornecidas, são mostrados o número de **fluxos de trabalho em execução** e o **status** da instância do AEM:

   * **Status: íntegro**
     ![status-healthy](/help/sites-cloud/administering/assets/status-healthy.png)

   * **Status: não íntegro**
     ![status-unhealthy](/help/sites-cloud/administering/assets/status-unhealthy.png)

1. Para obter os **detalhes do status** de instâncias de fluxo de trabalho, clique em **Detalhes** e as seguintes informações serão exibidas: **número de instâncias de fluxos de trabalho em execução**, **instâncias de fluxos de trabalho concluídos**, **instâncias de fluxos de trabalho interrompidos**, **instâncias de fluxos de trabalho com falha**, entre outros. por exemplo, abaixo estão as imagens fornecidas que mostram os **Detalhes do status** com:

   * **Detalhes do status: Íntegro**
     ![status-details-healthy](/help/sites-cloud/administering/assets/status-details-healthy.png)

   * **Detalhes do status: não íntegro**
     ![status-details-unhealthy](/help/sites-cloud/administering/assets/status-details-unhealthy.png)

   >[!NOTE]
   >
   > Para manter a integridade da instância de fluxo de trabalho, siga as práticas recomendadas de [limpeza regular de instâncias de fluxo de trabalho](#regular-purging-of-workflow-instances) ou as [práticas recomendadas de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-best-practices.html?lang=pt-BR).

## Pesquisar instâncias de fluxo de trabalho {#search-workflow-instances}

1. Usando a navegação, selecione **Ferramentas** e, em seguida, **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em andamento. No painel superior, no canto esquerdo, selecione **Filtros**. Como alternativa, você pode pressionar as teclas Alt+1. A seguinte caixa de diálogo é exibida:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. Na caixa de diálogo Filtro, selecione os critérios de pesquisa do fluxo de trabalho. Você pode pesquisar com base nessas entradas:

   * Caminho da carga: selecionar um caminho específico
   * Modelo de fluxo de trabalho: selecionar um modelo de fluxo de trabalho
   * Destinatário: selecionar um destinatário do fluxo de trabalho
   * Tipo: tarefa, item do fluxo de trabalho ou falha do fluxo de trabalho
   * Status da tarefa: ativo, concluído ou encerrado
   * Onde estou: proprietário AND destinatário, somente proprietário, somente destinatário
   * Data inicial: data inicial anterior ou posterior a uma data especificada
   * Data final: Data final anterior ou posterior a uma data especificada
   * Data de vencimento: data de vencimento anterior ou posterior a uma data especificada
   * Data atualizada: data atualizada anterior ou posterior a uma data especificada

## Suspensão, retomada e encerramento de uma instância de fluxo de trabalho {#suspending-resuming-and-terminating-a-workflow-instance}

1. Usando a navegação, selecione **Ferramentas** e, em seguida, **Fluxo de trabalho**.
1. Selecione **Instâncias** para exibir a lista de instâncias de fluxo de trabalho em andamento.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Selecione um item específico e use **Encerrar**, **Suspender** ou **Retomar**, conforme adequado; é necessária uma confirmação e/ou outros pormenores:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

   >[!NOTE]
   >
   >
   >Para encerrar ou interromper um fluxo de trabalho, ele deve ter sido colocado em um estado de espera pelo usuário, como em uma etapa do participante. A tentativa de abortar um fluxo de trabalho que está executando processos (threads ativos que estão em execução) pode não produzir os resultados esperados.


## Visualização de fluxos de trabalho arquivados {#viewing-archived-workflows}

1. Usando a navegação, selecione **Ferramentas** e, em seguida, **Fluxo de trabalho**.

1. Selecione **Arquivo** para exibir a lista de instâncias de fluxo de trabalho concluídas com sucesso.

   ![archived-instances](/help/sites-cloud/administering/assets/archived-instances.png)

   >[!NOTE]
   >
   >
   >O status interrompido é considerado um encerramento bem-sucedido, pois ocorre como resultado da ação do usuário; por exemplo:
   >
   >* o uso da ação **Encerrar**
   >* quando uma página que está sujeita a um fluxo de trabalho é excluída (à força), o fluxo de trabalho é encerrado.

1. Selecione um item específico e **Abra o histórico** para ver mais detalhes:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Correção de falhas na instância do fluxo de trabalho {#fixing-workflow-instance-failures}

Quando um fluxo de trabalho falha, o AEM fornece o console **Falhas**, que permite investigar e tomar as medidas apropriadas após tratar a causa original:

* **Detalhes da falha**
Abre uma janela para mostrar a **Mensagem de Falha**, **Etapa e &#x200B;** Pilha de Falhas**.

* **Abrir histórico**
Mostra detalhes do histórico do fluxo de trabalho.

* **Repetir etapa** Executa a instância do componente Etapa do script novamente. Use o comando Repetir etapa após corrigir a causa do erro original. Por exemplo, repita a etapa depois de corrigir um erro no script que a Etapa do processo executa.
* **Encerrar** Encerra o fluxo de trabalho se o erro tiver gerado uma situação irreparável para o fluxo de trabalho. Por exemplo, o fluxo de trabalho pode depender de condições ambientais, como informações no repositório que não são mais válidas para a instância do fluxo de trabalho.
* **Encerrar e tentar novamente**: semelhante a **Encerrar**, exceto que uma nova instância de fluxo de trabalho é iniciada usando o conteúdo, o título e a descrição originais.

Para investigar falhas e, em seguida, retomar ou encerrar o fluxo de trabalho, use as seguintes etapas:

1. Usando a navegação, selecione **Ferramentas** e, em seguida, **Fluxo de trabalho**.

1. Selecione **Falhas** para exibir a lista de instâncias de fluxo de trabalho que não foram concluídas com sucesso.
1. Selecione um item específico e, em seguida, a ação apropriada:

![workflow-failure](/help/sites-cloud/administering/assets/workflow-failure.png)

## Limpeza regular de instâncias de fluxo de trabalho {#regular-purging-of-workflow-instances}

Minimizar o número de instâncias de fluxo de trabalho aumenta o desempenho do motor de workflow. Portanto, você pode remover regularmente do repositório as instâncias de fluxo de trabalho concluídas ou em execução.

Defina a **configuração de limpeza de fluxos de trabalho do Adobe Granite** para remover instâncias de fluxo de trabalho de acordo com sua idade e status. Você também pode remover as instâncias de fluxo de trabalho de todos os modelos ou de um modelo específico.

Você também pode criar várias configurações do serviço para remover as instâncias de fluxo de trabalho que satisfaçam critérios diferentes. Por exemplo, crie uma configuração que remova as instâncias de um modelo de fluxo de trabalho específico quando elas estiverem em execução por muito mais tempo do que o esperado. Crie outra configuração que remova todos os fluxos de trabalho concluídos após um determinado número de dias para minimizar o tamanho do repositório.

Para configurar o serviço, você pode definir os arquivos de configuração do OSGi. Consulte [Arquivos de configuração do OSGi](/help/implementing/deploying/configuring-osgi.md). A tabela a seguir descreve as propriedades necessárias para qualquer método.

>[!NOTE]
>Para adicionar a configuração ao repositório, o PID do serviço é:
>`com.adobe.granite.workflow.purge.Scheduler`
>Como o serviço é de fábrica, o nome do nó `sling:OsgiConfig` requer um sufixo identificador. Por exemplo:
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

| Nome da propriedade (console da Web) | Nome da propriedade OSGi | Descrição |
|--- |--- |--- |
| Nome da tarefa  | `scheduledpurge.name` | Um nome descritivo para a limpeza agendada. |
| Status do fluxo de trabalho | `scheduledpurge.workflowStatus` | O status das instâncias de fluxo de trabalho a serem removidas. Os seguintes valores são válidos:<br><br>- CONCLUÍDO: as instâncias de fluxo de trabalho concluídas são removidas.<br>- EM EXECUÇÃO: as instâncias de fluxo de trabalho em execução são removidas. |
| Modelos a remover | `scheduledpurge.modelIds` | A ID dos modelos de fluxo de trabalho a serem removidos.<br>A ID é o caminho para o nó do modelo, por exemplo:<br> `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model` <br><br> Não especifique nenhum valor para remover instâncias de todos os modelos de fluxo de trabalho.<br>Para especificar vários modelos, clique no botão `+` no Console da Web. |
| Idade do fluxo de trabalho | `scheduledpurge.daysold` | A idade das instâncias de fluxo de trabalho a serem removidas, em dias. |
| Pacote de carga do fluxo de trabalho | `scheduledpurge.purgePackagePayload` | Indica se o pacote de carga deve ser limpo; `true` ou `false`. |


## Configuração do tamanho máximo da caixa de entrada {#setting-the-maximum-size-of-the-inbox}

É possível definir o tamanho máximo da caixa de entrada configurando o **Serviço de fluxo de trabalho do Adobe Granite**. Consulte [adicionar uma configuração OSGi ao repositório](/help/implementing/deploying/configuring-osgi.md). A tabela a seguir descreve a propriedade que você configura.

>[!NOTE]
>Para adicionar a configuração ao repositório, o PID do serviço é:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nome da propriedade (console da Web) | Nome da propriedade OSGi |
|---|---|
| Tamanho máximo da consulta da caixa de entrada | granite.workflow.inboxQuerySize |

## Uso de variáveis de fluxo de trabalho para armazenamentos de dados de propriedade do cliente {#using-workflow-variables-customer-datastore}

Os dados processados por fluxos de trabalho são armazenados no armazenamento fornecido pela Adobe (JCR). Esses dados podem ser de natureza sensível. É recomendado salvar todos os metadados/dados definidos pelo usuário em seu próprio armazenamento gerenciado, em vez de usar o armazenamento fornecido pela Adobe. Essas seções descrevem como configurar essas variáveis em um armazenamento externo.

### Definir o modelo para usar o armazenamento externo de metadados {#set-model-for-external-storage}

No nível do modelo de fluxo de trabalho, um sinalizador é fornecido para indicar que o modelo e suas instâncias de tempo de execução têm acesso ao armazenamento externo de metadados. As variáveis de fluxo de trabalho não serão mantidas no JCR para as instâncias de fluxo de trabalho cujos modelos foram marcados para armazenamento externo.

A propriedade *userMetadataPersistenceEnabled* está armazenada no nó *jcr:content* do modelo de fluxo de trabalho. Esse sinalizador é mantido nos metadados do fluxo de trabalho como *cq:userMetaDataCustomPersistenceEnabled*.

A ilustração abaixo mostra como definir o sinalizador em um fluxo de trabalho.

![workflow-externalize-config](/help/sites-cloud/administering/assets/workflow-externalize-config.png)

### APIs de metadados no armazenamento externo {#apis-for-metadata-external-storage}

Para armazenar as variáveis externamente, você deve implementar as APIs que o fluxo de trabalho expõe.

UserMetaDataPersistenceContext

Os exemplos a seguir mostram como usar a API.

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
} 
```
