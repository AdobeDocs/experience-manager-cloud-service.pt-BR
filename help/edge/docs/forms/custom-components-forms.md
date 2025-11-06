---
title: Criar componentes personalizados para um formulário EDS
description: Criar componentes personalizados para um formulário EDS
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Developer
exl-id: 77e90657-38db-4a49-9aac-3f3774b62624
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 1%

---

# Criar componentes personalizados

O Edge Delivery Services for AEM Forms permite personalizar os [componentes de formulário nativos do HTML](/help/edge/docs/forms/form-components.md) e criar formulários amigáveis e interativos. Ela permite modificar os componentes de formulário com marcação predefinida, conforme explicado em [Estilo de campos de formulário](/help/edge/docs/forms/style-theme-forms.md) usando CSS personalizado (Folhas de estilo em cascata) e código personalizado para decorar o componente, melhorando assim a aparência dos campos de formulário em um Bloco de Forms adaptável.

![Componente personalizado](/help/edge/assets/custom-component-image.png)

Este documento descreve as etapas para criar componentes personalizados estilizando os componentes de formulário nativos do HTML para melhorar a experiência do usuário e aumentar o apelo visual do formulário.

Vamos ver um exemplo de um componente `range` que exibe `Estimated trip cost` em um formulário. O componente `range` aparece como uma linha reta, sem mostrar valores como o mínimo, o máximo ou o valor selecionado.

![Componente de Intervalo Nativo](/help/edge/assets/native-range-component.png)

Vamos começar a personalizar o campo `range` para mostrar os valores mínimo, máximo e selecionado na linha adicionando estilo usando CSS e adicionando uma função personalizada para decorar um componente.

![Componente de intervalo personalizado](/help/edge/assets/custom-range-component.png)

No final deste artigo, você aprenderá a criar componentes personalizados, adicionando estilos ao arquivo CSS e à função personalizada.

## Pré-requisitos

Antes de começar a criar seu componente personalizado, você deve:

- Ter um conhecimento básico de [componentes nativos do HTML](/help/edge/docs/forms/form-components.md).
- Saiba como [estilizar campos de formulário com base no tipo de campo usando os seletores de CSS](/help/edge/docs/forms/style-theme-forms.md)


## Criar um componente personalizado


![etapas para criar componente personalizado](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

Agora vamos entender cada etapa em detalhes.

<!--Refer to the [enquiry spreadsheet](/help/edge/docs/forms/assets/enquiry.xlsx) to customize the `range` component, by following the steps as explained below.-->

### Adicionar uma função personalizada para decorar o componente

A função personalizada adicionada em `[../Form Block/components]` consiste em:

- **Declaração de função**: defina o nome da função e seus parâmetros.
- **Implementação lógica**: escreva a lógica para adicionar o comportamento personalizado do componente.
- **Exportação de função**: tornar a função acessível em `[Form Block]`.

Para adicionar uma função personalizada:

1. Navegue até `[../Form Block/components]`.
1. Localize um arquivo chamado `range.js`. se não estiver presente, crie-o.
1. Adicione a seguinte linha de código:

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
   '--total-steps': Math.ceil((max - min) /    step),
   '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   // eslint-disable-next-line no-unused-vars
   export default function decorateRange(fieldDiv, field) {
   loadCSS('/blocks/form/components/range/range.css');
   const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 1;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper';
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
   // as a best practice add a custom css class to apply custom styling
   fieldDiv.classList.add('decorated');
   return fieldDiv;    
   }
   ```

1. Salve as alterações.

### Inserir o decorador no Bloco de Formulário

O `[Form Block]` usa o HTML semântico para renderizar campos de formulário, incluindo campos de entrada, rótulos e texto de ajuda, com atributos padrão para acessibilidade. Para que o `[Form Block]` use o decorador personalizado para um componente especificado, defina-o no arquivo `mappings.js`. O arquivo `mappings.js` importa uma função que retorna o módulo responsável pela decoração de um componente específico. A função pega as propriedades do campo e retorna uma função de decorador para o campo de formulário.

Em nosso caso, a função verifica a propriedade `fieldType` do campo e retorna o decorador de intervalo personalizado do arquivo `range.js` presente em `[../Form Block/components]`.

Para inserir o decorador no Bloco de formulário:

1. Vá para `[../Form Block/]` e abra `mapping.js`.
1. Adicione a seguinte linha de código:

   ```javascript
   export default async function componentDecorator(fd) {
   const { ':type': type = '', fieldType } = fd;
   .... existing code ....
   if (fieldType === 'range') {
   const module = await import('./components/range.js');
   return module.default(element,fd);
   }
    return null; // null should be returned to use the original markup
   }
   ```

1. Salve as alterações.

### Adicionar estilo para o componente no arquivo CSS

Você pode alterar a aparência dos campos de formulário com base no tipo de campo e nos nomes de campo usando seletores CSS, permitindo um estilo consistente ou exclusivo com base nos requisitos. Para estilizar o componente, adicione código no arquivo `form.css` para modificar a aparência do componente de formulário.

Para personalizar o estilo do componente `range`, inclua um trecho de código CSS que estilize um elemento de entrada `range` e seus componentes associados dentro de um formulário. Isso pressupõe um layout estruturado de HTML com classes como `.form` e `.range-wrapper`.

Para adicionar o estilo de um componente no arquivo CSS:

1. Vá para `[../Form Block/]` e abra `form.css`.
1. Adicione a seguinte linha de código:

   ```javascript
       /** styling for range */
   main .form .range-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, var(--button-primary-color) calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #fff;
   border: 3px solid var(--button-primary-color);
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: var(--button-primary-color);
   }
   
   .range-wrapper.decorated .range-bubble {
   color: #17252e;
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   }
   
   .range-wrapper.decorated .range-min,
   .range-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-wrapper.decorated .range-max {
   float: right;
   }
   ```

1. Salve as alterações.

### Implantar os arquivos e criar o projeto

Implante os arquivos `range.js`, `mapping.js` e `form.css` atualizados no projeto GitHub e verifique se a compilação foi bem-sucedida.

### Visualizar o formulário usando o AEM sidekick

Visualize o formulário com a função recém-implementada que estiliza o componente `range`.

![Formulário de componente personalizado](/help/edge/assets/custom-componet-form.png)

O novo estilo do componente `range` mostra os valores mínimo, máximo e selecionado na linha ao adicionar estilos usando CSS e uma função personalizada que inclui um decorador para o componente.


