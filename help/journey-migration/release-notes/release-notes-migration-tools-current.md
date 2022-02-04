---
title: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.2.0
description: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.2.0
feature: Release Information
source-git-commit: 8876702f1a172282fd1ff46387ade2a45e187fed
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 7%

---


# Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.2.0 {#release-notes}

Esta página descreve as Notas de versão para as Ferramentas de migração AEM as a Cloud Service 2022.2.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.24 é 1 de fevereiro de 2022.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e relatar o número de ativos com e sem Tags inteligentes.
* Capacidade de detectar e relatar a versão do Componente principal usado.
* Capacidade de detectar e gerar relatórios sobre o tipo de camada de origem (Autor ou Publicação) em que o BPA foi executado.

### Correções de erros {#bug-fixes-bpa}

* A lógica de dimensionamento de BPA ficou mais rápida e eficiente.
* Em alguns cenários, o BPA não incrementou a contagem analisada quando foi executado. Isso foi corrigido.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta Transferência de conteúdo v1.8.6 é 3 de fevereiro de 2022.

### Novidades {#what-is-new-ctt}

* Validação de conteúdo - os usuários podem determinar de forma confiável se todo o conteúdo que foi extraído pela ferramenta Transferência de conteúdo foi assimilado com êxito na instância de destino. Para usar esse recurso, será necessário ativá-lo no `System Console` do ambiente de AEM de origem. Consulte [Validação de transferências de conteúdo - Introdução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) para obter mais detalhes.

### Correções de erros {#bug-fixes-ctt}

* Alguns usuários não foram mapeados porque o Mapeamento de usuários diferenciava maiúsculas de minúsculas. Isso foi corrigido. O Mapeamento de Usuário não diferencia mais maiúsculas de minúsculas.

