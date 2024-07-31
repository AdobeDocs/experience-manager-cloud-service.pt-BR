---
title: Mostrar uma mensagem de agradecimento personalizada após o envio do formulário
description: Saiba como configurar páginas de agradecimento e redirecionamento para o Bloqueio do Forms para otimizar a experiência do usuário e simplificar as jornadas do usuário.
feature: Edge Delivery Services
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Mostrar uma mensagem de agradecimento personalizada após o envio do formulário

Depois que um usuário envia um formulário, é crucial fornecer uma experiência perfeita por meio de uma mensagem de agradecimento. Ele não só confirma o envio bem-sucedido, mas também aumenta a satisfação do usuário e o orienta ainda mais em sua jornada.

* **Mensagem de agradecimento**: uma mensagem de agradecimento é a base da experiência do usuário, oferecendo tranquilidade e transmitindo informações importantes, além de reforçar a identidade da marca. Ele serve como um reconhecimento direto da ação do usuário, fomentando uma sensação de conclusão e satisfação.

* **Redirecionar**: um redirecionamento tem uma função essencial na orientação dos usuários para destinos relevantes, otimizando o engajamento e, em última análise, aumentando as taxas de conversão. Ao orientar os usuários para a próxima etapa da jornada de maneira contínua, o redirecionamento garante uma experiência de navegação tranquila. Por exemplo, redirecionando o usuário para a página de pagamentos após coletar os detalhes iniciais.

O comportamento padrão do bloco adaptável do Forms é exibir a seguinte mensagem de agradecimento no envio. A mensagem é exibida na parte superior do formulário no envio bem-sucedido do formulário.

![mensagem de agradecimento padrão](/help/edge/assets/thank-you-message.png)

No entanto, você tem a flexibilidade de personalizar essa experiência para atender às suas necessidades específicas. As opções incluem:

* Mostrar uma mensagem de agradecimento personalizada após o envio do formulário
* Redirecionar usuários para outra página após o envio para obter mais ações

>[!NOTE]
>
> Você pode consultar a [planilha de consulta](/help/edge/docs/forms/assets/enquiry.xlsx) a seguir para personalizar a mensagem de agradecimento de acordo com suas necessidades.

## Configurar uma mensagem de agradecimento personalizada

Caso deseje mostrar uma mensagem de agradecimento personalizada após o envio bem-sucedido do formulário, você pode configurar sua planilha para exibi-la.

Siga as etapas abaixo para configurar uma mensagem de agradecimento personalizada para o bloco adaptável do Forms:

1. Vá para a pasta do projeto do Edge Deliver no Microsoft SharePoint ou Google Workspace e abra a planilha.
1. Adicione uma mensagem de agradecimento personalizada na coluna `value` para o tipo de campo `submit` na planilha.

   ![Mensagem de agradecimento personalizada](/help/edge/docs/forms/assets/thankyou-custommessage.png)

   Por exemplo, adicione a mensagem `Submission Successful!` na coluna `value` para o tipo de campo `submit`.

1. Visualize e publique a planilha usando o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Mensagem de agradecimento personalizada](/help/edge/docs/forms/assets/customized-thank-you-message.png)

## Redirecionar usuários para outra página após o envio

Redirecionar um usuário para outra página após o envio do formulário pode aprimorar a experiência do usuário fornecendo informações relevantes, confirmando ações e orientando os usuários para os resultados desejados. Por exemplo,

* depois que um usuário conclui um formulário de compra, ele é redirecionado a uma página de pagamento para concluir a transação de forma segura.
* ao enviar um formulário de inscrição para um evento ou webinário, os usuários são redirecionados para uma página de confirmação exibindo detalhes do evento, como data, hora e local.

Siga as etapas abaixo para redirecionar os usuários para outra página:

1. Vá para a pasta do projeto do Edge Deliver no Microsoft SharePoint ou Google Workspace e abra a planilha.
1. Cole a URL na coluna `value` para o tipo de campo `submit` na planilha para redirecionar o usuário no envio bem-sucedido do formulário.
Para redirecionar a página para uma página diferente, use a URL da página [Documentação do Edge Delivery](https://www.aem.live/docs/).

   ![URL de redirecionamento de agradecimento](/help/edge/docs/forms/assets/thankyou-redirecturl.png)

1. Visualize e publique a planilha usando o [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content).

   ![Redirecionar mensagem de agradecimento](/help/edge/docs/forms/assets/thankyou-redirectpage.gif)

Você também pode criar um novo arquivo de documento e adicionar sua URL de visualização na coluna `value` para o tipo de campo `submit`.

Depois que um usuário enviar um formulário, é importante fornecer uma mensagem de agradecimento clara. Ele confirma que o envio foi bem-sucedido e melhora a satisfação do usuário.

## Consulte também:

{{see-more-forms-eds}}

<!--
## Configuring a custom thank you message

The default behavior of Adaptive Forms Block is to display the following thank you message on submission. The message is displayed on the top of the form. 

![default thank you message](/help/edge/assets/thank-you-message.png)


Follow the below steps to configure a custom thank you message for your Adaptive Forms Block:

1. Access your AEM Project on your local machine or GitHub repository.

2. Navigate to [AEM Project Folder]\blocks\form\submit.js file for editing.

3. Locate the following code 

    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Thanks for your submission';

    ```

4. Replace the default message with your custom message. For example, 


    ```JavaScript

        thankYouMessage.innerHTML = payload?.body?.thankYouMessage || 'Your submission has been received and noted.';

    ```


1. Save the file. Commit the updated file to your GitHub Repository. Now, when you submit a form, the custom thank you message is displayed. For example,

![Custom thank you message](/help/edge/assets/custom-thank-you-message.png)

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



## See also

{{see-more-forms-eds}}