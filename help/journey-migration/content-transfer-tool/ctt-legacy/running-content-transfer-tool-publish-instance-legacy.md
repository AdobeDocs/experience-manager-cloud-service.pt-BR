---
title: Execução da ferramenta Transferência de conteúdo em uma instância de publicação (herdada)
description: Execução da ferramenta Transferência de conteúdo em uma instância de publicação
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 4%

---

# Execução da ferramenta Transferência de conteúdo em uma instância de publicação (herdada) {#run-content-transfer-tool-publish-instance}

## Introdução {#introduction}

A Ferramenta de transferência de conteúdo (CTT) não executa nenhum tipo de análise de conteúdo antes de transferir o conteúdo da instância de origem para a instância de destino. Por exemplo, a CTT não diferencia entre conteúdo publicado e não publicado enquanto assimila conteúdo em um ambiente de publicação. Qualquer conteúdo especificado no conjunto de migração será assimilado na instância de destino escolhida. O usuário pode assimilar um conjunto de migração em uma instância de Autor ou de Publicação ou em ambos.

>[!NOTE]
>Recomenda-se que, ao mover o conteúdo para uma instância de Produção, a Ferramenta de Transferência de Conteúdo seja instalada na instância de Autor de origem para mover o conteúdo para a instância de Autor de destino e, de forma semelhante, instale a Ferramenta de Transferência de Conteúdo na instância de Publicação de origem para mover o conteúdo para a instância de Publicação de destino. Consulte [Abordagem recomendada](#recommended-approach) para obter mais detalhes.

## Abordagem recomendada {#recommended-approach}

Siga a abordagem recomendada conforme descrito abaixo:

* Use a mesma versão da ferramenta Transferência de conteúdo que foi usada na instância do autor.

* Somente um único nó de publicação precisa ser migrado. Ele deve ser removido do balanceador de carga antes de iniciar a extração.

* Ao criar o conjunto de migração, use o URL do autor AEM ambiente as a Cloud Service.

* Durante a assimilação para publicar, o nível de publicação não será reduzido (diferente do autor).

   >[!IMPORTANT]
   >Como precaução, evite quaisquer operações de gravação iniciadas pelo usuário, como:
   > * Distribuição de conteúdo de AEM autor as a Cloud Service para publicar nesse ambiente
   > * Sincronização de usuários entre instâncias de publicação

