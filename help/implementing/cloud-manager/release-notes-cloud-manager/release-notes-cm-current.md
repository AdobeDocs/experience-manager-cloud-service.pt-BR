---
title: Notas de versão do Cloud Manager 2022.3.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2022.3.0 em AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 428bba062fcfb44ebfbbf3c1d05ce1a4634fb429
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---


# Notas de versão do Cloud Manager 2022.3.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2022.3.0 AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager versão 2022.3.0 em AEM as a Cloud Service 10 de março de 2022. A próxima versão está planejada para 7 de abril de 2022.

## Novidades {#what-is-new}

* Um usuário com a **Desenvolvedor** agora pode acessar o log de ambiente AEM.
* [O `reliability_rating` métrica crítica](/help/implementing/cloud-manager/code-quality-testing.md) foi desativado.
* Agora, um usuário pode classificar as colunas na variável **Pipelines** no Cloud Manager.

## Correções de erros {#bug-fixes}

* Um subconjunto de repositórios git criados manualmente tinha valores de nome incorretos que afetavam [o recurso de reuso do artefato de compilação.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) Os nomes desses repositórios foram alterados e os usuários verão o nome corrigido na API/interface do usuário do Cloud Manager.
* [Ao adicionar ou editar um pipeline de qualidade de código,](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) o **Comportamento de falhas importantes da métrica** não são mais exibidas.
* Configurações inesperadas de variável de pipeline não causam mais erros na etapa de build.
