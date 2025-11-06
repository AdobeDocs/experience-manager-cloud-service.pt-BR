---
title: Este artigo descreve vários casos de uso para uma função personalizada em um formulário adaptável com base nos componentes principais.
description: O artigo descreve vários casos de uso para uma função personalizada em um formulário adaptável com base nos componentes principais. As funções personalizadas são usadas no editor de regras para criar regras personalizadas para o formulário.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: df92b91e-f3b0-4a08-bd40-e99edc9a50a5
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 0%

---

# Exemplos de desenvolvimento e uso de função personalizada

O artigo fornece exemplos detalhados de funções personalizadas para um Formulário adaptável com base em componentes principais, oferecendo insights valiosos sobre sua implementação eficaz em vários cenários. As funções personalizadas são usadas no editor de regras de uma AEM Forms, permitindo que os desenvolvedores definam e controlem a lógica que governa o comportamento do formulário.
Este artigo explora diferentes implementações de funções personalizadas, mostrando como elas podem ser usadas para adaptar formulários para atender a requisitos específicos e aprimorar a funcionalidade geral.

## Preencher as opções da lista suspensa usando funções personalizadas

O Editor de Regras nos Componentes Principais não oferece suporte à propriedade **Definir Opções** para preencher opções de lista suspensa dinamicamente em tempo de execução. No entanto, é possível preencher opções de lista suspensa usando funções personalizadas, que permitem recuperar opções com base em uma lógica específica. As funções personalizadas fornecem maior flexibilidade e controle sobre como e quando as opções suspensas são preenchidas, melhorando a experiência do usuário.

Para preencher as opções da lista suspensa usando uma função personalizada, adicione o seguinte código, conforme descrito na seção [create-custom-function](/help/forms/custom-function-core-component-create-function.md):


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

## Mostrar um painel usando a regra `SetProperty`

Saiba como as funções personalizadas usam campos e objetos globais com a ajuda de um formulário `Contact Us`.

![Formulário Contate-nos](/help/forms/assets/contact-us-form.png)

Adicione o seguinte código na função personalizada, como explicado na seção [create-custom-function](/help/forms/custom-function-core-component-create-function.md), para definir o campo de formulário como `Required`.

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

## Validar o campo

Saiba como as funções personalizadas usam campos e objetos globais para validar o campo com a ajuda de um formulário `Contact Us`.

Adicione o seguinte código na função personalizada conforme explicado na seção [create-custom-function](/help/forms/custom-function-core-component-create-function.md) para validar o campo.

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

## Redefinir um painel

Saiba como as funções personalizadas usam campos e objetos globais para redefinir o campo com a ajuda de um formulário `Contact Us`.

Adicione o seguinte código na função personalizada, como explicado na seção [create-custom-function](/help/forms/custom-function-core-component-create-function.md), para redefinir o painel.

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

## Para exibir uma mensagem personalizada no nível do campo e marcar o campo como inválido

Saiba como as funções personalizadas usam campos e objetos globais para exibir uma mensagem personalizada no nível do campo e marcar o campo como inválido com a ajuda de um formulário `Contact Us`.

Você pode usar a função `markFieldAsInvalid()` para definir um campo como inválido e definir uma mensagem de erro personalizada em nível de campo. O valor `fieldIdentifier` pode ser `fieldId`, `field qualifiedName` ou `field dataRef`. O valor do objeto nomeado `option` pode ser `{useId: true}`, `{useQualifiedName: true}` ou `{useDataRef: true}`.
As sintaxes usadas para marcar um campo como inválido e definir uma mensagem personalizada são:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Adicione o seguinte código na função personalizada conforme explicado na seção [create-custom-function](/help/forms/custom-function-core-component-create-function.md) para habilitar uma mensagem personalizada no nível do campo.

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

## Enviar dados alterados para o servidor

Saiba como as funções personalizadas usam campos e objetos globais para enviar dados manipulados no servidor com a ajuda de um formulário `Contact Us`.

A seguinte linha de código:
`globals.functions.submitForm(globals.functions.exportData(), false);` é usado para enviar os dados do formulário após manipulação.

* O primeiro argumento diz respeito aos dados a apresentar.
* O segundo argumento representa se o formulário deve ser validado antes do envio. Ele é `optional` e definido como `true` por padrão.
* O terceiro argumento é o `contentType` do envio, que também é opcional com o valor padrão como `multipart/form-data`. Os outros valores podem ser `application/json` e `application/x-www-form-urlencoded`.

