---
title: Componentes de formulário e propriedades
description: Este documento fornece uma visão geral dos componentes de formulário e suas propriedades disponíveis no Serviço de entrega de borda da AEM Forms.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e8fbe3efae7368c940cc2ed99cc9a352bbafbc22
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 3%

---


# Componentes de formulários

O Serviço de entrega de borda da AEM Forms permite criar formulários amigáveis e interativos usando vários componentes. Esses componentes atendem a diferentes tipos de coleção de dados e podem ser facilmente personalizados para atender às suas necessidades específicas.

O bloco de formulário adaptável gera um [estrutura de HTML uniforme](/help/edge/docs/forms/style-theme-forms.md) para todos os tipos de campo e containers (painéis), garantindo a consistência. Essa estrutura consistente facilita a [estilizar um formulário](/help/edge/docs/forms/style-theme-forms.md).


## Componentes disponíveis

Esta é uma visão geral dos componentes disponíveis:

### Campos de entrada

- Todos os HTML5 válidos [tipos de entrada](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) e [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea). Por exemplo, botão, caixa de seleção, cor, data, data-hora-local, email, arquivo, oculto, imagem, mês, número, senha, rádio, intervalo, redefinição, enviar, tel, texto, hora, url e semana.

### Controles de seleção

- [Grupos de caixas de seleção](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox): Para selecionar várias opções.
- [Grupos de opções](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio): Para selecionar uma única opção de um grupo.
- [Menus suspensos](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select): para exibir um menu de opções. Por exemplo, a caixa suspensa.

### Contêineres

- Painéis/Contêineres: para agrupar elementos de formulário relacionados para obter uma melhor organização. Trata-se de uma combinação das [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) e [legenda](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend).


## Propriedades dos componentes

Cada componente de formulário vem com várias propriedades que permitem controlar seu comportamento e aparência. Estas são as propriedades compatíveis com os componentes do Bloco de formulário adaptável:


| Propriedade | Componentes aplicáveis | Detalhes |
|--------------|------------------------------|----------------------------------------------------------------------|
| Tipo | Todos | Especifica o tipo do componente. Essa propriedade determina o comportamento e a aparência do campo de entrada. Por exemplo, para entradas de texto, o tipo pode ser &quot;texto&quot;, &quot;email&quot; para entradas de email, &quot;senha&quot; para entradas de senha. O bloco de formulário adaptável suporta todos os HTML5 válidos <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types">tipos de entrada</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">selecionar</a>, e <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a> como tipo. |
| Nome | Todos | Identifica o componente para envio de formulário. O atributo name é usado quando os dados de formulário são enviados ao servidor, associando a entrada do usuário a um campo específico. |
| Rótulo | Todos | Fornece informações contextuais aos usuários. O rótulo é o texto exibido ao lado do componente, fornecendo aos usuários orientação sobre quais informações inserir. |
| Valor | Texto, Senha, Email, Número, Intervalo, Data e suas variantes (datetime-local, mês, semana, hora), Caixa de seleção, Rádio, Oculto, Enviar, Botão | Especifica o valor inicial do componente. Para entradas de texto, área de texto e elementos de seleção, este é o texto ou opção padrão exibido. Para componentes de rádio e caixa de seleção, este é o valor/dado enviado quando eles são selecionados. O atributo value é opcional, mas deve ser considerado obrigatório para entradas de rádio e caixa de seleção. |
| Espaço reservado | Texto, Telefone, Email, Senha, Data (e suas variantes como mês, semana, hora, data e hora local), Número, Intervalo | Oferece dicas para a entrada esperada. O atributo de espaço reservado fornece uma breve dica que descreve o valor esperado do campo de entrada. Ele desaparece assim que o usuário começa a digitar. |
| Descrição | Todos | Fornece informações adicionais sobre o componente e serve como texto de ajuda. O campo de descrição permite obter mais explicações sobre a finalidade ou instruções para preencher o componente. Ele auxilia os usuários na compreensão do contexto do campo de entrada. |
| Visível | Todos | Controla a visibilidade inicial. O atributo visible é uma propriedade booleana que determina se o componente está inicialmente visível ou oculto quando o formulário é carregado. Se definido como true, o campo é exibido; caso contrário, ele fica oculto. |
| Obrigatório | Texto, Tel, Email, Senha, Data e suas variantes (data e hora local, mês, semana, hora), Número, Caixa de seleção, Rádio, Arquivo, Selecionar (lista suspensa), Textarea | Indica se o campo deve ser preenchido antes do envio. O atributo obrigatório é uma propriedade booleana usada para especificar se o usuário deve fornecer entrada para o campo antes de enviar o formulário. |
| Mínimo | Data (e suas variantes como mês, semana, hora, data e hora local), Número, Intervalo | Especifica o valor mínimo permitido. O atributo min define o valor mínimo que o usuário pode inserir no campo. Por exemplo, para entradas de número, define o número mais baixo aceitável. |
| Max | Data (e suas variantes como mês, semana, hora, data e hora local), Número, Intervalo | Especifica o valor máximo permitido. O atributo max define o valor máximo que o usuário pode inserir no campo. Por exemplo, para entradas de data, define a data mais alta aceitável. |
| Aceitar | Arquivo | Define os tipos de arquivos permitidos. O atributo accept é uma lista separada por vírgulas de especificadores de tipo de arquivo exclusivo que restringem os tipos de arquivos que os usuários podem selecionar em um campo de entrada de arquivo. |
| Múltiplas | Arquivo | Permite várias seleções. O atributo multiple é uma propriedade booleana usada com campos de entrada de arquivo. Quando definido como verdadeiro, permite que os usuários selecionem mais de um arquivo. |
| Opções | Lista suspensa | Especifica opções para menus suspensos. A propriedade options é uma lista separada por vírgulas de opções para menus suspensos que define as opções selecionáveis exibidas para o usuário. |
| Marcado | Caixa de seleção, Rádio | Determina se o campo é selecionado por padrão. O atributo marcado é uma propriedade booleana usada com entradas de caixa de seleção e rádio. Quando definido como true, indica que o campo é selecionado por padrão quando o formulário é carregado. |
| Fieldset | Todos | Agrupa campos para criar seções visualmente distintas em um formulário. O elemento fieldset agrupa campos relacionados em um formulário, separando-os visualmente para melhorar a organização e a experiência do usuário. </br> Para organizar um conjunto de campos em um conjunto de campos, use o `fieldset` e especifique seu atributo name. No exemplo abaixo, demonstramos como os botões de opção são encapsulados em um único conjunto de campo para melhorar a organização. ![Exemplo de conjunto de campos](/help/edge/assets/fieldset-example.png) |



