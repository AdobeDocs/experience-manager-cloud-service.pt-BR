---
title: Materiais de referência de API
description: AEM possui APIs extensas e poderosas que você pode usar em seu projeto de experiência digitais.
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
feature: Developing
role: Admin, Architect, Developer
source-git-commit: d9db32110e1e0aaa5bdc20bd6b4bff6da6a3a3a3
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 4%

---

# Materiais de referência de API {#api-reference-materials}

O Adobe Experience Manager (AEM) fornece muitas APIs para desenvolver aplicativos e estender o AEM. O AEM foi criado com base em várias tecnologias de código aberto, que também podem ser usadas.

## APIs principais do AEM {#core-aem-apis}

As APIs a seguir são fundamentais para o AEM.

| API | Descrição |
|---|---|
| [Adobe Experience Manager como Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Abstrações de produto, como páginas, ativos, fluxos de trabalho e assim por diante. |
| [Interface do usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Pilha da Web aberta da Adobe, fornecendo vários componentes essenciais (os materiais do Granite 6.5 se aplicam ao AEMaaCS) |
| [Interface do Coral](https://opensource.adobe.com/coral-spectrum/documentation/) | Estilo visual da Adobe Systems para interfaces nuvem, projetadas para fornecer consistência nos experiência do usuário |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

>[!NOTE]
>
>Para obter as informações mais recentes sobre APIs Experience Manager, também visita [Adobe Experience Manager como APIs](https://developer.adobe.com/experience-cloud/experience-manager-apis/) Cloud Service.

## Estruturas adicionais {#additional-apis}

AEM depende de várias APIs adicionais de código aberto.

| API | Descrição |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | Estrutura da Web que usa um Java Content Repository (JCR) para armazenar e gerenciar conteúdo |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Implementação de um Java Content Repository (JCR) hierárquico escalável e de alto desempenho para uso como base de sites da Web modernos de classe mundial |
| [Repositório de conteúdo Java](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | Especificação para o JCR versão 2.0 |
| [Apache Felix](https://felix.apache.org) | Implementação da estrutura da iniciativa Open Services Gateway (OSGi) e da plataforma de serviços |

## Diretrizes de preferência de API {#guidelines}

O AEM é construído nos quatro conjuntos principais de APIs Java a seguir, em ordem decrescente de preferência.

| Prioridade | API | Descrição |
|---|---|---|
| 1 | [Adobe Experience Manager como Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Abstraçãos de produto como páginas, ativos, workflows etc. |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST e abstrações baseadas em recursos, como recursos, mapas de valores e solicitações HTTP. |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Dados e abstrações de conteúdo, como nó, propriedades e sessões. |
| 4 | [Apache Felix](https://felix.apache.org/) | Abstrações do contêiner de aplicativo OSGi, como serviços e componentes (OSGi). |

Se uma API for fornecida pelo AEM, prefira-a ao Sling, JCR e OSGi. Se o AEM não fornecer uma API, prefira Sling a JCR e OSGi.

>[!TIP]
>
>Para obter detalhes sobre essas diretrizes, consulte o documento [Entender as práticas recomendadas da API Java](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html?lang=pt-BR).

## Serviços e APIs de entrega e gerenciamento de conteúdo da AEM {#delivery-apis}

O AEM oferece componentes personalizáveis e opções de entrega de conteúdo.

| Destaque | Descrição |
|---|---|
| [Os Componentes Principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) | Componentes padronizados de Gerenciamento de conteúdo da Web (WCM) para AEM acelerar o tempo de desenvolvimento e reduzir o custo de manutenção dos seus sites |
| [Exportador JSON](/help/implementing/developing/components/json-exporter.md) | Fornecer o conteúdo de qualquer AEM página no formato de modelo de dados JSON |
| [Ativação da exportação em JSON para um componente](/help/implementing/developing/components/enabling-json-exporter.md) | Gerar exportação JSON de conteúdo do componente com base em uma estrutura do modelador |
| [OpenAPIs de Fragmento de Conteúdo e de Modelo de Fragmento de Conteúdo](/help/headless/content-fragment-openapis.md) | OpenAPIs de fragmento de conteúdo e modelo de fragmento de conteúdo |
| [Entrega de fragmento de conteúdo do AEM com OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) | Uma API REST HTTP no AEM Edge Delivery Services, projetada para fornecer conteúdo estruturado de Fragmentos de conteúdo no formato JSON. |
| [API graphQL de fragmento do conteúdo](/help/headless/graphql-api/content-fragments.md) | Habilite a delivery eficiente dos Fragmentos de conteúdo para JavaScript clientes em implementações de CMS sem peramtruto |
|  |  |
| [API Assets](/help/assets/mac-api-assets.md) | Permite operações de criação, leitura, atualização e exclusão (CRUD) em ativos, incluindo binários, metadados, representações e comentários. Consulte API HTTP do AEM Assets |
| [API HTTP de fragmentos de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md) | Acessar conteúdo de fragmento de conteúdo diretamente pela API HTTP por meio de operações CRUD |
| [API HTTP do Assets de fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html?lang=pt-BR) | Formato exato de solicitações de ativos HTTP compatíveis |

>[!NOTE]
>
>Consulte [APIs do AEM para Entrega e Gerenciamento de Conteúdo Estruturado](/help/headless/apis-headless-and-content-fragments.md) para obter uma visão geral das várias APIs disponíveis e uma comparação de alguns dos conceitos envolvidos.

## APIs específicas de SPA {#spa-apis}

A estrutura do SDK do Editor de aplicativo de página única (SPA) do AEM fornece referências específicas da API do JavaScript.

| API | Descrição |
|---|---|
| [Mapeamento de Componente](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | Fornece uma maneira para o Aplicativo de Página único mapear componentes front-end para Adobe Experience Manager tipos de recursos (AEM Componentes) |
| [Gerenciador de modelos do Página](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Intérprete entre Adobe Experience Manager editor e o Adobe Experience Manager Página Single Página Application (SPA) editor |
| [Reagir Componentes Editáveis](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Fornece os componentes do React e a camada de integração para começar a usar o Editor de sites do Adobe Experience Manager |
| [Componentes editáveis do Angular](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Fornece os componentes do Angular e a camada de integração para ajudar você a começar a usar o Editor de sites do Adobe Experience Manager |

>[!TIP]
>
>Confira a [Introdução e apresentação do SPA](/help/implementing/developing/hybrid/introduction.md) para obter mais informações sobre aplicativos de página única.
