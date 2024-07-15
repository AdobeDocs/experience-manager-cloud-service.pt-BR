---
title: Criar e adicionar funções personalizadas em um Formulário adaptável
description: O AEM Forms é compatível com funções personalizadas, que permitem aos usuários criar e usar suas próprias funções no editor de regras.
keywords: Adicionar uma função personalizada, usar uma função personalizada, criar uma função personalizada, usar a função personalizada no editor de regras.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 24607dd1-2d65-480b-a831-9071e20c473d
role: User, Developer
source-git-commit: 52b87073cad84705b5dc0c6530aff44d1e686609
workflow-type: tm+mt
source-wordcount: '4333'
ht-degree: 0%

---


# Funções personalizadas no Adaptive Forms (Componentes principais)

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/create-and-use-custom-functions) |
| AEM as a Cloud Service | Este artigo |

## Introdução

O AEM Forms é compatível com funções personalizadas, permitindo que os usuários definam funções do JavaScript para implementar regras de negócios complexas. Essas funções personalizadas estendem os recursos dos formulários facilitando a manipulação e o processamento dos dados inseridos para atender a requisitos especificados. Elas também permitem a alteração dinâmica do comportamento do formulário com base em critérios predefinidos.

>[!NOTE]
>
> Verifique se o [componente principal](https://github.com/adobe/aem-core-forms-components) está definido como a versão mais recente para usar os recursos mais recentes.

### Usos de funções personalizadas {#uses-of-custom-function}

As vantagens de usar funções personalizadas no Adaptive Forms são:
* **Processamento de dados**: as funções personalizadas ajudam a processar dados inseridos nos campos de formulários.
* **Validação de dados**: as funções personalizadas permitem que você execute verificações personalizadas nas entradas do formulário e forneça mensagens de erro especificadas.
* **Comportamento dinâmico**: as funções personalizadas permitem que você controle o comportamento dinâmico de seus formulários com base em condições específicas. Por exemplo, você pode mostrar/ocultar campos, modificar valores de campo ou ajustar a lógica do formulário dinamicamente.
* **Integração**: você pode usar funções personalizadas para integrar-se a APIs ou serviços externos. Ele ajuda a buscar dados de fontes externas, enviar dados para endpoints Rest externos ou executar ações personalizadas com base em eventos externos.

As funções personalizadas são essencialmente bibliotecas de clientes adicionadas ao arquivo do JavaScript. Depois de criar uma função personalizada, ela fica disponível no editor de regras para seleção pelo usuário em um Formulário adaptável. As funções personalizadas são identificadas pelas anotações do JavaScript no editor de regras.

### Anotações do JavaScript compatíveis com a função personalizada {#js-annotations}

As anotações do JavaScript são usadas para fornecer metadados para o código JavaScript. Inclui comentários que começam com símbolos específicos, por exemplo, /** e @. As anotações fornecem informações importantes sobre funções, variáveis e outros elementos no código. O Formulário adaptável é compatível com as seguintes anotações do JavaScript para funções personalizadas:

#### Nome

O nome é usado para identificar a função personalizada no editor de regras de um Formulário adaptável. As seguintes sintaxes são usadas para nomear uma função personalizada:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`.
  `functionName` é o nome da função. Espaços não são permitidos.
  `<Function Name>` é o nome para exibição da função no editor de regras de um Formulário adaptável.
Se o nome da função for idêntico ao nome da própria função, você poderá omitir `[functionName]` da sintaxe.

#### Parâmetro

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
   * escopo: representa o objeto global, que contém variáveis somente leitura, como instâncias de formulário, instâncias de campo de destino e métodos para executar modificações de formulário em funções personalizadas. Ele é declarado como o último parâmetro nas anotações do JavaScript e não está visível no editor de regras de um Formulário adaptável. O parâmetro scope acessa o objeto do formulário ou componente para acionar a regra ou o evento necessário para o processamento do formulário. Para obter mais informações sobre o objeto Globals e como usá-lo, [clique aqui](/help/forms/create-and-use-custom-functions.md#support-field-and-global-objects).

O tipo de parâmetro não diferencia maiúsculas de minúsculas e espaços não são permitidos no nome do parâmetro.

`<Parameter Description>` contém detalhes sobre a finalidade do parâmetro. Ele pode ter várias palavras.

**Parâmetros Opcionais**
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

![Parâmetros ](/help/forms/assets/optional-default-params.png) opcionais ou obrigatórios

Você pode salvar a regra sem especificar um valor para os parâmetros necessários, mas a regra não é executada e exibe uma mensagem de aviso como:

![aviso de regra incompleta](/help/forms/assets/incomplete-rule.png)

Quando o usuário deixa o parâmetro opcional vazio, o valor &quot;Indefinido&quot; é passado para a função personalizada do parâmetro opcional.

Para saber mais sobre como definir parâmetros opcionais em JSDocs, [clique aqui](https://jsdoc.app/tags-param).

#### Tipo de retorno

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

#### Privado

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

## Criar uma função personalizada {#create-custom-function}

Crie uma biblioteca do cliente para chamar funções personalizadas no editor de regras. Para obter mais informações, consulte [Usando bibliotecas do lado do cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

As etapas para criar funções personalizadas são:
1. [Criar uma biblioteca do cliente](#create-client-library)
1. [Adicionar a biblioteca do cliente a um Formulário adaptável](#use-custom-function)


### Pré-requisitos para criar uma função personalizada

Antes de começar a adicionar uma função personalizada ao Adaptive Forms, verifique se você tem o seguinte:

**Software:**

* **Editor de Texto sem Formatação (IDE)**: embora qualquer editor de texto sem formatação possa funcionar, um IDE (Ambiente de Desenvolvimento Integrado) como o Microsoft Visual Studio Code oferece recursos avançados para facilitar a edição.

* **Git:** este sistema de controle de versão é necessário para gerenciar alterações de código. Se não estiver instalado, baixe-o de https://git-scm.com.

### Criar uma biblioteca do cliente {#create-client-library}

É possível adicionar funções personalizadas adicionando uma biblioteca do cliente. Para criar uma biblioteca do cliente, execute as seguintes etapas:

**Clonar o Repositório**

Clonar o [Repositório as a Cloud Service do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git):

1. Abra a linha de comando ou a janela do terminal.

1. Navegue até o local desejado na máquina em que deseja armazenar o repositório.

1. Execute o seguinte comando para clonar o repositório:

   `git clone [Git Repository URL]`

Este comando faz o download do repositório e cria uma pasta local do repositório clonado no computador. Neste guia, nos referimos a essa pasta como o [diretório do projeto AEMaaCS].

**Adicionar uma pasta da biblioteca do cliente**

Para adicionar uma nova pasta da biblioteca do cliente ao [diretório do projeto AEMaaCS], siga estas etapas:

1. Abra o [diretório do projeto AEMaaCS] em um editor.

   ![estrutura de pasta de função personalizada](/help/forms/assets/custom-library-folder-structure.png)

1. Localizar `ui.apps`.
1. Adicionar nova pasta. Por exemplo, adicione uma pasta chamada `experience-league`.
1. Navegue até a pasta `/experience-league/` e adicione um `ClientLibraryFolder`. Por exemplo, crie uma pasta da biblioteca do cliente chamada `customclientlibs`.

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**Adicionar arquivos e pastas à pasta da Biblioteca do Cliente**

Adicione o seguinte à pasta da biblioteca do cliente adicionada:

* arquivo .content.xml
* arquivo js.txt
* pasta js

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. Em `.content.xml`, adicione as seguintes linhas de código:

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > Você pode escolher qualquer nome para a propriedade `client library folder` e `categories`.

1. Em `js.txt`, adicione as seguintes linhas de código:

   ```javascript
         #base=js
       function.js
   ```
1. Na pasta `js`, adicione o arquivo javascript como `function.js`, o que inclui as funções personalizadas:

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
1. Salve os arquivos.

![estrutura de pasta de função personalizada](/help/forms/assets/custom-function-added-files.png)

**Incluir a nova pasta no filter.xml**:

1. Navegue até o arquivo `/ui.apps/src/main/content/META-INF/vault/filter.xml` no seu [diretório do projeto AEMaaCS].

1. Abra o arquivo e adicione a seguinte linha no final:

   `<filter root="/apps/experience-league" />`
1. Salve o arquivo.

![xml de filtro de função personalizada](/help/forms/assets/custom-function-filterxml.png)

**Implante a pasta da biblioteca do cliente recém-criada no seu ambiente AEM**

Implante o AEM as a Cloud Service, [diretório do projeto AEMaaCS], no seu ambiente Cloud Service. Para implantar no ambiente de Cloud Service:

1. Confirmar as alterações

   1. Adicione, confirme e envie as alterações no repositório usando os comandos abaixo:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. Implante o código atualizado:

   1. Acione uma implantação do seu código por meio do pipeline de pilha completa existente. Isso cria e implanta automaticamente o código atualizado.

Se você ainda não tiver configurado um pipeline, consulte o manual sobre [como configurar um pipeline para o AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline).

Depois que o pipeline for executado com êxito, a função personalizada adicionada à biblioteca do cliente ficará disponível em seu [editor de regras de Formulário adaptável](/help/forms/rule-editor-core-components.md).

### Adicionar a biblioteca do cliente a um Formulário adaptável{#use-custom-function}

Depois de implantar a biblioteca do cliente no ambiente do Forms CS, use os recursos dela no Formulário adaptável. Para adicionar a biblioteca do cliente no Formulário adaptável

1. Abra o formulário no modo de edição. Para abrir um formulário no modo de edição, selecione um formulário e selecione **[!UICONTROL Editar]**.
1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Abra a guia **[!UICONTROL Básico]** e selecione o nome da **[!UICONTROL categoria da biblioteca do cliente]** na lista suspensa (neste caso, selecione `customfunctionscategory`).

   ![Adicionando a biblioteca cliente de função personalizada](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > É possível adicionar várias categorias especificando uma lista separada por vírgulas no campo **[!UICONTROL Categoria da biblioteca do cliente]**.

1. Clique em **[!UICONTROL Concluído]**.

Você pode usar a função personalizada no [editor de regras de um Formulário Adaptável](/help/forms/rule-editor-core-components.md) usando as [anotações do JavaScript](##js-annotations).

## Uso de uma função personalizada em um Formulário adaptável

Em um Formulário adaptável, você pode usar [funções personalizadas no editor de regras](/help/forms/rule-editor-core-components.md). Vamos adicionar o seguinte código ao arquivo JavaScript (arquivo `Function.js`) para calcular a idade com base na Data de Nascimento (AAAA-MM-DD). Crie uma função personalizada como `calculateAge()` que use a data de nascimento como entrada e retorne a idade:

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

No exemplo acima, quando o usuário insere a data de nascimento no formato (AAAA-MM-DD), a função personalizada `calculateAge` é invocada e retorna a idade.

![Função personalizada Calcular Idade no Editor de Regras](/help/forms/assets/custom-function-calculate-age.png)

Vamos visualizar o formulário para observar como as funções personalizadas são implementadas por meio do editor de regras:

![Função personalizada Calcular Idade na Visualização de Formulário do Editor de Regras](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Você pode consultar a seguinte pasta [função personalizada](/help/forms/assets//customfunctions.zip). Baixe e instale esta pasta na instância do AEM usando o [Gerenciador de Pacotes](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).


### Definir as opções da lista suspensa usando funções personalizadas

O Editor de Regras nos Componentes Principais não oferece suporte à propriedade **Definir Opções de** para definir as opções da lista suspensa no tempo de execução. No entanto, é possível definir as opções da lista suspensa usando funções personalizadas.

Examine o código abaixo para ver como podemos definir as opções da lista suspensa usando funções personalizadas:

```javascript
    /**
    * @name setEnums
    * @returns {string[]}
    **/
    function setEnums() {
    return ["0","1","2","3","4","5","6"];   
    }

    /**
    * @name setEnumNames
    * @returns {string[]}
    **/
    function setEnumNames() {
    return ["Sunday","Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
    }
```

No código acima, `setEnums` é usado para definir a propriedade `enum` e `setEnumNames` é usado para definir a propriedade `enumNames` da lista suspensa.

Vamos criar uma regra para o botão `Next`, que define o valor da opção de lista suspensa quando o usuário clica no botão `Next`:

![Opções da lista suspensa](/help/forms/assets/drop-down-list-options.png)

Consulte a ilustração abaixo para demonstrar onde as opções da lista suspensa são definidas ao clicar no botão Display:

![Opções suspensas no Editor de regras](/help/forms/assets/drop-down-option-rule-editor.png)



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

No exemplo acima, a função asyncFunction é um `asynchronous function`. Ele executa uma operação assíncrona fazendo uma solicitação `GET` para `https://petstore.swagger.io/v2/store/inventory`. Ele aguarda a resposta usando `await`, analisa o corpo da resposta como JSON usando `response.json()` e retorna os dados. A função `callAsyncFunction` é uma função personalizada síncrona que chama a função `asyncFunction` e exibe os dados de resposta no console. Embora a função `callAsyncFunction` seja síncrona, ela chama a função asyncFunction assíncrona e manipula seu resultado com instruções `then` e `catch`.

Para ver seu funcionamento, vamos adicionar um botão e criar uma regra para o botão que chama a função assíncrona em um clique de botão.

![criando regra para função assíncrona](/help/forms/assets/rule-for-async-funct.png)

Consulte a ilustração da janela de console abaixo para demonstrar que, quando o usuário clica no botão `Fetch`, a função personalizada `callAsyncFunction` é invocada, o que, por sua vez, chama uma função assíncrona `asyncFunction`. Inspect na janela do console para exibir a resposta ao clique de botão:

![Janela de console](/help/forms/assets/async-custom-funct-console.png)

Vamos analisar os recursos de funções personalizadas.

## Vários recursos para funções personalizadas

Você pode usar funções personalizadas para adicionar recursos personalizados a formulários. Essas funções oferecem suporte a várias habilidades, como trabalhar com campos específicos, usar campos globais ou armazenar em cache. Essa flexibilidade permite personalizar formulários de acordo com os requisitos de sua organização.

### Objetos de escopo de campo e global em funções personalizadas {#support-field-and-global-objects}

Os objetos Field referem-se aos componentes ou elementos individuais em um formulário, como campos de texto e caixas de seleção. O objeto Globals contém variáveis somente leitura, como instância de formulário, instância de campo de destino e métodos para fazer modificações de formulário em funções personalizadas.

>[!NOTE]
>
> O `param {scope} globals` deve ser o último parâmetro e não é exibido no editor de regras de um Formulário adaptável.

<!-- Let us look at the following code snippet:

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
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

Saiba como as funções personalizadas usam campos e objetos globais com a ajuda de um formulário `Contact Us` usando casos de uso diferentes.

![Formulário Contate-nos](/help/forms/assets/contact-us-form.png)

+++ **Caso de uso**: mostrar um painel usando a regra `SetProperty`

Adicione o seguinte código na função personalizada, como explicado na seção [create-custom-function](#create-custom-function), para definir o campo de formulário como `Required`.

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
> * Você pode configurar as propriedades de campo usando as propriedades disponíveis localizadas em `[form-path]/jcr:content/guideContainer.model.json`.
> * As modificações feitas no formulário usando o método `setProperty` do objeto Globals são de natureza assíncrona e não são refletidas durante a execução da função personalizada.

Neste exemplo, a validação do painel `personaldetails` ocorre ao clicar no botão. Se nenhum erro for detectado no painel, outro painel, o painel `feedback`, ficará visível ao clicar no botão.

Vamos criar uma regra para o botão `Next`, que valida o painel `personaldetails` e torna o painel `feedback` visível quando o usuário clica no botão `Next`.

![Definir Propriedade](/help/forms/assets/custom-function-set-property.png)

Consulte a ilustração abaixo para demonstrar onde o painel `personaldetails` é validado ao clicar no botão `Next`. Caso todos os campos em `personaldetails` sejam validados, o painel `feedback` ficará visível.

![Definir Propriedade de Visualização de Formulário](/help/forms/assets/set-property-form-preview.png)

Se houver erros nos campos do painel `personaldetails`, eles serão exibidos no nível do campo ao clicar no botão `Next` e o painel `feedback` permanecerá invisível.

![Definir Propriedade de Visualização de Formulário](/help/forms/assets/set-property-panel.png)

+++

+++ **Caso de uso**: validar o campo.

Adicione o seguinte código na função personalizada conforme explicado na seção [create-custom-function](#create-custom-function) para validar o campo.

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
> Se nenhum argumento for passado na função `validate()`, ele validará o formulário.

Neste exemplo, um padrão de validação personalizado é aplicado ao campo `contact`. Os usuários precisam inserir um número de telefone começando com `10` seguido de `8` dígitos. Se o usuário digitar um número de telefone que não comece com `10` ou contenha mais ou menos de `8` dígitos, uma mensagem de erro de validação será exibida ao clicar no botão:

![Padrão de Validação de Endereço de Email](/help/forms/assets/custom-function-validation-pattern.png)

Agora, a próxima etapa é criar uma regra para o botão `Next` que valide o campo `contact` no clique de botão.

![Padrão de validação](/help/forms/assets/custom-function-validate.png)

Consulte a ilustração abaixo para demonstrar que, se o usuário digitar um número de telefone que não comece com `10`, uma mensagem de erro será exibida no nível do campo:

![Padrão de Validação de Endereço de Email](/help/forms/assets/custom-function-validate-error-message.png)

Se o usuário digitar um número de telefone válido e todos os campos no painel `personaldetails` forem validados, o painel `feedback` aparecerá na tela:

![Padrão de Validação de Endereço de Email](/help/forms/assets/validate-form-preview-form.png)

+++

+++ **Caso de uso**: redefinir um painel

Adicione o seguinte código na função personalizada, como explicado na seção [create-custom-function](#create-custom-function), para redefinir o painel.

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
> Se nenhum argumento for passado na função `reset()`, ele validará o formulário.

Neste exemplo, o painel `personaldetails` é redefinido ao clicar no botão `Clear`. A próxima etapa é criar uma regra para o botão `Clear` que redefina o painel no clique do botão.

![Botão Limpar](/help/forms/assets/custom-function-reset-field.png)

Consulte a ilustração abaixo para mostrar que, se o usuário clicar no botão `clear`, o painel `personaldetails` será redefinido:

![Redefinir Formulário](/help/forms/assets/custom-function-reset-form.png)

+++

+++ **Caso de uso**: para exibir uma mensagem personalizada no nível do campo e marcar o campo como inválido

Você pode usar a função `markFieldAsInvalid()` para definir um campo como inválido e definir uma mensagem de erro personalizada em nível de campo. O valor `fieldIdentifier` pode ser `fieldId`, `field qualifiedName` ou `field dataRef`. O valor do objeto nomeado `option` pode ser `{useId: true}`, `{useQualifiedName: true}` ou `{useDataRef: true}`.
As sintaxes usadas para marcar um campo como inválido e definir uma mensagem personalizada são:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Adicione o seguinte código na função personalizada conforme explicado na seção [create-custom-function](#create-custom-function) para habilitar uma mensagem personalizada no nível do campo.

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

A próxima etapa é criar uma regra para o campo `comments`:

![Marcar campo como Inválido](/help/forms/assets/custom-function-invalid-field.png)

Veja a demonstração abaixo para mostrar que inserir comentários negativos no campo `comments` aciona a exibição de uma mensagem personalizada no nível do campo:

![Marcar campo como Formulário de visualização inválido](/help/forms/assets/custom-function-invalidfield-form.png)

Se o usuário inserir mais de 15 caracteres na caixa de texto de comentários, o campo será validado e o formulário será enviado:

![Marcar campo como formulário de Visualização válido](/help/forms/assets/custom-function-validfield-form.png)

+++

+++ **Caso de uso**: enviar dados alterados para o servidor

A seguinte linha de código:
`globals.functions.submitForm(globals.functions.exportData(), false);` é usado para enviar os dados do formulário após manipulação.
* O primeiro argumento diz respeito aos dados a apresentar.
* O segundo argumento representa se o formulário deve ser validado antes do envio. Ele é `optional` e definido como `true` por padrão.
* O terceiro argumento é o `contentType` do envio, que também é opcional com o valor padrão como `multipart/form-data`. Os outros valores podem ser `application/json` e `application/x-www-form-urlencoded`.

Adicione o seguinte código na função personalizada, conforme explicado na seção [create-custom-function](#create-custom-function), para enviar os dados manipulados no servidor:

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

Neste exemplo, se o usuário deixar a caixa de texto `comments` vazia, o `NA` será enviado ao servidor no envio do formulário.

Agora, crie uma regra para o botão `Submit` que envia dados:

![Enviar dados](/help/forms/assets/custom-function-submit-data.png)

Consulte a ilustração da `console window` abaixo para demonstrar que, se o usuário deixar a caixa de texto `comments` vazia, o valor como `NA` será enviado ao servidor:

![Enviar dados na janela do console](/help/forms/assets/custom-function-submit-data-form.png)

Você também pode inspecionar a janela do console para visualizar os dados enviados para o servidor:

![Dados do Inspect na janela do console](/help/forms/assets/custom-function-submit-data-console-data.png)

+++

+++ **Caso de uso**: substituição de manipuladores de erros e de êxito no envio de formulários

Adicione a seguinte linha de código, conforme explicado na seção [create-custom-function](#create-custom-function), para personalizar a mensagem de envio ou de falha para envios de formulário e exibir as mensagens de envio de formulário em uma caixa modal:

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

Neste exemplo, quando o usuário usa as funções personalizadas `customSubmitSuccessHandler` e `customSubmitErrorHandler`, as mensagens de êxito e falha são exibidas em uma modal. A função de JavaScript `showModal(type, message)` é usada para criar e exibir dinamicamente uma caixa de diálogo modal em uma tela.

Agora, crie uma regra para o envio bem-sucedido do formulário:

![Êxito no envio do formulário](/help/forms/assets/form-submission-success.png)

Consulte a ilustração abaixo para demonstrar que, quando o formulário for enviado com êxito, a mensagem de sucesso será exibida em uma modal:

![Mensagem de êxito de envio de formulário](/help/forms/assets/form-submission-success-message.png)

Da mesma forma, vamos criar uma regra para envios de formulários com falha:

![Falha no envio do formulário](/help/forms/assets/form-submission-fail.png)

Consulte a ilustração abaixo para demonstrar que, quando o envio do formulário falhar, a mensagem de erro será exibida em uma modal:

![Mensagem de falha no envio do formulário](/help/forms/assets/form-submission-fail-message.png)

Para exibir o sucesso e a falha no envio de formulários de maneira padrão, as funções `Default submit Form Success Handler` e `Default submit Form Error Handler` estão disponíveis prontas para uso.

Caso o manipulador de envio personalizado não seja executado conforme esperado em projetos ou formulários AEM existentes, consulte a seção [solução de problemas](#troubleshooting).

+++

+++ **Caso de uso**: executar ações em uma instância específica do painel repetível

As regras criadas usando o editor visual de regras em um painel repetível se aplicam à última instância do painel repetível. Para escrever uma regra para uma instância específica do painel repetível, podemos usar uma função personalizada.

Vamos criar outro formulário para coletar informações sobre os viajantes que estão indo para um destino. Um painel de viagem é adicionado como um painel repetível, em que o usuário pode adicionar detalhes para 5 viajantes usando o botão `Add Traveler`.

![Informações do viajante](/help/forms/assets/traveler-info-form.png)

Adicione a seguinte linha de código, conforme explicado na seção [create-custom-function](#create-custom-function), para executar ações em uma instância específica do painel repetível, diferente da última:

```javascript
/**
* @name hidePanelInRepeatablePanel
* @param {scope} globals
*/
function hidePanelInRepeatablePanel(globals)
{    
    var repeatablePanel = globals.form.travelerinfo;
    // hides a panel inside second instance of repeatable panel
    globals.functions.setProperty(repeatablePanel[1].traveler, {visible : false});
}  
```

Neste exemplo, a função personalizada `hidePanelInRepeatablePanel` executa uma ação em uma instância específica do painel repetível. No código acima, `travelerinfo` representa o painel repetível. O código `repeatablePanel[1].traveler, {visible: false}` oculta o painel na segunda instância do painel repetível.

Vamos adicionar um botão rotulado `Hide` e adicionar uma regra para ocultar a segunda instância de um painel repetível.

![Ocultar regra do Painel](/help/forms/assets/custom-function-hidepanel-rule.png)

Consulte o vídeo abaixo para demonstrar que, quando o `Hide` for clicado, o painel na segunda instância repetível ficará oculto:

>[!VIDEO](https://video.tv.adobe.com/v/3429554?quality=12&learn=on)

+++

+++ **Caso de uso**: preencher previamente o campo com um valor quando o formulário for carregado

Adicione a seguinte linha de código, conforme explicado na seção [create-custom-function](#create-custom-function), para carregar o valor pré-preenchido em um campo quando o formulário for inicializado:

```javascript
/**
 * Tests import data
 * @name testImportData
 * @param {scope} globals
 */
function testImportData(globals)
{
    globals.functions.importData(Object.fromEntries([['amount','10000']]));
} 
```

No código mencionado acima, a função `testImportData` preenche o campo de caixa de texto `Booking Amount` quando o formulário é carregado. Vamos supor que o formulário de reserva exige que o valor mínimo de reserva seja `10,000`.

Vamos criar uma regra na inicialização do formulário, em que o valor no campo de caixa de texto `Booking Amount` é preenchido previamente com um valor especificado quando o formulário é carregado:

![Regra de Importação de Dados](/help/forms/assets/custom-function-import-data.png)

Consulte a captura de tela abaixo, que demonstra que, quando o formulário é carregado, o valor na caixa de texto `Booking Amount` é pré-preenchido com um valor especificado:

![Formulário de Regra de Importação de Dados](/help/forms/assets/custom-function-prefill-form.png)

+++

+++ **Caso de uso**: definir foco no campo específico

Adicione a seguinte linha de código, conforme explicado na seção [create-custom-function](#create-custom-function), para definir o foco no campo especificado quando o botão `Submit` for clicado.:

```javascript
/**
 * @name testSetFocus
 * @param {object} emailField
 * @param {scope} globals
 */
    function testSetFocus(field, globals)
    {
        globals.functions.setFocus(field);
    }
```

Vamos adicionar uma regra ao botão `Submit` para definir o foco no campo de caixa de texto `Email ID` quando ele for clicado:

![Definir Regra de Foco](/help/forms/assets/custom-function-set-focus.png)

Consulte a captura de tela abaixo, que demonstra que, quando o botão `Submit` é clicado, o foco é definido no campo `Email ID`:

![Definir Regra de Foco](/help/forms/assets/custom-function-set-focus-form.png)

>[!NOTE]
>
> Você pode usar o parâmetro `$focusOption` opcional se quiser focalizar no campo seguinte ou anterior relativo ao campo `email`.

+++

+++ **Caso de uso**: adicionar ou excluir o painel repetível usando a propriedade `dispatchEvent`

Adicione a seguinte linha de código, conforme explicado na seção [create-custom-function](#create-custom-function), para adicionar um painel quando o botão `Add Traveler` for clicado usando a propriedade `dispatchEvent`:

```javascript
/**
 * Tests add instance with dispatchEvent
 * @name testAddInstance
 * @param {scope} globals
 */
function testAddInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel,'addInstance');
}
```

Vamos adicionar uma regra ao botão `Add Traveler` para adicionar o painel repetível quando ele for clicado:

![Adicionar regra do painel](/help/forms/assets/custom-function-add-panel.png)

Consulte o gif abaixo, que demonstra que, quando o botão `Add Traveler` é clicado, o painel é adicionado usando a propriedade `dispatchEvent`:

![Adicionar Painel](/help/forms/assets/custom-function-add-panel.gif)

Da mesma forma, adicione a seguinte linha de código, como explicado na seção [create-custom-function](#create-custom-function), para excluir um painel quando o botão `Delete Traveler` for clicado usando a propriedade `dispatchEvent`:

```javascript
/**
 
 * @name testRemoveInstance
 * @param {scope} globals
 */
function testRemoveInstance(globals)
{
    var repeatablePanel = globals.form.traveler;
    globals.functions.dispatchEvent(repeatablePanel, 'removeInstance');
} 
```

Vamos adicionar uma regra ao botão `Delete Traveler` para excluir o painel repetível quando ele for clicado:

![Excluir regra do painel](/help/forms/assets/custom-function-delete-panel.png)

Consulte o gif abaixo, que demonstra que, quando o botão `Delete Traveler` é clicado, o painel do viajante é excluído usando a propriedade `dispatchEvent`:

![Excluir Painel](/help/forms/assets/custom-function-delete-panel.gif)

+++

## Suporte de cache para função personalizada

O Forms adaptável implementa o armazenamento em cache de funções personalizadas para melhorar o tempo de resposta ao recuperar a lista de funções personalizadas no editor de regras. Uma mensagem como `Fetched following custom functions list from cache` aparece no arquivo `error.log`.

![função personalizada com suporte a cache](/help/forms/assets/custom-function-cache-error.png)

Caso as funções personalizadas sejam modificadas, o armazenamento em cache é invalidado e é analisado.

## Resolução de problemas {#troubleshooting}

* Se o manipulador de envio personalizado não funcionar conforme esperado em projetos ou formulários AEM existentes, execute as seguintes etapas:
   * Verifique se a versão dos [componentes principais foi atualizada para 3.0.18 e posterior](https://github.com/adobe/aem-core-forms-components). No entanto, para projetos e formulários AEM existentes, há etapas adicionais a seguir:

   * Para o projeto AEM, o usuário deve substituir todas as instâncias de `submitForm('custom:submitSuccess', 'custom:submitError')` por `submitForm()` e implantar o projeto por meio do pipeline do Cloud Manager.

   * Para formulários existentes, se os manipuladores de envio personalizados não estiverem funcionando corretamente, o usuário precisará abrir e salvar a regra `submitForm` no botão **Enviar** usando o Editor de Regras. Esta ação substitui a regra existente de `submitForm('custom:submitSuccess', 'custom:submitError')` por `submitForm()` no formulário.


* Se o arquivo JavaScript que contém o código para funções personalizadas tiver um erro, as funções personalizadas não serão listadas no editor de regras de um Formulário adaptável. Para verificar a lista de funções personalizadas, você pode navegar até o arquivo `error.log` para localizar o erro. No caso de um erro, a lista de funções personalizadas aparece vazia:

  ![arquivo de log de erros](/help/forms/assets/custom-function-list-error-file.png)

  Caso não haja erro, as funções personalizadas são buscadas e aparecem no arquivo `error.log`. Uma mensagem como `Fetched following custom functions list` aparece no arquivo `error.log`:

  ![arquivo de log de erros com a função personalizada adequada](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Considerações

* O `parameter type` e o `return type` não dão suporte a `None`.

* As funções não suportadas na lista de funções personalizadas são:
   * Funções geradoras
   * Funções assíncronas/Await
   * Definições de método
   * Métodos de classe
   * Parâmetros padrão
   * Parâmetros rest

## Consulte também {#see-also}

{{see-also}}


