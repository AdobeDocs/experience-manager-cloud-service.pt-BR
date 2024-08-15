---
title: Configuração de endpoint do Dispatcher com AEM Headless
description: O Dispatcher é uma camada de segurança e cache na frente dos ambientes de publicação do Adobe Experience Manager. Várias configurações são usadas para abrir pontos de extremidade GraphQL em aplicativos headless.
feature: Headless, Dispatcher, GraphQL API
exl-id: 78a20021-910f-4cf0-87bf-6e2223994f76
role: Admin, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 85%

---


# Dispatcher - Configuração de endpoint com AEM Headless

O [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR) é uma camada de armazenamento em cache e segurança na frente dos ambientes de publicação do Adobe Experience Manager. Várias configurações são incluídas por padrão para abrir endpoints GraphQL em aplicativos headless.

>[!NOTE]
>
>Para obter a documentação detalhada sobre o Dispatcher, consulte o [Guia do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=pt-BR).

Os projetos do AEM incluem um módulo de Dispatcher que contém as configurações do Dispatcher. Projetos recém-gerados do [arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype) incluem automaticamente [filtros](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#defining-a-filter) que habilitam pontos de acesso GraphQL.

## Pontos de acesso GraphQL

Como parte dos filtros padrão, [endpoints GraphQL](/help/headless/graphql-api/graphql-endpoint.md) são abertos com a seguinte regra:

```
/0060 { /type "allow" /method '(POST|OPTIONS)' /url "/content/_cq_graphql/*/endpoint.json" }
```

O curinga `*` abre vários endpoints na instância do AEM. As consultas que utilizam um ponto de acesso GraphQL são feitas usando `POST`, e a resposta **não** é armazenada em cache.

## Consultas persistentes de GraphQL

A solicitação de consultas persistentes é feita em um ponto de acesso diferente. Como parte da configuração de filtro padrão, o URL das [consultas persistentes](/help/headless/graphql-api/persisted-queries.md) é aberto com a seguinte regra:

```
/0061 { /type "allow" /method '(GET|POST|OPTIONS)' /url "/graphql/execute.json*" }
```

Consultas persistentes podem ser solicitadas usando `GET`, armazenando a resposta em cache no nível do Dispatcher e do CDN. Mais detalhes sobre armazenamento em cache e invalidação de cache podem ser encontrados em [a Introdução ao armazenamento em cache no AEM as a Cloud Service](/help/implementing/dispatcher/caching.md).
