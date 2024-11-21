---
title: Replicação
description: Saiba mais sobre distribuição e solução de problemas de replicação no AEM as a Cloud Service.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
feature: Operations
role: Admin
source-git-commit: 60006b0e0b5215263b53cbb7fec840c47fcef1a8
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 31%

---

# Replicação {#replication}

O Adobe Experience Manager as a Cloud Service usa o recurso [Distribuição de Conteúdo do Sling](https://sling.apache.org/documentation/bundles/content-distribution.html) para mover o conteúdo e replica-lo em um serviço de pipeline executado no Adobe Developer, que está fora do tempo de execução do AEM.

>[!NOTE]
>
>Consulte [Distribuição](/help/overview/architecture.md#content-distribution) para obter mais informações.

## Métodos de publicação de conteúdo {#methods-of-publishing-content}

>[!NOTE]
>
>Se você estiver interessado em publicar conteúdo em massa, crie um fluxo de trabalho usando a [Etapa do Fluxo de Trabalho de Ativação da Árvore](#tree-activation), que pode lidar eficientemente com grandes cargas.
>Não é recomendável criar seu próprio código personalizado de publicação em massa.
>Se precisar personalizar por qualquer motivo, você poderá acionar um fluxo de trabalho com essa etapa usando APIs de fluxo de trabalho existentes.
>É sempre uma boa prática publicar somente conteúdo que deve ser publicado. E seja prudente ao não tentar publicar grandes números de conteúdo, se não for necessário. No entanto, não há limites para o conteúdo que você pode enviar por meio de workflows com a Etapa de fluxo de trabalho Ativação em árvore.

### Publicação/Cancelamento de publicação rápidos — Publicação/Cancelamento de publicação planejados {#publish-unpublish}

Esse recurso permite publicar as páginas selecionadas imediatamente, sem as opções adicionais possíveis por meio da abordagem Gerenciar publicação.

Para obter mais informações, consulte [Gerenciar publicação](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication).

### Tempos de ativação e desativação — Configuração do acionador {#on-and-off-times-trigger-configuration}

As possibilidades adicionais de **Tempo de ativação** e **Tempo de desativação** estão disponíveis na [guia Básico das propriedades de página](/help/sites-cloud/authoring/sites-console/page-properties.md#basic).

Para efetuar a replicação automática deste recurso, habilite **Replicação Automática** na [Configuração OSGi](/help/implementing/deploying/configuring-osgi.md) **Configuração do Acionador Ligado/Desligado**:

![Configuração do acionador ativado/desativado do OSGi](/help/operations/assets/replication-on-off-trigger.png)

### Gerenciar publicação    {#manage-publication}

Gerenciar publicação oferece mais opções do que o Quick Publish, permitindo a inclusão de páginas secundárias, a personalização das referências e o início de qualquer fluxo de trabalho aplicável, além de oferecer a opção de publicação posterior.

A inclusão dos filhos de uma pasta na opção &quot;publicar mais tarde&quot; chama o fluxo de trabalho da Árvore de conteúdo do Publish, descrito neste artigo.

Você pode encontrar informações mais detalhadas sobre Gerenciar publicação na [Documentação sobre princípios básicos de publicação](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication).

### Etapa do fluxo de trabalho de ativação da árvore {#tree-activation}

A etapa do fluxo de trabalho de Ativação em árvore destina-se a replicar com desempenho uma hierarquia profunda de nós de conteúdo. Ele faz uma pausa automaticamente quando a fila fica muito grande para permitir que outras replicações prossigam em paralelo com a latência mínima.

Criar um Modelo de Fluxo de Trabalho que use a etapa de processo `TreeActivation`:

1. Na página inicial do AEM as a Cloud Service, acesse **Ferramentas - Fluxo de trabalho - Modelos**.
1. Na página Modelos de fluxo de trabalho, pressione **Criar** no canto superior direito da tela.
1. Adicione um título e um nome ao modelo. Para obter mais informações, consulte [Criando Modelos de Fluxo de Trabalho](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=pt-BR).
1. Selecione o modelo criado na lista e pressione **Editar**
1. Na janela a seguir, exclua a Etapa exibida por padrão
1. Arraste e solte a Etapa do processo no fluxo do modelo atual:

   ![Etapa do processo](/help/operations/assets/processstep.png)

1. Selecione a etapa do processo no fluxo e selecione **Configurar** pressionando o ícone de chave inglesa.
1. Selecione a guia **Processo**, selecione `Publish Content Tree` na lista suspensa e marque a caixa de seleção **Avanço do manipulador**

   ![Treeactivation](/help/operations/assets/new-treeactivationstep.png)

1. Defina quaisquer parâmetros adicionais no campo **Argumentos**. Vários argumentos separados por vírgula podem ser agrupados. Por exemplo:

   `enableVersion=false,agentId=publish,chunkSize=50,maxTreeSize=500000,dryRun=false,filters=onlyModified,maxQueueSize=10`

   >[!NOTE]
   >
   >Para obter a lista de parâmetros, consulte a seção **Parâmetros** abaixo.

1. Pressione **Concluído** para salvar o modelo de fluxo de trabalho.

**Parâmetros**

| Nome | padrão | descrição |
| -------------- | ------- | --------------------------------------------------------------- |
| caminho |         | caminho raiz do qual iniciar |
| agentId | publicação | Nome do agente de replicação a ser usado |
| tamanhoParte | 50 | Número de caminhos a serem agrupados em uma única replicação |
| maxTreeSize | 500000 | Número máximo de nós para uma árvore ser considerada pequena |
| maxQueueSize | 10 | Número máximo de itens na fila de replicação |
| enableVersion | falso | Ativar controle de versão |
| dryRun | falso | Quando definido como verdadeiro, a replicação não é realmente chamada |
| userId |         | somente para trabalho. No workflow, o usuário que chama o workflow é usado |
| filtros |         | Lista de nomes de filtro de nó. Consulte o filtro compatível abaixo |

**Filtros de Suporte**

| Nome | descrição |
| ------------- | ------------------------------------------- |
| onlyModified | Nós modificados desde a última publicação |
| onlyPublished | Nós publicados antes de |


**Retomar suporte**

O fluxo de trabalho processa o conteúdo em partes, cada uma representando um subconjunto do conteúdo completo a ser publicado.  Se o workflow for interrompido pelo sistema, ele continuará de onde parou.

**Progresso do Fluxo de Trabalho de Monitoramento**

1. Na página inicial do AEM as a Cloud Service, vá para **Ferramentas - Geral - Trabalhos**.
1. Examine a linha correspondente ao seu fluxo de trabalho. A coluna *progress* fornece uma indicação do andamento da replicação. Por exemplo, ele pode exibir 41/564 e, após a atualização, pode ser atualizado para 52/564.

   ![Progresso da Treeactivation](/help/operations/assets/treeactivation-progress.png)


1. Selecionar a linha e abri-la fornecerá detalhes adicionais sobre o status da execução do workflow.

   ![Detalhes do status de Treeactivation](/help/operations/assets/treeactivation-progress-details.png)



### Fluxo de trabalho de publicação da árvore de conteúdo {#publish-content-tree-workflow}

>[!NOTE]
>
>Esse recurso está obsoleto em favor da etapa de Ativação da árvore, que tem um desempenho mais alto, e pode ser incluído em um fluxo de trabalho personalizado.

<details>
<summary>Clique aqui para saber mais sobre este recurso obsoleto.</summary>

Você pode acionar uma replicação em árvore ao escolher **Ferramentas - Fluxo de trabalho - Modelos** e copiar o modelo de fluxo de trabalho pronto para uso **Publicar árvore de conteúdo**, conforme mostrado abaixo:

![O Cartão de Fluxo de Trabalho da Árvore de Conteúdo do Publish](/help/operations/assets/publishcontenttreeworkflow.png)

Não chame o modelo original. Em vez disso, primeiro copie o modelo e chame essa cópia.

Como todos os fluxos de trabalho, também é possível chamá-lo por meio da API. Para obter mais informações, consulte [Interação programática com fluxos de trabalho](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html#extending-aem).

Como alternativa, você pode criar um Modelo de Fluxo de Trabalho que use a etapa de processo `Publish Content Tree`.

1. Na página inicial do AEM as a Cloud Service, acesse **Ferramentas - Fluxo de trabalho - Modelos**.
1. Na página Modelos de fluxo de trabalho, pressione **Criar** no canto superior direito da tela.
1. Adicione um título e um nome ao modelo. Para obter mais informações, consulte [Criando Modelos de Fluxo de Trabalho](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=pt-BR).
1. Selecione o modelo criado na lista e pressione **Editar**
1. Na janela a seguir, arraste e solte a etapa do processo no fluxo do modelo atual:

   ![Etapa do processo](/help/operations/assets/processstep.png)

1. Selecione a etapa do processo no fluxo e selecione **Configurar** pressionando o ícone de chave inglesa.
1. Selecione a guia **Processo**, selecione `Publish Content Tree` na lista suspensa e marque a caixa de seleção **Avanço do manipulador**

   ![Treeactivation](/help/operations/assets/newstep.png)

1. Defina quaisquer parâmetros adicionais no campo **Argumentos**. Vários argumentos separados por vírgula podem ser agrupados. Por exemplo:

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >Para obter a lista de parâmetros, consulte a seção **Parâmetros** abaixo.

1. Pressione **Concluído** para salvar o modelo de fluxo de trabalho.

**Parâmetros**

* `includeChildren` (valor booleano, padrão: `false`). O valor `false` significa que somente o caminho é publicado; `true` significa que os filhos também são publicados.
* `replicateAsParticipant` (valor booleano, padrão: `false`). Se configurado como `true`, a replicação está usando o `userid` do principal que executou a etapa do participante.
* `enableVersion` (valor booleano, padrão: `false`). Esse parâmetro determina se uma nova versão será criada na replicação.
* `agentId` (valor da string; o valor padrão significa que apenas os agentes para publicação são usados). É recomendado ser explícito sobre o agentId; por exemplo, definir o valor como: publicar. Definir o agente como `preview` publica no serviço de visualização.
* `filters` (valor da cadeia de caracteres; o valor padrão significa que todos os caminhos estão ativados). Os valores disponíveis são:
   * `onlyActivated` - ativar somente as páginas que (já) foram ativadas. Atua como uma forma de reativação.
   * `onlyModified` - ativar apenas os caminhos que já estejam ativados e tenham uma data de modificação posterior à data de ativação.
   * O conteúdo acima pode ser ORed com uma barra vertical “|”. Por exemplo, `onlyActivated|onlyModified`.

**Logs**

Quando a etapa do fluxo de trabalho de ativação da árvore é iniciada, ela registra os parâmetros de configuração no nível de log INFO. Quando os caminhos são ativados, uma declaração INFO também é registrada.

Uma declaração INFO final é registrada depois que a etapa do fluxo de trabalho replica todos os caminhos.

Além disso, você pode aumentar o nível de log dos registradores abaixo de `com.day.cq.wcm.workflow.process.impl` para DEBUG/TRACE para obter ainda mais informações de log.

Se houver erros, a etapa do fluxo de trabalho será encerrada com um `WorkflowException`, que envolve a Exceção subjacente.

A seguir estão exemplos de logs gerados durante um exemplo de fluxo de trabalho de publicação da árvore de conteúdo:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```
</details>

### API de replicação {#replication-api}

Você pode publicar conteúdo usando a API de replicação disponível no AEM as a Cloud Service.

Para obter mais informações, consulte a [Documentação da API](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html).

**Uso básico da API**

```
@Reference
Replicator replicator;
@Reference
ReplicationStatusProvider replicationStatusProvider;

....
Session session = ...
// Activate a single page to all agents, which are active by default
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en");
// Activate multiple pages (but try to limit it to approx 100 at max)
replicator.replicate(session,ReplicationActionType.ACTIVATE, new String[]{"/content/we-retail/en","/content/we-retail/de"});

// ways to get the replication status
Resource enResource = resourceResolver.getResource("/content/we-retail/en");
Resource deResource = resourceResolver.getResource("/content/we-retail/de");
ReplicationStatus enStatus = enResource.adaptTo(ReplicationStatus.class);
// if you need to get the status for more more than 1 resource at once, this approach is more performant
Map<String,ReplicationStatus> allStatus = replicationStatusProvider.getBatchReplicationStatus(enResource,deResource);
```

**Replicação com agentes específicos**

Ao replicar recursos, como no exemplo acima, somente os agentes que estão ativos por padrão são usados. No AEM as a Cloud Service, significa apenas o agente chamado &quot;publicar&quot;, que conecta o autor ao nível de publicação.

Para auxiliar a funcionalidade de visualização, um novo agente chamado “visualização” foi adicionado; esse agente não está ativo por padrão. Esse agente é usado para conectar o autor ao nível de visualização. Se quiser replicar somente por meio do agente de visualização, selecione explicitamente esse agente de visualização por meio de um `AgentFilter`.

Consulte o exemplo a seguir:

```
private static final String PREVIEW_AGENT = "preview";

ReplicationStatus beforeStatus = enResource.adaptTo(ReplicationStatus.class); // beforeStatus.isActivated == false

ReplicationOptions options = new ReplicationOptions();
options.setFilter(new AgentFilter() {
  @Override
  public boolean isIncluded (Agent agent) {
    return agent.getId().equals(PREVIEW_AGENT);
  }
});
// will replicate only to preview
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en", options);

ReplicationStatus afterStatus = enResource.adaptTo(ReplicationStatus.class); // afterStatus.isActivated == false
ReplicationStatus previewStatus = afterStatus.getStatusForAgent(PREVIEW_AGENT); // previewStatus.isActivated == true
```

Caso você não forneça esse filtro e use apenas o agente “publicar”, o agente “visualizar” não será usado e a ação de replicação não afetará o nível de visualização.

O `ReplicationStatus` geral de um recurso só será modificado se a ação de replicação incluir pelo menos um agente que esteja ativo por padrão. No exemplo acima, esse fluxo não era o caso. A replicação estava usando apenas o agente &quot;visualização&quot;. Portanto, você deve usar o novo método `getStatusForAgent()`, que permite consultar o status de um agente específico. Esse método também funciona para o agente “publicar”. Ele retorna um valor não nulo se houver alguma ação de replicação feita usando o agente fornecido.

### Métodos de invalidação de conteúdo {#invalidating-content}

Você pode invalidar o conteúdo diretamente usando a Invalidação de conteúdo do Sling (SCD) a partir do autor (o método preferencial) ou usando a API de replicação para chamar o agente de replicação de limpeza do Dispatcher de publicação. Consulte a página [Armazenamento em cache](/help/implementing/dispatcher/caching.md) para obter mais detalhes.

**Limites de capacidade da API de replicação**

Replicar menos de 100 caminhos de cada vez, sendo 500 o limite. Acima do limite, um `ReplicationException` é lançado.
Se a lógica do aplicativo não exigir uma replicação precisa, esse limite poderá ser ultrapassado definindo `ReplicationOptions.setUseAtomicCalls` como false, o que aceita qualquer número de caminhos, mas cria compartimentos internamente para permanecer abaixo desse limite.

O tamanho do conteúdo transmitido por chamada de replicação não deve exceder `10 MB`. Essa regra inclui os nós e as propriedades, mas não os binários (pacotes de fluxo de trabalho e de conteúdo são considerados binários).


## Resolução de problemas {#troubleshooting}

Para solucionar problemas de replicação, navegue até as filas de replicação na interface web do serviço do autor do AEM:

1. No menu Iniciar do AEM, navegue até **Ferramentas** > **Implantação** > **Distribuição**
1. Selecione o cartão **publicar**

   ![Status](assets/publish-status.png "Status")

1. Verifique o status da fila, que deve estar em verde
1. Você pode testar a conexão com o serviço de replicação
1. Selecione a guia **Logs**, que mostra o histórico de publicações de conteúdo

![Logs](assets/publish-logs.png "Logs")

Se o conteúdo não puder ser publicado, toda a publicação será revertida do serviço AEM Publish.

Nesse caso, a fila principal e editável mostra um status vermelho e deve ser revisada para identificar quais itens causaram o cancelamento da publicação. Ao clicar nessa fila, seus itens pendentes são exibidos, a partir dos quais um único item ou todos os itens podem ser apagados, se necessário.
