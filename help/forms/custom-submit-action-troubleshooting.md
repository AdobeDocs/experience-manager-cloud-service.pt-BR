---
title: Solução de problemas de erro 502 na ação de envio personalizada do Adaptive Forms
description: Saiba como identificar e resolver páginas de erro 502 que ocorrem ao usar ações de envio personalizadas no Adaptive Forms (Componentes principais). Este guia explica as causas comuns, como exceções não tratadas, e fornece etapas de resolução.
feature: Adaptive Forms, Core Components
role: Developer
level: Intermediate
badgeSaas: label="AEM Forms" type="Positive" tooltip="Aplicável ao AEM Forms)."
exl-id: a7469926-7059-4aca-90ff-2554d14c3944
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 2%

---

# Solução de problemas: página de erro 502 na ação de envio personalizada

Ao trabalhar com o Adaptive Forms (Componentes principais), você pode encontrar uma **página de erro 502 do HTML** após enviar um formulário que usa uma ação de envio personalizada.

## Problema

**Erro:** uma página de erro 502 do HTML é exibida quando um serviço de ação de envio personalizado falha.

**Motivo:** isso acontece se a ação de envio personalizada lançar um erro sem tratamento, por exemplo, ponteiro nulo, resposta de API inválida ou falha de tempo de execução.

## Resolução

Para evitar a página de erro 502, envolva a lógica de envio com blocos try-catch para lidar com erros normalmente.

Para obter etapas detalhadas, consulte [Criar uma ação de envio personalizada para o Forms Adaptável (Componentes Principais)](/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md).
