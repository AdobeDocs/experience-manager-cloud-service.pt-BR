---
title: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.4.0
description: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.4.0
feature: Release Information
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 5%

---

# Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2022.4.0 {#release-notes}

Esta página descreve as Notas de versão para as Ferramentas de migração AEM as a Cloud Service 2022.4.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.28 é 22 de abril de 2022.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e relatar o uso de APIs não compatíveis do Asset Manager. Há quatro APIs que não são mais suportadas em AEM as a Cloud Service. Os clientes devem garantir que não estejam mais usando essas APIs e devem usar o novo método de upload de ativos.

* Capacidade de detectar o uso de modelos de Fragmento de conteúdo. Os modelos de Fragmento de conteúdo não são mais compatíveis com a criação de novo fragmento de conteúdo AEM as a Cloud Service. Os clientes precisarão criar modelos de fragmento de conteúdo para substituir os modelos de fragmento de conteúdo.

* Capacidade de detectar ativos com mais de 100 descendentes no nó de metadados do ativo no repositório. É recomendável remover nós de metadados que não são necessários para melhorar o desempenho ao carregar pastas que consistem em tais ativos.

* Capacidade de detectar e relatar o tipo de armazenamento de dados usado.

* Padrão atualizado para AEM Portal de Formulários.

### Correções de erros {#bug-fixes-bpa}

* O BPA gerava relatórios de descobertas de componentes principais em vez de relatórios apenas de componentes do cliente. Isso foi corrigido.