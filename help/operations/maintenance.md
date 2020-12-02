---
title: Tarefas de manutenção em AEM como Cloud Service
description: 'Tarefas de manutenção em AEM como Cloud Service '
translation-type: tm+mt
source-git-commit: c3af507716ef60541ecca8dafb797651e8ece9d3
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 2%

---


# Tarefas de manutenção em AEM como Cloud Service

Tarefas de manutenção são processos que são executados de acordo com uma programação para otimizar o repositório. Com AEM como Cloud Service, a necessidade de os clientes configurarem as propriedades operacionais das tarefas de manutenção é mínima. Os clientes podem focar seus recursos em preocupações no nível do aplicativo, deixando as operações de infraestrutura para a Adobe.

Para obter informações adicionais sobre tarefas de manutenção, consulte as seguintes páginas:

* [Guia de manutenção de AEM](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [Tarefas de manutenção do Painel de operações](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## Configuração de tarefas de manutenção

Em versões anteriores do AEM, você poderia configurar tarefas de manutenção usando o Cartão de manutenção (Ferramentas > Operações > Manutenção). Para AEM como Cloud Service, a placa de manutenção não está mais disponível, portanto, as configurações devem ser confirmadas no controle de origem e implantadas usando o Gerenciador de nuvem. O Adobe gerenciará tarefas de manutenção que não exigem decisões do cliente (por exemplo, coleta de lixo do armazenamento de dados) enquanto outras tarefas de manutenção podem ser configuradas pelo cliente (consulte a tabela abaixo).

>[!CAUTION]
>
>O Adobe reserva-se o direito de substituir as configurações de tarefa de manutenção de um cliente para atenuar problemas como degradação do desempenho.

A tabela a seguir ilustra as tarefas de manutenção disponíveis no momento do lançamento do AEM como Cloud Service.

| Tarefa de manutenção | Quem é o proprietário da configuração | Como configurar (opcional) |
|---|---|---|
| Coleta de lixo de armazenamento de dados | Adobe | N/A - propriedade totalmente Adobe |
| Remoção da versão | Adobe | Totalmente pertencente à Adobe, mas no futuro os clientes poderão configurar determinados parâmetros. |
| Expurgação do Log de Auditoria | Adobe | Totalmente pertencente à Adobe, mas no futuro os clientes poderão configurar determinados parâmetros. |
| Limpeza de binários do Lucene | Adobe | Não utilizado e, portanto, desativado pelo Adobe. |
| Expurgação de Tarefa ad-hoc | Cliente | Deve ser feito de presente. <br> Substitua o nó de configuração predefinido da janela Manutenção em  `/libs` criando propriedades na pasta  `/apps/settings/granite/operations/maintenance/granite_weekly` ou  `granite_daily`. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração. <br> Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o  `granite_TaskPurgeTask`) com as propriedades apropriadas. <br> Configure as propriedades do OSGI para ver a documentação da Tarefa de manutenção  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Remoção do fluxo de trabalho | Cliente | Deve ser feito de presente. <br> Substitua o nó de configuração predefinido da janela Manutenção em  `/libs` criando propriedades sob a `/apps/settings/granite/operations/maintenance/granite_weekly` pasta  `granite_daily`. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração. <br> Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o  `granite_WorkflowPurgeTask`) com as propriedades apropriadas. <br> Configure as propriedades do OSGI consulte a documentação da Tarefa de manutenção  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Remoção do projeto | Cliente | Deve ser feito de presente. <br> Substitua o nó de configuração predefinido da janela Manutenção em  `/libs` criando propriedades na pasta  `/apps/settings/granite/operations/maintenance/granite_weekly` ou  `granite_daily`. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração. <br> Ative a tarefa de manutenção adicionando um nó sob o nó acima (nomeie-o  `granite_ProjectPurgeTask`) com as propriedades apropriadas. <br> Configurar propriedades OSGI consulte a documentação da Tarefa de manutenção  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

Os clientes podem programar cada uma das tarefas de Expurgação do Fluxo de Trabalho, Expurgação de Tarefa Ad-hoc e Manutenção de Expurgação do Projeto para serem executadas durante as janelas de manutenção diária, semanal ou mensal. Essas configurações devem ser editadas diretamente no controle de origem. A tabela abaixo descreve os parâmetros de configuração disponíveis para cada janela.

<table>
  <tr>
    <th>Configuração da janela de manutenção</th>
    <th>Quem é o proprietário da configuração</th>
    <th>Tipo de configuração</th>
    <th>Local</th>
    <th>Exemplo</th>
    <th>Parâmetros</th>
  </tr>
  <tr>
    <td>Diariamente</td>
    <td>Cliente</td>
    <td>Definição de nó JCR</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_daily </code></td>
    <td>Consulte a amostra de código 1 abaixo</td>
   <td>
    <ul>
    <li><strong>windowSchedule</strong> = diariamente (este valor não deve ser alterado)</li>
    <li><strong>windowStartTime</strong> = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Diária devem começar a ser executadas.</li>
    <li><strong>windowEndTime</strong> = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Diária devem parar de ser executadas se ainda não tiverem sido concluídas.</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>Semanalmente</td>
    <td>Cliente</td>
    <td>Definição de nó JCR</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_weekly</code></td>
    <td>Consulte o código exemplo 2 abaixo</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = week (este valor não deve ser alterado)</li>
    <li><strong>windowStartTime</strong> = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de manutenção associadas à Janela de manutenção semanal devem começar a ser executadas.</li>
    <li><strong>windowEndTime</strong> = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Semanal devem parar de ser executadas se ainda não tiverem sido concluídas.</li>
    <li><strong>windowScheduleWeekdays = Matriz de 2 valores de 1 a 7. por exemplo, [5,5].</strong> O primeiro valor da matriz é o dia de start quando a tarefa é programada e o segundo valor é o dia de término quando a tarefa seria interrompida. A hora exata do start e do fim é regida por windowStartTime e windowEndTime, respectivamente.</li>
    </ul> </td> 
  </tr>
  <tr>
    <td>Mensalmente</td>
    <td>Cliente</td>
    <td>Definição de nó JCR</td>
    <td><code>/apps/settings/granite/operations/maintenance/granite_monthly</code></td>
    <td>Consulte o código exemplo 3 abaixo</td>
     <td>
    <ul>
    <li><strong>windowSchedule</strong> = diariamente (este valor não deve ser alterado)</li>
    <li><strong>windowStartTime</strong> = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de manutenção associadas à Janela de manutenção mensal devem começar a ser executadas.</li>
    <li><strong>windowEndTime</strong> = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Mensal devem parar de ser executadas se ainda não tiverem sido concluídas.</li>
    <li><strong>windowScheduleWeekdays = Matriz de 2 valores de 1 a 7. por exemplo, [5,5].</strong> O primeiro valor da matriz é o dia de start quando a tarefa é programada e o segundo valor é o dia de término quando a tarefa seria interrompida. A hora exata do start e do fim é regida por windowStartTime e windowEndTime, respectivamente.</li>
    <li><strong>windowFirstLastStartDay - 0/1</strong> 0 para agendar na primeira semana do mês ou 1 para agendar na última semana do mês. A ausência de um valor programaria efetivamente jobs todos os dias, conforme governado por windowScheduleWeekdays a cada mês.</li>
    </ul> </td> 
  </tr>
</table>

Amostra de código 1

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

Amostra de código 2

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

Amostra de código 3

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
