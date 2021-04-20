---
title: Tarefas de manutenção no AEM como Cloud Service
description: Tarefas de manutenção no AEM como Cloud Service
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
translation-type: tm+mt
source-git-commit: 8adead735a5c3c0a03ee6f81372c1714634932ec
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 2%

---

# Tarefas de manutenção no AEM como Cloud Service

Tarefas de manutenção são processos que são executados de acordo com uma programação para otimizar o repositório. Com o AEM como Cloud Service, a necessidade de os clientes configurarem as propriedades operacionais das tarefas de manutenção é mínima. Os clientes podem concentrar seus recursos em preocupações no nível do aplicativo, deixando as operações de infraestrutura para o Adobe.

Para obter informações adicionais sobre tarefas de manutenção, consulte as seguintes páginas:

* [Guia de manutenção de AEM](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html)
* [Tarefas de manutenção do Painel de operações](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/operations-dashboard.html#AutomatedMaintenanceTasks)

## Configurar tarefas de manutenção

Em versões anteriores do AEM, você podia configurar tarefas de manutenção usando o Cartão de manutenção (Ferramentas > Operações > Manutenção). Para o AEM as a Cloud Service, a placa de manutenção não está mais disponível, portanto, as configurações devem ser comprometidas com o controle de origem e implantadas usando o Cloud Manager. O Adobe gerenciará tarefas de manutenção que não exigem decisões do cliente (por exemplo, Datastore Garbage Collection), enquanto outras tarefas de manutenção podem ser configuradas pelo cliente (consulte a tabela abaixo).

>[!CAUTION]
>
>O Adobe reserva o direito de substituir as configurações da tarefa de manutenção de um cliente para atenuar problemas como degradação de desempenho.

A tabela a seguir ilustra as tarefas de manutenção disponíveis no momento do lançamento do AEM como Cloud Service.

| Tarefa de manutenção | Quem é o proprietário da configuração | Como configurar (opcional) |
|---|---|---|
| Coleta de lixo do armazenamento de dados | Adobe | N/A - de propriedade totalmente Adobe |
| Remoção da versão | Adobe | Propriedade total do Adobe, mas no futuro os clientes poderão configurar determinados parâmetros. |
| Limpeza de Log de Auditoria | Adobe | Propriedade total do Adobe, mas no futuro os clientes poderão configurar determinados parâmetros. |
| Limpeza de binários do Lucene | Adobe | Não usado e, portanto, desabilitado pelo Adobe. |
| Limpeza de tarefa ad-hoc | Cliente | Deve ser feito no github. <br> Substitua o nó de configuração da janela de manutenção pronto para uso em  `/libs` criando propriedades na pasta  `/apps/settings/granite/operations/maintenance/granite_weekly` ou  `granite_daily`. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração. <br> Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o  `granite_TaskPurgeTask`) com as propriedades apropriadas. <br> Para configurar as propriedades do OSGI, consulte a documentação da Tarefa de manutenção  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Remoção do fluxo de trabalho | Cliente | Deve ser feito no github. <br> Substitua o nó de configuração da janela de manutenção pronto para uso em  `/libs` criando propriedades na `/apps/settings/granite/operations/maintenance/granite_weekly` pasta  `granite_daily`. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração. <br> Ative a tarefa de manutenção adicionando outro nó sob o nó acima (nomeie-o  `granite_WorkflowPurgeTask`) com as propriedades apropriadas. <br> Configure as propriedades do OSGI, consulte a documentação da Tarefa de manutenção  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |
| Remoção do projeto | Cliente | Deve ser feito no github. <br> Substitua o nó de configuração da janela de manutenção pronto para uso em  `/libs` criando propriedades na pasta  `/apps/settings/granite/operations/maintenance/granite_weekly` ou  `granite_daily`. Consulte a tabela Janela de manutenção abaixo para obter mais detalhes sobre a configuração. <br> Ative a tarefa de manutenção adicionando um nó sob o nó acima (nomeie-o  `granite_ProjectPurgeTask`) com as propriedades apropriadas. <br> Configurar as propriedades do OSGI consulte a documentação da Tarefa de manutenção  [AEM 6.5](https://helpx.adobe.com/experience-manager/kb/AEM6-Maintenance-Guide.html) |

Os clientes podem agendar cada uma das tarefas de Expurgação de fluxo de trabalho, Expurgação de tarefa ad-hoc e Manutenção de limpeza de projeto para serem executadas durante as janelas de manutenção diária, semanal ou mensal. Essas configurações devem ser editadas diretamente no controle do código-fonte. A tabela abaixo descreve os parâmetros de configuração disponíveis para cada janela.

<table>
  <tr>
    <th>Configuração da Janela de Manutenção</th>
    <th>Quem é o proprietário da configuração</th>
    <th>Tipo de configuração</th>
    <th>Local</th>
    <th>Exemplo</th>
    <th>Parâmetros</th>
  </tr>
  <tr>
    <td>Diariamente</td>
    <td>Cliente</td>
    <td>Definição de Nó JCR</td>
    <td>Veja o local 1 abaixo</td>
    <td>Consulte a amostra de código 1 abaixo</td>
  <td>
  <strong>windowSchedule</strong>  = diariamente (este valor não deve ser alterado) 
  <strong>windowStartTime</strong>  = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Diária devem começar a ser executadas.
  <strong>windowEndTime</strong>  = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Diária devem parar de ser executadas se ainda não tiverem sido concluídas.
  </td> 
  </tr>
  <tr>
    <td>Semanalmente</td>
    <td>Cliente</td>
    <td>Definição de Nó JCR</td>
    <td>Veja o local 2 abaixo</td>
    <td>Consulte a amostra de código 2 abaixo</td>
    <td>
    <strong>windowSchedule</strong>  = weekly (esse valor não deve ser alterado) 
    <strong>windowStartTime</strong>  = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção semanal devem começar a ser executadas.
    <strong>windowEndTime</strong>  = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Semanal devem parar de ser executadas caso ainda não tenham sido concluídas.
    <strong>windowScheduleWeekdays = Matriz de 2 valores de 1 a 7. por exemplo [5,5].</strong> O primeiro valor da matriz é o dia de início em que a tarefa é agendada e o segundo valor é o dia de término em que a tarefa seria interrompida. A hora exata do início e do fim é regida por windowStartTime e windowEndTime, respectivamente.
    </td> 
  </tr>
  <tr>
    <td>Mensalmente</td>
    <td>Cliente</td>
    <td>Definição de Nó JCR</td>
    <td>Veja o local 3 abaixo</td>
    <td>Ver exemplo de código 3 abaixo</td>
    <td>
    <strong>windowSchedule</strong>  = diariamente (este valor não deve ser alterado) 
    <strong>windowStartTime</strong>  = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Mensal devem começar a ser executadas.
    <strong>windowEndTime</strong>  = HH:MM usando como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Mensal devem parar de ser executadas se ainda não tiverem sido concluídas.
    <strong>windowScheduleWeekdays = Matriz de 2 valores de 1 a 7. por exemplo [5,5].</strong> O primeiro valor da matriz é o dia de início em que a tarefa é agendada e o segundo valor é o dia de término em que a tarefa seria interrompida. A hora exata do início e do fim é regida por windowStartTime e windowEndTime, respectivamente.
    <strong>windowFirstLastStartDay - 0/1</strong> 0 para agendar na primeira semana do mês ou 1 para agendar na última semana do mês. A ausência de um valor agendaria efetivamente trabalhos todos os dias, conforme determinado por windowScheduleWeekdays todos os meses.
    </td> 
    </tr>
</table>

Localizações:

1. /apps/settings/granite/operations/maintenance/granite_diariamente
2. /apps/settings/granite/operations/maintenance/granite_weekly
3. /apps/settings/granite/operations/maintenance/granite_mensal

Amostras de código:

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

| Configuração da Janela de Manutenção | Quem é o proprietário da configuração | Tipo de configuração | Local | Exemplo | Parâmetros |
|---|---|---|---|---|---|
| Diariamente | Cliente | Definição de Nó JCR | Veja o local 2 abaixo | Consulte a amostra de código 2 abaixo | **windowSchedule= daily**  (este valor não deve ser alterado).  <br> **windowStartTime= HH:** MMusing como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Diária devem começar a ser executadas. <br> **windowEndTime= HH:** MMusing como relógio de 24 horas. Define quando as Tarefas de Manutenção associadas à Janela de Manutenção Diária devem parar de ser executadas se ainda não tiverem sido concluídas. |
