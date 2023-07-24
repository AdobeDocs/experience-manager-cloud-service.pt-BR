---
title: Notas de versão do Cloud Manager 2023.7.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2023.7.0 no AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 2721cb20083eeda7546513817f1ddfe12e9cb43a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 38%

---


# Notas de versão do Cloud Manager 2023.7.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2023.7.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager 2023.7.0 no AEM as a Cloud Service é 29 de junho de 2023. A próxima versão está planejada para 10 de agosto de 2023.

## Novidades {#what-is-new}

* Os cartões na página de destino do Cloud Manager agora indicam se a [segurança aprimorada](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) está habilitada para os programas.
* Se um desenvolvimento [pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) não contém etapas de teste, os usuários agora têm a opção de incluir etapas de teste quando [inicie o pipeline.](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)
   * Isso será implementado em fases.
* Quando [cancelamento da execução,](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) a etapa aprovação da execução do pipeline agora solicita que o usuário forneça um motivo para o cancelamento.
   * Isso será implementado em fases.
* Os usuários agora podem acessar o [logs do processo de cópia de conteúdo.](/help/implementing/developing/tools/content-copy.md#accessing-logs)
   * Essa opção só estará disponível se os ambientes de origem e de destino estiverem na versão AEM `2023.7.12549` ou superior.

## Correções de erros {#bug-fixes}

* Navegar até a interface de criação no Cloud Manager não falha mais no redirecionamento para o Unified Shell após o logon.
* A edição da data de publicação por meio do widget de publicação agora navega até o **Go Live** em vez da guia **Segurança aprimorada** guia.
* Ao iniciar uma operação de cópia, o usuário não poderá mais selecionar um ambiente em que uma operação de cópia já tenha sido chamada.
