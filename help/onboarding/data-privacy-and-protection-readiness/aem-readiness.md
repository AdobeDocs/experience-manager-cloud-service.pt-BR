---
title: Regulamentos de proteção de dados e privacidade de dados - Adobe Experience Manager como uma preparação para o serviço em nuvem
description: 'Saiba mais sobre o Adobe Experience Manager como um suporte do Cloud Service para as várias regulamentações de proteção de dados e privacidade de dados; incluindo o Regulamento geral da UE sobre proteção de dados (RGPD), a Lei da Privacidade do Consumidor da Califórnia e como cumprir a implementação de um novo AEM como um projeto de serviço em nuvem. '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247

---


# Adobe Experience Manager como um serviço em nuvem pronto para proteção de dados e regulamentos de privacidade de dados {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não substitui o aconselhamento jurídico.
>
>Consulte o departamento jurídico da sua empresa para obter conselhos sobre as regulamentações de Proteção de Dados e Privacidade de Dados.

>[!NOTE]
>
>Para obter mais informações sobre a resposta da Adobe a problemas de privacidade e o que isso significa para você como cliente da Adobe, consulte o Centro [de privacidade da](https://www.adobe.com/privacy.html)Adobe.

A Adobe está fornecendo documentação e procedimentos (com APIs quando disponíveis), para que o administrador de privacidade do cliente ou o administrador do AEM atenda às solicitações de proteção de dados e privacidade e ajude nossos clientes a cumprir essas regulamentações. Os procedimentos documentados permitirão que os clientes executem as solicitações normativas manualmente ou chamando as APIs, quando disponíveis, de um portal ou serviço externo.

>[!CAUTION]
>
>Os detalhes documentados aqui estão restritos ao Adobe Experience Manager como um serviço em nuvem.
>
>Os dados de outro serviço sob demanda da Adobe, juntamente com quaisquer solicitações de privacidade relacionadas, exigirão ações nesse serviço.
>
>Para obter mais informações, consulte o Centro [de privacidade da](https://www.adobe.com/privacy.html)Adobe.

## Introdução {#introduction}

As instâncias do Adobe Experience Manager como um serviço em nuvem, e os aplicativos executados nelas, são de propriedade e operados por nossos clientes.

Como consequência, regulamentos de proteção de dados, como o RGPD, o CCPA e outros, são em grande parte da responsabilidade dos clientes.

Como introdução muito breve, os regulamentos relativos à privacidade e proteção de dados incluem novas regras que devem ser seguidas pelas funções de:

* Entidades de Negócios (CCPA) e/ou Controladores de Dados (RGPD)

* Fornecedores de serviços (CCPA) e/ou Processadores de dados (RGPD)

As principais disposições desses regulamentos são:

1. Definição ampliada de dados pessoais para incluir todas as IDs exclusivas; como nos dados direta e indiretamente identificáveis.

2. Requisitos de consentimento reforçados.

3. Aumento do foco nos direitos de exclusão (eliminação de dados).

4. Recusar a venda de dados.

Para o Adobe Experience Manager como um serviço em nuvem:

* As instâncias e os aplicativos que são executados nelas são de propriedade e operados pelo cliente.

   * Isso significa que o cliente gerencia efetivamente as funções normativas, incluindo Entidades de negócios e Provedor de serviços, Controlador de dados e Processador de dados, entre outros.

   * O Adobe Experience Platform Privacy Service não fará parte do fluxo de trabalho do AEM, como ilustrado no diagrama abaixo.

* O AEM inclui documentação e procedimentos para o administrador de privacidade do cliente e/ou o administrador do AEM executar as solicitações de regulamento de privacidade; manualmente ou por meio de APIs, quando disponível.

* Nenhum novo serviço ou interface de usuário foi adicionado.

   * Em vez disso, os procedimentos e as APIs são documentados para uso pelas interfaces de usuário/portais do cliente que lidam com solicitações de regulamentação de privacidade.

* O AEM não incluirá nenhuma ferramenta pronta para uso para suportar o fluxo de trabalho de solicitações de privacidade.

   * A Adobe fornecerá documentação e procedimentos para o administrador de privacidade do cliente e/ou o administrador de AEM, permitindo que ele execute manualmente solicitações relacionadas às regras de privacidade.

A Adobe está fornecendo procedimentos para lidar com solicitações de privacidade relacionadas ao Access, Delete e Opt-Out para o Adobe Experience Manager como um Serviço em nuvem. Em alguns casos, há APIs disponíveis que podem ser chamadas de um portal desenvolvido pelo cliente ou scripts para ajudar na automação.

O diagrama a seguir ilustra a aparência de um fluxo de trabalho de solicitação de privacidade (ilustrado com o Adobe Experience Manager 6.5):

![Proteção de dados e privacidade](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager como serviço em nuvem e disponibilidade normativa {#aem-as-a-cloud-service-and-regulatory-readiness}

Consulte as seções abaixo para obter a documentação normativa das áreas de produto do AEM como um serviço em nuvem.

## Adobe Experience Manager como uma base de serviços em nuvem {#aem-foundation}

Consulte Prontidão da Fundação [AEM para proteção de dados e regulamentos](/help/onboarding/data-privacy-and-protection-readiness/foundation-readiness.md)de privacidade de dados.

## Adobe Experience Manager como Sites de serviço em nuvem {#aem-sites}

Consulte Prontidão do [AEM Sites para proteção de dados e regulamentos de privacidade de dados.](/help/onboarding/data-privacy-and-protection-readiness/sites-readiness.md)

## Adobe Experience Manager como uma integração de serviço em nuvem com o Adobe Target e o Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Essas integrações do Adobe Experience Manager como um serviço em nuvem são feitas com serviços prontos de proteção e privacidade de dados (por exemplo, RGPD). Nenhum dado pessoal do Adobe Target ou Adobe Analytics é armazenado no AEM em relação às integrações.
Para obter mais informações, consulte:

* [Adobe Target - Visão geral de privacidade](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Fluxo de trabalho de privacidade de dados do Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)
