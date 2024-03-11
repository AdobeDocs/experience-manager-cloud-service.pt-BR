---
title: Visão geral do AEM Forms Edge Delivery Services
description: O AEM Forms Edge Delivery Services foi criado para desempenho máximo, permitindo que você visualize o futuro da coleta de dados simplificada e do engajamento do usuário.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 5cf8abe43987d145b302228877a38615f21ffd27
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# AEM Forms Edge Delivery Services

O AEM Forms Edge Delivery Services é um conjunto combinável de serviços que permite um ambiente de desenvolvimento rápido, em que os autores podem atualizar e publicar rapidamente e novos formulários são lançados rapidamente.

O AEM Forms Edge Delivery Services oferece experiências de formulários excepcionais que impulsionam o engajamento e as conversões, permitindo experiências de alto impacto que são fáceis de criar e desenvolver.

Esses serviços permitem:

* **Crie experiências de inscrição com ferramentas de sua escolha:** Aumente a eficiência da criação desvinculando as fontes de conteúdo. Você pode usar a criação baseada em documentos (Microsoft SharePoint ou Google Drive) e a criação do AEM (Adaptive Forms Editor). Dessa forma, você pode trabalhar com várias fontes de conteúdo no mesmo formulário e usar suas ferramentas de criação preferidas, como o Microsoft Excel, o Google Sheets ou o Adaptive Forms Editor.

* **Ofereça experiências excepcionais de inscrição digital:** Ofereça experiências de Inscrição digital que são carregadas e renderizadas rapidamente. Tempos de carregamento mais rápidos e experiência otimizada do usuário contribuem para taxas mais altas de conclusão e conversão de formulários.

* **Usar conjunto de ferramentas para desenvolvedores:** O AEM Forms usa o HTML simples, o CSS moderno e o JavaScript padrão para criar experiências excepcionais, evitando a curva de aprendizado íngreme de uma estrutura específica. Um desenvolvedor com habilidades básicas de desenvolvimento na Web pode personalizar e criar facilmente componentes e experiências de formulários. Não há necessidade de aguardar a execução de um pipeline. Basta fazer o check-in do código no Github e suas alterações estarão ativas.

## Visão geral do AEM Forms Edge Delivery Services {#edge-overview}

O diagrama a seguir ilustra como você pode editar formulários no Microsoft Excel ou no Google Sheets (edição baseada em documentos) e publicar no Edge Delivery Services. Ela também mostra o método de publicação AEM usando o Editor Forms adaptável.

![Arquitetura de entrega de borda](/help/edge/assets/AEM-forms-with-EDS-publishing.png)

Os serviços de entrega de borda da AEM Forms são um conjunto combinável de serviços que permitem um alto grau de flexibilidade na maneira como você cria formulários no seu site. Você pode usar a gestão de conteúdo do AEM com [Criação no AEM](/help/forms/creating-adaptive-form-core-components.md) bem como [criação baseada em documento](/help/edge/docs/forms/create-forms.md).

Por exemplo, você cria formulários diretamente no Microsoft Excel ou no Google Sheets e essas planilhas são transformadas em formulários para seu site. Qualquer novo conteúdo de formulário, como um novo campo de formulário, é disponibilizado instantaneamente em seu site sem a necessidade de um processo de recriação.

O Edge Delivery Services usa o GitHub para que os clientes possam gerenciar e implantar o código diretamente do repositório do GitHub. Por exemplo, você pode escrever formulários em [Google Sheets ou Microsoft Excel](/help/edge/docs/forms/create-forms.md) e os componentes de seus formulários podem ser desenvolvidos usando CSS e JavaScript no GitHub. Quando estiver pronto, você poderá usar o [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content) extensão do navegador para visualizar e publicar atualizações de conteúdo.

![Instalar o AEM Sidekick](/help/edge/assets/install-aem-sidekick.png)

