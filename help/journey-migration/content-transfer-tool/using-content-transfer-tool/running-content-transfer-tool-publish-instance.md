---
title: Execução da ferramenta Transferência de conteúdo em uma instância de publicação
description: Execução da ferramenta Transferência de conteúdo em uma instância de publicação
exl-id: 01faab94-a939-4004-b094-e9eb8f67b96e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 11%

---

# Execução da ferramenta Transferência de conteúdo em uma instância de publicação {#run-content-transfer-tool-publish-instance}

## Introdução {#introduction}

A ferramenta Transferência de conteúdo (CTT) não executa nenhum tipo de análise de conteúdo antes de transferir o conteúdo da instância de origem para a instância de destino. Por exemplo, a CTT não diferencia entre conteúdo publicado e não publicado ao assimilar conteúdo em um ambiente de publicação. Qualquer conteúdo especificado no conjunto de migração é assimilado na instância de destino escolhida. O usuário pode assimilar um conjunto de migração em uma instância de Autor ou instância de Publicação, ou ambos.

>[!NOTE]
>É recomendável que, ao mover o conteúdo para uma instância de Produção, a Ferramenta de transferência de conteúdo seja instalada na instância do Autor de origem para mover o conteúdo para a instância do Autor de destino e, de forma semelhante, instalar a Ferramenta de transferência de conteúdo na instância de Publicação de origem para mover o conteúdo para a instância de Publicação de destino. Consulte [Abordagem recomendada](#recommended-approach) abaixo para obter mais detalhes.

## Abordagem recomendada {#recommended-approach}

Siga a abordagem recomendada conforme descrito abaixo:

* Use a mesma versão da ferramenta Transferência de conteúdo que foi usada na instância do autor.

* Somente um único nó de publicação precisa ser migrado. Ele deve ser removido do balanceador de carga antes do início da extração.

* Durante a assimilação para publicação, o nível de publicação não será reduzido (ao contrário do autor).

  >[!IMPORTANT]
  >Como precaução, evite quaisquer operações de gravação iniciadas pelo usuário, como:
  > * Distribuição de conteúdo do autor do AEM as a Cloud Service para publicação nesse ambiente
  > * Sincronização de usuários entre instâncias de publicação
