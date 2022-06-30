---
title: Replicação
description: Distribuição e solução de problemas da replicação.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: 5791410fd5956cd8b82d4ed03f3920ade3bfedcb
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 4%

---

# Replicação {#replication}

A Adobe Experience Manager as a Cloud Service usa a variável [Distribuição de conteúdo Sling](https://sling.apache.org/documentation/bundles/content-distribution.html) capacidade de mover o conteúdo para replicar para um serviço de pipeline executado no Adobe I/O que está fora do tempo de execução AEM.

>[!NOTE]
>
>Ler [Distribuição](/help/overview/architecture.md#content-distribution) para obter mais informações.

## Métodos de publicação de conteúdo {#methods-of-publishing-content}

### Publicação/Cancelamento Rápido - Planejado/Publicação {#publish-unpublish}

Isso permite publicar as páginas selecionadas imediatamente, sem as opções adicionais possíveis por meio da abordagem Gerenciar publicação .

Para obter mais informações, consulte [Gerenciar publicação](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

### Tempos de ativação e desativação - Configuração de acionador {#on-and-off-times-trigger-configuration}

As possibilidades adicionais de **Hora de ligar** e **Hora de desligar** estão disponíveis no [Guia Básico das Propriedades da página](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic).

Para realizar a replicação automática para isso, você precisa ativar o **Replicação automática** no [Configuração do OSGi](/help/implementing/deploying/configuring-osgi.md) **Configuração do acionador ativado**:

![Configuração do Acionador Desligado do OSGi](/help/operations/assets/replication-on-off-trigger.png)

### Gerenciar publicação    {#manage-publication}

A opção Gerenciar publicação oferece mais opções do que a Publicação rápida, permitindo a inclusão de páginas filhas, a personalização das referências e o início de qualquer fluxo de trabalho aplicável, além de oferecer a opção de publicação em uma data posterior.

A inclusão dos filhos de uma pasta na opção &quot;publicar mais tarde&quot; chamará o fluxo de trabalho Publicar árvore de conteúdo, descrito neste artigo.

Você pode encontrar informações mais detalhadas sobre Gerenciar publicação no [Documentação de Princípios básicos de publicação](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

### documentação Fluxo de trabalho de publicação da árvore de conteúdo {#publish-content-tree-workflow}

Você pode acionar uma replicação em árvore escolhendo **Ferramentas - Fluxo de trabalho - Modelos** e copiar o **Publicar árvore de conteúdo** modelo de fluxo de trabalho pronto para uso, conforme mostrado abaixo:

![](/help/operations/assets/publishcontenttreeworkflow.png)

Não modifique ou chame o modelo original. Em vez disso, primeiro copie o modelo e depois modifique ou chame essa cópia.

Como todos os workflows, também é possível invocá-los por meio da API. Para obter mais informações, consulte [Interação com fluxos de trabalho programaticamente](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem).

Como alternativa, também é possível fazer isso criando um Modelo de fluxo de trabalho que usa a variável `Publish Content Tree` etapa do processo:

1. Na página inicial AEM as a Cloud Service, vá para **Ferramentas - Fluxo de trabalho - Modelos**
1. Na página Modelos de fluxo de trabalho , pressione **Criar** no canto superior direito da tela
1. Adicione um título e um nome ao modelo. Para obter mais informações, consulte [Criação de modelos de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)
1. Selecione o modelo recém-criado na lista e pressione **Editar**
1. Na janela a seguir, arraste e solte a Etapa do processo no fluxo do modelo atual:

   ![Etapa do processo](/help/operations/assets/processstep.png)

1. Clique na etapa Processo no fluxo e selecione **Configurar** pressionando o ícone da chave inglesa
1. Clique no botão **Processo** e selecione `Publish Content Tree` na lista suspensa

   ![Treeativation](/help/operations/assets/newstep.png)

1. Defina quaisquer parâmetros adicionais na **Argumentos** campo. Vários argumentos separados por vírgula podem ser stringidos juntos. Por exemplo:

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >Para obter a lista de parâmetros, consulte **Parâmetros** abaixo.

1. Press **Concluído** para salvar o modelo de Fluxo de trabalho.

**Parâmetros**

* `includeChildren` (valor booleano, padrão: `false`). false significa que somente o caminho é publicado. verdadeiro significa que as crianças também são publicadas.
* `replicateAsParticipant` (valor booleano, padrão: `false`). Se configurado como `true`, a replicação está usando o `userid` do principal que executou a etapa do participante.
* `enableVersion` (valor booleano, padrão: `true`). Esse parâmetro determina se uma nova versão será criada na replicação.
* `agentId` (valor da string, padrão significa que apenas os agentes para publicação são usados). Recomenda-se ser explícito sobre o agentId; por exemplo, definir o valor para : publicar. Configurar o agente para `preview` será publicado no serviço de visualização
* `filters` (valor da string, padrão significa que todos os caminhos estão ativados). Os valores disponíveis são:
   * `onlyActivated` - somente os caminhos que não estão marcados como ativados serão ativados.
   * `onlyModified` - ative apenas caminhos que já estejam ativados e tenham uma data de modificação posterior à data de ativação.
   * O acima pode ser ORed com uma barra vertical &quot;|&quot;. Por exemplo, `onlyActivated|onlyModified`.

**Logs**

Quando a etapa do fluxo de trabalho de ativação da árvore for iniciada, ele registrará os parâmetros de configuração no nível de log INFO. Quando os caminhos são ativados, uma instrução INFO também é registrada.

Uma instrução INFO final será registrada após a etapa do fluxo de trabalho ter replicado todos os caminhos.

Além disso, você pode aumentar o nível de log dos registradores abaixo `com.day.cq.wcm.workflow.process.impl` para DEBUG/TRACE para obter ainda mais informações de log.

No caso de erros, a etapa do fluxo de trabalho é finalizada com uma `WorkflowException`, que envolve a Exceção subjacente.

Abaixo você encontrará exemplos de logs gerados durante um exemplo de fluxo de trabalho da árvore de conteúdo de publicação:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**Retomar suporte**

O workflow processa o conteúdo em partes, cada uma representando um subconjunto do conteúdo completo a ser publicado. Se, por qualquer motivo, o workflow for interrompido pelo sistema, ele reiniciará e processará o segmento que ainda não foi processado. Uma declaração de log indicará que o conteúdo foi retomado de um caminho específico.

### API de replicação {#replication-api}

Você pode publicar conteúdo usando a API de replicação em AEM as a Cloud Service.

Para obter mais informações, consulte o [Documentação da API](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html).

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

Ao replicar recursos como no exemplo acima, somente os agentes que estão ativos por padrão serão usados. Em AEM as a Cloud Service, esse será apenas o agente chamado &quot;publicar&quot;, que conecta o autor ao nível de publicação.

Para oferecer suporte à funcionalidade de visualização, um novo agente chamado &quot;pré-visualização&quot; foi adicionado, o que não está ativo por padrão. Esse agente é usado para conectar o autor à camada de visualização. Se quiser replicar somente por meio do agente de visualização, é necessário selecionar explicitamente esse agente de visualização por meio de um `AgentFilter`.

Veja o exemplo abaixo sobre como fazer isso:

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

Caso não forneça esse filtro e use apenas o agente &quot;publicar&quot;, o agente &quot;visualizar&quot; não será usado e a ação de replicação não afetará o nível de visualização.

O `ReplicationStatus` de um recurso só será modificado se a ação de replicação incluir pelo menos um agente que esteja ativo por padrão. No exemplo acima, isso não ocorre, pois a replicação está usando apenas o agente &quot;preview&quot;. Portanto, é necessário usar o novo `getStatusForAgent()` , que permite consultar o status de um agente específico. Esse método também funciona para o agente &quot;publicar&quot;. Retorna um valor não nulo se houver alguma ação de replicação feita usando o agente fornecido.


**Limites de capacidade da API de replicação**

Recomenda-se replicar menos de 100 caminhos de cada vez, sendo 500 o limite rígido. Acima do limite rígido, uma `ReplicationException` será jogada.
Se a lógica do aplicativo não exigir replicação atômica, esse limite poderá ser ultrapassado definindo a variável `ReplicationOptions.setUseAtomicCalls` como falso, o que aceitará qualquer número de caminhos, mas criará compartimentos internamente para permanecer abaixo desse limite.

O tamanho do conteúdo transmitido por chamada de replicação não deve exceder `10 MB`. Isso inclui os nós e as propriedades, mas não qualquer binário (os pacotes de fluxo de trabalho e os pacotes de conteúdo são considerados binários).

## Resolução de problemas {#troubleshooting}

Para solucionar problemas de replicação, navegue até as filas de replicação na interface do usuário da Web do AEM Author Service:

1. No AEM menu Iniciar, navegue até **Ferramentas > Implantação > Distribuição**
2. Selecione o cartão **publicar**
   ![Status](assets/publish-status.png "Status")
3. Verifique o status da fila que deve estar verde
4. Você pode testar a conexão com o serviço de replicação
5. Selecione o **Logs** guia que mostra o histórico de publicações de conteúdo

![Logs](assets/publish-logs.png "Logs")

Se o conteúdo não puder ser publicado, toda a publicação será revertida do AEM Publish Service.
Nesse caso, a fila principal e editável mostrará um status vermelho e deverá ser revisada para identificar quais itens causaram o cancelamento da publicação. Ao clicar nessa fila, seus itens pendentes serão exibidos, a partir dos quais um único item ou todos os itens podem ser apagados, se necessário.
