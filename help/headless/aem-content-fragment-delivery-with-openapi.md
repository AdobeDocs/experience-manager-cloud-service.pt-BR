---
title: Entrega de fragmento de conteúdo do AEM com OpenAPI
description: Saiba mais sobre a entrega de fragmentos de conteúdo do AEM com OpenAPI
feature: Headless, Content Fragments, Edge Delivery Services
role: Admin, Developer
exl-id: b298db37-1033-4849-bc12-7db29fb77777
source-git-commit: de161d6707dcb8cedf032ee1f286d79e733be94d
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---


# Entrega de fragmento de conteúdo do AEM com OpenAPI {#aem-content-fragment-delivery-with-openapi}

No Adobe Experience Manager (AEM) as a Cloud Service, a API aberta do AEM para entrega de fragmentos de conteúdo:

* é uma OpenAPI otimizada para entrega ao vivo de fragmentos de conteúdo do AEM no formato JSON
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

>[!IMPORTANT]
>
>Para habilitar a Entrega de fragmento de conteúdo com OpenAPI no AEM as a Cloud Service, verifique se ela ainda não está habilitada e envie um tíquete de Suporte do Adobe com o título **Habilitar Entrega de Fragmento de Conteúdo com OpenAPI** e especifique:
>
>* as IDs de ambiente e programa do Cloud Service
>* detalhes do caso de uso que você deseja resolver com a OpenAPI de entrega de fragmento de conteúdo
>* detalhes de todos os contatos aos quais o Adobe deve responder e manter-se informado sobre a solicitação e o projeto (se necessário)

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

A entrega de fragmentos de conteúdo com OpenAPI é compatível com a invalidação ativa do cache CDN. Isso significa que sempre que o conteúdo é atualizado ou publicado, as respostas JSON OpenAPI correspondentes são invalidadas automaticamente, por meio de uma solicitação de limpeza temporária para o Fastly. Isso permite que você veja as alterações refletidas na saída JSON, antes que a idade real do cache do CDN (`s-maxage`) seja atingida.

## Disponibilidade {#availability}

A Entrega de fragmento de conteúdo com OpenAPI está disponível nos níveis de Pré-visualização e Publicação. A OpenAPI fornece Fragmentos de conteúdo no formato JSON, para visualização e entrega em tempo real.

Para pré-visualização, a entrega do fragmento de conteúdo com OpenAPI pode:

* publicar para visualização
* habilitar acesso para visualização com a lista de permissões de IP
* obter o URL de visualização

## CORS {#cors}

As [origens permitidas do CORS](/help/headless/deployment/cross-origin-resource-sharing.md) definem as origens que podem chamar a API.

As origens permitidas do CORS definidas no lado da configuração do dispatcher, especificamente para o GraphQL, não são consideradas por essa API.

## Limites de taxa de API {#api-rate-limits}

A API permite novas solicitações a uma taxa de até 200 solicitações por segundo, por ambiente.

Quando esse limite for excedido, a API começará a enviar [429 respostas de erro](https://www.rfc-editor.org/rfc/rfc6585#section-4). Esses erros devem ser tratados por qualquer aplicativo cliente e as solicitações com falha devem ser repetidas após uma nova tentativa de backoff exponencial. A resposta HTTP vem com um cabeçalho específico, `Retry-After`, que indica ao cliente quanto tempo ele precisa aguardar antes de enviar a solicitação novamente.

## Solicitações autenticadas {#authenticated-requests}

O suporte para solicitações autenticadas pode ser implementado com a [chave Edge CDN do AEM](/help/implementing/dispatcher/cdn-credentials-authentication.md). Usar a chave Edge de CDN da AEM permite que você confie na CDN da AEM e garanta que somente solicitações específicas possam acessar a API, com base no cabeçalho de chave da Edge fornecido.

>[!NOTE]
>
>No momento, a autorização baseada nas ACLs específicas do repositório não é suportada.

<!-- 
## Limitations {#limitations}
-->
