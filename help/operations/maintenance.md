---
title: Tarefas de manutenção no AEM as a Cloud Service
description: Tarefas de manutenção no AEM as a Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: def7f7071dac447397f40186de1380b8e5575608
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 100%

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
>A Adobe reserva o direito de substituir as configurações da tarefa de manutenção de um cliente para atenuar problemas como degradação de desempenho.

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
    <td>Para que o nível de criação permaneça com bom desempenho, as versões mais antigas de cada parte do conteúdo no nó <code>/content</code> do repositório são removidas de acordo com o seguinte comportamento:<br><br> <!--Alexandru: please leave the two line breaks in place, otherwise spacing won't render properly-->
     <ol>
       <li>Versões com mais de 30 dias são removidas</li>
       <li>As 5 versões mais recentes nos últimos 30 dias são mantidas</li>
       <li>Independentemente das regras acima, a versão mais recente é preservada.</li>
     </ol><br>OBSERVAÇÃO: o comportamento descrito acima é aplicado por padrão para novos ambientes criados após 14 de março de 2022. Envie um tíquete de suporte ao cliente se você precisar de configurações diferentes.</td>
  </td>
  </tr>
  <tr>
    <td>Limpeza do log de auditoria</td>
    <td>Adobe</td>
    <td>Para que o nível de criação permaneça com bom desempenho, os registros de auditoria mais antigos sob o nó <code>/content</code> do repositório são removidos de acordo com o seguinte comportamento:<br><br> <!-- See above for the two line breaks -->
     <ol>
       <li>Para auditoria de replicação, os logs de auditoria com mais de 3 dias são removidos</li>
       <li>Para auditoria do DAM (Assets), os logs de auditoria com mais de 30 dias são removidos</li>
       <li>Para auditoria de página, os logs com mais de 3 dias são removidos.</li>
     </ol><br>OBSERVAÇÃO: o comportamento descrito acima é aplicado por padrão a novos ambientes criados após 14 de março de 2022. Envie um tíquete de suporte ao cliente se você precisar de configurações diferentes.</td>
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
    <p>Deve ser feito no Git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code>, criando propriedades na pasta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> ou <code>granite_daily</code>.</p>
    <p>Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração. Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o como <code>granite_TaskPurgeTask</code>) com as propriedades adequadas. Configure as propriedades OSGI.</p>
  </td>
  </tr>
    <tr>
    <td>Remoção do fluxo de trabalho</td>
    <td>Cliente</td>
    <td>
    <p>Deve ser feito no Git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code>, criando propriedades na pasta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> ou <code>granite_daily</code>. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração.</p>
    <p>Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o como <code>granite_WorkflowPurgeTask</code>) com as propriedades adequadas. Para configurar as propriedades do OSGI, consulte <a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html?lang=pt-BR#regular-purging-of-workflow-instances">Documentação da tarefa de manutenção do AEM 6.5</a>.</p>
  </td>
  </tr>
  <tr>
    <td>Remoção do projeto</td>
    <td>Cliente</td>
    <td>
    <p>Deve ser feito no Git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code>, criando propriedades na pasta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> ou <code>granite_daily</code>. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração.</p>
    <p>Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o como <code>granite_ProjectPurgeTask</code>) com as propriedades apropriadas. Configure as propriedades OSGI.</p>
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
    <p><strong>windowScheduleWeekdays= Matriz de 2 valores de 1 a 7 (por exemplo, [5,5])</strong> O primeiro valor da matriz é o dia de início em que a tarefa é agendada e o segundo valor é o dia de término em que a tarefa será interrompida. A hora exata de início e término é regida pelos parâmetros windowStartTime e windowEndTime, respectivamente.</p>
    </td>
  </tr>
  <tr>
    <td>Mensalmente</td>
    <td>Cliente</td>
    <td>Definição de Nó JCR</td>
    <td>
    <p><strong>windowSchedule=daily</strong> (esse valor não deve ser alterado)</p>
    <p><strong>windowStartTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as tarefas de manutenção associadas à Janela de manutenção mensal devem começar a ser executadas.</p>
    <p><strong>windowEndTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as tarefas de manutenção associadas à Janela de manutenção mensal devem parar de ser executadas se ainda não tiverem sido concluídas.</p>
    <p><strong>windowScheduleWeekdays=Matriz de 2 valores de 1 a 7 (por exemplo, [5,5])</strong> O primeiro valor da matriz é o dia de início em que a tarefa é agendada e o segundo valor é o dia de término em que a tarefa será interrompida. A hora exata de início e término é regida pelos parâmetros windowStartTime e windowEndTime, respectivamente.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 para agendar na primeira semana do mês ou 1 para agendar na última semana do mês. A ausência de um valor agendaria trabalhos todos os dias, conforme determinado por windowScheduleWeekdays todos os meses.</p>
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
