---
title: Visão geral do Edge Delivery Services para AEM Forms
description: Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 4a8153ffbdbc4da401089ca0a6ef608dc2c53b22
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---

# Edge Delivery Services para AEM Forms


O Edge Delivery Services para AEM Forms é um conjunto de serviços combináveis que permite um ambiente de desenvolvimento rápido, em que os autores podem atualizar, publicar e lançar novos formulários rapidamente. Esses serviços oferecem experiências de formulários excepcionais e de alto impacto que impulsionam o engajamento e as conversões. Essas experiências de formulários são fáceis de criar e desenvolver.

Esses serviços permitem:

* **Crie experiências de inscrição com ferramentas de sua escolha:** Aumente a eficiência da criação dissociando as fontes de conteúdo. Você pode usar a Criação baseada em documento (Microsoft SharePoint ou Google Drive), a Criação WYSIWYG (Editor universal ou Editor adaptável do Forms) imediatamente. Você pode trabalhar com várias fontes de conteúdo no mesmo site de formulários e usar suas ferramentas de criação preferidas, como o Microsoft Excel, Google Sheets, Universal Editor ou Adaptive Forms Editor.

* **Ofereça experiências excepcionais de Inscrição Digital:** ofereça experiências de Inscrição Digital que carregam e renderizam de forma rápida e contínua, monitorando o desempenho de seus formulários por meio do monitoramento de uso real (RUM). Tempos de carregamento mais rápidos e experiência otimizada do usuário contribuem para taxas mais altas de conclusão e conversão de formulários.

* **Usar conjunto de ferramentas compatível com o desenvolvedor:** Edge Delivery Services para AEM Forms
O usa o HTML simples, o CSS moderno e o JavaScript padrão para criar experiências excepcionais, evitando a curva de aprendizado íngreme de uma estrutura específica. Um desenvolvedor com habilidades básicas de desenvolvimento na Web pode personalizar e criar facilmente componentes e experiências de formulários. Não há necessidade de aguardar a execução de um pipeline. Basta fazer o check-in do código no GitHub e suas alterações estarão ativas.

## Visão geral do Edge Delivery Services para AEM Forms {#edge-overview}

O Edge Delivery Services para AEM Forms permite um alto grau de flexibilidade na forma como você cria formulários no seu site. Você pode criar conteúdo e formulários com a [Criação WYSIWYG](/help/forms/creating-adaptive-form-core-components.md) e a [Criação baseada em documento](/help/edge/docs/forms/create-forms.md). Edge Delivery Services para AEM Forms
forneça um bloco de formulários, conhecido como [Bloco de Forms adaptável](/help/edge/docs/forms/create-forms.md), para adicionar um formulário ao seu site Edge Delivery Services.

Por exemplo, você cria formulários diretamente no Microsoft Excel ou no Google Sheets e essas planilhas são transformadas em formulários para seu site. Qualquer novo formulário ou conteúdo de formulário, como um novo campo de formulário, fica disponível instantaneamente em seu site sem exigir um processo de recriação.

O diagrama a seguir ilustra como você pode editar formulários no Microsoft Excel ou no Google Sheets (Criação baseada em documento) e publicar no Edge Delivery Services. Ela também mostra o método de publicação AEM usando a criação WYSIWYG (editor universal ou editor adaptável do Forms).

