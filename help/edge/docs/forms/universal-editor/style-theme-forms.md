---
title: Personalizar tema e estilo para um Edge Delivery Services para AEM Forms
description: Personalize efetivamente o tema e o estilo do AEM Forms fornecido pela Edge Delivery Services, garantindo uma experiência do usuário coesa e de marca.
feature: Edge Delivery Services
role: Admin, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 0%

---

# Personalizar a aparência dos formulários

O estilo de formulário no Edge Delivery Services para AEM Forms requer uma compreensão sofisticada das propriedades personalizadas de CSS, arquitetura baseada em blocos e estratégias de direcionamento específicas de componentes. Diferentemente das abordagens tradicionais de estilo de formulário, o bloco adaptável do Forms implementa um sistema de token de design sistemático que permite a criação de temas consistentes, mantendo os benefícios de desempenho e acessibilidade do Edge Delivery Services.

A arquitetura de blocos do Adaptive Forms gera estruturas padronizadas do HTML em todos os componentes de formulário, criando padrões previsíveis para o direcionamento e a personalização de CSS. Essa consistência permite que os desenvolvedores implementem sistemas de estilo abrangentes que podem ser dimensionados em implementações de formulários complexas, preservando ao mesmo tempo as otimizações de desempenho baseadas em blocos que tornam o Edge Delivery Services excepcionalmente rápido.

Este guia abrangente aborda os fundamentos técnicos do estilo de formulário no ecossistema do Edge Delivery Services, incluindo sistemas de propriedades personalizadas CSS, padrões de estrutura de HTML de componentes e técnicas de estilo avançadas. A documentação fornece compreensão teórica e orientação prática de implementação para criar experiências de formulário sofisticadas e de marca.

## O que você vai dominar

**Domínio de Propriedades Personalizadas de CSS**: Entenda o sistema completo de variáveis que controla a aparência do formulário, incluindo esquemas de cores, escalas de tipografia, sistemas de espaçamento e parâmetros de layout. Saiba como substituir e estender essas propriedades para implementar temas de marca abrangentes.

**Noções básicas sobre arquitetura de componentes**: obtenha um conhecimento profundo dos padrões de estrutura do HTML usados por cada tipo de componente de formulário, permitindo o direcionamento e a personalização precisos de CSS sem romper a funcionalidade subjacente ou os recursos de acessibilidade.

**Técnicas avançadas de estilo**: implemente padrões de estilo sofisticados, incluindo estilo baseado em estado, integração de design responsiva e estratégias de personalização com desempenho otimizado que mantenham as características de carregamento rápido do Edge Delivery Services.

**Estratégias de implementação profissional**: conheça as abordagens padrão do setor para o estilo de formulários, incluindo a integração do sistema de design, a arquitetura CSS que pode ser mantida e técnicas de solução de problemas para cenários de estilo complexos.

## Noções básicas sobre tipos de campos de formulário

Antes de mergulhar no estilo, vamos rever os [tipos de campo](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes) de formulário comuns compatíveis com o Bloco de Forms adaptável:

- Campos de entrada: incluem entradas de texto, entradas de email, entradas de senha e muito mais.
- Grupos de caixas de seleção: usado para selecionar várias opções.
- Grupos de opções: usados para selecionar apenas uma opção de um grupo.
- Menus suspensos: também conhecido como caixas de seleção, usadas para selecionar uma opção de uma lista.
- Painéis/Contêineres: usado para agrupar elementos de formulário relacionados.

## Princípios básicos de estilo

