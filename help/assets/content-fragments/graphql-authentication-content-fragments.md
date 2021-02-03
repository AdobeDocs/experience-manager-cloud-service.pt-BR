---
title: Autenticação para Query GraphQL de AEM Remotos em Fragmentos de Conteúdo
description: Saiba mais sobre a autenticação necessária para query GraphQL de AEM Remotos.
translation-type: tm+mt
source-git-commit: 42ca0c70f7018a6e3c9be68ef13adefafc987864
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Autenticação para Query GraphQL de AEM Remotos em Fragmentos de Conteúdo {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Um caso de uso principal para o Adobe Experience Manager [como uma API GraphQL Cloud Service (AEM) para o Delivery de fragmento de conteúdo](/help/assets/content-fragments/graphql-api-content-fragments.md) é aceitar query remotos de aplicativos ou serviços de terceiros.  Esses query remotos podem exigir acesso à API autenticada.

>[!NOTE]
>
>Para teste e desenvolvimento, você também pode acessar a API AEM GraphQL diretamente usando a interface [GraphiQL](/help/assets/content-fragments/graphql-api-content-fragments.md#graphiql-interface).

Para autenticação, o serviço de terceiros precisa usar um [Token de acesso](#access-token), que pode ser [usado no Pedido GraphQL](#use-access-token-in-graphql-request).

## Recuperando um Token de acesso {#retrieving-access-token}

Consulte [Gerando Tokens de acesso para APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) para obter detalhes completos.

## Uso do Token de acesso em uma solicitação GraphQL {#use-access-token-in-graphql-request}

Para que um serviço de terceiros se conecte a uma instância AEM, é necessário ter um *Token de acesso*. O serviço deve adicionar esse token ao cabeçalho `Authorization` na solicitação de POST.

Por exemplo, um cabeçalho de autorização GraphQL:

```xml
Authorization: Bearer <access_token>
```

## Requisitos de permissão {#permission-requirements}

Todas as solicitações feitas usando o token de acesso serão feitas *pela conta de usuário que gerou o token*.

Isso significa que é necessário verificar se a conta tem as permissões necessárias para executar query GraphQL.

Você pode verificar isso usando o GraphiQL na instância local.
