---
title: Configuração do filtro referenciador com o AEM Headless
description: O Filtro referenciador do Adobe Experience Manager permite o acesso de hosts de terceiros. Uma configuração OSGi para o Filtro referenciador é necessária para habilitar o acesso ao endpoint do GraphQL para aplicativos headless.
feature: GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
source-git-commit: 076cafe3d096fd7f4c808f1b2553a9ba6b6c1833
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 69%

---

# Filtro de referenciador {#referrer-filter}

O Filtro referenciador do Adobe Experience Manager permite o acesso de hosts de terceiros.

Uma configuração OSGi para o Filtro do Referenciador é necessária para habilitar o acesso ao ponto de extremidade do GraphQL para aplicativos sem periféricos no POST HTTP. Ao usar AEM Consultas Persistentes Sem Cabeçalho que acessam AEM por HTTP GET, uma configuração do Filtro do Referenciador não é necessária.

>[!WARNING]
> AEM Filtro de Referenciador não é uma fábrica de configuração OSGi, o que significa que apenas uma configuração está ativa em um serviço de AEM de cada vez. Quando possível, evite adicionar configurações personalizadas de Filtro de referenciador, pois isso substituirá AEM configurações nativas e poderá quebrar a funcionalidade do produto.

Isso é feito adicionando uma configuração OSGi apropriada para o Filtro referenciador que:

* especifica um nome de host de site confiável; `allow.hosts` ou `allow.hosts.regexp`
* concede acesso a esse nome de host.

O nome do arquivo deve ser `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

Por exemplo, para conceder acesso a solicitações com o referenciador `my.domain`, é possível:

```xml
{
    "allow.empty": false,
    "allow.hosts": [
      "my.domain"
    ],
    "allow.hosts.regexp": [
      ""
    ],
    "filter.methods": [
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp": [
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
