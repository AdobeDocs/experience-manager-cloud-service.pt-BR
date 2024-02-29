---
title: Visão geral do serviço de entrega de borda da AEM Forms
description: O serviço de entrega de borda da AEM Forms foi criado para oferecer desempenho máximo, permitindo que você visualize o futuro da coleta de dados simplificada e do envolvimento do usuário.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e21b681b12e90110436c7319797809c8d6b75eea
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---


# Serviço de entrega de borda do AEM Forms

Simplifique a criação de formulários e impulsione taxas de conclusão mais altas com o Serviço de entrega de borda do Adobe AEM Forms. Esse serviço eficiente e combinável permite que você crie formulários de nível empresarial com desempenho e apelo visual excepcionais. O AEM prioriza a experiência do usuário e seus objetivos comerciais, garantindo tempos de carregamento extremamente rápidos e maior conclusão de formulários.

![Principais recursos do EDS Forms](/help/edge/assets/eds-forms-key-features.png){width="70%"}

Você pode usar o serviço para:

* **Usuários do Captivate com formulários impressionantes**: crie formulários complexos e envolventes com facilidade usando uma biblioteca de componentes pré-construídos. Integre facilmente o reCAPTCHA, envie formulários diretamente por email e permita uploads de arquivos ininterruptos para soluções de armazenamento seguras, como Sharepoint, Armazenamento do Azure e Amazon S3. Crie até mesmo seus próprios componentes de formulários personalizados para dar vida à sua visão exclusiva.

* **Crie experiências de inscrição digital com as ferramentas de sua escolha**: aumente a eficiência da criação ao dissociar as fontes de conteúdo. Você pode usar a criação com base em documento (Microsoft 365 e Google Workspace) e a criação de AEM (editores de AEM). Dessa forma, você pode trabalhar com várias fontes de conteúdo no mesmo site e usar suas ferramentas de criação preferidas, como o Microsoft Excel, o Google Sheets ou o Adaptive Forms Editor.

* **Crie formulários com a pontuação perfeita do Lighthouse**: crie formulários que carregam e renderizam rapidamente, mesmo em conexões de Internet lentas. Carregamentos mais rápidos e experiência otimizada do usuário contribuem para taxas mais altas de preenchimento de formulários e taxas de conversão aprimoradas.


<!-- >
* **Captivate users with stunning forms**: 
Build complex and engaging forms with ease using a library of pre-built components. Easily integrate reCAPTCHA, submit forms directly to email, and allow seamless file uploads to secure storage solutions like Sharepoint, Azure Storage, and Amazon S3. Even create your own custom forms components to bring your unique vision to life. 

    ![Enrollment forms](/help/edge/assets/enrollment-form.png)

* **Build forms with perfect lighthouse score**: Build forms that load and render quickly, even on slow internet connections. Faster loading times and optimized user experience contribute to higher form completion rates and improved conversion rates.

    ![perfect lighthouse score for your forms](/help/edge/assets/lighthouse-forms.png)

* **Create digital enrollment experiences with tools of your choice**: Increase authoring efficiency by decoupling content sources. Out of the box you can use both AEM authoring and document-based authoring. As such, you can work with multiple content sources on the same website and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, or AEM Editors.

    ![Edge Delivery forms authoring tools](/help/edge/assets/edge-delivery-forms-authoring-tools.png)
    
<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
>[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## Começar a criar formulários

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Criar um formulário usando o eds forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Criar um formulário usando o Google Sheets ou o Microsoft Excel</b>
        </a>
        <p>Crie formulários que são carregados e renderizados de forma rápida e automática em dispositivos móveis.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Enviar formulário" alt="Usar fragmentos de formulário em um formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Enviar formulário para planilha</b>
        </a>
        <p>Envie formulários diretamente para o Microsoft Excel ou o Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Aplicar estilos ou temas a um formulário eds" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Personalizar um tema</b>
        </a>
        <p>Crie uma imagem de marca consistente aplicando o mesmo tema em vários formulários.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Adicionar validações a campos de formulário" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Aplicar validações de campo</b>
        </a>
        <p>Reduza erros e frustrações verificando as entradas do formulário para obter a formatação adequada.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Usar regras para adicionar comportamento dinâmico a um formulário" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Usar regras para adicionar comportamento dinâmico a um formulário</b>
        </a>
        <p>Reutilizar fragmentos pré-configurados em vários formulários.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Traduzir um formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Traduzir um formulário</b>
        </a>
        <p>Estenda o alcance de seus formulários mantendo os custos sob controle.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Adicionar seções que podem ser repetidas a um Formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Adicionar seções repetíveis</b>
        </a>
        <p>Crie e adicione facilmente seções repetíveis a um formulário.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Criar componentes de formulários personalizados usando JavaScript e CSS padrão"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Criar componentes personalizados</b>
        </a>
        <p>Use JavaScript e CSS padrão para criar componentes e temas.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Usar reCAPTCHA em um formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Usar reCAPTCHA</b>
        </a>
        <p>Use a integração OTB reCAPTCHA para uma proteção robusta contra spam e bot.</p>
    </div>


</div>


</br>