<!--

## Supported HTML 5 input types in Adaptive Form Block

The Adaptive Form Block supports a range of HTML 5 input types, and it also seamlessly renders forms created with AEM core components.
Here is the table which outlines how core components correspond to their HTML-5 input types in Edge Delivery:
<table>
 <tbody>
  <tr>
   <td><b>Core Components</b> </td>
   <td><b>HTML 5 input type</b> </td>
   <td><b>Details</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">Form Container</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">form </td>
   <td> Create a form to capture user inputs.
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">Text Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> Defines a single-line text input field. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">Number Input</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">number</a></td>
   <td>Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Lets user  enter a number input. You can also add built-in validation to reject non-numerical inputs. Initially, the input field is displayed as a number input. If a user applies a display pattern, it changes to text to allow the author to apply number formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing numbers.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">Date Picker</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">date </a></td>
   <td> Create an input field for entering a date. You have the option to input the date either through a text box, which validates the entry, or through a dedicated date picker interface. Initially, the native date input field is displayed. If a user applies a display pattern, it changes to text to allow the user to apply formatting, since HTML 5 lacks support for display patterns. However, when the user clicks it, it returns to typing a date.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">File Attachment</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">file</a></td>
   <td> Allows user to choose one or more files from the device storage. It supports enhanced file input validations, such as accepted file types, file size restrictions, and minimum/maximum file selection limits. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> Dropdown List</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a></td>
   <td> Allows users to select one or more options from a list of predefined options. The options can be of type String, Number, or Boolean.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">Checkbox Group</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">multiple checkbox</a></td>
   <td> Allow users to select one or more options from a list. Multiple checkboxes are generated with identical names, each corresponding to an item in the enum. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">Radio Button Group</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">multiple radio</a></td>
   <td> Allows a user to select one option from a group of related options. Multiple radio buttons are generated with identical names, each corresponding to an item in the enum.</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">Button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">button</a></td>
   <td>A UI element that allows users to trigger an action when clicked. </td>
  </tr>
  <tr>
   <td><a href =""https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">Panel</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset with legend</a></td>
   <td> Group sections within a form, where a nested *legend* element adds a caption for the form.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html">Wizard</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a></td>
   <td>Groups related sections within a form. It also controls the arrangement, supporting display options for positioning them at the top or at the left side. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">Text</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>A p tag marks a paragraph. In visual content, paragraphs are chunks of text separated by blank lines or an indented first line</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Submit button</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">submit</a></td>
   <td> A UI element that enables users to submit a form to the server upon clicking. If a user adds a submit rule to a button, it functions as the submit button. </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">Reset button</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">reset</a></td>
   <td>A UI element that resets a form upon clicking. If a user adds a reset rule to a button, it functions as the reset button. </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">Email Input</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">email</a></td>
   <td> Allows the user to enter and edit an email address. If the user adds the multiple attributes, a list of email addresses can be added or edited.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">Telephone Input</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">tel</a></td>
   <td>Allows user to enter and edit a telephone number.</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">Header</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> header</a></td>
   <td>It includes introductory content, typically a group of introductory or navigational aids. It is supported outside Form container. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">Footer</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">footer</a></td>
   <td> Contains information such as copyright data or links to related documents. It is supported outside Form container.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html">Accordion<a></td>
   <td><i>Not yet supported in Adaptive Form Block</i></td>
   <td> Allows user to create expandable and collapsible sections in a form. </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html">Horizontal tabs</a></td>
   <td><i>Not yet supported in Adaptive Form Block</i></td>
   <td>Organizes multiple sections of a form into separate tabs which are displayed horizontally.</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">Image</a></td>
   <td><i>Not yet supported in Adaptive Form Block</i></td>
   <td> Allows user to include images in a form.</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">Title</a></td>
   <td><i>Not yet supported in Adaptive Form Block</i></td>
   <td> Refers to the text that appears at the top of the form. </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">Switch</td>
   <td><i>Not yet supported in Adaptive Form Block</i></td>
   <td> A two-state toggle that allows user to select between two states such as enabling or disabling a feature, setting, or functionality.</td>
  </tr>
 </tbody>
</table>