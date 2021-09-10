---
title: Configurações do Dispatcher no Screens como um Cloud Service
description: Esta página descreve as configurações do Dispatcher no Screens como um Cloud Service.
source-git-commit: f7a201ed72011df2ed603528ad80cf191c9f2d77
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Configurações do Dispatcher no Screens como um Cloud Service{#dispatcher-configurations-screens-cloud}

Esta seção descreve as configurações do dispatcher para Screens como um Cloud Service.

## Configurações do Dispatcher para a implantação do Screens as a Cloud Service {#deployment}

Permita os seguintes filtros e regras de cache nos dispatchers para as instâncias de publicação no Screens as a Cloud Service.

### Filtros do AEM Screens {#filters}

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you're using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

### Regras de cache {#cache-rules}

* Adicione `/statfileslevel "10"` à seção `/cache` em `publish_farm.any`/.

   >[!NOTE]
   >Essa regra de cache oferece suporte ao armazenamento em cache de até 10 níveis a partir do ponto de cache e invalida quando o conteúdo é publicado, em vez de invalidar tudo. Você pode alterar esse nível com base no quão profundo sua estrutura de conteúdo está configurada.

* Adicione o seguinte à seção `/invalidate` em `publish_farm.any`.

   ```
   /0003 {
       /glob "*.json"
       /type "allow"
   }
   ```

* Adicione as seguintes regras à seção `/rules` em `/cache` em publish_farm.any ou em um arquivo incluído de `publish_farm.any`.

   ```
   ## Allow Dispatcher Cache for Screens channels
    /0002
        {
        /glob "/content/screens/*.html"
        /type "allow"
        }
   
   ## Allow Dispatcher Cache for Screens offline manifests
   
   /0003
       {
       /glob "/content/screens/*.manifest.json"
       /type "allow"
       }
   
   ## Allow Dispatcher Cache for Assets
   /0004
       {
       /glob "/content/dam/*"
       /type "allow"
       }
   
   ## Deny Screens Channels json
   /0005
       {
       /glob "/screens/channels.json"
       /type "deny"
       }
   ```
