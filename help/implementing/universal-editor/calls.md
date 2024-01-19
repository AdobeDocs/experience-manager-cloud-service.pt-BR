---
title: Chamadas do editor universal
description: Saiba mais sobre os diferentes tipos de chamadas feitas ao seu aplicativo pelo Editor universal para ajudá-lo a depurar.
exl-id: 00d66e59-e445-4b5c-a5b1-c0a9f032ebd9
source-git-commit: 7ef3efa6e074778b7b3e3a8159056200b2663b30
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---


# Chamadas do editor universal {#calls}

Saiba mais sobre os diferentes tipos de chamadas feitas ao seu aplicativo pelo Editor universal para ajudá-lo a depurar.

{{universal-editor-status}}

## Visão geral {#overview}

O Editor universal se comunica com seu aplicativo instrumentado por meio de uma série de chamadas definidas. Isso é transparente e não afeta a experiência do usuário final.

No entanto, para o desenvolvedor, entender essas chamadas e o que elas fazem pode ser útil ao depurar seu aplicativo ao usar o Universal Editor. Se você tiver instrumentado seu aplicativo e ele não estiver se comportando conforme o esperado, pode ser útil abrir o **Rede** das ferramentas do desenvolvedor no seu navegador e inspecione as chamadas ao editar o conteúdo no seu aplicativo.

![Exemplo de chamada de detalhes na guia Rede das ferramentas de desenvolvedor do navegador](assets/calls-network-tab.png)

* A variável **Carga** da chamada contém detalhes do que está sendo atualizado pelo editor, incluindo a identificação do que deve ser atualizado e como atualizá-lo.
* A variável **Resposta** inclui detalhes do que exatamente foi atualizado pelo serviço do editor. Isso facilita a atualização do conteúdo no editor. Em certos casos, como `move` chamada, a página inteira deve ser atualizada.

Veja a seguir uma lista dos tipos de chamadas que o Editor universal faz para o seu aplicativo, juntamente com amostras de cargas e respostas.

## Atualizar o {#update}

Um `update` A chamada de ocorre ao editar o conteúdo no aplicativo usando o Editor universal. A variável `update` mantém as alterações.

Sua carga útil inclui detalhes sobre o que gravar no JCR.

* `resource`: o caminho JCR a ser atualizado
* `prop`: a propriedade do JCR que está sendo atualizada
* `type`: o tipo de valor JCR da propriedade que está sendo atualizada
* `value`: Os dados atualizados

### Carga de exemplo {#update-payload}

```json
{
  "connections": [
    {
      "name": "aem",
      "protocol": "aem",
      "uri": "https://localhost:8443"
    }
  ],
  "target": {
    "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "type": "text",
    "prop": "jcr:title"
  },
  "value": "Tiny Toon Adventures"
}
```

### Exemplo de resposta {#update-response}

```json
{
  "updates": [
    {
      "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
      "prop": "jcr:title",
      "type": "text"
    }
  ]
}
```

## Detalhes {#details}

A `details` A chamada ocorre ao carregar o aplicativo no Editor universal para recuperar o conteúdo do aplicativo.

Sua carga inclui os dados a serem renderizados, bem como detalhes do que os dados representam (o esquema) para que possam ser renderizados no Editor universal.

* Para um componente, o Editor universal recupera apenas um `data` objeto, já que o schema dos dados é definido no aplicativo.
* Para Fragmentos de conteúdo, o Editor universal também recupera uma `schema` desde que o Modelo de fragmento de conteúdo seja definido no JCR.

### Carga de exemplo {#details-payload}

```json
{
  "connections": [
    {
      "name": "aem",
      "protocol": "aem",
      "uri": "https://localhost:8443"
    }
  ],
  "target": {
    "resource": "urn:aem:/content/wknd/language-masters/en/jcr:content/root/container/carousel/item_1571954853062",
    "type": "component",
    "prop": ""
  }
}
```

### Exemplo de resposta {#details-response}

```json
{
  "data": {
    "jcr:primaryType": "nt:unstructured",
    "jcr:title": "Tiny Toon Adventures",
    "fileReference": "/content/dam/wknd-shared/en/adventures/riverside-camping-australia/adobestock-216674449.jpeg",
    "cq:panelTitle": "WKND Adventures",
    "actionsEnabled": "true",
    "jcr:lastModifiedBy": "admin",
    "titleFromPage": "false",
    "jcr:description": "<p>With WKND Adventures, you don't just see the world you experinece it.</p>\r\n",
    "jcr:lastModified": "Fri Jan 19 2024 11:05:59 GMT+0100",
    "descriptionFromPage": "true",
    "sling:resourceType": "wknd/components/teaser",
    "textIsRich": "true",
    "cq:styleIds": [
      "1555543212672"
    ],
    "actions": {
      "jcr:primaryType": "nt:unstructured",
      "item0": {
        "jcr:primaryType": "nt:unstructured",
        "link": "/content/wknd/language-masters/en/adventures",
        "text": "View Trips"
      }
    }
  }
}
```

## Adicionar {#add}

Um `add` A chamada de ocorre quando você coloca um novo componente no aplicativo usando o Editor universal.

