---
title: Ações de enviar
description: Configurar as ações de envio para o formulário adaptável.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
source-git-commit: ba38294710553145a670ea42dd2b7571fa4eba7b
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---

# Ação de envio do formulário adaptável

Uma ação enviar especifica o destino dos dados coletados por meio de um formulário adaptável. O processo de envio começa quando o usuário clica no botão **[!UICONTROL Enviar]** no formulário. O AEM Forms oferece dois tipos de ações de envio descritos abaixo e permite que você crie e use ações de envio personalizadas para atender às suas necessidades específicas. As ações de envio prontas para uso são:

<!--To define a Submit Action for an Adaptive Form, you use the Properties dialog of the **Adaptive Form block** in the **Editor**-->

* [Enviar para endpoint REST](#rest-endpoint-submission-ue)
* [Enviar e-mail](#email-submission-ue)


### Enviar para endpoint REST {#rest-endpoint-submission-ue}

A ação Enviar para Ponto de Extremidade REST é usada para enviar os dados de formulário enviados para um ponto de extremidade REST especificado. O endpoint pode pertencer a um servidor interno em que o formulário está hospedado ou a um servidor externo usando um caminho relativo ou um caminho absoluto. Para enviar dados ao servidor do AEM que hospeda o formulário, use um caminho relativo correspondente ao caminho raiz do servidor do AEM. Por exemplo, `/content/forms/af/SampleForm.html`. Para enviar dados para qualquer outro servidor, use o caminho absoluto.

<!--Configuring the Submit Action to REST Endpoint for Adaptive Forms offers several benefits such as:  
* It facilitates seamless integration of form data with external systems and services via RESTful APIs.  
* Offers flexibility in managing data submissions from Adaptive Forms, accommodating dynamic and complex data structures.  
* Allows dynamic mapping of form fields to parameters within the REST endpoint URL, enabling adaptable and customizable data submissions.
-->



Para configurar um endpoint REST:

1. Abra o formulário adaptável no **[!UICONTROL Editor]**.
1. Selecione **[!UICONTROL Bloco de Formulários Adaptáveis]**.
1. Clique no ícone de propriedades ![propriedades](/help/forms/assets/Smock_Properties_18_N.svg).
1. Selecione o **[!UICONTROL Enviar para um ponto de extremidade REST]** na lista suspensa **[!UICONTROL Enviar Ação]**.
1. Especifique o URL do ponto de extremidade REST.
1. Você também pode **Habilitar a solicitação POST** e fornecer uma URL para publicar a solicitação.

![Habilitar solicitação de postagem para formulários adaptáveis](/help/forms/assets/enable-post-request-ue.png)

>[!NOTE]
>
> * Para publicar dados em um servidor interno, forneça o caminho do recurso. Os dados são publicados no caminho do recurso. Por exemplo, `/content/restEndPoint`. Para essas solicitações de publicação, as informações de autenticação da solicitação de envio são usadas.
> * Para publicar dados em um servidor externo, forneça um URL. O formato da URL é `https://host:port/path_to_rest_end_point`. Certifique-se de configurar o caminho para lidar com a solicitação POST de forma anônima.

### Enviar e-mail {#email-submission-ue}

Enviar email A ação de envio permite enviar um email para um ou mais recipients após o envio bem-sucedido do formulário. A configuração Enviar email ajuda a criar um email que pode incluir dados de formulário em um formato predefinido. Por exemplo, considere o seguinte modelo em que o nome do cliente, o endereço de entrega, o nome do estado e o CEP são recuperados dos dados de formulário enviado. [Saiba mais sobre Modelos de email no Forms Adaptável](/help/forms/html-email-templates-in-adaptive-forms.md). Algumas vantagens de configurar um Formulário adaptável com a ação Enviar email de envio são:

1. Ela permite a comunicação rápida, pois os dados do formulário são enviados diretamente para os destinatários de email designados.
1. Ajuda a simplificar o fluxo de trabalho, integrando diretamente os envios de formulários às notificações por email.
1. Ele ajuda as organizações a personalizar o conteúdo de email, tornando-o adequado para necessidades específicas de comunicação.

![Propriedades do Formulário Adaptável no Editor Universal](/help/forms/assets/submit-actions-ue.png)


Para configurar uma ação de envio como um Email para o envio do formulário:

1. Abra o formulário adaptável no **Editor**.
1. Selecione o **[!UICONTROL Bloco de Formulários Adaptáveis]**.
1. Clique no ícone de propriedades ![propriedades](/help/forms/assets/Smock_Properties_18_N.svg).
1. Selecione a opção **[!UICONTROL Enviar email]** na lista suspensa **[!UICONTROL Enviar Ação]**.
1. Após selecionar a opção enviar email, você pode configurar as seguintes propriedades, conforme mostrado na imagem abaixo.

<table>
  <thead>
    <tr>
      <th>Imagem</th>
      <th>Propriedade</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
    <td rowspan="7"><img src="/help/forms/assets/email-config-ue.png" alt="Configuração de email"></td> 
    <td><b>De</td>
    <td>Especifique o endereço de email do remetente.</td>
    </tr>
    <tr>
      <td><b>Para</td>
      <td>Especifique os principais destinatários do email. Vários endereços de email podem ser adicionados, separados por vírgulas.</td>
    </tr>
    <tr>
      <td><b>CC</td>
      <td>Especifique os recipients que devem receber uma cópia carbono (CC) do email.</td>
    </tr>
    <tr>
      <td><b>BCC</td>
      <td>Especifique os recipients que devem receber uma cópia oculta (CCO) do email.</td>
    </tr>
    <tr>
      <td><b>Assunto</td>
      <td>Especifique a linha de assunto do email.</td>
    </tr>
    <tr>
      <td><b>Usar modelo externo</td>
      <td>Permite o uso de um modelo de email externo para formatar o conteúdo do email. Forneça o URL ou o caminho para o modelo externo para integrar um modelo de email pré-projetado hospedado em sua pasta do AEM Assets.</td>
    </tr>
    <tr>
      <td><b>Incluir anexo</td>
      <td>Especifica se os dados de formulário enviados devem incluir um anexo enviado por meio do formulário no email. Os formatos de anexo compatíveis são PDF, XML e JSON.</td>
    </tr>
  </tbody>
</table>






<!--
        
        * **From**: The email address of the sender.
        * **To**: Specify the primary recipients of the email, multiple email addresses can be added, separated by commas.
        * **CC**: Specify the recipients who should receive a carbon copy (CC) of the email.
        * **BCC**: Specify the recipients who should receive a blind carbon copy (BCC) of the email.
        * **Subject**: Specify the subject line of the email.
        * **Use External Template**: Enables the use of an external email template for formatting the email content. Provide the URL or path to the External template path to integrate a pre-designed email template hosted in your AEM Assets folder.
        * **Include Attachment**: Specifies whether the submitted form data should include an attachment submitted through the form in the email.

    {width=50%,height=50%}![Enable post request for adaptive forms](/help/forms/assets/email-config-ue.png)

-->

## Mostrar uma mensagem de agradecimento personalizada no envio do Formulário adaptável {#submit-action-message-ue}

A opção Ao enviar ajuda a configurar uma mensagem de Ação de envio no envio do Formulário adaptável. Para configurar uma mensagem de Ação de envio para o seu formulário:

1. Abra o formulário adaptável no **Editor**.
1. Selecione o **[!UICONTROL Bloco de Formulários Adaptáveis]**.
1. Clique no ícone de propriedades ![propriedades](/help/forms/assets/Smock_Properties_18_N.svg).
1. Ao clicar em, você verá a seguinte opção:
   * **[!UICONTROL Ao Enviar]**: Ao Enviar ajuda você a personalizar uma mensagem a ser exibida quando um formulário for enviado. Por padrão, uma mensagem personalizada &quot;Obrigado por enviar o formulário&quot; é exibida ao usuário quando um formulário é enviado com êxito.
Você também pode personalizar a mensagem de agradecimento no envio do formulário, selecionando a opção para **[!UICONTROL Mostrar mensagem]** e adicionar/editar sua mensagem no Rich Text **Editor**.
