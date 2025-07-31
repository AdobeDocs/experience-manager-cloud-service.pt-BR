---
title: Como criar uma ação enviar personalizada para um formulário adaptável?
description: Saiba como criar uma Ação de envio personalizada para um Forms adaptável para atrasar o envio e processar dados antes de enviá-los para um endpoint restante, salvá-los em um armazenamento de dados e executar outras funções personalizadas.
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Intermediate
exl-id: 77131cc2-9cb1-4a00-bbc4-65b1a66e76f5
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '1697'
ht-degree: 0%

---

# Criar uma ação enviar personalizada para o Forms adaptável {#writing-custom-submit-action-for-adaptive-forms}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/customize-aem-forms/custom-submit-action-form.html?lang=pt-BR) |
| AEM as a Cloud Service (Componentes principais) | [Clique aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/custom-submit-action-for-adaptive-forms-based-on-core-components) |
| AEM as a Cloud Service (Componentes de base) | Este artigo |

Um Formulário adaptável fornece várias Ações de envio prontas para uso (OOTB). Uma Ação de envio especifica detalhes das ações a serem executadas nos dados coletados por meio do Formulário adaptável. Por exemplo, enviar dados em um email.

Você pode criar uma Ação de Envio personalizada para adicionar funcionalidades não incluídas em [Ações de Envio predefinidas](configuring-submit-actions.md) ou não suportadas por meio de uma única Ação de Envio OOTB. Por exemplo, enviar dados para um fluxo de trabalho, salvar os dados em um armazenamento de dados, enviar uma notificação por email à pessoa que envia o formulário e enviar um email à pessoa responsável pelo processamento do formulário enviado para aprovações e rejeições por meio de uma única Ação de envio.

## Formato de dados XML {#xml-data-format}

Os dados XML são enviados ao servlet usando o parâmetro de solicitação **`jcr:data`**. As Ações de envio podem acessar o parâmetro para processar os dados. O código a seguir descreve o formato dos dados XML. Os campos associados ao modelo de formulário aparecem na seção **`afBoundData`**. Campos não vinculados aparecem na seção `afUnoundData`. <!--For more information about the format of the `data.xml` file, see [Introduction to prepopulating Adaptive Form fields](prepopulate-adaptive-form-fields.md).-->

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

Uma Ação de envio pode adicionar campos de entrada ocultos (usando a marca [input](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) da HTML) ao formulário renderizado do HTML. Esses campos ocultos podem conter valores necessários ao processar o envio do formulário. Ao enviar o formulário, esses valores de campo são postados de volta como parâmetros de solicitação que a Ação de envio pode usar durante o manuseio do envio. Os campos de entrada são chamados de campos de ação.

Por exemplo, uma Ação Enviar que também capture o tempo gasto para preencher um formulário pode adicionar os campos de entrada ocultos `startTime` e `endTime`.

Um script pode fornecer os valores dos campos `startTime` e `endTime` quando o formulário é renderizado e antes do envio do formulário, respectivamente. O script de Ação de Envio `post.jsp` pode então acessar esses campos usando parâmetros de solicitação e calcular o tempo total necessário para preencher o formulário.

### Anexos de arquivo {#file-attachments}

As Ações de envio também podem usar os anexos de arquivo dos quais você faz upload usando o componente Anexo de arquivo. Os scripts de Ação Enviar podem acessar esses arquivos usando a [API RequestParameter](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html) do sling. O método [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) da API ajuda a identificar se o parâmetro de solicitação é um campo de arquivo ou de formulário. Você pode iterar sobre os parâmetros da Solicitação em uma Ação de envio para identificar os parâmetros de Anexo de arquivo.

