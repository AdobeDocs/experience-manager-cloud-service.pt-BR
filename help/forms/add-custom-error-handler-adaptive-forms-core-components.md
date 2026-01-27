---
title: Adicionar um manipulador de erros personalizado no Adaptive Forms com base nos Componentes principais do AEM Adaptive Forms
description: O AEM Forms fornece manipuladores de sucesso e erro prontos para uso para um formulário usando o endpoint REST configurado para chamar um serviço externo. Você pode adicionar um manipulador de erros padrão e um manipulador de erros personalizado em um Formulário adaptável do AEM.
keywords: Adicionar um manipulador de erros personalizado, adicionar um manipulador de erros padrão, adicionar um manipulador de erros no formulário, usar o serviço de chamada do editor de regras para adicionar um manipulador de erros personalizado, configurar o editor de regras para adicionar um manipulador de erros personalizado, adicionar manipulador de erros personalizado usando o editor de regras
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: 4496c4cc-a5d7-4f34-91f9-13eded77b362
role: User, Developer
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '2319'
ht-degree: 1%

---

# Manipuladores de erros para o formulário adaptável com base nos Componentes principais {#error-handlers-in-adaptive-form}


| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Este artigo |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/add-custom-error-handler-adaptive-forms-core-components.html) |

O AEM Forms fornece manipuladores de sucesso e erro prontos para uso para envios de formulários. Ele também fornece recursos para personalizar funções do manipulador de erros. Por exemplo, você pode chamar um fluxo de trabalho personalizado no backend para códigos de erro específicos ou informar ao cliente que o serviço está inativo. Os manipuladores são funções do lado do cliente executadas com base na resposta do servidor. Quando um serviço externo é chamado usando APIs, os dados são transmitidos ao servidor para validação, o que retorna uma resposta ao cliente com informações sobre o evento bem-sucedido ou com erro para o envio. As informações são passadas como parâmetros para o manipulador relevante para executar a função. Um manipulador de erros ajuda a gerenciar e exibir erros ou problemas de validação encontrados.

![fluxo de trabalho do manipulador de erros para entender como adicionar um manipulador de erros personalizado em formulários](/help/forms/assets/error-handler-workflow.png)

O Formulário adaptável valida as entradas que você fornece nos campos com base em critérios de validação predefinidos e verifica vários erros retornados pelo endpoint REST configurado para chamar um serviço externo. Você pode definir os critérios de validação com base na fonte de dados usada com o Formulário adaptável. Por exemplo, se você usar os serviços Web RESTful como fonte de dados, poderá definir os critérios de validação em um arquivo de definição do Swagger.

Se os valores de entrada atenderem aos critérios de validação, os valores serão enviados para a fonte de dados ou então, o Formulário adaptável exibirá uma mensagem de erro usando um manipulador de erros. Semelhante a essa abordagem, o Adaptive Forms é integrado a manipuladores de erro personalizados para executar validações de dados. Se os valores de entrada não atenderem aos critérios de validação, as mensagens de erro serão exibidas em nível de campo no Formulário adaptável. Isso ocorre quando a mensagem de erro de validação retornada pelo servidor está no formato de mensagem padrão.


## Usos de manipuladores de erros {#uses-of-error-handler}

Os manipuladores de erros são usados para vários propósitos. Alguns dos usos das funções do manipulador de erros estão listados abaixo:

* **Executar validação**: o tratamento de erros começa com a validação das entradas do usuário em relação a regras ou critérios predefinidos. À medida que os usuários preenchem um Formulário adaptável, o manipulador de erros valida a entrada para garantir que ela atenda ao formato, ao comprimento ou a qualquer outra restrição necessária.

* **Fornecer feedback em tempo real**: quando qualquer erro é detectado, o manipulador de erros exibe feedback imediato ao usuário, como mensagens de erro em linha abaixo dos campos de formulário correspondentes. Este feedback ajuda os usuários a identificar e corrigir erros sem precisar enviar o formulário e aguardar uma resposta.


