---
title: Personalização detectada
description: Personalização detectada
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 3%

---


# Personalização detectada {#cust-pattern}

Esta página descreve o código de padrão Detectado por Personalização.

## Segundo plano {#background}

Esse código de padrão é usado para identificar personalizações que foram feitas para a instância do AEM. Como a personalização do AEM é comum, esse padrão não indica necessariamente que há um problema. Ele identifica um registro de personalizações para que possam ser avaliadas em relação ao seu impacto nos planos de atualização.

As personalizações detectadas incluem:

* Código do cliente (pacotes) e configurações
* Pacotes de terceiros
* Integrações com serviços de terceiros
* Índices Oak não padrão

## Dados de padrão {#pattern-data}

Os seguintes objetos estão incluídos na representação JSON do padrão:

* **item.message**: refere-se à mensagem do padrão.
* **item.context**: consulte as informações adicionais sobre a visão geral:
   * *tipo*: customization.detected.
   * *dados*: Um objeto JSON que contém os dados que descrevem a personalização

### Possíveis implicações e riscos {#possible-implications}

Não aplicável.

### Soluções possíveis  {#possible-solutions}

Não aplicável.
