---
title: Visão geral da ferramenta Transferência de conteúdo
description: Visão geral da ferramenta Transferência de conteúdo
translation-type: tm+mt
source-git-commit: 7648adc4b1d9c5849363beb4162de2f42eac7cfd
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 69%

---


# Visão geral {#overview-content-transfer-tool}

A ferramenta Transferência de conteúdo é uma ferramenta desenvolvida pela Adobe que pode ser usada para mover o conteúdo existente de uma instância do AEM de origem (no local ou AMS) para a instância de destino do AEM Cloud Service.

Essa ferramenta também transfere entidades principais (usuários ou grupos) automaticamente.

Existem duas fases associadas à transferência de conteúdo:

1. **Extração**: Extração refere-se à extração de conteúdo da instância do AEM de origem em uma área temporária chamada de *conjunto de migração*. Um *conjunto de migração* é uma área de armazenamento em nuvem fornecida pela Adobe para armazenar temporariamente o conteúdo transferido entre a instância do AEM de origem e a instância do AEM Cloud Service.

   Consulte [Processo de extração na transferência de conteúdo](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process) para obter mais detalhes.

2. **Assimilação**: Assimilação refere-se à assimilação de conteúdo do *conjunto de migração* na instância de destino do Cloud Service.

   Consulte [Processo de assimilação na transferência de conteúdo](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process) para obter mais detalhes.

Um *conjunto de migração* possui os seguintes atributos:

* No máximo quatro conjuntos de migração podem ser criados e mantidos por vez durante a atividade de transferência de conteúdo.
* Cada conjunto de migração deve ter um nome exclusivo.
* Se um conjunto de migração estiver inativo por mais de 30 dias, ele será excluído automaticamente.
* Sempre que você cria um conjunto de migração, ele é associado a um ambiente específico. Você só pode assimilar em um autor ou uma instância de publicação do mesmo ambiente.

A ferramenta Transferência de conteúdo tem um recurso que oferece suporte a atualizações complementares de conteúdo diferencial, com o qual é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
> Após a transferência inicial do conteúdo, é recomendável fazer atualizações complementares frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar online no Cloud Service.

Na fase de extração, para ***complementar*** um conjunto de migração existente, a opção de *Substituir* deve estar desativada. Consulte [Extração complementar](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process) para obter mais detalhes.

Na fase de assimilação, para aplicar o conteúdo delta sobre o conteúdo atual, a opção de *limpeza* deve estar desativada. Consulte [Assimilação complementar](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process) para obter mais detalhes.


## Diretrizes e práticas recomendadas{#best-practices}

Siga a seção abaixo para entender as diretrizes e práticas recomendadas de uso da ferramenta Transferência de conteúdo:

* É aconselhável executar a Limpeza [de](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/revision-cleanup.html) revisão e as verificações [de consistência do armazenamento](https://helpx.adobe.com/experience-manager/kb/How-to-run-a-datastore-consistency-check-via-oak-run-AEM.html) de dados no repositório de **origem** para identificar possíveis problemas e reduzir o tamanho do repositório.

* Se a configuração da Rede do Delivery de conteúdo do autor da AEM Cloud (CDN) estiver configurada para ter uma lista de permissões de IPs, verifique se os IPs do ambiente de origem também são adicionados à lista de permissões para que o ambiente de origem e o ambiente da AEM Cloud possam se comunicar entre si.

* Na fase de assimilação, é recomendável executar a assimilação usando o modo de *limpeza* ativado, no qual o repositório existente (autor ou publicação) no ambiente de serviço do AEM Cloud Service será completamente excluído e depois atualizado com os dados do conjunto de migração. Esse modo é muito mais rápido que o modo sem limpeza, no qual o conjunto de migração é aplicado sobre o conteúdo atual.

* Após a conclusão da atividade de transferência de conteúdo, a estrutura correta do projeto é necessária no ambiente do Cloud Service para garantir que o conteúdo seja renderizado com êxito no ambiente do Cloud Service.

* Antes de executar a Ferramenta de transferência de conteúdo, verifique se há espaço em disco suficiente no `crx-quickstart` subdiretório da instância de origem do AEM. Isso ocorre porque a Ferramenta de transferência de conteúdo cria uma cópia local do repositório que é carregada posteriormente no conjunto de migração.
A fórmula geral para calcular o espaço livre em disco necessário é a seguinte:
   `data store size + node store size * 1.5`

   * *tamanho* do armazenamento de dados: a Ferramenta de transferência de conteúdo usa 64 GB, mesmo se o armazenamento de dados real for maior.
   * *tamanho*do armazenamento de nó: tamanho do diretório do repositório de segmentos ou tamanho do banco de dados MongoDB.
Assim, para um tamanho de armazenamento de segmento de 20 GB, o espaço livre em disco necessário seria de 94 GB.