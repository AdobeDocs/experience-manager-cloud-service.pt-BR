---
title: Autenticação para consultas remotas de GraphQL do AEM em fragmentos de conteúdo
description: Entenda a autenticação necessária para consultas do Adobe Experience Manager GraphQL remoto para proteger sua entrega de conteúdo headless.
feature: Content Fragments,GraphQL API
exl-id: dfeae661-06a1-4001-af24-b52ae12d625f
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 26%

---

# Autenticação para consultas remotas de GraphQL do AEM em fragmentos de conteúdo {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Um caso de uso principal para o [API do GraphQL do Adobe Experience Manager as a Cloud Service (AEM) para entrega de fragmentos de conteúdo](/help/headless/graphql-api/content-fragments.md) é aceitar consultas remotas de aplicativos ou serviços de terceiros. Essas consultas remotas podem exigir acesso à API autenticada para garantir a entrega de conteúdo headless.

>[!NOTE]
>
>Para testes e desenvolvimento, também é possível acessar a API GraphQL do AEM diretamente usando o [Interface GraphiQL](/help/headless/graphql-api/graphiql-ide.md).

Para autenticação, o serviço de terceiros deve [recuperar um token de acesso](#retrieving-access-token) que pode então ser [usado na solicitação do GraphQL](#use-access-token-in-graphql-request).

## Recuperar um token de acesso {#retrieving-access-token}

Consulte [Geração de tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) para obter detalhes completos.

## Uso do token de acesso em uma solicitação de GraphQL {#use-access-token-in-graphql-request}

Para que um serviço de terceiros se conecte a uma instância AEM, ele deve ter uma *Token de acesso*. O serviço deve então adicionar esse token ao cabeçalho `Authorization` na solicitação POST.

Por exemplo, um cabeçalho de autorização GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisitos de permissão {#permission-requirements}

Todas as solicitações feitas usando o token de acesso são feitas *pela conta de usuário que gerou o token*.

Essa conta de usuário significa que você deve verificar se a conta tem as permissões necessárias para executar consultas do GraphQL.

Você pode verificar essas permissões usando o GraphiQL na instância local. Mais detalhes sobre [permissões podem ser encontrados aqui](/help/headless/security/permissions.md).
