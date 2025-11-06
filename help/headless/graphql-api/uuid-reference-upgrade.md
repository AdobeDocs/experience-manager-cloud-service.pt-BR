---
title: Atualizar os fragmentos de conteúdo para referências UUID
description: Saiba como atualizar seus fragmentos de conteúdo para obter referências UUID otimizadas no Adobe Experience Manager as a Cloud Service para entrega de conteúdo headless.
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
exl-id: 004d1340-8e3a-4e9a-82dc-fa013cea45a7
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 2%

---

# Atualizar os fragmentos de conteúdo para referências UUID {#upgrade-content-fragments-for-UUID-references}

Para otimizar a estabilidade dos filtros do GraphQL, você pode atualizar as referências de conteúdo e fragmento nos fragmentos de conteúdo para que elas usem identificadores universalmente exclusivos (UUID).

Originalmente, os Modelos de Fragmento de Conteúdo forneceram os tipos de dados de **Referência de Conteúdo** e **Referência de Fragmento**. Ambas as referências usam um caminho para apontar para o recurso referenciado, e esse caminho pode se tornar desatualizado se o recurso for movido. Embora essas referências sejam mais do que suficientes na maioria dos cenários, os modelos de fragmento de conteúdo foram estendidos para também fornecer referências com base em uma UUID:

* **Referência de conteúdo (UUID)**
* **Referência de fragmento (UUID)**.

Esses novos tipos de referência podem ser usados em novos modelos e fragmentos de fragmento de conteúdo e para estender instâncias existentes.

Para atualizar fragmentos de conteúdo e modelos existentes, você pode executar o procedimento documentado aqui.

