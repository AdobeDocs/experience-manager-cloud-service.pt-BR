---
title: Disponibilidade para HIPAA para Adobe Experience Manager as a Cloud Service
description: Saiba mais sobre o suporte do Experience Manager as a Cloud Service para os Regulamentos HIPAA e como estar em conformidade ao implementar um novo projeto AEM as a Cloud Service.
feature: Compliance
role: Admin, Architect, Developer, Leader
source-git-commit: 49721ac71bc2bde10eb5f25db58ee1b07c8a82e5
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 6%

---

# Disponibilidade para HIPAA para Adobe Experience Manager as a Cloud Service {#hipaa-readiness-for-adobe-experience-manager-as-a-cloud-service}

>[!WARNING]
>
>O conteúdo deste documento não constitui um aconselhamento jurídico e não se destina a substituir tal aconselhamento.
>
>Consulte o departamento jurídico da sua empresa para obter aconselhamento sobre as normas da HIPAA.

>[!NOTE]
>
>Para obter mais informações sobre a resposta da Adobe a problemas de privacidade, e o que isso significa para você como cliente do Adobe, consulte:
>
>* [Produtos e serviços da HIPAA e da Adobe](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html) na Central de Confiabilidade da Adobe
>* [Centro de privacidade da Adobe](https://www.adobe.com/br/privacy.html)

Para o Adobe Experience Manager (AEM) as a Cloud Service, a Adobe está fornecendo documentação para ajudá-lo a entender a preparação para a HIPAA. Ela pode ajudá-lo a cumprir esses regulamentos.

## HIPAA (Health Insurance Portability and Accountability Act, Lei de Portabilidade e Responsabilidade de Seguros de Saúde) {#health-insurance-portability-and-accountability-act-hipaa}

### HIPAA (Health Insurance Portability and Accountability Act, Lei de Portabilidade e Responsabilidade do Seguro de Saúde) {#the-health-insurance-portability-and-accountability-act-hipaa}

As regras de privacidade, segurança e notificação de violação da HIPAA estabelecem proteções importantes para informações de saúde individualmente identificáveis conhecidas como PHI (Protected Health Information, informações protegidas de saúde).

Sob a HIPAA, uma entidade coberta é um provedor de assistência médica, um plano de saúde ou uma câmara de compensação de assistência médica. Um associado comercial é uma entidade que fornece serviços a uma entidade coberta que envolve acesso a PHI. As regras de privacidade e segurança da HIPAA exigem que uma entidade coberta obtenha garantias por escrito de um associado comercial na forma de um Business Associate Agreement (BAA) exigindo que o associado comercial proteja a privacidade e a segurança da PHI da entidade coberta.

### Fornecimento de PHI ao Adobe {#providing-phi-to-adobe}

A Adobe atua como um Business Associate para seus Serviços prontos para HIPAA, listados em [Disponibilidade dos serviços para HIPAA no AEM as a Cloud Service](#hipaa-readiness-of-services-in-aem-as-a-cloud-service).

Os clientes que licenciam qualquer serviço pronto para HIPAA da Adobe para processar PHI **devem** ter a licença correta e um BAA assinado com a Adobe.

>[!IMPORTANT]
>
>Os clientes não têm permissão para criar, receber, manter ou transmitir PHI por meio de produtos e serviços da Adobe que não sejam designados como Serviços prontos para HIPAA ou sem a licença apropriada para usar um Serviço pronto para HIPAA.

### Responsabilidades compartilhadas com a HIPAA {#hipaa-shared-responsibilities}

Os serviços prontos para HIPAA da Adobe contam com um modelo de segurança de responsabilidade compartilhada, exigindo que o cliente e a Adobe assumam responsabilidades distintas para manter a segurança da PHI. Sob esse modelo de segurança compartilhada, a Adobe depende do cliente para usar e configurar os Serviços prontos para HIPAA consistentes com a HIPAA.

Para obter mais informações sobre como executar um Adobe BAA para serviços prontos para HIPAA, entre em contato com o representante de vendas da Adobe ou com o gerente de sucesso do cliente.

>[!IMPORTANT]
>
>**Isenção de responsabilidade**:
>
>O Cliente é responsável por usar os Serviços prontos para HIPAA da Adobe e por garantir que os Serviços prontos para HIPAA da Adobe atendam aos requisitos de conformidade.

Para obter mais informações, consulte [Produtos e serviços da HIPAA e da Adobe](https://www.adobe.com/trust/compliance/hipaa-hds/hipaa-ready.html) na Central de Confiabilidade da Adobe.

## Terminologia da HIPAA {#hipaa-terminology}

A tabela a seguir descreve como os serviços da AEM são categorizados para uso de HIPAA.

| Disponibilidade para HIPAA | Descrição |
| --- | --- |
| Pronto para HIPAA | Projetado para processar PHI quando configurado adequadamente e usado com um BAA. |
| Não preparado para HIPAA | Não foi projetado para processar PHI e não deve ser usado em casos de uso relacionados à HIPAA. |

>[!NOTE]
>
>As classificações de prontidão para HIPAA são baseadas na funcionalidade desejada de cada serviço e podem mudar com o tempo.
>
>Os clientes devem consultar a documentação mais recente e os termos contratuais aplicáveis ao planejar implantações relacionadas à HIPAA.

## Disponibilidade de serviços para HIPAA no AEM as a Cloud Service {#hipaa-readiness-of-services-in-aem-as-a-cloud-service}

A tabela a seguir descreve quais serviços da AEM estão prontos para HIPAA e quais serviços podem ser usados junto com eles. Os serviços prontos para HIPAA exigem a aquisição da Segurança ampliada para a área de saúde, conforme descrito em [Requisitos adicionais](#additional-requirements).

| Produto/Recurso | Serviço(s) | Disponibilidade para HIPAA |
| --- | --- | --- |
| AEM Sites | AEM Sites, Publicação no AEM, Edge Delivery Services | Pronto para HIPAA |
| AEM Sites | Editor universal | Não preparado para HIPAA<br>[1] Pode ser adicionado a um Programa de Segurança Estendida quando nenhum PHI é introduzido. |
| AEM Sites Optimizer | Sites Optimizer | Não preparado para HIPAA<br>[1] Pode ser adicionado a um Programa de Segurança Estendida quando nenhum PHI é introduzido. |
| AEM Assets | AEM Assets | Pronto para HIPAA |
| AEM Assets | Centro de conteúdo | Não preparado para HIPAA<br>[1] Pode ser adicionado a um Programa de Segurança Estendida quando nenhum PHI é introduzido. |
| AEM Assets | Brand Portal | Não preparado para HIPAA |
| AEM Assets | OpenAPI do Dynamic Media | Não preparado para HIPAA<br>[1] Pode ser adicionado a um Programa de Segurança Estendida quando nenhum PHI é introduzido. |
| AEM Assets | Dynamic Media Scene 7 | Não preparado para HIPAA |
| AEM Forms | AEM Forms, Serviço de fachada de autenticação, Serviço de utilitário da PDF | Pronto para HIPAA |
| AEM CIF | Commerce Integration Framework | Não preparado para HIPAA |
| AEM Cloud Manager | AEM Cloud Manager, Orquestrador de versões, Alternadores de versão, Validador de versões | Pronto para HIPAA |
| AEM Cloud Manager | Distribuição de software | Não preparado para HIPAA<br>[1] Pode ser adicionado a um Programa de Segurança Estendida quando nenhum PHI é introduzido. |
|   |   |   |
| AEM Guides  | AEM Guides  | Não preparado para HIPAA |
|   |   |   |
| LLM Optimizer | LLM Optimizer | Não preparado para HIPAA<br>[1] Pode ser adicionado a um Programa de Segurança Estendida quando nenhum PHI é introduzido. |

>[!NOTE]
>
>[1]
>
>Para serviços não prontos para HIPAA indicados como podem ser adicionados a um programa de Segurança estendida, os clientes devem garantir que o PHI não seja roteado para ou armazenado nesses serviços.
>
>A introdução da PHI em um serviço que não está preparado para a HIPAA pode resultar em não-conformidade.

### Requisitos adicionais {#additional-requirements}

[Os serviços listados](#hipaa-readiness-of-services-in-aem-as-a-cloud-service) como prontos para HIPAA exigem a compra do Extended Security for Healthcare.

Quando a Extended Security for adquirida para a área de saúde, é necessário que:

* os produtos selecionados para esse programa estão prontos para HIPAA (conforme listado na tabela),
* A Segurança ampliada para a área de saúde foi adquirida para *cada* produto; isso garante créditos suficientes da Cloud Manager,
* A Segurança ampliada para a área de saúde é aplicada no momento da criação do programa.

Se os requisitos forem atendidos, a Segurança estendida para a área de saúde poderá ser aplicada na criação do programa AEM; consulte [Configuração](#setup) para obter detalhes.

>[!NOTE]
>
>Para obter mais detalhes sobre provisionamento e preços, entre em contato com o representante de vendas.

## Ambientes {#environments}

*Pronto para HIPAA* não se aplica a ambientes RDE (Rapid Development Environment), Dev ou Stage, pois PHI não é permitido nesses ambientes.

Isso significa que você deve:

* usar dados de teste para fins de desenvolvimento e teste
* processar somente PHI de ambientes de produção

A tabela a seguir mostra onde os tipos de ambiente podem ser compatíveis como prontos para HIPAA.

| | RDE | Dev | Estágio  | Prod |
| --- | --- | --- | --- | --- |
| Tipo de ambiente  | Não  | Não  | Não  | Sim  |

## Configurar {#setup}

Ao [Criar Programas de Produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md), a [guia Segurança fornece as opções para ativar a proteção HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security).