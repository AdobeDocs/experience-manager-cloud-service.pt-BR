---
title: Entrega de fragmento de conteúdo do AEM com OpenAPI
description: Saiba mais sobre a entrega de fragmentos de conteúdo do AEM com OpenAPI
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: 4f58a52c5ccc8178e768f9072e7b2047cbe3fb20
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Entrega de fragmento de conteúdo do AEM com OpenAPI {#aem-content-fragment-delivery-with-openapi}

No Adobe Experience Manager (AEM) as a Cloud Service, a API aberta do AEM para entrega de fragmentos de conteúdo:

* é uma API REST HTTP no [AEM Edge Delivery Services](/help/edge/overview.md), projetada para fornecer conteúdo estruturado de Fragmentos de conteúdo no formato JSON
* O oferece uma integração moderna de CDN que permite a invalidação de conteúdo ativo
* O se concentra na entrega de conteúdo (desempenho, escalabilidade, integração de CDN, controle e saída JSON otimizados)
* inclui a capacidade de hidratar o JSON para fragmentos e ativos referenciados

Esta API:

* é o sucessor do [Suporte a Fragmentos de Conteúdo na API HTTP do AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)

* complementa as [APIs Abertas de Fragmentos de conteúdo e Modelos de fragmento de conteúdo](/help/headless/content-fragment-openapis.md), que permitem gerenciar os Fragmentos de conteúdo e os Modelos de fragmento de conteúdo (CRUD)

* é uma alternativa HTTP REST à [API do AEM GraphQL para uso com Fragmentos de conteúdo](/help/headless/graphql-api/content-fragments.md)

Para obter a documentação completa, consulte [Entrega de fragmento de conteúdo do AEM com OpenAPI](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/contentfragments/delivery/).

>[!NOTE]
>
>Consulte [APIs do AEM para Entrega e Gerenciamento de Conteúdo Estruturado](/help/headless/apis-headless-and-content-fragments.md) para obter uma visão geral das várias APIs disponíveis e uma comparação de alguns dos conceitos envolvidos.

## Armazenamento em cache {#caching}

O AEM integra-se ao AEM CDN Fastly. Isso significa que as respostas JSON fornecidas no nível de publicação são armazenadas em cache no nível do Fastly.

As respostas são armazenadas em cache com base em cabeçalhos de cache predefinidos (não pode ser configurado):

* As respostas são armazenadas em cache por 5 minutos no cache do navegador/cliente
   * `max-age`=`300`
* As respostas são armazenadas em cache por 1 hora no cache CDN
   * `s-maxage`=`3600`
* O conteúdo obsoleto pode ser distribuído ao revalidar novas solicitações por até 1 hora
   * `stale-while-revalidate`=`3600`
* O conteúdo obsoleto pode ser distribuído, por erro, por até um dia
   * `stale-on-error`=`86400`

O AEM também vem com a invalidação do cache CDN ativo. Isso significa que sempre que o conteúdo é atualizado ou publicado, as respostas JSON OpenAPI correspondentes são invalidadas automaticamente, por meio de uma solicitação de limpeza temporária para o Fastly. Isso permite que você veja as alterações refletidas na saída JSON, antes que a idade real do cache do CDN (`s-maxage`) seja atingida.
