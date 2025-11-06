---
title: Visão geral do Edge Delivery Services para AEM Forms
description: Crie e forneça formulários de alto desempenho no Adobe Experience Manager Edge Delivery Services, com ênfase na abordagem de criação do Editor universal.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---


# Edge Delivery Services para AEM Forms


O Edge Delivery Services for AEM Forms é um conjunto combinável de serviços que permite um ambiente de desenvolvimento rápido, em que os autores podem atualizar, publicar e lançar novos formulários rapidamente. Esses serviços oferecem experiências de formulários excepcionais e de alto impacto que impulsionam o engajamento e as conversões. Essas experiências de formulários são fáceis de criar e desenvolver.

Esses serviços permitem:

- **Crie experiências de inscrição com ferramentas de sua escolha:** Aumente a eficiência da criação dissociando as fontes de conteúdo. Você pode usar a Criação baseada em documento (Microsoft SharePoint ou Google Drive), a Criação no WYSIWYG (Universal Editor ou Adaptive Forms Editor) prontas para uso. Você pode trabalhar com várias fontes de conteúdo no mesmo site de formulários e usar suas ferramentas de criação preferidas, como o Microsoft Excel, Google Sheets, Universal Editor ou Adaptive Forms Editor.

- **Ofereça experiências excepcionais de Inscrição Digital:** forneça experiências de Inscrição Digital que são carregadas e renderizadas de forma rápida e contínua, monitorando o desempenho de seus formulários por meio da Telemetria Operacional. Tempos de carregamento mais rápidos e experiência otimizada do usuário contribuem para taxas mais altas de conclusão e conversão de formulários.

- **Usar conjunto de ferramentas compatível com o desenvolvedor:** Edge Delivery Services for AEM Forms
O usa o HTML simples, o CSS moderno e o JavaScript padrão para criar experiências excepcionais, evitando a curva de aprendizado acentuada de uma estrutura específica. Um desenvolvedor com habilidades básicas de desenvolvimento na Web pode personalizar e criar facilmente componentes e experiências de formulários. Não há necessidade de aguardar a execução de um pipeline. Basta fazer o check-in do código no GitHub e suas alterações estarão ativas.

## Escolha de um método de criação


O Adobe Experience Manager (AEM) Edge Delivery Services (EDS) permite oferecer experiências da Web ultrarrápidas e altamente escaláveis. Este guia explica **como criar e publicar formulários para essas experiências**, com uma hierarquia de recomendação clara:

- **Editor Universal (UE) - a melhor opção para a maioria das equipes**
- **Criação Baseada em Documentos (Docs/Folhas) - Ideal para formulários simples e rápidos**
- **Criação de documentos (DA) - Use para inserir formulários em páginas criadas pelo DA**

Ao final, você poderá escolher o método de criação correto, entender as opções de envio e seguir as próximas etapas para criar formulários prontos para produção.


| Equipe e requisitos | Método recomendado | Por que |
|--------------------|--------------------|-----|
| Profissionais de marketing/designers precisam de controle visual, lógica condicional ou integrações do AEM | **Universal Editor** | Arrastar e soltar, regras avançadas, envios para FSS ou AEM Publish |
| Autores de conteúdo já trabalhando no Word/Google Docs/Sheets; captura de dados simples em planilha/email | **Criação Baseada em Documento** | Ferramentas familiares, caminho mais rápido para formulários básicos |
| Páginas do site criadas em **Document Authoring (DA)** | **Incorpore** um formulário UE ou Baseado em Doc na página do DA | O DA não cria formulários por conta própria |


## Métodos de criação em detalhes

### Editor universal

<!--
<span class="preview"> This is a pre-release feature available through our <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=pt-BR#new-features">pre-release channel</a>. </span>
-->

O [Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) é uma ferramenta de criação visual, do tipo arrastar-e-soltar, para profissionais de marketing e designers que combina velocidade e poder de nível empresarial:

- Edição em tempo real do WYSIWYG e visualizações de dispositivos.
- Integração direta com ativos, workflows e modelos de dados de formulário (FDM) do AEM.
- Entrega contínua para desenvolvedores para componentes personalizados em JS/CSS básicos.
- Editor de regras avançado para criar lógica complexa.
- Extensibilidade do lado do servidor para funcionalidades personalizadas.
- Experiência de edição do WYSIWYG para facilitar a criação e a visualização de formulários.
- Funcionalidade de documento de registro para criar arquivos à prova de violação de dados enviados.
- Integração com o Adobe Sign para assinaturas eletrônicas.
- Integração com o Adobe Workfront Fusion para acionar cenários do Adobe Workfront Fusion no envio do formulário.
- Integração com várias fontes de dados para pré-preencher formulários e enviar dados.
- Modelo de dados de formulário (FDM) para definir a estrutura de dados e as interações com várias fontes de dados.
- Capacidade de escolher entre várias ações de envio para manipular envios de formulários, incluindo o envio de dados para o Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics e muitas outras fontes de dados.
- Enviar usando o Serviço de envio do Forms (FSS) ou as ações de envio do AEM Publish

**Recomendação**: inicie todos os novos projetos de formulário com o Universal Editor, a menos que sua equipe seja 100% centrada em documentos e o formulário seja muito básico.


### Criação baseada em documento (usando documentos do Microsoft ou folhas do Google)

A [Criação baseada em documentos](/help/edge/docs/forms/tutorial.md) é mais adequada para criar formulários simples e de baixa complexidade usando ferramentas familiares, como o Microsoft Word, Google Docs ou Google Sheets. Esse método é ideal para equipes de conteúdo que exigem uma maneira rápida e direta de criar formulários.

- Componentes acessíveis para uma experiência simples.
- Estrutura padrão do HTML para renderização consistente.
- Regras e validações para garantir a precisão dos dados.
- Opções de anexo de arquivo para coleta de informações adicionais.
- Integração do Google reCAPTCHA para proteção contra spam.
- Capacidade de criar componentes de formulário personalizados para necessidades específicas.
- Envie dados de formulário diretamente para o Microsoft Excel ou o Google Sheets ou endereços de email.
- Monitorar o desempenho de formulários por meio da Telemetria Operacional


### Incorporação do Forms na Criação de documentos (DA)

A Criação de documentos (DA) foi projetada para criar conteúdo de página estruturada e não oferece suporte à criação de formulários nativos. Para adicionar um formulário a uma página criada pelo DA, você pode criar o formulário usando o **Editor Universal** (recomendado) ou Criação Baseada em Documento e incorporar o formulário à página Criação de Documento.

## Publicação do Edge Delivery Services Forms {#edge-overview}

O diagrama a seguir ilustra como você pode editar formulários no Microsoft Excel ou no Google Sheets (Criação baseada em documento) e publicar no Edge Delivery Services. Ela também mostra o método de publicação do AEM usando a Criação no WYSIWYG (Editor universal).

![Publicar no Edge Delivery Services e no AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)


<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |
-->

## Próximas etapas

- [Recursos e funcionalidades do Universal Editor para Edge Delivery Services para Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
- [Criar o primeiro formulário usando o Editor Universal](/help/edge/docs/forms/universal-editor/create-forms.md)
- [Crie seu primeiro formulário usando o Google Sheets ou o Microsoft Excel](/help/edge/docs/forms/tutorial.md).
- [Incorporar o Forms na Criação de Documentos (DA)](https://www.aem.live/developer/da-tutorial)


Agora você está pronto para criar seu primeiro formulário de alto desempenho com o AEM Edge Delivery Services.

<!--
## Start creating forms

- [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
- [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
- [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
- [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
- [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
- [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
- [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
- [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
- [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

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