Entender os [conceitos CSS fundamentais](https://www.w3schools.com/css/css_intro.asp) é fundamental antes de estilizar campos de formulário específicos:

- [Seletores](https://www.w3schools.com/css/css_selectors.asp): os Seletores de CSS permitem direcionar elementos HTML específicos para o estilo. Você pode usar seletores de elemento, seletores de classe ou seletores de ID.
- [Propriedades](https://www.w3schools.com/css/css_syntax.asp): as propriedades CSS definem a aparência visual dos elementos. As propriedades comuns para os campos de formulário de estilo incluem cor, cor de fundo, borda, preenchimento, margem e muito mais.
- [Modelo de caixa](https://www.w3schools.com/css/css_boxmodel.asp): o modelo de caixa CSS descreve a estrutura dos elementos do HTML como uma área de conteúdo cercada por preenchimento, bordas e margens.
- Flexbox/Grade: CSS [Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) e [Layouts de grade](https://www.w3schools.com/css/css_grid.asp) são ferramentas poderosas para criar designs responsivos e flexíveis.




## Estilo de formulário abrangente com propriedades personalizadas de CSS

O bloco adaptável do Forms utiliza uma arquitetura CSS sofisticada criada em propriedades personalizadas (variáveis CSS) que permite a definição de temas sistemática e o estilo consistente em todos os componentes do formulário. Entender essa estrutura é essencial para uma personalização eficaz do formulário e identidade visual.

### Noções básicas sobre a arquitetura do forms.css

Os estilos de formulário padrão estão localizados no repositório do projeto em `/blocks/form/form.css` e seguem uma abordagem estruturada que prioriza a manutenção, a consistência e a flexibilidade de personalização. A arquitetura consiste em vários componentes principais:

**Fundação de Propriedades Personalizadas de CSS**: o sistema de estilos é criado com base nas propriedades personalizadas de CSS definidas no nível `:root`, fornecendo um sistema de temas centralizado que funciona em cascata em todos os componentes de formulário. Essas variáveis estabelecem tokens de design para cores, tipografia, espaçamento e propriedades de layout.

**Estrutura CSS Baseada em Blocos**: a Edge Delivery Services emprega uma arquitetura baseada em blocos, na qual a classe `.form` serve como namespace primário para todos os estilos relacionados a formulários, garantindo o isolamento adequado do escopo e evitando conflitos de CSS com outros componentes da página.

**Estilo específico de componente**: componentes de formulário individuais são estilizados usando padrões de invólucro consistentes (`.{Type}-wrapper`) que fornecem direcionamento previsível para diferentes tipos de campo, mantendo a integridade geral do sistema de design.

### Referência e personalização de propriedades personalizadas de CSS

O sistema de estilo de formulário inclui mais de 50 propriedades personalizadas de CSS que controlam cada aspecto da aparência e do comportamento do formulário. Compreender essas propriedades permite uma personalização abrangente, mantendo a consistência do design.

+++ Variáveis de cores e temas

O sistema de cores estabelece uma base visual completa para formulários por meio de propriedades personalizadas cuidadosamente organizadas:

```css
:root {
    /* Primary color system */
    --background-color-primary: #fff;
    --label-color: #666;
    --border-color: #818a91;
    --form-error-color: #ff5f3f;
    
    /* Button color system */
    --button-primary-color: #5F8DDA;
    --button-secondary-color: #666;
    --button-primary-hover-color: #035fe6;
    
    /* Form-specific color applications */
    --form-background-color: var(--background-color-primary);
    --form-input-border-color: var(--border-color);
    --form-invalid-border-color: #ff5f3f;
    --form-label-color: var(--label-color);
}
```

**Exemplo de personalização prática**: para implementar um tema escuro em seus formulários, substitua as variáveis de cor base:

```css
:root {
    --background-color-primary: #1a1a1a;
    --label-color: #e0e0e0;
    --border-color: #404040;
    --form-error-color: #ff6b6b;
    --button-primary-color: #4a9eff;
}
```

Essa única alteração se propaga por todos os componentes do formulário porque o sistema usa referências variáveis em vez de valores codificados.

+++

+++ Variáveis de tipografia e espaçamento

As variáveis de tipografia e espaçamento fornecem controle abrangente sobre a apresentação de texto e o espaçamento do layout:

```css
:root {
    /* Font size system */
    --form-font-size-m: 22px;
    --form-font-size-s: 18px;
    --form-font-size-xs: 16px;
    
    /* Component-specific typography */
    --form-label-font-size: var(--form-font-size-s);
    --form-label-font-weight: 400;
    --form-title-font-weight: 600;
    --form-input-font-size: 1rem;
    
    /* Spacing system */
    --form-field-horz-gap: 40px;
    --form-field-vert-gap: 20px;
    --form-input-padding: 0.75rem 0.6rem;
    --form-padding: 0 10px;
}
```

**Exemplo de personalização prática**: Para criar um layout de formulário mais compacto com tipografia menor:

```css
:root {
    --form-font-size-m: 18px;
    --form-font-size-s: 14px;
    --form-font-size-xs: 12px;
    --form-field-horz-gap: 20px;
    --form-field-vert-gap: 15px;
    --form-input-padding: 0.5rem 0.4rem;
}
```

+++

+++ Variáveis de layout e estrutura

As variáveis de layout controlam as dimensões do formulário, o comportamento da grade e a organização do componente:

```css
:root {
    /* Form layout */
    --form-width: 100%;
    --form-columns: 12;
    --form-submit-width: 100%;
    
    /* Card-based components */
    --form-card-border-radius: 4px;
    --form-card-padding: 0.6rem 0.8rem;
    --form-card-shadow: 0 1px 2px rgb(0 0 0 / 3%);
    --form-card-hover-shadow: 0 2px 4px rgb(0 0 0 / 6%);
    
    /* Wizard-specific layout */
    --form-wizard-padding: 0px;
    --form-wizard-padding-bottom: 160px;
    --form-wizard-step-legend-padding: 10px;
}
```

**Exemplo de personalização prática**: Para criar um formulário de estilo cartão com profundidade visual aprimorada:

```css
:root {
    --form-card-border-radius: 12px;
    --form-card-padding: 1.5rem 2rem;
    --form-card-shadow: 0 4px 12px rgb(0 0 0 / 8%);
    --form-card-hover-shadow: 0 8px 24px rgb(0 0 0 / 12%);
    --form-background-color: #f8f9fa;
}

.form {
    background: var(--form-background-color);
    border-radius: var(--form-card-border-radius);
    box-shadow: var(--form-card-shadow);
    padding: var(--form-card-padding);
    max-width: 600px;
    margin: 2rem auto;
}
```

+++

### Padrões de estilo CSS e práticas recomendadas

O bloco adaptável do Forms segue padrões CSS específicos que garantem um estilo manutenível, com desempenho e consistente em todos os componentes.

+++ Padrões de estilo primários

**Contêiner de Formulário em Nível de Bloco**: Direcione o contêiner de formulário primário para o layout geral e estilo de plano de fundo:

```css
.form {
    /* Form-wide styles */
    max-width: 800px;
    margin: 0 auto;
    background-color: var(--form-background-color);
    padding: var(--form-padding);
    border-radius: var(--form-card-border-radius);
}
```

**Padrões de Wrapper de Componentes**: Direcione tipos de campo específicos usando classes de wrapper consistentes:

```css
/* Text input fields */
.form .text-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
    border-radius: 4px;
    width: 100%;
}

/* Email input fields */
.form .email-wrapper input {
    padding: var(--form-input-padding);
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    font-size: var(--form-input-font-size);
}

/* Button styling */
.form .button-wrapper button {
    background-color: var(--form-button-background-color);
    color: var(--form-button-color);
    padding: var(--form-button-padding);
    border: var(--form-button-border);
    font-size: var(--form-button-font-size);
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s ease;
}

.form .button-wrapper button:hover {
    background-color: var(--form-button-background-hover-color);
}
```

+++ 

+++ Padrões de personalização avançados

**Direcionamento Específico de Campo**: direcione campos individuais por nome para requisitos de estilo exclusivos:

```css
/* Style specific fields */
.form .field-email input {
    background-image: url('data:image/svg+xml;...'); /* Email icon */
    background-repeat: no-repeat;
    background-position: right 12px center;
    padding-right: 40px;
}

.form .field-phone input {
    text-align: center;
    letter-spacing: 1px;
    font-family: monospace;
}
```

**Estilo Baseado em Estado**: Implementar estados de validação e interação:

```css
/* Validation states */
.form .field-wrapper[data-valid="false"] input {
    border-color: var(--form-error-color);
    box-shadow: 0 0 0 2px rgba(255, 95, 63, 0.1);
}

.form .field-wrapper[data-valid="true"] input {
    border-color: #28a745;
    box-shadow: 0 0 0 2px rgba(40, 167, 69, 0.1);
}

/* Focus states */
.form .text-wrapper input:focus,
.form .email-wrapper input:focus {
    outline: none;
    border-color: var(--button-primary-color);
    box-shadow: 0 0 0 2px rgba(95, 141, 218, 0.2);
}
```

+++


## Estrutura de componentes

O bloco adaptável do Forms oferece uma estrutura consistente do HTML para vários elementos de formulário, garantindo um estilo e gerenciamento mais fáceis. É possível manipular os componentes usando o CSS para fins de estilo.

+++ Componentes gerais (exceto menus suspensos, grupos de rádio e grupos de caixas de seleção):

Todos os campos de formulário, exceto os menus suspensos, grupos de opções e grupos de caixas de seleção, têm a seguinte estrutura HTML:

### Estrutura HTML de componentes gerais

```HTML
  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     <label for="{FieldId}" class="field-label">First   Name</label>
     <input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>
```

- Classes: o elemento div tem várias classes para direcionar elementos específicos e estilo. Você precisa das classes `{Type}-wrapper` ou `field-{Name}` para desenvolver um Seletor de CSS para estilizar um campo de formulário:
- {Type}: Identifica o componente por tipo de campo. Por exemplo, texto (invólucro de texto), número (invólucro numérico), data (invólucro de data).
- {Name}: Identifica o componente por nome. O nome do campo pode ter apenas caracteres alfanuméricos, os vários traços consecutivos no nome são substituídos por um único traço `(-)` e os traços inicial e final em um nome de campo são removidos. Por exemplo, nome (field-first-name field-wrapper).
- {FieldId}: é um identificador exclusivo do campo, gerado automaticamente.
- {Required}: é um booleano indicando se o campo é obrigatório.
- Rótulo: o elemento `label` fornece um texto descritivo para o campo e o associa ao elemento de entrada usando o atributo `for`.
- Entrada: o elemento `input` define o tipo de dados a serem inseridos. Por exemplo, texto, número, email.
- Descrição (Opcional): O `div` com classe `field-description` fornece informações ou instruções adicionais para o usuário.

**Exemplo de estrutura HTML**

```HTML
<div class="text-wrapper field-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

#### Seletor de CSS para Componentes gerais

```css
/* Primary Pattern: Target field wrapper by type */
.form .{Type}-wrapper {
    /* Container styling for specific field types */
    margin-bottom: 1rem;
    border-radius: 4px;
}

/* Primary Pattern: Target input fields within wrapper */
.form .{Type}-wrapper input {
    /* Input field styling using CSS custom properties */
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
}

/* Context-specific: Target element by field name when higher specificity needed */
.form .field-{Name} input {
    /* Field-specific customizations */
    /* Use this pattern for unique styling requirements */
}
```

- `.form .{Type}-wrapper`: Direciona o elemento de wrapper de campo com base no tipo de campo. Por exemplo, `.form .text-wrapper` é direcionado a todos os contêineres de campo de texto.
- `.form .{Type}-wrapper input`: Direciona os elementos de entrada reais dentro do invólucro. Esse é o padrão recomendado para estilizar entradas de formulário.
- `.form .field-{Name}`: direciona elementos com base no nome do campo específico. Por exemplo, `.form .field-first-name` é direcionado ao contêiner de campo &quot;Nome&quot;. Use `.form .field-{Name} input` para direcionar o elemento de entrada especificamente.
- **Evitar**: `main .form form .{Type}-wrapper` - Isso cria especificidade CSS desnecessária e é mais difícil de manter.

**Exemplo de Seletores de CSS para Componentes Gerais**

```css
/* Primary Pattern: Target all text input fields */
.form .text-wrapper input {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    width: 100%;
    font-size: var(--form-input-font-size);
    background-color: var(--form-input-background-color);
}

/* Context-specific: Target field by name when higher specificity needed */
.form .field-first-name input {
    text-transform: capitalize;
    border-color: var(--button-primary-color);
}

/* Alternative with main context if needed */
main .form .text-wrapper input {
    /* Use only when you need higher specificity */
    color: var(--form-label-color);
}
```

+++

+++ Componente suspenso

Para menus suspensos, o elemento `select` é usado em vez de um elemento `input`:

#### Estrutura HTML do componente suspenso

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**Exemplo de estrutura do HTML**

```HTML
<div class="drop-down-wrapper field-country field-wrapper" data-required="true">
  <label for="country" class="field-label">Country</label>
  <select id="country" name="country">
    <option value="">Select Country</option>
    <option value="US">United States</option>
    <option value="CA">Canada</option>
  </select>
  <div class="field-description" aria-live="polite" id="country-description">
    Please select your country of residence.
  </div>
</div>
```

#### Seletores de CSS para o componente suspenso

O CSS a seguir lista alguns exemplos de Seletores de CSS para componentes suspensos.

```css
/* Primary Pattern: Target the dropdown wrapper */
.form .drop-down-wrapper {
    /* Container layout using flexbox */
    display: flex;
    flex-direction: column;
    margin-bottom: var(--form-field-vert-gap);
}

/* Target the select element */
.form .drop-down-wrapper select {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    background-color: var(--form-input-background-color);
    font-size: var(--form-input-font-size);
    color: var(--form-label-color);
}

/* Style the label */
.form .drop-down-wrapper .field-label {
    margin-bottom: 5px;
    font-weight: var(--form-label-font-weight);
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
}
```

- Direcionar o Wrapper: o primeiro seletor (`.drop-down-wrapper`) direciona o elemento wrapper externo, garantindo que os estilos se apliquem a todo o componente suspenso.
- Layout Flexbox: O Flexbox organiza o rótulo, a lista suspensa e a descrição verticalmente para um layout limpo.
- Estilo do rótulo: o rótulo se destaca com uma espessura de fonte mais ousada e uma pequena margem.
- Estilo suspenso: o elemento `select` recebe uma borda, um preenchimento e cantos arredondados para obter uma aparência polida.
- Cor do plano de fundo: uma cor de fundo consistente é definida para harmonia visual.
- Personalização de seta: os estilos opcionais ocultam a seta suspensa padrão e criam uma seta personalizada usando um caractere Unicode e o posicionamento.

+++

+++ Grupos de opções

Semelhante aos componentes suspensos, os grupos de rádio têm sua própria estrutura HTML e estrutura CSS:

#### Estrutura HTML do grupo de rádio

```HTML
<fieldset class="radio-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
      <input type="radio" value="" id="{UniqueId}" data-field-type="radio-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**Exemplo de estrutura do HTML**

```HTML
<fieldset class="radio-group-wrapper field-color field-wrapper" id="color_preference" name="color_preference" data-required="true">
  <legend for="color_preference" class="field-label">Favorite Color:</legend>
  <% for each radio in Group %>
    <div class="radio-wrapper field-color">
      <input type="radio" value="red" id="color_red" data-field-type="radio-group" name="color_preference">
      <label for="color_red" class="field-label">Red</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="green" id="color_green" data-field-type="radio-group" name="color_preference">
      <label for="color_green" class="field-label">Green</label>
    </div>
    <div class="radio-wrapper field-color">
      <input type="radio" value="blue" id="color_blue" data-field-type="radio-group" name="color_preference">
      <label for="color_blue" class="field-label">Blue</label>
    </div>
  <% end for %>
</fieldset>
```

#### Seletores de CSS para grupos de botões de opção

- Direcionamento do conjunto de campos

```css
/* Target radio group container */
.form .radio-group-wrapper {
    border: var(--form-input-border-size) solid var(--form-input-border-color);
    padding: var(--form-input-padding);
    border-radius: 4px;
    margin-bottom: var(--form-field-vert-gap);
}
```

Este seletor segmenta qualquer conjunto de campos com a classe radio-group-wrapper. Isso seria útil para aplicar estilos gerais a todo o grupo de rádio.

- Rótulos do botão de opção de direcionamento

```css
/* Target radio button labels */
.form .radio-wrapper label {
    font-weight: var(--form-label-font-weight);
    margin-right: 10px;
    color: var(--form-label-color);
    font-size: var(--form-label-font-size);
    cursor: pointer;
}
```

- Direcionar todos os rótulos de botão de opção em um conjunto de campos específico com base em seu nome

```css
/* Target all radio button labels within a specific fieldset based on its name */
.form .field-color .radio-wrapper label {
    /* Field-specific radio label customizations */
    /* Add your custom styles here */
}
```

+++

+++ Grupos de caixas de seleção

#### Estrutura HTML do grupo de caixas de seleção

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="checkbox-wrapper field-{Name}">
      <input type="checkbox" value="" id="{UniqueId}" data-field-type="checkbox-group" name="{FieldId}">
      <label for="{UniqueId}" class="field-label">...</label>
   </div>
   <% end for %>
</fieldset>
```

**Exemplo de estrutura do HTML**

```HTML
<fieldset class="checkbox-group-wrapper field-topping field-wrapper" id="topping_preference" name="topping_preference" data-required="false">
  <legend for="topping_preference" class="field-label">Pizza Toppings:</legend>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="pepperoni" id="topping_pepperoni" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_pepperoni" class="field-label">Pepperoni</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="mushrooms" id="topping_mushrooms" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_mushrooms" class="field-label">Mushrooms</label>
  </div>
  <div class="checkbox-wrapper field-topping">
    <input type="checkbox" value="onions" id="topping_onions" data-field-type="checkbox-group" name="topping_preference">
    <label for="topping_onions" class="field-label">Onions</label>
  </div>
</fieldset>
```

#### Seletores de CSS para grupos de caixas de seleção

- Direcionamento do invólucro externo: esses seletores segmentam os contêineres mais externos de grupos de opções e caixas de seleção, permitindo aplicar estilos gerais a toda a estrutura do grupo. Isso é útil para definir o espaçamento, alinhamento ou outras propriedades relacionadas ao layout.

```css
/* Primary Pattern: Targets radio group wrappers */
.form .radio-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between radio groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}

/* Primary Pattern: Targets checkbox group wrappers */
.form .checkbox-group-wrapper {
    margin-bottom: var(--form-field-vert-gap); /* Adds space between checkbox groups */
    display: flex;
    flex-direction: column;
    border: var(--form-fieldset-border);
    padding: var(--form-input-padding);
}
```

- Rótulos do grupo de direcionamento: esse seletor direciona o elemento `.field-label` aos invólucros do grupo de caixas de seleção e de rádio. Isso permite estilizar os rótulos especificamente para esses grupos, possivelmente fazendo com que eles se destaquem mais.

```css
/* Primary Pattern: Target group labels */
.form .radio-group-wrapper legend,
.form .checkbox-group-wrapper legend {
    font-weight: var(--form-title-font-weight); /* Makes the group label bold */
    margin-bottom: 0.5rem;
    font-size: var(--form-fieldset-legend-font-size);
    color: var(--form-fieldset-legend-color);
    padding: var(--form-fieldset-legend-padding);
    border: var(--form-fieldset-legend-border);
}
```

- Direcionamento de entradas e rótulos individuais: esses seletores fornecem controle mais granular sobre botões de opção individuais, caixas de seleção e seus rótulos associados. Você pode usá-los para ajustar o dimensionamento, o espaçamento ou aplicar estilos visuais mais distintos.

```css
/* Primary Pattern: Styling radio buttons */
.form .radio-group-wrapper input[type="radio"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling radio button labels */
.form .radio-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}

/* Primary Pattern: Styling checkboxes */
.form .checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 8px; /* Adds space between the input and its label */
    margin-bottom: 4px;
    cursor: pointer;
}

/* Primary Pattern: Styling checkbox labels */
.form .checkbox-group-wrapper label {
    font-size: var(--form-label-font-size); /* Changes the label font size */
    color: var(--form-label-color);
    font-weight: var(--form-label-font-weight);
    display: flex;
    align-items: center;
    cursor: pointer;
}
```

- Personalização da aparência de botões de opção e caixas de seleção: essa técnica oculta a entrada padrão e usa pseudoelementos `:before` e `:after` para criar visuais personalizados que alteram a aparência com base no estado &quot;marcado&quot;.

```css
/* Hide the default radio button or checkbox */
.form .radio-group-wrapper input[type="radio"],
.form .checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    width: 1px;
    height: 1px;
}

/* Create a custom radio button */
.form .radio-group-wrapper input[type="radio"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 50%;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .radio-group-wrapper input[type="radio"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    box-shadow: inset 0 0 0 3px var(--form-input-background-color);
}

/* Create a custom checkbox */
.form .checkbox-group-wrapper input[type="checkbox"] + label::before {
    content: '';
    display: inline-block;
    width: 16px;
    height: 16px;
    border: 2px solid var(--form-input-border-color);
    border-radius: 2px;
    margin-right: 8px;
    background-color: var(--form-input-background-color);
    transition: all 0.2s ease;
}

.form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
    background-color: var(--button-primary-color);
    border-color: var(--button-primary-color);
    background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16"><path fill="white" d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/></svg>');
    background-repeat: no-repeat;
    background-position: center;
}
```

+++

+++ Componentes de painel/contêiner

#### Estrutura HTML dos componentes do painel/contêiner

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
  </div>
</fieldset>
```

**Exemplo de estrutura do HTML**

```HTML
<fieldset class="panel-wrapper field-login field-wrapper">
  <legend for="login" class="field-label" data-visible="false">Login Information</legend>
  <div class="text-wrapper field-username field-wrapper">
    <label for="username" class="field-label">Username</label>
    <input type="text" placeholder="Enter your username" maxlength="50" id="username" name="username">
    <div class="field-description" aria-live="polite" id="username-description">
      Please enter your username or email address.
    </div>
  </div>
  <div class="password-wrapper field-password field-wrapper">
    <label for="password" class="field-label">Password</label>
    <input type="password" placeholder="Enter your password" maxlength="20" id="password" name="password">
    <div class="field-description" aria-live="polite" id="password-description">
      Your password must be at least 8 characters long.
    </div>
  </div>
</fieldset>
```

- O elemento fieldset atua como o contêiner do painel com o invólucro de painel de classe e classes adicionais para estilização com base no nome do painel (logon de campo).
- O elemento de legenda (`<legend>`) serve como o título do painel com o texto &quot;Informações de Logon&quot; e o rótulo de campo de classe. O atributo data-visible=&quot;false&quot; pode ser usado com o JavaScript para controlar a visibilidade do título.
- Dentro do conjunto de campos, vários.Os elementos {Type}-wrapper (.text-wrapper e .password-wrapper, neste caso) representam campos de formulário individuais dentro do painel.
- Cada invólucro contém um rótulo, campo de entrada e descrição, semelhantes aos exemplos anteriores.


#### Exemplo de seletores CSS para componentes de Painel/Contêiner

1. Direcionamento do painel:

```CSS
  /- Target the entire panel container */
  main .form form .panel-wrapper {
    /- Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

- O seletor `.panel-wrapper` estiliza todos os elementos com o invólucro de painel de classe, criando uma aparência consistente para todos os painéis.

1. Direcionamento do título do painel:

```CSS
  /- Target the legend element (panel title) */
  .panel-wrapper legend {
    /- Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /- Optional: create a separation line */
  }
```

- O seletor `.panel-wrapper legend` estiliza o elemento de legenda dentro do painel, fazendo com que o título se destaque visualmente.


1. Direcionamento de campos individuais no painel:

```CSS
/- Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

- O seletor `.panel-wrapper .{Type}-wrapper` é direcionado a todos os invólucros com a classe `.{Type}-wrapper` dentro do painel, permitindo que você estilize o espaçamento entre os campos de formulário.

1. Direcionamento de campos específicos (opcional):

```CSS
  /- Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username {
    /- Add your styles here (specific to username field) */
  }

  /- Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password {
    /- Add your styles here (specific to password field) */
  }
```

- Esses seletores opcionais permitem direcionar wrappers de campo específicos no painel para um estilo exclusivo, como realçar o campo de nome de usuário.


+++

+++ Painel repetível

#### Estrutura HTML de um painel repetível

```HTML
<fieldset class="panel-wrapper field-{PanelName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false">bannerComponent</legend>
  <div class="{Type}-wrapper field-{Name} field-wrapper">
    <label for="{FieldId}" class="field-label">First Name</label>
    <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}">
    <div class="field-description" aria-live="polite" id="{FieldId}-description">
      Hint - First name should be minimum 3 characters and a maximum of 10 characters.
    </div>
</fieldset>
```

**Exemplo de estrutura do HTML**

```HTML
<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-1" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-1" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-1" name="contacts[0].name">
    <div class="field-description" aria-live="polite" id="name-1-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-1" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-1" name="contacts[0].email">
    <div class="field-description" aria-live="polite" id="email-1-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>

<fieldset class="panel-wrapper field-contact field-wrapper" data-repeatable="true">
  <legend for="contact-2" class="field-label" data-visible="false">Contact Information</legend>
  <div class="text-wrapper field-name field-wrapper">
    <label for="name-2" class="field-label">Name</label>
    <input type="text" placeholder="Enter your name" maxlength="50" id="name-2" name="contacts[1].name">
    <div class="field-description" aria-live="polite" id="name-2-description">
      Please enter your full name.
    </div>
  </div>
  <div class="email-wrapper field-email field-wrapper">
    <label for="email-2" class="field-label">Email</label>
    <input type="email" placeholder="Enter your email address" maxlength="100" id="email-2" name="contacts[1].email">
    <div class="field-description" aria-live="polite" id="email-2-description">
      Please enter a valid email address.
    </div>
  </div>
</fieldset>
```

Cada painel tem a mesma estrutura que o exemplo de painel único, com atributos adicionais:

- data-repeat=&quot;true&quot;: este atributo indica que o painel pode ser repetido dinamicamente usando o JavaScript ou uma estrutura.

- IDs e nomes exclusivos: cada elemento no painel tem um ID exclusivo (por exemplo, name-1, email-1) e um atributo de nome com base no índice do painel (por exemplo, name=&quot;contacts[0].name&quot;). Isso permite a coleta de dados adequada quando vários painéis são enviados.


#### Seletores de CSS para um painel repetível

- Direcionamento de todos os painéis repetíveis:

```CSS
  /- Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] {
    /- Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

O seletor estimula todos os painéis que podem ser repetidos, garantindo uma aparência consistente.


- Direcionamento de campos individuais em um painel:

```CSS
/- Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /- Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

Este seletor estimula todos os invólucros de campo em um painel repetível, mantendo um espaçamento consistente entre os campos.

- Direcionamento de campos específicos (em um painel):

```CSS
/- Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /- Add your styles here (specific to first name field) */
}

/- Target all
```


+++


+++ Anexo de arquivo

#### Estrutura do HTML para anexo de arquivo

```HTML
<div class="file-wrapper field-{FileName} field-wrapper">
  <legend for="{id}" class="field-label" data-visible="false"> File Attachment </legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
    <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="{id}" name="{FileName}" autocomplete="off" multiple="" required="required">
  </div>
  <div class="files-list">
    <div data-index="0" class="file-description">
      <span class="file-description-name">ClaimForm.pdf</span>
      <span class="file-description-size">26 kb</span>
      <button class="file-description-remove" type="button"></button>
    </div>
  </div>
</div>
```

**Exemplo de estrutura do HTML**


```HTML
<div class="file-wrapper field-claim_form field-wrapper">
  <legend for="claim_form" class="field-label" data-visible="false">File Attachment</legend>
  <div class="file-drag-area">
    <div class="file-dragIcon"></div>
    <div class="file-dragText">Drag and Drop To Upload</div>
    <button class="file-attachButton" type="button">Attach</button>
  </div>
  <input type="file" accept="audio/*, video/*, image/*, text/*, application/pdf" id="claim_form"
         name="claim_form" autocomplete="off" multiple="" required="required" data-max-file-size="2MB">
  <div class="files-list">
    </div>
</div>
```

- O atributo de classe usa o nome fornecido para o anexo de arquivo (claim_form).
- Os atributos id e name do elemento de entrada correspondem ao nome do anexo de arquivo (claim_form).
- A seção da lista de arquivos está inicialmente vazia. Ele é preenchido dinamicamente com o JavaScript quando os arquivos são carregados.


#### Seletores de CSS para o componente de Anexo de arquivo

- Direcionar todo o componente de anexo de arquivo:

```CSS
/- Target the entire file attachment component */
main .form form .file-wrapper {
  /- Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

Este seletor estimula todo o componente de anexo do arquivo, incluindo a legenda, a área de arrastar, o campo de entrada e a lista.

- Direcionamento de elementos específicos:

```CSS
/- Target the drag and drop area */
main .form form .file-wrapper .file-drag-area {
  /- Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/- Target the file input element */
main .form form .file-wrapper input[type="file"] {
  /- Add your styles here (e.g., hide the default input) */
  display: none;
}

/- Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description {
  /- Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/- Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name {
  /- Add your styles here (e.g., font-weight) */
  font-weight: bold;
}
```

Esses seletores permitem estilizar várias partes do componente de anexo de arquivo individualmente. É possível ajustar os estilos para corresponder às suas preferências de design.

+++



## Componentes de estilo

Você pode estilizar campos de formulário com base em seu tipo específico (`{Type}-wrapper`) ou nomes individuais (`field-{Name}`). Isso permite um controle mais granular e a personalização da aparência do formulário.

+++ Estilo com base no tipo de campo

Você pode usar os Seletores de CSS para direcionar tipos de campo específicos e aplicar estilos de forma consistente.

### Estrutura do HTML

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id={FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
   </div>
</div>
```

**Exemplo de estrutura do HTML**

```HTML
<div class="text-wrapper field-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="number-wrapper field-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="email-wrapper field-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

- Cada campo é colocado em um elemento `div` com várias classes:
   - `{Type}-wrapper`: Identifica o tipo de campo. Por exemplo, `form-text-wrapper`, `form-number-wrapper`, `form-email-wrapper`.
   - `field-{Name}`: Identifica o campo pelo seu nome. Por exemplo `form-name`, `form-age`, `form-email`.
   - `field-wrapper`: uma classe genérica para todos os wrappers de campo.
- O atributo `data-required` indica se o campo é obrigatório ou opcional.
- Cada campo tem um rótulo correspondente, elemento de entrada e possíveis elementos adicionais, como espaços reservados e descrições.




### Exemplo de seletores CSS

```CSS
/- Primary Pattern: Target all text input fields */
.form .text-wrapper input {
  /- Add your styles here */
  width: 100%;
  padding: var(--form-input-padding);
}

/- Primary Pattern: Target all number input fields */
.form .number-wrapper input {
  /- Add your styles here */
  letter-spacing: 2px; /- Example for adding letter spacing to all number fields */
  text-align: center;
}
```

+++

+++ Estilo com base no nome do campo

Você também pode direcionar campos individuais por nome para aplicar estilos exclusivos.

#### Estrutura do HTML

```HTML
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required={Required}>
   <label for="{FieldId}" class="field-label">First Name</label>
   <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
   <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```

**Exemplo de estrutura do HTML**

```HTML
<div class="number-wrapper field-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp" aria-describedby="otp-description">
  <div class="field-description" aria-live="polite" id="otp-description">
    Hint - Enter the 6 digit number sent to your mobile number.
   </div>
</div>
```


#### Exemplo de seletor de CSS

```CSS
/- Primary Pattern: Target specific field by name */
.form .field-otp input {
   letter-spacing: 2px;
   text-align: center;
   font-family: monospace;
}

/- Context-specific: Use higher specificity when needed */
main .form .field-otp input {
   /- Use only when you need to override other styles */
   font-weight: bold;
}
```

Este CSS destina-se a todos os elementos de entrada localizados em um elemento que tem a classe `field-otp`. A estrutura do formulário do Edge Delivery Services segue as convenções de bloco do Adaptive Forms, onde os containers são marcados com classes específicas de campo, como &quot;field-otp&quot; para campos com o nome &quot;otp&quot;.


## Estrutura e implementação do arquivo CSS

### **Implementação de referência**

A referência completa do estilo do formulário está disponível no repositório do AEM Forms Boilerplate:

```
https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/blocks/form/form.css
```

Esse arquivo serve como a implementação canônica do sistema de propriedades personalizadas de CSS e fornece a base para todo o estilo de formulário. Ele inclui definições abrangentes para todas as variáveis CSS, padrões de estilo de componentes e implementações de design responsivas.

+++

+++ Integração de projeto

No seu projeto Edge Delivery Services, implemente o estilo de formulário por meio dessa abordagem estruturada:

```
/blocks/form/form.css          // Core form block styles (copied from boilerplate)
/styles/styles.css             // Global site styles and CSS variable overrides
/styles/lazy-styles.css        // Additional component enhancements
```

+++

+++ Estratégia de implementação

**Substituições de Propriedades Personalizadas de CSS**: substitua as variáveis de formulário nos seus estilos globais para implementar o tema específico da marca:

```css
/* In /styles/styles.css */
:root {
    /* Brand-specific overrides */
    --button-primary-color: #your-brand-color;
    --form-background-color: #your-background;
    --label-color: #your-text-color;
}
```

**Personalizações específicas de componente**:
Adicione o estilo específico do componente enquanto mantém o sistema de variáveis CSS:

```css
/* Enhanced component styling */
.form .text-wrapper input {
    border-radius: var(--form-card-border-radius);
    transition: all 0.2s ease;
}

.form .text-wrapper input:focus {
    transform: translateY(-1px);
    box-shadow: 0 0 0 3px rgba(var(--button-primary-color), 0.1);
}
```

**Integração de Design Responsiva**: utilize as propriedades personalizadas de CSS nas consultas de mídia para obter um comportamento responsivo consistente:

```css
@media (max-width: 768px) {
    :root {
        --form-input-padding: 0.875rem;
        --form-field-vert-gap: 1rem;
        --form-padding: 1rem;
    }
}
```

+++

### Exemplo completo de implementação de estilo

Esta seção demonstra como criar um formulário moderno e com marca usando propriedades personalizadas de CSS. A implementação é dividida em subseções claras para facilitar a compreensão e a navegação.



+++ &#x200B;1. Variáveis de tema da marca

Defina a paleta de cores, o espaçamento e a tipografia da sua marca usando as propriedades personalizadas de CSS.

```css
/* Custom brand theme */
:root {
  /* Brand color system */
  --brand-primary: #2563eb;
  --brand-secondary: #64748b;
  --brand-success: #059669;
  --brand-error: #dc2626;
  --brand-background: #f8fafc;
  
  /* Override form variables */
  --background-color-primary: #ffffff;
  --button-primary-color: var(--brand-primary);
  --button-primary-hover-color: #1d4ed8;
  --form-error-color: var(--brand-error);
  --form-background-color: var(--brand-background);
  --label-color: var(--brand-secondary);
  --border-color: #d1d5db;
  
  /* Enhanced spacing */
  --form-input-padding: 1rem;
  --form-field-vert-gap: 1.5rem;
  --form-padding: 2rem;
  
  /* Modern typography */
  --form-font-size-s: 16px;
  --form-label-font-weight: 500;
}
```


+++

+++ &#x200B;2. Estilo do contêiner do formulário

Aplique um plano de fundo moderno, raio da borda e sombra ao contêiner de formulário para obter um layout visualmente atraente.


```css
/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}
```




+++

+++ &#x200B;3. Estilo do campo de entrada

Estilize campos de entrada de texto, email e número para obter uma aparência limpa e moderna.


```css
/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}
```


+++

+++ &#x200B;4. Personalização adicional

É possível estender ainda mais o estilo do formulário ao direcionar campos, estados ou componentes específicos, conforme necessário. Consulte as seções anteriores para ver os padrões avançados.

```css
/* Custom brand theme */
:root {
    /* Brand color system */
    --brand-primary: #2563eb;
    --brand-secondary: #64748b;
    --brand-success: #059669;
    --brand-error: #dc2626;
    --brand-background: #f8fafc;
    
    /* Override form variables */
    --background-color-primary: #ffffff;
    --button-primary-color: var(--brand-primary);
    --button-primary-hover-color: #1d4ed8;
    --form-error-color: var(--brand-error);
    --form-background-color: var(--brand-background);
    --label-color: var(--brand-secondary);
    --border-color: #d1d5db;
    
    /* Enhanced spacing */
    --form-input-padding: 1rem;
    --form-field-vert-gap: 1.5rem;
    --form-padding: 2rem;
    
    /* Modern typography */
    --form-font-size-s: 16px;
    --form-label-font-weight: 500;
}

/* Enhanced form container */
.form {
    background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
    border-radius: 12px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
    max-width: 600px;
    margin: 2rem auto;
    overflow: hidden;
}

/* Modern input styling */
.form .text-wrapper input,
.form .email-wrapper input,
.form .number-wrapper input {
    background: white;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    padding: var(--form-input-padding);
    font-size: 16px;
    transition: all 0.2s ease;
    width: 100%;
}

.form .text-wrapper input:focus,
.form .email-wrapper input:focus,
.form .number-wrapper input:focus {
    border-color: var(--brand-primary);
    box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
    transform: translateY(-1px);
}

/* Enhanced button styling */
.form .button-wrapper button[type="submit"] {
    background: linear-gradient(135deg, var(--brand-primary) 0%, #1d4ed8 100%);
    color: white;
    border: none;
    border-radius: 8px;
    padding: 1rem 2rem;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
    width: 100%;
    box-shadow: 0 4px 12px rgba(37, 99, 235, 0.3);
}

.form .button-wrapper button[type="submit"]:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(37, 99, 235, 0.4);
}
```

Essa abordagem abrangente demonstra como as propriedades personalizadas de CSS permitem temas sofisticados, mantendo os recursos de integridade estrutural e acessibilidade do sistema Adaptive Forms Block.

+++

## Solução de problemas de CSS

+++ Problemas de especificidade de CSS

```css
/- ❌ Problem: Styles not applying */
.text-wrapper input {
  color: red;
}

/- ✅ Solution: Match or exceed existing specificity */
.form .text-wrapper input {
  color: red;
}

/- ✅ Alternative: Use higher specificity when needed */
main .form .text-wrapper input {
  color: red;
}
```

+++

+++ Problemas de substituição de variável CSS

```css
/- ❌ Problem: Variables not working */
.form {
  --form-border-color: blue; /- Local scope only */
}

/- ✅ Solution: Define in root scope */
:root {
  --form-border-color: blue; /- Global scope */
}
```

+++

+++ Estilo do estado do formulário

```css
/- Validation states */
.form .field-wrapper.error input {
  border-color: var(--form-error-color);
}

.form .field-wrapper.success input {
  border-color: var(--form-success-color);
}

/- Loading state */
.form[data-submitting="true"] {
  opacity: 0.7;
  pointer-events: none;
}

/- Disabled state */
.form input:disabled {
  background-color: var(--form-input-disabled-background);
  cursor: not-allowed;
}
```

+++

+++ Erros comuns no seletor

```css
/- ❌ Incorrect: Assumes direct nesting */
.form form input {
  /- This might miss inputs in wrappers */
}

/- ✅ Correct: Target actual structure */
.form .text-wrapper input {
  /- Targets actual HTML structure */
}

/- ❌ Avoid: Unnecessary specificity */
main .form form .text-wrapper input {
  /- Too specific, harder to override */
}

/- ✅ Preferred: Balanced specificity */
.form .text-wrapper input {
  /- Easier to maintain and override */
}
```

+++



### **Práticas recomendadas específicas de componente**


+++ Estilo do botão

```css
/- Primary buttons */
.form .button-wrapper button[type="submit"] {
  background-color: var(--form-focus-color);
  color: white;
  border: none;
  padding: var(--form-input-padding);
  border-radius: var(--form-border-radius);
}

/- Secondary buttons */
.form .button-wrapper button[type="reset"] {
  background-color: transparent;
  color: var(--form-text-color);
  border: 1px solid var(--form-border-color);
}
```

+++

+++ Design de formulário responsivo

```css
/- Mobile-first approach */
.form {
  width: 100%;
  padding: 1rem;
}

/- Tablet and up */
@media (min-width: 768px) {
  .form {
    max-width: var(--form-max-width);
    padding: var(--form-padding);
  }
}
```

+++

## Resumo de práticas recomendadas

1. **Usar propriedades personalizadas de CSS**: use variáveis para temas consistentes
2. **Seguir arquitetura baseada em bloco**: usar `.form` como seletor de bloco primário
3. **Evitar Especificidade Excessiva**: não use `main .form form`, a menos que seja necessário
4. **Wrappers de destino**: usar `.{Type}-wrapper` padrões para direcionamento de componentes
5. **Manter Consistência**: Use os mesmos padrões do seletor em todo o projeto
6. **Testar entre Dispositivos**: garantir que os formulários funcionem bem em dispositivos móveis, tablets e desktops
7. **Validar acessibilidade**: certifique-se de que os estilos não interfiram nos leitores de tela ou na navegação pelo teclado


