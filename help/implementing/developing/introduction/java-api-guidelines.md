---
title: Diretrizes da API Java
description: O AEM é criado em uma pilha de software de código aberto avançada que expõe muitas APIs Java para uso.
exl-id: 0be33ec9-a4c3-4400-99d3-ed8366c5b5f9
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Diretrizes da API Java {#java-api-guidelines}

O Adobe Experience Manager (AEM) é criado em uma pilha rica de software de código aberto que expõe muitas APIs Java para uso durante o desenvolvimento.

AEM é criado nos quatro conjuntos principais de API do Java a seguir em ordem decrescente de preferência.

1. **[Adobe Experience Manager (AEM)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/index.html)**  - abstrações de produto, como páginas, ativos, fluxos de trabalho, etc.
1. **[Apache Sling Web Framework](https://sling.apache.org/apidocs/sling11/)**  - REST e abstrações baseadas em recursos, como recursos, mapas de valor e solicitações HTTP.
1. **[JCR (Apache Jackrabbit Oak)](http://jackrabbit.apache.org/oak/docs/oak_api/overview.html)**  - abstrações de dados e conteúdo, como nó, propriedades e sessões.
1. **[OSGi (Apache Felix)](https://felix.apache.org)**  - abstrações do contêiner de aplicativos OSGi, como serviços e componentes (OSGi).

Se uma API for fornecida pelo AEM, prefira-a em vez do Sling, JCR e OSGi. Se AEM não fornecer uma API, então prefira Sling em vez de JCR e OSGi.

Para obter detalhes sobre essas diretrizes, consulte o documento [Entender práticas recomendadas da API Java.](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)
