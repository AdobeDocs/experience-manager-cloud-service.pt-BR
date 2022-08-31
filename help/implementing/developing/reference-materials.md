---
title: Materiais de referência de API
description: O AEM tem APIs abrangentes e eficientes que você pode aproveitar para o seu projeto de experiência digital.
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 6%

---

# Materiais de referência de API {#api-reference-materials}

O Adobe Experience Manager (AEM) fornece muitas APIs para desenvolver aplicativos e estender AEM. O AEM é construído sobre várias tecnologias de código aberto, que também podem ser aproveitadas.

## AEM APIs principais {#core-aem-apis}

As seguintes APIs são fundamentais para a AEM.

| API | Descrição |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | abstrações de produto, como páginas, ativos, fluxos de trabalho etc. |
| [Interface do usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Pilha Open Web do Adobe, fornecendo vários componentes essenciais (Observe que os materiais de Granite 6.5 se aplicam ao AEMaaCS) |
| [Interface do usuário do Coral](https://opensource.adobe.com/coral-spectrum/documentation/) | Estilo visual do Adobe para interfaces do usuário da nuvem, projetado para fornecer consistência à experiência do usuário |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

## Estruturas adicionais {#additional-apis}

O AEM depende de várias APIs de código aberto adicionais.

| API | Descrição |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | Estrutura da Web que usa um Java Content Repository (JCR) para armazenar e gerenciar conteúdo |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | Implementar um Java Content Repository (JCR) hierárquico escalável e de alto desempenho para uso como a base de sites da Web modernos e de classe internacional |
| [Repositório de conteúdo Java](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | Especificação para o JCR versão 2.0 |
| [Apache Felix](https://felix.apache.org) | Implementação da estrutura e plataforma de serviço da iniciativa Open Services Gateway (OSGi) |

## Diretrizes de preferência de API {#guidelines}

AEM é criado nos quatro conjuntos principais de API do Java a seguir em ordem decrescente de preferência.

| Prioridade | API | Descrição |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | abstrações de produto, como páginas, ativos, fluxos de trabalho etc. |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST e abstrações baseadas em recursos, como recursos, mapas de valor e solicitações HTTP. |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | abstrações de dados e conteúdo, como nó, propriedades e sessões. |
| 4 | [Apache Felix](https://felix.apache.org/) | abstrações do contêiner de aplicativos OSGi, como serviços e componentes (OSGi). |

Se uma API for fornecida pelo AEM, prefira-a em vez do Sling, JCR e OSGi. Se AEM não fornecer uma API, então prefira Sling em vez de JCR e OSGi.

>[!TIP]
>
>Para obter detalhes sobre essas diretrizes, consulte o documento [Entenda as práticas recomendadas da API Java.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

## Serviços e APIs de entrega e gerenciamento de conteúdo de AEM {#delivery-apis}

AEM oferece componentes personalizáveis e opções de entrega de conteúdo.

| Recurso | Descrição |
|---|---|
| [Os componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) | Componentes padronizados do Gerenciamento de conteúdo da Web (WCM) para AEM agilizar o tempo de desenvolvimento e reduzir o custo de manutenção de seus sites |
| [Exportador JSON](/help/implementing/developing/components/json-exporter.md) | Fornecer o conteúdo de qualquer página de AEM no formato de modelo de dados JSON |
| [Ativação da exportação em JSON para um componente](/help/implementing/developing/components/enabling-json-exporter.md) | Gerar exportação JSON do conteúdo do componente com base em uma estrutura de modelador |
| [API de ativos](/help/assets/mac-api-assets.md) | Permite a criação-leitura-atualização-exclusão (CRUD) de operações em ativos, incluindo binários, metadados, representações e comentários. Consulte API HTTP do AEM Assets |
| [API HTTP dos fragmentos de conteúdo](/help/assets/content-fragments/assets-api-content-fragments.md) | Acesse o conteúdo do fragmento de conteúdo diretamente pela API HTTP por meio de operações CRUD |
| [API GraphQL do fragmento de conteúdo](/help/headless/graphql-api/content-fragments.md) | Ativar a entrega eficiente de Fragmentos de conteúdo para clientes JavaScript em implementações CMS sem periféricos |
| [API HTTP dos ativos dos fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | Formato exato de solicitações de ativos HTTP compatíveis |

## APIs específicas do SPA {#spa-apis}

AEM estrutura do SDK do Editor de aplicativo de página única (SPA) fornece referências específicas à API do JavaScript.

| API | Descrição |
|---|---|
| [Mapeamento de componentes](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | Fornece uma maneira de o Aplicativo de página única mapear componentes de front-end para tipos de recursos do Adobe Experience Manager (Componentes de AEM) |
| [Gerenciador do modelo de página](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Um interpretador entre o Editor do Adobe Experience Manager e o Editor de aplicativo de página única (SPA) do Adobe Experience Manager |
| [Reagir componentes editáveis](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | Fornece os componentes React e a camada de integração para começar a usar o Editor de site do Adobe Experience Manager |
| [Componentes editáveis do Angular](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | Fornece os componentes do Angular e a camada de integração para começar a usar o Editor de sites da Adobe Experience Manager |

>[!TIP]
>
>Confira o [Introdução SPA e Apresentação](/help/implementing/developing/hybrid/introduction.md) para obter mais informações sobre aplicativos de página única.
