---
title: Personalizar tema e estilo para um formulário do Serviço de entrega do AEM Forms Edge
description: Personalizar tema e estilo para um formulário do Serviço de entrega do AEM Forms Edge
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 0%

---


# Campos do formulário de estilo

O Forms é fundamental para a interação do usuário em sites, permitindo que ele insira dados. Este guia aborda os fundamentos do estilo de vários campos de formulário dentro do [Bloco de formulário adaptável](/help/edge/docs/forms/create-forms.md), ajudando você a criar formulários visualmente atraentes e fáceis de usar.

## Noções básicas sobre tipos de campos de formulário

Antes de mergulhar no estilo, vamos rever os tipos de campos de formulário comuns compatíveis com o bloco Formulário adaptável:

* Campos de entrada: incluem entradas de texto, entradas de email, entradas de senha e muito mais.
* Grupos de caixas de seleção: usado para selecionar várias opções.
* Grupos de opções: usados para selecionar apenas uma opção de um grupo.
* Menus suspensos: também conhecido como caixas de seleção, usadas para selecionar uma opção de uma lista.
* Painéis/Contêineres: usado para agrupar elementos de formulário relacionados.

## Princípios básicos de estilo

A compreensão de conceitos CSS fundamentais é crucial antes de estilizar campos de formulário específicos:

* Seletores: os seletores de CSS permitem direcionar elementos de HTML específicos para o estilo. Você pode usar seletores de elemento, seletores de classe ou seletores de ID.
* Propriedades: as propriedades CSS definem a aparência visual dos elementos. As propriedades comuns para os campos de formulário de estilo incluem cor, cor de fundo, borda, preenchimento, margem e muito mais.
* Modelo de caixa: o modelo de caixa CSS descreve a estrutura dos elementos HTML como uma área de conteúdo cercada por preenchimento, bordas e margens.
* Flexbox/Grade: os layouts Flexbox e Grade CSS são ferramentas eficientes para criar designs responsivos e flexíveis.

## Criar um estilo de formulário para o bloco de formulário adaptável

O Bloco de formulário oferece uma estrutura de HTML padronizada, simplificando o processo de seleção e estilo de componentes de formulário:

* **Atualizar estilos padrão**: é possível modificar os estilos padrão de um formulário editando o `/blocks/form/form.css file`. Esse arquivo fornece um estilo abrangente para um formulário, compatível com formulários de assistente de várias etapas. Ela enfatiza o uso de variáveis CSS personalizadas para facilitar a personalização, a manutenção e o estilo uniforme em todos os formulários. Para obter instruções sobre como adicionar o bloco de formulário ao seu projeto, consulte [criar um formulário](/help/edge/docs/forms/create-forms.md).

* **Personalização**: usar o padrão `forms.css` como base e personalizá-lo para modificar a aparência dos componentes de formulário, tornando-o visualmente atraente e fácil de usar. A estrutura do arquivo incentiva a organização e mantém estilos para formulários, promovendo designs consistentes em todo o site.

## Detalhamento da estrutura do forms.css

* **Variáveis globais:** Definido no `:root` , essas variáveis (`--variable-name`) armazenam valores usados em toda a folha de estilos para garantir consistência e facilidade de atualizações. Essas variáveis definem cores, tamanhos de fonte, preenchimento e outras propriedades. Você pode declarar suas próprias variáveis globais ou modificar as existentes para alterar o estilo do formulário.

* **Estilos do seletor universal:** A variável `*` o seletor corresponde a cada elemento no formulário, garantindo que os estilos sejam aplicados a todos os componentes por padrão, incluindo a configuração do `box-sizing` propriedade para `border-box`.

* **Estilo do formulário:** Esta seção foca no estilo de componentes de formulário usando seletores para direcionar elementos de HTML específicos. Ele define estilos para campos de entrada, áreas de texto, caixas de seleção, botões de opção, entradas de arquivo, rótulos de formulário e descrições.

* **Estilo do assistente (se aplicável):** Esta seção é dedicada ao estilo do layout do assistente, um formulário de várias etapas, onde cada etapa é exibida uma de cada vez. Ele define estilos para o contêiner do assistente, conjuntos de campos, legendas, botões de navegação e layouts responsivos.

