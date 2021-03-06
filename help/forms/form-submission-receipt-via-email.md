---
title: Envio de uma confirmação de envio de formulário por email
seo-title: Sending a form submission acknowledgement via email
description: O AEM Forms permite configurar a Ação de envio de email que envia uma confirmação para um usuário ao enviar o formulário.
seo-description: AEM Forms allows you to configure the email Submit Action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Envio de uma confirmação de envio de formulário por email {#sending-a-form-submission-acknowledgement-via-email}

## Envio de dados do formulário adaptável {#adaptive-form-data-submission}

O Adaptive Forms fornece vários recursos prontos para uso [Enviar ações](configuring-submit-actions.md) fluxos de trabalho para enviar os dados do formulário para diferentes pontos de extremidade.

Por exemplo, a variável **[!UICONTROL Enviar email]** Enviar ação envia um email após o envio bem-sucedido de um formulário adaptável. Ele também pode ser configurado para enviar os dados do formulário e o PDF no email.

Este artigo detalha as etapas para habilitar a ação Email em um Formulário adaptável e diferentes configurações fornecidas.

>[!NOTE]
>
>Também é possível usar a variável **[!UICONTROL Enviar PDF por email]** para enviar o formulário preenchido por email como anexo de PDF. As opções de configuração disponíveis para essa ação são as mesmas opções disponíveis para a variável **[!UICONTROL Enviar email]** ação. A ação PDF de email está disponível somente para o Forms adaptável baseado em XFA

## Enviar ação por email {#email-action}

A ação Enviar email permite que um autor envie emails automaticamente para um ou mais recipients no envio bem-sucedido de um Formulário adaptável.

<!-- >>[!NOTE]
>
>To use the Send email action, you need to configure the AEM mail service as described in [Configuring the mail service](/help/sites-administering/notification.md#configuring-the-mail-service).

### Enabling Send email action on an Adaptive Form {#enabling-email-action-on-an-adaptive-form}

1. Open an Adaptive Form in **[!UICONTROL edit]** mode.

1. In the **[!UICONTROL Content]** tab, tap **[!UICONTROL Form Container]** and tap ![configure](assets/configure-icon.svg) to view the Adaptive Form properties.  

1. In the **[!UICONTROL Submission]** section, select **[!UICONTROL Send email]** from the **[!UICONTROL Submit Action]** drop-down list.  

   ![Submit Actions](assets/submission-actions.png)

1. Specify valid email IDs in the **[!UICONTROL To]**, **[!UICONTROL CC]**, and **[!UICONTROL BCC]** fields.

   Specify the subject and the body of the email in the **[!UICONTROL Subject]** and **[!UICONTROL Email Template]** fields, respectively.

   You can also specify variable placeholders in the fields, in which case, the values of the fields are processed when the form is successfully submitted by an end user. For more information, see [Using Adaptive Form field names to dynamically create email content](form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Select **[!UICONTROL Include attachments]** if the form includes file attachments and you want to attach these files in the email.

   >[!NOTE]
   >
   >If you choose the **[!UICONTROL Send PDF via Email]** option, you must select the Include attachments option.

1. Click ![save](assets/save_icon.svg) to save the changes. -->

### Uso de nomes de campos do formulário adaptável para criar conteúdo de email dinamicamente {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Os nomes de campos em um formulário adaptável são chamados de espaços reservados que são substituídos pelo valor desse campo depois que um usuário envia o formulário.

No **[!UICONTROL Enviar email]** , é possível usar espaços reservados que são processados quando a ação é executada. Isso implica que os cabeçalhos do email (como **[!UICONTROL Para]**, **[!UICONTROL CC]**, **[!UICONTROL CCO]**, **[!UICONTROL Assunto]**) são geradas quando o usuário envia o formulário.

Para definir um espaço reservado, especifique `${<field name>}` em um campo depois de selecionar **[!UICONTROL Enviar email]** como Ação de envio.

Por exemplo, se o formulário contiver a variável **[!UICONTROL Endereço de email]** campo, nome `email_addr`, para capturar a ID do email de um usuário, é possível especificar o seguinte na variável **[!UICONTROL Para]**, **[!UICONTROL CC]** ou **[!UICONTROL CCO]** campos.

`${email_addr}`

Quando um usuário envia o formulário, um email é enviado para a ID de email inserida na variável `email_addr` do formulário.

>[!NOTE]
>
>Você pode encontrar o nome de um campo na variável **[!UICONTROL Editar]** para o campo.

Os marcadores de posição de variável também podem ser usados na variável **[!UICONTROL Assunto]** e **[!UICONTROL Modelo de email]** campos.

Por exemplo:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Os campos em painéis repetíveis não podem ser usados como espaços reservados variáveis.

