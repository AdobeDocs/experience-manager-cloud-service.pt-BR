---
title: Uso de funções personalizadas em um Formulário adaptável
description: O AEM Forms é compatível com funções personalizadas, que permitem aos usuários criar e usar suas próprias funções no editor de regras.
keywords: Adicionar uma função personalizada, usar uma função personalizada, criar uma função personalizada, usar a função personalizada no editor de regras.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 1%

---


# Introdução às funções personalizadas para o Forms adaptável com base nos Componentes principais

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions-core-components) |
| AEM as a Cloud Service | Este artigo |

O AEM Forms é compatível com funções personalizadas, permitindo que os usuários definam funções do JavaScript para implementar regras de negócios complexas. Essas funções personalizadas estendem os recursos dos formulários facilitando a manipulação e o processamento dos dados inseridos para atender a requisitos especificados. Eles permitem a alteração dinâmica do comportamento do formulário com base em critérios predefinidos. As funções personalizadas também permitem que os desenvolvedores apliquem uma lógica de validação complexa, executem cálculos dinâmicos e controlem a exibição ou o comportamento de elementos de formulário com base em interações do usuário ou critérios predefinidos.

>[!NOTE]
>
> Verifique se o [componente principal](https://github.com/adobe/aem-core-forms-components) está definido como a versão mais recente para usar os recursos mais recentes.

## Usos de funções personalizadas {#uses-of-custom-function}

As vantagens de usar funções personalizadas no Adaptive Forms são:

* **Processamento de dados**: as funções personalizadas ajudam a processar dados inseridos nos campos de formulários.
* **Validação de dados**: as funções personalizadas permitem que você execute verificações personalizadas nas entradas do formulário e forneça mensagens de erro especificadas.
* **Comportamento dinâmico**: as funções personalizadas permitem que você controle o comportamento dinâmico de seus formulários com base em condições específicas. Por exemplo, você pode mostrar/ocultar campos, modificar valores de campo ou ajustar a lógica do formulário dinamicamente.
* **Integração**: você pode usar funções personalizadas para integrar-se a APIs ou serviços externos. Ele ajuda a buscar dados de fontes externas, enviar dados para endpoints Rest externos ou executar ações personalizadas com base em eventos externos.

As funções personalizadas são essencialmente bibliotecas de clientes adicionadas ao arquivo do JavaScript. Depois de criar uma função personalizada, ela fica disponível no editor de regras para seleção pelo usuário em um Formulário adaptável. As funções personalizadas são identificadas pelas anotações do JavaScript no editor de regras.

## Anotações do JavaScript compatíveis com a função personalizada {#js-annotations}

As anotações do JavaScript são usadas para fornecer metadados para o código JavaScript. Inclui comentários que começam com símbolos específicos, por exemplo, /** e @. As anotações fornecem informações importantes sobre funções, variáveis e outros elementos no código. O Formulário adaptável é compatível com as seguintes anotações do JavaScript para funções personalizadas:

### Nome

O nome é usado para identificar a função personalizada no editor de regras de um Formulário adaptável. As seguintes sintaxes são usadas para nomear uma função personalizada:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`.
  `functionName` é o nome da função. Espaços não são permitidos.
  `<Function Name>` é o nome para exibição da função no editor de regras de um Formulário adaptável.
Se o nome da função for idêntico ao nome da própria função, você poderá omitir `[functionName]` da sintaxe.

### Parâmetro

O parâmetro é uma lista de argumentos usados por funções personalizadas. Uma função pode suportar vários parâmetros. As sintaxes a seguir são usadas para definir um parâmetro em uma função personalizada:

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`.
  `{type}` representa o tipo de parâmetro.  Os tipos de parâmetros permitidos são:

   * string: representa um único valor de string.
   * number: representa um único valor numérico.
   * booleano: representa um único valor booleano (verdadeiro ou falso).
   * cadeia de caracteres []: representa uma matriz de valores de cadeia de caracteres.
   * número[]: representa uma matriz de valores numéricos.
   * booleano[]: representa uma matriz de valores booleanos.
   * date: representa um único valor de data.
   * date[]: representa uma matriz de valores de data.
   * array: representa uma matriz genérica contendo valores de vários tipos.
   * object: representa o objeto de formulário passado para uma função personalizada em vez de passar seu valor diretamente.
   * escopo: representa o objeto global, que contém variáveis somente leitura, como instâncias de formulário, instâncias de campo de destino e métodos para executar modificações de formulário em funções personalizadas. Ele é declarado como o último parâmetro nas anotações do JavaScript e não está visível no editor de regras de um Formulário adaptável. O parâmetro scope acessa o objeto do formulário ou componente para acionar a regra ou o evento necessário para o processamento do formulário. Para obter mais informações sobre o objeto Globals e como usá-lo, [clique aqui](/help/forms/custom-function-core-component-scope-function.md).

O tipo de parâmetro não diferencia maiúsculas de minúsculas e espaços não são permitidos no nome do parâmetro.

`<Parameter Description>` contém detalhes sobre a finalidade do parâmetro. Ele pode ter várias palavras.

#### Parâmetros opcionais

Por padrão, todos os parâmetros são obrigatórios. Você pode definir um parâmetro como opcional adicionando `=` após o tipo de parâmetro ou delimitando o nome do parâmetro em `[]`. Os parâmetros definidos como opcionais nas anotações do JavaScript são exibidos como opcionais no editor de regras.
Para definir uma variável como parâmetro opcional, você pode usar qualquer uma das seguintes sintaxes:

* `@param {type=} Input1`

Na linha de código acima, `Input1` é um parâmetro opcional sem nenhum valor padrão. Para declarar parâmetro opcional com valor padrão:
`@param {string=<value>} input1`

`input1` como um parâmetro opcional com o valor padrão definido como `value`.

* `@param {type} [Input1]`

Na linha de código acima, `Input1` é um parâmetro opcional sem nenhum valor padrão. Para declarar parâmetro opcional com valor padrão:
`@param {array} [input1=<value>]`
`input1` é um parâmetro opcional do tipo matriz com o valor padrão definido como `value`.
Verifique se o tipo de parâmetro está entre chaves {} e se o nome do parâmetro está entre colchetes.

Considere o seguinte trecho de código, em que input2 é definido como um parâmetro opcional:

```javascript
        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

A ilustração a seguir é exibida usando a função personalizada `OptionalParameterFunction` no editor de regras:

![Parâmetros &#x200B;](/help/forms/assets/optional-default-params.png) opcionais ou obrigatórios

Você pode salvar a regra sem especificar um valor para os parâmetros necessários, mas a regra não é executada e exibe uma mensagem de aviso como:

![aviso de regra incompleta](/help/forms/assets/incomplete-rule.png)

Quando o usuário deixa o parâmetro opcional vazio, o valor &quot;Indefinido&quot; é passado para a função personalizada do parâmetro opcional.

Para saber mais sobre como definir parâmetros opcionais em JSDocs, [clique aqui](https://jsdoc.app/tags-param).

### Tipo de retorno

O tipo de retorno especifica o tipo de valor que a função personalizada retorna após a execução. As sintaxes a seguir são usadas para definir um tipo de retorno em uma função personalizada:

* `@return {type}`
* `@returns {type}`
  `{type}` representa o tipo de retorno da função. Os tipos de retorno permitidos são:
   * string: representa um único valor de string.
   * number: representa um único valor numérico.
   * booleano: representa um único valor booleano (verdadeiro ou falso).
   * cadeia de caracteres []: representa uma matriz de valores de cadeia de caracteres.
   * número[]: representa uma matriz de valores numéricos.
   * booleano[]: representa uma matriz de valores booleanos.
   * date: representa um único valor de data.
   * date[]: representa uma matriz de valores de data.
   * array: representa uma matriz genérica contendo valores de vários tipos.
   * object: representa o objeto de formulário diretamente em vez do seu valor.

  O tipo de retorno não diferencia maiúsculas de minúsculas.

### Privado

A função personalizada declarada como privada não aparece na lista de funções personalizadas no editor de regras de um formulário adaptável. Por padrão, as funções personalizadas são públicas. A sintaxe para declarar função personalizada como privada é `@private`.


## Diretrizes ao criar funções personalizadas

Para listar as funções personalizadas no editor de regras, você pode usar qualquer um dos seguintes formatos:

### Instrução Function com ou sem comentários jsdoc

Você pode criar uma função personalizada com ou sem comentários jsdoc.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```

Se o usuário não adicionar anotações do JavaScript à função personalizada, ela será listada no editor de regras pelo nome da função. No entanto, é recomendável incluir anotações do JavaScript para melhorar a legibilidade das funções personalizadas.

### Função de seta com anotações ou comentários obrigatórios do JavaScript

É possível criar uma função personalizada com uma sintaxe de função de seta:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

Se o usuário não adicionar anotações JavaScript à função personalizada, a função personalizada não será listada no editor de regras de um Formulário adaptável.

### Expressão de função com anotações ou comentários obrigatórios do JavaScript

Para listar funções personalizadas no editor de regras de um Formulário adaptável, crie funções personalizadas no seguinte formato:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

Se o usuário não adicionar anotações JavaScript à função personalizada, a função personalizada não será listada no editor de regras de um Formulário adaptável.

## Problema conhecido

* As funções personalizadas não suportam literais de expressão regular do JavaScript. O uso de literais regex em uma função personalizada resulta em erros durante a execução. Por exemplo:
  `const pattern = /^abc$/;`

  Para garantir a compatibilidade, use o construtor RegExp nas funções personalizadas.

  `const pattern = new RegExp("^abc$");`
Refatore expressões regulares para usar o construtor RegExp para garantir uma execução consistente e confiável.

## Próxima etapa

Para criar e usar uma função personalizada no formulário adaptável, consulte o artigo [Criar uma função personalizada para um formulário adaptável com base nos componentes principais](/help/forms/custom-function-core-component-create-function.md).

## Consulte também

{{see-also-rule-editor}}