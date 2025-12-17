---
title: Tarefas de manutenção no AEM as a Cloud Service
description: Saiba mais sobre as tarefas de manutenção no AEM as a Cloud Service e como configurá-las.
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
feature: Operations
role: Admin
source-git-commit: d5addc40eb48000c515b670ef5f7c7a7e8b79928
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 28%

---


# Tarefas de manutenção no AEM as a Cloud Service {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="Tarefas de manutenção"
>abstract="Tarefas de manutenção são processos executados de acordo com um cronograma para otimizar o repositório. Com o AEM as a Cloud Service, a necessidade de os clientes configurarem as propriedades operacionais das tarefas de manutenção é mínima. Os clientes podem concentrar seus recursos em preocupações no nível do aplicativo, deixando as operações de infraestrutura para a Adobe."

Tarefas de manutenção são processos executados de acordo com um cronograma para otimizar o repositório. Com o AEM as a Cloud Service, a necessidade de os clientes configurarem as propriedades operacionais das tarefas de manutenção é mínima. Os clientes podem concentrar seus recursos em preocupações no nível do aplicativo, deixando as operações de infraestrutura para a Adobe.

## Configurar tarefas de manutenção {#maintenance-tasks-configuring}

Em versões anteriores do AEM, você podia configurar as tarefas de manutenção usando o Cartão de manutenção (Ferramentas > Operações > Manutenção). Para o AEM as a Cloud Service, o Cartão de manutenção não está mais disponível, portanto, as configurações devem ser enviadas ao controle de origem e implantadas usando o Cloud Manager. O Adobe gerencia as tarefas de manutenção que têm configurações não configuráveis pelos clientes (por exemplo, coleta de lixo do armazenamento de dados). Outras tarefas de manutenção podem ser configuradas pelos clientes, conforme descrito na tabela abaixo.

>[!CAUTION]
>
>A Adobe se reserva o direito de substituir as definições de configuração da tarefa de manutenção de um cliente para atenuar problemas como degradação de desempenho.

### Tarefas de manutenção {#maintenance-tasks}

A tabela a seguir ilustra as tarefas de manutenção disponíveis.

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Tarefa de manutenção</th>
    <th>Quem é o proprietário da configuração</th>
    <th>Como configurar (opcional)</th>
  </tr>  
  <tr>
    <td>Coleta de lixo do armazenamento de dados</td>
    <td>Adobe</td>
    <td>N/A — de propriedade total da Adobe</td>
  </td> 
  </tr>
  <tr>
    <td>Remoção da versão</td>
    <td>Cliente</td>
    <td>A limpeza de versão está desabilitada no momento por padrão, mas a política pode ser configurada, conforme descrito na seção <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">Tarefas de Manutenção de Limpeza de Versão e Limpeza de Log de Auditoria</a>.<br/><br/>A limpeza será em breve habilitada por padrão, com esses valores substituíveis.<br>
   </td>
  </td>
  </tr>
  <tr>
    <td>Limpeza do log de auditoria</td>
    <td>Cliente</td>
    <td>A limpeza de log de auditoria está desabilitada por padrão no momento, mas a política pode ser configurada, conforme descrito na seção <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">Tarefas de Manutenção de Limpeza de Versão e Limpeza de Log de Auditoria</a>.<br/><br/>A limpeza será em breve habilitada por padrão, com esses valores substituíveis.<br>
   </td>
   </td>
  </tr>
  <tr>
    <td>Limpeza de binários do Lucene</td>
    <td>Adobe</td>
    <td>Não usado e, portanto, desabilitado pela Adobe.</td>
  </td>
  </tr>
  <tr>
    <td>Limpeza de tarefa ad-hoc</td>
    <td>Cliente</td>
    <td>
    <p>Deve ser feito no Git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code> criando propriedades na pasta <code>/conf/global/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> ou <code>granite_monthly</code>.</p>
    <p>Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração. Ative a tarefa de manutenção adicionando outro nó sob o nó acima. Nomeie-o <code>granite_TaskPurgeTask</code>, com o atributo <code>sling:resourceType</code> definido como <code>granite/operations/components/maintenance/task</code> e o atributo <code>granite.maintenance.name</code> definido como <code>TaskPurge</code>. Para configurar as propriedades OSGI, consulte <code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code> para obter a lista de propriedades.</p>
  </td>
  </tr>
    <tr>
    <td>Remoção do fluxo de trabalho</td>
    <td>Cliente</td>
    <td>
    <p>Deve ser feito no Git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code> criando propriedades na pasta <code>/conf/global/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> ou <code>granite_monthly</code>. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração.</p>
    <p>Habilite a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o como <code>granite_WorkflowPurgeTask</code>) com as propriedades adequadas. Configure as propriedades OSGI, consulte <a href="/help/sites-cloud/administering/workflows-administering.md#regular-purging-of-workflow-instances">Limpeza Regular de Instâncias de Fluxo de Trabalho</a>.</p>
  </td>
  </tr>
  <tr>
    <td>Remoção do projeto</td>
    <td>Cliente</td>
    <td>
    <p>Deve ser feito no Git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code> criando propriedades na pasta <code>/conf/global/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> ou <code>granite_monthly</code>. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração.</p>
    <p>Habilite a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o como <code>granite_ProjectPurgeTask</code>) com as propriedades adequadas. Consulte a lista de <a href="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi">Propriedades OSGi</a> para <b>Configuração de Limpeza de Projetos Adobe</b> .</p>
  </td>
  </tr>
  </tbody>
