---
title: Visão geral do sistema AEM
description: Visão geral do sistema AEM
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 3%

---


# Visão geral do sistema AEM {#aem-system}

Esta página descreve a Visão geral do sistema do Adobe Experience Manager (AEM).

## Segundo plano {#background}

Esse padrão é usado para identificar informações gerais que fornecem uma visão geral do sistema AEM. As informações podem incluir itens como:

Versão do AEMproducts do AEM usados (sites, ativos, formulários etc.)Contagem de nós (páginas, ativos etc.)

## Dados de padrão {#pattern-data}

Os seguintes objetos estão incluídos na representação JSON do padrão:

* **item.message**: refere-se à mensagem do padrão.
* **item.context**: consulte as informações adicionais sobre a visão geral:
   * *tipo*: O tipo de dados de contexto, &quot;aem.version&quot;, &quot;aem.product&quot; ou &quot;node.count&quot;.
   * *dados*: Um objeto JSON que contém os dados correspondentes ao tipo: &quot;version&quot; (string), &quot;product&quot; (string) ou &quot;count&quot; (integer).

### Possíveis implicações e riscos {#possible-implications}

Não aplicável.

### Soluções possíveis  {#possible-solutions}

Não aplicável.