![Publish para Edge Delivery Services e AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

O Edge Delivery Services para AEM Forms usa o GitHub para que os clientes possam gerenciar e implantar código diretamente do repositório do GitHub. Por exemplo, você pode escrever formulários no [Google Sheets](/help/edge/docs/forms/create-forms.md) ou no [Microsoft Excel](/help/edge/docs/forms/create-forms.md) e os componentes de seus formulários podem ser desenvolvidos usando CSS e JavaScript em um repositório GitHub.

Quando os formulários estiverem prontos, você poderá usar o [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), uma extensão do navegador Chrome, para visualizar e publicar atualizações de conteúdo.

![Instalar AEM Sidekick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

A escolha entre a [Criação baseada em documento](#document-based-authoring-features) e a [Criação WYSIWYG](#wysiwyg-authoring-features) depende de seus requisitos específicos:

* Para formulários simples que apenas coletam informações básicas com alguns campos (pense em contatar-nos formulários, formulários de geração de clientes potenciais ou formulários de solicitação de serviço), e onde você precisar de conectividade rápida de dados usando uma planilha, a [Criação baseada em documento](#document-based-authoring-features) é uma boa opção. Você pode criar esses formulários da mesma forma que criaria um documento no Google Sheets ou no Microsoft Excel.

* Para formulários complexos, como formulários que exigem vários painéis, regras complexas e lógica de negócios, manipulação de dados, integração com sistemas externos ou fluxos de trabalho simplificados usando recursos de AEM, a [Criação WYSIWYG](#wysiwyg-authoring-features) é uma opção melhor.


### Principais recursos de criação com base em documento e criação WYSIWYG

A Criação baseada em documento oferece um conjunto básico de recursos, e a Criação WYSIWYG desbloqueia recursos adicionais, além da Criação baseada em documento, permitindo que você crie formulários mais complexos e interativos. Os principais recursos da Criação baseada em documento e da Criação WYSIWYG são:

#### Recursos de criação com base em documento

A Criação baseada em documento permite criar formulários usando ferramentas familiares, como o Microsoft Excel ou o Google Sheets. Esses formulários oferecem as seguintes funcionalidades:

* Componentes acessíveis para uma experiência simples.
* Estrutura de HTML padronizada para renderização consistente.
* Regras e validações para garantir a precisão dos dados.
* Opções de anexo de arquivo para coleta de informações adicionais.
* Integração do Google reCAPTCHA para proteção contra spam.
* Capacidade de criar componentes de formulário personalizados para necessidades específicas.
* Envie dados de formulário diretamente para o Microsoft Excel ou o Google Sheets ou endereços de email.
* Monitore o desempenho de seus formulários por meio do monitoramento de uso real (RUM)

#### Recursos de criação WYSIWYG

A Criação WYSIWYG fornece interfaces WYSIWYG (Universal Editor e Adaptive Forms Editor) para a criação de formulários e oferece todos os recursos da Criação baseada em documento, além de uma grande variedade de recursos adicionais:

* Editor de regras avançado para criar lógica complexa.
* Extensibilidade do lado do servidor para funcionalidades personalizadas.
* Experiência de edição WYSIWYG para facilitar a criação e a visualização de formulários.
* Funcionalidade de documento de registro para criar arquivos à prova de violação de dados enviados.
* Integração com o Adobe Sign para assinaturas eletrônicas.
* Integração com o Adobe Workfront Fusion para acionar cenários do Adobe Workfront Fusion no envio do formulário.
* Integração com várias fontes de dados para pré-preencher formulários e enviar dados.
* Modelo de dados de formulário (FDM) para definir a estrutura de dados e as interações com várias fontes de dados.
* Capacidade de escolher entre várias ações de envio para manipular envios de formulários, incluindo o envio de dados para o Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics e muitas outras fontes de dados.

Os recursos acima também estão disponíveis por meio do Editor Forms adaptável.

Basicamente, a criação WYSIWYG (Universal Editor e [Adaptive Forms Editor](/help/forms/creating-adaptive-form-core-components.md)) se baseia na [criação baseada em documentos](/help/edge/docs/forms/create-forms.md), fornecendo um kit de ferramentas mais avançado para criar e gerenciar formulários complexos.

>[!NOTE]
>
>
> O recurso de criação WYSIWYG está disponível no programa dos primeiros usuários. Caso esteja interessado, envie um email rápido do seu endereço comercial para aem-forms-ea@adobe.com para solicitar acesso ao recurso.

### Edge Delivery Services para AEM Forms

: criação, publicação e envio do Forms

Os diagramas a seguir ilustram o processo de criação, publicação e envio de formulários usando a Criação baseada em documento e a Criação WYSIWYG.

![Criação baseada em documento](/help/edge/assets/document-based-authoring-workflow.png)

![Criação WYSIWYG](/help/edge/assets/wysiwyg-authoring-workflow.png)

## Começar a criar formulários

* [Introdução aos Edge Delivery Services para AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Criar um formulário usando o Google Sheets ou o Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Configure seus arquivos do Google Sheets ou do Microsoft Excel para começar a aceitar dados&#x200B;](/help/edge/docs/forms/submit-forms.md)
* [Publish seu formulário e comece a coletar dados](/help/edge/docs/forms/publish-forms.md)
* [Personalize a aparência de seus formulários&#x200B;](/help/edge/docs/forms/style-theme-forms.md)
* [Adicionar seções repetíveis a um formulário&#x200B;](/help/edge/docs/forms/repeatable-forms.md)
* [Mostrar uma mensagem de agradecimento personalizada após o envio do formulário&#x200B;](/help/edge/docs/forms/thank-you-page-form.md)
* [Componentes de bloco de formulário adaptável e suas propriedades](/help/edge/docs/forms/form-components.md)
* [Monitoramento de uso real](https://www.aem.live/developer/rum#authentication)

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