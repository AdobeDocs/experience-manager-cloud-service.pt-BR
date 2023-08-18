---
title: Configuração do Compartilhamento de recursos entre origens (CORS) com o AEM Headless
description: O Compartilhamento de recursos entre origens (CORS) do Adobe Experience Manager permite que aplicativos web headless façam chamadas do lado do cliente para o AEM. Uma configuração do CORS é necessária para habilitar o acesso ao endpoint do GraphQL.
feature: GraphQL API
exl-id: 426be9f9-f44a-4744-ac08-e64bb97308a0
source-git-commit: 316680823fe4bc85e1f4359305047c0d1f517dc7
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 90%

---

# Configuração do Compartilhamento de recursos entre origens (CORS)

>[!CAUTION]
>
>Se [o armazenamento em cache no Dispatcher foi ativado](/help/headless/deployment/dispatcher-caching.md) então, o filtro CORS não é necessário e, portanto, esta seção pode ser ignorada.

>[!NOTE]
>
>Para obter uma visão geral detalhada da política de compartilhamento de recursos do CORS no AEM, consulte [Entenda o CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=pt-BR#understand-cross-origin-resource-sharing-(cors)).

Para acessar o endpoint do GraphQL, uma política do CORS deve ser configurada e adicionada a um projeto do AEM que esteja [implantado no AEM via Cloud Manager](/help/implementing/cloud-manager/deploy-code.md). Isso é feito adicionando um arquivo de configuração de CORS OSGi apropriado para os endpoints desejados. Várias configurações do CORS podem ser criadas e implantadas em diferentes ambientes. Exemplos podem ser encontrados no [site de referência WKND](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)

A configuração do CORS deve especificar uma origem de site confiável `alloworigin` ou `alloworiginregexp`, para a qual o acesso deve ser concedido.

O arquivo de configuração deve ser nomeado como: `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json`, onde `appname` reflete o nome do seu aplicativo.

Por exemplo, para conceder acesso ao endpoint do GraphQL `/content/cq:graphql/wknd/endpoint` e ao endpoint de consultas persistentes para `https://my.domain`, é possível usar:

```json
{
  "supportscredentials":false,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/cq:graphql/wknd/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Se você tiver configurado um caminho personalizado para o endpoint, também poderá usá-lo no `allowedpaths`.
