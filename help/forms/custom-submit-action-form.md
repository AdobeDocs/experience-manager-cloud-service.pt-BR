---
title: Como criar uma ação de envio personalizada para um formulário adaptável?
description: Saiba como criar uma Ação de envio personalizada para um Forms adaptável para atrasar o envio e o processamento de dados antes de enviá-los para um terminal restante, salvá-los em um armazenamento de dados e executar outras funções personalizadas.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 77131cc2-9cb1-4a00-bbc4-65b1a66e76f5
source-git-commit: 391a9482cc6ed97984693c21b41910fdd32ff25d
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 0%

---

# Criar uma ação de envio personalizada para o Adaptive Forms {#writing-custom-submit-action-for-adaptive-forms}

Um formulário adaptável fornece várias ações de envio prontas para uso (OOTB). Uma Ação de envio especifica os detalhes das ações a serem executadas nos dados coletados pelo Formulário adaptável. Por exemplo, envio de dados em um email.

Você pode criar uma Ação de envio personalizada para adicionar funcionalidades não incluídas em [ações de envio prontas para uso](configuring-submit-actions.md) ou não suportado por meio de uma única Ação de envio OOTB. Por exemplo, enviar dados para um workflow, salvar os dados em um armazenamento de dados, enviar uma notificação por email para a pessoa que envia o formulário e enviar um email para a pessoa responsável pelo processamento do formulário enviado para aprovações e rejeições por meio de uma única Ação de envio.

## Formato dos dados XML {#xml-data-format}

Os dados XML são enviados para o servlet usando o **`jcr:data`** parâmetro de solicitação. Enviar ações pode acessar o parâmetro para processar os dados. O código a seguir descreve o formato dos dados XML. Os campos vinculados ao modelo de formulário aparecem no **`afBoundData`** seção. Os campos não vinculados são exibidos na variável `afUnoundData`seção. <!--For more information about the format of the `data.xml` file, see [Introduction to prepopulating Adaptive Form fields](prepopulate-adaptive-form-fields.md).-->

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### Campos de ação {#action-fields}

Uma ação Enviar pode adicionar campos de entrada ocultos (usando o HTML [input](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) tag) para o HTML de formulário renderizado. Esses campos ocultos podem conter valores necessários durante o processamento do envio do formulário. Ao enviar o formulário, esses valores de campo são postados como parâmetros de solicitação que a Ação de envio pode usar durante o manuseio de envio. Os campos de entrada são chamados de campos de ação.

Por exemplo, uma Ação de envio que também captura o tempo gasto para preencher um formulário pode adicionar os campos de entrada ocultos `startTime` e `endTime`.

Um script pode fornecer os valores da variável `startTime` e `endTime` campos quando o formulário é renderizado e antes do envio do formulário, respectivamente. O script Enviar ação `post.jsp` O pode então acessar esses campos usando parâmetros de solicitação e calcular o tempo total necessário para preencher o formulário.

### Anexos de arquivo {#file-attachments}

As ações Enviar também podem usar os anexos de arquivo que você faz upload usando o componente Anexo de arquivo . Os scripts Submit Action podem acessar esses arquivos usando o sling [API RequestParameter](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). O [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) O método da API ajuda a identificar se o parâmetro da solicitação é um arquivo ou um campo de formulário. Você pode iterar sobre os parâmetros da Solicitação em uma Ação de envio para identificar os parâmetros do Anexo de arquivo.

