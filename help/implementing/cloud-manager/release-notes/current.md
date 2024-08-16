---
title: Notas de versão do Cloud Manager 2024.8.0 no Adobe Experience Manager as a Cloud Service
description: Saiba mais sobre as notas de versão do Cloud Manager 2024.8.0 no AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: a823bcd1461b847983d0243cd9abd59efd8d7b6f
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 14%

---


# Notas de versão do Cloud Manager 2024.8.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2024.8.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager 2024.8.0 no AEM as a Cloud Service é quinta-feira, 14 de agosto de 2024. A próxima versão está planejada para 14 de setembro de 2024.

## Novidades {#what-is-new}

* [Regiões de publicação adicionais](/help/operations/additional-publish-regions.md) e um [99.99% SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla) (Contrato de Nível de Serviço) agora estão disponíveis para o AEM Forms as a Cloud Service.
   * Esse aprimoramento permite que você obtenha SLAs mais altos com mais tempo de atividade e menos latência, garantindo as melhores experiências para seus usuários distribuídos globalmente.

## Programa de adoção antecipada {#early-adoption}

Para testar alguns recursos futuros, faça parte do programa de adoção antecipada do Adobe.

### Suporte para Edge Delivery Services no Cloud Manager {#edge-delivery-services}

Se você tiver licenciado Edge Delivery Services como parte do AEM Sites, [você pode agora integrar seu site com Edge Delivery Services diretamente no Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md) e ativar usando uma experiência guiada de autoatendimento.

Esse recurso fornece uma experiência unificada para todas as propriedades do AEM. Ele garante a consistência em fluxos de trabalho críticos, como gerenciamento de nomes de domínio, gerenciamento de certificados SSL e mapeamentos de CDN.

Se você estiver interessado em testar este novo recurso e compartilhar seus comentários, envie um email para `aemcs-cmedgedelsvs-program-adopter@adobe.com` a partir do endereço de email associado à sua Adobe ID.

### Certificados de domínio validado (DV)

Com o Cloud Manager, agora é possível [gerar e gerenciar certificados SSL de domínio validado (DV) por autoatendimento](/help/implementing/cloud-manager/managing-ssl-certifications/domain-validated-certificates.md). Esse recurso oferece a solução mais rápida, fácil e econômica para criar um site seguro para sua empresa online.

Se você quiser testar esse novo recurso e fornecer seu feedback, envie um email para `Grp-aemcs-dv-dert-adopter@adobe.com` usando o endereço de email vinculado à sua Adobe ID.

### Painel de auditoria de experiência {#experience-audit-dashboard}

[O painel de Auditoria de Experiência do Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) inclui uma exibição de tendências das pontuações de desempenho da página, juntamente com insights e recomendações para ajudá-lo a melhorá-las. A Auditoria de experiência está incluída como uma etapa no pipeline de produção do Cloud Manager.

O painel usa o Google Lighthouse, uma ferramenta de código aberto e automatizada para melhorar a qualidade dos seus aplicativos web. Você pode usá-lo para auditar qualquer página da Web, seja pública ou que exija autenticação. Ele fornece avaliações de desempenho, acessibilidade, aplicativos web progressivos, SEO e muito mais.

Quer experimentar o novo painel? Para começar, envie um email para `aem-lighthouse-pilot@adobe.com` usando o email vinculado à sua Adobe ID.

## Correção de erros

* Um problema raro foi corrigido em que as etapas do pipeline eram executadas após a exclusão do pipeline.
* Correção de um problema com pipelines de configuração mostrando incorretamente um status `FAILED` em casos raros.
