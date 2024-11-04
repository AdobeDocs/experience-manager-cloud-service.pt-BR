---
title: AEM REST OpenAPI para entrega de fragmentos de conteúdo
description: Saiba mais sobre a API aberta REST para entrega de fragmentos de conteúdo do AEM
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
source-git-commit: d98aa9d206486022d465ca19c8888088562d56c3
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# AEM REST OpenAPI para entrega de fragmentos de conteúdo {#aem-rest-openapi-for-content-fragment-delivery}

>[!IMPORTANT]
>
>Essa API está disponível por meio do Early Adoter Program.
>
>Para ver o status e saber como se candidatar caso esteja interessado, confira as [Notas de Versão](/help/release-notes/release-notes-cloud/release-notes-current.md).

No Adobe Experience Manager (AEM) as a Cloud Service AEM, a API aberta do REST para entrega de fragmentos de conteúdo:

* é uma API REST HTTP em [AEM Edge Delivery Services](/help/edge/overview.md), projetada para fornecer conteúdo estruturado de Fragmentos de conteúdo no formato JSON
* O oferece uma integração moderna de CDN que permite a invalidação de conteúdo ativo
* O se concentra na entrega de conteúdo (desempenho, escalabilidade, integração de CDN, controle e saída JSON otimizados)
* inclui a capacidade de hidratar o JSON para fragmentos e ativos referenciados

Esta API:

* é o sucessor do [Suporte a Fragmentos de Conteúdo na API HTTP do AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)

* complementa as [APIs Abertas de Fragmentos de conteúdo e Modelos de fragmento de conteúdo](/help/headless/content-fragment-openapis.md), que permitem gerenciar os Fragmentos de conteúdo e os Modelos de fragmento de conteúdo (CRUD)

* é uma alternativa HTTP REST para a [API AEM GraphQL para uso com Fragmentos de conteúdo](/help/headless/graphql-api/content-fragments.md)

Para obter a documentação completa, consulte [Esquemas de API do AEM Sites - API de entrega de fragmentos de conteúdo (2024.07-experimental)](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/sites/delivery/).

>[!NOTE]
>
>Consulte [APIs de AEM para Entrega e Gerenciamento de Conteúdo Estruturado](/help/headless/apis-headless-and-content-fragments.md) para obter uma visão geral das várias APIs disponíveis e uma comparação de alguns dos conceitos envolvidos.

## Armazenamento em cache {#caching}

AEM integra-se com o AEM CDN Fastly. Isso significa que as respostas JSON fornecidas no nível de publicação são armazenadas em cache no nível do Fastly.

As respostas são armazenadas em cache com base em cabeçalhos de cache predefinidos (não pode ser configurado):

* As respostas são armazenadas em cache por 5 minutos no cache do navegador/cliente
   * `max-age`=`300`
* As respostas são armazenadas em cache por 1 hora no cache CDN
   * `s-maxage`=`3600`
* O conteúdo obsoleto pode ser distribuído ao revalidar novas solicitações por até 1 hora
   * `stale-while-revalidate`=`3600`
* O conteúdo obsoleto pode ser distribuído, por erro, por até um dia
   * `stale-on-error`=`86400`

O AEM também vem com invalidação ativa do cache da CDN. Isso significa que sempre que o conteúdo é atualizado ou publicado, as respostas JSON OpenAPI correspondentes são invalidadas automaticamente, por meio de uma solicitação de limpeza temporária para o Fastly. Isso permite que você veja as alterações refletidas na saída JSON, antes que a idade real do cache do CDN (`s-maxage`) seja atingida.