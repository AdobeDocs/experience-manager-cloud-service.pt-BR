---
title: Definições de modelo, campos e tipos de componentes
description: Saiba mais sobre campos e os tipos de componentes que o Editor universal pode editar no painel de propriedades com exemplos. Entenda como você pode instrumentar seu próprio aplicativo criando uma definição de modelo e vinculando ao componente.
exl-id: cb4567b8-ebec-477c-b7b9-53f25b533192
source-git-commit: 550d26cde3d6b7be419bc9df70db8894851361c6
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 11%

---


# Definições de modelo, campos e tipos de componentes {#field-types}

Saiba mais sobre campos e os tipos de componentes que o Editor universal pode editar no painel de propriedades com exemplos. Entenda como você pode instrumentar seu próprio aplicativo criando uma definição de modelo e vinculando ao componente.

{{universal-editor-status}}

## Visão geral {#overview}

Ao adaptar seus próprios aplicativos para uso com o Universal Editor, você deve instrumentar os componentes e definir quais campos e tipos de componentes eles podem manipular no painel de propriedades do editor. Você faz isso criando um modelo e vinculando a ele a partir do componente.

Este documento fornece uma visão geral de uma definição de modelo e dos campos e dos tipos de componentes disponíveis para você, juntamente com exemplos de configurações.

>[!TIP]
>
>Se você não estiver familiarizado com como instrumentar seu aplicativo para o Universal Editor, consulte o documento [Visão geral do editor universal para desenvolvedores do AEM.](/help/implementing/universal-editor/developer-overview.md)

## Estrutura de definição do modelo {#model-structure}

Para configurar um componente por meio do painel de propriedades no Editor universal, uma definição de modelo deve existir e estar vinculada ao componente.

A definição do modelo é uma estrutura JSON, que começa com uma matriz de modelos.

```json
[
  {
    "id": "model-id",        // must be unique
    "fields": []             // array of fields which shall be rendered in the properties rail
  }
]
```

