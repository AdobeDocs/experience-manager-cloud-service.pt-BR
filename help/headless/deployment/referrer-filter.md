---
title: Configuração do filtro referenciador com o AEM Headless
description: O Filtro referenciador do Adobe Experience Manager permite o acesso de hosts de terceiros. Uma configuração OSGi para o Filtro referenciador é necessária para habilitar o acesso ao endpoint do GraphQL para aplicativos headless.
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: ht
source-wordcount: '212'
ht-degree: 100%

---


# Filtro de referenciador {#referrer-filter}

O Filtro referenciador do Adobe Experience Manager permite o acesso de hosts de terceiros. Uma configuração OSGi para o Filtro referenciador é necessária para habilitar o acesso ao endpoint do GraphQL para aplicativos headless.

Isso é feito adicionando uma configuração OSGi apropriada para o Filtro referenciador que:

* especifica um nome de host de site confiável; `allow.hosts` ou `allow.hosts.regexp`
* concede acesso a esse nome de host.

O nome do arquivo deve ser `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

Por exemplo, para conceder acesso a solicitações com o referenciador `my.domain`, é possível:

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
>* certificar-se de que nenhuma informação sensível seja exposta
>* não usar uma sintaxe [*] curinga; isso desativará o acesso autenticado ao endpoint do GraphQL e também irá expô-lo ao mundo inteiro.


>[!CAUTION]
>
>Toda os [esquemas](#schema-generation) de GraphQL (derivados de modelos de fragmento de conteúdo que foram **Habilitados**) são legíveis por meio do endpoint do GraphQL.
>
>Isso significa que você precisa garantir que não haja dados confidenciais disponíveis, pois eles poderiam ser vazados dessa maneira; por exemplo, isso inclui informações que podem estar presentes como nomes de campo na definição do modelo.
