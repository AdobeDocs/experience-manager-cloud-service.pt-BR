---
title: Ações de enviar
description: Configurar as ações de envio para o formulário adaptável.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
hide: true
hidefromToC: true
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 1%

---

# Ação de envio do formulário adaptável

## Visão geral

O envio de formulários é a etapa final crítica na jornada do usuário — é onde os dados coletados são processados e as ações são executadas. Este documento fornece um guia abrangente para configurar e gerenciar ações de envio para o Adaptive Forms no Universal Editor.

### O que você vai aprender

No final deste documento, você entenderá como:

- Configurar diferentes tipos de ações de envio para seus formulários
- Configurar envios de endpoint REST para integração com sistemas externos
- Configurar envios de email para respostas de formulário
- Implementar ações de envio personalizadas para necessidades comerciais específicas
- Lidar com cenários de erro e validação de formulário durante o envio

### Público-alvo

Este guia foi projetado para:

- **Desenvolvedores de formulários** implementando a lógica de envio
- **Integradores de sistemas** conectando formulários a sistemas back-end
- **Analistas de negócios** definindo fluxos de trabalho de formulário
- **Arquitetos técnicos** projetando processos de envio de formulário

### Ações de envio disponíveis

O Universal Editor fornece dois tipos de ação de envio principais:

1. **Enviar para ponto de extremidade REST** * Enviar dados de formulário para pontos de extremidade de API
2. **Enviar Email** * Enviar respostas do formulário por email

### Pré-requisitos

Antes de configurar ações de envio, verifique se você tem:

- Acesso ao Universal Editor
- Permissões apropriadas para a configuração do formulário
- Noções básicas do terminal de envio do target ou da configuração de email

Uma ação enviar especifica o destino dos dados coletados por meio de um formulário adaptável. O processo de envio começa quando o usuário clica no botão **[!UICONTROL Enviar]** no formulário. O AEM Forms oferece dois tipos de ações de envio descritos abaixo e permite que você crie e use ações de envio personalizadas para atender às suas necessidades específicas. As ações de envio prontas para uso são:

<!--To define a Submit Action for an Adaptive Form, you use the Properties dialog of the **Adaptive Form block** in the **Editor**-->

- [Enviar para endpoint REST](#rest-endpoint-submission-ue)
- [Enviar e-mail](#email-submission-ue)


### Enviar para endpoint REST {#rest-endpoint-submission-ue}

A ação Enviar para Ponto de Extremidade REST é usada para enviar os dados de formulário enviados para um ponto de extremidade REST especificado. O endpoint pode pertencer a um servidor interno em que o formulário está hospedado ou a um servidor externo usando um caminho relativo ou um caminho absoluto. Para enviar dados ao servidor do AEM que hospeda o formulário, use um caminho relativo correspondente ao caminho raiz do servidor do AEM. Por exemplo, `/content/forms/af/SampleForm.html`. Para enviar dados para qualquer outro servidor, use o caminho absoluto.

<!--Configuring the Submit Action to REST Endpoint for Adaptive Forms offers several benefits such as:  
- It facilitates seamless integration of form data with external systems and services via RESTful APIs.  
- Offers flexibility in managing data submissions from Adaptive Forms, accommodating dynamic and complex data structures.  
- Allows dynamic mapping of form fields to parameters within the REST endpoint URL, enabling adaptable and customizable data submissions.
-->



Para configurar um endpoint REST:

1. Abra o formulário adaptável no **[!UICONTROL Editor]**.
1. Selecione **[!UICONTROL Bloco de Formulários Adaptáveis]**.
1. Clique no ícone de propriedades ![propriedades](/help/forms/assets/Smock_Properties_18_N.svg).
1. Selecione o **[!UICONTROL Enviar para um ponto de extremidade REST]** na lista suspensa **[!UICONTROL Enviar Ação]**.
1. Especifique o URL do ponto de extremidade REST.
1. Você também pode **Habilitar a solicitação POST** e fornecer uma URL para publicar a solicitação.

![Captura de tela do painel de propriedades Editor Universal mostrando os campos de configuração de ponto de extremidade REST, incluindo a entrada de URL e a opção Habilitar solicitação POST para envio de formulário](/help/forms/assets/enable-post-request-ue.png)

>[!NOTE]
>
> - Para publicar dados em um servidor interno, forneça o caminho do recurso. Os dados são publicados no caminho do recurso. Por exemplo, `/content/restEndPoint`. Para essas solicitações de publicação, as informações de autenticação da solicitação de envio são usadas.
> - Para publicar dados em um servidor externo, forneça um URL. O formato da URL é `https://host:port/path_to_rest_end_point`. Certifique-se de configurar o caminho para lidar com a solicitação POST de forma anônima.

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

    ![Screenshot of the Universal Editor email configuration panel showing fields for From, To, CC, BCC, Subject, and options for external templates and attachments](/help/forms/assets/email-config-ue.png)

-->

## Mostrar uma mensagem de agradecimento personalizada no envio do Formulário adaptável {#submit-action-message-ue}

A opção Ao enviar ajuda a configurar uma mensagem de Ação de envio no envio do Formulário adaptável. Para configurar uma mensagem de Ação de envio para o seu formulário:

1. Abra o formulário adaptável no **Editor**.
1. Selecione o **[!UICONTROL Bloco de Formulários Adaptáveis]**.
1. Clique no ícone de propriedades ![propriedades](/help/forms/assets/Smock_Properties_18_N.svg).
1. Ao clicar em, você verá a seguinte opção:
   - **[!UICONTROL Ao Enviar]**: Ao Enviar ajuda você a personalizar uma mensagem a ser exibida quando um formulário for enviado. Por padrão, uma mensagem personalizada &quot;Obrigado por enviar o formulário&quot; é exibida ao usuário quando um formulário é enviado com êxito.
Você também pode personalizar a mensagem de agradecimento no envio do formulário, selecionando a opção para **[!UICONTROL Mostrar mensagem]** e adicionar/editar sua mensagem no Rich Text **Editor**.



