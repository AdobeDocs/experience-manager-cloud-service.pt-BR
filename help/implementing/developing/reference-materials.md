---
title: Materiais de referência de API
description: O AEM tem APIs abrangentes e poderosas que você pode usar para o seu projeto de experiência digital.
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
feature: Developing
role: Admin, Architect, Developer
source-git-commit: b3405279393be51b805c1129c171bb2249fd5726
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 4%

---

# Materiais de referência de API {#api-reference-materials}

O Adobe Experience Manager (AEM) fornece muitas APIs para o desenvolvimento de aplicativos e a extensão do AEM. O AEM é construído com base em várias tecnologias de código aberto, que também podem ser usadas.

## APIs principais de AEM {#core-aem-apis}

As seguintes APIs são fundamentais para o AEM.

| API | Descrição |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Abstrações de produto, como páginas, ativos, fluxos de trabalho e assim por diante. |
| [Interface do usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Pilha da Web aberta do Adobe, fornecendo vários componentes essenciais (os materiais do Granite 6.5 se aplicam ao AEMaaCS) |
| [Interface do Coral](https://opensource.adobe.com/coral-spectrum/documentation/) | Estilo visual do Adobe para interfaces do usuário em nuvem, projetado para fornecer consistência à experiência do usuário |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

>[!NOTE]
>
>Para obter as informações mais recentes sobre as APIs Experience Manager, visite também as [APIs Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

## Estruturas adicionais {#additional-apis}

O AEM depende de várias APIs adicionais de código aberto.

| API | Descrição |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | Estrutura da Web que usa um Java Content Repository (JCR) para armazenar e gerenciar conteúdo |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Implementação de um Java Content Repository (JCR) hierárquico escalável e de alto desempenho para uso como base de sites da Web modernos de classe mundial |
| [Repositório de conteúdo Java](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | Especificação para o JCR versão 2.0 |
| [Apache Felix](https://felix.apache.org) | Implementação da estrutura da iniciativa Open Services Gateway (OSGi) e da plataforma de serviços |

## Diretrizes de preferência de API {#guidelines}

O AEM é criado nos quatro conjuntos principais de APIs do Java a seguir, em ordem decrescente de preferência.

| Prioridade | API | Descrição |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | Abstrações de produto, como páginas, ativos, fluxos de trabalho e assim por diante. |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST e abstrações baseadas em recursos, como recursos, mapas de valores e solicitações HTTP. |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Dados e abstrações de conteúdo, como nó, propriedades e sessões. |
| 4 | [Apache Felix](https://felix.apache.org/) | Abstrações do contêiner de aplicativo OSGi, como serviços e componentes (OSGi). |

Se uma API for fornecida pelo AEM, prefira-a ao Sling, JCR e OSGi. Se o AEM não fornecer uma API, prefira Sling a JCR e OSGi.

>[!TIP]
>
>Para obter detalhes sobre essas diretrizes, consulte o documento [Entender as práticas recomendadas da API Java.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

## Entrega de AEM e serviços e APIs de gerenciamento de conteúdo {#delivery-apis}

O AEM oferece componentes personalizáveis e opções de entrega de conteúdo.

| Destaque | Descrição |
|---|---|
| [Os Componentes Principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) | Componentes Web Content Management (WCM) padronizados para AEM para acelerar o tempo de desenvolvimento e reduzir o custo de manutenção de seus sites |
| [Exportador JSON](/help/implementing/developing/components/json-exporter.md) | Entregar o conteúdo de qualquer página AEM no formato de modelo de dados JSON |
| [Ativação da exportação em JSON para um componente](/help/implementing/developing/components/enabling-json-exporter.md) | Gerar exportação JSON de conteúdo do componente com base em uma estrutura do modelador |
| [API Assets](/help/assets/mac-api-assets.md) | Permite operações de criação, leitura, atualização e exclusão (CRUD) em ativos, incluindo binários, metadados, representações e comentários. Consulte API HTTP do AEM Assets |
| [API HTTP de fragmentos de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md) | Acessar conteúdo de fragmento de conteúdo diretamente pela API HTTP por meio de operações CRUD |
| [API do GraphQL de fragmento de conteúdo](/help/headless/graphql-api/content-fragments.md) | Permitir a entrega eficiente de fragmentos de conteúdo aos clientes do JavaScript em implementações de CMS headless |
| [API HTTP do Assets de fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | Formato exato de solicitações de ativos HTTP compatíveis |
| [OpenAPIs de Fragmento de Conteúdo e de Modelo de Fragmento de Conteúdo](/help/headless/content-fragment-openapis.md) | OpenAPIs de fragmento de conteúdo e modelo de fragmento de conteúdo |

## APIs específicas para SPA {#spa-apis}

A estrutura do SDK do editor de aplicativo de página única (SPA) do AEM fornece referências específicas da API do JavaScript.

| API | Descrição |
|---|---|
| [Mapeamento de componentes](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | Fornece uma maneira para o aplicativo de página única mapear componentes de front-end para tipos de recursos do Adobe Experience Manager (componentes AEM) |
| [Gerenciador de Modelos de Página](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Um intérprete entre o Editor do Adobe Experience Manager e o Editor do aplicativo de página única (SPA) do Adobe Experience Manager |
| [Reagir Componentes Editáveis](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Fornece os componentes do React e a camada de integração para começar a usar o Editor de sites do Adobe Experience Manager |
| [Componentes editáveis do Angular](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Fornece os componentes do Angular e a camada de integração para ajudar você a começar a usar o Editor de sites do Adobe Experience Manager |

>[!TIP]
>
>Confira a [Introdução e apresentação do SPA](/help/implementing/developing/hybrid/introduction.md) para obter mais informações sobre aplicativos de página única.
