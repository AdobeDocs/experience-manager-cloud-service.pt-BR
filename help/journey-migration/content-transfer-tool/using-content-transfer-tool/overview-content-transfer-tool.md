---
title: Visão geral da ferramenta Transferência de conteúdo
description: Visão geral da ferramenta Transferência de conteúdo
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: 3bf12642e94076a67010e4701715a54138a490ee
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 43%

---

# Visão geral {#overview-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Visão geral"
>abstract="A ferramenta Transferência de conteúdo é uma ferramenta desenvolvida pelo Adobe que pode ser usada para mover o conteúdo existente de uma instância de origem AEM (no local ou AMS) para a instância de destino do AEM Cloud Service. Essa ferramenta também transfere entidades principais (usuários ou grupos) automaticamente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=en" text="Diretrizes e práticas recomendadas"

<!-- Alexandru: Old version of contextual help, keep for failover/debugging
>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Overview"
>abstract="Content Transfer Tool is a tool developed by Adobe that can be used to move existing content over from a source AEM instance (on-premise or AMS) to the target AEM Cloud Service instance. This tool also transfers principals (users or groups) automatically."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#extraction-process" text="Extraction Process"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#ingestion-process" text="Ingestion Process" -->

A ferramenta Transferência de conteúdo é uma ferramenta desenvolvida pela Adobe que pode ser usada para mover o conteúdo existente de uma instância do AEM de origem (no local ou AMS) para a instância de destino do AEM Cloud Service.

Essa ferramenta também transfere entidades principais (usuários ou grupos) automaticamente.

Uma nova versão da ferramenta Transferência de conteúdo está disponível e integra o processo de transferência de conteúdo ao Cloud Acceleration Manager. É altamente recomendável mudar para essa nova versão para aproveitar todos os benefícios que ela oferece:

* Maneira de autoatendimento de extrair um conjunto de migração uma vez e assimilá-lo em vários ambientes em paralelo
* Melhoria na experiência do usuário por meio de melhores estados de carregamento, medidas de proteção e tratamento de erros
* Os logs de assimilação são mantidos e sempre estão disponíveis para solução de problemas

Para começar a usar a nova versão (v2.0.10) <!-- update when version is available --> será necessário desinstalar as versões mais antigas da ferramenta Transferência de conteúdo, pois houve uma mudança importante na arquitetura da ferramenta.

>[!NOTE]
>
> Para situações em que uma migração já está em andamento, você pode continuar usando a versão anterior da CTT até que a migração seja concluída. Para obter a documentação relacionada à versão anterior da CTT, consulte o [documentação herdada](/help/journey-migration/content-transfer-tool/ctt-legacy/overview-content-transfer-tool-legacy.md).

## Fases na ferramenta Transferência de conteúdo {#phases-content-transfer-tool}

Existem duas fases associadas à transferência de conteúdo:

1. **Extração**: Extração refere-se à extração de conteúdo da instância do AEM de origem em uma área temporária chamada de *conjunto de migração*. Um *conjunto de migração* é uma área de armazenamento em nuvem fornecida pela Adobe para armazenar temporariamente o conteúdo transferido entre a instância do AEM de origem e a instância do AEM Cloud Service.

   Consulte [Processo de extração na transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html) para obter mais detalhes.

   >[!NOTE]
   > É recomendável executar a Ferramenta de Mapeamento de Usuário como parte da fase de Extração. Consulte [Usar a ferramenta Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.html) para obter mais detalhes.

1. **Assimilação**: Assimilação refere-se à assimilação de conteúdo do *conjunto de migração* na instância de destino do Cloud Service.

   Consulte [Processo de assimilação na transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html) para obter mais detalhes.

## Atributos de um conjunto de migração {#attributes-migration-set}

Um conjunto de migração possui os seguintes atributos:

* Com a nova versão, você pode criar no máximo cinco conjuntos de migração em um projeto criado no Cloud Acceleration Manager.
* Cada conjunto de migração deve ter um nome exclusivo.

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Na fase de extração, para ***complementar*** um conjunto de migração existente, a opção de *Substituir* deve estar desativada. Consulte [Extração complementar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process) para obter mais detalhes.

Na fase de assimilação, para aplicar o conteúdo delta sobre o conteúdo atual, a opção de *limpeza* deve estar desativada. Consulte [Assimilação complementar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process) para obter mais detalhes.

## O que vem a seguir {#whats-next}

Depois de saber mais sobre a ferramenta Transferência de conteúdo e sua visão geral que descreve essa ferramenta podem ser usadas para mover o conteúdo existente de uma instância de AEM de origem (no local ou AMS) para a instância de destino do AEM Cloud Service, você deve revisar [Pré-requisitos para a ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en).