Adicione o seguinte código na função personalizada, conforme explicado na seção [create-custom-function](/help/forms/custom-function-core-component-create-function.md), para enviar os dados manipulados no servidor:

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

![Inspecionar dados na janela do console](/help/forms/assets/custom-function-submit-data-console-data.png)

## Substituir manipuladores de erros e de sucesso no envio do formulário

Saiba como as funções personalizadas usam campos e objetos globais para substituir manipuladores de envio com a ajuda de um formulário `Contact Us`.

Adicione a seguinte linha de código, conforme explicado na seção [create-custom-functions](/help/forms/custom-function-core-component-create-function.md), para personalizar a mensagem de envio ou de falha para envios de formulários e exibir as mensagens de envio de formulários em uma caixa modal:

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

Caso o manipulador de envio personalizado não seja executado conforme esperado em projetos ou formulários do AEM existentes, consulte a seção [solução de problemas](#troubleshooting).

## Executar ações em uma instância específica do painel repetível

As regras criadas usando o editor visual de regras em um painel repetível se aplicam à última instância do painel repetível. Para escrever uma regra para uma instância específica do painel repetível, podemos usar uma função personalizada.

Vamos criar outro formulário como `Booking Form` para coletar informações sobre viajantes que vão para um destino. Um painel de viagem é adicionado como um painel repetível, em que o usuário pode adicionar detalhes para 5 viajantes usando o botão `Add Traveler`.

![Informações do viajante](/help/forms/assets/traveler-info-form.png)

Adicione a seguinte linha de código, conforme explicado na seção [create-custom-function](/help/forms/custom-function-core-component-create-function.md), para executar ações em uma instância específica do painel repetível, diferente da última:

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

## Preencha previamente o campo com um valor quando o formulário for carregado

Saiba como as funções personalizadas usam campos e objetos globais para preencher previamente campos com a ajuda de um `Booking Form`.

Adicione a seguinte linha de código, conforme explicado na seção [create-custom-function](/help/forms/custom-function-core-component-create-function.md), para carregar o valor pré-preenchido em um campo quando o formulário for inicializado:

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

## Definir foco no campo específico

Saiba como as funções personalizadas usam campos e objetos globais para definir o foco em um campo específico com a ajuda de um `Booking Form`.

Adicione a seguinte linha de código, conforme explicado na seção [create-custom-function](/help/forms/custom-function-core-component-create-function.md), para definir o foco no campo especificado quando o botão `Submit` for clicado.:

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

## Adicionar ou excluir o painel repetível usando a propriedade `dispatchEvent`

Saiba como as funções personalizadas usam campos e objetos globais para adicionar ou excluir o painel repetível usando a propriedade `dispatchEvent` com a ajuda de um `Booking Form`.

Adicione a seguinte linha de código, conforme explicado na seção [create-custom-function](/help/forms/custom-function-core-component-create-function.md), para adicionar um painel quando o botão `Add Traveler` for clicado usando a propriedade `dispatchEvent`:

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

## Problema conhecido

* As funções personalizadas não suportam literais de expressão regular do JavaScript. O uso de literais regex em uma função personalizada resulta em erros durante a execução. Por exemplo:
  `const pattern = /^abc$/;`

  Para garantir a compatibilidade, use o construtor RegExp nas funções personalizadas.

  `const pattern = new RegExp("^abc$");`
Refatore expressões regulares para usar o construtor RegExp para garantir uma execução consistente e confiável.

## Resolução de problemas

* Se o manipulador de envio personalizado não funcionar conforme esperado em projetos ou formulários do AEM existentes, execute as seguintes etapas:
   * Verifique se a versão dos [componentes principais foi atualizada para 3.0.18 e posterior](https://github.com/adobe/aem-core-forms-components). No entanto, para projetos e formulários existentes do AEM, há etapas adicionais a seguir:

   * Para o projeto do AEM, o usuário deve substituir todas as instâncias de `submitForm('custom:submitSuccess', 'custom:submitError')` por `submitForm()` e implantar o projeto por meio do pipeline do Cloud Manager.

   * Para formulários existentes, se os manipuladores de envio personalizados não estiverem funcionando corretamente, o usuário precisará abrir e salvar a regra `submitForm` no botão **Enviar** usando o Editor de Regras. Esta ação substitui a regra existente de `submitForm('custom:submitSuccess', 'custom:submitError')` por `submitForm()` no formulário.

## Consulte também

{{see-also-rule-editor}}
