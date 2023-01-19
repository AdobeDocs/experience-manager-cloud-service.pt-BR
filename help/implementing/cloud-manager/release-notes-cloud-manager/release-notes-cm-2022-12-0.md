---
title: Notas de versão do Cloud Manager 2022.12.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2022.12.0 no AEM as a Cloud Service.
feature: Release Information
source-git-commit: 5877f3c84ab6303520dd4697144e9b18d717b74f
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 48%

---


# Notas de versão do Cloud Manager 2022.12.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2022.12.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento da versão 2022.12.0 do Cloud Manager AEM as a Cloud Service é 29 de novembro de 2022. A próxima versão está planejada para 19 de janeiro de 2023.

## Novidades {#what-is-new}

* Notificações para [Atualizações de manutenção de AEM](/help/overview/what-is-new-and-different.md#aem-updates) será exibida na interface do usuário do Cloud Manager. Essa alteração será implementada em fases nas semanas após a versão 2022.12.0.
* Quando uma ingestão por meio do [Ferramenta de transferência de conteúdo (CTT)](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md) estiver em andamento, o status do ambiente no console do desenvolvedor e no Cloud Manager será exibido como `Ingestion in Progress`.
* Melhorias na disponibilidade e confiabilidade dos [pipelines do Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) foram feitas.

## Correções de erros {#bug-fixes}

* Foi efetuada uma alteração para evitar [Gasodutos front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) da execução enquanto uma execução de pipeline está em andamento no mesmo ambiente.
* Foi efetuada uma alteração para evitar uma `PATCH /program//environment//variables` solicitação para ambientes com o `FAILED` status.
