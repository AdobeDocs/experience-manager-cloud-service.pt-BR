---
title: Personalizar tema e estilo para um Edge Delivery Services para AEM Forms
description: Personalize efetivamente o tema e o estilo do AEM Forms fornecido pela Edge Delivery Services, garantindo uma experiência do usuário coesa e de marca.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: ac780399-34fe-457d-aaf4-b675656c024d
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 0%

---

# Personalizar a aparência dos formulários

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email de seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> com o nome da organização do GitHub e o nome do repositório. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>


O Forms é fundamental para a interação do usuário em sites, permitindo que ele insira dados. Você pode usar as Folhas de estilo em cascata (CSS) para criar estilos de campos de um formulário, aprimorando a apresentação visual de seus formulários e melhorando a experiência do usuário.

O bloco adaptável do Forms produz uma estrutura consistente para todos os campos de formulário. A estrutura consistente facilita o desenvolvimento de Seletores de CSS para selecionar e estilizar campos de formulário com base no tipo de campo e nos nomes de campo.

Este documento descreve a estrutura do HTML para vários componentes de formulário e ajuda a criar um entendimento de como criar Seletores de CSS para vários campos de formulário para estilizar campos de formulário de um Bloco de Forms adaptável.

Até o final do artigo:

* Você constrói uma compreensão da estrutura do arquivo CSS padrão incluído no Bloco Forms adaptável.
* Você constrói uma compreensão da estrutura HTML dos componentes de formulário fornecidos pelo Bloco de Forms adaptável, incluindo componentes gerais e componentes específicos, como menus suspensos, grupos de rádio e grupos de caixas de seleção.
* Você aprende a estilizar campos de formulário com base no tipo de campo e nos nomes de campo usando Seletores de CSS, permitindo um estilo consistente ou exclusivo com base nos requisitos.

## Noções básicas sobre tipos de campos de formulário

