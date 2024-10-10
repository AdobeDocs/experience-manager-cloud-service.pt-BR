---
title: Configuração do filtro referenciador com o AEM Headless
description: O Filtro referenciador do Adobe Experience Manager permite o acesso de hosts de terceiros. Uma configuração OSGi para o Filtro referenciador é necessária para habilitar o acesso ao endpoint do GraphQL para aplicativos headless.
feature: Headless, GraphQL API
exl-id: e2e3d2dc-b839-4811-b5d1-38ed8ec2cc87
solution: Experience Manager
role: Admin, Developer
source-git-commit: 3096436f8057833419249d51cb6c15e6c28e9e13
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 55%

---

# Filtro de referenciador {#referrer-filter}

O Filtro referenciador do Adobe Experience Manager permite o acesso de hosts de terceiros.

Uma configuração OSGi é necessária para o filtro referenciador a fim de habilitar o acesso ao ponto de acesso GraphQL para aplicativos headless por HTTP POST. Ao usar consultas persistentes do AEM Headless que acessam o AEM por HTTP GET, a configuração do filtro referenciador não é necessária.

>[!WARNING]
> O filtro referenciador não é uma fábrica de configurações OSGi, o que significa que apenas uma configuração pode ser ativada em um serviço do AEM de cada vez. Quando possível, evite adicionar configurações personalizadas do filtro referenciador, pois elas substituirão as configurações nativas do AEM e isso poderá prejudicar a funcionalidade do produto.

Isso é feito adicionando uma configuração OSGi apropriada para o Filtro referenciador que:

* especifica um nome de host de site confiável; `allow.hosts` ou `allow.hosts.regexp`
* concede acesso a esse nome de host.

O nome do arquivo deve ser `org.apache.sling.security.impl.ReferrerFilter.cfg.json`.

## Exemplo de configuração {#example-configuration}

Por exemplo, para conceder acesso a solicitações com o referenciador `my.domain`, é possível:

>[!CAUTION]
>
>Este é um exemplo básico que pode substituir a configuração padrão. Você precisa garantir que as atualizações do produto sejam sempre aplicadas a qualquer personalização.

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

## Segurança de dados {#data-security}

>[!CAUTION]
>
>Continua a ser sua responsabilidade abordar totalmente os seguintes pontos.

Para garantir a segurança de seus dados, você deve garantir que:

* o acesso é **somente** concedido a domínios confiáveis

* sintaxe do curinga [`*`] em **não** usada; isso desabilita o acesso autenticado ao ponto de extremidade do GraphQL e também o expõe ao mundo inteiro

* as informações confidenciais são **nunca** expostas; direta ou indiretamente:

   * Por exemplo, todos os [esquemas GraphQL](/help/headless/graphql-api/content-fragments.md#schema-generation) são:

      * derivado de modelos de fragmento de conteúdo que foram **Habilitados**

     **e**

      * são legíveis por meio do endpoint do GraphQL

     Isso significa que as informações presentes como nomes de campo na definição do modelo podem ficar disponíveis.

Você deve garantir que nenhum dado confidencial esteja disponível por qualquer meio, portanto, esses detalhes devem ser cuidadosamente considerados.
