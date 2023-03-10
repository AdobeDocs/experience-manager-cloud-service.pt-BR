---
title: Visão geral da ferramenta Transferência de conteúdo
description: Visão geral da ferramenta Transferência de conteúdo
exl-id: cfc0366a-2139-4d9d-b5bc-0b65bef4013c
source-git-commit: ac35bbe5ad78e07cc5292e089f3d71c6a8ed6ccc
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 39%

---

# Visão geral {#overview-content-transfer-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_overview"
>title="Visão geral"
>abstract="A ferramenta Transferência de conteúdo é uma ferramenta desenvolvida pelo Adobe que pode ser usada para mover o conteúdo existente de uma instância AEM de origem (no local ou AMS) para a instância AEM Cloud Service de destino. Essa ferramenta também transfere entidades principais (usuários ou grupos) automaticamente."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html" text="Diretrizes e práticas recomendadas"

A ferramenta Transferência de conteúdo é uma ferramenta desenvolvida pela Adobe que pode ser usada para mover o conteúdo existente de uma instância do AEM de origem (no local ou AMS) para a instância de destino do AEM Cloud Service.

Essa ferramenta também transfere entidades principais (usuários ou grupos) automaticamente.

Uma nova versão da ferramenta Transferência de conteúdo está disponível e integra o processo de transferência de conteúdo ao Cloud Acceleration Manager. É altamente recomendável mudar para essa nova versão para aproveitar todos os benefícios que ela oferece:

* Forma de autoatendimento para extrair um conjunto de migração uma vez e assimilá-lo em vários ambientes em paralelo
* Experiência do usuário aprimorada por meio de melhores estados de carregamento, medidas de proteção e tratamento de erros
* Os registros de assimilação são mantidos e estão sempre disponíveis para solução de problemas

Para começar a usar a nova versão, será necessário desinstalar versões mais antigas da ferramenta Transferência de conteúdo, pois houve uma grande mudança de arquitetura na ferramenta.

>[!NOTE]
>
> Para situações em que uma migração já está em andamento, você pode continuar usando a versão anterior da CTT até que a migração seja concluída. Para obter a documentação relacionada à versão anterior da CTT, consulte o [documentação herdada](/help/journey-migration/content-transfer-tool/ctt-legacy/overview-content-transfer-tool-legacy.md).

## Fases na ferramenta Transferência de conteúdo {#phases-content-transfer-tool}

Existem duas fases associadas à transferência de conteúdo:

1. **Extração**: Extração refere-se à extração de conteúdo da instância do AEM de origem em uma área temporária chamada de *conjunto de migração*. Um *conjunto de migração* é uma área de armazenamento em nuvem fornecida pela Adobe para armazenar temporariamente o conteúdo transferido entre a instância do AEM de origem e a instância do AEM Cloud Service.

   Consulte [Processo de extração na transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md) para obter mais detalhes.

   >[!NOTE]
   >O Mapeamento de usuário agora é executado automaticamente como parte da fase de Extração no autor (mas pode, opcionalmente, ser desativado no autor ou ativado na publicação). Consulte [Mapeamento de usuários e migração de entidade de segurança](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) para obter mais detalhes.

1. **Assimilação**: Assimilação refere-se à assimilação de conteúdo do *conjunto de migração* na instância de destino do Cloud Service.

   Consulte [Processo de assimilação na transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) para obter mais detalhes.

## Atributos de um conjunto de migração {#attributes-migration-set}

Um conjunto de migração possui os seguintes atributos:

* Com a nova versão, você pode criar no máximo cinco conjuntos de migração em um projeto criado no Cloud Acceleration Manager.
* Cada conjunto de migração deve ter um nome exclusivo.

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
>Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Na fase de extração, para ***complementar*** um conjunto de migração existente, a opção de *Substituir* deve estar desativada. Consulte [Extração complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process) para obter mais detalhes.

Na fase de assimilação, para aplicar o conteúdo delta sobre o conteúdo atual, a opção de *limpeza* deve estar desativada. Consulte [Assimilação complementar](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process) para obter mais detalhes.

## Expiração do conjunto de migração {#migration-set-expiry}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_migrationset_expiry"
>title="Expiração de um conjunto de migração"
>abstract="Saiba mais sobre a expiração de um conjunto de migração."

Todos os conjuntos de migração expiram após um período prolongado de inatividade de aproximadamente 90 dias. Depois que os indicadores forem exibidos no cartão do projeto e nas linhas da tabela de trabalhos de migração por um período, o conjunto de migração expirará e seus dados não estarão mais disponíveis. O tempo de expiração pode ser facilmente estendido atuando sobre a migração definida por:

* editar sua descrição
* obtendo a chave de extração
* executar uma extração para ele
* executar uma assimilação a partir dele

A expiração de um conjunto de migração pode ser monitorada na linha Conjunto de migração. Um indicador visual útil de que um conjunto de migração está se aproximando da data de expiração também adicionou o cartão do projeto.

![imagem](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam29.png)


## O que vem a seguir {#whats-next}

Depois de saber mais sobre a ferramenta Transferência de conteúdo e a visão geral que a descreve, é possível usá-la para mover o conteúdo existente de uma instância do AEM de origem (no local ou AMS) para a instância do AEM Cloud Service de destino, é necessário revisar [Pré-requisitos para a ferramenta Transferência de conteúdo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md).
