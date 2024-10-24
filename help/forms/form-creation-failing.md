---
title: Como solucionar falhas de criação de formulários?
description: Solução de problemas de falhas na criação de formulários no ambiente as a Cloud Service do AEM Forms.
feature: Adaptive Forms
role: User
exl-id: 169ea727-0941-4a1d-bc33-d9fe208b27ab
source-git-commit: 0b693cb51a96011235fa87a5899426c6b0c2509a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Problema ao publicar formulários{#form-creation-fails}

Depois que os usuários atualizarem para a versão as a Cloud Service do AEM Forms `2024.5.16461`:

**Alguns usuários** podem enfrentar problemas ao criar formulários. O problema é que, quando um usuário cria um formulário, a seguinte mensagem de erro aparece na caixa de diálogo de criação:

`A server error occurred. Try again after sometime.`

## Causa {#cause-form-creation-fails}

O problema ocorre porque o autor publica o formulário sem **publicar primeiro o modelo** usado nele. Isso resulta na adição de `jcr:uuid` e outras propriedades protegidas e geradas pelo sistema ao nó `<template-path>/initial/jcr:content`, causando falhas na criação subsequente do formulário.

## Solução alternativa {#resolution-form-creation-fails}

Para resolver o problema, execute as seguintes etapas:

1. Certifique-se de que o modelo usado no formulário não tenha o `jcr:uuid` e outras propriedades protegidas geradas pelo sistema no caminho `<template-path>/initial/jcr:content node`.
1. Publish o modelo usando explicitamente o console de modelo.
1. Agora, quando o modelo for publicado, tente criar novos formulários usando o modelo.
1. Se o modelo usado for atualizado nas próximas versões, Publish o modelo novamente (conforme fornecido na etapa 2) para evitar problemas de falha na criação de formulários.


<!--

# Issue {#form-creation-fails}

After updating to AEM Forms as a Cloud Service version `2024.5.16461.20240524T172309Z`, When a user publishes a form using an unpublished template, it fails to create a form and shows an error:

`Property is protected: jcr:uuid = 09e0d6be-f619-4405-b021-27eb1c5326d3`

## Solution {#troubleshoot-form-creation-fails}

To resolve the issue, perform the following workaround steps:

1. Publish the template explicitly using the template console.
    
    >[!NOTE]
    > Prior to this step ensure that the (unpublished) template does not have `jcr:uuid` and other system generated properties under the initial content's `jcr:content node`. To sort out it, first, sanitize the template to publish it explicitly.

    >[!NOTE]
    > This action doesn't replicate the initial content node.
1. Now, when your template is published, try creating new forms using the template.
1. If the template is changed in the future, publish it again as mentioned in the step 1.

-->
