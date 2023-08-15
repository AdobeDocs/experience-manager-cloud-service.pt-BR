---
title: Envio de uma confirmação de envio de formulário por email
description: O AEM Forms permite configurar a Ação enviar de email que envia uma confirmação para um usuário sobre o envio do formulário.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# Envio de uma confirmação de envio de formulário por email {#sending-a-form-submission-acknowledgement-via-email}

## Envio de dados do formulário adaptável {#adaptive-form-data-submission}

O Forms adaptável fornece vários recursos prontos para uso [Ações de envio](configuring-submit-actions.md) fluxos de trabalho para enviar os dados de formulário para diferentes endpoints.

Por exemplo, a variável **[!UICONTROL Enviar e-mail]** A Ação de envio envia um email ao enviar um Formulário adaptável com êxito. Ele também pode ser configurado para enviar os dados do formulário e o PDF no email.

Este artigo detalha as etapas para habilitar a ação de Email em um Formulário adaptável e as diferentes configurações que ele fornece.

>[!NOTE]
>
>Você também pode usar a variável **[!UICONTROL Enviar PDF por e-mail]** opção para enviar o formulário preenchido por email como um anexo PDF. As opções de configuração disponíveis para esta ação são as mesmas que as opções disponíveis para a **[!UICONTROL Enviar e-mail]** ação. A ação PDF de email está disponível somente para o Adaptive Forms baseado em XFA

## Enviar ação de email {#email-action}

A ação Enviar email permite que um autor envie email automaticamente para um ou mais recipients no envio bem-sucedido de um Formulário adaptável.

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

### Utilização de nomes de campos do Formulário adaptável para criar conteúdo de email dinamicamente {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Os nomes de campos em um Formulário adaptável são chamados de espaços reservados que são substituídos pelo valor desse campo depois que um usuário envia o formulário.

No **[!UICONTROL Enviar e-mail]** , é possível usar espaços reservados que são processados quando a ação é executada. Isso implica que os cabeçalhos do email (como **[!UICONTROL Para]**, **[!UICONTROL CC]**, **[!UICONTROL CCO]**, **[!UICONTROL Assunto]**) são gerados quando o usuário envia o formulário.

Para definir um espaço reservado, especifique `${<field name>}` em um campo depois de selecionar **[!UICONTROL Enviar e-mail]** como a Ação enviar.

Por exemplo, se o formulário contiver a variável **[!UICONTROL Endereço de email]** campo, nomeado `email_addr`, para capturar a ID de email de um usuário, você pode especificar o seguinte na **[!UICONTROL Para]**, **[!UICONTROL CC]** ou **[!UICONTROL CCO]** campos.

`${email_addr}`

Quando um usuário envia o formulário, um email é enviado para a ID de email inserida na `email_addr` do formulário.

>[!NOTE]
>
>É possível encontrar o nome de um campo no **[!UICONTROL Editar]** para o campo.

Espaços reservados para variáveis também podem ser usados no **[!UICONTROL Assunto]** e **[!UICONTROL Modelo de e-mail]** campos.

Por exemplo:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Os campos em painéis repetíveis não podem ser usados como espaços reservados para variáveis.

