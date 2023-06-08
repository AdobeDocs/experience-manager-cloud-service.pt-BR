---
title: Notas de versão do Cloud Manager 2023.6.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2023.6.0 no AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 80a5f58119dc304161d324491cd65c50e981ccd4
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 37%

---


# Notas de versão do Cloud Manager 2023.6.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2023.6.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager versão 2023.6.0 no AEM as a Cloud Service é 8 de junho de 2023. A próxima versão está planejada para 6 de julho de 2023.

## Novidades {#what-is-new}

* Ao criar um novo [programa ou ambiente,](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) o nome agora está restrito a aceitar apenas caracteres alfanuméricos e um conjunto limitado de caracteres especiais.
* Ao retomar uma [pipeline de produção,](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) uma caixa de diálogo de confirmação agora é exibida na etapa aprovar.
* Para o **[Testes funcionais do cliente](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)** e **[Testes de interface do usuário personalizados](/help/implementing/cloud-manager/ui-testing.md)** etapas do pipeline, um novo `INCOMPLETE` O status agora é possível, o que indica que esses testes não estavam presentes e, portanto, não foram executados.
   * Nesses casos, o pipeline não falha e avança para a próxima etapa.

## Correções de erros {#bug-fixes}

* A variável [pipeline de configuração no nível da web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) O não está mais ativado incorretamente para programas exclusivos ao Assets.
* Validação mais robusta foi adicionada para evitar determinados tipos de falhas durante o provisionamento do ambiente.
