---
title: Regulamentos de proteção e privacidade de dados - Adobe Experience Manager as a Cloud Service Readiness
description: Saiba mais sobre o Adobe Experience Manager as a Cloud Service Support para as várias regulamentações de proteção e privacidade de dados; incluindo o Regulamento Geral sobre a Proteção de Dados da UE (GDPR), a Lei de Privacidade do Consumidor da Califórnia e como fazer isso ao implementar um novo AEM como um projeto do Cloud Service.
exl-id: 5dfa353b-84c5-4b07-bfcd-b03c2d361553
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Regulamentos de disponibilidade para proteção e privacidade de dados do Adobe Experience Manager as a Cloud Service {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não se destina a substituir tal aconselhamento.
>
>Consulte o departamento jurídico da sua empresa para obter aconselhamento sobre as regras de proteção e privacidade de dados.

>[!NOTE]
>
>Para obter mais informações sobre resposta do Adobe a problemas de privacidade e o que isso significa para você como cliente de Adobe, consulte [Central de Privacidade do Adobe](https://www.adobe.com/privacy.html).

O Adobe está fornecendo documentação e procedimentos (com APIs quando disponíveis), para o administrador de privacidade do cliente ou AEM administrador lidar com solicitações de proteção e privacidade de dados e ajudar nossos clientes a cumprir essas regulamentações. Os procedimentos documentados permitirão que os clientes executem as solicitações normativas manualmente ou chamando APIs, quando disponíveis, de um portal ou serviço externo.

>[!CAUTION]
>
>Os detalhes documentados aqui estão restritos ao Adobe Experience Manager as a Cloud Service.
>
>Os dados de outro Serviço sob demanda do Adobe, juntamente com quaisquer solicitações de privacidade relacionadas, exigirão que ações sejam tomadas nesse serviço.
>
>Para obter mais informações, consulte [Central de Privacidade do Adobe](https://www.adobe.com/privacy.html).

## Introdução {#introduction}

As instâncias do Adobe Experience Manager as a Cloud Service e os aplicativos que as executam são de propriedade e operados por nossos clientes.

Como consequência, as regulamentações de proteção de dados, como GDPR, CCPA e outras, são em grande parte da responsabilidade dos clientes.

Como breve introdução, os regulamentos relativos à privacidade e proteção de dados incluem novas regras que devem ser seguidas pelas funções de:

* Entidades de Negócios (CCPA) e/ou Controladores de Dados (GDPR)

* Fornecedores de serviços (CCPA) e/ou Processadores de dados (GDPR)

As principais disposições desses regulamentos são as seguintes:

1. Definição ampliada de dados pessoais para incluir todas as IDs exclusivas; como nos dados direta e indiretamente identificáveis.

2. Requisitos de consentimento reforçados.

3. Aumento do foco nos direitos de exclusão (Eliminação de dados).

4. Recusar a venda de dados.

Para o Adobe Experience Manager as a Cloud Service:

* As instâncias e os aplicativos que são executados neles são de propriedade e operados pelo cliente.

   * Isso significa que o cliente gerencia as funções normativas, incluindo Entidades de negócios e Provedor de serviços, Controlador de dados e Processador de dados, entre outras.

   * O Adobe Experience Platform Privacy Service não fará parte do fluxo de trabalho do AEM, conforme ilustrado no diagrama abaixo.

* AEM inclui documentação e procedimentos para o administrador de privacidade do cliente e/ou AEM administrador para executar as solicitações de regulamento de privacidade; manualmente ou por meio de APIs, quando disponível.

* Nenhum novo serviço ou interface do usuário foi adicionado.

   * Em vez disso, os procedimentos e as APIs são documentados para uso pelas interfaces do usuário/portais do cliente que lidam com solicitações de regulamentação de privacidade.

* AEM não incluirá nenhuma ferramenta pronta para uso para suportar o fluxo de trabalho de solicitações de privacidade.

   * O Adobe fornecerá documentação e procedimentos para o administrador de privacidade do cliente e/ou AEM administrador, permitindo que ele execute manualmente solicitações relacionadas às regras de privacidade.

O Adobe está fornecendo procedimentos para lidar com solicitações de privacidade relacionadas ao Acesso, Exclusão e Não participação no Adobe Experience Manager as a Cloud Service. Em alguns casos, há APIs disponíveis que podem ser chamadas de um portal desenvolvido pelo cliente ou scripts para ajudar na automação.

O diagrama a seguir ilustra a aparência de um fluxo de trabalho de solicitação de privacidade (ilustrado com o Adobe Experience Manager 6.5):

![Proteção e privacidade de dados](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager como Cloud Service e disponibilidade dos regulamentos {#aem-as-a-cloud-service-and-regulatory-readiness}

Consulte as seções abaixo para obter a documentação regulamentar para as áreas de produtos do AEM como Cloud Service.

## Adobe Experience Manager as a Cloud Service Foundation {#aem-foundation}

Consulte [AEM Foundation Readiness for Data Protection and Data Privacy Regulations](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md).

## Sites do Adobe Experience Manager as a Cloud Service {#aem-sites}

Consulte [Regulamentos de disponibilidade do AEM Sites para proteção e privacidade de dados.](/help/compliance/data-privacy-and-protection-readiness/sites-readiness.md)

## Integração do Adobe Experience Manager as a Cloud Service com o Adobe Target e Adobe Analytics {#aem-integration-with-adobe-target-adobe-analytics}

Essas integrações do Adobe Experience Manager as a Cloud Service estão com serviços prontos para proteção e privacidade de dados (por exemplo, GDPR). Nenhum dado pessoal do Adobe Target ou Adobe Analytics é armazenado em AEM em relação às integrações.
Para obter mais informações, consulte:

* [Adobe Target - Visão geral de privacidade](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html)

* [Fluxo de trabalho da Privacidade de dados do Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html)