>[!CAUTION]
>
>Antes de executar o procedimento de atualização, você deve sempre [Executar uma simulação](#execute-a-dry-run) para realçar possíveis problemas com seu conteúdo.

## O que está atualizado {#what-is-upgraded}

As seguintes atualizações são feitas:

* Campos dos tipos de dados:
   * **Referência de Conteúdo** são convertidas em **Referência de Conteúdo (UUID)**
   * **Referência de fragmento** convertida em **Referência de fragmento (UUID)**
* Os valores das referências baseadas em caminho mantidas nesses campos são substituídos pelas UUIDs correspondentes

>[!NOTE]
>
>Após a atualização, ambos os tipos de dados ainda estarão disponíveis no editor do modelo de fragmento de conteúdo. Você pode criar novos campos com base em ambos os tipos (embora seja previsto que você usará os tipos baseados em UUID) e executar novamente a atualização, se necessário.

## O que NÃO é atualizado {#what-is-not-upgraded}

As seguintes referências não estão atualizadas:

* Referências de página - As UUIDs ainda não são compatíveis
* Qualquer referência inválida; por exemplo, onde o destino do caminho do Fragmento de conteúdo, ou caminho do ativo, não existe

   * Referências inválidas não são atualizadas, como se o caminho do Fragmento de conteúdo, ou o caminho do Ativo, fosse inválido. Não há uma UUID correspondente para atribuir. A referência original permanece intocada.

   * Use uma [simulação](#execute-a-dry-run) para detectar referências inválidas.

  >[!NOTE]
  >
  >Por serem inválidos, eles não podem ser usados, independentemente da atualização.

## Quando não for necessário atualizar {#when-you-should-not-upgrade}

Não atualizar:

* Quando qualquer um dos fragmentos de conteúdo usa referências de página, as referências de página ainda não têm suporte para UUIDs

## Limitações de referências UUID {#limitations-of-uuid-references}

Atualmente, as seguintes limitações se aplicam ao usar referências baseadas em uma UUID:

* Modelos

   * Novos modelos de fragmento de conteúdo com campos UUID de fragmento de conteúdo ou UUID de referência de conteúdo não podem ser criados por meio de OpenAPI.
   * O campo `id` para modelos não foi alterado para ser baseado em UUID. Ele usa o caminho decodificado na base64 do modelo. Os modelos não podem ser movidos, portanto, esse valor ainda é estável.

* Ativos

   * Ao criar um fragmento de conteúdo por meio de OpenAPI, os tipos de campo `fragment-reference` ou `content-reference` devem ser usados para especificar referências a um fragmento ou ativo, respectivamente - mesmo ao definir o valor de um campo de referência baseado em UUID.

## Planejamento de atualização {#upgrade-planning}

Existem algumas etapas de preparação antes de executar sua atualização.

### Executar uma simulação {#execute-a-dry-run}

Recomenda-se que *a cada* vez que atualizar seu conteúdo, você primeiro execute uma simulação. Isso criará arquivos de log com entradas que destacam possíveis problemas:

* Referências inválidas
* Referências de página

Executar a atualização de conteúdo no modo `dryRun` para:

* identificar quaisquer referências inválidas; listando-as nos arquivos de log
Você pode corrigir essas referências antes de executar a atualização de conteúdo real.
* identificar quaisquer referências de página; listando-as nos arquivos de log
Quando forem detectadas referências de página, você [não deverá executar a atualização de conteúdo](#when-you-should-not-upgrade).


### Forçar um congelamento de conteúdo {#enforce-a-content-freeze}

A execução da atualização de conteúdo deve ser planejada durante um período de congelamento de conteúdo.

A duração do congelamento do conteúdo depende do volume dos Fragmentos de conteúdo que estão sendo atualizados. Dessa forma, a atualização pode variar de alguns minutos a algumas horas e também depende dos parâmetros usados ao iniciar a atualização de conteúdo.

## Execução da atualização de conteúdo {#running-the-content-upgrade}

A atualização de conteúdo pode ser gerenciada usando o ponto de extremidade: `/libs/dam/cfm/maintenance.json`

>[!NOTE]
>
>Sua conta precisa da função `Administrator` para acessar o ponto de extremidade.

### Iniciar uma atualização de conteúdo {#start-a-content-upgrade}

| Terminal | tipo de solicitação HTTP | Comentar |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **Solicitar parâmetros** | **Valor** | |
| ação | `start` | |
| serviceTypeId | `uuidUpgradeService` | A ID do tipo de serviço (valor fixo, predefinido). |
|  segmentSize | `1000` | O número de fragmentos de conteúdo ou modelos que serão atualizados em um segmento (lote). |
| basePath | `/conf` | Especifique:<ul><li>a raiz `/conf` para atualizar todas as configurações do AEM</li><li>um caminho de configuração do AEM selecionado. para o qual a atualização de conteúdo é executada<br>Por exemplo: `/conf/wknd-shared` atualiza somente o único locatário `wknd-shared`</li></ul> |
| intervalo | `10` | Intervalo em segundos, após o qual o próximo segmento de fragmentos de conteúdo ou modelos é atualizado. |
| modo | `replicate`, `noReplicate` | <ul><li>`replicate`: replica o mesmo trabalho em todas as instâncias de publicação do AEM</li><li>`noReplicate`: executa o trabalho somente em instâncias do AEM Author</li></ul> |
| dryRun |  `true`, `false` | <ul><li>`false`: simular a atualização de conteúdo, sem salvar as alterações de conteúdo</li><li>`true`: faça a atualização do conteúdo e salve as alterações</li></ul> |
| **Detalhes da resposta** | **Valor** | |
| jobId | `UUID` |  A ID do trabalho que executa a atualização de conteúdo.<ul><li>Essa ID é necessária em todas as chamadas subsequentes relacionadas a essa execução.</li><li>Se o valor `mode` estiver definido como `replicate`, a execução nas instâncias de Publicação do AEM também precisará estar sob o mesmo `jobId`.</li></ul> |
| parâmetros | Os parâmetros de atualização de conteúdo | Isso inclui os parâmetros iniciais fornecidos para iniciar a atualização de conteúdo e alguns padrões internos. |


### Exemplo de solicitação de atualização de conteúdo {#example-content-upgrade-request}

+++Solicitação

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
 
{
    "action": "start",
    "serviceTypeId": "uuidUpgradeService",
    "segmentSize": 1000,
    "basePath": "/conf/wknd-shared",
    "interval": 10,
    "mode": "replicate",
    "dryRun": true
}
```

+++

+++Resposta

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:34:37 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 386
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "basePath": "/conf/wknd-shared",
    "topic": "cfm/maintenance",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  }
}
```

+++

### Obter o status de uma atualização de conteúdo {#get-the-status-of-a-content-upgrade}

| Terminal | tipo de solicitação HTTP | Comentar |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `GET` | |
| **Solicitar parâmetros** | **Valor** | |
| ação | status | |
| jobId | `<UUID>` | O `jobId` retornado da chamada para iniciar a atualização de conteúdo. |
| **Detalhes da resposta** | **Valor** | |
| status | Valores JSON | Contém o status detalhado da atualização de conteúdo:<ul><li>Atualizado após cada intervalo (segundos).</li><li>A execução de `uuidUpgradeService` tem duas fases:<ol><li>fase 0 para atualizar modelos de fragmento de conteúdo</li><li>fase 1 para atualizar fragmentos de conteúdo</li></ol></li><li>Em cada fase, as estatísticas são atualizadas após cada intervalo.</li><li>&quot;jobStatus&quot;: &quot;COMPLETED&quot; marca a atualização como concluída com êxito.</li><li>Outros valores de status são autoexplicativos.</li></ul> |

### Exemplo de solicitação de status de atualização de conteúdo {#example-content-upgrade-status-request}

+++Solicitação

```http
GET http://localhost:4502/libs/dam/cfm/maintenance.json?action=status&jobId=91af43a6-63ff-45e5-ac7b-06ccf565bdfa
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
```

+++

+++Resposta

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:35:51 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 1116
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "eventProcessed": 1,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "confPath": "/conf/wknd-shared",
    "topic": "cfm/uuid-migration",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  },
  "status": {
    "jobStatus": "COMPLETED",
    "lastModified": 1729089310301,
    "currentPhaseIndex": 1,
    "phases": {
      "phase-0": {
        "bookmark": 1727183332520,
        "stats": {
          "successCount": 2,
          "skippedCount": 1,
          "errorCount": 0
        },
        "name": "modelUpgrade",
        "lastModified": 1729089290040,
        "isCompleted": true
      },
      "phase-1": {
        "bookmark": 1727183347990,
        "stats": {
          "successCount": 29,
          "skippedCount": 0,
          "errorCount": 1
        },
        "name": "cfUpgrade",
        "lastModified": 1729089310298,
        "isCompleted": true
      }
    }
  }
}
```

+++

+++Arquivos de log de exemplo

Além do status de uma atualização de conteúdo em execução obtida do endpoint HTTP, os logs do AEM fornecem informações detalhadas sobre o progresso no nível de conteúdo. Por exemplo:

```xml
#Successful model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/article , status: SUCCESS, skips: [], errors: []
 
#Successful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/san-diego-surf-spots/san-diego-surfspots , status: SUCCESS, skips: [], errors: []
 
#Unsuccessful/Skipped model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/adventure , status: SKIPPED, skips: [Model: '/conf/wknd-shared/settings/dam/cfm/models/adventure', no upgradeable fields found], errors: []
 
#Unsuccessful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van , status: FAILED, skips: [], errors: [Path '/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van', Variation: 'master' Field 'featuredImage', Value '/content/dam/wknd-shared/en/magazine/western-australia/adobestock_156407519.jpeg' is invalid; will not upgrade this field.] 
```

Além disso, após o processamento de cada segmento (lote) de fragmentos e modelos de conteúdo, um status acumulado é registrado, resumindo o progresso até o momento. Por exemplo:

```xml
com.adobe.cq.dam.cfm.impl.servicing.PhaseChainProcessor Phase phase-x, processed a segment, stats: {successCount=29, skippedCount=0, errorCount=1}
```

+++

### Anular uma atualização de conteúdo {#abort-a-content-upgrade}

>[!CAUTION]
>
>Anular uma atualização de conteúdo (que não é uma simulação):
>
>* não reverte as alterações já feitas
>* pode deixar o conteúdo em um estado misto
>
>Use essa ação com cuidado.

| Terminal | tipo de solicitação HTTP | Comentar |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **Solicitar parâmetros** | **Valor** | |
| ação | abort | |
| jobId | `<UUID>` | O `jobId` retornado da chamada para iniciar a atualização de conteúdo. |
| **Detalhes da resposta** | **Valor** | |
| status | Valores JSON | Contém o status detalhado da atualização de conteúdo:<ul><li>O status a ser observado é &quot;jobStatus&quot;: &quot;ABORTED&quot;.<br>Após uma ação de anulação, os segmentos de dados pendentes não serão processados.</li><li>Se o jobStatus for &quot;CONCLUÍDO&quot; antes de um abort, a chamada não terá efeito.</li></ul> |

### Exemplo Anular uma solicitação de atualização de conteúdo {#example-abort-content-upgrade-request}

+++Solicitação

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: Basic YWRtaW46YWRtaW4=
Accept: application/json
 
{
    "action": "abort",
    "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807"
    "mode": "replicate",
}
```

+++

+++Resposta

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:39:03 GMT
 
{
  "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807",
   ...
  "eventProcessed": 2,
  "parameters": {
    ...
    "abort": true,
    ...
  },
  "status": {
     "jobStatus": "ABORTED",
    ...
  }
}
```

+++
