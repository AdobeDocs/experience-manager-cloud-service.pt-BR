---
title: Configuração do Dispatcher com AEM Headless
description: O Dispatcher é uma camada de segurança e cache na frente dos ambientes de publicação do Adobe Experience Manager. Várias configurações são usadas para abrir pontos de extremidade GraphQL em aplicativos sem periféricos.
feature: Dispatcher, GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 6%

---


# Configuração do Dispatcher com AEM Headless

O [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) é uma camada de armazenamento em cache e segurança na frente dos ambientes do Adobe Experience Manager Publish. Várias configurações são incluídas por padrão para abrir pontos de extremidade GraphQL em aplicativos sem periféricos.

>[!NOTE]
>
>Para obter a documentação detalhada sobre o Dispatcher, consulte o [Guia do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)

Como parte de um Projeto de AEM, é incluído um módulo de dispatcher que contém configurações para o dispatcher. Projetos recém-gerados da [Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype) inclui automaticamente [filtros](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?#defining-a-filter) que ativa pontos de extremidade GraphQL.

## Endpoint(s) GraphQL

Como parte dos filtros padrão, [Pontos de extremidade GraphQL.](/help/headless/graphql-api/graphql-endpoint.md) são abertas com a seguinte regra:

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

O `*` curinga abre vários endpoints na instância de AEM. A consulta usando um ponto de extremidade GraphQL será feita usando `POST` e a resposta **not** ser armazenado em cache.

## Consultas Persistentes GraphQL

A solicitação de consultas persistentes é feita em relação a um endpoint diferente. Como parte da configuração de filtro padrão, o url de [Consultas persistentes](/help/headless/graphql-api/persisted-queries.md) são abertas com a seguinte regra:

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

Consultas persistentes podem ser solicitadas usando `GET`, armazenando a resposta em cache no nível do Dispatcher e CDN. Mais detalhes sobre o armazenamento em cache e a invalidação do cache podem ser encontrados [here](/help/implementing/dispatcher/caching.md).
