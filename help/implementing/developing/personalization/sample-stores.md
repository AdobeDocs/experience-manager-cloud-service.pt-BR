---
title: Amostra de candidatos da loja do ContextHub
description: O ContextHub fornece vários exemplos de candidatos de armazenamento que você pode usar em suas soluções
exl-id: 9493d91e-0b23-4dc4-a014-d8d13687efad
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# Amostra de candidatos da loja do ContextHub {#sample-contexthub-store-candidates}

O ContextHub fornece vários exemplos de candidatos a armazenamento que você pode usar em suas soluções. As seguintes informações são fornecidas para cada amostra:

* Onde encontrar o código-fonte para poder abri-lo para fins de aprendizado.
* Como configurar as lojas que você cria a partir dos candidatos da loja.
* Como os dados do armazenamento são estruturados para que você possa acessá-los.

>[!WARNING]
>
>Os exemplos de candidatos a armazenamento são fornecidos como configurações de referência para ajudar você a criar sua própria configuração dedicada para o projeto. Não os utilize diretamente.

## Amostra de candidato da loja do aem.segmentation {#aem-segmentation-sample-store-candidate}

Armazene para segmentos do ContextHub resolvidos e não resolvidos. Recupera automaticamente segmentos do ContextHub SegmentManager.

### Localização do Source {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### Implementação base {#base-implementation-segmentation}

O candidato do armazenamento de segmentação aem estende [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuração {#configuration-segmentation}

Ao criar um armazenamento `aem.segmentation`, não é necessário fornecer uma configuração detalhada. A configuração padrão especifica o local das definições de segmento do ContextHub.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## contexthub.geolocation Amostra do candidato da loja {#contexthub-geolocation-sample-store-candidate}

O candidato de armazenamento de amostra `contexthub.geolocation` usa o Google Maps para obter e armazenar informações sobre o local do cliente.

### Localização do Source {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### Implementação base {#base-implementation-geolocation}

O candidato de armazenamento `contexthub.geolocation` estende [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuração {#configuration-geolocation}

A configuração padrão especifica informações sobre o serviço Google e as coordenadas iniciais de latitude e longitude.

```javascript
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### Itens de dados {#data-items-geolocation}

O armazenamento usa uma árvore de dados semelhante ao seguinte exemplo:

```javascript
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Uma política de segurança introduzida no Chrome 50.x exige que todas as chamadas relacionadas à geolocalização sejam feitas em uma conexão segura. Portanto, o AEM força o uso de https para chamadas de API de geolocalização se o AEM também estiver em execução em https. Caso contrário, o http será usado para estar em conformidade com a política da mesma origem.
>
>Consulte [esta publicação do blog do Google](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) para obter mais detalhes sobre a alteração no Chrome.

## contexthub.surferinfo Candidato da loja de amostra {#contexthub-surferinfo-sample-store-candidate}

Armazena informações sobre o ambiente atual do cliente, como o dispositivo, a janela, o navegador, a data e a hora.

### Localização do Source {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### Implementação base {#base-implementation-surferinfo}

O candidato de armazenamento `contexthub.surferinfo` estende [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Configuração {#configuration-surferinfo}

A configuração padrão é herdada de `ContextHub.Store.PersistedStore`.

### Itens de dados {#data-items-surferinfo}

Os armazenamentos que usam esse candidato a armazenamento têm uma árvore de dados semelhante ao seguinte exemplo:

```javascript
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## exemplo de candidato a armazenamento de granite.emulators {#granite-emulators-sample-store-candidate}

O candidato de armazenamento de amostra `granite.emulators` armazena informações sobre dispositivos cliente.

### Localização do Source {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### Implementação base {#base-implementation-emulators}

O candidato de armazenamento `granite.emulators` estende [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Configuração {#configuration-emulators}

A configuração padrão inclui uma matriz chamada `defaultEmulators` que contém informações sobre diferentes dispositivos. Ao criar uma loja, forneça diferentes perfis de dispositivo na propriedade Detail Configuration, conforme necessário, usando o formato ilustrado no exemplo a seguir:

```javascript
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### Itens de dados {#data-items-emulators}

A árvore de dados do armazenamento é semelhante ao seguinte exemplo:

```javascript
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## granite.profile Amostra de candidato da loja {#granite-profile-sample-store-candidate}

Armazena informações sobre o usuário atual.

### Localização do Source {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### Implementação base {#base-implementation-profile}

O candidato de armazenamento `granite.profile` estende [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuração {#configuration-profile}

A configuração padrão a seguir é usada. Você não deve alterar essa configuração.

```javascript
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### Itens de dados {#data-items-profile}

Os armazenamentos que usam esse candidato a armazenamento têm uma árvore de dados semelhante ao seguinte exemplo:

```javascript
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
