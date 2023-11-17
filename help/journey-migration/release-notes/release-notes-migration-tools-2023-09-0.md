---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.09.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.09.0
feature: Release Information
exl-id: 484a60d4-a439-43d6-a23e-4a3b45ef4160
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.09.0 {#release-notes}

Esta página descreve as notas de versão das ferramentas de migração no AEM as a Cloud Service 2022.09.0.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v3.0.0 é 7 de setembro de 2023.

### Novidades {#what-is-new-ctt}

A ferramenta Transferência de conteúdo foi significativamente aprimorada para oferecer os seguintes benefícios:

* Tempo de transferência reduzido ao migrar um subconjunto de um repositório de conteúdo usando o AzCopy para copiar somente as IDs de blob necessárias, em vez de copiar todas as IDs de blob
* Complementos de conteúdo diferencial mais rápidos usando o Oak-upgrade
* Robustez aprimorada ao separar o processo de indexação do processo de assimilação de conteúdo. No caso de uma indexação com falha, o conteúdo não precisará ser assimilado novamente. Somente a indexação será reiniciada automaticamente, economizando tempo e esforço significativos
