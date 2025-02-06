---
title: Como atualizar seu conteúdo por meio das APIs do AEM Assets
description: Nesta parte da jornada do desenvolvedor headless do AEM, saiba como usar a API REST para acessar e atualizar o conteúdo dos seus fragmentos de conteúdo.
exl-id: 84120856-fd1d-40f7-8df4-73d4cdfcc43b
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 84%

---

# Como atualizar seu conteúdo por meio das APIs do AEM Assets {#update-your-content}

Nesta parte da [Jornada de desenvolvedores sem periféricos do AEM](overview.md), saiba como usar a API REST para acessar e atualizar o conteúdo dos fragmentos de conteúdo.

## A história até agora {#story-so-far}

No documento anterior da jornada headless do AEM, [Como acessar seu conteúdo por meio das APIs de entrega do AEM](access-your-content.md), você aprendeu a acessar o conteúdo headless no AEM por meio da API GraphQL do AEM; agora você deve:

* Ter um alto nível de compreensão sobre GraphQL.
* Entender como a API GraphQL do AEM funciona.
* Conhecer alguns exemplos de consultas práticas.

Este artigo se baseia nesses fundamentos para que você entenda como atualizar o seu conteúdo headless existente no AEM por meio da API REST.

## Objetivo {#objective}

* **Público-alvo**: avançado
* **Objetivo**: aprender a usar a API REST para acessar e atualizar o conteúdo dos seus fragmentos de conteúdo:
   * Introdução à API HTTP do AEM Assets.
   * Apresentação e discussão sobre o suporte de fragmento de conteúdo da API.
   * Ilustração de detalhes da API.

<!--
  * Look at sample code to see how things work in practice.
-->

## Por que você precisa da API HTTP de ativos para fragmentos de conteúdo {#why-http-api}

No estágio anterior da jornada headless, você aprendeu como usar a API GraphQL do AEM para recuperar o conteúdo usando consultas.

Então, por que é necessária outra API?

A API HTTP do Assets permite **Ler** o seu conteúdo, mas também permite **Criar**, **Atualizar** e **Excluir** conteúdo - ações que não são possíveis com a API do GraphQL.

A API REST de ativos está disponível em cada instalação pronta para uso de versões recentes do Adobe Experience Manager as a Cloud Service.

## API HTTP de ativos {#assets-http-api}

A API HTTP de ativos abrange:

* API REST de ativos
* incluindo suporte para fragmentos de conteúdo

A implementação atual da API HTTP de ativos é baseada no estilo de arquitetura **REST** e permite que você acesse o conteúdo (armazenado no AEM) por meio de operações **CRUD** (criar, ler, atualizar, excluir).

Com essas operações, a API permite operar o Adobe Experience Manager as a Cloud Service como um CMS (Content Management System) headless, fornecendo Serviços de conteúdo a um aplicativo front-end do JavaScript. Ou qualquer outro aplicativo que possa executar solicitações HTTP e manipular respostas JSON. Por exemplo, aplicativos de página única (SPA) baseados em estrutura ou personalizados exigem conteúdo fornecido por meio de uma API, geralmente no formato JSON.

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter must be configured correctly.

