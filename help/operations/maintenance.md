---
title: Tarefas de manutenção no AEM as a Cloud Service
description: Tarefas de manutenção no AEM as a Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 6af0a140005bcc684c72151024affb117437f6ce
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 4%

---

# Tarefas de manutenção no AEM as a Cloud Service

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="Tarefas de manutenção"
>abstract="Tarefas de manutenção são processos que são executados de acordo com uma programação para otimizar o repositório. Com AEM as a Cloud Service, a necessidade de os clientes configurarem as propriedades operacionais das tarefas de manutenção é mínima. Os clientes podem concentrar seus recursos em preocupações no nível do aplicativo, deixando as operações de infraestrutura para o Adobe."

Tarefas de manutenção são processos que são executados de acordo com uma programação para otimizar o repositório. Com AEM as a Cloud Service, a necessidade de os clientes configurarem as propriedades operacionais das tarefas de manutenção é mínima. Os clientes podem concentrar seus recursos em preocupações no nível do aplicativo, deixando as operações de infraestrutura para o Adobe.

## Configurar tarefas de manutenção

Em versões anteriores do AEM, você podia configurar tarefas de manutenção usando o Cartão de manutenção (Ferramentas > Operações > Manutenção). Para AEM as a Cloud Service, o Cartão de Manutenção não está mais disponível, portanto, as configurações devem ser comprometidas com o controle de origem e implantadas usando o Cloud Manager. O Adobe gerencia as tarefas de manutenção que têm configurações que não são configuráveis pelos clientes (por exemplo, coleta de lixo do armazenamento de dados, limpeza de log de auditoria, limpeza de versão). Outras tarefas de manutenção podem ser configuradas pelos clientes, conforme descrito na tabela abaixo.

>[!CAUTION]
>
>O Adobe reserva o direito de substituir as configurações da tarefa de manutenção de um cliente para atenuar problemas como degradação de desempenho.

A tabela a seguir ilustra as tarefas de manutenção disponíveis no momento do lançamento AEM as a Cloud Service.

<!--| Maintenance Task | Who owns the configuration | How to configure (optional)  |
|---|---|---|
| Datastore garbage collection | Adobe | N/A - fully Adobe owned |
| Version Purge | Adobe | Fully owned by Adobe, but in the future, customers will be able to configure certain parameters. |
| Audit Log Purge  | Adobe | Fully owned by Adobe, but in the future, customers will be able to configure certain parameters. |
| Lucene Binaries Cleanup | Adobe | Unused and therefore disabled by Adobe. |
| Ad-hoc Task Purge | Customer | Must be done in git. <br> Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the the folder `/apps/settings/granite/operations/maintenance/granite_weekly` or `granite_daily`. See the Maintenance Window table below for additional configuration details. <br> Enable the maintenance task by adding another node under the node above (name it `granite_TaskPurgeTask`) with the appropriate properties. <br> Configure the OSGI properties see the [AEM 6.5 Maintenance Task documentation](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)|
| Workflow Purge | Customer |  Must be done in git. <br> Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the the folder`/apps/settings/granite/operations/maintenance/granite_weekly` or `granite_daily`. See the Maintenance Window table below for additional configuration details. <br> Enable the maintenance task by adding another node under the node above (name it `granite_WorkflowPurgeTask`) with the appropriate properties. <br> Configure the OSGI properties see [AEM 6.5 Maintenance Task documentation](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Project Purge | Customer |  Must be done in git. <br> Override the out-of-the-box Maintenance window configuration node under `/libs` by creating properties under the the folder `/apps/settings/granite/operations/maintenance/granite_weekly` or `granite_daily`. See the Maintenance Window table below for additional configuration details. <br> Enable the maintenance task by adding a node under the node above (name it `granite_ProjectPurgeTask`) with the appropriate properties. <br> Configure OSGI properties see [AEM 6.5 Maintenance Task documentation](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

Customers can schedule each of the Workflow Purge, Ad-hoc Task Purge and Project Purge Maintenance tasks to be executed during the daily, weekly, or monthly maintenance windows. These configurations should be edited directly in source control. The table below describes the configuration parameters available for each of the window. Also, see the locations and code samples provided after the table.-->

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
    <td>N/A - de propriedade totalmente Adobe</td>
  </td> 
  </tr>
  <tr>
    <td>Remoção da versão</td>
    <td>Adobe</td>
    <td>Para que o nível de criação permaneça executante, as versões mais antigas de cada parte do conteúdo na variável <code>/content</code> nó do repositório são removidos de acordo com o seguinte comportamento:<br><br> <!--Alexandru: please leave the two line breaks in place, otherwise spacing won't render properly-->
     <ol>
       <li>Versões com mais de 30 dias são removidas</li>
       <li>As 5 versões mais recentes nos últimos 30 dias são mantidas</li>
       <li>Independentemente das regras acima, a versão mais recente é preservada.</li>
     </ol><br>OBSERVAÇÃO: o comportamento descrito acima é aplicado a novos ambientes a partir de 14 de março de 2022 e será aplicado a ambientes existentes (aqueles que foram criados antes de 14 de março de 2022) em 21 de abril de 2022.</td>
  </td>
  </tr>
  <tr>
    <td>Limpeza de Log de Auditoria</td>
    <td>Adobe</td>
    <td>Para que o nível de criação permaneça executante, os registros de auditoria mais antigos serão registrados sob a <code>/content</code> nó do repositório são removidos de acordo com o seguinte comportamento:<br><br> <!-- See above for the two line breaks -->
     <ol>
       <li>Para auditoria de replicação, os logs de auditoria com mais de 3 dias são removidos</li>
       <li>Para auditoria do DAM (Assets), os logs de auditoria com mais de 30 dias são removidos</li>
       <li>Para auditoria de página, os logs com mais de 3 dias são removidos.</li>
     </ol><br>OBSERVAÇÃO: o comportamento descrito acima é aplicado a novos ambientes a partir de 14 de março de 2022 e será aplicado a ambientes existentes (aqueles que foram criados antes de 14 de março de 2022) em 21 de abril de 2022.</td>
   </td>
  </tr>
  <tr>
    <td>Limpeza de binários do Lucene</td>
    <td>Adobe</td>
    <td>Não usado e, portanto, desabilitado pelo Adobe.</td>
  </td>
  </tr>
  <tr>
    <td>Limpeza de tarefa ad-hoc</td>
    <td>Cliente</td>
    <td>
    <p>Deve ser feito no git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code> criando propriedades na pasta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> ou <code>granite_daily</code>.</p>
    <p>Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração. Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o <code>granite_TaskPurgeTask</code>) com as propriedades apropriadas. Para configurar as propriedades do OSGI, consulte a <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">Documentação da Tarefa de manutenção do AEM 6.5</a>.</p>
  </td>
  </tr>
    <tr>
    <td>Remoção do fluxo de trabalho</td>
    <td>Cliente</td>
    <td>
    <p>Deve ser feito no git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code> criando propriedades na pasta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> ou <code>granite_daily</code>. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração.</p>
    <p>Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o <code>granite_WorkflowPurgeTask</code>) com as propriedades apropriadas. Configure as propriedades OSGI, consulte <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">Documentação da Tarefa de manutenção do AEM 6.5</a>.</p>
  </td>
  </tr>
  <tr>
    <td>Remoção do projeto</td>
    <td>Cliente</td>
    <td>
    <p>Deve ser feito no git. Substitua o nó de configuração da janela de manutenção pronto para uso em <code>/libs</code> criando propriedades na pasta <code>/apps/settings/granite/operations/maintenance/granite_weekly</code> ou <code>granite_daily</code>. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração.</p>
    <p>Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o <code>granite_ProjectPurgeTask</code>) com as propriedades apropriadas. Configure as propriedades OSGI, consulte <a href="https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html">Documentação da Tarefa de manutenção do AEM 6.5</a>.</p>
  </td>
  </tr>
  </tbody>
