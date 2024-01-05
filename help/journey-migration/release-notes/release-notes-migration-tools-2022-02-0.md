---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.2.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.2.0
feature: Release Information
exl-id: b1cd871d-c71e-4902-a97e-2c859f6a4da4
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 55%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.2.0 {#release-notes}

Esta página descreve as notas de versão das ferramentas de migração no AEM as a Cloud Service 2022.2.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.24 é 1º de fevereiro de 2022.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e gerar relatórios sobre o número de ativos com e sem Tags inteligentes.
* Capacidade de detectar e gerar relatórios sobre a versão do Componente principal usada.
* Capacidade de detectar e gerar relatórios sobre o tipo de camada de origem (Autor ou Publicação) em que o BPA foi executado.

### Correções de erros {#bug-fixes-bpa}

* A lógica de dimensionamento de BPA ficou mais rápida e eficiente.
* Em alguns cenários, o BPA não incrementou a contagem analisada quando foi executado. Isso foi corrigido.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v1.8.6 é 3 de fevereiro de 2022.

### Novidades {#what-is-new-ctt}

* Validação de conteúdo - os usuários podem determinar com confiança se todo o conteúdo que foi extraído pela ferramenta Transferência de conteúdo foi assimilado com êxito na instância de destino. Para usar esse recurso, ative-o na `System Console` do ambiente AEM de origem. Consulte [Validação de transferências de conteúdo - Introdução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html#getting-started) para obter mais detalhes.

### Correções de erros {#bug-fixes-ctt}

* Alguns usuários não foram mapeados porque o mapeamento de usuários diferenciava letras maiúsculas de letras minúsculas. Isso foi corrigido. O mapeamento de usuário não diferencia mais letras maiúsculas de letras minúsculas.
