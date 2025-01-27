---
title: Visão geral do Edge Delivery Services para AEM Forms
description: Edge Delivery Services para AEM Forms
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: 7122022c4245887ec576d4c1cd9af288b440f0c2
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 5%

---

# Editor universal para Edge Delivery Services para Forms (bloco Forms do EDS)


O Editor universal foi projetado para ajudar criadores de conteúdo e autores de formulários a criar, gerenciar e editar formulários facilmente. Ele oferece uma experiência de edição simples, visual e eficiente focada em Edge Delivery Services (EDS).

Com o Editor universal, os usuários podem usar elementos de formulário (como campos de texto, caixas de seleção e botões de opção) para criar formulários em uma interface do What You See Is What You Get (WYSIWYG). Essa abordagem torna a criação de formulários intuitiva e acessível, mesmo para aqueles sem conhecimento técnico especializado.

![Editor Universal](/help/edge/docs/forms/universal-editor/assets/universal-editor.png)

O Universal Editor permite que criadores de conteúdo e autores de formulários criem, gerenciem e editem formulários de maneira simplificada e eficiente. Esse editor está focado especificamente em Edge Delivery Services (EDS).

A força principal do Editor universal está em seu conjunto de recursos robusto, que inclui recursos avançados de criação de formulários, edição dinâmica de regras e integração contínua com várias fontes de dados. Os usuários podem criar rapidamente formulários responsivos usando componentes pré-criados, modelos personalizáveis e uma ampla biblioteca de elementos de formulário. Esses recursos são cuidadosamente projetados para manter a renderização leve do lado do cliente, a compatibilidade entre navegadores e a rigorosa adesão aos padrões de acessibilidade.

## Principais recursos do Universal Editor para EDS Forms


<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG"> 
    <h3>Interface do WYSIWYG</h3>
    <p>O Universal Editor fornece uma interface WYSIWYG para design de formulários. Ele fornece biblioteca de componentes pré-criada, suporte de design responsivo e criação de formulários baseada em modelo. Você pode adicionar ou remover campos de formulário instantaneamente e modificar propriedades de campo (como rótulo, vinculação de dados, validação). Você também pode plug-in de componentes de formulário personalizados para o Universal Editor.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Editor de regras">
    <h3>Editor de regras</h3>
    <p>O editor de regras permite criar interações de formulário sofisticadas com regras orientadas por eventos, validação instantânea e tratamento de erros por meio de definições leves baseadas em JavaScript e JSON.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Ações de enviar">
    <h3>Modo responsivo </h3>
    <p>Crie formulários que se adaptam perfeitamente a todos os dispositivos (desktops, tablets e dispositivos móveis). Use o modo responsivo para visualizar formulários de vários tamanhos de tela.</p>
  </div>
</div>
<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG alt=" WYSIWYG Interface"> 
    <h3>Personalização</h3>
    <p>Personalização</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Editor de regras">
    <h3>Cabeçalhos de autenticação</h3>
    <p>O editor de regras permite criar interações de formulário sofisticadas com regras orientadas por eventos, validação instantânea e tratamento de erros por meio de definições leves baseadas em JavaScript e JSON.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Ações de enviar">
    <h3> Publicar/Desfazer publicação </h3>
    <p>Controle facilmente a visibilidade dos formulários publicando-os e desfazendo a publicação com apenas alguns cliques.</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Serviços de pré-preenchimento">
    <h3>Serviços de pré-preenchimento</h3>
    <p>Os serviços de pré-preenchimento melhoram a experiência do usuário preenchendo de forma inteligente os campos de formulário com dados relevantes de várias fontes, reduzindo a entrada manual de dados.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Vinculação de dados">
    <h3>Vinculação de dados</h3>
    <p>A vinculação de dados permite conexões diretas e dinâmicas entre campos de formulário e fontes de dados de back-end, oferecendo suporte à sincronização em tempo real e ao mapeamento de dados complexo.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Internacionalização/localização">
    <h3>Localização</h3>
    <p>O suporte à internacionalização garante acessibilidade global com renderização em vários idiomas, compatibilidade entre os idiomas da direita e da esquerda e formatação específica do local.</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Analytics e Rastreamento">
    <h3>Analytics e Rastreamento</h3>
    <p>Os mecanismos integrados de análise e rastreamento fornecem insights sobre interações de formulário, taxas de envio e comportamento do usuário, permitindo otimização contínua.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Experimentação (teste A/B)">
    <h3>Experimentação (teste A/B)</h3>
    <p>A experimentação permite que as organizações executem testes A/B em designs de formulário para identificar os layouts ou recursos de melhor desempenho.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Gerenciamento de tarefas">
    <h3>Gerenciamento de tarefas</h3>
    <p>A integração com o Adobe Workfront permite que as equipes gerenciem tarefas relacionadas à criação e manutenção de formulários, garantindo uma colaboração simplificada.</p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Personalização do editor">
    <h3>Personalização do editor</h3>
    <p>Os desenvolvedores podem estender a funcionalidade do Editor universal por meio de extensões da interface do usuário, permitindo soluções personalizadas que se ajustem a necessidades organizacionais específicas.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Incorporação do Forms">
    <h3>Incorporação do Forms</h3>
    <p>O Editor universal oferece suporte à incorporação de formulários diretamente nas páginas dos sites do Edge Deliver Services. Isso pode ser feito usando o componente de Incorporação fornecido imediatamente.</p>
  </div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Componentes personalizados">
    <h3>Componentes personalizados</h3>
    <p>Os componentes personalizados permitem aos desenvolvedores estender a funcionalidade de formulários criando elementos de formulário exclusivos personalizados para casos de uso específicos 
    </p>
  </div>
