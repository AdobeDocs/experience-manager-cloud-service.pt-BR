---
title: APIs REST
description: O Screens as a Cloud Service fornece uma API RESTful simples que segue a especificação do Siren. Siga esta página para saber como navegar na estrutura de conteúdo e enviar comandos para dispositivos no ambiente.
exl-id: 2c52583f-0dd9-4fa3-880b-7671442989ae
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 2%

---

# APIs REST {#rest-apis}

O AEM Screens fornece uma API RESTful simples que segue o [Sirene](https://github.com/kevinswiber/siren) especificação. Ele permite navegar pela estrutura do conteúdo e enviar comandos para dispositivos no ambiente.

A API pode ser acessada em [*http://localhost:4502/api/screens.json*](http://localhost:4502/api/screens.json).

## Navegar pela estrutura do conteúdo {#navigating-content-structure}

O JSON retornado pelas chamadas de API lista as entidades relacionadas ao recurso atual. Após o link próprio listado, cada uma dessas entidades é novamente acessível como um recurso REST.

Por exemplo, para acessar as exibições em nosso local principal de demonstração, você pode chamar:

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship.json HTTP/1.1
Host: http://localhost:4502
```

Ou usando curl:

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json
```

O resultado seria semelhante a:

```xml
{
  "class": [
    "aem-io/screens/location"
  ],
  "links": [
    {
      "rel": [
        "self"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json"
    },
    {
      "rel": [
        "parent"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo.json"
    }
  ],
  "properties": {…},
  "entities": [
    {
      "class": [
        "aem-io/screens/display"
      ],
      "links": [
        {
          "rel": [
            "self"
          ],
          "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json"
        }
      ],
      "rel": [
        "child"
      ],
      "properties": {
        "title": "Single Screen Display",
        "height": 1440,
        "description": "Demo location of a single screen display.",
        "name": "single",
        "width": 2560,
        "idletimeout": 300,
        "layoutrows": 1,
        "layoutcols": 1
      }
    },
    …
  ]
}
```

E, para acessar a Exibição de tela única, você pode chamar:

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

## Execução de ações no recurso {#executing-actions-on-the-resource}

O JSON retornado pelas chamadas de API pode conter uma lista de ações que estão disponíveis no recurso.

A exibição, por exemplo, lista um *broadcast-command* ação que permite enviar um comando para todos os dispositivos atribuídos a essa exibição.

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

Ou usando curl:

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```

***Resultado:***

```xml
{
  "class": [
    "aem-io/screens/display"
  ],
  "links": […],
  "properties": {…},
  "entities": […],
  "actions": [
    {
      "title": "",
      "name": "broadcast-command",
      "method": "POST",
      "href": "/api/screens/content/screens/we-retail/locations/demo/flagship/single",
      "fields": [
        {
          "name": ":operation",
          "value": "broadcast-command",
          "type": "hidden"
        },
        {
          "name": "msg",
          "type": "text"
        }
      ]
    }
  ]
}
```

Para acionar essa ação, é necessário chamar:

```xml
POST /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502

:operation=broadcast-command&msg=reboot
```

Ou usando curl:

```xml
curl -u admin:admin -X POST -d ':operation=broadcast-command&msg=reboot' http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```