</table>

### Configurações da janela de manutenção {#maintenance-window-configurations}

A tabela a seguir ilustra as configurações disponíveis da janela de manutenção.

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Configuração da janela de manutenção</th>
    <th>Quem é o proprietário da configuração</th>
    <th>Tipo de configuração</th>
    <th>Parâmetros</th>
  </tr>
  <tr>
    <td>Diariamente</td>
    <td>Cliente</td>
    <td>Definição de Nó JCR</td>
  <td>
  <p><strong>windowSchedule=daily</strong> (esse valor não deve ser alterado)</p>
  <p><strong>windowStartTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as tarefas de manutenção associadas à Janela de manutenção diária devem começar a ser executadas.</p>
  <p><strong>windowEndTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as tarefas de manutenção associadas à Janela de manutenção diária devem parar de ser executadas se ainda não tiverem sido concluídas.</p>
  <p>Uma tarefa de manutenção não pode ser executada mais de uma vez durante esse período.</p>
  </td> 
  </tr>
  <tr>
    <td>Semanalmente</td>
    <td>Cliente</td>
    <td>Definição de Nó JCR</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> (esse valor não deve ser alterado)</p>
    <p><strong>windowStartTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as tarefas de manutenção associadas à Janela de manutenção semanal devem começar a ser executadas.</p>
    <p><strong>windowEndTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as tarefas de manutenção associadas à Janela de manutenção semanal devem parar de ser executadas se ainda não tiverem sido concluídas.</p>
    <p>Uma tarefa de manutenção não pode ser executada mais de uma vez durante esse período.</p>
    <p><strong>windowScheduleWeekdays= Matriz de dois valores de 1 a 7 (por exemplo, [5,5])</strong> O primeiro valor da matriz é o dia de início em que o trabalho é agendado e o segundo valor é o dia de término em que o trabalho será interrompido. A hora exata de início e término é regida pelos parâmetros windowStartTime e windowEndTime, respectivamente.</p>
    </td>
  </tr>
  <tr>
    <td>Mensalmente</td>
    <td>Cliente</td>
    <td>Definição de Nó JCR</td>
    <td>
    <p><strong>windowSchedule=month</strong> (esse valor não deve ser alterado)</p>
    <p><strong>windowStartTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as tarefas de manutenção associadas à Janela de manutenção mensal devem começar a ser executadas.</p>
    <p><strong>windowEndTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as tarefas de manutenção associadas à Janela de manutenção mensal devem parar de ser executadas se ainda não tiverem sido concluídas.</p>
    <p>Uma tarefa de manutenção não pode ser executada mais de uma vez durante esse período.</p>
    <p><strong>windowScheduleWeekdays=Matriz de dois valores de 1 a 7 (por exemplo, [5,5])</strong> O primeiro valor da matriz é o dia de início em que o trabalho é agendado e o segundo valor é o dia de término em que o trabalho será interrompido. A hora exata de início e término é regida pelos parâmetros windowStartTime e windowEndTime, respectivamente.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 para agendar na primeira semana do mês ou 1 para agendar na última semana do mês. A ausência de um valor agendaria trabalhos no dia regido por windowScheduleWeekdays (todos os meses).</p>
    </td>
    </tr>
    </tbody>