* **Exibir mensagens de erro**: quando um envio de Formulário Adaptável encontra qualquer erro de validação, o manipulador de erros exibe uma mensagem de erro apropriada. As mensagens de erro devem ser claras, concisas e destacar os campos específicos que exigem atenção.

* **Realça o campo incorreto**: para chamar a atenção do usuário para campos incorretos específicos, o manipulador de erros realça ou diferencia visualmente os campos correspondentes. Ela é executada alterando a cor do plano de fundo, adicionando um ícone ou uma borda ou qualquer outra dica visual que ajude os usuários a localizar e corrigir os erros rapidamente.


## Formato de resposta de falha/erro {#failure-response-format}

Um Formulário adaptável exibe os erros em um nível de campo se as mensagens de erro de validação do servidor estiverem no seguinte formato padrão.
O código abaixo ilustra a estrutura de resposta de falha existente:

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


Em que:

* `errorCausedBy` descreve o motivo da falha.
* `errors` mencione a expressão dos campos que falharam nos critérios de validação junto com a mensagem de erro de validação.
* O campo `originCode` foi adicionado pelo AEM e contém o código de status http retornado pelo serviço externo.
* O campo `originMessage` foi adicionado pelo AEM e contém os dados brutos de erro retornados pelo serviço externo.

Com as melhorias nos recursos e atualizações subsequentes nas versões do AEM Forms, a estrutura de resposta a falhas existente mudou para um novo formato com base no RFC7807, que é compatível com versões anteriores com a estrutura de resposta a falhas existente:

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<qualified fieldname of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * Verifique se a estrutura de resposta de erro inclui **fieldName** ou **dataRef**.
> * Verifique se o cabeçalho **ContentType** é **application/problem+json**.

Em que:

* `type (required)` especifica o tipo de falha. Pode ser um dos seguintes valores:
   * `SERVER_SIDE_VALIDATION` indica uma falha devido à validação do lado do servidor.
   * `FORM_SUBMISSION` indica uma falha durante o envio do formulário
   * `SERVICE_INVOCATION` indica uma falha durante uma invocação de serviço de terceiros.
   * `FAILURE` indica uma falha geral.
   * `VALIDATION_ERROR` indica uma falha devido a um erro de validação.

* `title (optional)` fornece um título ou uma breve descrição da falha.
* `detail (optional)` fornece detalhes adicionais sobre a falha, se necessário.
* `instance (optional)` representa uma instância ou um identificador associado à falha e ajuda a rastrear ou identificar a ocorrência específica da falha.
* `validationErrors (required)` contém informações sobre erros de validação. Inclui os seguintes campos:
   * `fieldname` menciona o nome de campo qualificado dos campos que falharam nos critérios de validação.
   * `dataRef` representa o caminho JSON ou XPath dos campos que falharam na validação.
   * `details` contém a mensagem de erro de validação com o campo incorreto.
* Campo `originCode (optional)` adicionado pelo AEM e contém o código de status http retornado pelo serviço externo
* O campo `originMessage (optional)` foi adicionado pelo AEM e contém os dados brutos de erro retornados pelo serviço externo.

### Formato de resposta de erro de exemplo {#sample-error-response-format}

Algumas das opções para exibir as respostas de erro são:

