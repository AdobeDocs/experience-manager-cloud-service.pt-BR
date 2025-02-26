---
title: Como usar o editor de regras para aplicar regras a campos de formulário, permitindo um comportamento dinâmico e uma lógica complexa para formulários criados com a criação do WYSIWYG?
description: O editor de regras no Universal Editor permite adicionar comportamento dinâmico e criar lógica complexa em formulários sem codificação ou script.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '2214'
ht-degree: 1%

---


# Introdução ao Editor de regras na Criação do WYSIWYG

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email de seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> com o nome da organização do GitHub e o nome do repositório. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>


É possível adicionar um comportamento de formulário dinâmico usando o Editor de regras, que permite criar regras. Essas regras permitem visibilidade condicional de campo, automatizam cálculos com base na entrada do usuário e melhoram a experiência geral do usuário. Ao simplificar o processo de preenchimento de formulário, o Editor de regras ajuda a garantir precisão e eficiência.

O Editor de regras oferece uma interface visual intuitiva para criar e gerenciar regras. Sua abordagem amigável torna-o acessível a todos os usuários, mesmo aqueles sem extensa experiência técnica, permitindo-lhes implementar a lógica sem esforço dentro de suas formas.

## Noções básicas sobre uma regra

As regras são instruções que orientam os usuários sobre quais ações executar em condições específicas.

* **Condição**: uma condição é uma verificação ou regra que avalia se algo é verdadeiro ou falso. Ela responde à pergunta: &quot;Isso atende aos requisitos?&quot;

* **Ação**: uma ação é o que acontece quando a condição é verdadeira. É a tarefa ou o comportamento acionado com base na avaliação da condição.

Uma regra normalmente segue uma das seguintes construções:

* **Condition-Action**: verifique uma condição primeiro e, em seguida, execute uma ação. No editor de regras, o tipo de regra `When` impõe a construção `condition-action`.
* **Condição-ação**: execute uma ação primeiro e, em seguida, verifique uma condição. Os tipos de regra `Set Value Of` e `Validate` no editor de regras impõem a construção `action-condition`.
* **Ação-Condição-Alternativa**: Execute uma ação, verifique uma condição e execute a ação principal ou uma ação alternativa com base na condição. Por exemplo, por padrão, a ação alternativa para `Show` é `Hide`, e para `Enable` é `Disable`.

Por exemplo, uma condição pode verificar se um usuário inseriu um determinado valor em um campo e a ação pode ser mostrar ou ocultar um campo.
* **Condição**: verifique se a renda é superior a US$ 50.000.
* **Ação**: se a condição for verdadeira, mostrar o campo `Additional Deduction`; caso contrário, executar a ação alternativa: ocultar o campo `Additional Deduction`.

