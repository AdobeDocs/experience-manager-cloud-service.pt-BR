---
title: Regulamentos de proteção de dados e privacidade de dados - Adobe Experience Manager como uma preparação para o serviço em nuvem
description: 'Learn about Adobe Experience Manager as a Cloud Service support for the various Data Protection and Data Privacy Regulations; including the EU General Data Protection Regulation (GDPR), the California Consumer Privacy Act and how to comply when implementing a new AEM as a Cloud Service project. '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---


# Adobe Experience Manager as a Cloud Service Readiness for Data Protection and Data Privacy Regulations {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não substitui o aconselhamento jurídico.
>
>Consulte o departamento jurídico da sua empresa para obter informações sobre as regulamentações de Proteção de Dados e Privacidade de Dados.

>[!NOTE]
>
>Para obter mais informações sobre a resposta da Adobe a problemas de privacidade e o que isso significa para você como cliente da Adobe, consulte o Centro [de privacidade da](https://www.adobe.com/privacy.html)Adobe.

A Adobe está fornecendo documentação e procedimentos (com APIs quando disponíveis), para que o administrador de privacidade do cliente ou o administrador do AEM atenda às solicitações de proteção de dados e privacidade e ajude nossos clientes a cumprir essas regulamentações. Os procedimentos documentados permitirão que os clientes executem as solicitações normativas manualmente ou chamando as APIs, quando disponíveis, de um portal ou serviço externo.

>[!CAUTION]
>
>Os detalhes documentados aqui estão restritos ao Adobe Experience Manager como um serviço em nuvem.
>
>Data from another Adobe On-demand Service, together with any related privacy requests, will require actions to be taken on that service.
>
>For further information see [Adobe&#39;s Privacy Center](https://www.adobe.com/privacy.html).

## Introdução {#introduction}

As instâncias do Adobe Experience Manager como um serviço em nuvem, e os aplicativos executados nelas, são de propriedade e operados por nossos clientes.

As a consequence, data protection regulations, such as GDPR, CCPA, and others, are largely the responsibility of the customers.

Como introdução muito breve, os regulamentos relativos à privacidade e proteção de dados incluem novas regras que devem ser seguidas pelas funções de:

* Entidades de Negócios (CCPA) e/ou Controladores de Dados (RGPD)

* Provedores de serviço (CCPA) e/ou processadores de dados (RGPD)

As principais disposições desses regulamentos são as seguintes:

1. Expanded definition of personal data to include all unique IDs; as in directly and indirectly identifiable data.

2. Strengthened consent requirements.

3. Aumento do foco nos direitos de exclusão (eliminação de dados).

4. Recusar a venda de dados.

For Adobe Experience Manager as a Cloud Service:

* As instâncias e os aplicativos que são executados nelas são de propriedade e operados pelo cliente.

   * Isso significa que o cliente gerencia efetivamente as funções normativas, incluindo as Entidades de negócios e o Provedor de serviço, o Controlador de dados e o Processador de dados, entre outros.

   * O Adobe Experience Platform Privacy Service não fará parte do fluxo de trabalho do AEM, como ilustrado no diagrama abaixo.

* O AEM inclui documentação e procedimentos para o administrador de privacidade do cliente e/ou o administrador do AEM para executar as solicitações de regulamento de privacidade; manualmente ou por meio de APIs, quando disponível.

* No new service or UI has been added.

   * Instead procedures and APIs are documented for use by the customer UIs/portals that handle privacy regulation requests.

* O AEM não incluirá nenhuma ferramenta pronta para uso para suportar o fluxo de trabalho de solicitações de privacidade.

   * A Adobe fornecerá documentação e procedimentos para o administrador de privacidade do cliente e/ou o administrador de AEM, permitindo que ele execute manualmente solicitações relacionadas às regras de privacidade.

A Adobe está fornecendo procedimentos para lidar com solicitações de privacidade relacionadas ao Access, Delete e Opt-Out para o Adobe Experience Manager como um Serviço em nuvem. Em alguns casos, há APIs disponíveis que podem ser chamadas de um portal desenvolvido pelo cliente ou scripts para ajudar na automação.

O diagrama a seguir ilustra a aparência de um fluxo de trabalho de solicitação de privacidade (ilustrado com o Adobe Experience Manager 6.5):

![Proteção de dados e privacidade](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager as a Cloud Service and Regulatory Readiness {#aem-as-a-cloud-service-and-regulatory-readiness}

Please see the sections below for regulatory documentation for product areas of AEM as a Cloud Service.

## Adobe Experience Manager as a Cloud Service Foundation {#aem-foundation}

See [AEM Foundation Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Sites do Adobe Experience Manager as a Cloud Service {#aem-sites}

See [AEM Sites Readiness for Data Protection and Data Privacy Regulations.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager as a Cloud Service Integration with Adobe Target &amp; Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Essas integrações do Adobe Experience Manager como um serviço em nuvem são feitas com serviços prontos de proteção e privacidade de dados (por exemplo, RGPD). Nenhum dado pessoal do Adobe Público alvo ou do Adobe Analytics é armazenado no AEM em relação às integrações.
Para obter mais informações, consulte:

* [Público alvo da Adobe - Visão geral de privacidade](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics Data Privacy Workflow](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)