+++  Com base na propriedade fieldName do Formulário adaptável


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "$form.PetId",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```

+++


+++ Com base na propriedade Referência de vinculação de formulário adaptável

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
      {
          "type": "VALIDATION_ERROR",
          "validationErrors": [
          {
              "fieldName": "",
              "dataRef": "$.Pet.id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

Você pode exibir o valor de dataRef na janela **[!UICONTROL Propriedades]** de um componente de formulário.

+++

## Requisitos para adicionar manipulador de erros usando o serviço Chamar do Editor de regras {#before-you-start-to-add-error-handler}

Antes de adicionar um manipulador de erros usando o serviço Chamar do Editor de regras:

* Saiba como [criar funções personalizadas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#write-rules).


## Adicionar manipulador de erros usando o Editor de regras {#add-error-handler-using-rule-editor}

Usando a ação Chamar serviço[&#x200B; do &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html#invoke)Editor de regras, você define os critérios de validação com base na fonte de dados usada com o Formulário adaptável. Caso você use os serviços Web RESTful como fonte de dados, é possível definir os critérios de validação em um arquivo de definição do Swagger. Ao usar as funções do manipulador de erros e o Editor de regras no Adaptive Forms, você pode gerenciar e personalizar com eficiência a manipulação de erros. Você define as condições usando o Editor de regras e configura as ações desejadas a serem executadas quando a regra for acionada. O Formulário adaptável valida as entradas inseridas nos campos com base em critérios de validação predefinidos. Caso os valores de entrada não atendam aos critérios de validação, as mensagens de erro serão exibidas no nível do campo em um Formulário adaptável.

>[!NOTE]
>
> * Para usar manipuladores de erros com a ação de serviço Chamar do Editor de regras, configure o Adaptive Forms com um modelo de dados de formulário (FDM).
> * Um manipulador de erros padrão é fornecido para exibir mensagens de erro nos campos se a resposta do erro estiver no esquema padrão. Você também pode chamar o manipulador de erros padrão da função de manipulador de erros personalizado.

Usando o Editor de regras, você pode:

* [Adicionar função de manipulador de erros padrão](#add-default-errror-handler)
* [Adicionar função de manipulador de erro personalizada](#add-custom-errror-handler)


### Adicionar função de manipulador de erros padrão {#add-default-errror-handler}

Um manipulador de erros padrão é compatível com a exibição de mensagens de erro em campos se a resposta do erro estiver no esquema padrão ou na falha de validação do lado do servidor.
Para entender como usar um manipulador de erros padrão usando a ação Chamar serviço[&#x200B; do &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#invoke)Editor de regras, use um exemplo de um Formulário adaptável simples com dois campos, **ID de animal de estimação** e **Nome de animal de estimação** e use um manipulador de erros padrão no campo **ID de animal de estimação** para verificar vários erros retornados pelo ponto de extremidade REST configurado para chamar um serviço externo, por exemplo, `200 - OK`,`404 - Not Found`, `400 - Bad Request`. Para adicionar um manipulador de erros padrão usando a ação Chamar serviço do Editor de regras, execute as seguintes etapas:

1. Abra um Formulário adaptável no modo de criação, selecione um componente de formulário e selecione **[!UICONTROL Editor de regras]** para abrir o editor de regras.
1. Selecione **[!UICONTROL Criar]**.
1. Crie uma condição na seção **When** da regra. Por exemplo, **Quando[O campo Nome da ID do animal de estimação]** é alterado. A seleção foi alterada na lista suspensa **Selecionar estado**.
1. Na seção **Then**, selecione **[!UICONTROL Invocar Serviço]** na lista suspensa **Selecionar Ação**.
1. Selecione um **Serviço de postagem** e suas associações de dados correspondentes na seção **Entrada**. Por exemplo, para validar a **ID do Pet**, selecione um **Serviço de postagem** como **GET /pet/{petId}** e selecione **ID do Pet** na seção **Entrada**.
1. Selecione as associações de dados na seção **Saída**. Selecione o **Nome do Animal** na seção **Saída**.
1. Selecione **[!UICONTROL Manipulador de Erros Padrão]** na seção **Manipulador de Erros**.
1. Clique em **[!UICONTROL Concluído]**.

![adicionar um manipulador de erros padrão para verificações de validação de campo em um formulário](/help/forms/assets/default-error-handler.png)

Como resultado desta regra, os valores inseridos para **ID do Pet** verificam a validação para **Nome do Pet** usando o serviço externo chamado pelo ponto de extremidade REST. Se os critérios de validação com base na fonte de dados falharem, as mensagens de erro serão exibidas no nível do campo.

![exibir a mensagem de erro padrão ao adicionar um manipulador de erro padrão em um formulário para tratar respostas de erro](/help/forms/assets/default-error-message.png)

### Adicionar função de manipulador de erro personalizada {#add-custom-errror-handler}

Você pode adicionar uma função de manipulador de erros personalizada para executar algumas das ações, como:

* lidam com respostas de erro que usam respostas de erro não padrão ou padrão. É importante observar que essas respostas de erro não padrão não estão em conformidade com o [esquema padrão de respostas de erro](#failure-response-format).
* envie eventos do analytics para qualquer plataforma do analytics. Por exemplo, Adobe Analytics.
* exibir caixa de diálogo modal com mensagens de erro.

Além das ações mencionadas, os manipuladores de erros personalizados podem ser usados para executar funções personalizadas que atendam a requisitos específicos do usuário.

O manipulador de erros personalizado é uma função (Biblioteca do cliente) criada para responder aos erros retornados por um serviço externo e fornecer uma resposta personalizada aos usuários finais. Qualquer Biblioteca de Cliente com anotação `@errorHandler` é considerada uma função de manipulador de erro personalizada. Esta anotação ajuda a identificar a função do manipulador de erros especificada no arquivo `.js`.
Para entender como criar e usar um manipulador de erros personalizado usando a ação [Chamar serviço](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#invoke) do Editor de regras, vamos ver um exemplo de Formulário adaptável com dois campos, **Pet ID** e **Pet Name**, e usar um manipulador de erros personalizado no campo **Pet ID** para verificar vários erros retornados pelo ponto de extremidade REST configurado para invocar um serviço externo, por exemplo, `200 - OK`,`404 - Not Found`, `400 - Bad Request`.

Para adicionar e usar um manipulador de erros personalizado em um Formulário adaptável, execute as seguintes etapas:

1. [Criar um manipulador de erros personalizado](#create-custom-error-message)
1. [Usar o Editor de regras para configurar o manipulador de erros personalizado](#use-custom-error-handler)

#### &#x200B;1. Criar um manipulador de erros personalizado {#create-custom-error-message}

Para criar uma função de erro personalizada, execute as seguintes etapas:

Para criar uma função de erro personalizada, execute as seguintes etapas:

1. [Clonar o Repositório as a Cloud Service do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).
1. Crie uma pasta na pasta `[AEM Forms as a Cloud Service repository folder]/apps/`. Por exemplo, crie uma pasta chamada `experience-league`
1. Navegue até `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/experience-league/` e crie um `ClientLibraryFolder` como `clientlibs`.
1. Crie uma pasta chamada `js`.
1. Navegue até a pasta `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js`.
1. Adicione um arquivo JavaScript, por exemplo, `function.js`. O arquivo compreende o código do manipulador de erros personalizado.
Vamos adicionar o seguinte código ao arquivo JavaScript para exibir a resposta e os cabeçalhos, recebidos do ponto de extremidade do serviço REST, no console do navegador.

   ```javascript
       /** 
       Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers, globals)
   {
       console.log("Custom Error Handler processing start...");
       console.log("response:"+JSON.stringify(response));
       console.log("headers:"+JSON.stringify(headers));
       alert("CustomErrorHandler - Enter valid PetId.")
       console.log("Custom Error Handler processing end...");
       return true; // true - call default error handler, false - don't call default error handler.
   }
   ```

   No código acima, `return true` invoca o manipulador de erros padrão automaticamente. Para evitar que o manipulador de erros padrão seja chamado por padrão, inclua `return false`.

   >[!NOTE]
   >
   > No arquivo `.content.xml`, adicione `categories = [custom-errorhandler-name]`. Por exemplo, neste caso, [custom-errorhandler-name] é fornecido como `customfunctionsdemoV2`.


1. Salve o arquivo `function.js`.
1. Navegue até a pasta `[AEM Forms as a Cloud Service repository folder]/apps/[AEM Project Folder]/clientlibs/js`.
1. Adicione um arquivo de texto como `js.txt`. O arquivo contém:

   ```javascript
       #base=js
       functions.js
   ```

1. Salve o arquivo `js.txt`.\
   A estrutura de pastas criada é semelhante a:

   ![Estrutura da pasta de biblioteca do cliente criada](/help/forms/assets/customclientlibrary_folderstructure.png)

   >[!NOTE]
   >
   > Para saber mais sobre como criar funções personalizadas, clique em [funções personalizadas no Editor de Regras](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html?lang=en#write-rules).


1. Adicione, confirme e envie as alterações no repositório usando os comandos abaixo:

   ```javascript
       git add .
       git commit -a -m "Adding error handling files"
       git push
   ```

1. [Executar o pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline).

Depois que o pipeline é executado com êxito, o manipulador de erros personalizado fica disponível em seu editor de regras do Formulário adaptável. Agora, vamos entender como configurar e usar um manipulador de erros personalizado usando o serviço Chamar do editor de regras no AEM Forms.

#### &#x200B;2. Use o Editor de regras para configurar o manipulador de erros personalizado {#use-custom-error-handler}

Antes de implementar o manipulador de erros personalizado em um Formulário adaptável, verifique se o nome da biblioteca do cliente na **[!UICONTROL Categoria da biblioteca do cliente]** está alinhado com o nome especificado na opção de categorias do arquivo `.content.xml`.

![Adicionando o nome da biblioteca do cliente na configuração do Contêiner de Formulário Adaptável](/help/forms/assets/client-library-category-name-core-component.png)

Para usar um manipulador de erros personalizado usando a ação **[!UICONTROL Chamar serviço]** do Editor de regras:

1. Abra um Formulário adaptável no modo de criação, selecione um componente de formulário e selecione **[!UICONTROL Editor de regras]** para abrir o editor de regras.
1. Selecione **[!UICONTROL Criar]**.
1. Crie uma condição na seção **When** da regra. Por exemplo, Quando o **[Nome do campo de ID do Pet]** for alterado, selecione **foi alterado** na lista suspensa **Selecionar Estado**.
1. Na seção **Then**, selecione **[!UICONTROL Invocar Serviço]** na lista suspensa **Selecionar Ação**.
1. Selecione um **Serviço de postagem** e suas associações de dados correspondentes na seção **Entrada**. Por exemplo, para validar a **ID do Pet**, selecione um **Serviço de postagem** como **GET /pet/{petId}** e selecione **ID do Pet** na seção **Entrada**.
1. Selecione as associações de dados na seção **Saída**. Por exemplo, selecione **Nome do animal de estimação** na seção **Saída**.
1. Selecione **[!UICONTROL Manipulador de Erros Personalizado]** na seção **[!UICONTROL Manipulador de Erros]**.
1. Clique em **[!UICONTROL Concluído]**.

![adicionar manipulador de erros personalizado em um formulário para manipular respostas de erros](/help/forms/assets/custom-error-handler.png)s


Como resultado desta regra, os valores inseridos para **ID do Pet** verificam a validação para **Nome do Pet** usando o serviço externo chamado pelo ponto de extremidade REST. Se os critérios de validação com base na fonte de dados falharem, as mensagens de erro serão exibidas no nível do campo.

![adicione um manipulador de erros personalizado em um formulário para manipular respostas de erros](/help/forms/assets/custom-error-handler-message-core-component.png)

Abra o console do navegador e verifique a mensagem de erro de validação na resposta e no cabeçalho, recebidos do ponto de acesso do serviço REST.


A função de manipulador de erros personalizada é responsável por executar ações adicionais, como exibir uma caixa de diálogo modal ou enviar um evento de análise, com base na resposta do erro. Uma função de manipulador de erros personalizada oferece a flexibilidade para adaptar o tratamento de erros aos requisitos específicos do usuário.

<!-- 

## Configure Adaptive Form submission to add custom handlers {#configure-adaptive-form-submission}

If the server validation error message does not display in the standard format, you can enable asynchronous submission and add a custom error handler on Adaptive Form submission to convert the message into a standard format.

### Configure asynchronous Adaptive Form submission {#configure-asynchronous-adaptive-form-submission}

Before adding custom handler, you must configure the adaptive form for asynchronous submission. Execute the following steps:

1. In adaptive form authoring mode, select the Form Container object and select ![adaptive form properties](assets/configure_icon.png) to open its properties.
1. In the **[!UICONTROL Submission]** properties section, enable **[!UICONTROL Use asynchronous submission]**.
1. Select **[!UICONTROL Revalidate on server]** to validate the input field values on server before submission.
1. Select the Submit Action:

    * Select **[!UICONTROL Submit using Form Data Model]** and select the appropriate data model, if you are using RESTful web service based [form data model](work-with-form-data-model.md) as the data source.
    * Select **[!UICONTROL Submit to REST Service endpoint]** and specify the **[!UICONTROL Redirect URL/Path]**, if you are using RESTful web services as the data source.

    ![adaptive form submission properties](assets/af_submission_properties.png)

1. Select ![Save](assets/save_icon.png) to save the properties.

### Add custom error handler on Adaptive Form submission {#add-custom-error-handler-af-submission}

AEM Forms provides out-of-the-box success and error handlers for form submissions. Handlers are client-side functions that execute based on the server response. When an Adaptive Form is submitted, the data is transmitted to the server for validation, which returns a response to the client with information about the success or error event for the submission. The information is passed as parameters to the relevant handler to execute the function.

Execute the following steps to add custom error handler on Adaptive Form submission:

1. Open an Adaptive Form in authoring mode, select any form object, and select  to open the rule editor.
1. Select **[!UICONTROL Form]** in the Form Objects tree and select **[!UICONTROL Create]**.
1. Select **[!UICONTROL Error in Submission]** from the Event drop-down list.
1. Write a rule to convert custom error structure to the standard error structure and select **[!UICONTROL Done]** to save the rule.

The following is a sample code to convert a custom error structure to the standard error structure:

```javascript
var data = $event.data;
var som_map = {
    "id": "guide[0].guide1[0].guideRootPanel[0].Pet[0].id_1[0]",
    "name": "guide[0].guide1[0].guideRootPanel[0].Pet[0].name_2[0]",
    "status": "guide[0].guide1[0].guideRootPanel[0].Pet[0].status[0]"
};

var errorJson = {};
errorJson.errors = [];

if (data) {
    if (data.originMessage) {
        var errorData;
        try {
            errorData = JSON.parse(data.originMessage);
        } catch (err) {
            // not in json format
        }

        if (errorData) {
            Object.keys(errorData).forEach(function(key) {
                var som_key = som_map[key];
                if (som_key) {
                    var error = {};
                    error.somExpression = som_key;
                    error.errorMessage = errorData[key];
                    errorJson.errors.push(error);
                }
            });
        }
        window.guideBridge.handleServerValidationError(errorJson);
    } else {
        window.guideBridge.handleServerValidationError(data);
    }
}
```

The `var som_map` lists the SOM expression of the Adaptive Form fields that you want to transform into the standard format. You can view the SOM expression of any field in an adaptive form by tapping the field and selecting **[!UICONTROL View SOM Expression]**.

Using this custom error handler, the adaptive form converts the fields listed in `var som_map` to standard error message format. As a result, the validation error messages display at field-level in the adaptive form.

 -->

## Informações adicionais {#additional-information}

* [Criar um formulário adaptável independente baseado nos Componentes principais](/help/forms/creating-adaptive-form-core-components.md)
* [Criar estilo ou temas para seus formulários](/help/forms/using-themes-in-core-components.md)
* [Criar ou adicionar um formulário adaptável à página do AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

## Consulte também {#see-also}

{{see-also}}

