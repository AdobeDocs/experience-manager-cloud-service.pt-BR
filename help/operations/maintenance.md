---
title: Tarefas de manutenção no AEM as a Cloud Service
description: Tarefas de manutenção no AEM as a Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 63%

---

# Tarefas de manutenção no AEM as a Cloud Service {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="Tarefas de manutenção"
>abstract="Tarefas de manutenção são processos executados de acordo com um cronograma para otimizar o repositório. Com o AEM as a Cloud Service, a necessidade de os clientes configurarem as propriedades operacionais das tarefas de manutenção é mínima. Os clientes podem concentrar seus recursos em preocupações no nível do aplicativo, deixando as operações de infraestrutura para a Adobe."

Tarefas de manutenção são processos executados de acordo com um cronograma para otimizar o repositório. Com o AEM as a Cloud Service, a necessidade de os clientes configurarem as propriedades operacionais das tarefas de manutenção é mínima. Os clientes podem concentrar seus recursos em preocupações no nível do aplicativo, deixando as operações de infraestrutura para a Adobe.

## Configurar tarefas de manutenção {#maintenance-tasks-configuring}

Em versões anteriores do AEM, você podia configurar as tarefas de manutenção usando o Cartão de manutenção (Ferramentas > Operações > Manutenção). Para o AEM as a Cloud Service, o Cartão de manutenção não está mais disponível, portanto, as configurações devem ser enviadas ao controle de origem e implantadas usando o Cloud Manager. A Adobe gerencia as tarefas de manutenção que têm configurações não configuráveis pelos clientes (por exemplo, coleta de lixo do armazenamento de dados, limpeza de log de auditoria, limpeza de versão). Outras tarefas de manutenção podem ser configuradas pelos clientes, conforme descrito na tabela abaixo.

>[!CAUTION]
>
>O Adobe reserva o direito de substituir as configurações da tarefa de manutenção de um cliente para atenuar problemas como degradação de desempenho.

A tabela a seguir ilustra as tarefas de manutenção disponíveis no momento do lançamento do AEM as a Cloud Service.

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
    <td>Adobe</td>
    <td>Para ambientes existentes (aqueles criados antes de 1° de junho de 2023), a limpeza está desativada e não será ativada no futuro, a menos que seja explicitamente ativada pelo cliente, momento em que ele também poderá configurá-la com valores personalizados.<br><br> <!--Alexandru: leave the two line breaks in place, otherwise spacing won't render properly-->Os novos ambientes (criados a partir de 1 de junho de 2023) terão a limpeza ativada por padrão com os valores abaixo, com os clientes podendo configurar com valores personalizados.
     <ol>
       <li>Versões com mais de 30 dias são removidas</li>
       <li>As 5 versões mais recentes nos últimos 30 dias são mantidas</li>
       <li>Independentemente das regras acima, a versão mais recente é preservada.</li>
       <br>Recomenda-se que os clientes que têm requisitos normativos para renderizar as páginas do site exatamente como aparecem em uma data específica se integrem a serviços externos especializados.
     </ol></td>
  </td>
  </tr>
  <tr>
    <td>Limpeza do log de auditoria</td>
    <td>Adobe</td>
    <td>Para ambientes existentes (aqueles criados antes de 1° de junho de 2023), a limpeza está desativada e não será ativada no futuro, a menos que seja explicitamente ativada pelo cliente, momento em que ele também poderá configurá-la com valores personalizados.<br><br> <!-- See above for the two line breaks -->Os novos ambientes (criados a partir de 1º de junho de 2023) terão a limpeza ativada por padrão no <code>/content</code> do repositório de acordo com o seguinte comportamento:
     <ol>
       <li>Para auditoria de replicação, os logs de auditoria com mais de 3 dias são removidos</li>
       <li>Para auditoria do DAM (Assets), os logs de auditoria com mais de 30 dias são removidos</li>
       <li>Para auditoria de página, os logs com mais de 3 dias são removidos.</li>
       <br>Recomenda-se que os clientes que têm requisitos normativos para produzir logs de auditoria não editáveis se integrem a serviços externos especializados.
     </ol></td>
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
    <p>Deve ser feito no Git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code> criando propriedades na pasta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> ou <code>granite_monthly</code>.</p>
    <p>Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração. Ative a tarefa de manutenção adicionando outro nó sob o nó acima. Nomear como <code>granite_TaskPurgeTask</code>, com atributo <code>sling:resourceType</code> definir como <code>granite/operations/components/maintenance/task</code> atributo e <code>granite.maintenance.name</code> definir como <code>TaskPurge</code>. Para configurar as propriedades OSGI, consulte <code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code> para obter a lista de propriedades.</p>
  </td>
  </tr>
    <tr>
    <td>Remoção do fluxo de trabalho</td>
    <td>Cliente</td>
    <td>
    <p>Deve ser feito no Git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code> criando propriedades na pasta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> ou <code>granite_monthly</code>. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração.</p>
    <p>Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o como <code>granite_WorkflowPurgeTask</code>) com as propriedades adequadas. Para configurar as propriedades do OSGI, consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html?lang=pt-BR#regular-purging-of-workflow-instances">Documentação da tarefa de manutenção do AEM 6.5</a>.</p>
  </td>
  </tr>
  <tr>
    <td>Remoção do projeto</td>
    <td>Cliente</td>
    <td>
    <p>Deve ser feito no Git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code> criando propriedades na pasta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>, <code>granite_daily</code> ou <code>granite_monthly</code>. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração.</p>
    <p>Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o como <code>granite_ProjectPurgeTask</code>) com as propriedades apropriadas. Consulte a lista de propriedades OSGI em "Configuração de limpeza de projetos Adobe".</p>
  </td>
  </tr>
  </tbody>
