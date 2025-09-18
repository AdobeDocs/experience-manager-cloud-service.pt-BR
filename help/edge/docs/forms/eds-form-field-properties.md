---
title: Dominar propriedades de campo de bloco do Forms adaptável
description: Crie formulários poderosos mais rápido usando planilhas e propriedades adaptáveis do campo de bloco do Forms! Este guia lista todas as propriedades compatíveis com o Bloco de Forms do EDS.
feature: Edge Delivery Services
source-git-commit: ccc6439f68d8199154d4cd664b9cdb6428460a64
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 3%

---


# Propriedades adaptáveis do campo de bloco do Forms

Este documento resume como o esquema JSON mapeia para o HTML renderizado em `blocks/form/form.js`, com foco em como os campos são identificados e renderizados, padrões comuns e diferenças específicas de campo.

## Como Os Campos (`fieldType`) São Identificados?

Cada campo no esquema JSON tem uma propriedade `fieldType` que determina como ele é renderizado. O `fieldType` pode ser:

- **Um tipo especial**\
  Exemplos: `drop-down`, `radio-group`, `checkbox-group`, `panel`, `plain-text`, `image`, `heading`, etc.
- **Um tipo de entrada HTML válido**\
  Exemplos: `text`, `number`, `email`, `date`, `password`, `tel`, `range`, `file`, etc.
- **Um tipo com um sufixo `-input`**\
  Exemplos: `text-input`, `number-input`, etc. (normalizado para o tipo base como `text`, `number`).

Se o `fieldType` corresponder a um tipo especial, será usado um **renderizador personalizado**. Caso contrário, será tratado como um **tipo de entrada padrão**.

