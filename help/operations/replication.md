---
title: Replicação
description: Distribuição e Solução de problemas de replicação.
translation-type: tm+mt
source-git-commit: abb45225e880f3d08b9d26c29e243037564acef0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---


# Replicação {#replication}

A Adobe Experience Manager como Cloud Service usa o recurso de Distribuição [de conteúdo](https://sling.apache.org/documentation/bundles/content-distribution.html) Sling para mover o conteúdo para replicar para um serviço de pipeline executado no Adobe I/O que está fora do tempo de execução AEM.

>[!NOTE]
>
>Leia [Distribuição](/help/core-concepts/architecture.md#content-distribution) para obter mais informações.

## Métodos de publicação de conteúdo {#methods-of-publishing-content}

### Desfazer/publicar rapidamente - Desfazer/publicar planejado {#publish-unpublish}

Essas funcionalidades padrão de AEM para os autores não mudam com AEM Cloud Service.

### Tempos ligado e desligado - Configuração do acionador {#on-and-off-times-trigger-configuration}

As possibilidades adicionais de Tempo **ligado** e Tempo **desligado** estão disponíveis na guia [Básico das Propriedades](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)da página.

Para realizar a replicação automática para isso, é necessário ativar a Replicação **** automática na configuração [](/help/implementing/deploying/configuring-osgi.md) OSGi **Configuração** do acionador desligado:

![Configuração do Acionador Desligado do OSGi](/help/operations/assets/replication-on-off-trigger.png)

### Ativação de árvore {#tree-activation}

Para executar uma ativação em árvore:

1. No menu Start AEM, navegue até **Ferramentas > Implantação > Distribuição**
2. Selecione o cartão **forwardPublisher**
3. Uma vez na interface do console da Web do forwardPublisher, **selecione Distribuir**

   ![](assets/distribute.png "DistribuirDistribuir")
4. Selecione o caminho no navegador de caminho, escolha adicionar um nó, árvore ou excluir conforme necessário e selecione **Enviar**

## Resolução de problemas {#troubleshooting}

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
