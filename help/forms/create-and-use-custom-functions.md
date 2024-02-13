---
title: Criar e adicionar funções personalizadas em um Formulário adaptável
description: O AEM Forms é compatível com funções personalizadas que permitem aos usuários criar e usar suas próprias funções no editor de regras.
keywords: Adicionar uma função personalizada, usar uma função personalizada, criar uma função personalizada, usar a função personalizada no editor de regras.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
source-git-commit: 94a290964a92f8c6ed353d9c77f3dd3b8a5598a4
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 0%

---


# Funções personalizadas no Adaptive Forms (Componentes principais)

## Introdução

O AEM Forms é compatível com funções personalizadas, permitindo que os usuários definam funções JavaScript para implementar regras de negócios complexas. Essas funções personalizadas estendem os recursos dos formulários facilitando a manipulação e o processamento dos dados inseridos para atender a requisitos especificados. Elas também permitem a alteração dinâmica do comportamento do formulário com base em critérios predefinidos.
No Adaptive Forms, é possível usar funções personalizadas na [editor de regras de um Formulário adaptável](/help/forms/rule-editor.md#custom-functions) para criar regras de validação específicas para campos de formulário.

Vamos entender o uso da função personalizada em que os usuários inserem o endereço de email e você deseja garantir que o endereço de email inserido siga um formato específico (ele contém um símbolo &quot;@&quot; e um nome de domínio). Crie uma função personalizada como &quot;ValidateEmail&quot; que assume o endereço de email como entrada e retorna true se for válido, caso contrário, retorna false.

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

No exemplo acima, quando o usuário tenta enviar o formulário, a função personalizada &quot;ValidateEmail&quot; é invocada para verificar se o endereço de email inserido é válido.

### Usos de funções personalizadas {#uses-of-custom-function}

Algumas das vantagens de usar funções personalizadas no Adaptive Forms são:

* **Manipulação de dados**: as funções personalizadas manipulam e processam os dados inseridos nos campos de formulários.
* **Validação de dados**: As funções personalizadas permitem que você execute verificações personalizadas nas entradas do formulário e forneça mensagens de erro especificadas.
* **Comportamento dinâmico**: as funções personalizadas permitem controlar o comportamento dinâmico dos formulários com base em condições específicas. Por exemplo, você pode mostrar/ocultar campos, modificar valores de campo ou ajustar a lógica do formulário dinamicamente.
* **Integração**: você pode usar funções personalizadas para integrar-se a APIs ou serviços externos. Ele ajuda a buscar dados de fontes externas, enviar dados para endpoints Rest externos ou executar ações personalizadas com base em eventos externos.

## Considerações ao criar funções personalizadas {#considerations}

Para listar as funções personalizadas no editor de regras, é possível declará-las em qualquer um dos seguintes formatos:

* **Instrução Function com ou sem comentários jsdoc**

Você pode criar uma função personalizada com ou sem comentários jsdoc.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```

* **Função de seta com comentário jsdoc obrigatório**

Alguns exemplos para criar funções de Seta são:

```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} a some parameter description
    * @param {string} b another parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