>[!NOTE]
>
>For more information, see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For more information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (that is, folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example, its name, title, and so on Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## API HTTP de ativos e fragmentos de conteúdo {#assets-http-api-content-fragments}

Os fragmentos de conteúdo são usados para entrega headless e são um tipo especial de ativo. Eles são usados para acessar dados estruturados, como textos, números, datas, entre outros.

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, that is, the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore, the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, and so on, are part of the definition.

To create a content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## Uso da API REST de ativos {#using-aem-assets-rest-api}

### Acesso {#access}

A API REST de ativos usa o ponto de acesso `/api/assets` e necessita do caminho do ativo para acessá-lo (sem o `/content/dam` inicial).

* Isso significa que para acessar o ativo em:
   * `/content/dam/path/to/asset`
* Você precisa solicitar:
   * `/api/assets/path/to/asset`

Por exemplo, para acessar `/content/dam/wknd/en/adventures/cycling-tuscany`, solicite `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>O acesso por:
>
>* `/api/assets` **não** precisa da utilização do seletor `.model`.
>* `/content/path/to/page` **precisa** da utilização do seletor `.model`.

### Operação {#operation}

O método HTTP determina a operação a ser executada:

* **GET**: para recuperar uma representação JSON de um ativo ou uma pasta
* **POST**: para criar novos ativos ou pastas
* **PUT**: para atualizar as propriedades de um ativo ou pasta
* **DELETE**: para excluir um ativo ou pasta

>[!NOTE]
>
>O corpo da solicitação e/ou os parâmetros de URL podem ser usados para configurar algumas dessas operações; por exemplo, definir que uma pasta ou um ativo deve ser criado por uma solicitação **POST**.

O formato exato das solicitações compatíveis é definido na documentação de Referência da API.

O uso pode ser diferente dependendo se você está usando um ambiente de autor ou de publicação no AEM, juntamente com seu caso de uso específico.

* É altamente recomendável que a criação seja vinculada a uma instância de autor (e atualmente não há meios de replicar um fragmento para publicação usando essa API).
* A entrega é possível de ambos os ambientes, pois o AEM apresenta o conteúdo solicitado somente no formato JSON.

   * Armazenar e entregar a partir de uma instância de autor do AEM deve ser o suficiente para aplicativos de biblioteca de mídia por trás do firewall.

   * Para entrega em tempo real na web, recomenda-se uma instância de publicação do AEM.

>[!CAUTION]
>
>A configuração do Dispatcher em instâncias na nuvem do AEM pode bloquear o acesso ao `/api`.

>[!NOTE]
>
>Consulte a Referência da API [API do Adobe Experience Manager Assets - Fragmentos de conteúdo](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html).
>
>As [OpenAPIs](/help/headless/content-fragment-openapis.md) de Fragmento de Conteúdo e de Modelo de Fragmento de Conteúdo também estão disponíveis.

### Leitura/entrega {#read-delivery}

O uso é feito via:

`GET /{cfParentPath}/{cfName}.json`

Por exemplo:

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

A resposta é em JSON serializado e o conteúdo é estruturado de acordo com o fragmento de conteúdo. As referências são fornecidas como URLs de referência.

Dois tipos de operações de leitura são possíveis:

* Ao ler um fragmento de conteúdo específico por caminho, a representação JSON do fragmento de conteúdo é retornada.
* Leitura de uma pasta de fragmentos de conteúdo por caminho: retorna as representações JSON de todos os fragmentos de conteúdo contidos na pasta.

### Criar {#create}

O uso é feito via:

`POST /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON do fragmento de conteúdo a ser criado, incluindo qualquer conteúdo inicial que deve ser definido nos elementos do fragmento de conteúdo. É obrigatório definir a propriedade `cq:model` e ela deve apontar para um modelo de fragmento de conteúdo válido. Se isso não for feito, haverá um erro. Também é necessário adicionar um cabeçalho `Content-Type` definido como `application/json`.

### Atualizar o {#update}

O uso é feito via

`PUT /{cfParentPath}/{cfName}`

O corpo deve conter uma representação JSON referente ao que deve ser atualizado para o fragmento de conteúdo especificado.

Isso pode ser simplesmente o título ou a descrição de um fragmento de conteúdo, um único elemento ou todos os valores e/ou metadados do elemento.

### Excluir {#delete}

O uso é por meio de:

`DELETE /{cfParentPath}/{cfName}`

Para obter mais detalhes sobre como usar a API REST do AEM Assets, consulte o seguinte:

* API HTTP do Adobe Experience Manager Assets (recursos adicionais)
* Compatibilidade com fragmentos de conteúdo na API HTTP do AEM Assets (recursos adicionais)

## O que vem a seguir {#whats-next}

Agora que concluiu esta parte da jornada de desenvolvedores headless do AEM, você deve:

* Entender as noções básicas sobre a API HTTP do AEM Assets.
* Entender como os fragmentos de conteúdo são compatíveis com essa API.

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page is not going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

Você deve continuar a jornada headless do AEM revisando o documento [Como unir os conceitos: aplicativo e conteúdo no AEM headless](put-it-all-together.md), onde você se familiarizará com as noções básicas e as ferramentas da arquitetura do AEM necessárias para unir seu aplicativo.

## Recursos adicionais {#additional-resources}

* [APIs do Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/)
* [API HTTP de ativos](/help/assets/mac-api-assets.md)
* [API REST de fragmentos de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [Referência da API ](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [API do Adobe Experience Manager Assets - Fragmentos de conteúdo](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)
* [Trabalho com fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)
* [Componentes principais do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)
* [Explicação sobre o CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html?lang=pt-BR)
* [Vídeo - Desenvolvimento do CORS com o AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html?lang=pt-BR)
* [Introdução ao AEM as a Headless CMS](/help/headless/introduction.md)
* [Portal do desenvolvedor do AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)
* [Tutorials para Headless no AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR)
* As [OpenAPIs](/help/headless/content-fragment-openapis.md) de Fragmento de Conteúdo e de Modelo de Fragmento de Conteúdo também estão disponíveis.
