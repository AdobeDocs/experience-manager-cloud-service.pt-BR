---
title: Painel de Desempenho da CDN
description: Entenda como o Cloud Manager avalia o desempenho da rede de entrega de conteúdo (CDN) e o que você pode aprender com o painel.
source-git-commit: 0d60c19638707262dab7f290f84fa873b694bc22
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---


# Painel de Desempenho da CDN {#cdn-performance}

Entenda como o Cloud Manager avalia o desempenho da rede de entrega de conteúdo (CDN) e o que você pode aprender com o painel.

## Visão geral {#overview}

Todos os programas do Cloud Manager têm um painel de desempenho do CDN. Esse painel apresenta uma pontuação geral para o desempenho da CDN, juntamente com tendências, alertas e sugestões de melhoria, conforme necessário.

![Painel de desempenho do CDN](assets/cdn-performance-dashboard.png)

## Acessar o painel {#accessing}

O painel CDN está disponível na página de visão geral de cada programa.

1. Faça logon no Cloud Manager, em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/), e selecione a organização apropriada.

1. No **[Meus programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** toque ou clique no programa cujo painel CDN você deseja exibir.

   ![Página Meus programas](assets/my-programs.png)

1. No **Visão geral do programa** do seu programa, role para baixo abaixo da **Ambientes** e **Pipelines** cartões para ver o **Desempenho** cartão.

   ![Desempenho](assets/cdn-performance-overview.png)

## Usar o painel {#using}

O painel apresenta uma pontuação geral para o desempenho da CDN, juntamente com tendências, alertas e sugestões de melhoria, conforme necessário.

![Painel de desempenho do CDN](assets/cdn-performance-dashboard.png)

Para obter detalhes sobre o desempenho da CDN e sugestões sobre como melhorá-la, toque ou clique **Exibir tendência**.

![Tendência de desempenho](assets/cdn-performance-trend.png)

Toque ou clique **Exibir** abaixo do gráfico para alterar o intervalo de tempo do gráfico.

Para obter sugestões sobre como melhorar o desempenho do CDN, selecione o **Recommendations** guia.

![Recomendações da CDN](assets/cdn-performance-recommendations.png)

Toque ou clique na divisa ao lado de qualquer recomendação na lista para exibir detalhes sobre as etapas a serem executadas para melhorar e a causa do problema.

## Definição de Acertos do Cache {#cache-hit}

A taxa de ocorrência do cache mede quantas solicitações de conteúdo um cache pode preencher com êxito em comparação ao número de solicitações que recebe. Quanto maior a taxa de ocorrência do cache, melhor será o desempenho de um CDN.

>[!TIP]
>
>A Adobe recomenda que os usuários almejem uma taxa de acertos de cache de 99%.

```text
Cache Hit Ratio = Cache Hits / (Hits + Misses + Passes + Other)
```

* **Hit** - Os dados são solicitados do cache e são encontrados.
* **Srta.** - Os dados são solicitados do cache e não são encontrados.
* **Aprovado** - Os dados são solicitados do cache e estão configurados para não armazená-los em cache.
* **Outro** - Todas as solicitações de dados do cache que não correspondam a nenhum outro caso.

As métricas de cache são atualizadas a cada 24 horas.

>[!TIP]
>
>Para obter mais detalhes sobre como o Cloud Manager e o CDN interagem com o Dispatcher, consulte o documento [Armazenamento em cache no AEM as a Cloud Service.](/help/implementing/dispatcher/caching.md)
