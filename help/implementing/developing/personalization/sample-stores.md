---
title: Exemplos de candidatos à loja do ContextHub
description: O ContextHub fornece vários candidatos de armazenamento de exemplo que podem ser usados em suas soluções
exl-id: 9493d91e-0b23-4dc4-a014-d8d13687efad
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# Exemplos de candidatos à loja do ContextHub {#sample-contexthub-store-candidates}

O ContextHub fornece vários candidatos de armazenamento de amostra que podem ser usados em suas soluções. Para cada amostra são fornecidas as seguintes informações:

* Onde encontrar o código-fonte para que você possa abri-lo para fins de aprendizado.
* Como configurar as lojas criadas a partir dos candidatos à loja.
* Como os dados de armazenamento são estruturados para que você possa acessá-los.

>[!WARNING]
>
>Os candidatos à loja de amostras são fornecidos como configurações de referência para ajudar você a criar sua própria configuração dedicada para o seu projeto e, como tal, não devem ser usados diretamente.

## aem.segmentation Sample Store Candidato {#aem-segmentation-sample-store-candidate}

Armazenar para segmentos do ContextHub resolvidos e não resolvidos. Recupera automaticamente segmentos do ContextHub SegmentManager.

### Local de origem {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### Implementação base {#base-implementation-segmentation}

O candidato da loja de segmentação do aem estende [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuração {#configuration-segmentation}

Ao criar um `aem.segmentation` , não é necessário fornecer uma configuração detalhada. A configuração padrão especifica o local das definições de segmento do ContextHub.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## candidato a armazenamento de exemplo contexthub.geolocation {#contexthub-geolocation-sample-store-candidate}

O `contexthub.geolocation` O candidato da loja de amostras usa o Google Maps para obter e armazenar informações sobre a localização do cliente.

### Local de origem {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### Implementação base {#base-implementation-geolocation}

O `contexthub.geolocation` estende-se o candidato da loja [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

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
>Uma política de segurança introduzida no Chrome 50.x requer que todas as chamadas relacionadas à geolocalização sejam feitas por uma conexão segura. Portanto, o AEM força o uso de https para chamadas de API de geolocalização, se o AEM também estiver em execução em https. Caso contrário, http é usado para estar em conformidade com a política da mesma origem.
>
>Consulte [esta publicação do blog do Google](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) para obter mais detalhes sobre a alteração no Chrome.

## Candidato à Loja de Amostra do contexthub.surferinfo {#contexthub-surferinfo-sample-store-candidate}

Armazena informações sobre o ambiente cliente atual, como o dispositivo, a janela, o navegador, a data e a hora.

### Local de origem {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### Implementação base {#base-implementation-surferinfo}

O `contexthub.surferinfo` estende-se o candidato da loja [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Configuração {#configuration-surferinfo}

A configuração padrão é herdada de `ContextHub.Store.PersistedStore`.

### Itens de dados {#data-items-surferinfo}

As lojas que usam esse candidato a loja têm uma árvore de dados semelhante ao seguinte exemplo:

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

## Candidato à loja de amostra granite.emulators {#granite-emulators-sample-store-candidate}

O `granite.emulators` O candidato da loja de amostras armazena informações sobre dispositivos clientes.

### Local de origem {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### Implementação base {#base-implementation-emulators}

O `granite.emulators` estende-se o candidato da loja [`ContextHub.Store.PersistedStore`](contexthub-api.md#contexthub-store-persistedstore).

### Configuração {#configuration-emulators}

A configuração padrão inclui uma matriz chamada `defaultEmulators` que contém informações sobre diferentes dispositivos. Ao criar uma loja, forneça perfis de dispositivo diferentes na propriedade Configuração detalhada , conforme necessário, usando o formato ilustrado no exemplo a seguir:

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

A árvore de dados da loja é semelhante ao seguinte exemplo:

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

## Candidato à loja de amostra granite.profile {#granite-profile-sample-store-candidate}

Armazena informações sobre o usuário atual.

### Local de origem {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### Implementação base {#base-implementation-profile}

O `granite.profile` estende-se o candidato da loja [`ContextHub.Store.PersistedJSONPStore`](contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuração {#configuration-profile}

A seguinte configuração padrão é usada. Você não deve alterar essa configuração.

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

As lojas que usam esse candidato a loja têm uma árvore de dados semelhante ao seguinte exemplo:

```javascript
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
