---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2024.05.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2024.05.0
feature: Release Information
role: Admin
exl-id: f50a74fa-ad7d-4837-b0a1-9945c32af02f
source-git-commit: 3b2ed44b438fe8587a9b9603ddfacc41111fb903
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 6%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2024.05.0 {#release-notes}

Esta página descreve as Notas de versão das Ferramentas de migração no AEM as a Cloud Service 2024.05.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.50 é maio de 2024.

### Novidades {#what-is-new-bpa}

* O Analisador de práticas recomendadas (BPA) agora é compatível com o upload automático de relatórios gerados por BPA diretamente para o Cloud Acceleration Manager (CAM). Os usuários não precisarão mais baixar manualmente o relatório e carregá-lo no CAM. Para obter mais detalhes, consulte [Usando o Analisador de Práticas Recomendadas](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md)

### Correções de erros {#bug-fixes-bpa}

* O Analisador de práticas recomendadas agora detecta todos os nós maiores que 16 MB
* Condição de raça que causa ocorrências esporádicas de achados NCC corrigidos.

## Cloud Acceleration Manager {#cam-release}

### Novidades {#what-is-new-cam}

* O Cloud Acceleration Manager (CAM) agora é compatível com o upload automático de relatórios gerados pelo BPA diretamente para o CAM. Para saber mais, consulte [Fase de preparação no Cloud Acceleration Manager - Utilização do Cartão de Análise de Práticas Recomendadas](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#best-practices-analysis)

* O Cloud Acceleration Manager agora fornece uma estimativa de quanto tempo uma assimilação pode levar, determinados fatores, como contagem de nós, tamanho do armazenamento de dados etc. Saiba mais com [Assimilar conteúdo no Cloud Service](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md)
