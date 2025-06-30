---
title: APIs de entrega
description: Saiba como usar as APIs de entrega.
role: User
exl-id: 806ca38f-2323-4335-bfd8-a6c79f6f15fb
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# APIs de entrega {#delivery-apis}

Todos os [ativos aprovados](approve-assets.md) disponíveis no repositório de ativos da Experience Manager podem ser [pesquisados](search-assets-api.md) e entregues a aplicativos downstream integrados usando uma URL de entrega.

Quaisquer alterações feitas em ativos aprovados no DAM, incluindo atualizações de versão e modificações de metadados, são refletidas automaticamente nos URLs de entrega. Com um valor curto de Tempo de vida (TTL) de 10 minutos configurado para a entrega de ativos por meio da CDN, as atualizações se tornam visíveis em todas as interfaces de criação e publicação em menos de 10 minutos.

A imagem a seguir ilustra os URLs de entrega disponíveis:

![APIs de entrega](assets/delivery-url.png)

A tabela a seguir ilustra o uso das várias APIs de entrega disponíveis:

| API de entrega | Descrição |
|---|---|
| [Representação binária otimizada para a Web do ativo no formato de saída solicitado](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) | Retorna a representação binária otimizada para a Web do ativo no formato de saída solicitado com base na ID do ativo enviada na solicitação. Além disso, você pode definir vários modificadores de imagem, como largura, altura, rotação, inversão, qualidade, recorte, formato e [recorte inteligente](/help/assets/dynamic-media/image-profiles.md). Consulte os [detalhes da API](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat) para obter os formatos e modificadores de imagem compatíveis.<br>A Adobe recomenda usar essa API para todos os tipos de formato de imagem. |
| [Representação binária otimizada para a Web do ativo](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAsset) | A API de conveniência que aplica padrões à representação binária otimizada para a Web do ativo retornado na resposta. Os padrões incluem um formato JPEG/WEBP padrão, qualidade => 65 e largura => 1024. |
| [Binário original carregado do ativo](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetOriginal) | Retorna os binários carregados originalmente para o ativo. A Adobe recomenda usar essa API para tipos de formato de documento e imagens SVG. |
| [Representação pré-gerada do ativo disponível no ambiente de criação do AEM Assets](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetRendition) | Retorna o fluxo de bits da representação de ativos disponível no ambiente de criação do AEM Assets com base na ID do ativo e no nome da representação enviados na solicitação. |
| [Metadados do ativo](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetMetadata) | Retorna as propriedades associadas a um ativo, como, título, descrição, CreateDate, ModifyDate, entre outros. |
| [Contêiner de player do ativo de vídeo](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoPlayerDelivery) | Retorna o container do reprodutor do ativo de vídeo. Você pode incorporar o reprodutor em um elemento HTML do iframe e reproduzir o vídeo. |
| [Manifestos de reprodução no formato de saída selecionado](https://adobe-aem-assets-delivery.redoc.ly/#operation/videoManifestDelivery) | Retorna o arquivo de manifesto de reprodução do ativo de vídeo especificado no formato de saída selecionado. Você deve criar um reprodutor personalizado capaz de transmissão adaptável por meio dos protocolos HLS ou DASH para poder obter o arquivo de manifesto de reprodução e reproduzir o vídeo. |

O Dynamic Media com recursos de OpenAPI também é compatível com vídeos de formulários longos. Os vídeos podem suportar até 50 GB e 2 horas.

Para obter informações sobre as ofertas do Dynamic Media disponíveis e seus recursos, consulte [Dynamic Media Prime e Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).

## Endpoints das APIs de entrega {#delivery-apis-endpoint}

Os endpoints da API variam para cada API de entrega. Por exemplo, o ponto de extremidade da API `Web-optimized binary representation of the asset in the requested output format` é:
`https://delivery-pXXXX-eYYYY.adobeaemcloud.com/adobe/assets/{assetId}/as/{seoName}.{format}`

O domínio de delivery é semelhante em estrutura ao domínio do ambiente do autor do Experience Manager. A única diferença é a substituição do termo `author` por `delivery`.

`pXXXX` refere-se à ID do programa

`eYYYY` refere-se à ID de ambiente

Consulte [detalhes da API](https://adobe-aem-assets-delivery.redoc.ly/#tag/Assets) para obter mais informações.

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

Para invocar as APIs de Entrega, é necessário um token IMS nos detalhes `Authorization` para entregar um ativo restrito. O token IMS é obtido de uma conta técnica. Consulte [Buscar as credenciais do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=pt-BR#fetch-the-aem-as-a-cloud-service-credentials) para criar uma nova conta técnica. Consulte [Gerar o token de acesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=pt-BR#generating-the-access-token) para gerar o token IMS e usá-lo corretamente no cabeçalho da solicitação de APIs de Entrega.


Para exibir amostras de solicitações, amostras de respostas e códigos de resposta, consulte [APIs de entrega](https://adobe-aem-assets-delivery.redoc.ly/#operation/getAssetSeoFormat).
