---
title: APIs de entrega
description: Saiba como usar as APIs de entrega.
role: User
source-git-commit: 6fdc44b93e11a20b6859419813fd7eadbefd95c1
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# APIs de entrega {#delivery-apis}

Todos [ativos aprovados](approve-assets.md) disponível no repositório do Experience Manager assets pode ser [pesquisado](search-assets-api.md) e depois entregue aos aplicativos downstream integrados usando um URL de entrega.

Quaisquer alterações feitas em ativos aprovados no DAM, incluindo atualizações de versão e modificações de metadados, são refletidas automaticamente nos URLs de entrega. Com um valor curto de Tempo de vida (TTL) de 10 minutos configurado para a entrega de ativos por meio da CDN, as atualizações se tornam visíveis em todas as interfaces de criação e publicação em menos de 10 minutos.

A imagem a seguir ilustra os URLs de entrega disponíveis:

![APIs de entrega](assets/delivery-url.png)

A tabela a seguir ilustra o uso das várias APIs de entrega disponíveis:

| API de entrega | Descrição |
|---|---|
| [Representação binária otimizada para a Web do ativo no formato de saída solicitado](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) | Retorna a representação binária otimizada para a Web do ativo no formato de saída solicitado com base na ID do ativo enviada na solicitação. Além disso, você pode definir vários modificadores de imagem, como largura, altura, girar, virar, qualidade, recorte, formato e [recorte inteligente](/help/assets/dynamic-media/image-profiles.md). Consulte a [Detalhes da API](https://adobe-aem-assets-delivery-experimental.redoc.ly/#operation/getAssetSeoFormat) para formatos e modificadores de imagem compatíveis.<br>O Adobe recomenda o uso dessa API para todos os tipos de formato de imagem. |
| [Representação binária do ativo otimizada para a Web](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAsset) | A API de conveniência que aplica padrões à representação binária otimizada para a Web do ativo retornado na resposta. Os padrões incluem um formato JPEG/WEBP padrão, qualidade => 65 e largura => 1024. |
| [Binário original carregado do ativo](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetOriginal) | Retorna os binários carregados originalmente para o ativo. O Adobe recomenda usar essa API para tipos de formato de documento e imagens SVG. |
| [Representação pré-gerada do ativo disponível no ambiente de criação do AEM Assets](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetRendition) | Retorna o fluxo de bits da representação de ativos disponível no ambiente de criação do AEM Assets com base na ID do ativo e no nome da representação enviados na solicitação. |
| [Metadados do ativo](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetMetadata) | Retorna as propriedades associadas a um ativo, como, título, descrição, CreateDate, ModifyDate, entre outros. |
| [Contêiner do player para o ativo de vídeo](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoPlayerDelivery) | Retorna o container do reprodutor do ativo de vídeo. Você pode incorporar o reprodutor em um elemento de HTML iframe e reproduzir o vídeo. |
| [A reprodução se manifesta no formato de saída selecionado](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoManifestDelivery) | Retorna o arquivo de manifesto de reprodução do ativo de vídeo especificado no formato de saída selecionado. Você deve criar um reprodutor personalizado capaz de transmissão adaptável por meio dos protocolos HLS ou DASH para poder obter o arquivo de manifesto de reprodução e reproduzir o vídeo. |

## Endpoints das APIs de entrega {#delivery-apis-endpoint}

Os endpoints da API variam para cada API de entrega. Por exemplo, o endpoint da API para `Web-optimized binary representation of the asset in the requested output format` A API é:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

O domínio de delivery é semelhante em estrutura ao domínio do ambiente do autor do Experience Manager. A única diferença é substituir o termo `author` com `delivery`.

`pXXXX` refere-se à ID do programa

`eYYYY` refere-se à ID de ambiente

Consulte [Detalhes da API](https://adobe-aem-assets-delivery.redoc.ly/#tag/Assets) para obter mais informações.

## Método de solicitação de APIs de entrega {#delivery-api-request-method}

GET

## Cabeçalho das APIs de entrega {#deliver-assets-api-header}

Você precisa fornecer os seguintes detalhes ao definir um cabeçalho no cabeçalho das APIs de entrega:

```java
headers: {
      'If-None-Match': 'string',
      Authorization: 'Bearer <YOUR_JWT_HERE>'
    }
```

Para chamar as APIs de entrega, é necessário um token IMS na `Authorization` detalhes para entregar um ativo restrito. O token IMS é obtido de uma conta técnica. Consulte [Buscar as credenciais do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#fetch-the-aem-as-a-cloud-service-credentials) para criar uma nova conta técnica. Consulte [Gerar o token de acesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#generating-the-access-token) para gerar o token IMS e usá-lo corretamente no cabeçalho da solicitação das APIs de entrega.


Para exibir amostras de solicitações, amostras de respostas e códigos de resposta, consulte [APIs de entrega](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat).