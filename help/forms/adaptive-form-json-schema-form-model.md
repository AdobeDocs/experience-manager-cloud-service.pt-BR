---
title: Como projetar o esquema JSON para um formulário adaptável?
description: Saiba como criar um esquema JSON para um Formulário adaptável e criar um Formulário adaptável com base no esquema para produzir dados de reclamação de esquema.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 8eeb9c5e-6866-4bfe-b922-1f028728ef0d
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 5%

---

# Criar um esquema JSON para um Formulário adaptável {#creating-adaptive-forms-using-json-schema}


| Versão | Link do artigo |
| -------- | ---------------------------- |
| Componentes principais | [Clique aqui](/help/forms/adaptive-form-core-components-json-schema-form-model.md) |
| Foundation | Este artigo |

>[!NOTE]
>
> A Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/creating-adaptive-form-core-components.md) ou [adicionar o Adaptive Forms às páginas do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base.

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-json-schema-form-model.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |


## Pré-requisitos {#prerequisites}

A criação de um formulário adaptável usando um Esquema JSON como seu modelo de formulário requer compreensão básica do Esquema JSON. É recomendável ler o conteúdo a seguir antes deste artigo.

* [Criação de um formulário adaptável](creating-adaptive-form.md)
* [Esquema JSON](https://json-schema.org/)

## Utilização de um esquema JSON como modelo de formulário  {#using-a-json-schema-as-form-model}

O Adobe Experience Manager Forms oferece suporte à criação de um Formulário adaptável usando um Esquema JSON existente como o modelo de formulário. Esse esquema JSON representa a estrutura em que os dados são produzidos ou consumidos pelo sistema de back-end em sua organização. O Esquema JSON usado deve ser compatível com [especificações v4](https://json-schema.org/draft-04/schema).

Os principais recursos do uso de um Esquema JSON são:

* A estrutura do JSON é exibida como uma árvore na guia Localizador de conteúdo no modo de criação de um Formulário adaptável. Você pode arrastar e adicionar elemento da hierarquia JSON ao Formulário adaptável.
* Você pode preencher previamente o formulário usando o JSON compatível com o esquema associado.
* No envio, os dados inseridos pelo usuário são enviados como JSON, que se alinha ao esquema associado.
* Você também pode criar o formulário com base no esquema JSON de acordo com as especificações da [versão 2012-20](https://json-schema.org/draft/2020-12/release-notes).

Um Esquema JSON consiste em tipos de elementos simples e complexos. Os elementos têm atributos que adicionam regras ao elemento. Quando esses elementos e atributos são arrastados para um Formulário adaptável, eles são mapeados automaticamente para o componente de Formulário adaptável correspondente.

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
  }
```

<table>
 <tbody>
  <tr>
   <th><strong>Elemento JSON, propriedades ou atributos</strong></th>
   <th><strong>Componente de formulário adaptável</strong></th>
  </tr>
  <tr>
   <td><p>Propriedades de string com restrições enum e enumNames.</p> <p>Sintaxe,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>Componente suspenso:</p>
    <ul>
     <li>Os valores listados em enumNames são exibidos na caixa suspensa.</li>
     <li>Os valores listados na enumeração são usados para cálculo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Propriedade de cadeia de caracteres com restrição de formato. Por exemplo, email e data.</p> <p>Sintaxe,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>O componente de email é mapeado quando o tipo é string e o formato é email.</li>
     <li>O componente Caixa de texto com validação é mapeado quando o tipo é string e o formato é hostname.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> Campo de texto<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>propriedade numérica<br /> </td>
   <td>Campo numérico com subtipo definido como flutuante<br /> </td>
  </tr>
  <tr>
   <td>propriedade inteira<br /> </td>
   <td>Campo Numérico com subtipo definido como inteiro<br /> </td>
  </tr>
  <tr>
   <td>propriedade booleana<br /> </td>
   <td>Alternar<br /> </td>
  </tr>
  <tr>
   <td>propriedade de objeto <br /> </td>
   <td>Painel<br /> </td>
  </tr>
  <tr>
   <td>propriedade de matriz</td>
   <td>Painel repetível com mín. e máx. iguais a minItems e maxItems, respectivamente. Somente matrizes homogêneas são compatíveis. Portanto, a restrição de itens deve ser um objeto e não uma matriz.<br /> </td>
  </tr>
 </tbody>
</table>

### Propriedades comuns do esquema {#common-schema-properties}

O Formulário adaptável usa as informações disponíveis no Esquema JSON para mapear cada campo gerado. Em especial:

* A propriedade `title` serve como rótulo para os componentes do Formulário adaptável.
* A propriedade `description` é definida como descrição longa para um componente de Formulário adaptável.
* A propriedade `default` serve como valor inicial de um campo de Formulário adaptável.
* A propriedade `maxLength` está definida como atributo `maxlength` do componente de campo de texto.
* As propriedades `minimum`, `maximum`, `exclusiveMinimum` e `exclusiveMaximum` são usadas para o componente de Caixa Numérica.
* Para dar suporte ao intervalo de `DatePicker component`, são fornecidas as propriedades adicionais do Esquema JSON `minDate` e `maxDate`.
* As propriedades `minItems` e `maxItems` são usadas para restringir o número de itens/campos que podem ser adicionados ou removidos de um componente do painel.
* A propriedade `readOnly` define o atributo `readonly` de um componente de Formulário adaptável.
* A propriedade `required` marca o campo Formulário adaptável como obrigatório, enquanto no painel (em que o tipo é objeto), os dados JSON enviados finais têm campos com valor vazio que correspondem a esse objeto.
* A propriedade `pattern` é definida como o padrão de validação (expressão regular) no Formulário adaptável.
* A extensão do arquivo de Esquema JSON deve ser mantida em .schema.json. Por exemplo, &lt;nome do arquivo>.schema.json.

## Exemplo de esquema JSON {#sample-json-schema}

>[!BEGINTABS]

>[!TAB Esquema JSON v4]

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


>[!TAB Esquema JSON 2012-20]


```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://example.com/employee.schema.json",
  "$defs": {
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
          "$ref": "#/$defs/personalDetails"
        },
        "projectDetails": {
          "$ref": "#/$defs/projectDetails"
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
          "$ref": "#/$defs/GeneralDetails"
        },
        "Family": {
          "$ref": "#/$defs/Family"
        },
        "Income": {
          "$ref": "#/$defs/Income"
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
            "$ref": "#/$defs/projects"
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
            "$ref": "#/$defs/projectsAdditional"
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
      }
  }
  }
```

>[!ENDTABS]

As principais alterações das especificações do Esquema JSON V4 para a versão 2020-12 são:
* ID declarada como `$id`
* definições são declaradas como `$defs`

### Definições de esquema reutilizáveis {#reusable-schema-definitions}

As chaves de definição são usadas para identificar esquemas reutilizáveis. As definições de esquema reutilizáveis são usadas para criar fragmentos. <!-- It is similar to identifying complex types in XSD.--> Um exemplo de esquema JSON com definições é fornecido abaixo:

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

O exemplo acima define um registro de cliente, em que cada cliente tem um endereço de entrega e de cobrança. A estrutura de ambos os endereços é a mesma — os endereços têm endereço, cidade e estado — portanto, é uma boa ideia não duplicar os endereços. Também facilita a adição e a exclusão de campos para qualquer alteração futura.

## Pré-configuração de campos na definição do esquema JSON {#pre-configuring-fields-in-json-schema-definition}

Você pode usar a propriedade **aem:afProperties** para pré-configurar o campo de Esquema JSON para mapear para um componente de Formulário adaptável personalizado. Um exemplo está listado abaixo:

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

## Limitar valores aceitáveis para um componente de Formulário adaptável {#limit-acceptable-values-for-an-adaptive-form-component}

Você pode adicionar as seguintes restrições aos elementos do Esquema JSON para limitar os valores aceitáveis para um componente de Formulário adaptável:

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
   <td><p>String</p> </td>
   <td><p>Especifica o limite superior para valores numéricos e datas. Por padrão, o valor máximo é incluído.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador Numérico<br /> </li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o limite inferior para valores numéricos e datas. Por padrão, o valor mínimo é incluído.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador numérico</li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, o valor numérico ou a data especificada no componente do formulário deverá ser menor que o valor numérico ou a data especificada para a propriedade máxima.</p> <p>Se false, o valor numérico ou a data especificada no componente do formulário deve ser menor ou igual ao valor numérico ou à data especificada para a propriedade maximum.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador numérico</li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Se true, o valor numérico ou a data especificada no componente do formulário deverá ser maior que o valor numérico ou a data especificada para a propriedade minimum.</p> <p>Se false, o valor numérico ou a data especificada no componente do formulário deve ser maior ou igual ao valor numérico ou à data especificada para a propriedade minimum.</p> </td>
   <td>
    <ul>
     <li>Caixa numérica</li>
     <li>Escalonador numérico</li>
     <li>Seletor de data</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica o número mínimo de caracteres permitidos em um componente. O comprimento mínimo deve ser igual ou maior que zero.</p> </td>
   <td>
    <ul>
     <li>Caixa de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>String</td>
   <td>Especifica o número máximo de caracteres permitidos em um componente. O comprimento máximo deve ser igual ou maior que zero.</td>
   <td>
    <ul>
     <li>Caixa de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>String</p> </td>
   <td><p>Especifica a sequência dos caracteres. Um componente aceita os caracteres se eles estiverem em conformidade com o padrão especificado.</p> <p>A propriedade padrão mapeia para o padrão de validação do componente de Formulário adaptável correspondente.</p> </td>
   <td>
    <ul>
     <li>Todos os componentes adaptáveis do Forms mapeados para um esquema XSD </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>String</td>
   <td>Especifica o número máximo de itens em uma matriz. O máximo de itens deve ser igual ou maior que zero.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>String</td>
   <td>Especifica o número mínimo de itens em uma matriz. Os itens mínimos devem ser iguais ou maiores que zero.</td>
   <td> </td>
  </tr>
 </tbody>
</table>


## Ativar dados compatíveis com o esquema {#enablig-schema-compliant-data}

Para permitir que todo o Forms adaptável baseado em esquema JSON gere dados compatíveis com o esquema no envio do formulário, siga estas etapas:

1. Vá para o Experience Manager web console em `https://server:host/system/console/configMgr`.
1. Localize **[!UICONTROL Configuração de Canal da Web de Comunicação entre Interações e Formulários Adaptáveis]**.
1. Selecione para abrir a configuração no modo de edição.
1. Marque a caixa de seleção **[!UICONTROL Gerar dados compatíveis com o esquema]**.
1. Salve as configurações.

![configuração do canal da Web de formulário adaptável e comunicação interativa](/help/forms/assets/af-ic-web-channel-configuration.png)


## Construções não suportadas  {#non-supported-constructs}

O Forms adaptável não é compatível com as seguintes construções de esquema JSON:

* Tipo nulo
* Tipos de união, como qualquer um, e
* OneOf, AnyOf, AllOf e NOT
* Somente matrizes homogêneas são compatíveis. Portanto, a restrição de itens deve ser um objeto e não uma matriz.
* Referências de URI em $ref

## Perguntas frequentes {#frequently-asked-questions}

**Por que não consigo arrastar elementos individuais de um subformulário (estrutura gerada de qualquer tipo complexo) para subformulários repetíveis (valores minOccours ou maxOccurs são maiores que 1)?**

Em um subformulário repetível, você deve usar o subformulário completo. Se desejar apenas campos seletivos, use a estrutura inteira e exclua os indesejados.

**Tenho uma estrutura complexa longa no Localizador de Conteúdo. Como posso encontrar um elemento específico?**

Você tem duas opções:

* Rolar pela estrutura de árvore
* Use a caixa Pesquisar para localizar um elemento

**Qual deve ser a extensão do arquivo de esquema JSON?**

A extensão do arquivo de esquema JSON deve ser .schema.json. Por exemplo, &lt;nome do arquivo>.schema.json.

## Consulte também {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Design XML Schema for an Adaptive Form](/help/forms/adaptive-form-xml-schema-form-model.md)

-->