O código de exemplo a seguir identifica os anexos do arquivo na solicitação. Em seguida, ele lê os dados no arquivo usando o [Obter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Finalmente, ele cria um objeto de Documento usando os dados e o anexa a uma lista.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

Ao anexar arquivos ao Formulário adaptável, o servidor valida os anexos do arquivo após o envio do Formulário adaptativo e retorna uma mensagem de erro se:

* Os anexos de arquivo incluem um nome de arquivo que começa com (.) caractere, contém \ / : * ? &quot; &lt; > | ; % $ caracteres ou contém nomes de arquivo especiais reservados para o sistema operacional Windows, como `nul`, `prn`, `con`, `lpt`ou `com`.

* O tamanho do anexo do arquivo é de 0 bytes.

* O formato do anexo do arquivo não é definido na variável [Tipos de arquivo suportados](https://helpx.adobe.com/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text) ao configurar o componente de anexo de arquivo em um formulário adaptável.

### Caminho de encaminhamento e URL de redirecionamento {#forward-path-and-redirect-url}

Depois de executar a ação necessária, o servlet Enviar encaminha a solicitação para o caminho de encaminhamento. Uma ação usa a API setForwardPath para definir o caminho de encaminhamento no servlet Guide Submit.

Se a ação não fornecer um caminho de encaminhamento, o servlet Enviar redirecionará o navegador usando o URL de redirecionamento. O autor configura o URL de redirecionamento usando a configuração da Página de agradecimento na caixa de diálogo Edição de formulário adaptável. Você também pode configurar o URL de redirecionamento por meio da Ação de envio ou da API setRedirectUrl no servlet Guide Submit. Você também pode configurar os parâmetros de Solicitação enviados para o URL de redirecionamento usando a API setRedirectParameters no servlet Guide Submit.

>[!NOTE]
>
>Um autor fornece o URL de redirecionamento (usando a Configuração da página de agradecimento). [Ações de envio de OOTB](configuring-submit-actions.md) use o URL de redirecionamento para redirecionar o navegador do recurso que o caminho de encaminhamento faz referência.
>
>Você pode gravar uma Ação de envio personalizada que encaminhe uma solicitação a um recurso ou servlet. O Adobe recomenda que o script que executa a manipulação de recursos para o caminho de encaminhamento redirecione a solicitação para o URL de redirecionamento quando o processamento for concluído.

## Ação de envio {#submit-action}

Uma Ação de envio é uma sling:Folder que inclui o seguinte:

* **addfields.jsp**: Esse script fornece os campos de ação adicionados ao arquivo HTML durante a representação. Use esse script para adicionar os parâmetros de entrada ocultos necessários durante a submissão no script post.POST.jsp.
* **dialog.xml**: Esse script é semelhante à caixa de diálogo do Componente CQ. Ele fornece informações de configuração personalizadas pelo autor. Os campos são exibidos na guia Enviar ações na caixa de diálogo Editar formulário adaptável ao selecionar a Ação de envio.
* **post.POST.jsp**: O servlet Enviar chama esse script com os dados enviados e os dados adicionais das seções anteriores. Qualquer menção de executar uma ação nesta página implica executar o script post.POST.jsp. Para registrar a Ação de envio no Adaptive Forms para exibir na caixa de diálogo Edição de formulário adaptável, adicione essas propriedades ao sling:Folder:

   * **guideComponentType** do tipo String e value **fd/af/components/guidesubmittype**
   * **guideDataModel** do tipo String que especifica o tipo de Formulário adaptável ao qual a Ação de envio é aplicável. <!--**xfa** is supported for XFA-based Adaptive Forms while -->**xsd** O é compatível com o Adaptive Forms baseado em XSD. **básico** é compatível com o Adaptive Forms que não usa XDP ou XSD. Para exibir a ação em vários tipos de Adaptive Forms, adicione as strings correspondentes. Separe cada string por vírgula. Por exemplo, para tornar uma ação visível em <!--XFA- and -->Forms adaptável baseado em XSD, especifique o valor como <!--**xfa** and--> **xsd**.

   * **jcr:description** do tipo String. O valor dessa propriedade é exibido na lista Enviar ação da guia Enviar ações da caixa de diálogo Editar formulário adaptável. As ações OOTB estão presentes no repositório CRX no local **/libs/fd/af/components/guidesubmittype**.

   * **submitService** do tipo String. Para obter mais informações, consulte [Agendar envio de formulário adaptável para ações personalizadas](#schedule-adaptive-form-submission).

## Criação de uma ação de envio personalizada {#creating-a-custom-submit-action}

Execute as etapas a seguir para criar uma Ação de envio personalizada que salve os dados no repositório CRX e, em seguida, envie um email para você. O Formulário adaptativo contém o Conteúdo do repositório de ações de envio OOTB (obsoleto) que salva os dados no repositório CRX. Além disso, o AEM fornece uma [Email](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/mailer/package-summary.html) API que pode ser usada para enviar emails. Antes de usar a API de email, configure o serviço Day CQ Mail pelo console do sistema. Você pode reutilizar a ação Armazenar conteúdo (obsoleto) para armazenar os dados no repositório. A ação Armazenar conteúdo (obsoleto) está disponível no local /libs/fd/af/components/guidesubmittype/store no repositório CRX.

1. Faça logon no CRXDE Lite no URL https://&lt;server>:&lt;port>/crx/de/index.jsp. Crie um nó com a propriedade sling:Folder e name store_and_mail na pasta /apps/custom_submit_action. Crie a pasta custom_submit_action se ela ainda não existir.

   ![Captura de tela representando a criação de um nó com a propriedade sling:Folder](assets/step1.png)

1. **Forneça os campos de configuração obrigatórios.**

   Adicione a configuração necessária para a ação Loja. Copie o **cq:dialog** nó da ação Loja de /libs/fd/af/components/guidesubmittype/store para a pasta de ações em /apps/custom_submit_action/store_and_email.

   ![Captura de tela mostrando a cópia do nó de diálogo para a pasta de ações](assets/step2.png)

1. **Forneça campos de configuração para solicitar a configuração do email ao autor.**

   O formulário adaptável também fornece uma ação de email que envia emails para os usuários. Personalize essa ação com base em suas necessidades. Navegue até /libs/fd/af/components/guidesubmittype/email/dialog. Copie os nós no nó cq:dialog para o nó cq:dialog de sua Ação de Enviar (/apps/custom_submit_action/store_and_email/dialog).

   ![Personalização da ação de email](assets/step3.png)

1. **Disponibilize a ação na caixa de diálogo Adaptive Form Edit .**

   Adicione as seguintes propriedades no nó store_and_email:

   * **guideComponentType** de tipo **String** e valor **fd/af/components/guidesubmittype**

   * **guideDataModel** de tipo **String** e valor **<!--xfa, -->xsd, básico**

   * **jcr:description** de tipo **String** e valor **Ação de armazenamento e email**

   * **submitService** de tipo **String** e valor **Armazenar e enviar email**. Para obter mais informações, consulte [Agendar envio de formulário adaptável para ações personalizadas](#schedule-adaptive-form-submission).

1. Abra qualquer formulário adaptável. Clique no botão **Editar** botão ao lado de **Iniciar** para abrir o **Editar** caixa de diálogo do contêiner Formulário adaptável . A nova ação é exibida na variável **Enviar ações** Guia. Selecionar o **Ação de armazenamento e email** exibe a configuração adicionada no nó da caixa de diálogo.

   ![Caixa de diálogo de configuração Enviar ação](assets/store_and_email_submit_action_dialog.jpg)

1. **Use a ação para concluir uma tarefa.**

   Adicione o script post.POST.jsp à sua ação. (/apps/custom_submit_action/store_and_mail/).

   Execute a ação Loja OOTB (script post.POST.jsp). Use o [FormsHelper.runAction](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction-java.lang.String-java.lang.String-org.apache.sling.api.resource.Resource-org.apache.sling.api.SlingHttpServletRequest-org.apache.sling.api.SlingHttpServletResponse-)(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse) API que o CQ fornece em seu código para executar a ação Loja. Adicione o seguinte código em seu arquivo JSP:

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   Para enviar o email, o código lê o endereço de email do recipient na configuração. Para buscar o valor de configuração no script da ação, leia as propriedades do recurso atual usando o código a seguir. Da mesma forma, é possível ler os outros arquivos de configuração.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Por fim, use a API de email do CQ para enviar o email. Use o [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) classe para criar o Objeto de email conforme mostrado abaixo:

   >[!NOTE]
   >
   >Certifique-se de que o arquivo JSP tenha o nome post.POST.jsp.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   Selecione a ação no formulário adaptável. A ação envia um email e armazena os dados.

## Usar a propriedade submitService para ações de envio personalizadas {#submitservice-property}

Ao definir a Ação de envio personalizada, que inclui a variável `submitService` , o formulário aciona a variável [FormSubmitActionService](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/service/FormSubmitActionService.html) após a submissão. O `FormSubmitActionService` usa a variável `getServiceName` para recuperar o valor da variável `submitService` propriedade. Com base no valor da variável `submitService` , o serviço chama o método de envio apropriado. Inclua a `FormSubmitActionService` para o pacote personalizado que você faz upload para o [!DNL AEM Forms] servidor.

Adicione o `submitService` propriedade do tipo string para `sling:Folder` da sua Ação de envio personalizada para ativar [!DNL Adobe Sign] para o formulário adaptável. Você pode selecionar a variável **[!UICONTROL Ativar o Adobe Sign]** na **[!UICONTROL Assinatura eletrônica]** seção das propriedades do contêiner do Formulário adaptável somente após definir o valor para a variável `submitService` propriedade da sua Ação de envio personalizada.

<!--As a result of setting an appropriate value for the `submitService` property and enabling [!DNL Adobe Sign], you can schedule the submission of an Adaptive Form to ensure that all configured signers have taken an action on the form. [!DNL Adobe Sign] Configuration Service keeps polling [!DNL Adobe Sign] server at regular intervals to verify the status of signatures. If all the signers complete signing the form, the Submit Action service is started and the form is submitted.-->


![Enviar propriedade de serviço](assets/submit-service-property.png)

<!-- You can't do comments within comments, so I changed comment tags to <start-comment> <end-comment> -->

<!--
## Workflow for a Submit Action {#workflow-for-a-submit-action}

The flowchart depicts the workflow for a Submit Action that is triggered when you click the **[!UICONTROL Submit]** button in an Adaptive Form. The files in the File Attachment component are uploaded to the server, and the form data is updated with the URLs of the uploaded files. Within the client, the data is stored in the JSON format. The client sends an Ajax request to an internal servlet that massages the data you specified and returns it in the XML format. The client collates this data with action fields. It submits the data to the final servlet (Guide Submit servlet) through a Form Submit Action. Then, the servlet forwards the control to the Submit Action. The Submit Action can forward the request to a different sling resource or redirect the browser to another URL.

![Flowchart depicting the workflow for Submit Action](assets/diagram1.png)

### XML data format {#xml-data-format}

The XML data is sent to the servlet using the **`jcr:data`** request parameter. Submit Actions can access the parameter to process the data. The following code describes the format of the XML data. The fields that are bound to the Form model appear in the **`afBoundData`** section. Unbound fields appear in the `afUnoundData`section. For more information about the format of the `data.xml` file, see [Introduction to prepopulating Adaptive Form fields](prepopulate-adaptive-form-fields.md).

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<start comment> xml corresponding to the Form Model /XML Schema <end comment>
<start comment> </afBoundData> <end comment>
</afData>
```

### Action fields {#action-fields}

A Submit Action can add hidden input fields (using the HTML [input](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) tag) to the rendered form HTML. These hidden fields can contain values that it needs while processing form submission. When submitting the form, these field values are posted back as request parameters that the Submit Action can use during submission handling. The input fields are called action fields.

For example, a Submit Action that also captures the time taken to fill a form can add the hidden input fields `startTime` and `endTime`.

A script can supply the values of the `startTime` and `endTime` fields when the form renders and before form submission, respectively. The Submit Action script `post.jsp` can then access these fields using request parameters and compute the total time required to fill the form.

### File attachments {#file-attachments}

Submit Actions can also use the file attachments you upload using the File Attachment component. Submit Action scripts can access these files using the sling [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). The [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) method of the API helps identify whether the request parameter is a file or a form field. You can iterate over the Request parameters in a Submit Action to identify File Attachment parameters.

The following sample code identifies the file attachments in the request. Next, it reads the data into the file using the [Get API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Finally, it creates a Document object using the data and appends it to a list.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### Forward path and Redirect URL {#forward-path-and-redirect-url}

After performing the required action, the Submit servlet forwards the request to the forward path. An action uses the setForwardPath API to set the forward path in the Guide Submit servlet.

If the action doesn't provide a forward path, the Submit servlet redirects the browser using the Redirect URL. The author configures the Redirect URL using the Thank You Page configuration in the Adaptive Form Edit dialog. You can also configure the Redirect URL through the Submit Action or the setRedirectUrl API in the Guide Submit servlet. You can also configure the Request parameters sent to the Redirect URL using the setRedirectParameters API in the Guide Submit servlet.

>[!NOTE]
>
>An author provides the Redirect URL (using the Thank You Page Configuration). [OOTB Submit Actions](configuring-submit-actions.md) use the Redirect URL to redirect the browser from the resource that the forward path references.
>
>You can write a custom Submit Action that forwards a request to a resource or servlet. Adobe recommends that the script that performs resource handling for the forward path redirect the request to the Redirect URL when the processing completes.

## Submit Action {#submit-action}

A Submit Action is a sling:Folder that includes the following:

* **addfields.jsp**: This script provides the action fields that are added to the HTML file during rendition. Use this script to add hidden input parameters required during submission in the post.POST.jsp script.
* **dialog.xml**: This script is similar to the CQ Component dialog. It provides configuration information that the author customizes. The fields are displayed in the Submit Actions Tab in the Adaptive Form Edit dialog when you select the Submit Action.
* **post.POST.jsp**: The Submit servlet calls this script with the data that you submit and the additional data in the previous sections. Any mention of running an action in this page implies running the post.POST.jsp script. To register the Submit Action with the Adaptive Forms to display in the Adaptive Form Edit dialog, add these properties to the sling:Folder:

    * **guideComponentType** of type String and value **fd/af/components/guidesubmittype**
    * **guideDataModel** of type String that specifies the type of Adaptive Form for which the Submit Action is applicable. **xfa** is supported for XFA-based Adaptive Forms while **xsd** is supported for XSD-based Adaptive Forms. **basic** is supported for Adaptive Forms that do not use XDP or XSD. To display the action on multiple types of Adaptive Forms, add the corresponding strings. Separate each string by a comma. For example, to make an action visible on XFA- and XSD-based Adaptive Forms, specify the values **xfa** and **xsd** respectively.

    * **jcr:description** of type String. The value of this property is displayed in the Submit Action list in the Submit Actions Tab of the Adaptive Form Edit dialog. The OOTB actions are present in the CRX repository at the location **/libs/fd/af/components/guidesubmittype**.

## Creating a custom Submit Action {#creating-a-custom-submit-action}

Perform the following steps to create a custom Submit Action that saves the data in the CRX repository and then sends you an email. The Adaptive Form contains the OOTB Submit Action Store Content (deprecated) that saves the data in the CRX repository. In addition, CQ provides a [Mail](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/mailer/package-summary.html) API that can be used to send emails. Before using the Mail API, configure the Day CQ Mail service through the system console. You can reuse the Store Content (deprecated) action to store the data in the repository. The Store Content (deprecated) action is available at the location /libs/fd/af/components/guidesubmittype/store in the CRX repository.

1. Log in to CRXDE Lite at the URL https://&lt;server&gt;:&lt;port&gt;/crx/de/index.jsp. Create a node with the property sling:Folder and name store_and_mail in the /apps/custom_submit_action folder. Create the custom_submit_action folder if it doesn't exist already.

   ![Screenshot depicting the creation of a node with the property sling:Folder](assets/step1.png)

1. **Provide the mandatory configuration fields.**

   Add the configuration the Store action requires. Copy the **cq:dialog** node of the Store action from /libs/fd/af/components/guidesubmittype/store to the action folder at /apps/custom_submit_action/store_and_email.

   ![Screenshot showing the copying of the dialog node to the action folder](assets/step2.png)

1. **Provide configuration fields to prompt the author for email configuration.**

   The Adaptive Form also provides an Email action that sends emails to users. Customize this action based on your requirements. Navigate to /libs/fd/af/components/guidesubmittype/email/dialog. Copy the nodes within the cq:dialog node to cq:dialog node of your Submit Action (/apps/custom_submit_action/store_and_email/dialog).

   ![Customizing the email action](assets/step3.png)

1. **Make the action available in the Adaptive Form Edit dialog.**

   Add the following properties in the store_and_email node:

    * **guideComponentType** of type **String** and value **fd/af/components/guidesubmittype**

    * **guideDataModel** of type **String** and value **xfa, xsd, basic**

    * **jcr:description** of type **String** and value **Store and Email Action**

1. Open any Adaptive Form. Click the **Edit** button next to **Start** to open the **Edit** dialog of the Adaptive Form container. The new action is displayed in the **Submit Actions** Tab. Selecting the **Store and Email Action** displays the configuration added in the dialog node.

   ![Submit Action configuration dialog](assets/store_and_email_submit_action_dialog.jpg)

1. **Use the action to complete a task.**

   Add the post.POST.jsp script to your action. (/apps/custom_submit_action/store_and_mail/).

   Run the OOTB Store action (post.POST.jsp script). Use the [FormsHelper.runAction](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction-java.lang.String-java.lang.String-org.apache.sling.api.resource.Resource-org.apache.sling.api.SlingHttpServletRequest-org.apache.sling.api.SlingHttpServletResponse-(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse)) API that CQ provides in your code to run the Store action. Add the following code in your JSP file:

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   To send the email, the code reads the recipient's email address from the configuration. To fetch the configuration value in the action's script, read the properties of the current resource using the following code. Similarly you can read the other configuration files.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Finally, use the CQ Mail API to send the email. Use the [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) class to create the Email Object as depicted below:

   >[!NOTE]
   >
   >Ensure that the JSP file has the name post.POST.jsp.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   Select the action in the Adaptive Form. The action sends an email and stores the data. 

-->