Consulte a **[Campos](#fields)** seção deste documento para obter mais informações sobre como definir `fields` matriz.

Para usar a definição do modelo com um componente, a variável `data-aue-model` atributo pode ser usado.

```html
<div data-aue-resource="urn:datasource:/content/path" data-aue-type="component"  data-aue-model="model-id">Click me</div>
```

## Carregando uma Definição de Modelo {#loading-model}

Depois que um modelo é criado, ele pode ser referenciado como um arquivo externo.

```html
<script type="application/vnd.adobe.aue.model+json" src="<url-of-model-definition>"></script>
```

Como alternativa, também é possível definir o modelo em linha.

```html
<script type="application/vnd.adobe.aue.model+json">
  { ... model definition ... }
</script>
```

## Campos {#fields}

Um objeto de campo tem a seguinte definição de tipo.

| Configuração | Tipo de valor | Descrição | Obrigatório |
|---|---|---|---|
| `component` | `ComponentType` | Renderizador do componente | Sim |
| `name` | `string` | Propriedade em que os dados devem ser mantidos | Sim |
| `label` | `FieldLabel` | Rótulo do campo | Sim |
| `description` | `FieldDescription` | Descrição do campo | Não |
| `placeholder` | `string` | Espaço reservado para o campo | Não |
| `value` | `FieldValue` | Valor padrão | Não |
| `valueType` | `ValueType` | Validação padrão, pode ser `string`, `string[]`, `number`, `date`, `boolean` | Não |
| `required` | `boolean` | O campo é obrigatório? | Não |
| `readOnly` | `boolean` | O campo é somente leitura | Não |
| `hidden` | `boolean` | O campo está oculto por padrão? | Não |
| `condition` | `RulesLogic` | Regra para mostrar ou ocultar o campo com base em um [condição](/help/implementing/universal-editor/customizing.md#conditionally-hide) | Não |
| `multi` | `boolean` | O campo é um campo múltiplo? | Não |
| `validation` | `ValidationType` | Regra ou regras de validação para o campo | Não |
| `raw` | `unknown` | Dados brutos que podem ser usados pelo componente | Não |

### Tipos de componentes {#component-types}

A seguir estão os tipos de componentes possíveis para usar em campos de renderização.

#### Tag AEM {#aem-tag}

Um tipo de componente de tag AEM habilita um seletor de tags AEM, que pode ser usado para anexar tags ao componente.

##### Amostra {#sample-aem-tag}

```json
{
  "id": "aem-tag-picker",
  "fields": [
    {
      "component": "aem-tag",
      "label": "AEM Tag Picker",
      "name": "cq:tags",
      "valueType": "string"
    }
  ]
}
```

##### Captura de tela {#screenshot-aem-tag}

![Captura de tela do tipo de componente da tag AEM](assets/component-types/aem-tag-picker.png)

#### Conteúdo AEM {#aem-content}

Um tipo de componente de conteúdo do AEM permite um seletor de conteúdo do AEM, que pode ser usado para definir referências de conteúdo.

##### Amostra {#sample-aem-content}

```json
{
  "id": "aem-content-picker",
  "fields": [
    {
      "component": "aem-content",
      "name": "reference",
      "value": "",
      "label": "AEM Content Picker",
      "valueType": "string"
    }
  ]
}
```

##### Captura de tela {#screenshot-aem-content}

![Captura de tela do tipo de componente de conteúdo do AEM](assets/component-types/aem-content-picker.png)

#### Booleano {#boolean}

Um tipo de componente booleano armazena um valor simples true/false renderizado como alternância. Ele oferece um tipo de validação adicional.

| Tipo de validação | Tipo de valor | Descrição | Obrigatório |
|---|---|---|---|
| `customErrorMsg` | `string` | Mensagem que será exibida se o valor inserido não for um valor booleano | Não |

##### Amostra {#sample-boolean}

```json
{
  "id": "boolean",
  "fields": [
    {
      "component": "boolean",
      "label": "Boolean",
      "name": "boolean",
      "valueType": "boolean"
    }
  ]
}
```

```json
{
  "id": "another-boolean",
  "fields": [
    {
      "component": "boolean",
      "label": "Boolean",
      "name": "boolean",
      "valueType": "boolean",
      "validation": {
        "customErrorMsg": "Think, McFly. Think!"
      }
    }
  ]
}
```

##### Captura de tela {#screenshot-boolean}

![Captura de tela do tipo de componente booleano](assets/component-types/boolean.png)

#### Grupos de caixa de seleção {#checkbox-group}

Semelhante a um booleano, um tipo de componente Grupo de caixas de seleção permite a seleção de vários itens true/false, renderizados como várias caixas de seleção.

##### Amostra {#sample-checkbox-group}

```json
{
  "id": "checkbox-group",
  "fields": [
    {
      "component": "checkbox-group",
      "label": "Checkbox Group",
      "name": "checkbox",
      "valueType": "string[]",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

#### Captura de tela {#screenshot-checkbox-group}

![Captura de tela do tipo de componente do grupo de caixas de seleção](assets/component-types/checkbox-group.png)

#### Contêiner {#container}

Um tipo de componente de contêiner permite o agrupamento de componentes. Ela oferece uma configuração adicional.

| Configuração | Tipo de valor | Descrição | Obrigatório |
|---|---|---|---|
| `collapsible` | `boolean` | O contêiner é recolhível | Não |

##### Amostra {#sample-container}

```json
 {
  "id": "container",
  "fields": [
    {
      "component": "container",
      "label": "Container",
      "name": "container",
      "valueType": "string",
      "collapsible": true,
      "fields": [
        {
          "component": "text-input",
          "label": "Simple Text 1",
          "name": "text",
          "valueType": "string"
        },
        {
          "component": "text-input",
          "label": "Simple Text 2",
          "name": "text2",
          "valueType": "string"
        }
      ]
    }
  ]
}
```

##### Captura de tela {#screenshot-container}

![Captura de tela do tipo de componente do contêiner](assets/component-types/container.png)

#### Data e hora {#date-time}

Um tipo de componente de data e hora permite a especificação de uma data, hora ou combinação destas. Ele oferece configurações adicionais.

| Configuração | Tipo de valor | Descrição | Obrigatório |
|---|---|---|---|
| `displayFormat` | `string` | Formato com o qual exibir a cadeia de caracteres de data | Sim |
| `valueFormat` | `string` | Formato no qual armazenar a cadeia de caracteres de data | Sim |

Também oferece um tipo de validação adicional.

| Tipo de validação | Tipo de valor | Descrição | Obrigatório |
|---|---|---|---|
| `customErrorMsg` | `string` | Mensagem que será exibida se `valueFormat` não foi atendido | Não |

##### Amostra {#sample-date-time}

```json
{
  "id": "date-time",
  "fields": [
    {
      "component": "date-time",
      "label": "Date & Time",
      "name": "date",
      "valueType": "date"
    }
  ]
}
```

```json
{
  "id": "another-date-time",
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

##### Captura de tela {#screenshot-date-time}

![Captura de tela do tipo de componente de data e hora](assets/component-types/date-time.png)

#### Multisseleção {#multiselect}

Um tipo de componente de seleção múltipla apresenta vários itens para seleção em uma lista suspensa, incluindo a capacidade de agrupar os elementos selecionáveis.

##### Amostras {#sample-multiselect}

```json
{
  "id": "multiselect",
  "fields": [
    {
      "component": "multiselect",
      "name": "multiselect",
      "label": "Multi Select",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

```json
{
  "id": "multiselect-grouped",
  "fields": [
    {
      "component": "multiselect",
      "name": "property",
      "label": "Multiselect field",
      "valueType": "string",
      "required": true,
      "maxSize": 2,
      "options": [
        {
          "name": "Theme",
          "children": [
            { "name": "Light", "value": "light" },
            { "name": "Dark",  "value": "dark" }
          ]
        },
        {
          "name": "Type",
          "children": [
            { "name": "Alpha", "value": "alpha" },
            { "name": "Beta", "value": "beta" },
            { "name": "Gamma", "value": "gamma" }
          ]
        }
      ]
    }
  ]
}
```

##### Capturas de tela {#screenshot-multiselect}

![Captura de tela do tipo de componente de seleção múltipla](assets/component-types/multiselect.png)
![Captura de tela do tipo de componente de seleção múltipla com agrupamento](assets/component-types/multiselect-group.png)

#### Número {#number}

Um tipo de componente numérico permite a entrada de um número. Ela oferece tipos de validação adicionais.

| Tipo de validação | Tipo de valor | Descrição | Obrigatório |
|---|---|---|---|
| `numberMin` | `number` | Número mínimo permitido | Não |
| `numberMax` | `number` | Número máximo permitido | Não |
| `customErrorMsg` | `string` | Mensagem que será exibida se `numberMin` ou `numberMax` não foi atendido | Não |

##### Amostra {#sample-number}

```json
{
  "id": "number",
  "fields": [
    {
      "component": "number",
      "name": "number",
      "label": "Number",
      "valueType": "number",
      "value": 0
    }
  ]
}
```

```json
{
  "id": "another-number",
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
        "numberMin": 0,
        "numberMax": 88,
        "customErrorMsg": "You also need 1.21 gigawatts."
      }
    }
  ]
}
```

##### Captura de tela {#screenshot-number}

![Captura de tela do tipo de componente número](assets/component-types/number.png)

#### Grupo radial {#radio-group}

Um tipo de componente Grupo de opções permite uma seleção mutuamente exclusiva de várias opções renderizadas como um grupo semelhante a um grupo de caixas de seleção.

##### Amostra {#sample-radio-group}

```json
{
  "id": "radio-group",
  "fields": [
    {
      "component": "radio-group",
      "label": "Radio Group",
      "name": "radio",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

##### Captura de tela {#screenshot-radio-group}

![Captura de tela do tipo de componente Grupo de opções](assets/component-types/radio.png)

#### Referência {#reference}

Um tipo de componente de referência permite uma referência a outro objeto de dados do objeto atual.

##### Amostra {#sample-reference}

```json
{
  "id": "reference",
  "fields": [
    {
      "component": "reference",
      "label": "Reference",
      "name": "reference",
      "valueType": "string"
    }
  ]
}
```

##### Captura de tela {#screenshot-reference}

![Captura de tela do tipo de componente de referência](assets/component-types/reference.png)

#### Selecionar {#select}

Um tipo de componente de seleção permite selecionar uma única opção em uma lista de opções predefinidas em um menu suspenso.

##### Amostra {#sample-select}

```json
{
  "id": "select",
  "fields": [
    {
      "component": "select",
      "label": "Select",
      "name": "select",
      "valueType": "string",
      "options": [
        { "name": "Option 1", "value": "option1" },
        { "name": "Option 2", "value": "option2" }
      ]
    }
  ]
}
```

##### Captura de tela {#screenshot-select}

![Captura de tela do tipo de componente selecionado](assets/component-types/select.png)

#### Guia {#tab}

Um tipo de componente de guia permite agrupar outros campos de entrada em várias guias para melhorar a organização do layout dos autores.

A `tab` definição pode ser considerada como um separador na matriz de `fields`. Tudo que vem depois de um `tab` será colocado nessa guia até que um novo `tab` for encontrada, em que os itens a seguir serão colocados na nova guia.

Se desejar que itens sejam exibidos acima de todas as guias, eles deverão ser definidos antes de qualquer guia.

##### Amostra {#sample-tab}

```json
{
  "id": "tab",
  "fields": [
    {
      "component": "tab",
      "label": "Tab 1",
      "name": "tab1"
    },
    {
      "component": "text-input",
      "label": "Text 1",
      "name": "text1",
      "valueType": "string"
    },
    {
      "component": "tab",
      "label": "Tab 2",
      "name": "tab2"
    },
    {
      "component": "text-input",
      "label": "Text 2",
      "name": "text2",
      "valueType": "string"
    }
  ]
}
```

##### Captura de tela {#screenshot-tab}

![Captura de tela do tipo de componente guia](assets/component-types/tab.png)

#### Área de texto {#text-area}

Uma área de texto permite entrada de rich text em várias linhas. Ela oferece tipos de validação adicionais.

| Tipo de validação | Tipo de valor | Descrição | Obrigatório |
|---|---|---|---|
| `maxSize` | `number` | Número máximo de caracteres permitido | Não |
| `customErrorMsg` | `string` | Mensagem que será exibida se `maxSize` é excedido | Não |

##### Amostra {#sample-text-area}

```json
{
  "id": "richtext",
  "fields": [
    {
      "component": "text-area",
      "name": "rte",
      "label": "Rich Text",
      "valueType": "string"
    }
  ]
}
```

```json
{
  "id": "another-richtext",
  "fields": [
    {
      "component": "text-area",
      "name": "rte",
      "label": "Rich Text",
      "valueType": "string",
      "validation": {
        "maxSize": 1000,
        "customErrorMsg": "That's about as funny as a screen door on a battleship."
      }
    }
  ]
}
```

##### Captura de tela {#screenshot-text-area}

![Captura de tela do tipo de componente da área de texto](assets/component-types/richtext.png)

#### Entrada de texto {#text-input}

Uma entrada de texto permite uma única linha de entrada de texto.  Inclui tipos de validação adicionais.

| Tipo de validação | Tipo de valor | Descrição | Obrigatório |
|---|---|---|---|
| `minLength` | `number` | Número mínimo de caracteres permitidos | Não |
| `maxLength` | `number` | Número máximo de caracteres permitidos | Não |
| `regExp` | `string` | Expressão regular à qual o texto de entrada deve corresponder | Não |
| `customErrorMsg` | `string` | Mensagem que será exibida se `minLength`, `maxLength`, e/ou `regExp` é/são violado(s) | Não |

##### Amostra {#sample-text-input}

```json
{
  "id": "simpletext",
  "fields": [
    {
      "component": "text-input",
      "name": "text",
      "label": "Simple Text",
      "valueType": "string"
    }
  ]
}
```

```json
{
  "id": "another simpletext",
  "fields": [
    {
      "component": "text-input",
      "name": "text",
      "label": "Simple Text",
      "valueType": "string",
      "description": "This is a text input with validation.",
      "required": true,
      "validation": {
        "minLength": 1955,
        "maxLength": 1985,
        "regExp": "^foo:.*",
        "customErrorMsg": "Why don't you make like a tree and get outta here?"
      }
    }
  ]
}
```

##### Captura de tela {#screenshot-text-input}

![Captura de tela do tipo de componente de entrada de texto](assets/component-types/simpletext.png)
