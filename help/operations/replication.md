---
title: Replicação
description: Distribuição e Solução de problemas de replicação.
translation-type: tm+mt
source-git-commit: 8fba31951276d7e0de1f3bd079e42e431edaff4e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---


# Replicação {#replication}

O Adobe Experience Manager como um serviço em nuvem usa o recurso [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) para mover o conteúdo para replicar para um serviço de pipeline executado em E/S da Adobe fora do tempo de execução do AEM.

>[!NOTE]
>
> Leia [Distribuição](/help/core-concepts/architecture.md#content-distribution) para obter mais informações.

## Métodos de publicação de conteúdo {#methods-of-publishing-content}

### Desfazer/publicar rapidamente - Desfazer/publicar planejado {#publish-unpublish}

Essas funcionalidades padrão do AEM para os autores não são alteradas com o serviço da AEM Cloud.

### Ativação de árvore {#tree-activation}

Para executar uma ativação em árvore:

1. No menu Start AEM, navegue até **Ferramentas > Implantação > Distribuição**
2. Selecione o cartão **forwardPublisher**
3. Uma vez na interface do console da Web do forwardPublisher, **selecione Distribuir**

   ![](assets/distribute.png "DistribuirDistribuir")
4. Selecione o caminho no navegador de caminho, escolha adicionar um nó, árvore ou excluir conforme necessário e selecione **Enviar**

## Resolução de Problemas{#troubleshooting}

Para solucionar problemas de replicação, navegue até as Filas de Replicação na interface do usuário da Web do Serviço de Autor de AEM:

1. No menu Start AEM, navegue até **Ferramentas > Implantação > Distribuição**
2. Selecione o cartão **forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. Verifique o status da fila que deve estar verde
4. Você pode testar a conexão com o serviço de replicação
5. Selecione a guia **Logs** que mostra o histórico de publicações de conteúdo

![](assets/logs.png "LogsLogs")

Se o conteúdo não puder ser publicado, toda a publicação será revertida do Serviço de publicação de AEM.
Nesse caso, as filas de espera devem ser revistas a fim de identificar quais os itens que causaram o cancelamento da publicação. Ao clicar em uma fila mostrando um status vermelho, a fila com itens pendentes apareceria, a partir da qual um ou todos os itens podem ser apagados, se necessário.