O AEM Forms Edge Delivery Services fornece um bloco de formulários, conhecido como [Bloco Forms adaptável](/help/edge/docs/forms/create-forms.md) para adicionar um formulário ao site do Edge Delivery Services.

### Principais recursos de criação com base em documentos e criação de AEM

A Criação baseada em documento oferece um conjunto básico de recursos, e a Criação por AEM desbloqueia recursos adicionais, além da criação baseada em documento, permitindo que você crie formulários mais complexos e interativos. Os principais recursos da Criação baseada em documentos e da Criação por AEM são:

<!-- 

>[!BEGINTABS]

>[!TAB Document-based authoring]

Document-based authoring is a versatile option suitable for creating simple forms with essential functionalities. It allows you to integrate various input types like text fields, dropdown menus, and radio buttons, enabling you to collect user data effectively. It offers a basic version of rules to add dynamic behaviour to forms. Key features of Document-based authoring are: 

* **[HTML5-based Form Field components](/help/edge/docs/forms/form-components.md)**: AEM Forms Edge Delivery Services allow you to create user-friendly and interactive forms using form components based on HTML5 [input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">textarea</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, and <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elements. These components cater to different types of data collection and can be easily customized to fit your specific needs.  

* **Accessibility**: The fields in the form block are accessible. Each label is linked with its respective input element, and IDs are auto-generated for linking. Descriptions associated with fields are linked via the aria-describedby attribute. Keyboard navigation using the standard Tab/Shift + Tab keys is supported.

* **[Styling](/help/edge/docs/forms/style-theme-forms.md)**: Each form field has a fixed HTML structure that can be easily decorated using custom CSS or JavaScript files. Selectors for targeting fields in CSS and JS are provided based on type and name. You can easily create new selectors due to the standradized structure and style your form. 

* **Basic Rules**: Easily create logic that adjusts field visibility, validation, and behavior based on user input or predefined conditions. Rules offer a flexible and intuitive way to add intelligence to your forms, ensuring they adapt seamlessly based on user inputs.

* **Validations**: Before submission, the form is validated, and invalid fields are appropriately marked with error messages displayed to the user. Adaptive Forms Block support all the HTML form validation, supported by modern browsers, and provide additional validation mechanism like validation script, file size, file type, overall file size, and more. 

* **File Uploads**: You can add file attachment capabilities to your forms. Whether you need to gather documents, images, or other files from your users, file upload functionality serves you effortlessly. With custom handling options available, you can tailor the file upload process to suit your specific requirements.

* **reCAPTCHA**: Benefit from seamless integration of Google reCAPTCHA into your forms with our out-of-the-box (OOTB) support. Safeguard your forms against fraudulent activities, spam, and abuse, while maintaining a smooth and uninterrupted user experience. Adaptive Forms Block supports reCaptcha V3 and reCaptcha Enterprise. 

* **Send email notification on form submission**: Eliminate the hassle of manual follow-ups and ensure timely communication with our built-in email automation for form submissions. This integrated solution lets you effortlessly notify relevant parties, including sending form data, whenever someone fills out a form on your website. No need for complex configurations or additional tools – it's ready to use out of the box.

>[!TAB AEM Authoring]

AEM Authoring unlocks additional capabilities beyond the document-based authoring, empowering you to build more complex and interactive forms. In additon to the features of Document-based authoring, AEM authoring offers the following additional features:  

* Advanced Rules: Define logic-based actions within your forms. You can use rules to conditionally show or hide form sections, pre-populate fields based on user input, and perform various validations to ensure data integrity.

* Server-side extensibility: Extend the functionalities of your forms by integrating them with server-side logic. This allows you to perform complex calculations, interact with external systems, and automate specific tasks based on user actions within the form.
* Streamline workflows and data management: Leverage the power of AEM to:
    * Design user-friendly forms using AEM editors.
    * Generate a "Document of Record" for secure and tamper-proof archiving of submitted data.
    * Facilitate e-signing with Adobe Sign for a smooth and secure signing experience.
    * Automate business processes through AEM workflows, triggering actions based on form submissions.
    * Effortlessly integrate with various data sources, enabling seamless data flow and exchange.

>[!ENDTABS]



## Start creating forms

-->

#### Recursos de criação com base em documento

A Criação baseada em documento permite criar formulários usando ferramentas familiares, como o Microsoft Excel ou o Google Sheets. Esses formulários oferecem as seguintes funcionalidades:

* Componentes acessíveis para uma experiência simples.
* Estrutura de HTML padronizada para renderização consistente.
* Regras e validações para garantir a precisão dos dados.
* Opções de anexo de arquivo para coleta de informações adicionais.
* Integração do Google reCAPTCHA para proteção contra spam.
* Capacidade de criar componentes de formulário personalizados para necessidades específicas.
* Envie dados de formulário diretamente para o Microsoft Excel ou o Google Sheets ou endereços de email.

#### Recursos de criação do AEM

A criação de AEM (usando o Editor Forms adaptável) fornece uma interface WYSIWYG para criar formulários e oferece todos os recursos da criação baseada em documentos, além de uma grande variedade de recursos adicionais:

* Editor de regras avançado para criar lógica complexa.
* Extensibilidade do lado do servidor para funcionalidades personalizadas.
* Experiência de edição WYSIWYG para facilitar a criação e a visualização de formulários.
* Funcionalidade de documento de registro para criar arquivos à prova de violação de dados enviados.
* Integração com o Adobe Sign para assinaturas eletrônicas.
* Integração com o Adobe Workfront Fusion para acionar cenários do Adobe Workfront Fusion no envio do formulário.
* Integração com várias fontes de dados para pré-preencher formulários e enviar dados.
* Modelo de dados de formulário para definir a estrutura de dados e as interações com várias fontes de dados.
* Capacidade de configurar várias ações de envio para manipular envios de formulários, incluindo o envio de dados para o Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics e muitas outras fontes de dados.

Basicamente, a criação de AEM se baseia na base da criação com base em documentos, fornecendo um kit de ferramentas mais avançado para criar e gerenciar formulários complexos.

## Começar a criar formulários

* [Introdução ao AEM Forms Edge Delivery Services](/help/edge/docs/forms/tutorial.md)
* [Criar um formulário usando o Google Sheets ou o Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Configure seus arquivos do Google Sheets ou do Microsoft Excel para começar a aceitar dados&#x200B;](/help/edge/docs/forms/submit-forms.md)
* [Publicar seu formulário e começar a coletar dados](/help/edge/docs/forms/publish-forms.md)
* [Personalize a aparência de seus formulários&#x200B;](/help/edge/docs/forms/style-theme-forms.md)
* [Adicionar seções repetíveis a um formulário&#x200B;](/help/edge/docs/forms/repeatable-forms.md)
* [Mostrar uma mensagem de agradecimento personalizada após o envio do formulário&#x200B;](/help/edge/docs/forms/thank-you-page-form.md)
* [Componentes de bloco de formulário adaptável e suas propriedades](/help/edge/docs/forms/form-components.md)



<!-- 

## Start creating forms

<div>

  <style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using eds forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an eds form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Customize a theme</b>
        </a>
        <p>Create a consistent brand image by applying the same theme across forms.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Add validations to form fields" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Apply field validations</b>
        </a>
        <p>Reduce errors and frustration by checking form inputs for proper formatting.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Use rules to add dynamic behaviour to a form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use rules to add dynamic behaviour to a form</b>
        </a>
        <p>Reuse preconfigured fragments across multiple forms.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Add repeatable sections</b>
        </a>
        <p>Effortlessly create and add repeatable sections to a form.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Create custom forms components using standard JavaScript and CSS"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create custom components</b>
        </a>
        <p>Use standard JavaScript and CSS to create components and themes.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an EDS Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->