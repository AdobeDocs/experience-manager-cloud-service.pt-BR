---
title: Fragmentos de conteúdo e OpenAPIs de modelos de fragmento de conteúdo
description: Saiba mais sobre os Fragmentos de conteúdo e as OpenAPIs dos Modelos de fragmento de conteúdo.
exl-id: 077eed73-a066-4273-b2f5-da4bf5cd900c
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 1fb1201fa976e4c0e3c87f22bd9327a55828efef
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Fragmentos de conteúdo e OpenAPIs de gerenciamento de modelos de fragmento de conteúdo {#content-fragments-and-content-fragment-models-management-openapis}

A implementação modernizada da OpenAPI da API de gerenciamento de fragmento de conteúdo permite que os desenvolvedores executem programaticamente operações de criação, leitura, atualização e exclusão no AEM Author para gerenciar modelos de fragmento de conteúdo e fragmentos de conteúdo armazenados no AEM. Essas APIs são compatíveis com vários casos de uso.

Para obter a documentação completa, consulte [API de gerenciamento de fragmento de conteúdo](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/).

>[!NOTE]
>
>O uso existente da [API HTTP do Assets](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets) para fragmentos de conteúdo deve ser migrado para a nova OpenAPI de gerenciamento de fragmento de conteúdo.

>[!NOTE]
>
>É necessária autorização para acessar a OpenAPI quando você não está conectado ao AEM; por exemplo, quando a OpenAPI é usada de outro produto como parte de uma integração.
>
>Consulte [APIs baseadas em OpenAPI](/help/implementing/developing/open-api-based-apis.md) para obter detalhes sobre como autorizar seu acesso à OpenAPI.

>[!CAUTION]
>
>Por padrão, a OpenAPI de gerenciamento de fragmento de conteúdo é desativada na publicação. Em vez disso, para casos de uso orientados para entrega, recomendamos usar a [API aberta de entrega de fragmento de conteúdo](/help/headless/aem-content-fragment-delivery-with-openapi.md).

>[!NOTE]
>
>Consulte [APIs do AEM para Entrega e Gerenciamento de Conteúdo Estruturado](/help/headless/apis-headless-and-content-fragments.md) para obter uma visão geral das várias APIs disponíveis e uma comparação de alguns dos conceitos envolvidos.