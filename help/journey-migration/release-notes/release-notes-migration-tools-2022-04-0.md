---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.4.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.4.0
feature: Release Information
exl-id: 4941736b-82cd-4050-b3e9-aef250d5c4c7
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2022.4.0 {#release-notes}

Esta página descreve as Notas de versão das Ferramentas de migração no AEM as a Cloud Service 2022.4.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.28 é 22 de abril de 2022.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e relatar o uso de APIs incompatíveis do Asset Manager. Há quatro APIs que não são mais compatíveis com o AEM as a Cloud Service. Os clientes devem garantir que não estejam mais usando essas APIs e devem usar o novo método para fazer upload de ativos.

* Capacidade de detectar o uso de modelos de Fragmento de conteúdo. Os modelos de Fragmento de conteúdo não são mais compatíveis com a criação de novos fragmentos de conteúdo no AEM as a Cloud Service. Os clientes precisam criar modelos de fragmento de conteúdo para substituir os modelos de fragmento de conteúdo.

* Capacidade de detectar ativos com mais de 100 descendentes no nó de metadados do ativo no repositório. É recomendável remover nós de metadados que não são necessários para melhorar o desempenho ao carregar pastas que consistem nesses ativos.

* Capacidade de detectar e relatar o tipo de armazenamento de dados usado.

* Padrão atualizado para o portal de formulários AEM.

### Correções de erros {#bug-fixes-bpa}

* O BPA relatava os resultados dos componentes principais, em vez de relatar apenas os componentes do cliente. Isso foi corrigido.
