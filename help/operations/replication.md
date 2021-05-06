---
title: Replicação
description: Distribuição e Solução de problemas de replicação.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
translation-type: tm+mt
source-git-commit: eb92c66f2b9e8e6ec859114da2de049747ec251e
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 2%

---

# Replicação {#replication}

O Adobe Experience Manager as a Cloud Service usa o recurso [Distribuição de conteúdo de sling](https://sling.apache.org/documentation/bundles/content-distribution.html) para mover o conteúdo para replicar para um serviço de pipeline executado no Adobe I/O que está fora do tempo de execução AEM.

>[!NOTE]
>
>Leia [Distribution](/help/core-concepts/architecture.md#content-distribution) para obter mais informações.

## Métodos de publicação de conteúdo {#methods-of-publishing-content}

### Publicação/Cancelamento Rápido - Planejado {#publish-unpublish}

Essas funcionalidades de AEM padrão para os autores não são alteradas com AEM Cloud Service.

### Tempos de ativação e desativação - Configuração do acionador {#on-and-off-times-trigger-configuration}

As possibilidades adicionais de **No Tempo** e **Tempo desligado** estão disponíveis na guia [Básico das Propriedades da página](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic).

Para realizar a replicação automática para isso, você precisa ativar a **Replicação automática** na [configuração OSGi](/help/implementing/deploying/configuring-osgi.md) **Configuração do Acionador Desligado**:

![Configuração do Acionador Desligado do OSGi](/help/operations/assets/replication-on-off-trigger.png)

### Ativação de árvore {#tree-activation}

Para executar uma ativação de árvore:

1. No menu Iniciar AEM, navegue até **Ferramentas > Implantação > Distribuição**
2. Selecione o cartão **forwardPublisher**
3. Uma vez na interface do console da Web do forwardPublisher, **selecione Distribuir**

   ![](assets/distribute.png "DistribuirDistribuir")
4. Selecione o caminho no navegador de caminho, escolha adicionar um nó, árvore ou excluir conforme necessário e selecione **Enviar**

### Fluxo de trabalho da árvore de conteúdo de publicação {#publish-content-tree-workflow}

Você pode acionar uma replicação de árvore escolhendo **Ferramentas - Fluxo de trabalho - Modelos** e copiando o modelo de fluxo de trabalho pronto para uso **Publicar árvore de conteúdo**, conforme mostrado abaixo:

![](/help/operations/assets/publishcontenttreeworkflow.png)

Não modifique ou chame o modelo original. Em vez disso, primeiro copie o modelo e depois modifique ou chame essa cópia.

Como todos os workflows, também é possível invocá-los por meio da API. Para obter mais informações, consulte [Interagir com workflows programaticamente](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem).

Como alternativa, você também pode fazer isso criando um Modelo de fluxo de trabalho que usa a etapa do processo `Publish Content Tree`:

1. Na página inicial do AEM as a Cloud Service, vá para **Ferramentas - Fluxo de trabalho - Modelos**
1. Na página Modelos de fluxo de trabalho , pressione **Create** no canto superior direito da tela
1. Adicione um título e um nome ao modelo. Para obter mais informações, consulte [Criação de modelos de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)
1. Selecione o modelo recém-criado na lista e pressione **Edit**
1. Na janela a seguir, arraste e solte a Etapa do processo no fluxo do modelo atual:

   ![Etapa do processo](/help/operations/assets/processstep.png)

1. Clique na etapa Processo no fluxo e selecione **Configurar** pressionando o ícone da chave inglesa
1. Clique na guia **Process** e selecione `Publish Content Tree` na lista suspensa

   ![Treeativation](/help/operations/assets/newstep.png)

1. Defina quaisquer parâmetros adicionais no campo **Argumentos**. Vários argumentos separados por vírgula podem ser stringidos juntos. Por exemplo:

   `enableVersion=true,agentId=publish`


   >[!NOTE]
   >
   >Para obter a lista de parâmetros, consulte a seção **Parameters** abaixo.

1. Pressione **Concluído** para salvar o modelo de Fluxo de trabalho.

**Parâmetros**

* `replicateAsParticipant` (valor booleano, padrão:  `false`). Se configurado como `true`, a replicação está usando o `userid` do principal que executou a etapa do participante.
* `enableVersion` (valor booleano, padrão:  `true`). Esse parâmetro determina se uma nova versão será criada na replicação.
* `agentId` (valor da string, padrão significa que todos os agentes ativados são usados).
* `filters` (valor da string, padrão significa que todos os caminhos estão ativados). Os valores disponíveis são:
   * `onlyActivated` - somente os caminhos que não estão marcados como ativados serão ativados.
   * `onlyModified` - ative apenas caminhos que já estejam ativados e tenham uma data de modificação posterior à data de ativação.
   * O acima pode ser ORed com uma barra vertical &quot;|&quot;. Por exemplo, `onlyActivated|onlyModified`.

**Logs**

Quando a etapa do fluxo de trabalho de ativação da árvore for iniciada, ele registrará os parâmetros de configuração no nível de log INFO. Quando os caminhos são ativados, uma instrução INFO também é registrada.

Uma instrução INFO final será registrada após a etapa do fluxo de trabalho ter replicado todos os caminhos.

Além disso, você pode aumentar o nível de log dos registradores abaixo `com.day.cq.wcm.workflow.process.impl` para DEBUG/TRACE para obter ainda mais informações de log.

No caso de erros, a etapa do fluxo de trabalho termina com um `WorkflowException`, que envolve a Exceção subjacente.

Abaixo você encontrará exemplos de logs gerados durante um exemplo de fluxo de trabalho da árvore de conteúdo de publicação:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**Retomar suporte**

O workflow processa o conteúdo em partes, cada uma representando um subconjunto do conteúdo completo a ser publicado. Se, por qualquer motivo, o workflow for interrompido pelo sistema, ele reiniciará e processará o segmento que ainda não foi processado. Uma declaração de log indicará que o conteúdo foi retomado de um caminho específico.

## Resolução de problemas {#troubleshooting}

Para solucionar problemas de replicação, navegue até as filas de replicação na interface do usuário da Web do AEM Author Service:

1. No menu Iniciar AEM, navegue até **Ferramentas > Implantação > Distribuição**
2. Selecione o cartão **forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. Verifique o status da fila que deve estar verde
4. Você pode testar a conexão com o serviço de replicação
5. Selecione a guia **Logs** que mostra o histórico de publicações de conteúdo

![](assets/logs.png "LogsLogs")

Se o conteúdo não puder ser publicado, toda a publicação será revertida do AEM Publish Service.
Nesse caso, as filas devem ser revistas para identificar quais itens causaram o cancelamento da publicação. Ao clicar em uma fila mostrando um status vermelho, a fila com itens pendentes seria exibida, a partir da qual um ou todos os itens podem ser apagados, se necessário.
