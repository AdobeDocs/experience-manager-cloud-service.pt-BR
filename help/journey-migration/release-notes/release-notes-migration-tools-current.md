---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.03.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.03.0
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: 5815dacd2806cc7886aa0c7c5c9fd329306b3e1b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 15%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.03.0 {#release-notes}

Esta página descreve as notas de versão das ferramentas de migração no AEM as a Cloud Service 2022.03.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.40 é 03 de março de 2023.

### Novidades {#what-is-new-bpa}

* Agora, o BPA pode detectar e gerar relatórios sobre nós conflitantes - nós com o mesmo `jcr:uuid`. Essas descobertas são sinalizadas como críticas, pois podem levar a falhas de assimilação de conteúdo ao mover o conteúdo para o AEM as a Cloud Service.
* O BPA agora pode detectar e relatar o uso de Ouvintes de eventos. É recomendável refatorar esse tipo de mecanismo de tratamento de eventos para trabalhos do sling ao mudar para o AEM as a Cloud Service.

### Correções de erros {#bug-fixes-bpa}

* O BPA relatava falsos positivos no `grouprendercondition`. Isso foi corrigido.