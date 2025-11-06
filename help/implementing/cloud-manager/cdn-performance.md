---
title: Painel de Desempenho da CDN
description: Entenda como o Cloud Manager avalia o desempenho da rede de entrega de conteúdo (CDN) e o que você pode aprender com o painel.
exl-id: ecd8c1ca-873f-4e73-ad73-b5f7561eb109
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 3%

---

# Painel de desempenho do CDN {#cdn-performance}

Entenda como o Cloud Manager avalia o desempenho da rede de entrega de conteúdo (CDN) e o que você pode aprender com o painel.

## Visão geral {#overview}

Todos os programas do Cloud Manager têm um painel de desempenho CDN. Esse painel apresenta uma pontuação geral para o desempenho da CDN, juntamente com tendências, alertas e sugestões de melhoria, conforme necessário.

![Painel de desempenho da CDN](assets/cdn-performance-dashboard.png)

## Acessar o painel {#accessing}

O painel CDN está disponível na página de visão geral de cada programa.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No console **[Meus Programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, clique no programa cujo painel CDN você deseja exibir.

   ![Página Meus programas](assets/my-programs.png)

1. Na página **Visão geral do programa** do seu programa, role para baixo os cartões **Ambientes** e **Pipelines** para ver o cartão **Desempenho**.

   ![Desempenho](assets/cdn-performance-overview.png)

## Usar o painel {#using}

O painel apresenta uma pontuação geral para o desempenho da CDN, juntamente com tendências, alertas e sugestões de melhoria, conforme necessário.

![Painel de desempenho da CDN](assets/cdn-performance-dashboard.png)

Para obter detalhes sobre o desempenho da CDN e sugestões sobre como melhorá-la, clique em **Exibir tendência**.

![Tendência de desempenho](assets/cdn-performance-trend.png)

Clique em **Exibir** abaixo do gráfico para alterar o período do gráfico.

Para obter sugestões sobre como melhorar o desempenho da CDN, selecione a guia **Recommendations**.

![Recomendações da CDN](assets/cdn-performance-recommendations.png)

Clique na divisa ao lado de qualquer recomendação na lista para exibir detalhes sobre as etapas a serem executadas para melhorar e a causa do problema.

## Definição de ocorrência de cache {#cache-hit}

A taxa de ocorrência do cache mede quantas solicitações de conteúdo um cache pode preencher com êxito em comparação ao número de solicitações que recebe. Quanto maior a taxa de ocorrência do cache, melhor será o desempenho de um CDN.

>[!TIP]
>
>A Adobe recomenda que os usuários almejem uma taxa de acertos de cache de 99%.

```text
Cache Hit Ratio = Cache Hits / (Hits + Misses + Passes + Other)
```

* **Ocorrência** - Os dados são solicitados do cache e foram encontrados.
* **Erro** - Os dados são solicitados do cache e não foram encontrados.
* **Passagem** - Os dados são solicitados do cache e estão configurados para não armazenarem esses dados em cache.
* **Outros** - Todas as solicitações de dados do cache que não correspondem a nenhum outro caso.

As métricas de cache são atualizadas a cada 24 horas.

>[!TIP]
>
>Para obter mais detalhes sobre como o Cloud Manager e a CDN interagem com a Dispatcher, consulte [Armazenamento em cache no AEM as a Cloud Service](/help/implementing/dispatcher/caching.md).