* **Consultas de mídia:** Eles fornecem estilos para diferentes tamanhos de tela, ajustando o layout e o estilo de acordo.

* **Estilos diversos:**: esta seção aborda estilos para mensagens de sucesso ou erro, áreas de upload de arquivos e outros elementos que você pode encontrar em um formulário.


## Estrutura de componentes

O Bloco de formulário oferece uma estrutura de HTML consistente para vários elementos de formulário, garantindo um estilo e gerenciamento mais fáceis. É possível manipular os componentes usando o CSS para fins de estilo.

### Componentes gerais (exceto menus suspensos, grupos de rádio e grupos de caixas de seleção):

Todos os campos de formulário, exceto os detalhamentos, grupos de rádio e grupos de caixas de seleção, têm a seguinte estrutura de HTML:

#### Estrutura de HTML

```HTML
<div class="form-{Type}-wrapper form-{Name} field-wrapper" data-required={Required}>
  <label for="{FieldId}" class="field-label">Field Label</label>
  <input type="{Type}" placeholder="{Placeholder}" maxlength="{Max}" id="{FieldId}" name="{Name}" aria-describedby="{FieldId}-description">
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Description of the field.
  </div>
</div>
```

* Classes: o elemento div tem várias classes para direcionar elementos específicos e estilo. Você exige o `form-{Type}-wrapper` ou `form-{Name}` classes para desenvolver um seletor de CSS para estilizar um campo de formulário:
   * {Type}: identifica o componente por tipo de campo. Por exemplo, texto (form-text-wrapper), número (form-number-wrapper), data (form-date-wrapper).
   * {Name}: identifica o componente por nome. O nome do campo pode ter apenas caracteres alfanuméricos, os vários traços consecutivos no nome são substituídos por um único traço `(-)`, e os traços inicial e final em um nome de campo são removidos. Por exemplo, nome (form-first-name field-wrapper).
   * {FieldId}: é o identificador exclusivo do campo, gerado automaticamente.
   * {Required}: é um booleano que indica se o campo é obrigatório.
* Label: a variável `label` element fornece um texto descritivo para o campo e o associa ao elemento de entrada usando o `for` atributo.
* Entrada: O `input` define o tipo de dados a serem inseridos. Por exemplo, texto, número, email.
* Descrição (Opcional): A variável `div` com classe `field-description` O fornece informações ou instruções adicionais para o usuário.

**Exemplo de estrutura de HTML**

```HTML
<div class="form-text-wrapper form-first-name field-wrapper" data-required="true">
  <label for="firstName" class="field-label">First Name</label>
  <input type="text" placeholder="Enter your first name" maxlength="50" id="firstName" name="firstName" aria-describedby="firstName-description">
  <div class="field-description" aria-live="polite" id="firstName-description">
    Please enter your legal first name.
  </div>
</div>
```

**Seletor de CSS para Componentes gerais**

```CSS
.form-{Type}-wrapper input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}


.form-{Name} input {
  /* Add your styles here */
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

* `.form-{Type}-wrapper`: segmenta o exterior `div` elemento com base no tipo de campo. Por exemplo, `.form-text-wrapper` direciona todos os campos de entrada de texto.
* `.form-{Name}`: seleciona ainda mais o elemento com base no nome do campo específico. Por exemplo, `.form-first-name` direciona o campo de texto &quot;Nome&quot;.

**Exemplo de seletores CSS para Componentes gerais**

```CSS
/*Target all text input fields */

.form-text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}

/*Target all fields with name first-name*/

.form-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```


### Componente suspenso

Para menus suspensos, a variável `select` elemento é usado em vez de um `input` elemento:


#### Estrutura de HTML

```HTML
<div class="form-drop-down-wrapper form-{Name} field-wrapper" data-required={required}>
  <label for="{FieldId}" class="field-label">First Name</label>
  <select id="{FieldId}" name="{Name}"><option></option><option></option></select>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - First name should be minimum 3 characters and a maximum of 10 characters.
  </div>
