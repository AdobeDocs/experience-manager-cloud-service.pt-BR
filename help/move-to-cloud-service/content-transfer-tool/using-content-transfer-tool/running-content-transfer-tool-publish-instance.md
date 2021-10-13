---
title: Execução da ferramenta Transferência de conteúdo em uma instância de publicação
description: Execução da ferramenta Transferência de conteúdo em uma instância de publicação
source-git-commit: 65847fc03770fe973c3bfee4a515748f7e487ab6
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---


# Execução da ferramenta Transferência de conteúdo em uma instância de publicação {#run-content-transfer-tool-publish-instance}

## Introdução {#introduction}

A Ferramenta de transferência de conteúdo (CTT) não executa nenhum tipo de análise de conteúdo antes de transferir o conteúdo da instância de origem para a instância de destino. Por exemplo, a CTT não diferencia entre conteúdo publicado e não publicado enquanto assimila conteúdo em um ambiente de publicação. Qualquer conteúdo especificado no conjunto de migração será assimilado na instância de destino escolhida. O usuário pode assimilar um conjunto de migração em uma instância de Autor ou de Publicação ou em ambos.

>[!NOTE]
>Recomenda-se que, ao mover o conteúdo para uma instância de Produção, a Ferramenta de Transferência de Conteúdo seja instalada na instância de Autor de origem para mover o conteúdo para a instância de Autor de destino e, de forma semelhante, instale a Ferramenta de Transferência de Conteúdo na instância de Publicação de origem para mover o conteúdo para a instância de Publicação de destino. Consulte a seção [Abordagem recomendada](#recommended-approach) abaixo para obter mais detalhes.

## Abordagem recomendada {#recommended-approach}

Siga a abordagem recomendada conforme descrito abaixo:

* Use a mesma versão da ferramenta Transferência de conteúdo que foi usada na instância do autor.

* Somente um único nó de publicação precisa ser migrado. Ele deve ser removido do balanceador de carga antes de iniciar a extração.

* Ao criar o conjunto de migração, use o URL do autor AEM ambiente as a Cloud Service.

* Durante a assimilação para publicar, o nível de publicação NÃO será dimensionado para baixo (diferente do autor). Como precaução, evite quaisquer operações de gravação iniciadas pelo usuário, como:

   * Distribuição de conteúdo de AEM autor as a Cloud Service para publicar nesse ambiente
   * Sincronização de usuários entre instâncias de publicação