</table>

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>Configuração da Janela de Manutenção</th>
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
  <p><strong>windowStartTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Diária devem começar a ser executadas.</p>
  <p><strong>windowEndTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Diária devem parar de ser executadas se ainda não tiverem sido concluídas.</p>
  </td> 
  </tr>
  <tr>
    <td>Semanalmente</td>
    <td>Cliente</td>
    <td>Definição de Nó JCR</td>
    <td>
    <p><strong>windowSchedule=weekly</strong> (esse valor não deve ser alterado)</p>
    <p><strong>windowStartTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção semanal devem começar a ser executadas.</p>
    <p><strong>windowEndTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Semanal devem parar de ser executadas caso ainda não tenham sido concluídas.</p>
    <p><strong>windowScheduleWeekdays= Matriz de 2 valores de 1 a 7 (por exemplo, [5,5]</strong> O primeiro valor da matriz é o dia de início em que a tarefa é agendada e o segundo valor é o dia de término em que a tarefa seria interrompida. A hora exata do início e do fim é regida por windowStartTime e windowEndTime, respectivamente.</p>
    </td>
  </tr>
  <tr>
    <td>Mensalmente</td>
    <td>Cliente</td>
    <td>Definição de Nó JCR</td>
    <td>
    <p><strong>windowSchedule=daily</strong> (esse valor não deve ser alterado)</p>
    <p><strong>windowStartTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Mensal devem começar a ser executadas.</p>
    <p><strong>windowEndTime=HH:MM</strong> usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Mensal devem parar de ser executadas se ainda não tiverem sido concluídas.</p>
    <p><strong>windowScheduleWeekdays=Array de 2 valores de 1 a 7 (por exemplo, [5,5]</strong> O primeiro valor da matriz é o dia de início em que a tarefa é agendada e o segundo valor é o dia de término em que a tarefa seria interrompida. A hora exata do início e do fim é regida por windowStartTime e windowEndTime, respectivamente.</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 para agendar na primeira semana do mês ou 1 para agendar na última semana do mês. A ausência de um valor agendaria efetivamente trabalhos todos os dias, conforme determinado por windowScheduleWeekdays todos os meses.</p>
    </td> 
    </tr>
    </tbody>
</table>

**Localizações**:

* Diariamente - /apps/settings/granite/operations/maintenance/granite_daily
* Semanalmente - /apps/settings/granite/operations/maintenance/granite_weekly
* Mensalmente - /apps/settings/granite/operations/maintenance/granite_mensal

**Amostras de código**:

Amostra de código 1 (diariamente)

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

Amostra de código 2 (semanalmente)

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

Amostra de código 3 (mensalmente)

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
