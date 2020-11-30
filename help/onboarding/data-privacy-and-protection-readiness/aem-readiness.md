---
title: Regulamentos de proteção de dados e privacidade de dados - Adobe Experience Manager como disponibilidade para Cloud Service
description: 'Saiba mais sobre a Adobe Experience Manager como suporte para Cloud Service para as várias regulamentações de proteção de dados e privacidade de dados; incluindo o Regulamento Geral da UE sobre Proteção de Dados (RGPD), a Lei da Privacidade do Consumidor da Califórnia e como cumprir ao implementar um novo AEM como um projeto Cloud Service. '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---


# Adobe Experience Manager como Cloud Service para a prontidão para proteção de dados e regulamentos de privacidade de dados {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não substitui o aconselhamento jurídico.
>
>Consulte o departamento jurídico da sua empresa para obter informações sobre as regulamentações de Proteção de Dados e Privacidade de Dados.

>[!NOTE]
>
>Para obter mais informações sobre o que isso significa em relação a problemas de privacidade, consulte o Centro de privacidade do [Adobe](https://www.adobe.com/privacy.html).

A Adobe está fornecendo documentação e procedimentos (com APIs quando disponíveis), para o administrador de privacidade do cliente ou administrador de AEM para lidar com solicitações de proteção de dados e privacidade e ajudar nossos clientes a cumprir essas regulamentações. Os procedimentos documentados permitirão que os clientes executem as solicitações normativas manualmente ou chamando as APIs, quando disponíveis, de um portal ou serviço externo.

>[!CAUTION]
>
>Os detalhes documentados aqui estão restritos à Adobe Experience Manager como Cloud Service.
>
>Os dados de outro Serviço sob demanda do Adobe, juntamente com quaisquer solicitações de privacidade relacionadas, exigirão ações nesse serviço.
>
>Para obter mais informações, consulte Central [de privacidade do](https://www.adobe.com/privacy.html)Adobe.

## Introdução {#introduction}

Instâncias da Adobe Experience Manager como Cloud Service, e os aplicativos que são executados neles, são de propriedade e operados por nossos clientes.

Como consequência, regulamentos de proteção de dados, como o RGPD, o CCPA e outros, são em grande parte da responsabilidade dos clientes.

Como introdução muito breve, os regulamentos relativos à privacidade e proteção de dados incluem novas regras que devem ser seguidas pelas funções de:

* Entidades de Negócios (CCPA) e/ou Controladores de Dados (RGPD)

* provedores de serviço (CCPA) e/ou processadores de dados (RGPD)

As principais disposições desses regulamentos são as seguintes:

1. Definição ampliada de dados pessoais para incluir todas as IDs exclusivas; como nos dados direta e indiretamente identificáveis.

2. Requisitos de consentimento reforçados.

3. Aumento do foco nos direitos de exclusão (eliminação de dados).

4. Recusar a venda de dados.

Para Adobe Experience Manager como Cloud Service:

* As instâncias e os aplicativos que são executados nelas são de propriedade e operados pelo cliente.

   * Isso significa que o cliente gerencia efetivamente as funções normativas, incluindo as Entidades de negócios e o Provedor de serviço, o Controlador de dados e o Processador de dados, entre outros.

   * O Adobe Experience Platform Privacy Service não fará parte do fluxo de trabalho do AEM, conforme ilustrado no diagrama abaixo.

* AEM inclui documentação e procedimentos para o administrador de privacidade do cliente e/ou AEM administrador executar as solicitações de regulamentação de privacidade; manualmente ou por meio de APIs, quando disponível.

* Nenhum novo serviço ou interface de usuário foi adicionado.

   * Em vez disso, os procedimentos e as APIs são documentados para uso pelas interfaces de usuário/portais do cliente que lidam com solicitações de regulamentação de privacidade.

* AEM não incluirá nenhuma ferramenta pronta para uso para suportar o fluxo de trabalho de solicitações de privacidade.

   * O Adobe fornecerá documentação e procedimentos para o administrador de privacidade do cliente e/ou AEM administrador, permitindo que ele execute manualmente solicitações relacionadas às regras de privacidade.

O Adobe está fornecendo procedimentos para lidar com solicitações de privacidade relacionadas ao Access, Delete e Opt-Out para Adobe Experience Manager como Cloud Service. Em alguns casos, há APIs disponíveis que podem ser chamadas de um portal desenvolvido pelo cliente ou scripts para ajudar na automação.

O diagrama a seguir ilustra a aparência de um fluxo de trabalho de solicitação de privacidade (ilustrado com o Adobe Experience Manager 6.5):

![Proteção de dados e privacidade](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager como Cloud Service e disponibilidade normativa {#aem-as-a-cloud-service-and-regulatory-readiness}

Consulte as seções abaixo para obter a documentação normativa das áreas de produtos de AEM como Cloud Service.

## Adobe Experience Manager as a Cloud Service Foundation {#aem-foundation}

See [AEM Foundation Readiness for Data Protection and Data Privacy Regulations](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md).

## Sites do Adobe Experience Manager as a Cloud Service {#aem-sites}

See [AEM Sites Readiness for Data Protection and Data Privacy Regulations.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager como uma integração de Cloud Service com Adobe Target e Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Essas integrações Adobe Experience Manager como Cloud Service estão com serviços prontos para proteção e privacidade de dados (por exemplo, RGPD). Nenhum dado pessoal da Adobe Target ou Adobe Analytics é armazenado em AEM em relação às integrações.
Para obter mais informações, consulte:

* [Adobe Target - Visão geral de privacidade](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Fluxo de trabalho de privacidade de dados da Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)
