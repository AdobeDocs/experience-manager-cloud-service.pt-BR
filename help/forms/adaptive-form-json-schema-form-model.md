---
title: Design do esquema JSON para um formulário adaptável
description: Saiba como criar o Adaptive Forms usando o esquema JSON como modelo de formulário. Você pode usar esquemas JSON existentes para criar o Adaptive Forms. Aprofunde-se com uma amostra de esquema JSON, pré-configure os campos na definição do esquema JSON, limite os valores aceitáveis para um componente Formulário adaptável e aprenda construções não suportadas.
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 8eeb9c5e-6866-4bfe-b922-1f028728ef0d
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 4%

---

# Design do esquema JSON para um formulário adaptável {#creating-adaptive-forms-using-json-schema}

## Pré-requisitos {#prerequisites}

A criação de um formulário adaptável usando um esquema JSON como modelo de formulário requer compreensão básica do esquema JSON. É recomendável ler o seguinte conteúdo antes deste artigo.

* [Criação de um formulário adaptável](creating-adaptive-form.md)
* [Esquema JSON](https://json-schema.org/)

## Uso de um esquema JSON como modelo de formulário  {#using-a-json-schema-as-form-model}

O Adobe Experience Manager Forms suporta a criação de um Formulário adaptável usando um Esquema JSON existente como o modelo de formulário. Esse Esquema JSON representa a estrutura na qual os dados são produzidos ou consumidos pelo sistema de back-end na organização. O Esquema JSON que você usa deve ser compatível com [especificações v4](https://json-schema.org/draft-04/schema).

Os principais recursos do uso de um Esquema JSON são:

* A estrutura do JSON é exibida como uma árvore na guia Localizador de conteúdo no modo de criação de um formulário adaptável. Você pode arrastar e adicionar elemento da hierarquia JSON para o Formulário adaptável.
* É possível preencher previamente o formulário usando JSON compatível com o schema associado.
* Ao enviar, os dados inseridos pelo usuário são enviados como JSON que se alinha ao schema associado.

Um Esquema JSON consiste em tipos de elementos simples e complexos. Os elementos têm atributos que adicionam regras ao elemento. Quando esses elementos e atributos são arrastados para um Formulário adaptável, eles são mapeados automaticamente para o componente Formulário adaptativo correspondente.

Esse mapeamento de elementos JSON com componentes de Formulário adaptável é o seguinte:

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>Elemento, propriedades ou atributos JSON</strong></th>
   <th><strong>Componente de formulário adaptável</strong></th>
  </tr>
  <tr>
   <td><p>Propriedades de string com a restrição enum e enumNames.</p> <p>Sintaxe,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>Componente suspenso:</p>
    <ul>
     <li>Os valores listados em enumNames são exibidos na caixa suspensa.</li>
     <li>Os valores listados no enum são usados para o cálculo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Propriedade String com restrição de formato. Por exemplo, email e data.</p> <p>Sintaxe,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>O componente de email é mapeado quando o tipo é string e o formato é email.</li>
     <li>O componente de caixa de texto com validação é mapeado quando o tipo é string e o formato é nome do host.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> Campo de texto<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>propriedade number<br /> </td>
   <td>Campo numérico com subtipo definido para flutuante<br /> </td>
  </tr>
  <tr>
   <td>propriedade integer<br /> </td>
   <td>Campo numérico com subtipo definido como inteiro<br /> </td>
  </tr>
  <tr>
   <td>propriedade booleana<br /> </td>
   <td>Alternar<br /> </td>
  </tr>
  <tr>
   <td>propriedade de objeto<br /> </td>
   <td>Painel<br /> </td>
  </tr>
  <tr>
   <td>propriedade array</td>
   <td>Painel repetível com mín. e máx. iguais a minItems e maxItems, respectivamente. Somente arrays homogêneos são compatíveis. Portanto, a restrição de itens deve ser um objeto e não uma matriz.<br /> </td>
  </tr>
 </tbody>
</table>

### Propriedades comuns do schema {#common-schema-properties}

O Formulário adaptável usa as informações disponíveis no Esquema JSON para mapear cada campo gerado. Em especial:

* O `title` serve como rótulo para os componentes do Formulário adaptável.
* O `description` é definida como descrição longa para um componente Formulário adaptável.
* O `default` serve como valor inicial de um campo de Formulário adaptável.
* O `maxLength` a propriedade é definida como `maxlength` do componente de campo de texto.
* O `minimum`, `maximum`, `exclusiveMinimum`e `exclusiveMaximum` As propriedades são usadas para o componente de caixa numérica.
* Para oferecer suporte ao intervalo de `DatePicker component` propriedades adicionais do Esquema JSON `minDate` e `maxDate` são fornecidas.
* O `minItems` e `maxItems` As propriedades são usadas para restringir o número de itens/campos que podem ser adicionados ou removidos de um componente do painel.
* O `readOnly` a propriedade define a variável `readonly` de um componente de Formulário adaptável.
* O `required` marca o campo Formulário adaptável como obrigatório, enquanto no painel (onde o tipo é objeto), os dados JSON enviados finais têm campos com valor vazio correspondente a esse objeto.
* O `pattern` é definida como o padrão de validação (expressão regular) no Formulário adaptável.
* A extensão do arquivo Esquema JSON deve ser mantida .schema.json. Por exemplo, &lt;filename>.schema.json.

## Exemplo de esquema JSON {#sample-json-schema}

Aqui está um exemplo de um Esquema JSON.

```json
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### Definições de esquema reutilizáveis {#reusable-schema-definitions}

As chaves de definição são usadas para identificar esquemas reutilizáveis. As definições de esquema reutilizáveis são usadas para criar fragmentos. <!-- It is similar to identifying complex types in XSD.--> Um exemplo de Esquema JSON com definições é fornecido abaixo:

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

O exemplo acima define um registro de cliente, em que cada cliente tem um endereço de envio e de faturamento. A estrutura de ambos os endereços é a mesma — os endereços têm um endereço de rua, cidade e estado — portanto, é uma boa ideia não duplicar os endereços. Também facilita a adição e exclusão de campos para qualquer alteração futura.

## Pré-configuração de campos na definição do esquema JSON {#pre-configuring-fields-in-json-schema-definition}

Você pode usar o **aem:afProperties** propriedade para pré-configurar o campo Esquema JSON para mapear para um componente Formulário adaptável personalizado. Um exemplo é listado abaixo:

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

<!--- ## Configure scripts or expressions for form objects  {#configure-scripts-or-expressions-for-form-objects}

JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. You can pre-configure form objects to [evaluate an expression](adaptive-form-expressions.md) on a form event.

Use the aem:afproperties property to preconfigure Adaptive Form expressions or scripts for Adaptive Form components. For example, when the initialize event is triggered, the below code sets value of telephone field and prints a value to the log :

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

You should be a member of the [forms-power-user group](forms-groups-privileges-tasks.md) to configure scripts or expressions for form object. The below table lists all the script events supported for an Adaptive Form component.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Component \ Event</th>
   <th>initialize <br /> </th>
   <td>Calculate</td>
   <td>Visibility</td>
   <td>Validate</td>
   <td>Enabled</td>
   <td>Value Commit</td>
   <td>Click </td>
   <td>Options</td>
  </tr>
  <tr>
   <td>Text Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numeric Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Numeric Stepper</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Radio Button</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Telephone</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Switch</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Button</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Check Box</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Drop-down</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Image Choice</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Date Input Field</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Date Picker</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Email</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>File Attachment</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Image</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Panel</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Some examples of using events in a JSON are hiding a field on initialize event and configure value of another field on value commit event. For detailed information about creating expressions for the script events, see [Adaptive Form Expressions](adaptive-form-expressions.md).

Here is the sample JSON code for previously mentioned examples.

### Hiding a field on initialize event {#hiding-a-field-on-initialize-event}

```json

"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### Configure value of another field on value commit event {#configure-value-of-another-field-on-value-commit-event}

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}

```
-->

## Limites de valores aceitáveis para um componente de Formulário adaptável {#limit-acceptable-values-for-an-adaptive-form-component}

É possível adicionar as seguintes restrições aos elementos do Esquema JSON para limitar os valores aceitáveis para um componente de Formulário adaptável:

<table>
 <tbody>
  <tr>
   <td><p><strong> Propriedade do esquema</strong></p> </td>
   <td><p><strong>Tipo de dados</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Sequência de caracteres</p> </td>
   <td><p>Especifica o limite superior para valores numéricos e datas. Por padrão, o valor máximo é incluído.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador Numérico<br /> </li>
     <li>Seletor de datas</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>Sequência de caracteres</p> </td>
   <td><p>Especifica o limite inferior para valores numéricos e datas. Por padrão, o valor mínimo é incluído.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador Numérico</li>
     <li>Seletor de datas</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se verdadeiro, o valor numérico ou a data especificada no componente do formulário deve ser menor que o valor numérico ou a data especificada para a propriedade máxima.</p> <p>Se falso, o valor numérico ou a data especificada no componente do formulário deve ser menor ou igual ao valor numérico ou à data especificada para a propriedade maximum .</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador Numérico</li>
     <li>Seletor de datas</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se verdadeiro, o valor numérico ou a data especificada no componente do formulário deve ser maior que o valor numérico ou a data especificada para a propriedade mínima.</p> <p>Se falso, o valor numérico ou a data especificada no componente do formulário deve ser maior ou igual ao valor numérico ou à data especificada para a propriedade mínima.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador Numérico</li>
     <li>Seletor de datas</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>Sequência de caracteres</p> </td>
   <td><p>Especifica o número mínimo de caracteres permitidos em um componente. O comprimento mínimo deve ser igual ou superior a zero.</p> </td>
   <td>
    <ul>
     <li>Caixa de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>Sequência de caracteres</td>
   <td>Especifica o número máximo de caracteres permitidos em um componente. O comprimento máximo deve ser igual ou superior a zero.</td>
   <td>
    <ul>
     <li>Caixa de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Sequência de caracteres</p> </td>
   <td><p>Especifica a sequência de caracteres. Um componente aceita os caracteres se eles estiverem em conformidade com o padrão especificado.</p> <p>A propriedade pattern mapeia para o padrão de validação do componente Formulário adaptável correspondente.</p> </td>
   <td>
    <ul>
     <li>Todos os componentes adaptáveis do Forms que estão mapeados para um esquema XSD </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>Sequência de caracteres</td>
   <td>Especifica o número máximo de itens em uma matriz. Os itens máximos devem ser iguais ou maiores que zero.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>Sequência de caracteres</td>
   <td>Especifica o número mínimo de itens em uma matriz. Os itens mínimos devem ser iguais ou maiores que zero.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Construções não suportadas  {#non-supported-constructs}

O Adaptive Forms não suporta as seguintes construções do Esquema JSON:

* Tipo nulo
* Tipos de União como qualquer, e
* OneOf, AnyOf, AllOf e NOT
* Somente arrays homogêneos são compatíveis. Portanto, a restrição de itens deve ser um objeto e não uma matriz.

## Perguntas frequentes {#frequently-asked-questions}

**Por que não consigo arrastar elementos individuais de um subformulário (estrutura gerada de qualquer tipo complexo) para subformulários repetíveis (os valores minOccours ou maxOccurs são maiores que 1)?**

Em um subformulário repetível, é necessário usar o subformulário completo. Se quiser apenas campos seletivos, use toda a estrutura e exclua os não desejados.

**Tenho uma estrutura complexa longa no Localizador de conteúdo. Como posso encontrar um elemento específico?**

Você tem duas opções:

* Rolar pela estrutura de árvore
* Use a caixa Pesquisar para localizar um elemento

**Qual deve ser a extensão do arquivo de esquema JSON?**

A extensão do arquivo Esquema JSON deve ser .schema.json. Por exemplo, &lt;filename>.schema.json.