</div>

<div>
  <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Configuração de agradecimento">
    <h3>Configuração de agradecimento</h3>
    <p>Personalize a mensagem ou página de confirmação exibida após o envio do formulário.</p>
  </div>
    <div class="card" style="display: inline-block; width: calc(30% - 20px); margin: 10px; border: 1px solid #ccc; padding: 10px; text-align: center;">
    <img src="/help/edge/docs/forms/universal-editor/assets/generate-forms.svg" alt="Interface do WYSIWYG" alt="Ações de enviar">
    <h3>Ações de enviar</h3>
    <p>As Ações de envio facilitam os fluxos de trabalho de envio de formulário com opções de integração de backend, pré-processadores de dados, lógica de envio condicional e conexões de endpoint seguras.</p>
  </div>
</div>


<!-- ![Universal Editor](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg)  **WYSIWYG interface for Form creation**: Universal Editor provides a WYSIWYG interface for form design. It provides pre-built component library, responsive design support, and template-based form creation. You can instantly add or remove form fields and modify field properties (like label, data binding, validation). You can also plugin custom form components to Universal Editor.


* **Rule editor**: The rule editor stands out as a powerful mechanism for creating sophisticated form interactions. It supports event-driven rules, instant validation, and error handling through lightweight JavaScript and JSON-based definitions. This allows developers to implement complex form logic, such as conditional field visibility, automatic calculations, and dynamic form behaviour without extensive coding.

* **Submit actions**: Submit Actions enable form submission workflows. These actions provide comprehensive backend integration options, supporting protocols like REST API. The system allows you configure data pre-processors for automatic data transformation, conditional submission logic based on form field values, and secure endpoint connections. Organizations can define complex submission rules that validate data, and manage form responses with granular control.

* **Pre-fill services:** Pre-fill Services enhance user experience by intelligently populating form fields with relevant data. These services connect to various data sources, including user profiles, browser local storage, and external databases. The mechanism supports dynamic data population, enabling automatic completion of form fields based on contextual information. Users benefit from reduced manual data entry, while administrators gain flexibility in configuring pre-fill rules across different form types and scenarios. The pre-fill functionality adapts to different authentication methods, including session-based approaches and token-based systems, ensuring both convenience and security.

* **Data binding capabilities**: Data binding in the Universal Editor enables direct, dynamic connections between form fields and backend data sources. This feature allows real-time synchronization of form data, supporting complex data mapping scenarios. The system supports transforming form inputs into structured database records with minimal configuration. Advanced mapping supports nested data structures, allowing complex form designs to interact seamlessly with intricate data models.

* **Internationalization/localization capabilities**: Internationalization support ensures global accessibility, with multi-language rendering, right-to-left language compatibility, and locale-specific formatting.

* **Analytics and tracking mechanisms**: The built-in analytics and tracking mechanisms provide comprehensive insights into form interactions, submission rates, and user behavior, enabling continuous optimization of form design and performance. 

* **Experimentation (A/B Testing)**: The Universal Editor supports experimentation by allowing organizations to run A/B tests on form designs to identify the best-performing layouts or features.

* **Task Management via Adobe Workfront**: Integration with Adobe Workfront allows teams to manage tasks related to form creation and maintenance, ensuring streamlined collaboration and efficient workflows.

* **Editor Customization via UI Extension**: Developers can extend the functionality of the Universal Editor through UI extensions, enabling tailored solutions that fit specific organizational needs. -->

## Componentes de formulário pré-construídos

O Editor universal fornece os seguintes componentes de formulário prontos para uso:

<table>
  <thead>
    <tr>
      <th>Adorável</th> 
      <th>Componentes de formulários</th>
      <th>Descrição</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="Componentes de formulários" style="width: 100%;"></td> 
      <td><b>Acordeão</b></td>
      <td>Estrutura do painel flexível para organizar o conteúdo.</td>
    </tr>
    <tr>
      <td><b>Botão</b></td>
      <td>Adiciona elementos interativos para ações como navegação ou lógica personalizada.</td>
    </tr>
    <tr>
      <td><b>Captcha</b></td>
      <td>Evita spam exigindo que os usuários concluam uma tarefa de verificação humana usando o Google reCaptcha ou HCaptcha.</td>
    </tr>
    <tr>
      <td><b>Caixa de seleção</b></td>
      <td>Permite que os usuários configurem uma caixa de seleção.</td>
    </tr>
    <tr>
      <td><b>Grupos de caixa de seleção</b></td>
      <td>Permite aos usuários selecionar várias opções de um grupo.</td>
    </tr>
    <tr>
      <td><b>Seletor de data</b></td>
      <td>Permite que os usuários selecionem uma data usando uma interface de calendário.</td>
    </tr>
    <tr>
      <td><b>Listas Suspensas</b></td>
      <td>Oferece opções de seleção única ou múltipla de uma lista predefinida.</td>
    </tr>
    <tr>
      <td><b>Email</b></td>
      <td>Captura endereços de email com validação básica de formato.</td>
    </tr>
    <tr>
      <td><b>Anexo de arquivo</b></td>
      <td>Permite o upload de documentos, imagens ou outros tipos de arquivos.</td>
    </tr>
    <tr>
      <td><b>Fragmentos de formulários</b></td>
      <td>Componentes de formulário reutilizáveis para seções como campos de endereço ou detalhes de contato.</td>
    </tr>
    <tr>
      <td><b>Imagem</b></td>
      <td>Suporta o upload e a exibição de imagens em formulários.</td>
    </tr>
    <tr>
      <td><b>Modal</b></td>
      <td>Exibe uma caixa de diálogo pop-up, geralmente usada para alertas, informações adicionais ou confirmação.</td>
    </tr>
    <tr>
      <td><b>Campo numérico</b></td>
      <td>Registra entrada numérica, permitindo a validação de números ou intervalos.</td>
    </tr>
    <tr>
      <td><b>Painel</b></td>
      <td>Organiza seções de formulário com painéis expansíveis/recolhíveis.</td>
    </tr>
    <tr>
      <td><b>Botões de opção</b></td>
      <td>Habilita a seleção de escolha única de um grupo de opções.</td>
    </tr>
    <tr>
      <td><b>Avaliação</b></td>
      <td>Permite que os usuários forneçam uma classificação baseada em estrelas.</td>
    </tr>
    <tr>
      <td><b>Botão Redefinir</b></td>
      <td>Redefine os campos de formulário para seu estado padrão.</td>
    </tr>
    <tr>
      <td><b>Botão Enviar</b></td>
      <td>Aciona o envio do formulário e inicia fluxos de trabalho definidos.</td>
    </tr>
    <tr>
      <td><b>Campo de número de telefone</b></td>
      <td>Registra números de telefone com formatação baseada no país.</td>
    </tr>
    <tr>
      <td><b>Texto</b></td>
      <td>Fornece uma seção dedicada para exibir termos legais e coletar contratos de usuário por meio de caixas de seleção.</td>
    </tr>
    <tr>
      <td><b>Campo de texto</b></td>
      <td>DCaptura a entrada de linha única, como nomes ou endereços de email.</td>
    </tr>
    <tr>
      <td><b>Assistente</b></td>
      <td>Orienta os usuários passo a passo por um processo de formulário de várias partes.</td>
    </tr>
  </tbody>
</table>

<!-- * Footer: Adds a footer section for consistent design or additional information.
* Form Container: Wraps all form elements and manages overall form properties.
* Header: Adds a header section for form titles, branding, or instructions.-->
<!-- * 
* Prefillable Fields: Automatically populates form fields with data from predefined sources such as user profiles or APIs. 

* Switches/Toggle Buttons: Provides binary on/off choices for user input.


* Title: Adds a text-based heading or label to improve form clarity and organization.


In-addtion to pre-built form components, the Universal editor also provides support for:

* **Embedding Forms in Another Webpage**: The Universal Editor supports embedding forms directly into Edge Deliver Services Sites pages. This can be done using the embed component provided out of the box.

* **Validation Messages**: Validation messages provide real-time feedback to users when they enter incorrect or incomplete data. Features include:
    * Dynamic Error Display: Instantly alerts users to errors, such as invalid email addresses or missing required fields.
    * Customizable Messages: Allows form authors to define user-friendly error texts.
    * Rule-Based Validation: Supports advanced validation logic, such as checking dependencies between fields or implementing conditional rules.

* **Hidden Fields**: Hidden fields store data invisibly within the form, often for backend processing or prefilled values. Use cases include:
    * Passing contextual information (e.g., user ID or session data) to the backend without displaying it to users.
    * Capturing metadata like timestamps or tracking IDs.
    * Hidden fields are not visible to end-users but can be prefilled, updated dynamically, or used in workflows.

* **Custom Components**: Custom components allow developers to extend the functionality of forms by creating specialized or third-party integrations. Features include:
    * Flexibility: Developers can design unique form elements tailored to specific use cases.
    * Third-Party Integration: Embed widgets or tools like payment gateways, analytics trackers, or AI-driven input fields.
    * Seamless Compatibility: Custom components can integrate with the Universal Editor's drag-and-drop interface and existing features like data binding or validation.

* **Thank you Configuration**: Customize the acknowledgment message or page shown after form submission.
-->


## Integração

Para ativar o Editor universal e o Editor de regras para o seu ambiente ou solicitar recursos adicionais como o Forms Portal, Documento de registro, integração com o Adobe Sign ou suporte de idioma da direita para a esquerda, basta enviar um email para mailto:aem-forms-ea@adobe.com do endereço oficial com a solicitação.



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
        width: calc(30% - 10px);;
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