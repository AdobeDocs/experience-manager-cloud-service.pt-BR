---
title: APIs de AEM para entrega de conteúdo estruturado e gerenciamento de fragmento de conteúdo
description: Saiba mais sobre as APIs disponíveis para Entrega de conteúdo estruturado e Gerenciamento de fragmento de conteúdo
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
source-git-commit: 21599676916068f3529976410a93951b02f750b0
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---


# APIs do AEM para entrega e gerenciamento de conteúdo estruturado {#aem-apis-structured-content-delivery-and-management}

O Adobe Experience Manager (AEM) as a Cloud Service várias APIs para a entrega de conteúdo estruturado do gerenciamento de Fragmentos de conteúdo e Fragmentos de conteúdo. Consulte as páginas individuais para obter mais detalhes sobre as APIs específicas.

* AEM [OpenAPI REST para Entrega de Fragmento de Conteúdo](/help/headless/aem-rest-openapi-content-fragment-delivery.md)
   * Essa API cria respostas JSON para fornecer conteúdo estruturado de fragmentos de conteúdo no AEM.
   * Ele usa um caminho para um fragmento de conteúdo como endpoint.
   * Essa API é baseada em REST.
   * Ele é otimizado para entrega de conteúdo, incluindo integração de CDN.
* [AEM API do GraphQL para entrega de fragmentos de conteúdo](/help/headless/graphql-api/content-fragments.md)
   * Essa API é baseada em esquemas. Os esquemas de API são representados por Modelos de fragmento de conteúdo, que definem a estrutura do conteúdo.
   * Essa API é baseada no GraphQL.
* [Fragmentos de conteúdo e OpenAPIs de modelos de fragmento de conteúdo](/help/headless/content-fragment-openapis.md)
   * Essas APIs são destinadas ao gerenciamento de conteúdo estruturado.
   * Os respectivos operadores de GET não são otimizados para a entrega de conteúdo.
   * Essa API é baseada em REST.
* [Suporte a fragmentos de conteúdo na API HTTP do AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
   * A API original da saída JSON para entrega de conteúdo estruturado no AEM.
      * Embora robusta e comprovada, essa API não fornece saída JSON *totalmente hidratada*. As referências são geradas apenas como caminhos, exigindo solicitações de API secundárias para recuperar mais conteúdo.
   * A API HTTP do Assets também pode ser usada para gerenciar os Fragmentos de conteúdo e os Modelos de fragmento de conteúdo (CRUD).
   * Essa API é baseada em REST.
   * O suporte a fragmentos de conteúdo na API HTTP do Assets será descontinuado no futuro, pois está sendo sucedido pela API REST Edge Delivery Services JSON. A escala de tempo ainda não foi decidida.

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

A API usada é uma decisão para os desenvolvedores - o AEM suporta ambos.

Muitas comparações estão disponíveis online, mas alguns destaques e benefícios do REST incluem:

* Simplicidade

   * Os desenvolvedores estão (geralmente) familiarizados com HTTP e REST. De acordo com o [Estado Postman do relatório de APIs](https://www.postman.com/state-of-api/), uma alta porcentagem de desenvolvedores usam REST.

   * Com simplicidade vem a familiaridade. Com o REST, não há perguntas organizacionais sobre quem é o proprietário das consultas e quem é o proprietário do aplicativo, enquanto essas perguntas podem surgir com o GraphQL.

   * Com familiaridade (normalmente), existe uma ampla comunidade e um cenário de ferramentas. Não é uma desvantagem inerente do GraphQL, mas provavelmente será mais ampla e profunda para REST.

   * A abordagem mais simples também pode facilitar a implementação da segurança. Com REST, a filtragem para determinar o conteúdo para renderizar tudo acontece no aplicativo cliente. Com o GraphQL, isso acontece em uma consulta baseada em esquema entre cliente e servidor.

* Flexibilidade

   * Com REST, o desenvolvedor pode `GET` qualquer recurso. Com o GraphQL, eles são limitados a recursos definidos em um esquema.

* Armazenamento em cache

   * As respostas JSON para solicitações REST `GET` são inerentemente armazenáveis em cache. As solicitações `POST` do GraphQL não podem ser armazenadas em cache, a menos que sejam feitas dessa forma; por exemplo, usando consultas AEM persistidas armazenadas no servidor e solicitadas com solicitações `GET` semelhantes a REST.

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