</table>

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
    <p><strong>windowScheduleWeekdays= Matriz de dois valores de 1 a 7 (por exemplo, [5,5])</strong> O primeiro valor da matriz é o dia de início em que a tarefa é agendada e o segundo valor é o dia de término em que a tarefa será interrompida. A hora exata de início e término é regida pelos parâmetros windowStartTime e windowEndTime, respectivamente.</p>
    </td>
  </tr>
  <tr>
    <td>Mensalmente</td>
    <td>Cliente</td>
    <td>Definição de Nó JCR</td>
    <td>
    <p><strong>windowSchedule=month</strong> (este valor não deve ser alterado)</p>
    <p><strong>windowStartTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as tarefas de manutenção associadas à Janela de manutenção mensal devem começar a ser executadas.</p>
    <p><strong>windowEndTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as tarefas de manutenção associadas à Janela de manutenção mensal devem parar de ser executadas se ainda não tiverem sido concluídas.</p>
    <p>Uma tarefa de manutenção não pode ser executada mais de uma vez durante esse período.</p>
    <p><strong>windowScheduleWeekdays=Matriz de dois valores de 1 a 7 (por exemplo, [5,5])</strong> O primeiro valor da matriz é o dia de início em que a tarefa é agendada e o segundo valor é o dia de término em que a tarefa será interrompida. A hora exata de início e término é regida pelos parâmetros windowStartTime e windowEndTime, respectivamente.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 para agendar na primeira semana do mês ou 1 para agendar na última semana do mês. A ausência de um valor agendaria trabalhos no dia regido por windowScheduleWeekdays (todos os meses).</p>
    </td>
    </tr>
    </tbody>
</table>

**Localizações**:

* Diariamente - /apps/settings/granite/operations/maintenance/granite_daily
* Semanalmente - /apps/settings/granite/operations/maintenance/granite_weekly
* Mensalmente - /apps/settings/granite/operations/maintenance/granite_monthly

**Exemplos de código**:

Exemplo de código 1 (diariamente)

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

Exemplo de código 2 (semanalmente)

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

Exemplo de código 3 (mensalmente)

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
