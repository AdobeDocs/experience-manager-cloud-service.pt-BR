---
title: Atualização dos fragmentos de conteúdo para a filtragem otimizada do GraphQL
description: Saiba como atualizar os fragmentos de conteúdo para uma filtragem otimizada do GraphQL no Adobe Experience Manager as a Cloud Service para entrega de conteúdo headless.
source-git-commit: 44f39df675ff7b3bd40d76e1ebb0e0f17f1e128b
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 6%

---


# Atualização dos fragmentos de conteúdo para uma filtragem otimizada do GraphQL {#updating-content-fragments-for-optimized-graphql-filtering}

Para otimizar o desempenho dos filtros do GraphQL, é necessário executar um procedimento para atualizar os fragmentos de conteúdo.

>[!NOTE]
>
>Depois de atualizar os fragmentos de conteúdo, você pode seguir as recomendações para [Otimização de consultas do GraphQL](/help/headless/graphql-api/graphql-optimization.md).


## Pré-requisitos {#prerequisites}

Verifique se você tem um mínimo da versão 2023.1.0 do AEM as a Cloud Service.

## Atualização dos fragmentos de conteúdo {#updating-content-fragments}

Para executar o procedimento, siga as etapas abaixo:

1. Ative a atualização definindo as seguintes variáveis para sua instância usando a interface do usuário do Cloud Manager:

   ![Configuração do ambiente do Cloud Manager](assets/cfm-graphql-update-01.png "Configuração do ambiente do Cloud Manager")

   As variáveis disponíveis são:

   <table style="table-layout:auto">
    <tbody>
     <tr>
      <th> </th>
      <th>Nome</th>
      <th>Valor</th>
      <th>Valor padrão</th>
      <th>Serviço</th>
      <th>Aplicado</th>
      <th>Tipo</th>
      <th>Notas</th>
     </tr>
     <tr>
      <td>1</td>
      <td>"AEM_RELEASE_CHANNEL" </td>
      <td>"prerelease" </td>
      <td> </td>
      <td>Todos </td>
      <td> </td>
      <td>Variável </td>
      <td>Necessário para habilitar o recurso. </td>
     </tr>
     <tr>
      <td>2</td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variável </td>
      <td>Habilita(!=0) ou desativa(0) o acionamento do trabalho de migração de Fragmento de conteúdo. </td>
     </tr>
     <tr>
      <td>3</td>
      <td>"CF_MIGRATION_ENFORCE" </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variável </td>
      <td>Forçar (!=0) remigração de fragmentos de conteúdo.<br>Definir esse sinalizador como 0 fará uma migração incremental de CFs. Isso significa que, se a tarefa for encerrada por algum motivo, a próxima execução da tarefa iniciará a migração a partir do ponto em que foi encerrada. Observe que, é recomendável aplicar a primeira migração (valor=1). </td>
     </tr>
     <tr>
      <td>4</td>
      <td>"CF_MIGRATION_BATCH" </td>
      <td>`50` </td>
      <td>`50` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variável </td>
      <td>Tamanho do lote para salvar o número de Fragmentos de conteúdo após a migração.<br>Isso é relevante para quantos CFs serão salvos no repositório em um lote e pode ser usado para otimizar o número de gravações no repositório. </td>
     </tr>
     <tr>
      <td>5</td>
      <td>"CF_MIGRATION_LIMIT" </td>
      <td>`1000` </td>
      <td>`1000` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variável </td>
      <td>Número máximo de fragmentos de conteúdo a serem processados de cada vez.<br>Consulte também as notas para "CF_MIGRATION_INTERVAL". </td>
     </tr>
     <tr>
      <td>6</td>
      <td>"CF_MIGRATION_INTERVAL" </td>
      <td>`60` </td>
      <td>`600` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variável </td>
      <td>Intervalo (segundos) para processar os fragmentos de conteúdo restantes até o próximo limite<br>Esse intervalo também é considerado como um tempo de espera antes de iniciar o trabalho, bem como um atraso entre o processamento de cada número de CFs CF_MIGRATION_LIMIT subsequente.<br>(*)</td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >(*)
   >
   >O valor de `CF_MIGRATION_INTERVAL` O também pode ajudar a aproximar o tempo total de execução do trabalho de migração.
   >
   >Por exemplo:
   >
   >* Número total de fragmentos de conteúdo = 20.000
   >* CF_MIGRATION_LIMIT = 1000
   >* CF_MIGRATION_INTERNAL = 60 (Seg)
   >* Tempo aproximado necessário para concluir a migração = 60 + (20.000/1.000 * 60) = 1.260 Seg = 21 Minutos
      >  Os &quot;60&quot; segundos adicionais adicionados no início se devem ao atraso inicial ao iniciar o trabalho.

   >
   >Você também deve estar ciente de que esta é apenas a *mínimo* tempo necessário para concluir o trabalho, e não inclui o tempo de E/S. O tempo efetivamente gasto poderia ser significativamente maior do que esta estimativa.

