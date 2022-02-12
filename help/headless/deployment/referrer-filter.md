---
title: Configuração do filtro referenciador com AEM headless
description: O Filtro de referenciador da Adobe Experience Manager permite o acesso de hosts de terceiros. Uma configuração OSGi para o Filtro de referência é necessária para habilitar o acesso ao ponto de extremidade GraphQL para aplicativos sem periféricos.
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# Filtro referenciador {#referrer-filter}

O Filtro de referenciador da Adobe Experience Manager permite o acesso de hosts de terceiros. Uma configuração OSGi para o Filtro de referência é necessária para habilitar o acesso ao ponto de extremidade GraphQL para aplicativos sem periféricos.

Isso é feito adicionando uma configuração OSGi apropriada para o Filtro do referenciador que:

* especifica um nome de host de site confiável; ou `allow.hosts` ou `allow.hosts.regexp`,
* concede acesso a esse nome de host.

O nome do arquivo deve ser `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

Por exemplo, para conceder acesso a solicitações com o Referenciador `my.domain` é possível:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Continua a ser responsabilidade do cliente:
>
>* conceder acesso somente a domínios confiáveis
>* certifique-se de que nenhuma informação sensível seja exposta
>* não usar curinga [*] sintaxe; isso desativará o acesso autenticado ao ponto de extremidade GraphQL e também o exporá ao mundo inteiro.


>[!CAUTION]
>
>Toda a GraphQL [esquemas](#schema-generation) (derivado de Modelos de fragmentos do conteúdo que foram **Ativado**) são legíveis por meio do ponto de extremidade GraphQL.
>
>Isso significa que você precisa garantir que não haja dados confidenciais disponíveis, pois eles poderiam ser vazados dessa forma; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.
