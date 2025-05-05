---
title: Criar componentes personalizados para um formulário EDS
description: Criar componentes personalizados para um formulário EDS
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 0%

---

# Criar componente personalizado na criação do WYSIWYG

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email com o nome da sua organização GitHub e o nome do repositório do seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>


O Edge Delivery Services Forms oferece personalização, permitindo que desenvolvedores de front-end criem componentes de formulário personalizados. Esses componentes personalizados se integram perfeitamente à experiência de criação do WYSIWYG, permitindo que os autores de formulários os adicionem, configurem e gerenciem facilmente no editor de formulários. Com componentes personalizados, os autores podem aprimorar a funcionalidade e, ao mesmo tempo, garantir um processo de criação simples e intuitivo.

Este documento descreve as etapas para criar componentes personalizados estilizando os componentes de formulário nativos do HTML para melhorar a experiência do usuário e aumentar o apelo visual do formulário.

## Pré-requisitos

Antes de começar a criar seu componente personalizado, você deve:

* Ter um conhecimento básico de [componentes nativos do HTML](/help/edge/docs/forms/form-components.md).
* Saiba como [estilizar campos de formulário com base no tipo de campo usando os seletores de CSS](/help/edge/docs/forms/style-theme-forms.md)

## Criar um componente personalizado

Adicionar um componente personalizado no Editor universal significa disponibilizar um novo componente para os autores de formulários usarem ao criar formulários. Isso envolve registrar o componente, definir suas propriedades e configurar onde ele pode ser usado. As etapas para criar componentes personalizados são:

