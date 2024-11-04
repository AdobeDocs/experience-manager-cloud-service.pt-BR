---
title: Introdução a objetos de escopo em funções personalizadas
description: Form suporta objetos de escopo em funções personalizadas que são passadas como um último argumento para funções quando a regra é executada.
keywords: objetos de escopo em funções personalizadas, objetos globais, objetos de campo.
feature: Adaptive Forms, Core Components
role: User, Developer
source-git-commit: af211649a4f22d06f4e8669335a8267ee948a408
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Objeto de escopo em funções personalizadas

No Adaptive Forms, um objeto de escopo é passado como o último argumento para funções quando uma regra é executada. Ela pode ser usada para ler propriedades de formulário/campo e modificar o formulário de dentro das funções. O objeto de escopo contém um objeto proxy somente leitura para o formulário, o evento acionado e o campo de destino. As propriedades de formulário e campo podem ser acessadas usando o objeto de escopo com o anexo `$`, por exemplo, `scope.form.$id` e `scope.field.$id`, respectivamente.

## Funções de modificação de formulário usando o objeto de escopo

O objeto de escopo tem as seguintes funções para modificação de formulário:

| Função | Sintaxe | Descrição | Exemplo de código |
|-----------------|----------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|-----------------------------|
| **setProperty** | `setProperty(any $element, any $payload)` | Define uma propriedade de `$element` usando `$payload`. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#show-a-panel-using-the-setproperty-rule) para exibir o exemplo. |
| **validar** | `validate([any $element])` | Executa a validação em `$element`. Se nenhum elemento for fornecido, ele validará o formulário inteiro. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#validate-the-field) para exibir o exemplo. |
| **redefinir** | `reset([any $element])` | Redefine o `$element`. Se nenhum elemento for fornecido, ele redefinirá todo o formulário. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#reset-a-panel) para exibir o exemplo. |
| **importData** | `importData(any $payload)` | Importa dados para o formulário, substituindo quaisquer dados de formulário existentes. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#pre-fill-the-field-with-a-value-when-the-form-loads) para exibir o exemplo. |
| **exportData** | `exportData()` | Retorna os dados do formulário. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) para exibir o exemplo. |
| **submitForm** | `submitForm(any $data [, boolean $validate_form = true, string $submit_as = 'multipart/form-data'])` | Aciona o envio de um formulário. O parâmetro `$data` especifica o que enviar, e `$submit_as` define o tipo de conteúdo (o padrão é &quot;multipart/form-data&quot;). O `$validate_form` opcional determina se o formulário deve ser validado (padrão: verdadeiro). Com êxito, `submitSuccess` é acionado; na falha, `submitError` é acionado. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#submit-altered-data-to-the-server) para exibir o exemplo. |
| **setFocus** | `setFocus(any $element [, FocusOption $focusOption])` | Define o foco para `$element`, que pode ser um painel ou campo. Se nenhum elemento for fornecido, o foco será definido para o campo que acionou a regra. O parâmetro `$focusOption` opcional (do tipo enum `FocusOption`) especifica se o foco deve ser no &#39;nextItem&#39; ou &#39;previousItem&#39; relativo a `$element`. Se um painel for especificado, a navegação é restrita a esse painel; com um campo, a navegação acontece no painel principal. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#set-focus-on-the-specific-field) para exibir o exemplo. |
| **dispatEvent** | `dispatchEvent(any $element, string $eventName [, any $payload])` | Despacha um evento do tipo `$eventName` no elemento especificado por `$element`. Se nenhum elemento for fornecido, o evento será despachado no formulário. O `$payload` opcional é disponibilizado para expressões que manipulam o evento. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#add-or-delete-repeatable-panel-using-the-dispatchevent-property) para exibir o exemplo. |
| **markFieldAsInvalid** | `markFieldAsInvalid(string $fieldIdentifier, string $validationMessage [, any $option = {useId: true}])` | Marca o campo identificado por `$fieldIdentifier` como inválido e define a mensagem de validação como `$validationMessage`. O parâmetro `$option` opcional especifica se `$fieldIdentifier` é interpretado como `id`, `name` ou `dataRef`. O valor padrão é `{useId: true}`, e os valores com suporte incluem `{useId: true}`, `{useDataRef: true}` e `{useQualifiedName: true}`. | [Clique aqui](/help/forms/custom-function-core-components-use-cases.md#to-display-a-custom-message-at-the-field-level-and-marking-the-field-as-invalid) para exibir o exemplo. |

## Consulte também

{{see-also-rule-editor}}