---
title: Integração de comércio AEM e de terceiros usando a estrutura de integração de comércio
description: Integração de comércio AEM e de terceiros usando a estrutura de integração de comércio
translation-type: tm+mt
source-git-commit: c5694cf8651cf8ba5331c730fa1b1180310dd35a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Integração de comércio AEM e de terceiros usando a estrutura de integração de comércio {#aem-third-party}

As empresas corporativas podem exigir soluções adicionais de comércio de terceiros para potencializar sua vitrine. O Commerce Integration Framework (CIF) pode ser usado em cenários de integração onde, além do Magento, uma solução de comércio terceirizado também precisa ser integrada ao AEM. O CIF fornece elementos como uma vitrine de referência do acelerador, AEM os componentes principais CIF e ferramentas de criação que funcionam com o Magento out-of-the-box. Para integrar AEM e uma solução de comércio de terceiros e reutilizar esses elementos CIF, é necessário um desenvolvimento adicional.

## Arquitetura {#architecture}

A arquitetura geral é a seguinte:

![Visão geral da arquitetura AEM não-Magento/de terceiros](/help/commerce-cloud/assets/AEM_nonMagento_Architecture.JPG)

A principal diferença entre a arquitetura de integração para o comércio AEM - Magento e AEM - de terceiros é a adição de uma camada de integração e transformação de dados, como mostrado na imagem acima. A camada de integração precisa ser hospedada na plataforma Adobe I/O Runtime, que é a plataforma sem servidor Adobe. Você pode aprender mais sobre o Adobe I/O Runtime [aqui](https://www.adobe.io/apis/experienceplatform/runtime.html).

A finalidade dessa camada de integração é mapear APIs de terceiros ou não Magento contra APIs de comércio de Adobe (Magento GraphQL APIs). Esse mapeamento permite que os componentes [principais CIF e as ferramentas de criação CIF](https://github.com/adobe/aem-core-cif-components) AEM recuperem dados da solução não-Magento. Com essa abordagem, a camada de integração encapsula a lógica de integração e cria uma separação de preocupações entre AEM e a solução de terceiros. Isso permite o uso dos elementos CIF de forma agnóstica com várias soluções de terceiros. As vantagens de usar os elementos CIF em seu projeto foram descritas na [Introdução](/help/commerce-cloud/overview.md).

## Desenvolver uma integração {#develop-integration}

Para ajudá-lo a começar a criar a camada de integração necessária para integrar uma solução de terceiros/não-Magento com AEM, criamos uma implementação [de](https://github.com/adobe/commerce-cif-graphql-integration-reference) referência para demonstrar isso. Essa referência pode ser usada como ponto de partida em seu projeto.