[1. Adicionando estrutura para novo componente personalizado](#1-adding-structure-for-new-custom-component)
[2. Definindo as propriedades do componente personalizado para criação](#2-defining-the-properties-of-your-custom-component-for-authoring)
[3.  Tornando seu componente personalizado visível na lista de componentes do WYSIWYG](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)
[4. Registrando seu componente personalizado](#4-registering-your-custom-component)
[5. Adicionando o comportamento do tempo de execução para seu componente personalizado](#5-adding-the-runtime-behaviour-for-your-custom-component)

Vamos ver um exemplo de criação de um novo componente personalizado chamado **intervalo**. O componente de Intervalo é exibido como uma linha reta e exibe valores como o valor mínimo, máximo ou selecionado.

![Estilo do componente do intervalo](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

No final deste artigo, você aprenderá a criar componentes personalizados do zero.

### 1. Adição de estrutura para novo componente personalizado

Antes de um componente personalizado poder ser usado, ele deve ser registrado para que o Editor universal o reconheça como uma opção disponível. Isso é feito por meio de uma definição de componente, que inclui um identificador exclusivo, propriedades padrão e a estrutura do componente.Execute as seguintes etapas para disponibilizar o componente personalizado para criação de formulário:

1. **Adicionar nova pasta e arquivos**
Adicione novas pastas e arquivos para o novo componente personalizado no projeto do AEM.
   1. Abra o projeto do AEM e navegue até `../blocks/form/components/`.
   1. Adicione uma nova pasta para o componente personalizado em `../blocks/form/components/<component_name>`. Neste exemplo, criamos uma pasta chamada `range`.
   1. Navegue até a pasta recém-criada em `../blocks/form/components/<component_name>`. Por exemplo, navegue até `../blocks/form/components/range` e adicione os seguintes arquivos:
      * `/blocks/form/components/range/_range.json`: contém a definição do componente personalizado.
      * `../blocks/form/components/range/range.css`: define o estilo do componente personalizado.
      * `../blocks/form/components/range/range.js`: Personaliza o componente personalizado no tempo de execução.

        ![Adicionando o componente personalizado para criação](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > Certifique-se de que o arquivo json inclua um sublinhado (_) como um prefixo em seu nome de arquivo.

1. Navegue até o arquivo `/blocks/form/components/range/_range.json` e adicione a definição do componente para o componente personalizado.

1. **Adicionar a definição do componente**

   Para adicionar a definição, os campos que precisam ser adicionados ao arquivo `_range.json` são:

   * **título**: o título do componente que é exibido no Editor Universal.
   * **id**: um identificador exclusivo do componente.
   * **fieldType**: o Forms oferece suporte a vários **fieldType** para capturar tipos específicos de entrada de usuário. Você pode encontrar o [fieldType com suporte na seção Byte Extra](#supported-fieldtypes).
   * **resourceType**: cada componente personalizado tem um tipo de recurso associado com base em seu fieldType. Você pode encontrar o [resourceType com suporte na seção Byte Extra](#supported-resourcetype).
   * **jcr:title**: é semelhante a um título, mas é armazenado na estrutura do componente.
   * **fd:viewType**: representa o nome do componente personalizado. É o identificador exclusivo do componente. É necessário criar uma exibição personalizada para o componente.

O arquivo `_range.json`, após adicionar a definição do componente, é o seguinte:

```javascript
{
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ]
}
```

>[!NOTE]
>
> Todos os componentes relacionados ao formulário seguem a mesma abordagem que o Sites ao adicionar blocos ao Universal Editor. Consulte o artigo [Criação de blocos instrumentados para uso com o Editor universal](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block) para obter mais informações.

### 2. Definir as propriedades do componente personalizado para criação

O componente personalizado inclui um modelo de componente que especifica quais propriedades são configuráveis pelo autor do formulário. Essas propriedades aparecem na caixa de diálogo **Propriedades** do Editor Universal, permitindo que os autores ajustem configurações como rótulos, regras de validação, estilos e outros atributos. Para definir propriedades:

1. Navegue até o arquivo `/blocks/form/components/range/_range.json` e adicione o modelo de componente para o componente personalizado.

1. **Adicionar o modelo de componente**

   Para definir o modelo do componente para seu componente personalizado, é necessário adicionar os campos relevantes ao arquivo `_range.json`.

   1. **Criar novo modelo**

      * Na matriz de modelos, adicione um novo objeto e defina o `id` do modelo de componente para corresponder à propriedade `fd:viewType` configurada anteriormente na definição do componente.
      * Incluir uma matriz de campos neste objeto.

   2. **Definir Campos para a caixa de diálogo Propriedade**

      * Cada objeto na matriz de campos deve ser um componente do tipo contêiner, permitindo que apareça como uma guia na caixa de diálogo **Propriedade**.
      * Alguns campos podem fazer referência a propriedades reutilizáveis disponíveis em `models/form-common`.

   3. **Usar um modelo de componente existente como referência**

      * Você pode copiar o conteúdo de um modelo de componente existente que corresponda ao `fieldType` escolhido e modificá-lo conforme necessário. Por exemplo, o componente `number-input` é estendido para criar um componente **range**, para que possamos usar a matriz de modelos de `models/form-components/_number-input.json` como uma referência.

   O arquivo `_range.json`, após adicionar o modelo de componente, é o seguinte:

   ```javascript
   "models": [
   {
     "id": "range",
     "fields": [
       {
         "component": "container",
         "name": "basic",
         "label": "Basic",
         "collapsible": false,
         "...": "../../../../models/form-common/_basic-input-fields.json"
       },
       {
         "...": "../../../../models/form-common/_help-container.json"
       },
       {
         "component": "container",
         "name": "validation",
         "label": "Validation",
         "collapsible": true,
         "...": "../../../../models/form-common/_number-validation-fields.json"
       }
     ]
   }
   ]
   ```

   >[!NOTE]
   >
   > Para adicionar um novo campo à caixa de diálogo **Propriedade** de um componente personalizado, siga o [esquema definido](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model).

   Você também pode [adicionar propriedades personalizadas](#adding-custom-properties-for-your-custom-component) a um componente personalizado para estender sua funcionalidade.

#### Adicionar propriedades personalizadas ao seu componente personalizado

As propriedades personalizadas permitem definir comportamentos específicos com base em valores definidos na caixa de diálogo Propriedade de um componente. Isso ajuda a estender a funcionalidade do componente e as opções de personalização.

Neste exemplo, adicionamos o Valor da etapa como uma propriedade personalizada ao componente Intervalo.

![Propriedade personalizada de valor de etapa](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

Para adicionar a propriedade personalizada Valor da Etapa, anexe o modelo de componente com as seguintes linhas de código no arquivo ` _<component>.json`:

```javascript
      {
      "component": "number",
      "name": "stepValue",
      "label": "Step Value",
      "valueType": "number"
      }
```

O trecho JSON define uma propriedade personalizada chamada **Valor da Etapa** para um componente **Intervalo**. Abaixo está uma análise de cada campo:

* **componente**: especifica o tipo de campo de entrada usado na caixa de diálogo Propriedade. Nesse caso, `number` indica que o campo aceita valores numéricos.
* **nome**: o identificador da propriedade, usado para referenciá-la na lógica do componente. Aqui, `stepValue` representa a configuração do valor da etapa para o intervalo.
* **rótulo**: o nome para exibição da propriedade conforme visto na caixa de diálogo Propriedade.
* **valueType**: define o tipo de dados esperado para a propriedade. `number` garante que somente entradas numéricas sejam permitidas.

Agora você pode usar `stepValue` como uma propriedade personalizada nas propriedades JSON de `range.js` e implementar o comportamento dinâmico com base em seu valor no tempo de execução.

Portanto, o arquivo `_range.json` final, após adicionar a definição do componente, o modelo do componente e as propriedades personalizadas, é o seguinte:

```javascript
 {
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ],
  "models": [
    {
      "id": "range",
      "fields": [
        {
          "component": "container",
          "name": "basic",
          "label": "Basic",
          "collapsible": false,
          "...": "../../../../models/form-common/_basic-input-fields.json"
         {
           "component": "number",
           "name": "stepValue",
            "label": "Step Value",
             "valueType": "number"
}
        },
        {
          "...": "../../../../models/form-common/_help-container.json"
        },
        {
          "component": "container",
          "name": "validation",
          "label": "Validation",
          "collapsible": true,
          "...": "../../../../models/form-common/_number-validation-fields.json"
        }
      ]
    }
  ]
}
```

![definição e modelo de componente](/help/edge/docs/forms/universal-editor/assets/custom-component-json-file.png)


### 3. Tornar o componente personalizado visível na lista de componentes do WYSIWYG

Um filtro define em qual seção o componente personalizado pode ser usado no Universal Editor. Isso garante que o componente só possa ser usado em seções apropriadas, mantendo a estrutura e a usabilidade.

Para garantir que o componente personalizado apareça na lista de componentes disponíveis durante a criação do formulário no WYSIWYG:

1. Navegue até o arquivo `/blocks/form/_form.json`.
1. Localize a matriz de componentes dentro do objeto que tem `id="form"`.
1. Adicione o valor `fd:viewType` de `definitions[]` à matriz de componentes do objeto com `id="form"`.

```javascript
 "filters": [
    {
      "id": "form",
      "components": [
        "captcha",
        "checkbox",
        "checkbox-group",
        "date-input",
        "drop-down",
        "email",
        "file-input",
        "form-accordion",
        "form-button",
        "form-fragment",
        "form-image",
        "form-modal",
        "form-reset-button",
        "form-submit-button",
        "number-input",
        "panel",
        "plain-text",
        "radio-group",
        "rating",
        "telephone-input",
        "text-input",
        "tnc",
        "wizard",
        "range"
      ]
    }
  ]
```

![filtro de componente](/help/edge/docs/forms/universal-editor/assets/custom-component-form-file.png)

### 4. Registrar o componente personalizado

Para permitir que o bloco de formulário reconheça o componente personalizado e carregue suas propriedades definidas no modelo de componente durante a criação do formulário, adicione o valor `fd:viewType` da definição de componente ao arquivo `mappings.js`.
Para registrar um componente:
1. Navegue até o arquivo `/blocks/form/mappings.js`.
1. Localize a matriz `customComponents[]`.
1. Adicione o valor `fd:viewType` da matriz `definitions[]` à matriz `customComponents[]`.

```javascript
let customComponents = ["range"];
const OOTBComponentDecorators = ['file-input',
                                 'wizard', 
                                 'modal', 'tnc',
                                'toggleable-link',
                                'rating',
                                'datetime',
                                'list',
                                'location',
                                'accordion'];
```

![mapeamento de componentes](/help/edge/docs/forms/universal-editor/assets/custom-component-mapping-file.png)

Depois de concluir as etapas acima, o componente personalizado aparece na lista de componentes do formulário no Editor universal. Em seguida, você pode arrastá-lo e soltá-lo na seção do formulário.

![componente de intervalo](/help/edge/docs/forms/universal-editor/assets/custom-component-range.png)

A captura de tela abaixo mostra as propriedades do componente `range` adicionadas ao modelo de componente, que especifica as propriedades que o autor do formulário pode configurar.:

![Propriedades do componente de intervalo](/help/edge/docs/forms/universal-editor/assets/range-properties.png)

Agora é possível definir o comportamento em tempo de execução do componente personalizado adicionando estilo e funcionalidade.

### 5. Adicionar o comportamento do tempo de execução ao componente personalizado

Você pode modificar componentes personalizados usando marcação predefinida, conforme explicado em [Estilo de campos de formulário](/help/edge/docs/forms/style-theme-forms.md). Isso pode ser feito com CSS personalizado (Folhas de estilo em cascata) e código personalizado para aprimorar a aparência do componente. Para adicionar o comportamento do tempo de execução do componente:

1. Para adicionar o estilo, navegue até o arquivo `/blocks/form/components/range/range.css` e adicione a seguinte linha de código:

   ```javascript
   /** Styling for range */
   main .form .range-widget-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, #ADD8E6 calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-widget-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-widget-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #00008B; /* Dark Blue */
   border: 3px solid #00008B; /* Dark Blue */
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-widget-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: #00008B; /* Dark Blue */
   }
   
   .range-widget-wrapper.decorated .range-bubble {
   color: #00008B; /* Dark Blue */
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   font-weight: bold;
   }
   
   .range-widget-wrapper.decorated .range-min,
   .range-widget-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-widget-wrapper.decorated .range-max {
   float: right;
   }
   ```

   O código ajuda a definir o estilo e a aparência visual do componente personalizado.

1. Para adicionar a funcionalidade, navegue até o arquivo `/blocks/form/components/range/range.js` e adicione a seguinte linha de código:

   ```javascript
   function updateBubble(input, element) {
   const step = input.step || 1;
   const max = input.max || 0;
   const min = input.min || 1;
   const value = input.value || 1;
   const current = Math.ceil((value - min) / step);
   const total = Math.ceil((max - min) / step);
   const bubble = element.querySelector('.range-bubble');
   // during initial render the width is 0. Hence using a default here.
   const bubbleWidth = bubble.getBoundingClientRect().width || 31;
   const left = `${(current / total) * 100}% - ${(current / total) * bubbleWidth}px`;
   bubble.innerText = `${value}`;
   const steps = {
       '--total-steps': Math.ceil((max - min) / step),
       '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   
   export default async function decorate(fieldDiv, fieldJson) {
   console.log('RANGE DIV: ', fieldDiv);
   console.log('RANGE JSON: fieldJson', fieldJson);
    const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 10;
   input.max = input.max || 1000;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper decorated';
   input.after(div);
   const hover = document.createElement('span');
   hover.className = 'range-bubble';
   const rangeMinEl = document.createElement('span');
   rangeMinEl.className = 'range-min';
   const rangeMaxEl = document.createElement('span');
   rangeMaxEl.className = 'range-max';
   rangeMinEl.innerText = `${input.min || 1}`;
   rangeMaxEl.innerText = `${input.max}`;
   div.appendChild(hover);
   // move the input element within the wrapper div
   div.appendChild(input);
   div.appendChild(rangeMinEl);
   div.appendChild(rangeMaxEl);
   input.addEventListener('input', (e) => {
   updateBubble(e.target, div);
   });
   updateBubble(input, div);
   return fieldDiv;
   }
   ```

   Ele controla como o componente personalizado interage com as entradas do usuário, processa dados e se integra ao bloco de formulários no Editor universal.

   Depois de incorporar o estilo e a funcionalidade personalizados, a aparência e o comportamento do componente de Intervalo são aprimorados. O design atualizado reflete os estilos aplicados, enquanto a funcionalidade adicionada garante uma experiência do usuário mais dinâmica e interativa.
A captura de tela abaixo ilustra o componente de intervalo atualizado.

![Estilo do componente do intervalo](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## Perguntas frequentes

* **Se eu adicionar estilo em component.css e forms.css, qual terá prioridade?**
Quando os estilos são definidos em `component.css` e **forms.css**, `component.css` tem prioridade. Isso ocorre porque os estilos no nível do componente são mais específicos e substituem os estilos globais de `forms.css`.

* **Meu componente personalizado não está visível na lista de componentes disponíveis no Universal Editor. Como posso corrigir isso?**
Se o componente personalizado não estiver aparecendo, verifique os seguintes arquivos para garantir que o componente esteja registrado corretamente:
   * **component-definition.json**: verifique se o componente está definido corretamente.
   * **component-filters.json**: verifique se o componente é permitido nas seções apropriadas.
   * **component-models.json**: Confirme se o modelo de componente está configurado corretamente.

## Práticas recomendadas

* É recomendável [configurar um ambiente de desenvolvimento do AEM](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment) local para desenvolver estilos e componentes personalizados localmente.


## Byte extra

### resourceType compatível

| Tipo de campo | Tipo de recurso |
|--------------|------------------------------------------------------------------|
| text-input | core/fd/components/form/textinput/v1/textinput |
| number-input | core/fd/components/form/numberinput/v1/numberinput |
| date-input | core/fd/components/form/datepicker/v1/datepicker |
| painel | core/fd/components/form/panelcontainer/v1/panelcontainer |
| caixa de seleção | core/fd/components/form/checkbox/v1/checkbox |
| menu suspenso | core/fd/components/form/dropdown/v1/dropdown |
| grupo de rádio | core/fd/components/form/radiobutton/v1/radiobutton |
| texto sem formatação | core/fd/components/form/text/v1/text |
| entrada de arquivo | core/fd/components/form/fileinput/v2/fileinput |
| email | core/fd/components/form/emailinput/v1/emailinput |
| imagem | core/fd/components/form/image/v1/image |
| botão | core/fd/components/form/button/v1/button |

### Tipos de campo aceitos

Os fieldTypes compatíveis para formulários são:
* text-input
* number-input
* date-input
* painel
* caixa de seleção
* menu suspenso
* grupo de rádio
* texto sem formatação
* entrada de arquivo
* email
* imagem
* botão

## Consulte também:

{{universal-editor-see-also}}
