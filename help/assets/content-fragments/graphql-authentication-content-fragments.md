---
title: Autenticação para consultas GraphQL de AEM Remotas em Fragmentos de Conteúdo
description: Entenda a autenticação necessária para consultas GraphQL de AEM Remotas para proteger sua entrega de conteúdo sem periféricos.
feature: Fragmentos de conteúdo, API GraphQL
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Autenticação para consultas GraphQL de AEM Remotas em Fragmentos de Conteúdo {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Um caso de uso principal para A API GraphQL do [Adobe Experience Manager as a Cloud Service (AEM) para entrega de fragmento de conteúdo](/help/assets/content-fragments/graphql-api-content-fragments.md) é aceitar consultas remotas de aplicativos ou serviços de terceiros. Essas consultas remotas podem exigir acesso à API autenticada para proteger a entrega de conteúdo sem cabeçalho.

>[!NOTE]
>
>Para testes e desenvolvimento, você também pode acessar a API GraphQL AEM diretamente usando a interface [GraphiQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface).

Para autenticação, o serviço de terceiros precisa usar um [Token de acesso](#access-token), que pode ser [usado na Solicitação GraphQL](#use-access-token-in-graphql-request).

## Recuperar um token de acesso {#retrieving-access-token}

Consulte [Gerando tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) para obter detalhes completos.

## Usar o token de acesso em uma solicitação GraphQL {#use-access-token-in-graphql-request}

Para que um serviço de terceiros se conecte a uma instância de AEM, ele precisa ter um *Token de acesso*. O serviço deve então adicionar esse token ao cabeçalho `Authorization` na solicitação do POST.

Por exemplo, um cabeçalho de autorização GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisitos de permissão {#permission-requirements}

Todas as solicitações feitas usando o token de acesso serão feitas *pela conta de usuário que gerou o token*.

Isso significa que é necessário verificar se a conta tem as permissões necessárias para executar consultas GraphQL.

Você pode verificar isso usando GraphiQL na instância local.
