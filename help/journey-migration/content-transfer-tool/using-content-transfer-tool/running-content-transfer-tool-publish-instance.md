---
title: Execução da ferramenta Transferência de conteúdo em uma instância de publicação
description: Execução da ferramenta Transferência de conteúdo em uma instância de publicação
source-git-commit: a1c57a9d8165c9e67ce270a3f0c2ad80c75b7196
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---


# Execução da ferramenta Transferência de conteúdo em uma instância de publicação {#run-content-transfer-tool-publish-instance}

## Introdução {#introduction}

A Ferramenta de transferência de conteúdo (CTT) não executa nenhum tipo de análise de conteúdo antes de transferir o conteúdo da instância de origem para a instância de destino. For example, CTT does not differentiate between published and unpublished content while ingesting content into a Publish environment. Whatever content is specified in the migration set will be ingested into the chosen target instance. O usuário pode assimilar um conjunto de migração em uma instância de Autor ou de Publicação ou em ambos.

>[!NOTE]
>Recomenda-se que, ao mover o conteúdo para uma instância de Produção, a Ferramenta de Transferência de Conteúdo seja instalada na instância de Autor de origem para mover o conteúdo para a instância de Autor de destino e, de forma semelhante, instale a Ferramenta de Transferência de Conteúdo na instância de Publicação de origem para mover o conteúdo para a instância de Publicação de destino. Consulte [Abordagem recomendada](#recommended-approach) para obter mais detalhes.

## Abordagem recomendada {#recommended-approach}

Siga a abordagem recomendada conforme descrito abaixo:

* Use a mesma versão da ferramenta Transferência de conteúdo que foi usada na instância do autor.

* Somente um único nó de publicação precisa ser migrado. It should be removed from the load balancer prior to beginning the extraction.

* Ao criar o conjunto de migração, use o URL do autor AEM ambiente as a Cloud Service.

* Durante a assimilação para publicar, o nível de publicação não será reduzido (diferente do autor).

   >[!IMPORTANT]
   >As a precaution, please avoid any user initiated write operations, such as:
   > * Distribuição de conteúdo de AEM autor as a Cloud Service para publicar nesse ambiente
   > * Sincronização de usuários entre instâncias de publicação

