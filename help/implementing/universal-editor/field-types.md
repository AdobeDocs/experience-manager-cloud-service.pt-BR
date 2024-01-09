---
title: Tipos de campos
description: Saiba mais sobre os diferentes tipos de campos que o Editor universal pode editar no painel Componentes com exemplos de como você pode instrumentar seu próprio aplicativo.
source-git-commit: 44073e27ce7eb35bc0d71cb963c1bd0f14183f00
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 7%

---


# Tipos de campos {#field-types}

Saiba mais sobre os diferentes tipos de campos que o Editor universal pode editar no painel Componentes com exemplos de como você pode instrumentar seu próprio aplicativo.

{{universal-editor-status}}

## Visão geral {#overview}

Ao adaptar seus próprios aplicativos para uso com o Editor universal, você deve instrumentar os componentes e definir quais tipos de dados eles podem manipular no painel de componentes do editor.

Este documento fornece uma visão geral dos tipos de campo disponíveis para você, juntamente com exemplos de configurações.

>[!TIP]
>
>Se você não estiver familiarizado com como instrumentar seu aplicativo para o Universal Editor, consulte o documento [Visão geral do editor universal para desenvolvedores do AEM.](/help/implementing/universal-editor/developer-overview.md)

## Booleano {#boolean}

Um campo booleano armazena um valor verdadeiro/falso simples renderizado como uma caixa de seleção.

### Amostra {#sample-boolean}

```json
{
  "fields": [   
   {
      "component": "boolean",
      "valueType": "boolean",
      "name": "field1",
      "label": "Boolean Field",
      "description": "This is a boolean field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "customErrorMsg": "This is an error."
      }
    }
  ]
}
```

## Grupos de caixa de seleção {#checkbox-group}

Semelhante a um booleano, um grupo de caixas de seleção permite a seleção de vários itens verdadeiros/falsos.

### Amostra {#sample-checkbox-group}

```json
{
  "fields": [   
   {
      "component": "checkbox-group",
      "valueType": "string-array",
      "name": "field1",
      "label": "Checkbox Group",
      "description": "This is a checkbox group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "First option", "value": "one" },
        { "name": "Second option", "value": "two" },
        { "name": "Third option", "value": "three" }
      ]
    }
  ]
}
```

## Data e hora {#date-time}

Um campo de data e hora permite a especificação de uma data, hora ou combinação delas.

### Amostra {#sample-date-time}

```json
{
  "fields": [   
      {
      "component": "date-time",
      "valueType": "date-time",
      "name": "field1",
      "label": "Date Time",
      "description": "This is a date time field that stores both date and time.",
      "required": true,
      "placeholder": "YYYY-MM-DD HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Marty! You have to come back with me!"
      }
    },
    {
      "component": "date-time",
      "valueType": "date",
      "name": "field2",
      "label": "Another Date Time",
      "description": "This is another date time field that only stores the date.",
      "required": true,
      "placeholder": "YYYY-MM-DD",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Back to the future!"
      }
    },
    {
      "component": "date-time",
      "valueType": "time",
      "name": "field3",
      "label": "Yet Another Date Time",
      "description": "This is another date time field that only stores the time.",
      "required": true,
      "placeholder": "HH:mm:ss",
      "displayFormat": null,
      "valueFormat": null,
      "validation": {
        "customErrorMsg": "Great Scott!"
      }
    }
  ]
}
```

## Número {#number}

Um campo de número permite a entrada de um número.

### Amostra {#sample-number}

```json
{
  "fields": [   
   {
      "component": "number",
      "valueType": "number",
      "name": "field1",
      "label": "Number Field",
      "description": "This is a number field.",
      "required": true,
      "placeholder": null,
      "validation": {
        "numberMin": null,
        "numberMax": null,
        "customErrorMsg": "Please don't do that."
      }
    }
  ]
}
```

## Grupo radial {#radio-group}

Um grupo de opções permite uma seleção mutuamente exclusiva de várias opções renderizadas como um grupo semelhante a um grupo de caixas de seleção.

### Amostra {#sample-radio-group}

```json
{
  "fields": [   
   {
      "component": "radio-group",
      "valueType": "string",
      "name": "field1",
      "label": "Radio Group",
      "description": "This is a radio group.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ]
    }
  ]
}
```

## Referência {#reference}

Uma referência permite a especificação de outro objeto de dados como uma referência do objeto atual.

## Selecionar {#select}

Uma seleção permite selecionar uma ou mais opções predefinidas em um menu suspenso.

### Amostra {#sample-select}

```json
{
  "fields": [   
   {
      "component": "select",
      "valueType": "string",
      "name": "field1",
      "label": "Select",
      "description": "This is a select.",
      "required": true,
      "placeholder": null,
      "options": [
        { "name": "Option One", "value": "one" },
        { "name": "Option Two", "value": "two" },
        { "name": "Option Three", "value": "three" }
      ],
      "emptyOption": true
    }
  ]
}
```

## Área de texto {#text-area}

Uma área de texto permite a entrada de texto multilinha.

### Amostra {#sample-text-area}

```json
{
  "fields": [   
   {
      "component": "text-area",
      "valueType": "string",
      "name": "field1",
      "label": "Text Area",
      "description": "This is a text area.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "mimeType": "text/x-markdown"
    }
  ]
}
```

## Entrada de texto {#text-input}

Uma entrada de texto permite uma única linha de entrada de texto.

### Amostra {#sample-text-input}

```json
{
  "fields": [   
   {
      "component": "text-input",
      "valueType": "string",
      "name": "field1",
      "label": "Text Input",
      "description": "This is a text input.",
      "required": true,
      "multi": true,
      "placeholder": null
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "field2",
      "label": "Another Text Input",
      "description": "This is a text input with validation.",
      "required": true,
      "multi": true,
      "placeholder": null,
      "validation": {
        "minLength": 5,
        "maxLength": 10,
        "regExp": "^foo:.*",
        "customErrorMsg": "I'm sorry, Dave. I can't do that."
      }
    }
  ]
}
```

## Guia {#tab}

Uma guia permite agrupar outros campos de entrada em várias guias para melhorar a organização do layout dos autores.

A `tab` definição pode ser considerada como um separador na matriz de `fields`. Tudo que vem depois de um `tab` será colocado nessa guia até que um novo `tab` for encontrada, em que os itens a seguir serão colocados na nova guia.

Se desejar que itens sejam exibidos acima de todas as guias, eles deverão ser definidos antes de qualquer guia.

### Amostra {#sample-tab}

```json
{
  "id": "title",
  "fields": [
    {
      "component": "tab",
      "label": "Tab",
      "name": "tab1"
    },
    {
      "component": "text-input",
      "name": "tab-response",
      "value": "",
      "placeholder": "Tab? I can't give you a tab unless you order something.",
      "label": "Lou",
      "valueType": "string"
    },
    {
      "component": "tab",
      "label": "Pepsi Free",
      "name": "tab2"
    },
    {
      "component": "text-input",
      "name": "pepsi-free-response",
      "value": "",
      "placeholder": "You want a Pepsi, pal, you're gonna pay for it.",
      "label": "Mr. Carruthers",
      "valueType": "string"
    },
    {
      "component": "select",
      "name": "without-sugar",
      "value": "coffee",
      "label": "Something without sugar",
      "valueType": "string",
      "options": [
        { "name": "Coffee", "value": "coffee" },
        { "name": "Hot Coffee", "value": "hot-coffee" },
        { "name": "Hotter Coffee", "value": "hotter-coffee" }
      ]
    }
  ]
}
```
