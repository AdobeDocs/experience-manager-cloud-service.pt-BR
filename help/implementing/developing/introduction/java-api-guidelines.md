---
title: Diretrizes da API Java
description: AEM é criado em uma pilha rica de software de código aberto que expõe muitas APIs Java para uso.
translation-type: tm+mt
source-git-commit: b927992107d7e7e4df5511a366c71449ff73ec93
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# Diretrizes da API Java {#java-api-guidelines}

A Adobe Experience Manager (AEM) foi criada em uma pilha rica de software de código aberto que expõe muitas APIs Java para uso durante o desenvolvimento.

AEM é criado nos quatro conjuntos principais de APIs do Java a seguir, em ordem decrescente de preferência.

1. **Adobe Experience Manager (AEM)**  - abstrações de produtos, como páginas, ativos, workflows etc.
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)**  - REST e abstrações baseadas em recursos, como recursos, mapas de valor e solicitações HTTP.
1. **[JCR (Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)**  - abstrações de dados e conteúdo, como nó, propriedades e sessões.
1. **[OSGi (Apache Felix)](https://felix.apache.org)** - abstrações de container de aplicativos OSGi, como serviços e componentes (OSGi).

Se uma API for fornecida pelo AEM, prefira-a em vez de Sling, JCR e OSGi. Se AEM não fornecer uma API, então prefira Sling em vez de JCR e OSGi.

Para obter detalhes sobre essas diretrizes, consulte o documento [Entender as práticas recomendadas da API Java.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
