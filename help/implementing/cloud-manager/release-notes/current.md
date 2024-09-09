---
title: Notas de versão do Cloud Manager 2024.9.0 no Adobe Experience Manager as a Cloud Service
description: Saiba mais sobre as notas de versão do Cloud Manager 2024.9.0 no AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: cfaa3be31195929b80310610120a779a20537c61
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 13%

---

# Notas de versão do Cloud Manager 2024.9.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2024.9.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte as [notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager versão 2024.9.0 no AEM as a Cloud Service é 5 de setembro de 2024. A próxima versão está planejada para sexta-feira, 3 de outubro de 2024.

## Novidades {#what-is-new}

* **Painel de Auditoria de Experiência:**

  O [painel aprimorado da Auditoria de experiência](/help/implementing/cloud-manager/experience-audit-dashboard.md) do Adobe Cloud Manager, viabilizado pelo Google Lighthouse, fornece informações sobre a qualidade e o desempenho do AEM Sites, avaliando os principais sinais vitais da Web, SEO e métricas de acessibilidade. Ele ajuda os usuários a identificar áreas a serem aprimoradas, oferecendo recomendações acionáveis, permitindo que as equipes melhorem a experiência do usuário, os tempos de carregamento da página e a conformidade do site. Esse painel simplifica o monitoramento de métricas críticas do site e garante que os aplicativos AEM atendam a altos padrões de desempenho e acessibilidade.

* **Certificados de Validação de Domínio gerados e gerenciados por Adobe:**

  Com o Cloud Manager, agora é possível [usar o autoatendimento de certificados SSL de DV (Validação de Domínio) gerados e gerenciados pelo Adobe](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). Esse recurso oferece a solução mais rápida, fácil e econômica para criar um site seguro para sua organização ou empresa online. <!-- CMGR-52403 -->

* Suporte a **Edge Delivery Services no Cloud Manager:**

  Se você tiver uma licença do Edge Delivery Services como parte do AEM Sites, [você pode agora integrar seu site com o Edge Delivery Services diretamente pelo Cloud Manager](/help/implementing/cloud-manager/edge-delivery-services.md). Esse recurso permite uma experiência de ativação guiada e de autoatendimento. Ele também unifica fluxos de trabalho essenciais, como gerenciamento de nomes de domínio, certificados SSL e mapeamentos de CDN, em todas as propriedades AEM, garantindo consistência e eficiência. <!-- CMGR-49859 -->

* Os clientes que usam repositórios GitHub agora podem criar e usar pipelines de configuração no nível da Web. <!--( KEEP IN? SP: YES CMGR-59046 and Slack https://cq-dev.slack.com/archives/C07LFP5BZ2L/p1725407057847379 ) -->

<!--
## Early adoption program {#early-adoption}

For a chance to test some upcoming features, be a part of Adobe's early adoption program. -->


## Correções de erros

* A paginação para a exibição de tabela de certificados SSL agora funciona conforme esperado. <!-- (CMGR-60804 - [UI] Pagination doesn't work for ssl certificates) -->
* A versão incorreta do artefato foi promovida ao usar o botão **Promover Compilação** de uma execução. <!-- ( KEEP IN? SP: YES CMGR-59519 and Slack https://cq-dev.slack.com/archives/C07LFPN2R08/p1725408253474129 ) -->

<!-- * Slack message says next release? SP: REMOVE (Leave in for now) SSL Certificates table in Cloud Manager now enables pagination in the user experience. ( https://jira.corp.adobe.com/browse/CMGR-61041 and Slack https://cq-dev.slack.com/archives/C07LFRE9QJU/p1725408553760009 ) --<>
