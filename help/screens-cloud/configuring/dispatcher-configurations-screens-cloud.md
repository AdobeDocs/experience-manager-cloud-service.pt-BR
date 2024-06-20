---
title: Configurações do Dispatcher no Screens as a Cloud Service
description: Esta página descreve as Configurações do Dispatcher no Screens as a Cloud Service.
exl-id: cc04b480-9310-4975-a7c2-20682c567fa4
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Configurações do Dispatcher no Screens as a Cloud Service {#dispatcher-configurations-screens-cloud}

Esta seção descreve as configurações do dispatcher para o Screens as a Cloud Service.

## Adição de filtros e regras de cache na implantação as a Cloud Service do Dispatcher for Screens {#deployment}

Permita os seguintes filtros e regras de cache nos dispatchers para as instâncias de publicação no Screens as a Cloud Service.

### Filtros do AEM Screens {#filters}

```
## # Content Configurations
/0200 { /type "allow" /method '(GET|HEAD)' /url "/content/screens/*" }
#/0201 { /type "allow" /method '(GET|HEAD)' /url "/content/experience-fragments/*" } ## uncomment this, if you are using experience-fragments
## add any other formats required for your project here
/0202 { /type "allow" /extension '(css|eot|gif|ico|jpeg|jpg|js|gif|pdf|png|svg|swf|ttf|woff|woff2|html|mp4|mov|m4v)' /path "/content/dam/*" }
/0203 { /type "allow" /method 'GET' /url "/screens/channels.json" }
## # Enable clientlibs proxy servlet
/0210 { /type "allow" /method "GET" /url "/etc.clientlibs/*" }
```

### Regras de cache {#cache-rules}

* Adicionar `/statfileslevel "10"` para `/cache` seção em `publish_farm.any`/.

  >[!NOTE]
  >Essa regra de cache aceita o armazenamento em cache de até 10 níveis do docroot do cache e invalida quando o conteúdo é publicado, em vez de invalidar tudo. Você pode alterar esse nível com base na profundidade da configuração da estrutura de conteúdo.

* Adicione o seguinte a `/invalidate` seção em `publish_farm.any`.

  ```
  /0003 {
      /glob "*.json"
      /type "allow"
  }
  ```

* Adicione as seguintes regras a `/rules` seção em `/cache` em publish_farm.any ou em um arquivo incluído de `publish_farm.any`.

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
