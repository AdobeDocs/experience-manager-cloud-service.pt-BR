---
title: Autenticação para consultas remotas de GraphQL do AEM em fragmentos de conteúdo
description: Entenda a autenticação necessária para consultas remotas de GraphQL do Adobe Experience Manager para proteger sua entrega de conteúdo headless.
feature: Headless, Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
role: Admin, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 96%

---

# Autenticação para consultas remotas de GraphQL do AEM em fragmentos de conteúdo {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Um caso de uso fundamental para a [entrega de fragmentos de conteúdo da API GraphQL do Adobe Experience Manager as a Cloud Service (AEM)](/help/headless/graphql-api/content-fragments.md) é o de aceitar consultas remotas de aplicativos ou serviços de terceiros. Essas consultas remotas podem exigir acesso à API autenticado para garantir a entrega de conteúdo headless.

>[!NOTE]
>
>Para testes e desenvolvimento, também é possível acessar a API GraphQL do AEM diretamente, usando a [interface GraphiQL](/help/headless/graphql-api/graphiql-ide.md).

Para autenticação, o serviço de terceiros precisa [recuperar um token de acesso](#retrieving-access-token), que pode ser [usado na solicitação de GraphQL](#use-access-token-in-graphql-request).

## Recuperação de um token de acesso {#retrieving-access-token}

Consulte[Geração de tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) para obter detalhes completos.

## Uso do token de acesso em uma solicitação de GraphQL {#use-access-token-in-graphql-request}

Para que um serviço de terceiros se conecte a uma instância do AEM, é necessário ter um *token de acesso*. O serviço deve então adicionar esse token ao cabeçalho `Authorization` na solicitação POST.

Por exemplo, um cabeçalho de autorização GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisitos de permissão {#permission-requirements}

Todas as solicitações feitas usando o token de acesso serão realizadas *pela conta de usuário que gerou o token*.

Isso significa que é necessário verificar se a conta tem as permissões necessárias para executar consultas de GraphQL.

É possível verificar essas permissões usando o GraphiQL na instância local. Para obter mais detalhes, consulte [Considerações de permissão para conteúdo headless](/help/headless/security/permissions.md).
