---
title: Pesquisar API do Assets
description: Saiba como usar a API do Search Assets.
role: User
source-git-commit: 3e2fe458460fe8ec4c1dd12152c1134bfb9ca62b
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# Pesquisar API do Assets {#search-assets-api}

Todos [ativos aprovados](approve-assets.md) disponível no repositório do Experience Manager assets pode ser pesquisado e entregue aos aplicativos downstream integrados usando um URL de entrega.

Pesquisar os ativos corretos aprovados no repositório Experience Manager é a primeira etapa para fornecer ativos usando o URL de entrega. A resposta à solicitação de pesquisa compreende uma variedade de documentos JSON correspondentes aos ativos que atendem aos critérios de pesquisa. Cada documento JSON é identificado usando um `id` que é usado para compor a solicitação de entrega do ativo.

![Visão geral do protocolo de upload binário direto](assets/search-assets-api-overview.png)

Você pode definir propriedades na solicitação da API Search Assets para ativar os seguintes recursos:

* **Pesquisa de texto completo**: Use o `match` query para definir o texto a ser pesquisado.  Também é possível usar operadores dentro do `match` query para filtrar os resultados.

* **Aplicar filtros**: Use o `term` consulta para filtrar ainda mais os resultados definindo um `key` e um ou vários valores. `key` identifica o campo cujo valor deve ser correspondido e `value` representa o que deve ser comparado. Da mesma forma, você pode usar o `range` consulta para definir um intervalo para um campo usando as propriedades Greater-than (gt), Greater-than or equal-to (gte), Less-than (lt) e Less-than or equal-to (lte).

* **Classificar resultados**: Use o `OrderBy` para classificar os resultados da pesquisa com base em um ou vários campos. Você pode classificar os resultados em uma ordem crescente ou decrescente.

* **Paginação**: Use o `limit` e `cursor` para definir propriedades de paginação em uma solicitação de API de pesquisa. `limit` define o máximo de itens a serem recuperados em uma resposta de API. `cursor` propriedade facilita a recuperação do ponto de partida para o próximo conjunto de ativos definido na `limit` propriedade. Por exemplo, se você definir `50` como o limite na solicitação da API, você pode usar o `cursor` para iniciar e recuperar os próximos 50 itens usando a próxima solicitação de API.

## Pesquisar ponto de extremidade da API de ativos {#search-assets-api-endpoint}

O endpoint em uma solicitação da API de ativos de Pesquisa deve estar no seguinte formato:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/search`

O domínio de delivery é semelhante em estrutura ao domínio do ambiente do autor do Experience Manager. A única diferença é substituir o termo `author` com `delivery`.

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

Para chamar a API de pesquisa, é necessário um token IMS para definir na `Authorization` detalhes. O token IMS é obtido de uma conta técnica. Consulte [Buscar as credenciais do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) para criar uma nova conta técnica. Consulte [Gerar o token de acesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) para gerar o token IMS e usá-lo corretamente no cabeçalho da solicitação da API de ativos de pesquisa.

Para exibir amostras de solicitações, amostras de respostas e códigos de resposta, consulte [Pesquisar API do Assets](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/search).
