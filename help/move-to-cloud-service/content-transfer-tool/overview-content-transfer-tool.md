---
title: Visão geral da ferramenta de transferência de conteúdo
description: Visão geral da ferramenta de transferência de conteúdo
translation-type: tm+mt
source-git-commit: 1ca9b2091befbafad0878d83fc7963c779146b2a
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---


# Visão geral {#overview-content-transfer-tool}

A Ferramenta de transferência de conteúdo é uma ferramenta desenvolvida pela Adobe que pode ser usada para mover o conteúdo existente de uma instância de AEM de origem (local ou AMS) para a instância de serviço da AEM Cloud do público alvo.

Essa ferramenta também transfere principais (usuários ou grupos) automaticamente.

Há duas fases associadas à transferência de conteúdo:

1. **Extração**:  A Extração refere-se à extração de conteúdo da instância do AEM de origem para uma área temporária chamada conjunto *de* migração. Um conjunto *de* migração é uma área de armazenamento em nuvem fornecida pela Adobe para armazenar temporariamente o conteúdo transferido entre a instância de AEM de origem e a instância de AEM do serviço em nuvem.

   Consulte Processo de [Extração na Transferência](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process) de conteúdo para obter mais detalhes.

2. **Ingestão**: A ingestão refere-se à assimilação de conteúdo do conjunto *de* migração para a instância do Serviço da público alvo Cloud.

   Consulte Processo de [ingestão na Transferência](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process) de conteúdo para obter mais detalhes.

Um conjunto *de* migração tem os seguintes atributos:

* Um máximo de quatro conjuntos de migração podem ser criados e mantidos por vez durante a atividade de transferência de conteúdo.
* Cada conjunto de migração deve ter um nome exclusivo.
* Se um conjunto de migração estiver inativo por mais de 30 dias, ele será automaticamente excluído.
* Sempre que você cria um conjunto de migração, ele é associado a um ambiente específico. Você só pode assimilar uma instância de autor ou publicação do mesmo ambiente.

A Ferramenta de transferência de conteúdo tem um recurso que oferece suporte ao conteúdo diferencial de complementos, onde é possível transferir somente as alterações feitas desde a atividade de transferência de conteúdo anterior.

>[!NOTE]
> Após a transferência inicial de conteúdo, é recomendável fazer atualizações frequentes de conteúdo diferencial para reduzir o período de congelamento de conteúdo para a transferência final de conteúdo diferencial antes de entrar em funcionamento no Cloud Service.

Na fase de extração, para ***cima*** de um conjunto de migração existente, a opção de *substituição* deve estar desativada. Consulte a Extração [Superior](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process) para obter mais detalhes.

Na fase de ingestão, para aplicar o conteúdo delta na parte superior do conteúdo atual, a opção de *limpeza* deve estar desativada. Consulte a [Ingestão](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process) acima para obter mais detalhes.


## Diretrizes e práticas recomendadas {#best-practices}

Siga a seção abaixo para entender as diretrizes e as práticas recomendadas para usar a Ferramenta de transferência de conteúdo:

* É aconselhável executar verificações de compactação e consistência do armazenamento de dados nos repositórios antes de detectar possíveis problemas e também reduzir o lixo presente no repositório.

* Se a configuração da Rede de Delivery de conteúdo do autor da AEM Cloud (CDN) estiver configurada para ter uma lista de permissões de IPs, verifique se os IPs de ambiente de origem também são adicionados à lista de permissões para que o ambiente de origem e o ambiente da AEM Cloud possam se comunicar entre si.

* Na fase de ingestão, é recomendável executar a ingestão usando o modo de *limpeza* ativado, no qual o repositório existente (autor ou publicação) no ambiente de serviço da AEM Cloud do público alvo será completamente excluído e atualizado com os dados do conjunto de migração. Esse modo é muito mais rápido do que o modo sem limpeza, onde o conjunto de migração é aplicado sobre o conteúdo atual.

* Depois que a atividade de transferência de conteúdo é concluída, a estrutura correta do projeto é necessária no ambiente do serviço em nuvem para garantir que o conteúdo seja renderizado com êxito no ambiente do serviço em nuvem.

* Antes de executar a Ferramenta de transferência de conteúdo, verifique se há espaço em disco suficiente no `crx-quickstart` subdiretório da instância de origem do AEM. Isso ocorre porque a Ferramenta de transferência de conteúdo cria uma cópia local do repositório que é carregada posteriormente no conjunto de migração.
A fórmula geral para calcular o espaço livre em disco necessário é a seguinte:
   `data store size + node store size * 1.5`

   * *tamanho* do armazenamento de dados: a Ferramenta de transferência de conteúdo usa 64 GB, mesmo se o armazenamento de dados real for maior.
   * *tamanho*do armazenamento de nó: tamanho do diretório do repositório de segmentos ou tamanho do banco de dados MongoDB.
Assim, para um tamanho de armazenamento de segmento de 20 GB, o espaço livre em disco necessário seria de 94 GB.