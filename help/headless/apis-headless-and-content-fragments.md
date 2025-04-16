---
title: APIs do AEM para entrega de conteúdo estruturado e gerenciamento de fragmento de conteúdo
description: Saiba mais sobre as APIs disponíveis para Entrega de conteúdo estruturado e Gerenciamento de fragmento de conteúdo
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: 95aecd30-566a-42a9-b97a-7efe45fd389c
source-git-commit: d9db32110e1e0aaa5bdc20bd6b4bff6da6a3a3a3
workflow-type: tm+mt
source-wordcount: '591'
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
* [Suporte a fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
   * A API original da saída JSON para entrega de conteúdo estruturado no AEM.
      * Embora robusta e comprovada, essa API não fornece saída JSON *totalmente hidratada*. As referências são geradas apenas como caminhos, exigindo solicitações de API secundárias para recuperar mais conteúdo.
   * A API HTTP do Assets também pode ser usada para gerenciar os Fragmentos de conteúdo e os Modelos de fragmento de conteúdo (CRUD).
   * Essa API é baseada em REST.
   * O suporte a fragmentos de conteúdo na API HTTP do Assets será descontinuado no futuro, pois está sendo sucedido pela API REST JSON do Edge Delivery Services. A escala de tempo ainda não foi decidida.

<!--
## JSON vs HTML {#json-vs-HTML}

The content delivery format used is driven by frontend implementation. Unstructured content/HTML for full-stack implementations, structured content/JSON for headless implementations, or a combination of both in hybrid implementations. 

Key considerations include:

* Definition
  * JSON (JavaScript Object Notation) - used to represent, access and process structured data. 
  * HTML (HyperText Markup Language) - a markup language of tags and elements in a hierarchical structure.
* Primary Purpose
  * JSON is often used for transferring structure content between the server and client app.
  * HTML is the standard markup language for creating and rendering web pages in a browser.
-->

## REST vs GraphQL {#rest-vs-graphql}

The API used is a decision for the developers - AEM supports both.

Muitas comparações estão disponíveis online, mas alguns destaques e benefícios do REST incluem:

* Simplicidade

   * Os desenvolvedores estão (geralmente) familiarizados com HTTP e REST. De acordo com o [Estado Postman do relatório de APIs](https://www.postman.com/state-of-api/), uma alta porcentagem de desenvolvedores usam REST.

   * Com simplicidade vem a familiaridade. Com o REST, não há perguntas organizacionais sobre quem é o proprietário das consultas e quem é o proprietário do aplicativo, enquanto essas perguntas podem surgir com o GraphQL.

   * With familiarity (typically) comes a broad community and tooling landscape. Not an inherent disadvantage of GraphQL, but likely to be broader and deeper for REST.

   * The simpler approach can also make the security implementation easier. With REST, the filtering to determine the content to render all happens in the client app. With GraphQL this happens in a schema-based query between client and server.

* Flexibilidade

   * Com REST, o desenvolvedor pode `GET` qualquer recurso. Com o GraphQL, eles são limitados a recursos definidos em um esquema.

* Armazenamento em cache

   * JSON responses to REST `GET` requests are inherently cacheable. GraphQL `POST` requests are not cacheable, unless they are made so; for example, by using AEM Persisted Queries that are stored on the server and requested with REST-like `GET`requests.

Benefits of GraphQL include:

* Efficiency of content delivery

   * Foco

      * Com o GraphQL, os aplicativos cliente podem solicitar o conteúdo exato que precisam para renderização - e não mais. Essa abordagem evita a entrega excessiva de conteúdo, com cargas úteis excessivas de conteúdo e consumo desnecessário de largura de banda.

   * Endpoint único

      * Enquanto no REST cada solicitação de API é um endpoint, no GraphQL há apenas um endpoint comum e solicitações de conteúdo diferentes são expressas como consultas usando esse endpoint comum.

* Rapid Prototyping

   * With GraphQL this is a one-step process, brought together in the GraphQL query, and can make prototyping easier. O REST, por outro lado, é um processo de duas etapas:

      1. Fetch content with API.
      2. In the JSON response, determine what to use for rendering in the client app.
