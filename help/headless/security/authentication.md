---
title: Autenticação para consultas remotas de GraphQL do AEM em fragmentos de conteúdo
description: Entenda a autenticação necessária para consultas GraphQL de AEM Remotas para proteger sua entrega de conteúdo sem periféricos.
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: 4e37db128aa31d6e8e950be0d077eae921a27468
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 7%

---

# Autenticação para consultas remotas de GraphQL do AEM em fragmentos de conteúdo {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Um caso de uso principal para A [API GraphQL da Adobe Experience Manager as a Cloud Service (AEM) para entrega de fragmento de conteúdo](/help/headless/graphql-api/content-fragments.md) O é aceitar consultas remotas de aplicativos ou serviços de terceiros. Essas consultas remotas podem exigir acesso à API autenticada para proteger a entrega de conteúdo sem cabeçalho.

>[!NOTE]
>
>Para testes e desenvolvimento, você também pode acessar a API GraphQL da AEM diretamente usando o [Interface GraphiQL](/help/headless/graphql-api/graphiql-ide.md) interface.

Para autenticação, o serviço de terceiros precisa [recuperar um token de acesso](#retrieving-access-token), que pode ser [usada na solicitação GraphQL](#use-access-token-in-graphql-request).

## Recuperar um token de acesso {#retrieving-access-token}

Consulte [Gerar tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) para obter detalhes completos.

## Uso do token de acesso em uma solicitação GraphQL {#use-access-token-in-graphql-request}

Para que um serviço de terceiros se conecte a uma instância de AEM, é necessário ter um *Token de acesso*. O serviço deve então adicionar esse token ao `Authorization` na solicitação POST.

Por exemplo, um cabeçalho de autorização GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisitos de permissão {#permission-requirements}

Todas as solicitações feitas usando o token de acesso serão realmente feitas *pela conta de usuário que gerou o token*.

Isso significa que é necessário verificar se a conta tem as permissões necessárias para executar consultas GraphQL.

Você pode verificar isso usando GraphiQL na instância local. Mais detalhes sobre [permissões podem ser encontradas aqui](/help/headless/security/permissions.md).
