---
title: Usar regras para adicionar comportamento dinâmico a um formulário
description: O Edge Delivery Services for AEM Forms foi criado para oferecer desempenho máximo, permitindo que você visualize o futuro da coleta de dados simplificada e do engajamento do usuário. Use regras para adicionar comportamento dinâmico aos formulários.
feature: Edge Delivery Services
exl-id: 58042016-e655-446f-a2bf-83f1811525e3
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 0%

---

# Usar regras para adicionar comportamento dinâmico aos formulários

Um dos recursos avançados de criação de formulários usando uma planilha é a capacidade de usar funções de planilha integradas para criar regras, permitindo exibir ou ocultar condicionalmente campos de formulário, automatizar cálculos com base na entrada do usuário e criar uma experiência do usuário mais dinâmica.

Este artigo mostra como usar várias propriedades de Bloco de Formulário Adaptável, principalmente as propriedades [`Visible`](#visible-property), [`Visibility Expression`](#visible-expression-property) e [`Value Expression`](#value-expression-property), juntamente com as [funções de planilha](#spreadsheet-functions-for-rules), para criar regras eficazes para seus formulários. Também exploraremos alguns exemplos para ilustrar como essas regras podem ser implementadas na prática.

## Compreender os construtores de uma regra

Regras são como instruções que nos dizem o que fazer em diferentes situações. Uma regra geralmente tem as seguintes construções:

- Condições : especificam as circunstâncias em que a regra se aplica. Pense neles como uma pergunta que precisa ser respondida (sim ou não).

- Ações: definem o que acontece quando a condição é atendida (true) ou não é atendida (false).


Por exemplo, para exibir uma caixa de email, quando uma caixa de seleção estiver marcada:

- Condição: a mensagem &quot;Você gosta de se inscrever para Revista e Atividades?&quot; está marcada. (Sim ou não?). Essa condição é definida na propriedade `Visible` do formulário.
- Ação (True): a caixa de email é exibida. (O que acontece se a resposta for sim). O `Visibility Expression` usa a condição definida para a propriedade `visible` para mostrar campos dinamicamente.
- Ação (False): a caixa de email está oculta. (O que acontece se não houver). O `Visibility Expression` usa a condição definida para o `Value` para ocultar campos dinamicamente.

Para obter instruções detalhadas passo a passo, consulte o [campo mostrar/ocultar email com base em uma condição](#example-1-conditional-email-field)


## Noções básicas sobre valor, visível, expressão de visibilidade e propriedades de expressão de valor

### Propriedade visível

Imagine um interruptor para o seu campo de formulário. A propriedade `Visible` é como essa opção, controlando se o campo está inicialmente visível no formulário quando carregado pela primeira vez.

- True (como a opção de luz &quot;ligada&quot;): o campo é mostrado no formulário.
- False (como o botão luminoso estar &quot;desligado&quot;): o campo fica oculto no formulário.

Você pode usar a Fórmula de Planilha (incluindo a tag = ) para escrever uma fórmula usando uma lógica semelhante a uma planilha para determinar a visibilidade do campo. Você pode usar os valores de outros campos no formulário dentro desta fórmula. Por exemplo, se um usuário selecionar &quot;Individual&quot; em um campo de tipo de registro, você poderá ocultar o campo de email usando uma fórmula que verifica esse valor.

### Propriedade de expressão visível (mostrar/ocultar um campo)

A propriedade `Visible Expression` permite usar a regra adicionada à propriedade `Visible` para decidir se o campo deve ser exibido ou ocultado com base nas interações do usuário.

Use o `=FORMULATEXT("Address of the corresponding Visible property)` para trazer a fórmula mencionada na Propriedade `Visible` como uma cadeia de caracteres para o campo de propriedade `Visible Expression`. Isso é necessário para mostrar/ocultar campos dinamicamente em um formulário publicado.

![Textodefórmula](/help/edge/assets/aem-forms-formulatext.png)

### Propriedade do valor (definir os dados iniciais)

Imagine um valor predefinido em um interruptor regulador para a luz da sala. A propriedade `Value` é semelhante, determinando o estado inicial dos dados que um usuário vê no campo.  Ele define ou recupera os dados atuais exibidos no campo de formulário.

Quando o formulário é carregado pela primeira vez, a propriedade `Value` determina o que o usuário vê no campo antes de fazer qualquer alteração. Ao contrário das propriedades `Visible` e `Visible Expression` que controlam a visibilidade, a propriedade Value afeta diretamente os dados em si. Os usuários podem modificar esse valor digitando, selecionando opções (menus suspensos) ou interagindo com o campo.

Você pode usar Fórmula do Excel (incluindo a tag = ) para escrever uma fórmula usando uma lógica semelhante a uma planilha para determinar o valor mostrado no campo. Você pode usar os valores de outros campos no formulário dentro desta fórmula. Por exemplo, você pode calcular um desconto automaticamente com base no valor do pedido inserido em outro campo.


### Propriedade de Expressão de Valor (Calcular Valores a serem exibidos em um campo)

Essa propriedade permite controlar o valor exibido em um campo com base em uma fórmula, semelhante à Expressão visível. Imagine uma calculadora feita em campo.

Use o `=FORMULATEXT("Address of the corresponding Value property)` para trazer a fórmula mencionada na Propriedade `Value` como uma cadeia de caracteres para o campo de propriedade `Value Expression`. Isso é necessário para calcular dinamicamente e mostrar valores calculados em um formulário publicado.

![Textodefórmula](/help/edge/assets/aem-forms-formulatext-value.png)

Veja uma analogia para solidificar esses conceitos:

- Visível: Imagine uma forma como uma casa. A propriedade &quot;Visible&quot; é como o botão de luz de cada sala (campo). Você decide se a sala está inicialmente iluminada (visível) ou escura (oculta) quando alguém entra na casa (abre o formulário).
- Expressão visível: é como um interruptor de luz do sensor de movimento. A sala (campo) pode estar inicialmente escura (oculta), mas uma fórmula (sensor de movimento) pode ligá-la (mostrar o campo) se alguém passar (altera o valor em outro campo).
- Valor: é como um interruptor de regulador predefinido para a luz (dados iniciais no campo). Os usuários podem ajustar o brilho (modificar o valor).
- Expressão de valor: é como uma calculadora sofisticada criada na etiqueta de preço de um produto na casa (formulário). A etiqueta de preço (campo) mostra o preço final com base em uma fórmula (por exemplo, adicionar imposto ao preço base) que usa outras informações como o preço base (valor de outro campo).

Ao combinar essas propriedades com as [funções da planilha](#spreadsheet-functions-for-rules), é possível obter uma grande variedade de comportamentos dinâmicos em seus formulários.

## Funções de Planilha para Regras

O bloco adaptável do Forms suporta uma variedade de funções de planilha que podem ser usadas para criar regras. Estas são as funções que estão disponíveis prontas para uso (OOTB):

### Funções lógicas

- [NOT()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018452_715980110): reverte o estado lógico (TRUE torna-se FALSE e vice-versa).
- [AND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#AND): retorna TRUE somente se todas as condições especificadas forem TRUE.
- [OR()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#OR): retornará TRUE se pelo menos uma das condições especificadas for TRUE.

### Funções condicionais

- [IF()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018446_715980110): avalia uma condição e retorna um valor específico se TRUE, e outro valor se FALSE.

### Funções matemáticas

- [SUM()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#SUM): adiciona valores de um intervalo de células especificado.
- [ROUND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#ROUND): arredonda um número para um número especificado de casas decimais.
- [MIN()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#MIN): retorna o menor valor de um intervalo de células especificado.

## Criação de uma regra

Vamos nos aprofundar em alguns exemplos práticos para ilustrar como as regras podem ser usadas para aprimorar seus formulários:

## Exemplo 1: campo de email condicional

Este exemplo mostra como a caixa de seleção atua como uma condição. Quando está selecionada (a condição é verdadeira), a caixa de email aparece (ação para verdadeira). Se não for selecionada (a condição é false), a caixa de email permanecerá oculta (ação para false).

Crie um formulário com uma caixa de seleção e uma caixa de email, conforme exibido na imagem abaixo:

![Formulário de email condicional](/help/edge/assets/aem-forms-conditional-email-form.png)


Veja a seguir como usar uma regra para mostrar o campo de email na seleção de uma caixa de seleção:

1. Defina a propriedade `Value` do campo de caixa de seleção como `TRUE`.
1. Defina a propriedade `Checked` do campo de caixa de seleção como `FALSE`. Isso garante que a caixa de seleção não esteja selecionada, por padrão.
1. Defina a propriedade `Visible` do campo de email como `=[address of Checked property of the checkbox field] = true()`. Por exemplo, `=Q11=TRUE()`. A fórmula é avaliada se a caixa de seleção estiver marcada ou não. Se a caixa de seleção estiver marcada, a fórmula será avaliada como TRUE. Se a caixa de seleção não estiver marcada, a fórmula será avaliada como FALSE.



   A função `TRUE()` retorna o valor lógico quando você o define para apontar para a propriedade `Checked`, se `checked = false` ela retorna falso. Se `checked=true`, retorna `true`. Isso garante que o campo de email fique oculto, por padrão.


1. Defina a propriedade `Visible Expression` do campo de caixa de seleção como `=FORMULATEXT ((address of Visible property of the checkbox field))`. Por exemplo, `=FORMULATEXT((G12))`. A função FORMULATEXT () pega uma fórmula como entrada e retorna a fórmula em si como um texto. Ajuda a usar a fórmula no formulário.

   ![Campo de email condicional](/help/edge/assets/aem-forms-visible-expression-formula-text.png)

1. Visualize e publique seu formulário. Agora, ao marcar a caixa de seleção, o campo de email é revelado e, ao desmarcá-lo, o campo fica oculto, o que fornece uma experiência do usuário dinâmica.

   ![Email Condicional](/help/edge/assets/aem-forms-coditional-email.gif)


## Exemplo 2: Cálculo automático

Este exemplo mostra como um formulário calcula automaticamente o Custo Estimado do Percurso na seleção de datas de percurso em um formulário.

Crie um formulário com um campo de data, orçamento de sala, campos Custo estimado da viagem conforme exibido abaixo e uma caixa de email, conforme exibido na imagem abaixo:

![Formulário de email condicional](/help/edge/assets/aem-forms-automatic-calculations-form.png)

Veja como usar um cálculo automático para mostrar o Custo Estimado do Percurso:

1. Defina a propriedade `Value` do campo `amount` como `=F6*DAYS(F3,F2)`. Esta fórmula calcula o número de dias de `Start Date` e `End Date`, multiplica o número de dias com orçamento de sala e exibe o resultado no campo `Estimated Trip Cost`.

1. Defina a propriedade `Value Expression` do campo `Estimated Trip Cost` como `=FORMULATEXT ((address of value property of the amount field))`. Por exemplo, `=FORMULATEXT(F7)`. A função FORMULATEXT () pega uma fórmula como entrada e retorna a fórmula em si como um texto. Ajuda a usar a fórmula no formulário.

1. Visualize e publique seu formulário. Agora, sobre a especificação de um `Start Date`, `End Date` e Orçamento de Sala. O `Estimated Trip Cost` é calculado automaticamente.

## Exemplos de funções da planilha


Estes são alguns exemplos das funções de planilha comumente usadas:

**Funções lógicas:**

- **NOT():** Reverte o estado lógico (TRUE torna-se FALSE e vice-versa).

  Exemplo: ocultar um campo &quot;Confirmar email&quot; se o campo de email ficar em branco.

   1. Defina a propriedade `Visible` do campo &quot;Confirmar email&quot; como `=NOT(if('address of email field'=""))`.

      ![Campo para ocultar e confirmar email do AEM Forms](/help/edge/assets/aem-forms-not-function-hide-email-field.png)


   1. Defina a expressão visível do campo &quot;Confirmar email&quot; para `=FORMULATEXT ((address of visible property of the Confirm Email field))`

      ![Fórmula de expressão visível do AEM Forms](/help/edge/assets/aem-forms-visible-expression-formula-text.png)


- AND(): retorna TRUE somente se todas as condições especificadas forem TRUE.

   - Exemplo: habilitar um botão &quot;enviar&quot; somente se todos os campos obrigatórios estiverem preenchidos.

   1. Defina a propriedade `Visible` do botão &quot;enviar&quot; como:



      ```JavaScript
      =AND(NOT(address of `value` property of the `name` field = ""), NOT(address of `value` property of the `email` field = ""), NOT(address of `value` property of the `phone` field))
      ```

      Por exemplo,

      ```JavaScript
      =AND(NOT(F9=""), NOT(F12=""), NOT(F10=""))
      ```

   1. Defina a expressão visível do campo &quot;Confirmar email&quot; para

      ```JavaScript
      =FORMULATEXT ((address of visible property of the Confirm Email field))
      ```

      Por exemplo,

      ```JavaScript
      =FORMULATEXT(G14)
      ```

      Esta fórmula mostra o botão &quot;enviar&quot; (TRUE) somente se todos os campos (nome, email, telefone) estiverem preenchidos (NOT()) retorna TRUE para cada um), caso contrário, ele oculta o botão (AND(multiple FALSES) = FALSE).

- OR(): retorna TRUE se pelo menos uma das condições especificadas for TRUE.

   - Exemplo: Aplicar um desconto se um usuário inserir qualquer um dos códigos de cupom de desconto aplicáveis.

   1. Defina a propriedade `Visible` do campo &quot;valor final&quot; como:


  ```JavaScript
     =IF(OR(F14="BlackFridaySale", F14="NewYearDiscount"), (F6*DAYS(F3,F2)* 0.7) , (F6*DAYS(F3,F2)))
  ```

   1. Defina a expressão de valor do campo &quot;Confirmar email&quot; para

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      Por exemplo,

      ```JavaScript
      =FORMULATEXT(F7)
      ```

      Essa fórmula calcula um desconto de 30% se o usuário inserir um código de cupom (couponCode = &quot;NewYearDiscount&quot;) OU (couponCode = &quot;BlackFridaySale&quot;), caso contrário, definirá o desconto como 0.

**Funções de texto:**

- IF(): Avalia uma condição e retorna um valor específico se TRUE, e outro valor se FALSE.

   - Exemplo: exibição de uma mensagem personalizada com base em uma categoria de produto escolhida.

   1. Defina a propriedade `Value` do campo `message` como `Only upto 7 kg check-in lagguage is allowed!`:

   1. Defina a propriedade `Visible` do campo `message` como:


      ```JavaScript
      =if(address of value property of chosen product category ="Economy", TRUE(), FALSE())
      ```

      Por exemplo,

      ```JavaScript
      =if(F5="Economy", TRUE(), FALSE())
      ```

   1. Defina a expressão de valor do campo `message` como

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      Por exemplo,

      ```JavaScript
      =FORMULATEXT(G15)
      ```

      Esta fórmula exibe a mensagem &quot;Apenas até 7 kg bagagem check-in é permitido!&quot; se a classe escolhida for &quot;Economia&quot;, caso contrário, deixará o campo de mensagem em branco.

**Funções matemáticas:**

- SUM(): Adiciona valores de um intervalo de células especificado.

  Exemplo: cálculo do custo total de itens em um carrinho de compras.

  Na expressão de valor do campo &quot;custo total&quot;:
SUM(preço * quantidade)

  Essa fórmula supõe que você tenha campos separados para &quot;preço&quot; e &quot;quantidade&quot; de cada item. Ele os multiplica e usa SUM() para somar o custo total de todos os itens no carrinho.

- ROUND(): Arredonda um número para um número especificado de casas decimais.

  Exemplo: Arredondamento de um valor de desconto calculado para duas casas decimais.

  Na expressão de valor do campo &quot;valor de desconto&quot; (supondo que um desconto seja calculado em outro lugar):
ROUND(desconto, 2)

  Esta fórmula arredonda o valor do desconto para duas casas decimais.

- MIN(): Retorna o menor valor de um intervalo de células especificado.

  Exemplo: localização da idade mínima necessária para um formulário de inscrição com base em um país selecionado.

  Na expressão de valor de um campo &quot;idade mínima&quot;:
MIN(ageLimits[&quot;EUA&quot;], ageLimits[&quot;Reino Unido&quot;], ageLimits[&quot;França&quot;])

  Essa fórmula pressupõe que você tenha uma tabela chamada &quot;ageLimits&quot; que armazena requisitos de idade mínima para países diferentes. Ele usa MIN() para encontrar o menor valor entre eles.


Além disso, o bloco Adaptive Forms permite que você assuma o controle total dos seus formulários ao criar [funções personalizadas](#creating-custom-functions). As funções personalizadas permitem definir suas próprias regras e lógicas, fornecendo controle total sobre como os formulários se comportam.


## Criação e implantação de Funções personalizadas

O bloco OOTB (pronto para uso) do Adaptive Forms fornece implementações para muitas [funções comuns de planilha](#spreadsheet-functions-for-rules). No entanto, para obter um controle mais granular sobre seus formulários, é possível usar qualquer uma das funções OOTB disponíveis no Microsoft® Excel ou no Google Sheets dentro dos blocos do Adaptive Forms. O bloco adaptável do Forms não contém implementação para todas as funções OOTB disponíveis no Microsoft® Excel ou no Google Sheets. Se você precisar de qualquer uma dessas funções, é possível desenvolver uma função personalizada com sintaxe semelhante para obter a funcionalidade fornecida pelo Microsoft® Excel ou pelo Google Sheets. Por exemplo, você pode implementar a [função Year() do Microsoft® Excel](https://support.microsoft.com/en-us/office/calculate-age-113d599f-5fea-448f-a4c3-268927911b37#) para calcular a idade a partir da data de nascimento.


### Criar uma função personalizada

As funções personalizadas residem no arquivo `[Adaptive form block]/functions.js`. O processo de criação geralmente envolve as seguintes etapas:

- Declaração de função: defina o nome da função e seus parâmetros (as entradas que ela aceita).
- Implementação lógica: escreva o código que descreve os cálculos ou manipulações específicos executados pela função.
- Exportação de função: torne a função acessível em suas regras, exportando-a do arquivo relevante.

### Exemplo: Função Ano

Este exemplo demonstra duas funções personalizadas que imitam a função YEAR() do Microsoft® Excel para calcular a idade:


```JavaScript
/**
 - Get the current date and time
 - @name now
 - @returns {Date} The current date and time as a Date object
 */
function now() {
  const today = new Date();
  return today;
}

/**
 - Get the year from a Date object
 - @name year
 - @param {Date} date The date object
 - @throws {TypeError} If the input is not a Date object
 - @returns {number} The year as a number
 */
function year(date) {
  let inputDate = new Date(date)

  if (!(inputDate instanceof Date)) {
    throw new TypeError("Input must be a Date object");
  }

  const year = inputDate.getFullYear();

  return year;
}

// Make the function accessible for use in rules
export { now, year };
```

### Use uma função personalizada em seu formulário

Para usar a função personalizada no formulário:

1. **Adicionar a Função**: inclua sua função personalizada no arquivo `[Adaptive form block]/functions.js`. Lembre-se de adicioná-lo à instrução de exportação no arquivo.
1. **Implantar o arquivo**: implante o arquivo `functions.js` atualizado em seu projeto GitHub e verifique se a compilação foi bem-sucedida.
1. **Uso da Função**: acesse a função na planilha do formulário usando as propriedades `Value`, `Value Expression`, `Visible` ou `Visible Expression`, semelhantes a qualquer outra função de planilha com suporte para OOTB.
1. **Visualizar o Formulário**: use o AEM Sidekick para visualizar seu formulário com a função recém-implementada.