O código de exemplo a seguir identifica os anexos de arquivo na solicitação. Em seguida, ele lê os dados no arquivo usando a [Obter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Por fim, ele cria um objeto Documento usando os dados e o anexa a uma lista.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

Ao anexar arquivos ao Formulário adaptável, o servidor valida os anexos de arquivo após o envio do Formulário adaptável e retorna uma mensagem de erro se:

* Os anexos de arquivo incluem um nome de arquivo que começa com o caractere (.), contém \ / : * ? &quot; &lt; > | ; % $ caracteres ou contém nomes de arquivo especiais reservados para o sistema operacional Windows, como `nul`, `prn`, `con`, `lpt` ou `com`.

* O tamanho do anexo de arquivo é de 0 bytes.

* O formato do anexo de arquivo não está definido na seção [Tipos de Arquivo com Suporte](https://helpx.adobe.com/br/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text) ao configurar o componente Anexo de Arquivo em um Formulário Adaptável.

### Caminho de encaminhamento e URL de redirecionamento {#forward-path-and-redirect-url}

Depois de executar a ação necessária, o servlet Submit encaminha a solicitação para o caminho de encaminhamento. Uma ação usa a API setForwardPath para definir o caminho de encaminhamento no servlet Guide Submit.

Se a ação não fornecer um caminho de encaminhamento, o servlet Submit redirecionará o navegador usando o URL de redirecionamento. O autor configura o URL de redirecionamento usando a configuração da página de agradecimento na caixa de diálogo Edição do formulário adaptável. Você também pode configurar o URL de redirecionamento por meio da Ação enviar ou da API setRedirectUrl no servlet Guide Submit. Você também pode configurar os parâmetros de Solicitação enviados para o URL de redirecionamento usando a API setRedirectParameters no servlet de Envio do guia.

>[!NOTE]
>
>Um autor fornece o URL de redirecionamento (usando a Configuração da página de agradecimento). [Ações de Envio de OOTB](configuring-submit-actions.md) use a URL de Redirecionamento para redirecionar o navegador a partir do recurso ao qual o caminho de encaminhamento faz referência.
>
>Você pode escrever uma ação enviar personalizada que encaminhe uma solicitação para um recurso ou servlet. A Adobe recomenda que o script que executa o manuseio de recursos para o caminho de encaminhamento redirecione a solicitação para o URL de redirecionamento quando o processamento for concluído.

## Ação de envio {#submit-action}

Uma Ação Enviar é uma sling:Folder que inclui o seguinte:

* **addfields.jsp**: este script fornece os campos de ação que são adicionados ao arquivo HTML durante a representação. Use esse script para adicionar os parâmetros de entrada ocultos necessários durante o envio no script post.POST.jsp.
* **dialog.xml**: este script é semelhante à caixa de diálogo Componente CQ. Ela fornece informações de configuração que o autor personaliza. Os campos são exibidos na guia Enviar Ações na caixa de diálogo Editar formulário adaptável ao selecionar a Ação de envio.
* **post.POST.jsp**: o servlet Submit chama esse script com os dados enviados e os dados adicionais nas seções anteriores. Qualquer menção à execução de uma ação nesta página implica em executar o script post.POST.jsp. Para registrar a Ação de envio com o Forms adaptável a ser exibido na caixa de diálogo Editar formulário adaptável, adicione essas propriedades ao `sling:Folder`:

   * **guideComponentType** do tipo String e valor **fd/af/components/guidesubmittype**
   * **guideDataModel** do tipo Cadeia de Caracteres que especifica o tipo de Formulário Adaptável ao qual a Ação de Envio se aplica. <!--**xfa** is supported for XFA-based Adaptive Forms while -->**xsd** é compatível com o Adaptive Forms baseado em XSD. Há suporte para **basic** para o Adaptive Forms que não usam XDP ou XSD. Para exibir a ação em vários tipos de Forms adaptável, adicione as cadeias de caracteres correspondentes. Separe cada string por vírgula. Por exemplo, para tornar uma ação visível no <!--XFA- and -->Forms adaptável baseado em XSD, especifique o valor como <!--**xfa** and--> **xsd**.

   * **jcr:description** do tipo String. O valor dessa propriedade é exibido na lista Ação de envio na guia Ações de envio da caixa de diálogo Edição do formulário adaptável. As ações OOTB estão presentes no repositório do CRX no local **/libs/fd/af/components/guidesubmittype**.

   * **submitService** do tipo Cadeia de caracteres. Para obter mais informações, consulte [Agendar envio do Formulário Adaptável para ações personalizadas](#schedule-adaptive-form-submission).

## Criação de uma Ação de envio personalizada {#creating-a-custom-submit-action}

>[!NOTE]
>
> Para saber como criar uma ação de envio personalizada para Componentes Principais, consulte [Criar uma ação de envio personalizada para o Adaptive Forms (Componentes Principais)](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/custom-submit-action-for-adaptive-forms-based-on-core-components).

Execute as seguintes etapas para criar uma Ação enviar personalizada que salve os dados no repositório do CRX e envie um email para você. O formulário adaptável contém o conteúdo do armazenamento de ação de envio OOTB (desaprovado) que salva os dados no repositório do CRX. Além disso, o AEM fornece uma API de [Email](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/mailer/package-summary.html) que pode ser usada para enviar emails. Antes de usar a API de email, configure o serviço Day CQ Mail por meio do console do sistema. Você pode reutilizar a ação Armazenar conteúdo (obsoleto) para armazenar os dados no repositório. A ação Armazenar conteúdo (obsoleto) está disponível no local /libs/fd/af/components/guidesubmittype/store no repositório do CRX.

1. Faça logon no CRXDE Lite no URL https://&lt;server>:&lt;port>/crx/de/index.jsp. Crie um nó com a propriedade sling:Folder e o nome store_and_mail na pasta /apps/custom_submit_action. Crie a pasta custom_submit_action se ela ainda não existir.

   ![Captura de tela representando a criação de um nó com a propriedade sling:Folder](assets/step1.png)

2. **Forneça os campos de configuração obrigatórios.**

   Adicione a configuração exigida pela ação Armazenar. Copie o nó **cq:dialog** da ação Armazenar de /libs/fd/af/components/guidesubmittype/store para a pasta de ações em /apps/custom_submit_action/store_and_email.

   ![Captura de tela mostrando a cópia do nó da caixa de diálogo para a pasta de ação](assets/step2.png)

3. **Forneça campos de configuração para solicitar ao autor a configuração de email.**

   O Formulário adaptável também fornece uma ação Email que envia emails para os usuários. Personalize esta ação com base em suas necessidades. Navegue até /libs/fd/af/components/guidesubmittype/email/dialog. Copie os nós no nó cq:dialog para o nó cq:dialog da sua Ação de Envio (/apps/custom_submit_action/store_and_email/dialog).

   ![Personalizando a ação de email](assets/step3.png)

4. **Disponibilizar a ação na caixa de diálogo Editar Formulário Adaptável.**

   Adicione as seguintes propriedades no nó store_and_email:

   * **guideComponentType** do tipo **String** e valor **fd/af/components/guidesubmittype**

   * **guideDataModel** do tipo **String** e valor **<!--xfa, -->xsd, basic**

   * **jcr:description** do tipo **Cadeia de caracteres** e valor **Ação de armazenamento e email**

   * **submitService** do tipo **cadeia de caracteres** e valor **Armazenamento e email**. Para obter mais informações, consulte [Agendar envio do Formulário Adaptável para ações personalizadas](#schedule-adaptive-form-submission).

5. Abra qualquer Formulário adaptável. Clique no botão **Editar** ao lado de **Iniciar** para abrir a caixa de diálogo **Editar** do contêiner de Formulário Adaptável. A nova ação é exibida na guia **Enviar Ações**. Selecionar a **Ação de Armazenamento e Email** exibe a configuração adicionada no nó da caixa de diálogo.

   ![Caixa de diálogo de configuração Enviar Ação](assets/store_and_email_submit_action_dialog.jpg)

6. **Use a ação para concluir uma tarefa.**

   Adicione o script post.POST.jsp à ação. (/apps/custom_submit_action/store_and_mail/).

   Execute a ação Armazenamento OOTB (script post.POST.jsp). Use a API [FormsHelper.runAction](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction-java.lang.String-java.lang.String-org.apache.sling.api.resource.Resource-org.apache.sling.api.SlingHttpServletRequest-org.apache.sling.api.SlingHttpServletResponse-)&#x200B;(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse)) que o CQ fornece no código para executar a ação Armazenar. Adicione o seguinte código no arquivo JSP:

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   Para enviar o email, o código lê o endereço de email do recipient na configuração. Para buscar o valor de configuração no script da ação, leia as propriedades do recurso atual usando o código a seguir. Da mesma forma, você pode ler os outros arquivos de configuração.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Por fim, use a API de email do CQ para enviar o email. Use a classe [SimpleEmail](https://commons.apache.org/proper/commons-email/commons-email2-javax/apidocs/org/apache/commons/mail2/javax/SimpleEmail.html) para criar o Objeto de Email conforme mostrado abaixo:

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

   Selecione a ação no Formulário adaptável. A ação envia um email e armazena os dados.

## Usar a propriedade submitService para ações de envio personalizadas {#submitservice-property}

Ao definir a Ação de Envio personalizada, que inclui a propriedade `submitService`, o formulário aciona o [FormSubmitActionService](https://helpx.adobe.com/br/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/service/FormSubmitActionService.html) no envio. O `FormSubmitActionService` usa o método `getServiceName` para recuperar o valor da propriedade `submitService`. Com base no valor da propriedade `submitService`, o serviço invoca o método de envio apropriado. Inclua o `FormSubmitActionService` no pacote personalizado que você carregou para o servidor [!DNL AEM Forms].

Adicione a propriedade `submitService` do tipo cadeia de caracteres ao `sling:Folder` de sua Ação de Envio personalizada para habilitar [!DNL Adobe Sign] para o Formulário adaptável. Você pode selecionar a opção **[!UICONTROL Habilitar Adobe Sign]** na seção **[!UICONTROL Assinatura Eletrônica]** das propriedades do contêiner de Formulário Adaptável somente após definir o valor da propriedade `submitService` da sua Ação de Envio personalizada.

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

If the action does not provide a forward path, the Submit servlet redirects the browser using the Redirect URL. The author configures the Redirect URL using the Thank You Page configuration in the Adaptive Form Edit dialog. You can also configure the Redirect URL through the Submit Action or the setRedirectUrl API in the Guide Submit servlet. You can also configure the Request parameters sent to the Redirect URL using the setRedirectParameters API in the Guide Submit servlet.

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

1. Log in to CRXDE Lite at the URL https://&lt;server&gt;:&lt;port&gt;/crx/de/index.jsp. Create a node with the property sling:Folder and name store_and_mail in the /apps/custom_submit_action folder. Create the custom_submit_action folder if it does not exist already.

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

>[!MORELIKETHIS]
>
>* [Configurar uma Ação de Envio para um Formulário Adaptável](/help/forms/configure-submit-actions-core-components.md)