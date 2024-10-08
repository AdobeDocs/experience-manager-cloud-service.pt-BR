---
title: Indexação após a migração do conteúdo
description: Saiba como o processo de migração indexará o conteúdo assimilado na instância do Cloud Service de destino.
exl-id: a13d5df4-b351-410a-9336-1b34a8af21b6
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 7%

---

# Indexação após a migração do conteúdo {#Indexing-content}

## Indexação {#aem-indexing-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_indexing"
>title="Indexação de conteúdo"
>abstract="A indexação do AEM refere-se à indexação do conteúdo na instância do Cloud Service após migrar o conteúdo para ele. A indexação é necessária para oferecer suporte à pesquisa de conteúdo nessa instância."

Depois que o Cloud Acceleration Manager concluir a assimilação do conteúdo na instância do Cloud Service, ele estará pronto para ser usado. Inicialmente, o conteúdo não é indexado, o que provavelmente resulta em um ambiente instável, em que podem ser esperados problemas como conteúdo não pesquisável e desempenho degradado. Para obter o desempenho ideal na instância, o processo de migração iniciará automaticamente a indexação do conteúdo. Não há nada a ser feito, exceto para monitorar o progresso da indexação.

> Para obter informações sobre como iniciar uma assimilação, consulte [Assimilar conteúdo no Cloud Service](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md).

As etapas a seguir mostram o fluxo geral que você pode esperar ver na interface do usuário durante a indexação. Alguns rótulos fornecem contexto útil em dicas de ferramentas, portanto, passe o mouse sobre os itens para saber mais sobre o status de indexação atual.

Para começar, acesse o Cloud Acceleration Manager. Clique no cartão do projeto e depois no cartão Transferência de conteúdo. Navegue até **Trabalhos de assimilação** e veja os trabalhos listados.

>[!NOTE]
>Você pode visualizar ou baixar os logs de indexação usando as ações do trabalho de assimilação com a lista suspensa .... Os logs estarão disponíveis no
> Seção de ações &quot;Log de indexação&quot;, após a conclusão do trabalho de indexação

### Pendente

É assim que a linha do trabalho de assimilação aparecerá quando a assimilação estiver em execução, antes que o trabalho de indexação tenha sido iniciado. Nenhuma ação é necessária por parte do usuário. Se a assimilação falhar por qualquer motivo, a fila do trabalho de índice será rescindida e não será iniciada.

![imagem](/help/journey-migration/content-transfer-tool/assets-indexing/pending.png)

### Em execução

Quando a assimilação é bem-sucedida, o trabalho de indexação é iniciado automaticamente. A linha de trabalho de assimilação mostrará um ícone de progresso para o status de indexação do AEM. Você pode abrir a caixa de diálogo de duração para ver o progresso do trabalho.

![imagem](/help/journey-migration/content-transfer-tool/assets-indexing/running.png)

### Concluído

Quando o trabalho de indexação for bem-sucedido, a instância estará pronta para ser usada no desempenho ideal. Nesse ponto, os logs do trabalho de indexação estão disponíveis para visualização ou download para inspecioná-los.

![imagem](/help/journey-migration/content-transfer-tool/assets-indexing/complete.png)

### Erros

A indexação da instância de Cloud Service de destino provavelmente terá êxito. Em alguns casos, pode falhar e a linha do trabalho de assimilação aparecerá da seguinte maneira. Em todos os casos, você pode encontrar alguns detalhes da falha ao passar o cursor do mouse sobre o status da falha, e isso pode fornecer mais informações para ajudá-lo a determinar as próximas etapas. Nesse ponto, os logs do trabalho de indexação estão disponíveis para visualização ou download para ajudar a descobrir a origem da falha. Se a próxima etapa não estiver clara, entre em contato com o Suporte do Adobe com detalhes da assimilação e do log de indexação.

>[!TIP]
>
> Se o trabalho de indexação parecer estar sendo executado por muito tempo, verifique se uma [Inclui na lista de permissões de IP não foi aplicada](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) por meio do Cloud Manager, pois ela impede que o Cloud Acceleration Manager acesse o serviço de migração.

![imagem](/help/journey-migration/content-transfer-tool/assets-indexing/failed.png)

## O que vem a seguir {#whats-next}

Depois que a instância do Cloud Service de destino tiver sido indexada, você poderá visualizar os logs dos trabalhos de indexação e procurar detalhes e erros.

A migração foi concluída. O teste e a validação da instância do Cloud Service de destino podem começar.
