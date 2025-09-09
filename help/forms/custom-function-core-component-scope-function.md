---
title: Introdução a objetos de escopo em funções personalizadas
description: Form suporta objetos de escopo em funções personalizadas que são passadas como um último argumento para funções quando a regra é executada.
keywords: objetos de escopo em funções personalizadas, objetos globais, objetos de campo.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 248c75a5-6335-41d2-aa0a-28a20a710f88
source-git-commit: e2bc958104bd9b75845ad2c213eec18d2560a3a4
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Objeto de escopo em funções personalizadas

No Adaptive Forms, um objeto de escopo é passado como o último argumento para funções quando uma regra é executada. Ela pode ser usada para ler propriedades de formulário/campo e modificar o formulário de dentro das funções. O objeto de escopo contém um objeto proxy somente leitura para o formulário, o evento acionado e o campo de destino. As propriedades de formulário e campo podem ser acessadas usando o objeto de escopo com o anexo `$`, por exemplo, `scope.form.$id` e `scope.field.$id`, respectivamente.

## Funções de modificação de formulário usando o objeto de escopo

O objeto de escopo tem as seguintes funções para modificação de formulário:

| Função | Sintaxe | Descrição | Exemplo de código |
|-----------------|--------|-------------|-------------|
| **setProperty** | `setProperty(any $element, any $payload)` | Define uma propriedade no campo de destino usando o `$payload`. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule) para exibir o exemplo. |
| **validar** | `validate([any $element])` | Executa a validação no campo de destino. Executa a validação em todo o formulário se nenhum destino for fornecido e retorna uma matriz de erros de validação. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#validate-the-field) para exibir o exemplo. |
| **redefinir** *(obsoleto)* | `reset([any $element])` | Obsoleto. Em vez disso, use `dispatchEvent($target, 'reset')`. Redefine o campo de destino ou, se nenhum destino for fornecido, redefine todo o formulário. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel) para exibir o exemplo. |
| **importData** | `importData(any $payload)` | Importa dados para o formulário, substituindo quaisquer dados de formulário existentes. Se `qualifiedName` for especificado, os dados serão importados somente para esse campo de container. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads) para exibir o exemplo. |
| **exportData** | `exportData()` | Retorna os dados do formulário. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) para exibir o exemplo. |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | Aciona o envio de um formulário. Você pode especificar o que enviar por meio do parâmetro `$payload` e definir o tipo de conteúdo por meio do parâmetro `$contentType`. Os dados são enviados como `multipart/form-data` por padrão. O parâmetro `$validateForm` opcional especifica se o formulário deve ser validado antes do envio (padrão: verdadeiro). Com êxito, `submitSuccess` é acionado; na falha, `submitError` é acionado. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) para exibir o exemplo. |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | Define o foco para o campo de destino, que pode ser um painel ou campo de formulário. Se nenhum target for fornecido, o foco será definido para o campo que acionou a regra. O parâmetro `$focusOption` opcional especifica se o item seguinte ou anterior relativo ao destino deve ser focalizado. Valores com suporte: `'nextItem'`, `'previousItem'`. Se usada com um painel, a navegação é restrita a esse painel. Se usada com um campo, a navegação ocorre dentro do painel principal desse campo. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field) para exibir o exemplo. |
| **dispatEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | Despacha um evento do tipo `$eventName` no elemento determinado por `$target`. Se nenhum target for fornecido, o evento será despachado no formulário. O `$payload` opcional está disponível para expressões que manipulam o evento. O parâmetro `$dispatch` opcional controla o comportamento de propagação do evento. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property) para exibir o exemplo. |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | Marca o campo identificado por `$fieldIdentifier` como inválido e exibe o `$validationMessage`. O parâmetro `$option` opcional especifica se `$fieldIdentifier` é interpretado como `id`, `dataRef` ou `qualifiedName`. O valor padrão é `{useId: true}`. Valores com suporte: `{useId: true}`, `{useDataRef: true}`, `{useQualifiedName: true}`. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid) para exibir o exemplo. |

## Consulte também

{{see-also-rule-editor}}

