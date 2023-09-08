---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.07.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.07.0
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 1f01408223a661c0149d959b1901293dc91ed7ee
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 7%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.07.0 {#release-notes}

Esta página descreve as notas de versão das ferramentas de migração no AEM as a Cloud Service 2022.07.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.42 é 6 de julho de 2023.

### Novidades {#what-is-new-bpa}

* Vários padrões de práticas recomendadas foram adicionados a esta versão do Analisador de práticas recomendadas. Dentre elas:
   * Identificação da configuração mínima da tarefa de manutenção
   * Detecção de consultas longas/pesadas
   * Detecção de um alto número de fluxos de trabalho do autor em estado de execução ou obsoleto
   * Detecção da configuração do trabalho OSGI Apache Sling
   * Detecção de Guava-caches personalizados

### Correções de erros {#bug-fixes-bpa}

* O BPA foi aprimorado para evitar falhas de geração de relatório de memória insuficiente para relatórios com um alto número de conclusões.
* O BPA foi aprimorado para detectar caracteres de escape em caminhos para evitar falhas de assimilação de conteúdo ao migrar o conteúdo para o AEM as a Cloud Service.
