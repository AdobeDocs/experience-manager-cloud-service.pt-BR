---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.3.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.3.0
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 86%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.3.0 {#release-notes}

Esta página descreve as notas de versão das ferramentas de migração no AEM as a Cloud Service 2022.3.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.26 é 16 de março de 2022.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar ativos não processados. Se ativos não processados forem detectados, precisarão ser definidos como processados ou removidos do conjunto de migração durante a transferência de conteúdo para evitar problemas durante a assimilação de conteúdo.
* Capacidade de detectar se o conteúdo tem mais de 1.000 URLs personalizados. Usar um alto número de URLs personalizados não é uma prática recomendada, pois coloca uma carga nos servidores do Dispatcher e do Publish.
* Capacidade de identificar problemas relacionados às definições de índice do Oak e de detectar incompatibilidades com o AEM as a Cloud Service.
* Capacidade de detectar e relatar o uso de configurações do Externalizador. No AEM as a Cloud Service, as configurações do Externalizador são definidas pelo Cloud Manager, portanto, as configurações existentes precisam ser alteradas para manter a compatibilidade.

### Correções de erros {#bug-fixes-bpa}

* Em alguns cenários, o BPA falhou ao ser executado por causa do FormsSelectiveFeaturesAnalysis, que gerou um erro de assertiva. Isso foi corrigido.
* O BPA relatava conclusões relacionadas ao padrão WRK como GRAVE em vez de CRÍTICA. Isso foi corrigido.
* O BPA relatava incorretamente as conclusões relacionadas às definições de índice do OAK em ui.apps como CRÍTICA. Isso foi corrigido..

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da Ferramenta de transferência de conteúdo v1.9.0 é 28 de fevereiro de 2022.

### Novidades {#what-is-new-ctt}

* Proteções de verificação de tamanho - O recurso de verificação de tamanho da Ferramenta de transferência de conteúdo ajuda a reduzir as falhas nas transferências de conteúdo. Com o recurso de verificação de tamanho, os usuários podem: 1) determinar se têm espaço em disco suficiente no subdiretório `crx-quickstart` antes da extração e 2) estimar o tamanho do conjunto de migração e verificar se ele é compatível. Se uma ou ambas as verificações forem violadas, os usuários verão avisos na interface da ferramenta de transferência de conteúdo (CTT). Com essa proteção, é possível evitar falhas de transferência de conteúdo e discutir proativamente as opções de migração com o Atendimento ao cliente da Adobe. Consulte [Determinar o tamanho do conjunto de migração e o espaço em disco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=pt-BR#migration-set-size) para obter mais detalhes.
