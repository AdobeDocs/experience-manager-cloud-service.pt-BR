---
title: Notas de versão do Cloud Manager 2024.6.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2024.6.0 no AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
role: Admin
source-git-commit: 958d8fb3526bafeb5a3be9828bddfa3330c05fec
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 38%

---


# Notas de versão do Cloud Manager 2024.6.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2024.6.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager versão 2024.6.0 no AEM as a Cloud Service é 6 de junho de 2024. A próxima versão está planejada para 11 de julho de 2024.

## Novidades {#what-is-new}

* Agora você pode [usar seus próprios repositórios GitHub](/help/implementing/cloud-manager/managing-code/private-repositories.md) como fontes para pipelines de pilha completa e de front-end.
   * Além disso, é possível aproveitar os repositórios GitHub com [submódulos Git,](/help/implementing/cloud-manager/managing-code/git-submodules.md) fornecendo um controle aprimorado sobre os pipelines gerados automaticamente usados para validação de solicitação de pull e permitindo definir comportamentos para métricas cruciais durante a fase de verificação de código.
   * [Você também tem a opção](/help/implementing/cloud-manager/managing-code/github-check-config.md) de preservar o histórico do relatório no GitHub, nomear o pipeline e definir variáveis de pipeline para atender às suas necessidades.
* [Restauração de conteúdo de autoatendimento](/help/operations/restore.md) oferece restauração de backup por até sete dias e recursos:
   * Restauração de backup point-in-time nas últimas 24 horas
   * Restaurações por tempo fixo de até sete dias
* [Novas regras do OakPal](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-ui-content-package) foram adicionados à verificação de qualidade do código do Cloud Manager.
   * Todas as nova regras adicionadas até junho de 2024 são alterações secundárias.
   * Recomendamos que você resolva isso o mais rápido possível, pois essas novas regras causarão falhas nos pipelines a partir da versão de agosto de 2024 do Cloud Manager.

## Programa de adoção antecipada {#early-adoption}

Para testar alguns recursos futuros, faça parte do programa de adoção antecipada do Adobe.

### Suporte a Edge Delivery Services no Cloud Manager {#edge-delivery-services}

Se você tiver licenciado o Edge Delivery Services como parte do Adobe Experience Manager Sites, [agora você pode integrar seu site com o Edge Delivery Services diretamente no Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md) e entrar em funcionamento usando uma experiência guiada de autoatendimento.

Isso permite uma experiência unificada para todas as propriedades do AEM, garantindo a consistência com todos os workflows críticos, incluindo o gerenciamento de nomes de domínio, o gerenciamento de certificados SSL e os mapeamentos de CDN.

Se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie um email para `aemcs-cmedgedelsvs-program-adopter@adobe.com` do endereço de email associado à sua Adobe ID.

### Certificados validados por domínio (DV)

O Cloud Manager agora permite [o autoatendimento gera e gerencia certificados SSL DV (domain validated).](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md) Isso oferece a solução mais rápida, fácil e econômica para criar um site seguro para sua empresa online.

Se você estiver interessado em testar esse novo recurso e compartilhar seu feedback, envie um email para `Grp-aemcs-dv-dert-adopter@adobe.com` do endereço de email associado à sua Adobe ID.

<!-- RICK: REMOVED THIS SECTION AS PER EMAIL REQUEST TO DL-AEM-DOCS FROM SHWETA DUA, WEDNESDAY, JUNE 12, 2024 ### Client-Side Collection via Real Use Monitoring (RUM) {#rum}

You can leverage the [Real Use Monitoring (RUM) Data Service](/help/implementing/cloud-manager/content-requests.md#cliendside-collection) to enable client-side collection for AEM as a Cloud Service.

Real Use Monitoring (RUM) Data Service offers a more precise reflection of user interactions, ensuring a reliable measure of website engagement. It is a great opportunity to gain advanced insights into your page performance. This is beneficial for customers who use either Adobe-managed CDN or non-Adobe managed CDN. For customers using a non-Adobe managed CDN, automated traffic reporting can now be enabled for them, thus removing the need to share any traffic report with Adobe.

If you are interested in testing this new feature and sharing your feedback, please send an email to `aemcs-rum-adopter@adobe.com` from the email address associated with your Adobe ID. Please include the domain name for production, stage, and dev environments in your email.  Availability of the early adopter program of this feature is limited. -->

### Painel de auditoria de experiência {#experience-audit-dashboard}

[O painel de Auditoria de experiência do Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) O inclui uma exibição de tendências das pontuações de desempenho da página, juntamente com insights e recomendações para ajudar você a melhorá-las. A Auditoria de experiência está incluída como uma etapa no pipeline de produção do Cloud Manager.

O painel usa o Google Lighthouse, uma ferramenta de código aberto e automatizada para melhorar a qualidade dos seus aplicativos web. Você pode executá-lo em qualquer página da Web, público ou que exija autenticação. Ele tem auditorias de desempenho, acessibilidade, aplicativos web progressivos, SEO e muito mais.

Interessado em testar o novo painel? Para começar, envie um email para `aem-lighthouse-pilot@adobe.com` do email associado à Adobe ID.