Sua carga inclui uma `path` objeto que contém onde o conteúdo deve ser adicionado.

Inclui igualmente uma `content` objeto com objetos adicionais para detalhes específicos do endpoint do conteúdo a ser armazenado [para cada plug-in.](/help/implementing/universal-editor/architecture.md) Por exemplo, se seu aplicativo tem como base o conteúdo do AEM e do Magento, a carga útil conteria um objeto de dados para cada sistema.

### Carga de exemplo {#add-payload}

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "target": {
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
    }
  },
  "content": {
    "name": "text",
    "aem": {
      "page": {
        "resourceType": "wknd/components/text",
        "template": {
          "text": "Default Text"
        }
      }
    }
  }
}
```

### Exemplo de resposta {#add-response}

```json
{
  "updates": [
    {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container"
    }
  ],
  "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1138559521"
}
```

## Mover {#move}

A `move` A chamada de ocorre quando você move um componente no aplicativo usando o Editor universal.

Sua carga inclui uma `from` objeto que define onde o componente estava e um `to` objeto que define para onde foi movido.

### Carga de exemplo {#move-payload}

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "from": {
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
    },
    "component": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_275525847",
      "type": "media",
      "prop": "fileReference"
    }
  },
  "to": {
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
    }
  }
}
```

### Exemplo de resposta {#move-response}

```json
{
  "updates": [
    {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container"
    }
  ]
}
```

## Remover {#remove}

A `remove` A chamada de ocorre quando você exclui um componente no aplicativo usando o Editor universal.

Sua carga inclui o caminho do objeto que é removido.

### Carga de exemplo {#remove-payload}

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "target": {
    "component": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_593170193",
      "type": "text",
      "prop": "text"
    },
    "container": {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "type": "container",
      "prop": ""
    }
  }
}
```

### Exemplo de resposta {#remove-response}

```json
{
  "updates": [
    {
      "resource": "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
      "prop": "",
      "type": "container"
    }
  ]
}
```

## Publicação {#publish}

A `publish` a chamada ocorre ao clicar no botão **Publish** no Editor Universal para publicar o conteúdo editado.

O Universal Editor repete o conteúdo e gera uma lista de referências que também devem ser publicadas.

### Carga de exemplo {#publish-payload}

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-pXXXX-eYYYYY.adobeaemcloud.com"
    }
  ],
  "references": [
    "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/bali-surf-camp/bali-surf-camp/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/climbing-new-zealand/climbing-new-zealand/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/cycling-southern-utah/cycling-southern-utah/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/cycling-tuscany/cycling-tuscany/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/downhill-skiing-wyoming/downhill-skiing-wyoming/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/napa-wine-tasting/napa-wine-tasting/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/riverside-camping-australia/riverside-camping-australia/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/ski-touring-mont-blanc/ski-touring-mont-blanc/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/surf-camp-in-costa-rica/surf-camp-costa-rica/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/tahoe-skiing/tahoe-skiing/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/west-coast-cycling/west-coast-cycling/jcr:content/data/master",
    "urn:aemconnection:/content/dam/wknd-shared/en/adventures/yosemite-backpacking/yosemite-backpacking/jcr:content/data/master",
    "urn:aemconnection:/content/wknd/us/en/newsletter/jcr:content/root/container/title",
    "urn:aemconnection:/content/wknd/us/en/newsletter/jcr:content/root/container/text",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/title",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_229050934",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_2123678383",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1668104604",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/text_1138559521",
    "urn:aemconnection:/content/wknd/language-masters/en/universal-editor-container/jcr:content/root/container/image_275525847"
  ]
}
```

### Exemplo de resposta {#publish-response}

```json
{
  "publishes": [
    "/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway",
    "/content/dam/wknd-shared/en/adventures/bali-surf-camp/bali-surf-camp",
    "/content/dam/wknd-shared/en/adventures/climbing-new-zealand/climbing-new-zealand",
    "/content/dam/wknd-shared/en/adventures/cycling-southern-utah/cycling-southern-utah",
    "/content/dam/wknd-shared/en/adventures/cycling-tuscany/cycling-tuscany",
    "/content/dam/wknd-shared/en/adventures/downhill-skiing-wyoming/downhill-skiing-wyoming",
    "/content/dam/wknd-shared/en/adventures/napa-wine-tasting/napa-wine-tasting",
    "/content/dam/wknd-shared/en/adventures/riverside-camping-australia/riverside-camping-australia",
    "/content/dam/wknd-shared/en/adventures/ski-touring-mont-blanc/ski-touring-mont-blanc",
    "/content/dam/wknd-shared/en/adventures/surf-camp-in-costa-rica/surf-camp-costa-rica",
    "/content/dam/wknd-shared/en/adventures/tahoe-skiing/tahoe-skiing",
    "/content/dam/wknd-shared/en/adventures/west-coast-cycling/west-coast-cycling",
    "/content/dam/wknd-shared/en/adventures/yosemite-backpacking/yosemite-backpacking",
    "/content/wknd/us/en/newsletter",
    "/content/wknd/language-masters/en/universal-editor-container"
  ]
}
```