```

<!-- 
    * @param {string=} b another parameter description
      /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;-->

* **Expressão de função com comentário jsdoc obrigatório**

Crie funções personalizadas nos seguintes formatos para listá-las no editor de regras de um Formulário adaptável. Por exemplo:

```javascript
    /**
    * test function
    * @name testFunction test function
    * @param {string} input1 parameter description
    * @param {string} input2 another parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

<!--
* @param {string=} input2 another parameter description
The functions that are not supported in the custom function list are:
* Generator functions
* Async/Await functions 
* Method definitions
* Class methods
* Default parameters
* Rest parameters -->

>[!NOTE]
>
> Você pode verificar o `error.log` arquivo em caso de erros, como funções personalizadas, não são listadas no editor de regras.

<!--The `error.log` file also displays the methods and parameters that are not supported for custom functions. -->


## Criar uma função personalizada {#create-custom-function}

Crie uma biblioteca do cliente para chamar funções personalizadas no editor de regras. Para obter mais informações, consulte [Uso de bibliotecas do lado do cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).

As etapas para criar funções personalizadas são:
1. [Criar uma biblioteca do cliente](#create-client-library)
1. [Adicionar biblioteca do cliente em um Formulário adaptável](#use-custom-function)

### Criar uma biblioteca do cliente {#create-client-library}

Você pode adicionar funções personalizadas adicionando a biblioteca do cliente. Para criar uma biblioteca do cliente, execute as seguintes etapas:

1. [Clonar o repositório as a Cloud Service do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).
1. Crie uma pasta em `[AEM Forms as a Cloud Service repository folder]/apps/` pasta. Por exemplo, crie uma pasta chamada como `experience-league`
1. Navegue até `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` e criar um `ClientLibraryFolder` as `es6clientlibs`.
1. Adicionar uma propriedade do `categories`com valor de tipo de string como `es6customfunctions` para o `es6clientlibs` pasta.

   >[!NOTE]
   >
   >`es6customfunctions`é uma categoria de exemplo. Você pode escolher qualquer nome para a categoria.

1. Crie uma pasta chamada `js`.
1. Navegue até a `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/es6clientlibs/js` pasta.
1. Adicione um arquivo JavaScript, por exemplo, `function.js`. O arquivo é composto pelo código da função personalizada.

   >[!NOTE]
   >
   >* Se o arquivo JavaScript que contém o código para funções personalizadas tiver um erro, as funções personalizadas não serão listadas no editor de regras de um Formulário adaptável. Você também pode verificar o `error.log` para o erro.

   <!-- 
    >* AEM Adaptive Form supports the caching of custom functions. If the JavaScript is modified, the caching becomes invalidated, and it is parsed. You can see a message as `Fetched following custom functions list from cache` in the `error.log` file.  -->

1. Salve o `function.js` arquivo.
1. Navegue até a `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/es6clientlibs/js` pasta.
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

1. [Execute o pipeline.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline)

Depois que o pipeline for executado com êxito, a função personalizada adicionada à biblioteca do cliente ficará disponível no [Editor de regras do Formulário adaptável](/help/forms/rule-editor.md).

### Adicionar biblioteca do cliente em um Formulário adaptável{#use-custom-function}

Depois de adicionar a biblioteca do cliente, use-a no Formulário adaptável. Ele permite que você use seu [função personalizada como uma regra no seu formulário](/help/forms/rule-editor.md#custom-functions). Para adicionar a biblioteca do cliente no formulário adaptável, execute as seguintes etapas:

1. Abra o formulário no modo de edição.
Para abrir um formulário no modo de edição, selecione um formulário e **[!UICONTROL Abertura]**.
1. No modo de edição, selecione um componente e selecione ![nível de campo](assets/select_parent_icon.svg) > **[!UICONTROL Contêiner de formulário adaptável]** e selecione ![cmppr](assets/configure-icon.svg).
1. Na barra lateral, em Nome da biblioteca do cliente, adicione a biblioteca do cliente. ( `es6customfunctions` no exemplo.)

   ![Adição da biblioteca de cliente de função personalizada](/help/forms/assets/clientlib-custom-function.png)

Crie uma regra para usar a função personalizada no editor de regras.

<!--

### Support for the optional parameters in custom functions{#support-for-optional-parameter}

AEM supports including optional parameters in JSDocs. These parameters are displayed as optional in the rule editor. There are two ways to add optional parameters in JSDocs:
*  `@param {string=abc} b -- some description for b which is optional`

    In the above line of code, `b` is an optional parameter with the default value set to `abc`. 
    Alternatively, you can define `b` as an optional parameter without assigning any default value as `@param {string=} b -- some description for b which is optional`

* `@param {array} [z=[def,xyz]] - - some description for z which is optional`

    In the above line of code, `z` is an optional parameter of array type with the default value set to `[def , xyz]`. 
    Alternatively, you can define `z` as an optional parameter without assigning any default value as `@param {array} [z=] - - some description for z which is optional`

>[!NOTE]
>
> Ensure that the parameter name is enclosed in square brackets [] and the parameter type is enclosed in curly brackets {}. 

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

In the rule editor of an Adaptive Form, the parameters are displayed as `required`. By default the parameters are `required`, if not defined as optional in JSDocs.

  ![Optional or required parameters](/help/forms/assets/optional-default-params.png) 

  You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

  ![incomplete rule warning message](/help/forms/assets/incomplete-rule.png) 
  
  The rule is executed even if you do not specify a value for optional parameters. Undefined values are passed for optional parameters on executing the rule.

  ### Support for field and globals objects in custom functions {#support-field-and-global-objects}

  needs to be discussed

  -->

## Consulte também {#see-also}

{{see-also}}





