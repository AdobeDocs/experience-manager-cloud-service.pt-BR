---
title: API para chamar o serviço de Modelo de dados de formulário do Adaptive Forms
description: Explica a API invokeWebServices que você pode usar para chamar serviços da Web escritos em WSDL de dentro de um campo Formulário adaptável.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
source-git-commit: 92f89243b79c6c2377db3ca2b8ea244957416626
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---


# API para chamar o serviço de Modelo de dados de formulário do Adaptive Forms {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Visão geral {#overview}

[!DNL AEM Forms] O permite que os autores de formulários simplifiquem e aprimorem ainda mais a experiência de preenchimento, chamando serviços configurados em um Modelo de dados de formulário de um campo de Formulário adaptável. Para chamar um serviço de modelo de dados, você pode criar uma regra no editor visual ou especificar um JavaScript usando o `guidelib.dataIntegrationUtils.executeOperation` API no editor de código do [editor de regras](rule-editor.md).

Este documento se concentra na gravação de um JavaScript usando o `guidelib.dataIntegrationUtils.executeOperation` API para invocar um serviço.

## Uso da API {#using-the-api}

A variável `guidelib.dataIntegrationUtils.executeOperation` A API chama um serviço de dentro de um campo de Formulário adaptável. A sintaxe da API é a seguinte:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

A estrutura do `guidelib.dataIntegrationUtils.executeOperation` A API especifica detalhes sobre a operação do serviço. A sintaxe da estrutura é a seguinte:

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

A estrutura da API especifica os seguintes detalhes sobre a operação de serviço.

<table>
 <tbody>
  <tr>
   <th>Parâmetro</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>Estrutura para especificar o identificador do modelo de dados de formulário, o título da operação e o nome da operação</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Especifica o caminho do repositório para o modelo de dados de formulário, incluindo seu nome</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Especifica o nome da operação de serviço a ser executada</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>Mapeia um ou mais objetos de formulário para os argumentos de entrada da operação de serviço</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Mapeia um ou mais objetos de formulário para valores de saída da operação de serviço a fim de preencher campos de formulário<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Retorna valores com base nos argumentos de entrada da operação de serviço. É um parâmetro opcional usado como uma função de retorno de chamada.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Exibe uma mensagem de erro se a função de retorno de chamada bem-sucedida falhar ao exibir os valores de saída com base nos argumentos de entrada. É um parâmetro opcional usado como uma função de retorno de chamada.<br /> </td>
  </tr>
 </tbody>
</table>

## Exemplo de script para chamar um serviço {#sample-script-to-invoke-a-service}

O exemplo de script a seguir usa o `guidelib.dataIntegrationUtils.executeOperation` API para invocar o `getAccountById` operação de serviço configurada no `employeeAccount` modelo de dados de formulário.

A variável `getAccountById` A operação utiliza o valor no `employeeID` campo de formulário como entrada para o `empId` argumento e retorna o nome, o número e o saldo da conta do funcionário correspondente. Os valores de saída são preenchidos nos campos de formulário especificados. Por exemplo, o valor em `name` O argumento é preenchido na variável `fullName` elemento de formulário e valor para `accountNumber` argumento em `account` elemento de formulário.

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## Uso da API com função de retorno de chamada {#using-the-api-callback}

Você também pode chamar o serviço de Modelo de dados de formulário usando o `guidelib.dataIntegrationUtils.executeOperation` API com uma função de retorno de chamada. A sintaxe da API é a seguinte:

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

A função de retorno de chamada pode ter `success` e `failure` funções de retorno de chamada.

### Exemplo de script com funções de retorno de chamada de sucesso e falha {#callback-function-success-failure}

O exemplo de script a seguir usa o `guidelib.dataIntegrationUtils.executeOperation` API para invocar o `GETOrder` operação de serviço configurada no `employeeOrder` modelo de dados de formulário.

A variável `GETOrder` A operação utiliza o valor no `Order ID` campo de formulário como entrada para o `orderId` argumento e retorna o valor da quantidade da ordem no `success` função de retorno de chamada.  Se a variável `success` a função de retorno de chamada não retornar a quantidade da ordem, a variável `failure` a função de retorno de chamada exibe a variável `Error occured` mensagem.

>[!NOTE]
>
> Se você usar o `success` função de retorno de chamada, os valores de saída não serão preenchidos nos campos de formulário especificados.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