</div>
```

**Exemplo de estrutura HTML**

```HTML
    <div class="form-drop-down-wrapper form-country field-wrapper" data-required="true">
      <label for="country" class="field-label">Country</label>
      <select id="country" name="country">
         <option value="">Select Country</option>
         <option value="US">United States</option>
         <option value="CA">Canada</option>
    </select>
   <div class="field-description" aria-live="polite" id="country-description">Please select your country of residence.</div>
   </div>
```

#### Exemplo de seletores CSS para o componente suspenso

```CSS
/* Target the outer wrapper */
.form-drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
.form-drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}

/* Style the dropdown itself */
.form-drop-down-wrapper select {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  background-color: white; /* Ensure a consistent background */
  /* Adjust arrow appearance as needed */
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

/* Optional: Style the dropdown arrow */
.form-drop-down-wrapper select::-ms-expand {
  display: none; /* Hide the default arrow for IE11 */
}

.form-drop-down-wrapper select::after {
  content: "\25BC";
  font-size: 12px;
  color: #ccc;
  /* Adjust positioning as needed */
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
}
```

* Direcionar o Wrapper: o primeiro seletor (`.form-drop-down-wrapper`) direciona o elemento invólucro externo, garantindo que os estilos sejam aplicados a todo o componente suspenso.
* Layout Flexbox: O Flexbox organiza o rótulo, a lista suspensa e a descrição verticalmente para um layout limpo.
* Estilo do rótulo: o rótulo se destaca com uma espessura de fonte mais ousada e uma pequena margem.
* Estilo suspenso: o elemento selecionado recebe uma borda, um preenchimento e cantos arredondados para obter uma aparência polida.
* Cor do plano de fundo: uma cor de fundo consistente é definida para harmonia visual.
* Personalização de seta: os estilos opcionais ocultam a seta suspensa padrão e criam uma seta personalizada usando um caractere Unicode e o posicionamento.

### Grupos de opções e caixas de seleção

Semelhante aos componentes suspensos, os grupos de rádio e de caixa de seleção têm sua própria estrutura de HTML e considerações de CSS:

#### Estrutura de HTML do grupo de rádio

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```


#### Estrutura de HTML do grupo de caixas de seleção

```HTML
<div class="form-checkbox-group-wrapper form-{Name} field-wrapper" data-required={required}>
  <label class="field-label">{Label Text}</label>
  <div class="checkbox-group">
    <input type="checkbox" id="{FieldId}-1" name="{Name}" value="{Value1}">
    <label for="{FieldId}-1">{Option 1 Text}</label>
    <input type="checkbox" id="{FieldId}-2" name="{Name}" value="{Value2}">
    <label for="{FieldId}-2">{Option 2 Text}</label>
    </div>
  <div class="field-description" aria-live="polite" id="{FieldId}-description">
    Hint - Select multiple options (if applicable).
  </div>
</div>
```

**Exemplo de seletores CSS para grupos de opções e caixas de seleção**

* Direcionamento do Outer Wrapper: esses seletores direcionam os contêineres mais externos dos grupos de rádio e de caixa de seleção, permitindo aplicar estilos gerais a toda a estrutura do grupo. Isso é útil para definir o espaçamento, alinhamento ou outras propriedades relacionadas ao layout.


  ```CSS
     /* Targets all radio group wrappers */
  .form-radio-group-wrapper {
    margin-bottom: 20px; /* Adds space between radio groups */
  }
  
  /* Targets all checkbox group wrappers */
  .form-checkbox-group-wrapper {
    margin-bottom: 20px; /* Adds space between checkbox groups */
  }
  ```


* Rótulos dos grupos de direcionamento: esse seletor direciona os `.field-label` elemento em invólucros de grupos de caixas de seleção e de rádio. Isso permite estilizar os rótulos especificamente para esses grupos, possivelmente fazendo com que eles se destaquem mais.

  ```CSS
  .form-radio-group-wrapper .field-label,
  .form-checkbox-group-wrapper .field-label {
   font-weight: bold; /* Makes the group label bold */
  }
  ```



* Direcionamento de entradas e rótulos individuais: esses seletores fornecem controle mais granular sobre botões de opção individuais, caixas de seleção e seus rótulos associados. Você pode usá-los para ajustar o dimensionamento, o espaçamento ou aplicar estilos visuais mais distintos.

  ```CSS
  /* Styling radio buttons */
  .form-radio-group-wrapper input[type="radio"] {
    margin-right: 5px; /* Adds space between the input and its   label */
  } 
  
  /* Styling radio button labels */
  .form-radio-group-wrapper label {
    font-size: 15px; /* Changes the label font size */
  }
  
  /* Styling checkboxes */
  .form-checkbox-group-wrapper input[type="checkbox"] {
    margin-right: 5px;  /* Adds space between the input and its  label */ 
  }
  
  /* Styling checkbox labels */
  .form-checkbox-group-wrapper label {
    font-size: 15px; /* Changes the label font size */
  }
  ```




* Personalização da aparência de botões de opção e caixas de seleção: essa técnica oculta a entrada padrão e usa os pseudoelementos :before e :after para criar visuais personalizados que alteram a aparência com base no estado &quot;marcado&quot;.

  ```CSS
  /* Hide the default radio button or checkbox */
  .form-radio-group-wrapper input[type="radio"],
  .form-checkbox-group-wrapper input[type="checkbox"] {
    opacity: 0; 
    position: absolute; 
  }
  
  /* Create a custom radio button */
  .form-radio-group-wrapper input[type="radio"] + label::before { 
    content: "";
    display: inline-block;
    width: 16px; 
    height: 16px; 
    border: 2px solid #ccc; 
    border-radius: 50%;
    margin-right: 5px;
  }
  
  .form-radio-group-wrapper input[type="radio"]:checked +  label::before {
    background-color: #007bff; 
  }
  
  /* Create a custom checkbox */
  /* Similar styling as above, with adjustments for a square shape  */
  ```


## Componentes de estilo

Também é possível estilizar campos de formulário com base no tipo específico ou em nomes individuais. Isso permite um controle mais granular e a personalização da aparência do formulário.

### Estilo com base no tipo de campo

Você pode usar seletores de CSS para direcionar tipos de campo específicos e aplicar estilos de forma consistente.

**Exemplo de estrutura HTML**

```HTML
<div class="form-text-wrapper form-name field-wrapper" data-required="true">
  <label for="name" class="field-label">Name</label>
  <input type="text" placeholder="Enter your name" maxlength="50" id="name" name="name">
</div>

<div class="form-number-wrapper form-age field-wrapper" data-required="true">
  <label for="age" class="field-label">Age</label>
  <input type="number" placeholder="Enter your age" id="age" name="age">
</div>

<div class="form-email-wrapper form-email field-wrapper" data-required="true">
  <label for="email" class="field-label">Email Address</label>
  <input type="email" placeholder="Enter your email" id="email" name="email">
</div>
```

* Cada campo é envolvido em um `div` elemento com várias classes:
   * `form-{Type}-wrapper`: identifica o tipo de campo. Por exemplo, `form-text-wrapper`, `form-number-wrapper`, `form-email-wrapper`.
   * `form-{Name}`: identifica o campo pelo seu nome. Por exemplo `form-name`, `form-age`, `form-email`.
   * `field-wrapper`: uma classe genérica para todos os invólucros de campo.
* A variável `data-required` atributo indica se o campo é obrigatório ou opcional.
* Cada campo tem um rótulo correspondente, elemento de entrada e possíveis elementos adicionais, como espaços reservados e descrições.

**Exemplo de seletores CSS**

```CSS
/* Target all text input fields */
.form-text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
.form-number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

### Estilo com base no nome do campo

Você também pode direcionar campos individuais por nome para aplicar estilos exclusivos.

**Exemplo de estrutura HTML**

```HTML
<div class="form-number-wrapper form-otp field-wrapper" data-required="true">
  <label for="otp" class="field-label">OTP</label>
  <input type="number" placeholder="Enter your OTP" maxlength="6" id="otp" name="otp">
</div>
```

**Exemplo de seletor de CSS**

```CSS
.form-otp input {
   letter-spacing: 2px
}
```

Este CSS segmenta todos os elementos de entrada localizados em um elemento que tem a classe `form-otp`. A estrutura de HTML do seu formulário segue as convenções do Bloco de formulário, isso implica que há um container marcado com a classe &quot;form-otp&quot; que mantém o campo com o nome &quot;otp&quot;.


