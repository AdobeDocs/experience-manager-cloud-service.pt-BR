---
title: Integração de comércio de terceiros com o AEM usando a Commerce Integration Framework
description: Integração de comércio de terceiros com o AEM usando a Commerce Integration Framework
translation-type: ht
source-git-commit: c5694cf8651cf8ba5331c730fa1b1180310dd35a
workflow-type: ht
source-wordcount: '338'
ht-degree: 100%

---


# Integração de comércio de terceiros com o AEM usando a Commerce Integration Framework {#aem-third-party}

Corporações podem exigir outras soluções comerciais de terceiros para potencializar a loja. A Commerce Integration Framework (CIF) pode ser usada em casos que requerem, além da Magento, a integração de uma solução comercial de terceiros ao AEM. A CIF fornece elementos como uma loja de referência do acelerador, os Componentes principais da CIF do AEM e ferramentas de criação que funcionam imediatamente com a Magento. Para integrar o AEM e uma solução comercial de terceiros e reutilizar esses elementos da CIF, é necessário um desenvolvimento adicional.

## Arquitetura {#architecture}

Esta é a arquitetura geral:

![Visão geral da arquitetura do AEM sem a Magento e com soluções de terceiros](/help/commerce-cloud/assets/AEM_nonMagento_Architecture.JPG)

A principal diferença entre a arquitetura de integração do AEM com a Magento e do AEM com soluções comerciais de terceiros é a adição de uma camada de integração e transformação de dados, como mostrado na imagem acima. A camada de integração precisa ser hospedada na plataforma Adobe I/O Runtime, que é a plataforma sem servidor da Adobe. Você pode obter mais informações sobre a Adobe I/O Runtime [aqui](https://www.adobe.io/apis/experienceplatform/runtime.html).

A finalidade dessa camada de integração é o mapeamento entre APIs de terceiros ou que não sejam da Magento e APIs do Adobe Commerce (APIs GraphQL da Magento). Com esse mapeamento, os [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) podem recuperar dados de solução diferentes da Magento. Com essa abordagem, a camada de integração encapsula a lógica de integração e cria uma separação de interesses entre o AEM e a solução de terceiros. Dessa forma, você pode usar os elementos da CIF de forma agnóstica com várias soluções de terceiros. As vantagens de usar os elementos da CIF em seu projeto estão descritas na [Introdução](/help/commerce-cloud/overview.md).

## Desenvolver uma integração {#develop-integration}

Para ajudar você a começar a criar a camada de integração necessária para integrar uma solução de terceiros que não seja a Magento com o AEM, criamos uma [implementação de referência](https://github.com/adobe/commerce-cif-graphql-integration-reference) para demonstrar o processo. Essa referência pode ser usada como ponto de partida em seu projeto.
