---
title: Mostrar uma mensagem de agradecimento personalizada após o envio do formulário
description: Saiba como configurar páginas de agradecimento e redirecionamento para o Bloqueio do Forms para otimizar a experiência do usuário e simplificar as jornadas do usuário.
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 3%

---

# Mostrar uma mensagem de agradecimento personalizada após o envio do formulário

Depois que um usuário envia um formulário, é crucial fornecer uma experiência perfeita por meio de uma mensagem de agradecimento. Isso não só confirma o envio bem-sucedido, como também aumenta a satisfação do usuário e o orienta ainda mais em sua jornada.

## Configuração de uma mensagem de agradecimento personalizada

O comportamento padrão do bloco adaptável do Forms é exibir a seguinte mensagem de agradecimento no envio. A mensagem é exibida na parte superior do formulário.

![mensagem de agradecimento padrão](/help/edge/assets/thank-you-message.png)


Siga as etapas abaixo para configurar uma mensagem de agradecimento personalizada para o bloco adaptável do Forms:

1. Acesse o projeto do AEM no computador local ou no repositório do GitHub.

1. Navegue até [Pasta do projeto AEM]\blocks\form\submit.js para editar.

1. Localize o seguinte código

   ```JavaScript
       thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Thanks for your submission';
   ```

1. Substitua a mensagem padrão pela mensagem personalizada. Por exemplo,


   ```JavaScript
       thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Your submission has been received and noted.';
   ```


1. Salve o arquivo. Confirme o arquivo atualizado no repositório GitHub. Agora, ao enviar um formulário, a mensagem de agradecimento personalizada é exibida. Por exemplo,

![Mensagem de agradecimento personalizada](/help/edge/assets/custom-thank-you-message.png)

<!-- 

* **Thank you message**: A thank you message is a cornerstone of user experience, offering reassurance and conveying important information while reinforcing brand identity. It serves as a direct acknowledgment of the user's action, fostering a sense of completion and satisfaction.

* **Redirect**: A redirect plays a pivotal role in steering users towards relevant destinations, optimizing engagement, and ultimately boosting conversion rates. By seamlessly guiding users to the next step in their journey, a redirect ensures a smooth navigation experience. For example, redirecting user to payments page after collecting initial details. 

In the Adaptive Forms Block, the default behavior is to display a thank you message. However, you have the flexibility to tailor this experience to meet your specific needs. Options include:

* [Configuring a custom thank you message to align with your brand and communication goals](#configuring-the-thank-you-page-and-message) 
* [Redirecting users to another page post-submission for further action](#redirect-users-to-another-page-post-submission)

## Redirect users to another page post-submission

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 





1. Access your AEM Edge Delivery project folder on Microsoft SharePoint or Google Workspace.
1. Create a Microsoft Word or Google Docs file named "thankyou" within your project directory.
1. Add your thank you message to the "thankyou" file. </br>
   
    ![Example thank you page](/help/edge/assets/sample-thankyou-page.png) 

1. Use AEM Sidekick to preview and publish the "thankyou" file.

 Your Adaptive Forms Block displays the "thankyou" page on form submission. 

## Redirect users to another page post-submission

By default, the Adaptive Forms Block redirects the users to the "thankyou" page. To redirect users to a page other than the default "thankyou" page, you have two options: 

* [Replace the "thankyou" page with a different page](#replace-the-existing-thankyou-page) 
* [Use website redirects for "thankyou" page redirection](#use-website-redirects-for-thankyou-page-redirection) 

### Replace the "thankyou" page

1. Open the "[EDS Project]/blocks/form/form.js" file for editing.
1. Change the `thankyou` page in the following line to page of your choice:

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'thankyou';

    ```

    For example,

    ```JavaScript

    window.location.href = form.dataset?.redirect || 'payment';
        
    ```
    
    >[!NOTE]
    >
    > Ensure that a page with the same name exists in your Edge Delivery Services project folder on either Microsoft SharePoint or Google Workspace. If the page does not exist, proceed to create and publish it.  

1. Proceed to check in the updated 'form.js' folder and its underlying files to your Edge Delivery Services project on GitHub. This update ensures that the form now redirects to the updated page as specified.

1. Ensure that the page exists in your EDS project folder and publish it.


### Use website redirects for "thankyou" page redirection

Redirecting a user to another page after form submission can enhance user experience by providing relevant information, confirming actions, and guiding users towards desired outcomes. For example, 

* after a user completes a purchase form, they are redirected to a payment page to complete the transaction securely. 
* upon submitting a registration form for an event or webinar, users are redirected to a confirmation page displaying event details, such as date, time, and location.

To redirect the "thankyou" page to a different page, use the [website redirects](https://www.aem.live/docs/redirects) spreadsheet. 

-->

## Consulte também:

{{see-more-forms-eds}}