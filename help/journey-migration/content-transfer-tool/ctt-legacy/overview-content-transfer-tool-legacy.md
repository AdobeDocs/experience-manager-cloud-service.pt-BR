---
title: Visão geral da ferramenta Transferência de conteúdo (Legada)
description: Visão geral da ferramenta Transferência de conteúdo
hide: true
hidefromtoc: true
exl-id: dd031580-e9d7-461e-8689-9bc3dbb2121b
source-git-commit: 3c8035e4db5729f58bae29136a32a0b9944d6a2f
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 70%

---

# Visão geral da ferramenta Transferência de conteúdo (Legada) {#overview-content-transfer-tool}

A ferramenta Transferência de conteúdo é uma ferramenta desenvolvida pela Adobe que pode ser usada para mover o conteúdo existente de uma instância do AEM de origem (no local ou AMS) para a instância de destino do AEM Cloud Service.

Essa ferramenta também transfere entidades principais (usuários ou grupos) automaticamente.

## Fases na ferramenta Transferência de conteúdo {#phases-content-transfer-tool}

Existem duas fases associadas à transferência de conteúdo:

1. **Extração**: Extração refere-se à extração de conteúdo da instância do AEM de origem em uma área temporária chamada de *conjunto de migração*. Um *conjunto de migração* é uma área de armazenamento em nuvem fornecida pela Adobe para armazenar temporariamente o conteúdo transferido entre a instância do AEM de origem e a instância do AEM Cloud Service.

   Consulte [Processo de extração na transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html) para obter mais detalhes.

   >[!NOTE]
   >Execute a Ferramenta de mapeamento de usuário como parte da fase de Extração. Consulte [Usar a ferramenta de Mapeamento de usuários](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html?lang=en) para obter mais detalhes.

1. **Assimilação**: refere-se à assimilação de conteúdo do *conjunto de migração* na instância de destino do Cloud Service.

   Consulte [Processo de assimilação na transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html) para obter mais detalhes.

## Atributos de um conjunto de migração {#attributes-migration-set}

Um conjunto de migração possui os seguintes atributos:

* Um máximo de dez conjuntos de migração podem ser criados e mantidos por vez durante a atividade de transferência de conteúdo.
* Cada conjunto de migração deve ter um nome exclusivo.
* Se um conjunto de migração estiver inativo por mais de 30 dias, ele será excluído automaticamente.
* Sempre que você cria um conjunto de migração, ele é associado a um ambiente específico. Você só pode assimilar em um autor ou uma instância de publicação do mesmo ambiente.


A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Na fase de extração, para ***complementar*** um conjunto de migração existente, a variável *substituir* deve estar desabilitada. Consulte [Extração complementar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html?lang=en#top-up-extraction-process) para obter mais detalhes.

Na fase de assimilação, para aplicar o conteúdo delta sobre o conteúdo atual, a opção de *limpeza* deve estar desativada. Consulte [Assimilação complementar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en#top-up-ingestion-process) para obter mais detalhes.

## O que vem a seguir {#whats-next}

Depois de aprender sobre a ferramenta Transferência de conteúdo e sua visão geral, essa ferramenta pode ser usada para mover o conteúdo existente de uma instância do AEM de origem (no local ou AMS) para a instância do AEM Cloud Service de destino. Revisão [Pré-requisitos para a ferramenta Transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en).
