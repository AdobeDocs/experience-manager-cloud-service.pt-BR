---
title: Visão geral do serviço de entrega de borda AEM Forms
description: AEM Forms Serviço de entrega de borda construído para o desempenho de pico, capacitando-o a vislumbrar o futuro de coleção de dados e engajamento do usuário simplificadas.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 1c6e44fd6652d93ba73bc2eb3604cd08eae7a33c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---


# Serviço de entrega do AEM Forms Edge

Simplifique a criação de formulários e impulsionar taxas de conclusão mais altas com o AEM Forms Serviço de Entrega de Borda da Adobe Systems. Esse serviço poderoso e composável capacita você a build formulários de nível empresarial com desempenho excepcional e apelo visual. AEM prioriza as experiência do usuário e suas metas comerciais, garantindo tempos de carregamento rápido e maior conclusão de formulário.

Você pode usar o serviço para:

* **Cative usuários com formulários impressionantes**: crie formulários complexos e envolventes com facilidade usando uma biblioteca de componentes pré-construído. Integre facilmente o reCAPTCHA, envie formulários diretamente para email e permita uploads ininterruptos de arquivos para garantir soluções armazenamento curtir Sharepoint, Azure Storage e Amazon S3. Até mesmo crie seus próprios componentes de formulários personalizados para dar vida a sua visão única.

* **Criar experiências de inscrição digital com ferramentas de sua escolha**: aumente a eficiência da criação ao dissociar conteúdo fontes. Você pode usar tanto a criação baseada em documento (Microsoft 365 e o Google Área de trabalho) quanto a criação de AEM (Editores AEM). Dessa forma, você pode trabalhar com várias conteúdo fontes no mesmo site e usar suas ferramentas de criação preferidas, como Microsoft Excel, Google Sheets ou Adaptive Forms editor.

* **Crie formulários com a pontuação** perfect Lighthouse: crie formulários que carregam e renderizam rapidamente, mesmo em conexões lentas de internet. Tempos de carregamento mais rápidos e experiência do usuário otimizados contribuem para taxas de conclusão de formulários mais altas e taxas de conversão aprimoradas.

  <div>
    <style>
    .image-container {
    width: 80%;
    text-align: center; 
    }
    .image-container img {
        width: 70%; /* Set image width to 70% of the container */
        border: .5px solid; /* Maintain the border style */
        padding: 15px; /* Maintain the padding */
    }
</style>
    <div class="image-container">
    <img src="/help/edge/assets/eds-forms-key-features.png" alt="Recursos principais do EDS Forms">
    </div>


</div>
&lt;!-- &gt;
* **Usuários do Captivate com formulários impressionantes**: 
Crie formulários complexos e envolventes com facilidade usando uma biblioteca de componentes pré-construído. Integre facilmente o reCAPTCHA, envie formulários diretamente para email e permita uploads ininterruptos de arquivos para garantir soluções armazenamento curtir Sharepoint, Azure Storage e Amazon S3. Até mesmo crie seus próprios componentes de formulários personalizados para dar vida a sua visão única.

    ![Formulários de inscrição] (/help/edge/ativos/enrollment-form.png)

* **Crie formulários com pontuação** de farol perfeita: crie formulários que carregam e renderizam rapidamente, mesmo em conexões lentas de internet. Tempos de carregamento mais rápidos e experiência do usuário otimizados contribuem para taxas de conclusão de formulários mais altas e taxas de conversão aprimoradas.

  ![pontuação de farol perfeito para seus formulários](/help/edge/assets/lighthouse-forms.png)

* **Criar experiências de inscrição digital com ferramentas de sua escolha**: aumente a eficiência da criação ao dissociar conteúdo fontes. Prontos para uso, é possível usar tanto a criação AEM como a criação baseada em documento. Dessa forma, você pode trabalhar com várias conteúdo fontes no mesmo site e usar suas ferramentas de criação preferidas, como Microsoft Excel, Google Sheets ou Editores AEM.

  ![Ferramentas de criação de formulários de entrega do Edge](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
>[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## criar formulários Início

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Criar um formulário usando formulários eds" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Criar um formulário usando o Google Sheets ou o Microsoft Excel
            </b>
        </a>
        <p>Criar formulários que carregam e renderizam reflows rapidamente e automaticamente em dispositivos móveis.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Enviar formulário" alt="Usar fragmentos de formulário em um formulário EDS" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Enviar formulário para a planilha
            </b>
        </a>
        <p>Envie formulários diretamente para Microsoft Excel ou Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Aplicar estilos ou temas para um formulário eds" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Personalizar um tema
            </b>
        </a>
        <p>Criar uma imagem de marca consistente aplicando o mesmo tema nos formulários.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Adicionar validações aos campos do formulário" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Validações de campo de Aplicar
            </b>
        </a>
        <p>Reduza erros e frustrações verificando as entradas do formulário para obter a formatação adequada.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Usar regras para adicionar comportamento dinâmico a um formulário" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Usar regras para adicionar comportamento dinâmico a um formulário
            </b>
        </a>
        <p>Reutilize fragmentos pré-configurados em vários formulários.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Traduzir um formulário EDS" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Traduzir um formulário
            </b>
        </a>
        <p>Amplie o alcance dos seus formulários mantendo os custos sob controle.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Adicionar seções repetíveis a um formulário EDS" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Adicionar seções repetíveis
            </b>
        </a>
        <p>Crie e adicione seções repetíveis sem esforço a um formulário.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Criar componentes de formulários personalizados usando JavaScript e CSS padrão"  style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Criar componentes personalizados
            </b>
        </a>
        <p>Use JavaScript e CSS padrão para criar componentes e temas.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Usar reCAPTCHA em um formulário EDS" style="border-radius: 5px;"></b><br><b style="margin-top: 5px;">Usar reCAPTCHA
            </b>
        </a>
        <p>Use a integração OOTB reCAPTCHA para proteção robusta de spam e bot.</p>
    </div>


</div>


</br>









