---
title: APIs do AEM para entrega de conteúdo estruturado e gerenciamento de fragmento de conteúdo
description: Saiba mais sobre as APIs disponíveis para Entrega de conteúdo estruturado e Gerenciamento de fragmento de conteúdo
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: 95aecd30-566a-42a9-b97a-7efe45fd389c
source-git-commit: 243adc6f6428cea23c04ca788bd8ad0bda7e4501
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# APIs do AEM para entrega e gerenciamento de conteúdo estruturado {#aem-apis-structured-content-delivery-and-management}

O Adobe Experience Manager (AEM) as a Cloud Service oferece várias APIs para entrega de conteúdo estruturado a partir de fragmentos de conteúdo e do gerenciamento de fragmentos de conteúdo. Consulte as páginas individuais para obter mais detalhes sobre as APIs específicas.

* [Entrega de fragmento de conteúdo do AEM com OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md)
   * Essa API cria respostas JSON para fornecer conteúdo estruturado de fragmentos de conteúdo no AEM.
   * Ele usa um caminho para um fragmento de conteúdo como endpoint.
   * Essa API é baseada em REST.
   * Ele é otimizado para entrega de conteúdo, incluindo integração de CDN.
* [API do AEM GraphQL para entrega de fragmentos de conteúdo](/help/headless/graphql-api/content-fragments.md)
   * Essa API é baseada em esquemas. Os esquemas de API são representados por Modelos de fragmento de conteúdo, que definem a estrutura do conteúdo.
   * Essa API é baseada no GraphQL.
* [Fragmentos de conteúdo e OpenAPIs de modelos de fragmento de conteúdo](/help/headless/content-fragment-openapis.md)
   * Essas APIs são destinadas ao gerenciamento de conteúdo estruturado.
   * Os respectivos operadores do GET não estão otimizados para a entrega de conteúdo.
   * Essa API é baseada em REST.

>[!NOTE]
>
>O [Suporte a Fragmento de Conteúdo na API HTTP do Assets](/help/assets/content-fragments/assets-api-content-fragments.md) agora está [obsoleto](/help/release-notes/deprecated-removed-features.md). Ele foi substituído por [Entrega de fragmento de conteúdo com OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md), juntamente com [Fragmentos de conteúdo e OpenAPIs de gerenciamento de modelos de fragmento de conteúdo](/help/headless/content-fragment-openapis.md).

## REST vs GraphQL {#rest-vs-graphql}

A API usada é uma decisão para os desenvolvedores. O AEM oferece suporte a ambos.

Muitas comparações estão disponíveis online, mas alguns destaques e benefícios do REST incluem:

* Simplicidade

   * Os desenvolvedores estão (geralmente) familiarizados com HTTP e REST. De acordo com o [Estado Postman do relatório de APIs](https://www.postman.com/state-of-api/), uma alta porcentagem de desenvolvedores usam REST.

   * Com simplicidade vem a familiaridade. Com o REST, não há perguntas organizacionais sobre quem é o proprietário das consultas e quem é o proprietário do aplicativo, enquanto essas perguntas podem surgir com o GraphQL.

   * Com familiaridade (normalmente), existe uma ampla comunidade e um cenário de ferramentas. Não é uma desvantagem inerente do GraphQL, mas provavelmente será mais ampla e profunda para REST.

   * A abordagem mais simples também pode facilitar a implementação da segurança. Com REST, a filtragem para determinar o conteúdo para renderizar tudo acontece no aplicativo cliente. Com o GraphQL, isso acontece em uma consulta baseada em esquema entre cliente e servidor.

* Flexibilidade

   * Com REST, o desenvolvedor pode `GET` qualquer recurso. Com o GraphQL, eles são limitados a recursos definidos em um esquema.

* Armazenamento em cache

   * As respostas JSON para solicitações REST `GET` são inerentemente armazenáveis em cache. As solicitações do GraphQL `POST` não podem ser armazenadas em cache, a menos que sejam feitas assim; por exemplo, usando as Consultas AEM persistidas armazenadas no servidor e solicitadas com solicitações `GET` semelhantes a REST.

Os benefícios da GraphQL incluem:

* Eficiência da entrega de conteúdo

   * Foco

      * Com o GraphQL, os aplicativos cliente podem solicitar o conteúdo exato que precisam para renderização - e não mais. Essa abordagem evita a entrega excessiva de conteúdo, com cargas úteis excessivas de conteúdo e consumo desnecessário de largura de banda.

   * Endpoint único

      * Enquanto no REST cada solicitação de API é um endpoint, no GraphQL há apenas um endpoint comum e solicitações de conteúdo diferentes são expressas como consultas usando esse endpoint comum.

* Prototipagem rápida

   * Com o GraphQL, esse é um processo de uma etapa, reunido na query do GraphQL, e pode facilitar a criação de protótipos. O REST, por outro lado, é um processo de duas etapas:

      1. Buscar conteúdo com a API.
      2. Na resposta JSON, determine o que usar para renderização no aplicativo do cliente.