1. Monitore o progresso e a conclusão da atualização.

   Para fazer isso, monitore os logs no autor e na publicação ouro do:

   * `com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob`

      * Logs do autor; por exemplo:

         ```shell
         23.01.2023 13:13:45.926 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<dd9ffdc1-0c28-4d04-9a96-5d4d223e457e> is the leader, will schedule the upgrade schedule job.
         ...
         23.01.2023 13:13:45.941 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
         
         23.01.2023 13:20:40.960 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 6m, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
         ```
   * Golden-publish logs; por exemplo:

      ```shell
      23.01.2023 12:35:05.150 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<ad1b399e-77be-408e-bc3f-57097498fddb> is the leader, will schedule the upgrade schedule job.
      
      23.01.2023 12:35:05.161 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
      ...
      23.01.2023 12:40:45.180 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 5m, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
      ```


1. Desative o procedimento de atualização.

   >[!IMPORTANT]
   >
   >Esta etapa é necessária para concluir a atualização.

   Depois que o procedimento de atualização for executado, redefina a variável de ambiente de nuvem `CF_MIGRATION_ENABLED` para &#39;0&#39;, para acionar a reciclagem de todos os pods.

   <table style="table-layout:auto">
    <tbody>
     <tr>
      <th> </th>
      <th>Nome</th>
      <th>Valor</th>
      <th>Valor padrão</th>
      <th>Serviço</th>
      <th>Aplicado</th>
      <th>Tipo</th>
      <th>Notas</th>
     </tr>
     <tr>
      <td></td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`0` </td>
      <td>`0` </td>
      <td>Todos </td>
      <td> </td>
      <td>Variável </td>
      <td>Disables(0) (ou Enables(!=0)) acionamento do trabalho de migração de Fragmento de conteúdo. </td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >Isso é particularmente importante para o nível de publicação, pois a atualização de conteúdo é feita apenas na golden-publish e, ao reciclar pods, todos os pods de publicação normais se baseiam na golden-publish.

1. Verifique a conclusão do procedimento de atualização.

   Você pode verificar a conclusão bem-sucedida da atualização usando o navegador do repositório no console do desenvolvedor do Cloud Manager para verificar os dados do fragmento de conteúdo.

   * Antes da primeira migração completa, a variável `cfGlobalVersion` a propriedade não existirá.
Portanto, a presença dessa propriedade no nó JCR `/content/dam` com um valor de `1`, confirma a conclusão da migração.

   * Você também pode verificar as seguintes propriedades nos Fragmentos de conteúdo individuais:

      * `_strucVersion` deve ter o valor de `1`
      * `indexedData` a estrutura deve existir

      >[!NOTE]
      >
      >O procedimento atualizará os Fragmentos de conteúdo nas instâncias de autor e publicação.
      >
      >Portanto, é recomendável executar a verificação via navegador do repositório para *pelo menos* um autor *e* uma instância de publicação.


## Limitações {#limitations}

Esteja ciente das seguintes limitações:

* A otimização do desempenho dos filtros do GraphQL só será possível após uma atualização completa de todos os fragmentos de conteúdo (indicada pela presença da variável `cfGlobalVersion` propriedade para o nó JCR `/content/dam`)

* Se os fragmentos de conteúdo forem importados de um pacote de conteúdo (usando `crx/de`) depois que o procedimento de atualização for executado, esses fragmentos de conteúdo não serão considerados nos resultados da consulta do GraphQL, até que o procedimento de atualização seja executado novamente.