Antes de mergulhar no estilo, vamos rever os [tipos de campo](/help/edge/docs/forms/universal-editor/create-custom-component.md#supported-fieldtypes) de formulário comuns compatíveis com o Bloco de Forms adaptável:

* Campos de entrada: incluem entradas de texto, entradas de email, entradas de senha e muito mais.
* Grupos de caixas de seleção: usado para selecionar várias opções.
* Grupos de opções: usados para selecionar apenas uma opção de um grupo.
* Menus suspensos: também conhecido como caixas de seleção, usadas para selecionar uma opção de uma lista.
* Painéis/Contêineres: usado para agrupar elementos de formulário relacionados.

## Princípios básicos de estilo

Entender os [conceitos CSS fundamentais](https://www.w3schools.com/css/css_intro.asp) é fundamental antes de estilizar campos de formulário específicos:

* [Seletores](https://www.w3schools.com/css/css_selectors.asp): os Seletores de CSS permitem direcionar elementos HTML específicos para o estilo. Você pode usar seletores de elemento, seletores de classe ou seletores de ID.
* [Propriedades](https://www.w3schools.com/css/css_syntax.asp): as propriedades CSS definem a aparência visual dos elementos. As propriedades comuns para os campos de formulário de estilo incluem cor, cor de fundo, borda, preenchimento, margem e muito mais.
* [Modelo de caixa](https://www.w3schools.com/css/css_boxmodel.asp): o modelo de caixa CSS descreve a estrutura dos elementos do HTML como uma área de conteúdo cercada por preenchimento, bordas e margens.
* Flexbox/Grade: CSS [Flexbox](https://www.w3schools.com/css/css3_flexbox.asp) e [Layouts de grade](https://www.w3schools.com/css/css_grid.asp) são ferramentas poderosas para criar designs responsivos e flexíveis.


## Criar um estilo de formulário para o bloco adaptável do Forms

O bloco Forms adaptável oferece uma estrutura HTML padronizada, simplificando o processo de seleção e estilo de componentes de formulário:

* **Atualizar estilos padrão**: você pode modificar os estilos padrão de um formulário editando o `/blocks/form/form.css file`. Esse arquivo fornece um estilo abrangente para um formulário, compatível com formulários de assistente de várias etapas. Ela enfatiza o uso de variáveis CSS personalizadas para facilitar a personalização, a manutenção e o estilo uniforme em todos os formulários.

* **Estilo CSS para o Forms**: para garantir que seus estilos sejam aplicados corretamente, envolva o CSS específico do formulário no seletor `main .form form`. Isso garante que seus estilos direcionem somente os elementos de formulário na área de conteúdo principal, evitando conflitos com outras partes do site.
Exemplo:

  ```css
    main .form form input {
        /* Add styles specific to input fields inside the form */
    }
  
    main .form form button {
        /* Add styles specific to buttons inside the form */
    }
  
    main .form form label {
        /* Add styles specific to labels inside the form */
    }
  
## Estrutura dos componentes

O bloco adaptável do Forms oferece uma estrutura consistente do HTML para vários elementos de formulário, garantindo um estilo e gerenciamento mais fáceis. É possível manipular os componentes usando o CSS para fins de estilo.

### Componentes gerais (exceto menus suspensos, grupos de rádio e grupos de caixas de seleção):

Todos os campos de formulário, exceto os menus suspensos, grupos de opções e grupos de caixas de seleção, têm a seguinte estrutura HTML:

+++ Estrutura HTML de componentes gerais

```HTML
  <div class="{Type}-wrapper field-{Name}   field-wrapper" data-required={Required}>
     <label for="{FieldId}" class="field-label">First   Name</label>
     <input type="{Type}" placeholder="{Placeholder}"   maxlength="{Max}" id={FieldId}" name="{Name}"   aria-describedby="{FieldId}-description">
     <div class="field-description" aria-live="polite"  id="{FieldId}-description">
      Hint - First name should be minimum 3 characters  and a maximum of 10 characters.
     </div>
  </div>
```

* Classes: o elemento div tem várias classes para direcionar elementos específicos e estilo. Você precisa das classes `{Type}-wrapper` ou `field-{Name}` para desenvolver um Seletor de CSS para estilizar um campo de formulário:
* {Type}: Identifica o componente por tipo de campo. Por exemplo, texto (invólucro de texto), número (invólucro numérico), data (invólucro de data).
* {Name}: Identifica o componente por nome. O nome do campo pode ter apenas caracteres alfanuméricos, os vários traços consecutivos no nome são substituídos por um único traço `(-)` e os traços inicial e final em um nome de campo são removidos. Por exemplo, nome (field-first-name field-wrapper).
* {FieldId}: é um identificador exclusivo do campo, gerado automaticamente.
* {Required}: é um booleano indicando se o campo é obrigatório.
* Rótulo: o elemento `label` fornece um texto descritivo para o campo e o associa ao elemento de entrada usando o atributo `for`.
* Entrada: o elemento `input` define o tipo de dados a serem inseridos. Por exemplo, texto, número, email.
* Descrição (Opcional): O `div` com classe `field-description` fornece informações ou instruções adicionais para o usuário.

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

+++

+++ Seletor de CSS para Componentes gerais

```CSS
  
  /* Target all input fields within any .{Type}-wrapper  */
  main .form form .{Type}-wrapper  {
    /* Add your styles here */
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
  }
  
  /* Target all input fields within any .{Type}-wrapper  */
  main .form form .{Type}-wrapper input {
    /* Add your styles here */
    border: 1px solid #ccc;
    padding: 8px;
    border-radius: 4px;
  }
  
  /* Target any element with the class field-{Name}  */
  main .form form .field-{Name} {
    /* Add your styles here */
    /* This could be used for styles specific to all elements with   field-{Name} class, not just inputs */
  }
  
```
* `.{Type}-wrapper`: Direciona o elemento `div` externo com base em    o tipo de campo. Por exemplo, `.text-wrapper` é direcionado a todo o texto    campos.
* `.field-{Name}`: Seleciona ainda mais o elemento com base no nome do campo específico. Por exemplo, `.field-first-name` é direcionado ao campo de texto &quot;Nome&quot;. Embora esse seletor possa ser usado para direcionar elementos com a classe field-{Name}, é importante ter cuidado. Nesse caso específico, não seria útil para estilizar campos de entrada, pois direcionaria não apenas a própria entrada, mas também os elementos de rótulo e descrição. É recomendável usar seletores mais específicos como os que você tem para direcionar campos de entrada de texto (entrada .text-wrapper).

**Exemplo de Seletores de CSS para Componentes Gerais**

```CSS
/*Target all text input fields */
main .form form .text-wrapper input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
  color: red;
}

/*Target all fields with name first-name*/
main .form form .field-first-name input {
  border: 1px solid #ccc;
  padding: 8px;
  border-radius: 4px;
}
```

+++

### Componente suspenso

Para menus suspensos, o elemento `select` é usado em vez de um elemento `input`:

+++ Estrutura HTML do componente suspenso

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

+++

+++ Seletores de CSS para o componente suspenso

O CSS a seguir lista alguns exemplos de Seletores de CSS para componentes suspensos.

```CSS
/* Target the outer wrapper */
main .form form .drop-down-wrapper {
  /* Add your styles here */
  display: flex;
  flex-direction: column;
  margin-bottom: 15px;
}

/* Style the label */
main .form form .drop-down-wrapper .field-label {
  margin-bottom: 5px;
  font-weight: bold;
}
```
* Direcionar o Wrapper: o primeiro seletor (`.drop-down-wrapper`) direciona o elemento wrapper externo, garantindo que os estilos se apliquem a todo o componente suspenso.
* Layout Flexbox: O Flexbox organiza o rótulo, a lista suspensa e a descrição verticalmente para um layout limpo.
* Estilo do rótulo: o rótulo se destaca com uma espessura de fonte mais ousada e uma pequena margem.
* Estilo suspenso: o elemento `select` recebe uma borda, um preenchimento e cantos arredondados para obter uma aparência polida.
* Cor do plano de fundo: uma cor de fundo consistente é definida para harmonia visual.
* Personalização de seta: os estilos opcionais ocultam a seta suspensa padrão e criam uma seta personalizada usando um caractere Unicode e o posicionamento.

+++

---

### Grupos de opções

Semelhante aos componentes suspensos, os grupos de rádio têm sua própria estrutura HTML e estrutura CSS:

+++ Estrutura HTML do grupo de rádio

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

+++

+++ Seletores de CSS para grupos de botões de opção

* Direcionamento do conjunto de campos

```CSS
  main .form form .radio-group-wrapper {
    border: 1px solid #ccc;
    padding: 10px;
  }
```
Este seletor segmenta qualquer conjunto de campos com a classe radio-group-wrapper. Isso seria útil para aplicar estilos gerais a todo o grupo de rádio.

* Rótulos do botão de opção de direcionamento

```CSS
main .form form .radio-wrapper label {
    font-weight: normal;
    margin-right: 10px;
  }
```

* Direcionar todos os rótulos de botão de opção em um conjunto de campos específico com base em seu nome

```CSS
main .form form .field-color .radio-wrapper label {
  /* Your styles here */
}
```

+++

### Grupos de caixas de seleção

+++ Estrutura HTML do grupo de caixas de seleção

```HTML
<fieldset class="checkbox-group-wrapper field-{Name} field-wrapper" id="{FieldId}" name="{Name}" data-required="{Required}">
   <legend for="{FieldId}" class="field-label">....</legend>
   <% for each radio in Group %>
   <div class="radio-wrapper field-{Name}">
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

+++

+++ Seletores de CSS para grupos de caixas de seleção

* Direcionamento do invólucro externo: esses seletores segmentam os contêineres mais externos de grupos de opções e caixas de seleção, permitindo aplicar estilos gerais a toda a estrutura do grupo. Isso é útil para definir o espaçamento, alinhamento ou outras propriedades relacionadas ao layout.

```CSS
  
  /* Targets radio group wrappers */
  main .form form .radio-group-wrapper {
    margin-bottom: 20px; /* Adds space between radio groups */  
  }

  /* Targets checkbox group wrappers */
  main .form form .checkbox-group-wrapper {
    margin-bottom: 20px; /* Adds space between checkbox groups */
  }
```

* Rótulos do grupo de direcionamento: esse seletor direciona o elemento `.field-label` aos invólucros do grupo de caixas de seleção e de rádio. Isso permite estilizar os rótulos especificamente para esses grupos, possivelmente fazendo com que eles se destaquem mais.

```CSS
main .form form .radio-group-wrapper legend,
main .form form .checkbox-group-wrapper legend {
  font-weight: bold; /* Makes the group label bold */
}
```

* Direcionamento de entradas e rótulos individuais: esses seletores fornecem controle mais granular sobre botões de opção individuais, caixas de seleção e seus rótulos associados. Você pode usá-los para ajustar o dimensionamento, o espaçamento ou aplicar estilos visuais mais distintos.

```CSS
/* Styling radio buttons */
main .form form .radio-group-wrapper input[type="radio"] {
  margin-right: 5px; /* Adds space between the input and its label */
}

/* Styling radio button labels */
main .form form .radio-group-wrapper label {
  font-size: 15px; /* Changes the label font size */
}

/* Styling checkboxes */
main .form form .checkbox-group-wrapper input[type="checkbox"] {
  margin-right: 5px; /* Adds space between the input and its label */
}

/* Styling checkbox labels */
main .form form .checkbox-group-wrapper label {
  font-size: 15px; /* Changes the label font size */
}
```

* Personalização da aparência de botões de opção e caixas de seleção: essa técnica oculta a entrada padrão e usa pseudoelementos `:before` e `:after` para criar visuais personalizados que alteram a aparência com base no estado &quot;marcado&quot;.

```CSS
/* Hide the default radio button or checkbox */
main .form form .radio-group-wrapper input[type="radio"],
main .form form .checkbox-group-wrapper input[type="checkbox"] {
  opacity: 0;
  position: absolute;
}

/* Create a custom radio button */
main .form form .radio-group-wrapper input[type="radio"] + label::before {
  /* ... styles for custom radio button ... */
}

main .form form .radio-group-wrapper input[type="radio"]:checked + label::before {
  /* ... styles for checked radio button ... */
}

/* Create a custom checkbox */
main .form form .checkbox-group-wrapper input[type="checkbox"] + label::before {
  /* ... styles for custom checkbox ... */
}

main .form form .checkbox-group-wrapper input[type="checkbox"]:checked + label::before {
  /* ... styles for checked checkbox ... */
}
```

+++

### Componentes de painel/contêiner

+++ Estrutura HTML dos componentes do painel/contêiner

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

* O elemento fieldset atua como o contêiner do painel com o invólucro de painel de classe e classes adicionais para estilização com base no nome do painel (logon de campo).
* O elemento da legenda (<legend>) serve como o título do painel com o texto &quot;Informações de logon&quot; e o rótulo de campo da classe. O atributo data-visible=&quot;false&quot; pode ser usado com o JavaScript para controlar a visibilidade do título.
* Dentro do conjunto de campos, vários.Os elementos {Type}-wrapper (.text-wrapper e .password-wrapper, neste caso) representam campos de formulário individuais dentro do painel.
* Cada invólucro contém um rótulo, campo de entrada e descrição, semelhantes aos exemplos anteriores.

+++

+++ Exemplo de seletores CSS para componentes de Painel/Contêiner

1. Direcionamento do painel:

```CSS
  /* Target the entire panel container */
  main .form form .panel-wrapper {
    /* Add your styles here (e.g., border, padding, background color) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
 }
```

* O seletor `.panel-wrapper` estiliza todos os elementos com o invólucro de painel de classe, criando uma aparência consistente para todos os painéis.

1. Direcionamento do título do painel:

```CSS
  /* Target the legend element (panel title) */
  .panel-wrapper legend {
    /* Add your styles here (e.g., font-weight, font-size) */
    font-weight: bold;
    font-size: 16px;
    padding-bottom: 5px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ddd; /* Optional: create a separation line */
  }
```

* O seletor `.panel-wrapper legend` estiliza o elemento de legenda dentro do painel, fazendo com que o título se destaque visualmente.


1. Direcionamento de campos individuais no painel:

```CSS
/* Target all form field wrappers within a panel */
main .form form .panel-wrapper .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```

* O seletor `.panel-wrapper .{Type}-wrapper` é direcionado a todos os invólucros com a classe `.{Type}-wrapper` dentro do painel, permitindo que você estilize o espaçamento entre os campos de formulário.

1. Direcionamento de campos específicos (opcional):

```CSS
  /* Target the username field wrapper */
  main .form form .panel-wrapper .text-wrapper.field-username {
    /* Add your styles here (specific to username field) */
  }

  /* Target the password field wrapper */
  main .form form .panel-wrapper .password-wrapper.field-password {
    /* Add your styles here (specific to password field) */
  }
```

* Esses seletores opcionais permitem direcionar wrappers de campo específicos no painel para um estilo exclusivo, como realçar o campo de nome de usuário.

+++

### Painel repetível

+++ Estrutura HTML de um painel repetível

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

* data-repeat=&quot;true&quot;: este atributo indica que o painel pode ser repetido dinamicamente usando o JavaScript ou uma estrutura.

* IDs e nomes exclusivos: cada elemento no painel tem um ID exclusivo (por exemplo, name-1, email-1) e um atributo de nome com base no índice do painel (por exemplo, name=&quot;contacts[0].name&quot;). Isso permite a coleta de dados adequada quando vários painéis são enviados.

+++

+++ Seletores de CSS para um painel repetível

* Direcionamento de todos os painéis repetíveis:

```CSS
  /* Target all panels with the repeatable attribute */
 main .form form .panel-wrapper[data-repeatable="true"] {
    /* Add your styles here (e.g., border, margin) */
    border: 1px solid #ccc;
    padding: 15px;
    border-radius: 4px;
    margin-bottom: 20px;
  }
```

O seletor estimula todos os painéis que podem ser repetidos, garantindo uma aparência consistente.


* Direcionamento de campos individuais em um painel:

```CSS
/* Target all form field wrappers within a repeatable panel */
main .form form .panel-wrapper[data-repeatable="true"] .{Type}-wrapper {
  /* Add your styles here (e.g., margin) */
  margin-bottom: 10px;
}
```
Este seletor estimula todos os invólucros de campo em um painel repetível, mantendo um espaçamento consistente entre os campos.

* Direcionamento de campos específicos (em um painel):

```CSS
/* Target the name field wrapper within the first panel */
main .form form .panel-wrapper[data-repeatable="true"][data-index="0"] .text-wrapper.field-name {
  /* Add your styles here (specific to first name field) */
}

/* Target all
```

+++

### Anexo de arquivo

+++ Estrutura do HTML para anexo de arquivo

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

* O atributo de classe usa o nome fornecido para o anexo de arquivo (claim_form).
* Os atributos id e name do elemento de entrada correspondem ao nome do anexo de arquivo (claim_form).
* A seção da lista de arquivos está inicialmente vazia. Ele é preenchido dinamicamente com o JavaScript quando os arquivos são carregados.

+++

+++ Seletores de CSS para o componente de Anexo de arquivo

* Direcionar todo o componente de anexo de arquivo:

```CSS
/* Target the entire file attachment component */
main .form form .file-wrapper {
  /* Add your styles here (e.g., border, padding) */
  border: 1px solid #ccc;
  padding: 15px;
  border-radius: 4px;
  margin-bottom: 20px;
}
```

Este seletor estimula todo o componente de anexo do arquivo, incluindo a legenda, a área de arrastar, o campo de entrada e a lista.

* Direcionamento de elementos específicos:

```CSS
/* Target the drag and drop area */
main .form form .file-wrapper .file-drag-area {
  /* Add your styles here (e.g., background color, border) */
  background-color: #f0f0f0;
  border: 1px dashed #ddd;
  padding: 10px;
  text-align: center;
}

/* Target the file input element */
main .form form .file-wrapper input[type="file"] {
  /* Add your styles here (e.g., hide the default input) */
  display: none;
}

/* Target individual file descriptions within the list (populated dynamically) */
main .form form .file-wrapper .files-list .file-description {
  /* Add your styles here (e.g., margin, display) */
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}

/* Target the file name within the description */
main .form form .file-wrapper .files-list .file-description .file-description-name {
  /* Add your styles here (e.g., font-weight) */
  font-weight: bold;
}
```

Esses seletores permitem estilizar várias partes do componente de anexo de arquivo individualmente. É possível ajustar os estilos para corresponder às suas preferências de design.

+++


## Componentes de estilo

Você pode estilizar campos de formulário com base em seu tipo específico (`{Type}-wrapper`) ou nomes individuais (`field-{Name}`). Isso permite um controle mais granular e a personalização da aparência do formulário.

### Estilo com base no tipo de campo

Você pode usar os Seletores de CSS para direcionar tipos de campo específicos e aplicar estilos de forma consistente.

+++ Estrutura do HTML

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

* Cada campo é colocado em um elemento `div` com várias classes:
   * `{Type}-wrapper`: Identifica o tipo de campo. Por exemplo, `form-text-wrapper`, `form-number-wrapper`, `form-email-wrapper`.
   * `field-{Name}`: Identifica o campo pelo seu nome. Por exemplo `form-name`, `form-age`, `form-email`.
   * `field-wrapper`: uma classe genérica para todos os wrappers de campo.
* O atributo `data-required` indica se o campo é obrigatório ou opcional.
* Cada campo tem um rótulo correspondente, elemento de entrada e possíveis elementos adicionais, como espaços reservados e descrições.


+++


+++ Exemplo de seletores CSS

```CSS
/* Target all text input fields */
main .form form .text-wrapper input {
  /* Add your styles here */
}

/* Target all number input fields */
main .form form .number-wrapper input {
  /* Add your styles here */
  letter-spacing: 2px; /* Example for adding letter spacing to all number fields */
}
```

+++

### Estilo com base no nome do campo

Você também pode direcionar campos individuais por nome para aplicar estilos exclusivos.

+++ Estrutura do HTML

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

+++

+++ Exemplo de seletor de CSS

```CSS
main .form form .field-otp input {
   letter-spacing: 2px
}
```

Este CSS destina-se a todos os elementos de entrada localizados em um elemento que tem a classe `field-otp`. A estrutura do HTML do seu formulário segue as convenções do Bloco de Forms adaptável, isso implica que há um container marcado com a classe &quot;field-otp&quot; que contém o campo com o nome &quot;otp&quot;.

+++




## Consulte também:

{{universal-editor-see-also}}
