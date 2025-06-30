---
title: Pesquisar API do Assets
description: Saiba como usar a API do Search Assets.
role: User
exl-id: 0c52e793-4c33-4230-b4f2-27296dd9e4b3
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Pesquisar API do Assets {#search-assets-api}

Todos os [ativos aprovados](approve-assets.md) disponíveis no repositório de ativos da Experience Manager podem ser pesquisados e entregues a aplicativos downstream integrados usando uma URL de entrega.

Pesquisar os ativos corretos aprovados no repositório do Experience Manager é a primeira etapa para fornecer ativos usando o URL de entrega. A resposta à solicitação de pesquisa compreende uma variedade de documentos JSON correspondentes aos ativos que atendem aos critérios de pesquisa. Cada documento JSON é identificado usando um campo `id`, que é usado para compor a solicitação de entrega de ativos.

![Visão geral do protocolo de carregamento binário direto](assets/search-assets-api-overview.png)

Você pode definir propriedades na solicitação da API Search Assets para ativar os seguintes recursos:

* **Pesquisa de texto completo**: use a consulta `match` para definir o texto a ser pesquisado.  Você também pode usar operadores dentro da consulta `match` para filtrar os resultados.

* **Aplicar filtros**: use a consulta `term` para filtrar ainda mais os resultados definindo um `key` e um ou vários valores. `key` identifica o campo cujo valor deve ser combinado e `value` representa o que deve ser comparado. Da mesma forma, você pode usar a consulta `range` para definir um intervalo para um campo usando as propriedades Greater-than (gt), Greater-than ou equal-to (gte), Less-than (lt) e Less-than or equal-to (lte).

* **Classificar resultados**: use a propriedade `OrderBy` para classificar resultados de pesquisa com base em um ou vários campos. Você pode classificar os resultados em uma ordem crescente ou decrescente.

* **Paginação**: use as propriedades `limit` e `cursor` para definir propriedades de paginação em uma solicitação de API de Pesquisa. A propriedade `limit` define o número máximo de itens a serem recuperados em uma resposta de API. A propriedade `cursor` facilita a recuperação do ponto inicial para o próximo conjunto de ativos definido na propriedade `limit`. Por exemplo, se você definir `50` como o limite na solicitação de API, poderá usar a propriedade `cursor` para iniciar e recuperar os próximos 50 itens usando a próxima solicitação de API.

## Pesquisar ponto de extremidade da API de ativos {#search-assets-api-endpoint}

O endpoint em uma solicitação da API de ativos de Pesquisa deve estar no seguinte formato:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

O domínio de delivery é semelhante em estrutura ao domínio do ambiente do autor do Experience Manager. A única diferença é a substituição do termo `author` por `delivery`.

`pXXXX` refere-se à ID do programa

`eYYYY` refere-se à ID de ambiente

## Pesquisar método de solicitação da API de ativos {#search-assets-api-request-method}

POST

## Pesquisar cabeçalho da API do Assets {#search-assets-api-header}

Você precisa fornecer os seguintes detalhes ao definir um cabeçalho na API de ativos de pesquisa:

```java
headers: {
      'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    },
```

Para invocar a API de Pesquisa, é necessário um token IMS para definir nos detalhes de `Authorization`. O token IMS é obtido de uma conta técnica. Consulte [Buscar as credenciais do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) para criar uma nova conta técnica. Consulte [Gerar o token de acesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) para gerar o token IMS e usá-lo corretamente no cabeçalho de solicitação da API de ativos de pesquisa.

Para exibir amostras de solicitações, amostras de respostas e códigos de resposta, consulte [API de Assets de Pesquisa](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/search).
