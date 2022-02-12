---
title: Configuração do CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens) com AEM Headless
description: O CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos de várias origens) da Adobe Experience Manager permite que aplicativos Web sem periféricos façam chamadas do lado do cliente para AEM. Uma configuração do CORS é necessária para habilitar o acesso ao ponto de extremidade GraphQL.
feature: GraphQL API
source-git-commit: 0cc131209f497241949f8da6e8144dfcaffe7e6e
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Configuração do CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens)

>[!NOTE]
>
>Para obter uma visão geral detalhada da política de compartilhamento de recursos do CORS no AEM consulte [Entenda o CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html#understand-cross-origin-resource-sharing-(cors)).

Para acessar o ponto de extremidade GraphQL, uma política CORS deve ser configurada e adicionada a um Projeto AEM que esteja [implantado no AEM via Cloud Manager](/help/implementing/cloud-manager/deploy-code.md). Isso é feito adicionando um arquivo de configuração de CORS OSGi apropriado para os endpoints desejados. Várias configurações do CORS podem ser criadas e implantadas em diferentes ambientes. Os exemplos podem ser encontrados no [Site de referência WKND](https://github.com/adobe/aem-guides-wknd/tree/master/ui.config/src/main/content/jcr_root/apps/wknd/osgiconfig)

A configuração do CORS deve especificar uma origem de site confiável `alloworigin` ou `alloworiginregexp` cujo acesso deve ser concedido.

O arquivo de configuração deve ser nomeado como: `com.adobe.granite.cors.impl.CORSPolicyImpl~appname-graphql.cfg.json` em que `appname` O reflete o nome do seu aplicativo.

Por exemplo, para conceder acesso ao ponto de extremidade GraphQL `/content/cq:graphql/wknd/endpoint` e o endpoint de consultas persistentes para `https://my.domain` você pode usar:

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

Se você tiver configurado um caminho personalizado para o endpoint, também poderá usá-lo em `allowedpaths`.


