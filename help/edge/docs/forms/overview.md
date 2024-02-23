---
title: Visão geral do serviço de entrega de borda da AEM Forms
description: O serviço de entrega de borda da AEM Forms foi criado para oferecer desempenho máximo, permitindo que você visualize o futuro da coleta de dados simplificada e do envolvimento do usuário.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 87ed5f0aed5554f56e28f317d1399429245a2d06
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---


# Serviço de entrega de borda do AEM Forms {#aem-forms-edge-delivery-service-overview}

O Serviço de entrega de borda da AEM Forms é um serviço de composição oferecido pelo Adobe que permite criar e fornecer formulários web de alto impacto e desempenho rápido. Você pode usar o serviço para:

* **Formas de artesanato visualmente deslumbrante**: corte os designs insípidos e cortadores de cookies e encante os usuários com formas dinâmicas e modernas que refletem a identidade da sua marca. Aproveite componentes pré-criados ou crie seus próprios componentes personalizados para dar vida à sua visão de forma rápida e fácil.

* **Crie formulários com a pontuação perfeita do farol**: crie formulários que carregam e renderizam rapidamente, mesmo em conexões de Internet lentas. Carregamentos mais rápidos e experiência otimizada do usuário contribuem para taxas mais altas de preenchimento de formulários e taxas de conversão aprimoradas.

* **Simplificar a criação e os envios**: crie formulários usando ferramentas familiares, como o Microsoft Excel ou o Google Sheets, em vez dos ambientes de criação tradicionais. Envie formulários diretamente para o Microsoft Excel ou o Google Sheets e use o ecossistema para processar facilmente os dados enviados.


Esse serviço de composição é dissociado da fonte de conteúdo e oferece flexibilidade para a criação de conteúdo, permitindo que os usuários usem suas ferramentas de criação preferidas.

![Ferramentas de criação de formulários de entrega de borda](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

Os criadores de conteúdo podem aproveitar as ferramentas com as quais estão familiarizados, como o Microsoft Excel ou o Google Sheets (criação baseada em documentos), arquivos JSON (criação headless) ou o editor do AEM Forms Adaptive Forms (criação WYSIWYG), para projetar e criar seus formulários.

>[!NOTE]
>
>
> O recurso de criação WYSIWYG está disponível no programa dos primeiros usuários. Você pode escrever para aem-forms-early-adopter-program@adobe.com a partir de sua ID de e-mail oficial para participar do programa de adoção antecipada e solicitar acesso ao recurso.

## Comece com as noções básicas

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
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Adicionar validações a campos de formulário" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Aplicar validações de campo</b>
        </a>
        <p>Reduza erros e frustrações verificando as entradas do formulário para obter a formatação adequada.</p>
    </div>    <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Aplicar estilos ou temas a um formulário eds" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Personalizar um tema</b>
        </a>
        <p>Crie uma imagem de marca consistente aplicando o mesmo tema em vários formulários.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Traduzir um formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Traduzir um formulário</b>
        </a>
        <p>Estenda o alcance de seus formulários mantendo os custos sob controle.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Usar fragmentos de formulário em um formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Criar fragmentos de formulário</b>
        </a>
        <p>Reutilizar fragmentos pré-configurados em vários formulários.</p>
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
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Enviar formulário" alt="Usar fragmentos de formulário em um formulário EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Enviar formulário para planilha</b>
        </a>
        <p>Envie formulários diretamente para o Microsoft Excel ou o Google Sheets.</p>
    </div>
</div>


</br>









