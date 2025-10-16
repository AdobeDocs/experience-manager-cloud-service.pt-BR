---
title: Criar uma solicitação de API - Configuração Headless
description: Saiba como usar a API GraphQL para a entrega headless do conteúdo do Fragmento de conteúdo e a API REST do AEM Assets para gerenciar Fragmentos de conteúdo.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 85%

---

# Criar uma solicitação de API - Configuração Headless {#accessing-delivering-content-fragments}

Saiba como usar a API GraphQL para a entrega headless do conteúdo do Fragmento de conteúdo e a API REST do AEM Assets para gerenciar Fragmentos de conteúdo.

## O que são as APIs REST do GraphQL e do Assets? {#what-are-the-apis}

[Agora que criou alguns fragmentos de conteúdo](create-content-fragment.md), você pode usar as APIs do AEM para entregá-los de forma headless.

* A [API GraphQL](/help/headless/graphql-api/content-fragments.md) permite criar solicitações para acessar e fornecer Fragmentos de conteúdo. Essa API oferece o conjunto mais robusto de recursos para consultar e consumir conteúdo de Fragmentos de conteúdo.
   * Para usar a API, [defina e habilite os pontos de acesso no AEM](/help/headless/graphql-api/graphql-endpoint.md)e, se necessário, na [Interface GraphiQL instalada](/help/headless/graphql-api/graphiql-ide.md).
* Uma seleção de [APIs do AEM para Entrega e Gerenciamento de Conteúdo Estruturado](/help/headless/apis-headless-and-content-fragments.md) está disponível para uso com Fragmentos de Conteúdo.

O restante deste guia terá como foco o acesso ao GraphQL e a entrega de Fragmentos de conteúdo.

## Habilitar endpoint GraphQL {#enable-graphql-endpoint}

Para que as APIs GraphQL possam ser usadas, é necessário criar um endpoint GraphQL.

Para obter detalhes, consulte [Gerenciar pontos de extremidade do GraphQL no AEM](/help/headless/graphql-api/graphql-endpoint.md).

## Consultar conteúdo usando GraphQL com o GraphiQL

Os arquitetos da informação projetam consultas para seus pontos de acesso de canal para fornecer conteúdo. Considere essas consultas apenas uma vez por ponto de acesso, por modelo. Para os propósitos deste guia de introdução, só é necessário criar um.

GraphiQL é um IDE, incluído no seu ambiente do AEM; ele se torna acessível/visível após [configurar seus pontos de acesso](#enable-graphql-endpoint).

Para obter detalhes, consulte [Uso do GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md).

O GraphQL permite consultas estruturadas que podem direcionar não apenas conjuntos de dados específicos ou objetos de dados individuais, mas também fornecer elementos específicos dos objetos, resultados aninhados, oferecer suporte para variáveis de consulta e muito mais.

O GraphQL pode evitar solicitações de API iterativas e entrega em excesso e, em vez disso, permite a entrega em massa exatamente do que é necessário para renderizar em resposta a uma única consulta de API. O JSON resultante pode ser usado para fornecer dados a outros sites ou aplicativos.

## Próximas etapas {#next-steps}

Pronto! Agora você tem uma compreensão básica do gerenciamento de conteúdo headless no AEM. Existem muitos outros recursos onde é possível se aprofundar para obter um entendimento abrangente dos recursos disponíveis.

* **[Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md)** - Para obter detalhes sobre a criação e o gerenciamento dos Fragmentos de conteúdo
* **[Suporte a fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)** - Para obter detalhes sobre como acessar conteúdo do AEM diretamente pela API HTTP, por meio de operações CRUD (Criar, Ler, Atualizar, Excluir)
* **[API GraphQL](/help/headless/graphql-api/content-fragments.md)** - Para obter detalhes sobre como fornecer Fragmentos de conteúdo de forma headless

>[!NOTE]
>
>As [OpenAPIs](/help/headless/content-fragment-openapis.md) de Fragmento de Conteúdo e de Modelo de Fragmento de Conteúdo também estão disponíveis.
