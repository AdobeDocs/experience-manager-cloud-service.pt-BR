---
title: Configuração do Dispatcher com o AEM Headless
description: O Dispatcher é uma camada de segurança e cache na frente dos ambientes de publicação do Adobe Experience Manager. Várias configurações são usadas para abrir pontos de extremidade GraphQL em aplicativos headless.
feature: Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 55%

---

# Configuração do Dispatcher com o AEM Headless

O [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) é uma camada de armazenamento em cache e segurança na frente dos ambientes de publicação do Adobe Experience Manager. Várias configurações são incluídas por padrão para abrir endpoints GraphQL em aplicativos headless.

>[!NOTE]
>
>Para obter a documentação detalhada sobre o Dispatcher, consulte o [Guia do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR).

Como parte de um Projeto AEM, é incluído um módulo do Dispatcher que contém configurações para o Dispatcher. Projetos recém-gerados do [Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype) incluir automaticamente [filtros](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#defining-a-filter) que ativam endpoints do GraphQL.

## Endpoints do GraphQL

Como parte dos filtros padrão, [endpoints GraphQL](/help/headless/graphql-api/graphql-endpoint.md) são abertos com a seguinte regra:

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

O curinga `*` abre vários endpoints na instância do AEM. A consulta usando um endpoint do GraphQL é feita usando `POST` e a resposta é **não** em cache.

## Consultas GraphQL Persistidas

A solicitação de consultas persistidas é feita em um endpoint diferente. Como parte da configuração de filtro padrão, o URL de [Consultas persistentes](/help/headless/graphql-api/persisted-queries.md) é aberto com a seguinte regra:

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

Consultas persistentes podem ser solicitadas usando `GET`, armazenando a resposta em cache no nível do Dispatcher e do CDN. Mais detalhes sobre armazenamento em cache e invalidação de cache podem ser encontrados [aqui](/help/implementing/dispatcher/caching.md).
