---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.1.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.1.0
feature: Release Information
exl-id: cbd0c316-bda3-48fb-89d6-a8f97bad1970
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.1.0 {#release-notes}

Esta página descreve as notas de versão das ferramentas de migração no AEM as a Cloud Service 2022.1.0.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v1.7.18 é 18 de janeiro de 2022.

### Novidades {#what-is-new-ctt}

* Alternância adicionada à fase de extração na ferramenta Transferência de conteúdo para permitir que os usuários desativem o [pré-cópia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html) durante a extração. Para obter as velocidades de extração ideais, a pré-cópia durante a extração deve ser desativada para pequenos conjuntos de migração ou se apenas alguns blobs tiverem sido adicionados desde a última extração.

### Correções de erros {#bug-fixes-ctt}

* Configurações padrão atualizadas para reduzir os tempos limite de execução durante a extração.