Consulte as seções abaixo para obter a [estrutura completa do HTML e as propriedades](#common-html-structure) para cada tipo de campo.

## Propriedades comuns usadas por campos

Abaixo estão as propriedades usadas pela maioria dos campos:

- `id`: especifica a ID do elemento e oferece suporte à acessibilidade.
- `name`: Define o atributo `name` para elementos de entrada, seleção ou conjunto de campos.
- `label.value`, `label.richText`, `label.visible`: especifica o texto do rótulo/legenda, o conteúdo do HTML e a visibilidade.
- `value`: representa o valor atual do campo.
- `required`: Adiciona o atributo `required` ou os dados de validação.
- `readOnly`, `enabled`: Controla se o campo é editável ou está desabilitado.
- `description`: Exibe o texto de ajuda abaixo do campo.
- `tooltip`: define o atributo `title` para entradas.
- `constraintMessages`: Fornece mensagens de erro personalizadas como atributos de dados.

## Estrutura comum do HTML

A maioria dos campos é renderizada em um invólucro que inclui um rótulo e um texto de ajuda opcional. O trecho a seguir demonstra a estrutura:

```html
<div class="<fieldType>-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<!-- Field-specific input/element here -->
<div class="field-description" id="<id>-description">Description or error
message</div>
</div>
```

Para grupos (opção/caixa de seleção) e painéis, um `<fieldset>` com um `<legend>` é usado em vez de um `<div>/<label>`. O texto de ajuda <div> está presente somente se description estiver definida.

## Exibição de mensagem de erro

Mensagens de erro são exibidas no mesmo elemento `.field-description` usado para texto de ajuda, que é atualizado dinamicamente.

**Quando um campo é inválido**:

- O invólucro (por exemplo, `.field-wrapper`) é atribuído à classe `.field-invalid`.
- O conteúdo `.field-description` é substituído pela mensagem de erro correspondente.

**Quando o campo se tornar válido**:

- A classe `.field-invalid` foi removida.
- O `.field-description` é restaurado ao texto de ajuda original (se disponível) ou removido, se nenhum existir.

As mensagens de erro personalizadas podem ser definidas usando a propriedade `constraintMessages` no JSON.\
Eles são adicionados como `data-<constraint>ErrorMessage` atributos no invólucro (por exemplo, `data-requiredErrorMessage`).

## Tipos de Entrada Padrão (HTML Input ou `*-input`)

Se `fieldType` não for um tipo especial, será tratado como um tipo de entrada padrão do HTML ou como `<type>-input`, por exemplo, `text`, `number`, `email`, `date`, `text-input`, `number-input`.

- O sufixo `-input` é removido, e o tipo base é usado como o atributo `type` da entrada.
- Esses tipos são manipulados por padrão em `renderField()`.
Os tipos de entrada padrão comuns são `text`, `number`, `email`, `date`, `password`, `tel`, `range`, `file`, etc.  Eles também aceitam `text-input`, `number-input`, etc., que são normalizados para o tipo base.

## Restrições para tipos de entrada padrão

Restrições são adicionadas como atributos no elemento de entrada com base nas propriedades JSON.

| Propriedade JSON | Atributo do HTML | Aplica-se a |
|--------------|---------------|------------|
| maxLength | maxlength | texto, email, senha, tel |
| minLength | minlength | texto, email, senha, tel |
| padrão | padrão | texto, email, senha, tel |
| máximo | máx | número, intervalo, data |
| mínimo | min. | número, intervalo, data |
| etapa | etapa | número, intervalo, data |
| Aceitar | Aceitar | arquivo |
| múltiplo | múltiplo | arquivo |
| maxOccur | data-max | painel |
| minOccur | data-min | painel |

>[!NOTE]
>
> `multiple` é uma propriedade booleana. Se true, o atributo `multiple` será adicionado.

Esses atributos são definidos automaticamente pelo renderizador de formulário com base na definição JSON do campo.

## Exemplo: estrutura do HTML com restrições

O exemplo a seguir demonstra como um campo numérico é renderizado com restrições de validação e atributos de manipulação de erros.

```html
<div class="number-wrapper field-wrapper field-age" data-id="age"
data-required="true"
data-minimumErrorMessage="Too small" data-maximumErrorMessage="Too large">
<label for="age" class="field-label">Age</label>
<input type="number"
id="age" name="age"
value="30" required min="18"
max="99" step="1"
placeholder="Enter your age" />
<div class="field-description" id="age-description"> Description or error message
</div>
</div>
```

Cada parte da estrutura do HTML desempenha um papel na vinculação de dados, validação e exibição de mensagens de ajuda ou erro.

## Propriedades específicas do campo e suas estruturas do HTML

### Suspenso

**Propriedades Extras:**

- `enum` / `enumNames`: Defina os valores de opção e seus rótulos de exibição para o menu suspenso.
- `type`: Habilita seleção múltipla se definida como `array`.
- `placeholder`: adiciona uma opção de espaço reservado desabilitada para orientar os usuários antes da seleção.

Exemplo:

```html
<div class="drop-down-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="This field is required">
<label for="<id>" class="field-label">Label</label>
<select id="<id>" name="<name>" required title="Tooltip" multiple>
<option disabled selected value="">Placeholder</option>
<option value="opt1">Option 1</option>
<option value="opt2">Option 2</option>
</select>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Texto sem formatação

**Propriedades Extras**:

- `richText`: Se verdadeiro, renderiza o HTML no parágrafo.

Exemplo:

```html
<div class="plain-text-wrapper field-wrapper field-<name>" data-id="<id>">
<label for="<id>" class="field-label">Label</label>
<p>Text or <a href="..." target="_blank">link</a></p>
</div>
```

### Caixa de seleção

**Propriedades Extras**:

- `enum`: Define os valores dos estados marcado e desmarcado da caixa de seleção.
- `properties.variant / properties.alignment`: Especifica o estilo visual e o alinhamento das caixas de seleção de estilo de opção.

Exemplo:

```html
<div class="checkbox-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true"
data-requiredErrorMessage="Please check this box">
<label for="<id>" class="field-label">Label</label>
<input type="checkbox"
id="<id>"
name="<name>" value="on"
required
data-unchecked-value="off" />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Botão

**Propriedades Extras**:

- `buttonType`: especifica o comportamento do botão definindo seu tipo (botão, envio ou redefinição).

Exemplo:

```html
<div class="button-wrapper field-wrapper field-<name>" data-id="<id>">
<button id="<id>" name="<name>" type="submit" class="button"> Label
</button>
</div>
```

### Entrada multilinha

**Propriedades Extras**:

- `minLength`: especifica o número mínimo de caracteres permitidos em uma entrada de área de texto ou texto.
- `maxLength`: especifica o número máximo de caracteres permitidos em uma entrada de área de texto ou texto.
- `pattern`: define uma expressão regular que o valor de entrada deve corresponder para ser considerado válido.
- `placeholder`: exibe o texto do espaço reservado dentro da entrada ou área de texto até que um valor seja inserido.

Exemplo:

```html
<div class="multiline-wrapper field-wrapper field-<name>" data-id="<id>"
data-minLengthErrorMessage="Too short" data-maxLengthErrorMessage="Too long">
<label for="<id>" class="field-label">Label</label>
<textarea id="<id>"
name="<name>" required
minlength="2"
maxlength="100"
pattern="[A-Za-z]+"
placeholder="Type here..."></textarea>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Painel

**Propriedades Extras**:

- `repeatable`: especifica se o painel pode ser repetido dinamicamente.
- `minOccur`: Define o número mínimo de instâncias do painel necessárias.   maxOccur: Define o número máximo de instâncias de painel permitidas.
- `properties.variant`: Define o estilo visual ou a variante do painel.
- `properties.colspan`: Especifica quantas colunas o painel abrange em um layout de grade.
- `index`: indica a posição do painel em seu contêiner pai.
- `fieldset`: campos relacionados a grupos sob um elemento `<fieldset>` com legenda ou rótulo.

Exemplo:

```html
<fieldset class="panel-wrapper field-wrapper field-<name>" data-id="<id>"
name="<name>"
data-repeatable="true" data-index="0">
<legend class="field-label">Label</legend>
<!-- Nested fields here -->
<button type="button" class="add">Add</button>
<button type="button" class="remove">Remove</button>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### Opções

**Propriedades Extras**:

- `enum`: Define o conjunto de valores permitidos para o campo de opção, usado como o atributo de valor para cada opção de botão de opção.

Exemplo:

```html
<div class="radio-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<label for="<id>" class="field-label">Label</label>
<input type="radio" id="<id>" name="<name>" value="opt1" required />
<div class="field-description" id="<id>-description"> Description or error message
</div>
</div>
```

### Grupo radial

**Propriedades Extras**:

- `enum`: Define a lista de valores de opção para o grupo de opções, usado como o valor de cada botão de opção.
- `enumNames`: Fornece rótulos de exibição para os botões de opção, correspondendo à ordem de enumeração.

Exemplo:

```html
<fieldset class="radio-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true">
<legend class="field-label">Label</legend>
<div>
<input type="radio" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="radio" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### **Grupo de caixas de seleção**

**Propriedades Extras**:

- `enum`: define a lista de valores de opção para o grupo de caixas de seleção, usado como o valor de cada caixa de seleção.
- `enumNames`: Fornece rótulos de exibição para as caixas de seleção, correspondendo à ordem de enumeração.
- `minItems`: Define o número mínimo de caixas de seleção que devem ser marcadas para validade.
- `maxItems`: Define o número máximo de caixas de seleção que podem ser selecionadas antes de um erro ser disparado.

Exemplo:

```html
<fieldset class="checkbox-group-wrapper field-wrapper field-<name>" data-id="<id>"
data-required="true" data-minItems="1"
data-maxItems="3">
<legend class="field-label">Label</legend>
<div>
<input type="checkbox" id="<id>-0" name="<name>" value="opt1" required />
<label for="<id>-0">Option 1</label>
</div>
<div>
<input type="checkbox" id="<id>-1" name="<name>" value="opt2" />
<label for="<id>-1">Option 2</label>
</div>
<div class="field-description" id="<id>-description"> Description or error message
</div>
</fieldset>
```

### Imagem

**Propriedades Extras**:

- `value / properties['fd:repoPath']`: Define o caminho de origem da imagem ou o caminho do repositório para renderizar a imagem.
- `altText`: Fornece texto alternativo para a imagem (atributo alt) para melhorar a acessibilidade.

Exemplo:

```html
<div class="image-wrapper field-wrapper field-<name>" data-id="<id>">
<picture>
<img src="..." alt="..." />
<!-- Optimized sources -->
</picture>
</div>
```

### Cabeçalho

**Propriedades Extras**:

- `value`: especifica o conteúdo do texto a ser exibido dentro do elemento de cabeçalho (por exemplo, `<h2>`).

Exemplo:

```html
<div class="heading-wrapper field-wrapper field-<name>" data-id="<id>">
<h2 id="<id>">Heading Text</h2>
</div>
```

Para obter mais detalhes, consulte a implementação em `blocks/form/form.js` e `blocks/form/util.js`.


<!--Each form field is represented as a dedicated row in the spreadsheet, analogous to fields in a database table. The column headers act as labels for the various properties supported by the form field block.

Think of your form as a table in a spreadsheet, where each line represents a different question or piece of information you want to collect. The table headings tell you what kind of answers you can expect for each section.

The below table lists all the properties that are supported by the Adaptive Forms Block.

**Master Your Forms with These Adaptive Forms Block Field Properties:**

This table details all the properties you can use to customize your Adaptive Forms Block fields:

| Property | Description | Example |
|---|---|---|
| **Type** | [HTML input type](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) (text, email, number, etc.), [textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea), [select](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select), [fieldset](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset) | `text`, `email`, `radio`, `select` |
| **Name** | This defines the unique identifier for submitted data (e.g., 'email' for an email address field).  Choose a clear and unique name for each field, as the name serves as internal field identifier used for data mapping during submission. | `user_name`, `email_address` |
| **Label** | User-friendly field label | `"Full Name"`, `"Choose your country"` |
| **Value** | Default value displayed | `"John Doe"`, `"United States"` |
| **Placeholder** | Hint text within the field | `"Enter your email address"` |
| **Description** | Help text for users | `"Please enter a valid email address"` |
| **Visible** | Show/hide the field initially | `true`, `false` |
| **Mandatory** | Require a value from the user | `true`, `false` |
| **Min/Max** | Set minimum/maximum values (number, date, text length) | `18` (age), `2025-12-31` (date) |
| **Accept** | Allowed file types for file upload | `"image/jpeg,image/png"` |
| **Multiple** | Allow multiple file selections | `true`, `false` |
| **Options** | Comma-separated list for dropdown menus | `"Option 1, Option 2, Option 3"` |
| **Checked** | Default-selected radio button/checkbox | `true`, `false` |
| **Fieldset** | Group fields together | Fieldset name (e.g., `"Personal Information"`) |-->

