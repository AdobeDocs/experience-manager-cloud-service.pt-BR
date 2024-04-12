---
title: Criar e adicionar funções personalizadas em um Formulário adaptável
description: O AEM Forms é compatível com funções personalizadas que permitem aos usuários criar e usar suas próprias funções no editor de regras.
keywords: Adicionar uma função personalizada, usar uma função personalizada, criar uma função personalizada, usar a função personalizada no editor de regras.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
source-git-commit: e71e247f5b6de806b36c5c759b29e7273511f94e
workflow-type: tm+mt
source-wordcount: '3108'
ht-degree: 0%

---


<span class="preview"> Este artigo apresenta conteúdo para alguns recursos de pré-lançamento. Esses recursos de pré-lançamento estão acessíveis somente por meio de nossos [canal de pré-lançamento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). Os recursos do programa de pré-lançamento são:
* Suporte a parâmetros opcionais em funções personalizadas
* Recurso de armazenamento em cache para funções personalizadas
* Suporte a objetos de escopo global e objetos de campo para funções personalizadas
* Suporte para recursos modernos do JavaScript, como funções let e arrow (suporte ES10).
Certifique-se de que o [o componente principal está definido para a versão 3.0.8](https://github.com/adobe/aem-core-forms-components) para usar os recursos de pré-lançamento na função personalizada. </span>

# Funções personalizadas no Adaptive Forms (Componentes principais)

## Introdução

O AEM Forms é compatível com funções personalizadas, permitindo que os usuários definam funções JavaScript para implementar regras de negócios complexas. Essas funções personalizadas estendem os recursos dos formulários facilitando a manipulação e o processamento dos dados inseridos para atender a requisitos especificados. Elas também permitem a alteração dinâmica do comportamento do formulário com base em critérios predefinidos.

### Usos de funções personalizadas {#uses-of-custom-function}

As vantagens de usar funções personalizadas no Adaptive Forms são:

* **Tratamento de dados**: as funções personalizadas ajudam a processar dados inseridos nos campos de formulários.
* **Validação de dados**: As funções personalizadas permitem que você execute verificações personalizadas nas entradas do formulário e forneça mensagens de erro especificadas.
* **Comportamento dinâmico**: as funções personalizadas permitem controlar o comportamento dinâmico dos formulários com base em condições específicas. Por exemplo, você pode mostrar/ocultar campos, modificar valores de campo ou ajustar a lógica do formulário dinamicamente.
* **Integração**: você pode usar funções personalizadas para integrar-se a APIs ou serviços externos. Ele ajuda a buscar dados de fontes externas, enviar dados para endpoints Rest externos ou executar ações personalizadas com base em eventos externos.

As funções personalizadas são essencialmente bibliotecas de clientes adicionadas ao arquivo JavaScript. Depois de criar uma função personalizada, ela fica disponível no editor de regras para seleção pelo usuário em um Formulário adaptável. As funções personalizadas são identificadas pelas anotações JavaScript no editor de regras.

### Anotações JavaScript compatíveis com a função personalizada {#js-annotations}

As anotações JavaScript são usadas para fornecer metadados para o código JavaScript. Inclui comentários que começam com símbolos específicos, por exemplo, /** e @. As anotações fornecem informações importantes sobre funções, variáveis e outros elementos no código. O Formulário adaptável é compatível com as seguintes anotações JavaScript para funções personalizadas:

#### Nome

O nome é usado para identificar a função personalizada no editor de regras de um formulário adaptável. As seguintes sintaxes são usadas para nomear uma função personalizada:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`.
  `functionName` é o nome da função. Espaços não são permitidos.
  `<Function Name>` é o nome de exibição da função no editor de regras de um Formulário adaptável.
Se o nome da função for idêntico ao nome da própria função, você poderá omitir `[functionName]` na sintaxe. <!-- For example,  in the `calculateAge` custom function, the name is defined as:
`* @name calculateAge` -->

#### Parâmetro

O parâmetro é uma lista de argumentos usados por funções personalizadas. Uma função pode suportar vários parâmetros. As sintaxes a seguir são usadas para definir um parâmetro em uma função personalizada:

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`.
  `{type}` representa o tipo de parâmetro.  Os tipos de parâmetros permitidos são:
   * string: representa um único valor de string.
   * number: representa um único valor numérico.
   * booleano: representa um único valor booleano (verdadeiro ou falso).
   * string[]: representa uma matriz de valores de cadeia de caracteres.
   * número[]: representa uma matriz de valores numéricos.
   * booleano[]: representa uma matriz de valores booleanos.
   * date: representa um único valor de data.
   * data[]: representa uma matriz de valores de data.
   * array: representa uma matriz genérica contendo valores de vários tipos.
   * object: representa o objeto de formulário passado para uma função personalizada em vez de passar seu valor diretamente.
   * scope: representa o objeto global usado pelas funções personalizadas no tempo de execução. Ele é declarado como o último parâmetro nas anotações JavaScript e não está visível no editor de regras de um Formulário adaptável. O parâmetro scope acessa o objeto do formulário ou componente para acionar a regra ou o evento necessário para o processamento do formulário.

    O tipo de parâmetro não diferencia maiúsculas de minúsculas e espaços não são permitidos no nome do parâmetro.
    
    `&lt;parameter description=&quot;&quot;>` contém detalhes sobre a finalidade do parâmetro. Ele pode ter várias palavras.
    
    Por padrão, todos os parâmetros são obrigatórios. Você pode definir um parâmetro como opcional adicionando `=` após o tipo de parâmetro ou colocando o nome do parâmetro em `[]`. Os parâmetros definidos como opcionais nas anotações JavaScript são exibidos como opcionais no editor de regras.
    Para definir uma variável como parâmetro opcional, você pode usar qualquer uma das seguintes sintaxes:
    
    * `@param {type=} Input1`
    
    Na linha de código acima, &quot;Input1&quot; é um parâmetro opcional sem qualquer valor padrão. Para declarar parâmetro opcional com valor padrão:
    `@param {string=&lt;value>} input1`
    
    &quot;input1&quot; como um parâmetro opcional com o valor padrão definido como &quot;value&quot;.
    
    * `@param {type} [Input1]`
    
    Na linha de código acima, &quot;Input1&quot; é um parâmetro opcional sem qualquer valor padrão. Para declarar parâmetro opcional com valor padrão:
    `@param {array} [entrada1=&lt;value>]`
    &quot;input1&quot; é um parâmetro opcional do tipo de matriz com o valor padrão definido como &quot;value&quot;.
    Certifique-se de que o tipo de parâmetro esteja entre chaves {} e o nome do parâmetro está entre colchetes [].
    
    Considere o seguinte trecho de código, em que input2 é definido como um parâmetro opcional:
    
    &quot;javascript
    
    /**
    * função de parâmetro opcional
    * @name OptionalParameterFunction
    * @param {string} entrada1
    * @param {string=} input2
    * @return {string}
    */
    função OptionalParameterFunction(input1, input2) {
    let result = &quot;Resultado: &quot;;
    resultado += input1;
    if (input2 !== null) {
    result += &quot; &quot; + input2;
    }
    resultado de retorno;
    }
    &quot;
    
    A ilustração a seguir é exibida usando a função personalizada &quot;OptionalParameterFunction&quot; no editor de regras:
    
    &lt;!>— ![Parâmetros opcionais ou obrigatórios ](/help/forms/assets/optional-default-params.png) —>
    
    Você pode salvar a regra sem especificar um valor para os parâmetros necessários, mas a regra não é executada e exibe uma mensagem de aviso como:
    
    &lt;!>— ![aviso de regra incompleta](/help/forms/assets/incomplete-rule.png) —>
    
    Quando o usuário deixa o parâmetro opcional vazio, o valor &quot;Indefinido&quot; é passado para a função personalizada do parâmetro opcional.

#### Tipo de retorno

O tipo de retorno especifica o tipo de valor que a função personalizada retorna após a execução. As sintaxes a seguir são usadas para definir um tipo de retorno em uma função personalizada:

* `@return {type}`
* `@returns {type}`
  `{type}` representa o tipo de retorno da função. Os tipos de retorno permitidos são:
   * string: representa um único valor de string.
   * number: representa um único valor numérico.
   * booleano: representa um único valor booleano (verdadeiro ou falso).
   * string[]: representa uma matriz de valores de cadeia de caracteres.
   * número[]: representa uma matriz de valores numéricos.
   * booleano[]: representa uma matriz de valores booleanos.
   * date: representa um único valor de data.
   * data[]: representa uma matriz de valores de data.
   * array: representa uma matriz genérica contendo valores de vários tipos.
   * object: representa o objeto de formulário diretamente em vez do seu valor.

  O tipo de retorno não diferencia maiúsculas de minúsculas.

#### Privado

A função personalizada, declarada como privada, não aparece na lista de funções personalizadas no editor de regras de um formulário adaptável. Por padrão, as funções personalizadas são públicas. A sintaxe para declarar função personalizada como privada é `@private`.

Para saber mais sobre como definir parâmetros opcionais em JSDocs, [clique aqui](https://jsdoc.app/tags-param).

## Diretrizes ao criar funções personalizadas {#considerations}

Para listar as funções personalizadas no editor de regras, você pode usar qualquer um dos seguintes formatos:

* **Instrução Function com ou sem comentários jsdoc**

Você pode criar uma função personalizada com ou sem comentários jsdoc.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```
Se o usuário não adicionar anotações JavaScript à função personalizada, ela será listada no editor de regras pelo nome da função. No entanto, é recomendável incluir anotações JavaScript para melhorar a legibilidade das funções personalizadas.

* **Função de seta com anotações ou comentários obrigatórios do JavaScript**

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

* **Expressão de função com anotações ou comentários obrigatórios do JavaScript**

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

## Criar uma função personalizada {#create-custom-function}

Crie uma biblioteca do cliente para chamar funções personalizadas no editor de regras. Para obter mais informações, consulte [Uso de bibliotecas do lado do cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

As etapas para criar funções personalizadas são:
1. [Criar uma biblioteca do cliente](#create-client-library)
1. [Adicionar a biblioteca do cliente a um Formulário adaptável](#use-custom-function)

### Criar uma biblioteca do cliente {#create-client-library}

Você pode adicionar funções personalizadas adicionando a biblioteca do cliente. Para criar uma biblioteca do cliente, execute as seguintes etapas:

1. [Clonar o repositório as a Cloud Service do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).
1. Crie uma pasta em `[AEM Forms as a Cloud Service repository folder]/apps/` pasta. Por exemplo, crie uma pasta chamada como `experience-league`.
1. Navegue até `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` e criar um `ClientLibraryFolder`. Por exemplo, criar uma pasta da biblioteca do cliente como `customclientlibs`.
1. Adicionar uma propriedade do `categories` com valor de tipo de string. Por exemplo, atribuir o valor `customfunctionscategory` para o `categories` propriedade para o `customclientlibs` pasta.

   >[!NOTE]
   >
   > Você pode escolher qualquer nome para `client library folder` e `categories` propriedade.

1. Crie uma pasta chamada `js`.
1. Navegue até a `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` pasta.
1. Adicione um arquivo JavaScript, por exemplo, `function.js`. O arquivo é composto pelo código da função personalizada.
1. Salve o `function.js` arquivo.
1. Navegue até a `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/customclientlibs/js` pasta.
1. Adicionar um arquivo de texto como `js.txt`. O arquivo contém:

   ```javascript
       #base=js
       functions.js
   ```

1. Salve o `js.txt` arquivo.
1. Adicione, confirme e envie as alterações no repositório usando os comandos abaixo:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. [Executar o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) para implantar a função personalizada.

Depois que o pipeline for executado com êxito, a função personalizada adicionada à biblioteca do cliente ficará disponível no [Editor de regras do Formulário adaptável](/help/forms/rule-editor-core-components.md).

### Adicionar a biblioteca do cliente a um Formulário adaptável{#use-custom-function}

Depois de implantar a biblioteca do cliente no ambiente do Forms CS, use os recursos dela no Formulário adaptável. Para adicionar a biblioteca do cliente no Formulário adaptável

1. Abra o formulário no modo de edição. Para abrir um formulário no modo de edição, selecione um formulário e **[!UICONTROL Editar]**.
1. Abra o Navegador de conteúdo e selecione a variável **[!UICONTROL Contêiner do guia]** componente do seu Formulário adaptável.
1. Clique nas propriedades do Container do guia ![Propriedades do guia](/help/forms/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Abra o **[!UICONTROL Básico]** e selecione o nome da variável **[!UICONTROL categoria da biblioteca do cliente]** na lista suspensa (nesse caso, selecione `customfunctionscategory`).

   ![Adição da biblioteca de cliente de função personalizada](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > É possível adicionar várias categorias especificando uma lista separada por vírgulas na **[!UICONTROL Categoria da biblioteca do cliente]** campo.

1. Clique em **[!UICONTROL Concluído]**.

Você pode usar a função personalizada no [editor de regras de um Formulário adaptável](/help/forms/rule-editor-core-components.md) usando o [Anotações Javascript](##js-annotations).

## Uso da função personalizada em um formulário adaptável

Em um Formulário adaptável, é possível usar [funções personalizadas no editor de regras](/help/forms/rule-editor-core-components.md). Vamos adicionar o seguinte código ao arquivo JavaScript (`Function.js` arquivo) para calcular a idade com base na Data de nascimento (AAAA-MM-DD). Criar uma função personalizada como `calculateAge()` que toma a data de nascimento como entrada e retorna a idade:

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

No exemplo acima, quando o usuário insere a data de nascimento no formato (AAAA-MM-DD), a função personalizada `calculateAge` é chamado e retorna a idade.

![Função personalizada Calcular idade no Editor de regras](/help/forms/assets/custom-function-calculate-age.png)

Vamos visualizar o formulário para observar como as funções personalizadas são implementadas por meio do editor de regras:

![Função personalizada Calcular Idade na Visualização de Formulário do Editor de Regras](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Você pode consultar o seguinte [função personalizada](/help/forms/assets//customfunctions.zip) pasta. Baixe e instale essa pasta na instância do AEM usando o [Gerenciador de pacotes](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).

### Suporte para funções assíncronas em funções personalizadas {#support-of-async-functions}

As funções personalizadas assíncronas não aparecem na lista do editor de regras. No entanto, é possível chamar funções assíncronas em funções personalizadas criadas usando expressões de função síncrona.

![Função personalizada síncrona e assíncrona](/help/forms/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> A vantagem de chamar funções assíncronas em funções personalizadas é que as funções assíncronas permitem a execução simultânea de várias tarefas, com o resultado de cada função usada nas funções personalizadas.

Examine o código abaixo para ver como podemos chamar funções assíncronas usando funções personalizadas:

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

No exemplo acima, a função asyncFunction é uma `asynchronous function`. Ele executa uma operação assíncrona tornando um `GET` solicitação para `https://petstore.swagger.io/v2/store/inventory`. Ele aguarda a resposta usando `await`, analisa o corpo da resposta como JSON usando o `response.json()`e retorna os dados. A variável `callAsyncFunction` é uma função personalizada síncrona que chama a variável `asyncFunction` e exibe os dados de resposta no console. Embora a `callAsyncFunction` é síncrona, ela chama a função assíncrona asyncFunction e lida com seu resultado com `then` e `catch` declarações.

Para ver seu funcionamento, vamos adicionar um botão e criar uma regra para o botão que chama a função assíncrona em um clique de botão.

![criando regra para função assíncrona](/help/forms/assets/rule-for-async-funct.png)

Consulte a ilustração da janela de console abaixo para demonstrar que, quando o usuário clicar no ícone `Fetch` botão, a função personalizada `callAsyncFunction` é invocado, que por sua vez chama uma função assíncrona `asyncFunction`. Inspect na janela do console para exibir a resposta ao clicar no botão:

![Janela do console](/help/forms/assets/async-custom-funct-console.png)

Vamos analisar os recursos de funções personalizadas.

## Vários recursos para funções personalizadas

Você pode usar funções personalizadas para adicionar recursos personalizados a formulários. Essas funções oferecem suporte a várias habilidades, como trabalhar com campos específicos, usar campos globais ou armazenar em cache. Essa flexibilidade permite personalizar formulários de acordo com os requisitos de sua organização.

### Objetos de escopo de campo e global em funções personalizadas {#support-field-and-global-objects}

Objetos de campo referem-se aos componentes ou elementos individuais em um formulário, como campos de texto e caixas de seleção. Os objetos de escopo global se referem às variáveis ou configurações globais que são acessíveis em todo o formulário. Vamos analisar o seguinte fragmento de código:

```JavaScript
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals 
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time
    field.value = formattedDateTime;
    }
```

>[!NOTE]
>
> A variável `param {scope} globals` deve ser o último parâmetro e não é exibido no editor de regras de um Formulário adaptável.

No trecho de código acima, uma função personalizada chamada `updateDateTime` A obtém parâmetros como um objeto de campo e um objeto global. Os objetos de data e hora são acessados usando o escopo global. O campo representa o objeto de caixa de texto em que o valor de data e hora formatado é exibido no formulário.

Saiba como as funções personalizadas usam campos e objetos globais com a ajuda de um `Contact Us` formulário usando casos de uso diferentes.

![Formulário Contate-nos](/help/forms/assets/contact-us-form.png)

#### **Caso de uso**: mostrar um painel usando o `SetProperty` regra

Adicione o seguinte código na função personalizada, conforme explicado na [create-custom-function](#create-custom-function) para definir o campo de formulário como `Required`.

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> É possível configurar as propriedades do campo usando as propriedades disponíveis localizadas em `[form-path]/jcr:content/guideContainer.model.json`.

Neste exemplo, a validação do `personaldetails` ocorre ao clicar no botão. Se nenhum erro for detectado no painel, outro painel, o `feedback` fica visível ao clicar no botão.

Vamos criar uma regra para o `Next` botão, que valida a `personaldetails` e torna o `feedback`  painel visível quando o usuário clicar no botão `Next` botão.

![Definir propriedade](/help/forms/assets/custom-function-set-property.png)

Consulte a ilustração abaixo para demonstrar onde a variável `personaldetails` for validado ao clicar no link `Next` botão. Caso todos os campos dentro do `personaldetails` forem validados, a variável `feedback` painel fica visível.

![Definir propriedade para visualização do formulário](/help/forms/assets/set-property-form-preview.png)

Se houver erros nos campos do `personaldetails` são exibidos no nível do campo ao clicar no botão `Next` e o botão `feedback` permanece invisível.

![Definir propriedade para visualização do formulário](/help/forms/assets/set-property-panel.png)

#### **Caso de uso**: valide o campo.

Adicione o seguinte código na função personalizada, conforme explicado na [create-custom-function](#create-custom-function) para validar o campo.

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> Se nenhum argumento for transmitido na variável `validate()` valida o formulário.

Neste exemplo, um padrão de validação personalizado é aplicado à variável `contact` campo. Os usuários devem inserir um número de telefone começando com `10` seguido por `8` dígitos. Se o usuário digitar um número de telefone que não inicia com `10` ou contém mais ou menos que `8` dígitos, uma mensagem de erro de validação é exibida ao clicar no botão:

![Padrão de validação do endereço de email](/help/forms/assets/custom-function-validation-pattern.png)

Agora, a próxima etapa é criar uma regra para o `Next` botão que valida o `contact` no botão, clique em.

![Padrão de validação](/help/forms/assets/custom-function-validate.png)

Consulte a ilustração abaixo para demonstrar que, se o usuário digitar um número de telefone que não comece com `10`, uma mensagem de erro é exibida no nível do campo:

![Padrão de validação do endereço de email](/help/forms/assets/custom-function-validate-error-message.png)

Se o usuário digitar um número de telefone válido e todos os campos na variável `personaldetails` forem validados, a variável `feedback` será exibido na tela:

![Padrão de validação do endereço de email](/help/forms/assets/validate-form-preview-form.png)

#### **Caso de uso**: redefinir um painel

Adicione o seguinte código na função personalizada, conforme explicado na [create-custom-function](#create-custom-function) para redefinir o painel.

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> Se nenhum argumento for transmitido na variável `reset()` valida o formulário.

Neste exemplo, a variável `personaldetails` O painel é redefinido ao clicar no ícone `Clear` botão. A próxima etapa é criar uma regra para o `Clear` botão que redefine o painel no clique de botão.

![Botão Limpar](/help/forms/assets/custom-function-reset-field.png)

Consulte a ilustração abaixo para exibir que, se o usuário clicar no ícone `clear` botão, o botão `personaldetails` o painel é redefinido:

![Redefinir formulário](/help/forms/assets/custom-function-reset-form.png)

#### **Caso de uso**: para exibir uma mensagem personalizada no nível do campo e marcar o campo como inválido

Você pode usar o `markFieldAsInvalid()` função para definir um campo como inválido e definir mensagem de erro personalizada em nível de campo. A variável `fieldIdentifier` o valor pode ser `fieldId`ou `field qualifiedName`ou `field dataRef`. O valor do objeto chamado `option` pode ser `{useId: true}`, `{useQualifiedName: true}`ou `{useDataRef: true}`.
As sintaxes usadas para marcar o campo como inválido e definir uma mensagem personalizada são:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Adicione o seguinte código na função personalizada, conforme explicado na [create-custom-function](#create-custom-function) para ativar a mensagem personalizada no nível do campo.

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

Neste exemplo, se o usuário inserir menos de 15 caracteres na caixa de texto comentários, uma mensagem personalizada será exibida no nível do campo.

A próxima etapa é criar uma regra para o `comments` campo:

![Marcar campo como inválido](/help/forms/assets/custom-function-invalid-field.png)

Consulte a demonstração abaixo para exibir que inserir feedback negativo na `comments` aciona a exibição de uma mensagem personalizada no nível do campo:

![Marcar campo como Formulário de visualização inválido](/help/forms/assets/custom-function-invalidfield-form.png)

Se o usuário inserir mais de 15 caracteres na caixa de texto de comentários, o campo será validado e o formulário será enviado:

![Marcar campo como formulário de Visualização válido](/help/forms/assets/custom-function-validfield-form.png)


#### **Caso de uso**: Enviar os dados alterados para o servidor

A seguinte linha de código:
`globals.functions.submitForm(globals.functions.exportData(), false);` é usado para enviar os dados do formulário após manipulação.
* O primeiro argumento diz respeito aos dados a apresentar.
* O segundo argumento representa se o formulário deve ser validado antes do envio. É necessário `optional` e definir como `true` por padrão.
* O terceiro argumento é `contentType` da apresentação, que é igualmente `optional` com o valor padrão como `multipart/form-data`.

Adicione o seguinte código na função personalizada, conforme explicado na [create-custom-function](#create-custom-function) para enviar os dados manipulados no servidor:

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */

    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

Neste exemplo, se o usuário deixar a variável `comments` caixa de texto vazia, a variável `NA` é enviado ao servidor no envio do formulário.

Agora crie uma regra para o `Submit` botão que envia dados:

![Enviar dados](/help/forms/assets/custom-function-submit-data.png)

Consulte a ilustração do `console window` abaixo para demonstrar que, se o usuário deixar o `comments` caixa de texto vazia, depois o valor como `NA` é enviado ao servidor:

![Enviar dados na janela do console](/help/forms/assets/custom-function-submit-data-form.png)

Você também pode inspecionar a janela do console para visualizar os dados enviados para o servidor:

![Dados do Inspect na janela do console](/help/forms/assets/custom-function-submit-data-console-data.png)

## Suporte de cache para função personalizada

O Forms adaptável implementa o armazenamento em cache de funções personalizadas para melhorar o tempo de resposta ao recuperar a lista de funções personalizadas no editor de regras. Uma mensagem como `Fetched following custom functions list from cache` aparece na guia `error.log` arquivo.

![função personalizada com suporte a cache](/help/forms/assets/custom-function-cache-error.png)

Caso as funções personalizadas sejam modificadas, o armazenamento em cache é invalidado e é analisado.

## Resolução de problemas

Se o arquivo JavaScript que contém o código para funções personalizadas tiver um erro, as funções personalizadas não serão listadas no editor de regras de um Formulário adaptável. Para verificar a lista de funções personalizadas, você pode navegar até a `error.log` para o erro. No caso de um erro, a lista de funções personalizadas aparece vazia:

![arquivo de log de erros](/help/forms/assets/custom-function-list-error-file.png)

Caso não haja erro, a função personalizada é buscada e aparece no `error.log` arquivo. Uma mensagem como `Fetched following custom functions list` aparece na guia `error.log` arquivo:

![arquivo de log de erros com função personalizada adequada](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Considerações

* A variável `parameter type` e `return type` não oferecem suporte `None`.

* As funções não suportadas na lista de funções personalizadas são:
   * Funções geradoras
   * Funções assíncronas/Await
   * Definições de método
   * Métodos de classe
   * Parâmetros padrão
   * Parâmetros rest

## Consulte também {#see-also}

{{see-also}}


