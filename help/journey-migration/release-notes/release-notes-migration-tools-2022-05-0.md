---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.5.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.5.0
feature: Release Information
exl-id: 1aa49e85-1914-44d9-bcf7-0a1b03926df0
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.5.0 {#release-notes}

Esta página descreve as notas de versão das ferramentas de migração no AEM as a Cloud Service 2022.5.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.30 é 1º de junho de 2022.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e relatar o uso de dispositivos de diálogo personalizados usando CoralUI e dispositivos de diálogo clássicos. É recomendável converter widgets de diálogo clássicos personalizados de ExtJS para CoralUI. Os Dispositivos de diálogo Coral personalizados devem ser atualizados para CoralUI3.
* Capacidade de detectar e relatar o uso e a versão do Assets Share Commons. O Asset Share Commons 1.x não é compatível com o AEM as a Cloud Service e deve ser atualizado para a versão 2.x.
* Capacidade de detectar e relatar o número de nós das versões.
* Capacidade de detectar e emitir relatórios sobre agentes de replicação personalizados ou agentes de replicação prontos para uso que foram modificados.

### Correções de erros {#bug-fixes-bpa}

* O BPA relatava conclusões NCC (alterações não compatíveis), UMI (problema de erro de configuração de atualização) e PCX (complexidade da página) que são falsos positivos. Elas foram corrigidas.
* O BPA relatava falhas quando qualquer comprimento de nome de nó excedia 150 bytes. Isso foi corrigido para detectar essas falhas somente quando o caminho principal do nó é igual ou maior que 350 bytes.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v2.0.10 é 2 de junho de 2022.

### Novidades {#what-is-new-ctt}

* A ferramenta de transferência de conteúdo (CTT) foi desenvolvida para funcionar com o Cloud Acceleration Manager para simplificar todo o processo de transferência de conteúdo. A CTT agora se concentra em executar extrações de conteúdo. O serviço de assimilação de CTT agora está integrado ao Cloud Acceleration Manager. Os benefícios fornecidos por meio dessa evolução são:
   * Forma de autoatendimento para extrair um conjunto de migração uma vez e assimilá-lo em vários ambientes simultaneamente.
   * Experiência do usuário aprimorada por meio de melhores estados de carregamento, medidas de proteção e manipulação de erros.
   * Os registros de assimilação são mantidos e estão sempre disponíveis para solução de problemas.

## Cloud Acceleration Manager {#cam-release}

### Data de lançamento {#release-date-cam}

A data de lançamento do Cloud Acceleration Manager é 2 de junho de 2022.

### Novidades {#what-is-new-cam}

* O Cloud Acceleration Manager agora fornece aos usuários iniciar e gerenciar transferências de conteúdo para mover o conteúdo da instância do AEM de um cliente (No local ou Adobe Managed Services AEM as a Cloud Service) para o como parte de um projeto de migração. Consulte [Usar o cartão de transferência de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer) para obter mais detalhes.