Para obter instruções detalhadas passo a passo, consulte [adicionar uma regra condicional](#2-add-a-conditional-rule).

## Como ativar a extensão do Editor de regras?

No Editor universal, a extensão Editor de regras não é ativada por padrão. Para habilitar a gravação da extensão do Editor de Regras em [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) da sua ID de email oficial.

Depois que a extensão Editor de regras for habilitada para o seu ambiente, o ícone ![editar-regras](/help/forms/assets/edit-rules-icon.svg) aparecerá no canto superior direito do editor.

![Editor de regras do Universal Editor](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

Selecione o componente de formulário para o qual deseja gravar uma regra e clique no ícone ![editar-regras](/help/forms/assets/edit-rules-icon.svg). A interface do usuário do Editor de regras é exibida.

![Interface do usuário do Editor de Regras](/help/edge/docs/forms/assets/rule-editor-for-field.png)

Neste artigo, `form object` e `form component` são usados alternadamente.

Agora, você pode começar a escrever regras ou lógica de negócios para o campo de formulário selecionado usando os [tipos de regras disponíveis no Editor de regras](#available-rule-types-in-rule-editor).

## Noções básicas sobre a interface do usuário do Editor de regras

O editor do Editor de regras é aberto quando você clica no ícone ![edit-rules](/help/forms/assets/edit-rules-icon.svg):

![Interface do usuário do Editor de Regras](/help/edge/docs/forms/assets/rule-editor-interface.png)

<table border="1">
  <thead>
    <tr>
      <th>Componente do Editor de regras</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1. Título</td>
      <td>Exibe o título do componente de formulário e o tipo de regra selecionado. Por exemplo, 'Inserir Salário Bruto' é um componente da caixa de texto para o qual o tipo de regra 'Quando' está selecionado. </td>
    </tr>
    <tr>
      <td>2. Funções e objetos de formulário</td>
      <td>A guia <b>Objetos Forms</b> mostra uma exibição hierárquica de todos os componentes contidos no formulário. A guia <b>Funções</b> inclui um conjunto de funções integradas no editor de regras.</td>
    </tr>
    <tr>
      <td>3. Alternância entre objetos de formulário e funções</td>
      <td>O botão de alternância alternadamente mostra ou oculta o painel de funções e objetos de formulário. </td>
    </tr>
    <tr>
      <td>4. Editor de regras visuais</td>
      <td>O Editor visual de regras é a interface em que você pode criar regras para os componentes de formulário.</td>
    </tr>
    <tr>
      <td>5. Botões Concluído e Cancelar</td>
      <td>O botão <b>Concluído</b> é usado para salvar uma regra. O botão <b>Cancelar</b> descarta todas as alterações feitas em uma regra e fecha o Editor de Regras.</td>
    </tr>
  </tbody>
</table>

Todas as regras existentes em um componente de formulário são listadas ao selecionar o componente. É possível exibir o título e uma pré-visualização do resumo da regra no Editor de regras. Além disso, você pode alterar a ordem das regras, editar regras, habilitar/desabilitar regras ou excluir regras.

![mostrar as regras disponíveis do objeto de formulário](/help/edge/docs/forms/assets/rule-editor15.png)

## Tipos de regras disponíveis

O Editor de regras fornece um conjunto de tipos de regras predefinidos que você pode usar para escrever regras, conforme exibido na tabela abaixo:

<table border="1">
  <thead>
    <tr>
      <th>Tipo de regra</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Definir valor de</td>
      <td>Define o valor de um componente de formulário dependendo se a condição especificada é atendida ou não.</td>
    </tr>
    <tr>
      <td>Limpar Valor de</td>
      <td>Limpa o valor do componente de formulário especificado.</td>
    </tr>
    <tr>
      <td>Ocultar/Mostrar</td>
      <td>Oculta ou mostra um componente de formulário com base no fato de uma condição ser atendida ou não.</td>
    </tr>
    <tr>
      <td>Habilitar/desabilitar</td>
      <td>Ativa ou desativa um componente de formulário com base no fato de uma condição ser atendida ou não.</td>
    </tr>
    <tr>
      <td>Validar</td>
      <td>Verifica o componente de formulário com base em uma condição e exibe um erro se a condição não for atendida. </td>
    </tr>
    <tr>
      <td>Quando</td>
      <td>Especifica uma condição para avaliação seguida por uma ação para acionar se a condição for atendida. Ela segue a construção da regra de ação <i>condition-action-alternate</i> ou a construção da regra <i>condition-action</i>. </td>
    </tr>
    <tr>
      <td>Formato</td>
      <td> Modifica o valor de exibição do componente de formulário usando a expressão fornecida quando seu valor é alterado.</td>
    </tr>
    <tr>
      <td>Executar serviço</td>
      <td>Chama um serviço configurado usando APIs externas, Modelo de dados de formulário ou serviços Web RESTful.</td>
    </tr>
    <tr>
      <td>Definir Propriedade</td>
      <td>Define o valor de uma propriedade do componente de formulário especificado com base em uma condição.</td>
    </tr>
    <tr>
      <td>Definir Foco</td>
      <td>Define o foco no componente de formulário especificado.</td>
    </tr>
    <tr>
      <td>Salvar Formulário</td>
      <td>Ele permite que o usuário salve o formulário como rascunho usando o componente Rascunhos e envios do Forms Portal. </td>
    </tr>
    <tr>
      <td>Enviar Formulário</td>
      <td>Envia o formulário.</td>
    </tr>
    <tr>
      <td>Restaurar Formulário</td>
      <td>Redefine o formulário.</td>
    </tr>
    <tr>
      <td>Adicionar/Remover Instância</td>
      <td>Adiciona ou remove uma ocorrência da linha de tabela ou painel repetível especificada.</td>
    </tr>
    <tr>
      <td>Navegar para</td>
      <td>Navega até outro Forms adaptável, outros ativos, como imagens ou fragmentos de documentos, ou um URL externo.</td>
    </tr>
    <tr>
      <td>Evento de envio</td>
      <td>Aciona ações específicas com base em condições ou eventos predefinidos.</td>
    </tr>
    <tr>
      <td>Navegar entre os painéis</td>
      <td>Permite alterar o foco entre diferentes painéis em um formulário.</td>
    </tr>
  </tbody>
</table>


Agora, vamos explorar como [gravar regras no Editor de regras](#write-rules).

## Regras de gravação

Para entender como escrever regras no Editor de regras visuais, considere um exemplo simples de um formulário de cálculo de imposto:

![Exemplo do Editor de Regras](/help/edge/docs/forms/assets/rule-editor-1.png)

No formulário descrito acima, o usuário informa o salário bruto. Com base nessa entrada, o campo condicional é exibido e o imposto a pagar é calculado.

**Campos de formulário:**
* Salário Bruto (entrada do usuário)
* Dedução Adicional (campo condicional)
* Receita Tributável (campo calculado)
* Imposto a Pagar (campo calculado)

**Regra condicional:**
* Condição: Salário Bruto > 50.000
* Ação: Mostrar o campo Dedução Adicional

**Regras de Cálculo:**

* Receita Tributável = Salário Bruto - Dedução Adicional (se aplicável)
* Imposto a Pagar = Receita Tributável * Alíquota de Imposto (para simplificar, suponha uma alíquota fixa de 10%)

Para gravar regras, execute as seguintes etapas:

### 1. Criar um formulário

Para criar um formulário no Universal Editor:

1. Abra um formulário no Universal Editor para edição.
1. Adicione os seguintes componentes de formulário:
   * Formulário de Cálculo de Imposto (Título)
   * Salário Bruto (Entrada de Número)
   * Dedução Adicional (Entrada de Número)
   * Receita Tributável (Entrada de Número)
   * Imposto a Pagar (Entrada de Número)
   * Enviar (Botão Enviar)
1. Oculte o campo de formulário `Additional Deduction` abrindo seu `Properties`.

   ![Exemplo do Editor de Regras](/help/edge/docs/forms/assets/rule-editor2.png)

### 2. Adicionar uma regra condicional para um campo de formulário

Depois de criar o formulário, escreva a primeira regra para mostrar o campo `Additional Deduction` somente se o salário bruto exceder $50.000. Para adicionar uma regra condicional:

1. Abra um formulário no Editor Universal para edição e selecione o campo **[!UICONTROL Salário Bruto]** na árvore de conteúdo e selecione ![edit-rules](/help/forms/assets/edit-rules-icon.svg). Como alternativa, você pode selecionar o campo **[!UICONTROL Salário Bruto]** diretamente do painel **[!UICONTROL Objeto do Forms]**.
   ![Exemplo do Editor de Regras1](/help/edge/docs/forms/assets/rule-editor3.png)
A interface visual do Editor de regras é exibida.
1. Clique em **[!UICONTROL Criar]** para criar regras.
   ![Exemplo do Editor de Regras2](/help/edge/docs/forms/assets/rule-editor4.png)
Por padrão, o tipo de regra `Set Value Of` está selecionado. Embora não seja possível alterar ou modificar o objeto selecionado, você poderá usar o menu suspenso de regras para selecionar outro tipo de regra.\
   ![Exemplo do Editor de Regras3](/help/edge/docs/forms/assets/rule-editor5.png)
1. Abra a lista suspensa tipo de regra e selecione o tipo de regra **[!UICONTROL Quando]**.
   ![Exemplo do Editor de Regras4](/help/edge/docs/forms/assets/rule-editor6.png)
1. Selecione o menu suspenso **[!UICONTROL Selecionar Estado]** e selecione **[!UICONTROL é maior que]**. O campo **[!UICONTROL Inserir um Número]** é exibido.
   ![Exemplo do Editor de Regras5](/help/edge/docs/forms/assets/rule-editor7.png)
1. Insira `50000` no campo **[!UICONTROL Insira um Número]** na regra.
   ![Exemplo do Editor de Regras6](/help/edge/docs/forms/assets/rule-editor8.png)
Você definiu a condição como `When Gross Salary is greater than 50000`. Em seguida, defina a ação a ser executada se esta condição for `True`.
1. Na instrução `Then`, selecione **[!UICONTROL Mostrar]** no menu suspenso **[!UICONTROL Selecionar Ação]**.
   ![Exemplo do Editor de Regras7](/help/edge/docs/forms/assets/rule-editor9.png)
1. Arraste e solte o campo **[!UICONTROL Dedução Adicional]** da guia Objetos de Formulário no campo **[!UICONTROL Soltar objeto ou selecionar aqui]**. Como alternativa, selecione o campo **[!UICONTROL Soltar objeto ou selecione aqui]** e selecione o campo **[!UICONTROL Dedução Adicional]** no menu pop-up, que lista todos os objetos de formulário no formulário.
   ![Exemplo do Editor de Regras8](/help/edge/docs/forms/assets/rule-editor10.png)
1. Clique em **[!UICONTROL Adicionar Seção Mais]** para adicionar outra condição ao campo **[!UICONTROL Salário Bruto]**, caso insira um salário menor que `50000`.
   ![Exemplo do Editor de Regras9](/help/edge/docs/forms/assets/rule-editor11.png)
1. Selecione **[!UICONTROL Ocultar]** no menu suspenso **[!UICONTROL Selecionar Ação]** na instrução `Else`.
   ![Exemplo do Editor de Regras10](/help/edge/docs/forms/assets/rule-editor12.png)
1. Arraste e solte o campo **[!UICONTROL Dedução Adicional]** da guia Objetos de Formulário no campo **[!UICONTROL Soltar objeto ou selecionar aqui]**. Como alternativa, selecione o campo **[!UICONTROL Soltar objeto ou selecione aqui]** e selecione o campo **[!UICONTROL Dedução Adicional]** no menu pop-up, que lista todos os objetos de formulário no formulário.
   ![Exemplo do Editor de Regras11](/help/edge/docs/forms/assets/rule-editor13.png)
1. Selecione **[!UICONTROL Concluído]** para salvar a regra.
A regra é exibida da seguinte maneira no Editor de regras:
   ![Exemplo do Editor de Regras12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> Como alternativa, você pode escrever uma regra Mostrar no campo Dedução Adicional, em vez de uma regra Quando no campo Salário Bruto, para implementar o mesmo comportamento.

### 3. Adicionar regras de cálculo para os campos de formulário

Em seguida, escreva uma regra para calcular o `Taxable Income`, que é a diferença entre `Gross Salary` e `Additional Deduction` (se aplicável). Para adicionar uma regra de cálculo ao campo **[!UICONTROL Receita Tributável]**, execute as seguintes etapas:

1. No modo de criação, selecione o campo **[!UICONTROL Receita Tributável]** e selecione o ícone ![edit-rules](/help/forms/assets/edit-rules-icon.svg). Como alternativa, você pode selecionar o campo **[!UICONTROL Receita Tributável]** diretamente do painel **[!UICONTROL Objeto Forms]**.
1. Em seguida, selecione **[!UICONTROL Criar]** para criar a regra.
   ![Exemplo do Editor de Regras13](/help/edge/docs/forms/assets/rule-editor16.png)
1. Selecione **[!UICONTROL Selecionar Opção]** e selecione **[!UICONTROL Expressão Matemática]**. Um campo para escrever expressão matemática é aberto.
   ![Exemplo do Editor de Regras14](/help/edge/docs/forms/assets/rule-editor17.png)

1. No campo de expressão matemática:

   * Selecione ou arraste e solte da guia Objeto do Forms o campo **[!UICONTROL Salário Bruto]** no primeiro objeto **[!UICONTROL Soltar ou selecione aqui]**.

   * Selecione **[!UICONTROL Menos]** no campo **[!UICONTROL Selecionar Operador]**.

   * Selecione ou arraste e solte da guia Objeto do Forms o campo **[!UICONTROL Dedução Adicional]** no outro objeto **[!UICONTROL Soltar ou selecione aqui]**.
     ![Exemplo do Editor de Regras15](/help/edge/docs/forms/assets/rule-editor18.png)

1. Selecione **[!UICONTROL Concluído]** para salvar a regra.

   Agora, adicione uma regra para o campo `Tax Payable `, que é determinado pela multiplicação da receita tributável pela alíquota do imposto. Para simplificar, suponha uma alíquota de imposto fixa de `10%`.

1. No modo de criação, selecione o campo **[!UICONTROL Imposto a Pagar]** e selecione o ícone ![edit-rules](/help/forms/assets/edit-rules-icon.svg). Em seguida, selecione **[!UICONTROL Criar]** para criar regras.
   ![Exemplo do Editor de Regras16](/help/edge/docs/forms/assets/rule-editor19.png)
1. Selecione **[!UICONTROL Selecionar Opção]** e selecione **[!UICONTROL Expressão Matemática]**. Um campo para escrever expressão matemática é aberto.
   ![Exemplo do Editor de Regras17](/help/edge/docs/forms/assets/rule-editor20.png)
1. No campo de expressão matemática:

   * Selecione ou arraste e solte da guia Objeto do Forms o campo **[!UICONTROL Receita Tributável]** no primeiro objeto **[!UICONTROL Soltar ou selecione aqui]**.

   * Selecione **[!UICONTROL Multiplicado por]** no campo **[!UICONTROL Selecionar operador]**.

   * Selecione **Número** no campo **[!UICONTROL Selecionar Opção]** e insira o valor como `10` no campo **[!UICONTROL Inserir um Número]**.
     ![Exemplo do Editor de Regras18](/help/edge/docs/forms/assets/rule-editor21.png)
1. Em seguida, selecione na área destacada ao redor do campo de expressão e selecione **[!UICONTROL Estender expressão]**.
   ![Exemplo do Editor de Regras19](/help/edge/docs/forms/assets/rule-editor22.png)
1. No campo de expressão estendida, selecione **[!UICONTROL dividido por]** no campo **[!UICONTROL Selecionar Operador]** e **[!UICONTROL Número]** no campo **[!UICONTROL Selecionar Opção]**. Em seguida, especifique `100` no campo de número.
   ![Exemplo do Editor de Regras20](/help/edge/docs/forms/assets/rule-editor23.png)
1. Selecione **[!UICONTROL Concluído]** para salvar a regra.

### 4. Pré-visualizar um formulário

Agora, ao visualizar o formulário e inserir o **Salário Bruto** como `60,000`, o campo **Dedução Adicional** será exibido e a **Renda Tributável** e o **Imposto a Pagar** serão calculados adequadamente.

![Visualizar um formulário](/help/edge/docs/forms/assets/rule-editor-form.png)

Além das funções prontas para uso como Sum, Average que estão listadas em Saída de funções, você pode [gravar funções personalizadas](#create-a-custom-function) para implementar lógicas de negócios complexas.

## Função personalizada no editor de regras

O Edge Delivery Services Forms é compatível com funções personalizadas, que permitem aos usuários definir funções do JavaScript para implementar regras de negócios complexas. As funções personalizadas estendem os recursos dos formulários facilitando a manipulação e o processamento dos dados inseridos para atender a requisitos especificados.

### Criar uma função personalizada

Para criar funções personalizadas, edite o arquivo `../[blocks]/form/functions.js`. O processo de criação geralmente envolve as seguintes etapas:

* **Declaração de função**: defina o nome da função e seus parâmetros (as entradas que ela aceita).
* **Implementação lógica**: escreva o código que descreve os cálculos ou manipulações específicos executados pela função.
* **Exportação de Função**: torne a função acessível em suas regras exportando-a do arquivo relevante.


Este exemplo demonstra duas funções personalizadas como `getFullName` e `days`:

```JavaScript
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in Stringformat
 * @param {string} lastname in Stringformat
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

/**
 * Calculate the number of days between two dates.
 * @param {*} endDate
 * @param {*} startDate
 * @name days Calculates the numebr of days between two dates
 * @returns {number} returns the number of days between two dates
 */
function days(endDate, startDate) {
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // return zero if dates are valid
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// eslint-disable-next-line import/prefer-default-export
export { getFullName, days };
```
![Adicionando Função personalizada](/help/edge/docs/forms/assets/create-custom-function.png)

### Usar uma função personalizada no editor de regras

Para usar a função personalizada no Editor de regras:

1. **Adicionar a Função**: Inclua sua função personalizada no arquivo`../[blocks]/form/functions.js`. Lembre-se de adicioná-lo à instrução `export` no arquivo.
1. **Implantar o arquivo**: implante o arquivo `functions.js` atualizado em seu projeto GitHub e verifique se a compilação foi bem-sucedida.
1. **Uso da Função**: acesse a função no Editor de Regras do formulário selecionando a opção `Function Output` no campo **[!UICONTROL Selecionar Ação]**.

   ![Função personalizada no editor de regras](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

1. **Visualizar o formulário**: visualize o formulário com a função recém-implementada.

## Informações adicionais

>[!NOTE]
>
> No Universal Editor, importações estáticas e dinâmicas não são suportadas em scripts de função personalizados. É necessário adicionar o código completo no arquivo `../[blocks]/form/functions.js`.

Este artigo fornece informações limitadas sobre o Editor de regras disponível no Editor universal. Para saber mais sobre o Editor de regras e as funções personalizadas, consulte os seguintes artigos:

{{see-also-rule-editor}}

## Consulte também:

{{universal-editor-see-also}}