</table>

### Localizações {#locations}

* Diariamente - /conf/global/settings/granite/operations/maintenance/granite_daily
* Semanalmente - /conf/global/settings/granite/operations/maintenance/granite_weekly
* Mensal - /conf/global/settings/granite/operations/maintenance/granite_month

### Amostras de código {#code-samples}

**Amostra de código 1 (diariamente)**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
  xmlns:jcr="http://www.jcp.org/jcr/1.0" 
  jcr:primaryType="sling:Folder"
  sling:configCollectionInherit="true"
  sling:configPropertyInherit="true"
  windowSchedule="daily"
  windowStartTime="03:00"
  windowEndTime="05:00"
 />
```

**Amostra de código 2 (semanalmente)**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="weekly"
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

**Amostra de código 3 (mensalmente)**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="monthly"
   windowFirstLastStartDay=0
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

## Tarefas de Manutenção de Limpeza de Versão e Limpeza de Log de Auditoria {#purge-tasks}

A limpeza de versões e do log de auditoria reduz o tamanho do repositório e, em alguns cenários, pode melhorar o desempenho.

>[!NOTE]
>
>Os clientes do AEM Guides não devem configurar a Limpeza de versão.

### Padrões {#defaults}

Atualmente, a limpeza não está habilitada por padrão, mas isso será alterado no futuro. Os ambientes criados antes da ativação da limpeza padrão terão um limite mais conservador para que a limpeza não ocorra inesperadamente. Consulte as seções Limpeza de versão e Limpeza de log de auditoria abaixo para obter mais detalhes sobre a política de limpeza padrão.
<!-- Version purging and audit log purging are on by default, with different default values for environments with ids higher than **TBD** versus those with ids lower than that value. -->

<!-- ### Overriding the default values with a new configuration {#override} -->

Os valores de limpeza padrão podem ser substituídos declarando um arquivo de configuração e implantando-o conforme descrito abaixo.

<!-- The reason for this behavior is to clarify the ambiguity over whether the default purge values would take effect once you remove the declaration. -->

### Aplicar uma configuração {#configure-purge}

Declare um arquivo de configuração e implante-o conforme descrito nas etapas a seguir.

>[!NOTE]
>Depois de implantar o nó de limpeza de versão no arquivo de configuração, você deve mantê-lo declarado e não removê-lo. O pipeline de configuração falhará se você tentar fazer isso.
> 
>Da mesma forma, depois de implantar o nó de expurgação do log de auditoria no arquivo de configuração, você deve mantê-lo declarado e não removê-lo.

1. Crie um arquivo com o nome `mt.yaml` ou similar.

1. Coloque o arquivo em algum lugar em uma pasta de nível superior chamada `config` ou similar, conforme descrito em [Usando Pipelines de Configuração](/help/operations/config-pipeline.md#folder-structure).

1. Declare as propriedades no arquivo de configuração, que incluem:

   * algumas propriedades acima do nó de dados — consulte [Uso de Pipelines de Configuração](/help/operations/config-pipeline.md#common-syntax) para obter uma descrição. O valor da propriedade `kind` deve ser *MaintenanceTasks* e a versão deve ser definida como *1*.

   * um objeto de dados com objetos `versionPurge` e `auditLogPurge`.

   Consulte as definições e a sintaxe dos objetos `versionPurge` e `auditLogPurge` abaixo.

   Estruture a configuração semelhante ao seguinte exemplo:

   ```
   kind: "MaintenanceTasks"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     versionPurge:
       maximumVersions: 15
       maximumAgeDays: 20
       paths: ["/content"]
       minimumVersions: 1
       retainLabelledVersions: false
     auditLogPurge:
       rules:
         - replication:
             maximumAgeDays: 15
             contentPath: "/content"
             types: ["Activate", "Deactivate", "Delete", "Test", "Reverse", "Internal Poll"]
         - pages:
             maximumAgeDays: 15
             contentPath: "/content"
             types: ["PageCreated", "PageModified", "PageMoved", "PageDeleted", "VersionCreated", "PageRestored", "PageValid", "PageInvalid"]
         - dam:
             maximumAgeDays: 15
             contentPath: "/content"
             types: ["ASSET_EXPIRING", "METADATA_UPDATED", "ASSET_EXPIRED", "ASSET_REMOVED", "RESTORED", "ASSET_MOVED", "ASSET_VIEWED", "PROJECT_VIEWED", "PUBLISHED_EXTERNAL", "COLLECTION_VIEWED", "VERSIONED", "ADDED_COMMENT", "RENDITION_UPDATED", "ACCEPTED", "DOWNLOADED", "SUBASSET_UPDATED", "SUBASSET_REMOVED", "ASSET_CREATED", "ASSET_SHARED", "RENDITION_REMOVED", "ASSET_PUBLISHED", "ORIGINAL_UPDATED", "RENDITION_DOWNLOADED", "REJECTED"]
   ```

   Lembre-se de que para que a configuração seja válida:

   * todas as propriedades devem ser definidas. Não há padrões herdados.
   * os tipos (números inteiros, strings, booleanos etc.) nas tabelas de propriedades abaixo devem ser respeitados.

1. Crie um pipeline de configuração no Cloud Manager, conforme descrito no [artigo sobre configuração de pipeline](/help/operations/config-pipeline.md#managing-in-cloud-manager).

### Remoção da versão {#version-purge}

>[!NOTE]
>
>Os clientes do AEM Guides não devem configurar a Limpeza de versão.

#### Padrões de Expurgação de Versão {#version-purge-defaults}

<!-- For version purging, environments with an id higher than **TBD** have the following default values: -->

Atualmente, a limpeza não está habilitada por padrão, mas isso será alterado no futuro.

Os ambientes criados após a ativação da limpeza padrão terão os seguintes valores padrão:

* Versões com mais de 30 dias são removidas.
* As cinco versões mais recentes nos últimos 30 dias são mantidas.
* Independentemente das regras acima, a versão mais recente (além do arquivo atual) é preservada.

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

Os ambientes criados antes da limpeza padrão estarem habilitados terão os valores padrão listados abaixo, no entanto, é recomendável reduzir esses valores para otimizar o desempenho.

* Versões com mais de 7 anos são removidas.
* Todas as versões nos últimos sete anos são mantidas.
* Após 7 anos, versões diferentes da versão mais recente (além do arquivo atual) são removidas.

#### Propriedades de limpeza de versão {#version-purge-properties}

As propriedades permitidas estão listadas abaixo.

As colunas que indicam *padrão* indicam os valores padrão no futuro, quando os padrões são aplicados; *TBD* reflete uma ID de ambiente que ainda não foi determinada.

| Propriedades | padrão futuro para envs>TBD | padrão futuro para envs&lt;=TBD | obrigatório | tipo | Valores |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| caminhos | [&quot;/conteúdo&quot;] | [&quot;/conteúdo&quot;] | Sim | matriz de strings | Especifica em quais caminhos as versões serão removidas quando novas versões forem criadas.  Os clientes devem declarar essa propriedade, mas o único valor permitido é &quot;/content&quot;. |
| maximumAgeDays | 30 | 2557 (7 anos + 2 dias bissextos) | Sim | Número inteiro | Qualquer versão anterior ao valor configurado é removida. Se o valor for 0, a limpeza não será executada com base na idade da versão. |
| maximumVersions | 5 | 0 (sem limite) | Sim | Número inteiro | Qualquer versão anterior à n-ésima versão mais recente é removida. Se o valor for 0, a limpeza não será executada com base no número de versões. |
| minimumVersions | 1 | 1 | Sim | Número inteiro | O número mínimo de versões que são mantidas independentemente da idade. Observe que pelo menos 1 versão é sempre mantida; seu valor deve ser 1 ou superior. |
| keepLabelledVersioned | falso | falso | Sim | booleano | Determina se as versões rotuladas explicitamente serão excluídas da limpeza. Para obter uma melhor otimização do repositório, é recomendável definir esse valor como false. |

**Interações de propriedade**

Os exemplos a seguir ilustram como as propriedades interagem quando combinadas.

Exemplo:

```
maximumAgeDays = 30
maximumVersions = 10
minimumVersions = 2
```

Se houver 11 versões no dia 23, a versão mais antiga será removida na próxima vez que a tarefa de manutenção de limpeza for executada, já que a propriedade `maximumVersions` está definida como 10.

Se houver 5 versões no dia 31, somente 3 serão removidas, pois a propriedade `minimumVersions` está definida como 2.

Exemplo:

```
maximumAgeDays = 30
maximumVersions = 0
minimumVersions = 1
```

Nenhuma versão com mais de 30 dias será removida, pois a propriedade `maximumVersions` está definida como 0.

Uma versão com mais de 30 dias será mantida.

### Limpeza do log de auditoria {#audit-purge}

#### Padrões de Expurgação de Log de Auditoria {#audit-purge-defaults}

<!-- For audit log purging, environments with an id higher than **TBD** have the following default values: -->

Atualmente, a limpeza não está habilitada por padrão, mas isso será alterado no futuro.

Os ambientes criados após a ativação da limpeza padrão terão os seguintes valores padrão:

* Os logs de auditoria de replicação, DAM e página com mais de 7 dias são removidos.
* Todos os eventos possíveis são registrados.

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

Os ambientes criados antes da limpeza padrão estarem habilitados terão os valores padrão listados abaixo, no entanto, é recomendável reduzir esses valores para otimizar o desempenho.

* Replicação, DAM e logs de auditoria de página com mais de 7 anos são removidos.
* Todos os eventos possíveis são registrados.

>[!NOTE]
>Recomenda-se que os clientes que têm requisitos normativos para produzir logs de auditoria não editáveis se integrem a serviços externos especializados.

#### Propriedades de limpeza de log de auditoria {#audit-purge-properties}

As propriedades permitidas estão listadas abaixo.

As colunas que indicam *padrão* indicam os valores padrão no futuro, quando os padrões são aplicados; *TBD* reflete uma ID de ambiente que ainda não foi determinada.

| Propriedades | padrão futuro para envs>TBD | padrão futuro para envs&lt;=TBD | obrigatório | tipo | Valores |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| regras | - | - | Sim | Objeto | Um ou mais dos seguintes nós: replicação, páginas, dam. Cada um desses nós define regras, com as propriedades abaixo. Todas as propriedades devem ser declaradas. |
| maximumAgeDays | 7 dias | 2557 (7 anos + 2 dias bissextos) | Sim | inteiro | Para replicação, páginas ou DAM: o número de dias que os logs de auditoria são mantidos. Os logs de auditoria anteriores ao valor configurado são removidos. |
| contentPath | &quot;/content&quot; | &quot;/content&quot; | Sim | String | O caminho sob o qual os logs de auditoria serão removidos para o tipo relacionado. Deve ser definido como &quot;/content&quot;. |
| tipos | todos os valores | todos os valores | Sim | Matriz de enumeração | Para **replicação**, os valores enumerados são: Ativar, Desativar, Excluir, Testar, Reverter, Sondagem Interna. Para **páginas**, os valores enumerados são: PageCreated, PageModified, PageMoved, PageDeleted, VersionCreated, PageRestoring, PageRolled Out, PageValid, PageInvalid. Para **dam**, os valores enumerados são: ASSET_EXPIRING, METADATA_UPDATED, ASSET_EXPIRED, ASSET_REMOVED, RESTORED, ASSET_MOVED, ASSET_VIEWED, PROJECT_VIEWED, PUBLISHED_EXTERNAL, COLLECTION_VIEWED, VERSIONED, ADDED_COMMENT, RENDITION_UPDATED, ACCEPTED, DOWNLOADED, SUBASSET_UPDATED, SUBASSET_REMOVED, ASSET_CREATED, ASSET_SHARED, RENDITION_REMOVED, ASSET_PUBLISHED, ORIGINAL_UPDATED, RENDITION_DOWNLOADED, REJECTED. |
