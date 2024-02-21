---
title: Visão geral do serviço de entrega de borda da AEM Forms
description: O serviço de entrega de borda da AEM Forms foi criado para oferecer desempenho máximo, permitindo que você visualize o futuro da coleta de dados simplificada e do envolvimento do usuário.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 9c084461f5a99f2417b5cc34e851f703fe328f7d
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---


# Serviço de entrega de borda do AEM Forms {#aem-forms-edge-delivery-service-overview}

O Serviço de entrega de borda da AEM Forms é um serviço de composição oferecido pelo Adobe que permite criar e fornecer formulários web de alto impacto e desempenho rápido. Esse serviço combinável integra-se perfeitamente ao Adobe Experience Manager (AEM) para capacitá-lo a projetar, criar e implantar formulários web de alto impacto e velocidade surpreendente com um fluxo de trabalho intuitivo e eficiente.

O Serviço de entrega de borda da AEM Forms ajuda você a:

* **Formas de artesanato visualmente deslumbrante**: corte os designs insípidos e cortadores de cookies e encante os usuários com formas dinâmicas e modernas que refletem a identidade da sua marca. Aproveite componentes pré-criados ou crie seus próprios componentes personalizados para dar vida à sua visão de forma rápida e fácil.

* **Crie formulários com a pontuação perfeita do farol**: crie formulários que carregam e renderizam rapidamente, mesmo em conexões de Internet lentas. Carregamentos mais rápidos e experiência otimizada do usuário contribuem para taxas mais altas de preenchimento de formulários e taxas de conversão aprimoradas.

* **Simplificar a criação e os envios**: crie formulários usando ferramentas familiares, como o Microsoft Excel ou o Google Sheets, em vez dos ambientes de criação tradicionais. Envie formulários diretamente para o Microsoft Excel ou o Google Sheets e use o ecossistema para processar facilmente os dados enviados.

## Introdução ao Serviço de entrega de borda da AEM Forms

<div>

<style>
    .card-container {
        width: calc(33% - 10px);
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
            <br><b style="margin-top: 5px;">Criar um formulário</b>
        </a>
        <p>Crie formulários que são carregados e renderizados de forma rápida e automática em dispositivos móveis.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Adicionar validações a campos de formulário" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Aplicar validações de campo</b>
        </a>
        <p>Reduza erros e frustrações verificando as entradas do formulário para obter a formatação adequada.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Usar fragmentos de formulário em um formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Criar fragmentos de formulário</b>
        </a>
        <p>Reutilizar fragmentos pré-configurados em vários formulários.</p>
    </div>
    <!-- Repeat the same structure for other cards -->

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
  <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
          <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Traduzir um formulário EDS" style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Traduzir um formulário</b>
      </a>
      <p>Estenda o alcance de seus formulários mantendo os custos sob controle.</p>
  </div>
  <div class="card-container">
      <a href="/help/edge/docs/forms/style-theme-forms.md">
          <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Aplicar estilos ou temas a um formulário eds" style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Personalizar um tema</b>
      </a>
      <p>Crie uma imagem de marca consistente aplicando o mesmo tema em vários formulários.</p>
  </div>
  <div class="card-container">
    <a href="/help/edge/docs/forms/repeatable-forms.md">  
      <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Adicionar seções que podem ser repetidas a um Formulário EDS" alt="Usar fragmentos de formulário em um formulário EDS" style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Adicionar seções repetíveis</b>
      </a>
      <p>Crie e adicione facilmente seções repetíveis a um formulário.</p>
  </div>


<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
  <div class="card-container">
    <a href="/help/edge/docs/forms/custom-components-forms.md"> 
      <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Criar componentes de formulários personalizados usando JavaScript e CSS padrão"  style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Criar componentes personalizados</b>
      </a>
      <p>defina JavaScript e CSS padrão para criar componentes e temas.</p>
  </div>
  <div class="card-container">
    <a href="/help/edge/docs/forms/recaptacha-forms.md">  
      <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Usar reCAPTCHA em um formulário EDS" style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Usar reCAPTCHA</b>
      </a>
      <p>Use a integração OTB reCAPTCHA para uma proteção robusta contra spam e bot.</p>
  </div>
  <div class="card-container">
    <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
      <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Enviar formulário" alt="Usar fragmentos de formulário em um formulário EDS" style="border-radius: 5px;"> </b>
          <br><b style="margin-top: 5px;">Enviar formulário para planilha</b>
      </a>
      <p>Envie formulários diretamente para o Microsoft Excel ou o Google Sheets.</p>
  </div>
</div>
</div>

</div>
<!-- Repeat the same structure for other cards -->

</br>

<!-- 
<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: 5px;">
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
       <a href="/help/edge/docs/forms/create-forms.md"> <img src="/help/edge/assets/smock_devices_18_n.svg"alt="Create a form using eds forms" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;"> Create a form</b> </a>
        <p> Create forms that that load and render quickly and automatically reflows on mobile devices.</p> <a href="/help/edge/docs/forms/create-forms.md"> </a>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/validate-forms.md"> <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Add validations to form fields" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Apply field validations</b> </a>
        <p>Reduce errors and frustration by checking form inputs for proper formatting.</p>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/form-fragments.md">  <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Use Form Fragments in an EDS Form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Create form fragments</b> </a>
        <p>Reuse preconfigured fragments across multiple forms.</p>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/translate-forms.md">  <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an EDS Form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Translate a form </b> </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/style-theme-forms.md">  <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an eds form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Customize a theme</b> </a>
        <p>Create a consistent brand image by applying same theme across forms. </p>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an EDS Form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Add repeatable sections</b> </a>
        <p>Effortlessly create and add repeatable sections to a form.</p>
    </div>
   <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
         <a href="/help/edge/docs/forms/custom-components-forms.md"> <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Create custom forms components using standard JavaScript and CSS" style="width: 75px, Height: 50px; border-radius: 5px;">  
        <b style="margin-top: 10px;">Create custom components</b> </a>
        <p>Use standard JavaScript and CSS to create components and themes.</p>
    </div>
    <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
         <a href="/help/edge/docs/forms/recaptacha-forms.md">  <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an EDS Form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Use reCAPTCHA</b> </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>
        <div style="width: 30%; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 5px; padding: 10px; box-sizing: border-box;">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" style="width: 75px, Height: 50px; border-radius: 5px;"> 
        <b style="margin-top: 10px;">Submit form to spreadsheet</b> </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
    
</div>

-->








