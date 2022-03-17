---
title: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.3.0
description: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.3.0
feature: Release Information
source-git-commit: c497424271ea960d22a30b4a6c66432935ec820d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 7%

---


# Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.3.0 {#release-notes}

Esta página descreve as Notas de versão para as Ferramentas de migração AEM as a Cloud Service 2022.3.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.26 é 16 de março de 2022.

### Novidades {#what-is-new-bpa}

* Capacidade para detectar ativos não processados. Se os ativos não processados forem detectados, esses ativos precisarão ser definidos como processados ou precisam ser removidos do conjunto de migração durante a transferência de conteúdo para evitar problemas durante a assimilação de conteúdo.
* Capacidade de detectar se o conteúdo tem mais de 1000 URLs personalizadas. Usar um alto número de URLs personalizadas não é a prática recomendada, pois coloca uma carga nos servidores do Dispatcher e do Publish.
* Capacidade de identificar problemas relacionados às definições do índice Oak e detectar incompatibilidades com AEM as a Cloud Service.
* Capacidade de detectar e relatar o uso de configurações do Externalizador. AEM configurações as a Cloud Service do Externalizador são definidas pelo Cloud Manager, portanto, as configurações existentes do Externalizador precisam ser refatoradas para manter a compatibilidade.

### Correções de erros {#bug-fixes-bpa}

* Em alguns cenários, o BPA falhou ao ser executado por causa do FormsSelectiveFeaturesAnalysis, gerando um erro de asserção. Isso foi corrigido.
* O BPA estava relatando conclusões relacionadas ao padrão WRK como MAJOR em vez de CRÍTICO. Isso foi corrigido.
* O BPA relatava incorretamente as conclusões relacionadas às definições do índice OAK em ui.apps como CRÍTICO. Isso foi corrigido.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta Transferência de conteúdo v1.9.0 é 28 de fevereiro de 2022.

### Novidades {#what-is-new-ctt}

* Verificar medidas de proteção - O recurso Tamanho da verificação da ferramenta Transferência de conteúdo ajuda a reduzir transferências de conteúdo com falha.  Com o recurso Verificar tamanho, os usuários podem 1) determinar se têm espaço em disco suficiente no `crx-quickstart` subdiretório antes da extração e 2) estime o tamanho do conjunto de migração e verifique se ele é compatível. Se uma ou ambas as verificações forem violadas, os usuários verão avisos na interface do usuário da CTT. Com essa garantia, você pode evitar falhas de transferência de conteúdo e discutir proativamente as opções de migração com o Atendimento ao cliente do Adobe. Consulte [Determinando o tamanho e o espaço em disco do conjunto de migração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) para obter mais detalhes.