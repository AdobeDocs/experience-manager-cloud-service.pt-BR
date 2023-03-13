---
title: Configuração do Dispatcher com o AEM Headless
description: O Dispatcher é uma camada de segurança e cache na frente dos ambientes de publicação do Adobe Experience Manager. Várias configurações são usadas para abrir pontos de extremidade GraphQL em aplicativos headless.
feature: Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
source-git-commit: 9bfb5bc4b340439fcc34e97f4e87d711805c0d82
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 100%

---

# Configuração do Dispatcher com o AEM Headless

O [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) é uma camada de armazenamento em cache e segurança na frente dos ambientes de publicação do Adobe Experience Manager. Várias configurações são incluídas por padrão para abrir endpoints GraphQL em aplicativos headless.

>[!NOTE]
>
>Para obter a documentação detalhada sobre o Dispatcher, consulte o [Guia do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR)

Como parte de um Projeto do AEM, é incluído um módulo de dispatcher que contém configurações para o dispatcher. Projetos recém-gerados do [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype) incluem automaticamente [filtros](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#defining-a-filter) que ativam endpoints GraphQL.

## Endpoint(s) GraphQL

Como parte dos filtros padrão, [endpoints GraphQL](/help/headless/graphql-api/graphql-endpoint.md) são abertos com a seguinte regra:

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

O curinga `*` abre vários endpoints na instância do AEM. A consulta usando um endpoint GraphQL será feita usando `POST` e a resposta **not** será armazenada em cache.

## Consultas GraphQL Persistidas

A solicitação de consultas persistidas é feita em um endpoint diferente. Como parte da configuração de filtro padrão, o URL de [consultas persistidas](/help/headless/graphql-api/persisted-queries.md) é aberto com a seguinte regra:

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

Consultas persistentes podem ser solicitadas usando `GET`, armazenando a resposta em cache no nível do Dispatcher e do CDN. Mais detalhes sobre armazenamento em cache e invalidação de cache podem ser encontrados [aqui](/help/implementing/dispatcher/caching.md).
