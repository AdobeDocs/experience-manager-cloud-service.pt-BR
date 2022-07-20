---
title: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.5.0
description: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.5.0
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
source-git-commit: f84327096951772e1bed8656334841e1292d6bcf
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.5.0 {#release-notes}

Esta página descreve as Notas de versão para as Ferramentas de migração AEM as a Cloud Service 2022.5.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.30 é 1º de junho de 2022.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e relatar o uso de widgets de diálogo personalizados usando widgets de diálogo CoralUI e Classic. É recomendável converter widgets de diálogo clássico personalizados de ExtJS para CoralUI. Os widgets da caixa de diálogo Coral personalizado devem ser atualizados para CoralUI3.
* Capacidade de detectar e gerar relatórios sobre o uso e a versão de Ativos Compartilham Commons. O Asset Share Commons 1.x não é compatível com AEM as a Cloud Service e deve ser atualizado para 2.x.
* Capacidade de detectar e relatar o número de nós de versões.
* Capacidade de detectar e relatar agentes de replicação personalizados ou agentes de replicação prontos para uso que foram modificados.

### Correções de erros {#bug-fixes-bpa}

* O BPA relatava NCC (Alterações não compatíveis), UMI (Problemas de configuração incorreta de atualização) e conclusões PCX (Complexidade de página) que são falsos positivos. Elas foram corrigidas.
* O BPA relatava falhas quando qualquer comprimento de nome de nó excedia 150 bytes. Isso foi corrigido para detectar essas falhas somente quando o caminho pai do nó é igual ou maior que 350 bytes.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta de transferência de conteúdo v2.0.10 é 2 de junho de 2022.

### Novidades {#what-is-new-ctt}

* A Ferramenta de transferência de conteúdo (CTT) foi desenvolvida para funcionar com o Cloud Acceleration Manager para simplificar todo o processo de transferência de conteúdo. A CTT agora se concentra na execução de extrações de conteúdo. O serviço de assimilação de CTT agora está integrado ao Cloud Acceleration Manager. Os benefícios fornecidos por essa evolução são:
   * Maneira de autoatendimento de extrair um conjunto de migração uma vez e assimilá-lo em vários ambientes simultaneamente.
   * Melhoria na experiência do usuário por meio de melhores estados de carregamento, grades de proteção e tratamento de erros.
   * Os logs de assimilação são mantidos e sempre estão disponíveis para solução de problemas.

## Cloud Acceleration Manager {#cam-release}

### Data de lançamento {#release-date-cam}

A data de lançamento do Cloud Acceleration Manager é 2 de junho de 2022.

### Novidades {#what-is-new-cam}

* O Cloud Acceleration Manager agora fornece aos usuários para iniciar e gerenciar transferências de conteúdo para mover o conteúdo de uma instância de AEM do cliente (serviços no local ou Adobe Managed Services) para AEM as a Cloud Service como parte de um projeto de migração. Consulte [Uso do cartão de transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer) para obter mais detalhes.
