---
title: Visão geral do Edge Delivery Services para AEM Forms
description: O Edge Delivery Services for AEM Forms foi criado para oferecer desempenho máximo, permitindo que você visualize o futuro da coleta de dados simplificada e do engajamento do usuário.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 67fe933807f8a1bca681a6bcee7164f7c117bcac
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 1%

---


# Introdução ao Forms no AEM Edge Delivery Services

<span class="preview"> É um recurso de pré-lançamento acessível através do nosso [canal de pré-lançamento](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/release-notes/prerelease#new-features). </span>

Este guia ajuda você a entender e implementar formulários usando o Adobe Experience Manager (AEM) Edge Delivery Services (EDS). Se você estiver criando um formulário de contato simples ou uma ferramenta complexa de coleção de dados, esta página o guiará pelas suas opções.

## Noções básicas sobre o Forms no Edge Delivery Services

O Edge Delivery Services é a solução moderna da Adobe para fornecer conteúdo da Web, incluindo formulários, com desempenho e agilidade excepcionais. Ao usar o Edge Delivery Services para seus formulários, você pode:

* **Ofereça experiências mais rápidas:** o Forms é carregado com uma rapidez incrível porque é disponibilizado por uma rede global de servidores de borda (CDNs) próximos aos usuários. Isso melhora a satisfação do usuário e pode aumentar as taxas de conclusão de formulários.
* **Atualizar o Forms mais facilmente:** a abordagem do Edge Delivery Services geralmente permite ciclos de desenvolvimento e atualizações de conteúdo mais rápidos, para que você possa adaptar seus formulários rapidamente.
* **Criar Forms moderno e responsivo:** Crie formulários com ótima aparência e que funcionem perfeitamente em qualquer dispositivo.
* **Benefícios da Escalabilidade e Confiabilidade:** seus formulários serão tão robustos e escaláveis quanto a infraestrutura de borda subjacente.

Este guia irá:

* Explique as diferentes maneiras de criar (criar) formulários para o Edge Delivery Sites.
* Mostrar como configurar o que acontece depois que um usuário envia um formulário (ações de envio).
* Ajudar você a escolher os melhores métodos para suas necessidades específicas e habilidades de equipe.
* Fornecer diagramas de arquitetura e práticas recomendadas.

## Termos principais que você deve saber

* **Edge Delivery Services (EDS):** a arquitetura de desempenho pioneira da Adobe para entrega de conteúdo do AEM via CDNs. Também conhecido como Projeto Franklin.
* **AEM Forms:** a solução da Adobe para criar, gerenciar e processar formulários.
* **Editor Universal (UE):** um editor visual do WYSIWYG para conteúdo do AEM, incluindo formulários.
* **Criação Baseada em Documento:** Criar formulários usando o Microsoft Word ou Google Docs/Sheets.
* **Criação de Documentos (DA):** um serviço hospedado pela Adobe para a criação de conteúdo (incluindo páginas que podem hospedar formulários) para o Edge Delivery Services.
* **FSS (Forms Submission Service):** Um serviço da Adobe que simplifica o envio de dados de formulário para planilhas ou email.
* **Instância de Publicação do AEM:** O ambiente do Live AEM que pode processar envios complexos de formulários.
* **CORS (Cross-Origin Resource Sharing):** Um recurso de segurança de navegador que precisa de configuração ao incorporar formulários de domínios diferentes.
* **CDN (Content Delivery Network):** uma rede de servidores que fornece conteúdo da Web rapidamente aos usuários com base em sua localização geográfica.


**Diagrama Conceitual da Interação do Edge Delivery Services Form**

<!--  
```mermaid
graph LR
    User[User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
    EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
    CDN >|Serves Content| User
    EdgeForm >|Submits Data| Backend[Backend Processing - e.g. Forms Submission Service / AEM Publish]
    style User fill:#f9f,stroke:#333,stroke-width:2px
    style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
    style CDN fill:#9cf,stroke:#333,stroke-width:2px
    style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![Interação de formulários](/help/forms/assets/eds-form-interaction.png)
Este diagrama mostra um usuário interagindo com um formulário entregue rapidamente por meio de um CDN. Os dados enviados são manipulados por um sistema de back-end.

## Como o Forms funciona na Edge?

Com o EDS, o conteúdo do site (incluindo a estrutura dos formulários) pode ser originário de várias fontes, como o AEM as a Cloud Service, o SharePoint, o Google Drive ou o serviço de Criação de documentos (DA). Esse conteúdo é então publicado em um CDN global. Quando um usuário visita o site, o conteúdo é distribuído diretamente do servidor de borda CDN mais próximo, garantindo a velocidade máxima.

<!--*   **Where AEM Forms Fit In**
    Forms in an EDS architecture are designed to be:
    *   **Fast Loading:** Form structures are often simple HTML rendered client-side.
    *   **Decoupled:** The visual part of the form (frontend) is separate from where the data goes after submission (backend).
    *   **Flexible to Create:** You have different tools to build your forms.
    *   **Configurable for Submission:** You can send data to simple services or powerful AEM backends.-->

**Arquitetura simplificada do Edge Delivery Services com o Forms**

<!--
```mermaid
    graph TD
        UserStart[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device] >|Interacts| EdgeForm[Edge-Delivered Form Page]
        EdgeForm >|Loads Instantly| CDN[CDN Edge Server]
        CDN >|Serves Content| UserEnd[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User on Device]
        EdgeForm >|Submits Data| Backend[Backend Processing - Form Submission Service / AEM Publish]

        style UserStart fill:#f9f,stroke:#333,stroke-width:2px
        style UserEnd fill:#f9f,stroke:#333,stroke-width:2px
        style EdgeForm fill:#ccf,stroke:#333,stroke-width:2px
        style CDN fill:#9cf,stroke:#333,stroke-width:2px
        style Backend fill:#fca,stroke:#333,stroke-width:2px
``` -->

![Arquitetura](/help/forms/assets/eds-simplified-architecture.png)
Este diagrama mostra a jornada: os formulários são definidos em um sistema de criação, publicados na borda, enviados aos usuários e os dados enviados são processados por um back-end.

## Escolhendo seu método de criação de formulário

Há três principais maneiras de criar formulários para seus sites do Edge Delivery Services. Sua escolha dependerá das habilidades de sua equipe, da complexidade do formulário e das necessidades de seu projeto.

### Qual abordagem de criação é a certa para você?

Use esta árvore decisória para ajudá-lo a escolher:

**Árvore de decisão de criação de formulário**
<!--    
```mermaid
    graph TD
        A{Start: I need to create a form for an Edge Delivery Services site} > B{What are my team's primary content creation tools & skills?}
        B -- "We mainly use Word / Google Docs / Sheets" > C{How complex is the form and where does the data need to go?}
        B -- "We use AEM and prefer visual tools (Marketers or Designers)" > D[Use Universal Editor - WYSIWYG]
        B -- "Our site content is managed in Document Authoring (DA)" > E[Use Document Authoring - Embed Forms]
        C -- "Simple to moderate form, data to a spreadsheet or email" > F[Use Document-Based Authoring]
        C -- "More complex logic or needs AEM backend integration" > D
        E > G[Create form using Document-Based Authoring or Universal Editor, then embed in your DA page]

        style A fill:#f9f,stroke:#333,stroke-width:2px
        style F fill:#ccf,stroke:#333,stroke-width:2px
        style D fill:#ccf,stroke:#333,stroke-width:2px
        style G fill:#ccf,stroke:#333,stroke-width:2px
``` -->

![Selecionando a plataforma correta](/help/forms/assets/eds-authoring-selection.png)

Essa árvore decisória ajuda a selecionar um método de criação com base nas necessidades de equipe e formulário.

### Criação de Forms com documentos (Word/Google Docs)

Este método é ótimo para [criar formulários rapidamente se sua equipe estiver familiarizada com o Microsoft Word ou Google Docs/Sheets](/help/edge/docs/forms/create-forms.md).

**Como Funciona: Do Documento ao Formulário Web**

Você define os campos, rótulos e tipos do formulário diretamente em um documento do Word ou em uma planilha do Google usando um formato de tabela especial ou um &quot;Bloco de formulário&quot;. Ao publicar esse documento, o Edge Delivery Services o converte automaticamente em um formulário do HTML pronto para a Web com o qual os usuários podem interagir no site.

**Recursos e funcionalidades**

* Crie em ferramentas familiares: Word, Google Docs, Google Sheets.
* Defina campos: entradas de texto, email, menus suspensos, caixas de seleção, botões de opção, áreas de texto.
* Adicione rótulos, espaços reservados e mensagens de ajuda.
* Definir regras básicas de validação: campos obrigatórios, formato do email.
* Integre o reCAPTCHA para proteção contra spam.
* Permitir uploads de arquivo.
* Publicar instantaneamente: as alterações no documento refletem rapidamente no site que está no ar.
* Estender com código personalizado: os usuários avançados podem adicionar componentes de formulário personalizados e estilo por meio do GitHub.

**Considerações**

* Sua equipe usa regularmente o Word ou Google Docs/Sheets para conteúdo.
* Você precisa criar rapidamente formulários simples a moderadamente complexos.
* Você deseja enviar dados de formulário diretamente para uma planilha ou um endereço de email com configuração mínima.

**Como funcionam os envios (principalmente o Forms Submission Service)**

A Forms criou desta forma geralmente [envia seus dados para o Serviço de Envio da AEM Forms](/help/forms/forms-submission-service.md). Você configurará isso (geralmente no próprio documento de origem) para enviar dados para uma Planilha do Google, um arquivo do Excel no OneDrive/SharePoint ou como um email.

**Conceito de Criação Baseada em Documento**
<!--    
```mermaid
    graph LR
        subgraph Authoring["You define your form in a Google Sheet or Word Document"]
        Sheet[Spreadsheet or Document with field definitions:\nField Name - Type - Label\nemail - email - Email Address\nmessage - textarea - Your Message]
    end

        Sheet >|Edge Delivery Services automatically converts it| JSON[Internal Form Definition as JSON]
    JSON >|A 'Form Block' on your page renders it as| HTMLForm[Live HTML Form on Your Website]

        style Sheet fill:#e6ffe6,stroke:#333
        style JSON fill:#e6e6ff,stroke:#333
        style HTMLForm fill:#ffe6e6,stroke:#333
```-->

![Baseado em documento](/help/forms/assets/eds-doc-based.png)
Este diagrama mostra como um formulário definido em um documento se torna um formulário web ativo.

### Forms Visualmente com Universal Editor

O [Editor Universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) oferece uma interface moderna de arrastar e soltar para criar formulários diretamente no navegador da Web.

**Como funciona: criação de formulários com o recurso arrastar e soltar**

Use uma interface visual para arrastar componentes de formulário (como campos de entrada, botões, listas suspensas) para a página. Em seguida, você pode configurar as propriedades de cada componente (rótulos, validação etc.) por meio de um painel de propriedades. O Editor universal mostra uma visualização em tempo real do formulário.

**Recursos e funcionalidades**

* Criação visual de formulários com uma biblioteca de componentes pré-construídos.
* Configurar a validação em tempo real e a lógica de negócios (por exemplo, mostrar/ocultar campos com base em seleções).
* Veja visualizações ao vivo de diferentes dispositivos (desktop, dispositivos móveis).
* Integre com recursos do AEM, como Fragmentos de conteúdo, Fluxos de trabalho do AEM e permissões de usuário.
* Use o &quot;Experience Builder&quot; para obter assistência de IA para criar ou editar formulários usando prompts.

**Considerações**

* Você precisa criar formulários complexos com lógica condicional, painéis de várias etapas ou personalização.
* Sua equipe (por exemplo, profissionais de marketing, usuários empresariais) prefere ferramentas visuais.
* Você precisa de uma forte integração com o AEM as a Cloud Service para governança, fluxos de trabalho ou uso de ativos do AEM em seus formulários.

**Como funcionam os envios (Forms Submission Service ou AEM Publish)**

O Forms criado com o Universal Editor pode:

* Use o [Serviço de Envio do Forms](/help/forms/forms-submission-service.md) simples (para enviar dados para planilhas ou email).
* Envie dados para sua instância de publicação do AEM para obter processamento mais avançado (como iniciar um fluxo de trabalho do AEM, usar o modelo de dados de formulário ou integrar com outros sistemas corporativos).

**Conceito de Editor Universal**

<!--    
```mermaid
    graph TD
    subgraph UE_Interface["Universal Editor Interface in your Browser"]
        Toolbar[Editor Toolbar and Asset Finder]
        Canvas[Your Page with the Form Being Built]
        ComponentPalette[Available Form Components:\nInput / Dropdown / Button\nDrag and drop]
        PropertiesPanel[Configure Selected Component:\nLabel / Validation / Rules]
    end
    ComponentPalette >|Drag & Drop onto| Canvas
    Canvas >|Select a component to edit its| PropertiesPanel
    UE_Interface >|Creates| RenderedForm[Live Form on Your Website]

    style UE_Interface fill:#f0f8ff,stroke:#333
    style RenderedForm fill:#ffe6e6,stroke:#333
```-->

![Editor Universal](/help/forms/assets/eds-ue-based.png)

Este diagrama mostra as partes principais do Editor universal usadas para a criação de formulários.

### Uso do Forms com criação de documentos (DA)

O [Document Authoring (DA)](https://www.aem.live/developer/da-tutorial) é um serviço hospedado pela Adobe para criar e gerenciar o conteúdo principal do site (páginas, artigos) que será entregue via Edge Delivery Services. É uma alternativa ao uso do SharePoint ou do Google Drive para o conteúdo de origem do Edge Delivery Services.

**Noções básicas sobre a criação de documentos (DA) para conteúdo do Edge Delivery Services**

A Criação de documentos oferece um ambiente de criação de nível empresarial usando o sistema de design (Spectrum system) da Adobe e o modelo de documento (blocos, seções) da AEM. Ele foi projetado para o gerenciamento de conteúdo estruturado da EDS.

**Como o DA lida com o Forms (incorporando, não com criação direta)**

O próprio DA **não é uma ferramenta para criar formulários do zero**. Em vez disso, você usa o DA para criar suas páginas da Web e, em seguida, *incorpora* formulários (que foram criados usando a Criação baseada em documento ou o Editor universal) nessas páginas criadas pelo DA.

**Etapas para inserir o Forms nas páginas do DA**

1. **Criar o Formulário:** Crie o formulário usando:
   * Criação baseada em documento (Word/Google Docs)
   * Editor universal

1. **Publicar seu Formulário:** Verifique se o formulário foi publicado e está acessível por meio da própria URL do Edge Delivery (por exemplo, `https://your-eds-project.hlx.page/forms/contact-us`).
1. **Crie sua página no DA:** Crie ou edite a página no Document Authoring onde deseja que o formulário seja exibido.
1. **Incorporar o formulário:** Use um &quot;bloco&quot; ou componente específico em sua página do DA para referenciar e incorporar o formulário de sua URL. A página do DA buscará e exibirá esse formulário criado externamente.

**Criação de Documentos com Formulário Inserido**
<!--
```mermaid
    graph TD
    subgraph FormCreation["1. Create Form using other methods"]
        UE_Form[Universal Editor Form] >|Published to| FormLocation[Form lives at its own Edge Delivery Services URL:\nfor example: /forms/my-contact-form]
        DocBased_Form[Document-Based Form] >|Published to| FormLocation
    end

    subgraph DA_Content["2. Author Page in Document Authoring"]
        DAPage[Your Web Page Authored in DA\nExample: /main-site/landing-page]
        EmbedBlock[On DA Page, add 'Embed Form' Block\nPoints to /forms/my-contact-form]
    end

    DAPage > EmbedBlock
    User[User visits your DA Page] > DAPage
    EmbedBlock >|DA Page fetches and displays| FormLocation[The Form appears on your DA Page]

    style FormCreation fill:#e6ffe6,stroke:#333
    style DA_Content fill:#ffe6cc,stroke:#333
    style FormLocation fill:#ccf,stroke:#333
```-->

![Criação de documentos](/help/forms/assets/eds-da-based.png)

Este diagrama mostra que você primeiro cria um formulário usando UE ou Docs e, em seguida, incorpora-o em uma página que você criou na Criação de documentos.


### Comparando Opções de Criação

| Critérios | Criação baseada em documento | Editor universal (WYSIWYG) | Forms na criação de documentos (DA) |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **Ferramenta de criação primária** | Word/Google Docs/Planilhas | Navegador (AEM Universal Editor) | N/D (Forms estão *inseridos*) |
| **Nível de habilidade da equipe** | Familiarizar-se com editores de documento | Confortável com as ferramentas visuais da Web | Usa DA para conteúdo da página |
| **Complexidade típica de formulários** | Simples a moderado | Moderado a complexo, nível empresarial | Depende do formulário incorporado |
| **Opção de Envio 1 (Simples)** | Serviço de envio de Forms (para planilha/e-mail) | Serviço de envio de Forms (para planilha/e-mail) | Segue a configuração do formulário incorporado |
| **Opção de Envio 2 (Avançada)** | N/A | Publicação do AEM (fluxo de trabalho, FDM etc.) | Segue a configuração do formulário incorporado |
| **Integração com o AEM Backend** | Mínimo | Alto (com o envio do AEM Publish) | Indiretamente, por meio do formulário incorporado do Editor universal |
| **Recomendado Para...** | Criação rápida de formulários simples por equipes de conteúdo, captura rápida de dados. | Profissionais de marketing e usuários empresariais que precisam de controle visual, formulários complexos ou integração profunda com o AEM. | Sites onde o conteúdo principal é gerenciado no DA, exigindo formulários de outras fontes. |

**Árvore de decisão aprimorada**
<!--
```mermaid
    graph TD
    A{Start Here: I need a form on my Edge Delivery Services Site} > B{What's my team's main authoring tool & skill for form content?};
    B -- "Word/Google Docs" > C{How complex is the form & data destination?};
    C -- "Simple form, data to Sheet/Email" > Sol1[CHOOSE: Document-Based Authoring + Forms Submission Service];
    C -- "Needs more logic OR AEM backend\nlike Workflow or FDM" > Sol2[CONSIDER: Can Universal Editor meet this need better?];

    B -- "AEM User / Visual Editor needed\nMarketer or Designer" > D{Where does the form data need to go?};
    D -- "Simple - to Sheet/Email" > Sol3[CHOOSE: Universal Editor + Forms Submission Service];
    D -- "Advanced - AEM Workflow, FDM,\n3rd Party via AEM" > Sol4[CHOOSE: Universal Editor + AEM Publish Submissions\nRequires additional setup];

    B -- "Our main site content is in Document Authoring (DA)" > Sol5[STRATEGY: Author form using Sol1, Sol2, Sol3 or Sol4 first\nTHEN embed that form into your DA page];

    A > F{Will this form be embedded or fetched from another site or domain?};
    F -- "Yes" > G[IMPORTANT: Configure CORS on the site hosting the form.\nEnsure any form JavaScript blocks are available where the form is displayed];

    style Sol1 fill:#90ee90,stroke:#333
    style Sol2 fill:#fffacd,stroke:#333
    style Sol3 fill:#90ee90,stroke:#333
    style Sol4 fill:#90ee90,stroke:#333
    style Sol5 fill:#add8e6,stroke:#333
    style G fill:#ffb6c1,stroke:#333
```-->

![Árvore de decisão](/help/forms/assets/eds-enhanced-decision.png)

## Comparação de recursos de Métodos de criação

A tabela a seguir fornece uma comparação detalhada dos principais recursos entre os diferentes métodos de criação de formulário do AEM, auxiliando na seleção da abordagem mais adequada para suas necessidades.&#x200B;

| **Recurso** | **Editor Universal (WYSIWYG)** | **Criação baseada em documento** | **Criação de Documentos (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Composição Unificada com Sites** | ✅ |                              | ✅ (com formulários inseridos) |
| **Incorporando Suporte a Formulários** | ✅ | ✅ | ✅ (incorporado do Editor Universal ou Docs) |
| **Regras (Comportamento Dinâmico)** | Editor de regras avançado com funções personalizadas | Limitado: Mostrar/ocultar, valor de computação, funções personalizadas | Depende do formulário incorporado |
| **Suporte ao Anexo** | ✅ | ℹ️ (Acesso antecipado) | Depende do formulário incorporado |
| **Suporte ao CAPTCHA** | reCAPTCHA Enterprise | reCAPTCHA Enterprise | Depende do formulário incorporado |
| **Recursos de Envio** | REST, Email, FDM, Fluxo de trabalho, SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion (EA) | Somente planilha | Segue a configuração do formulário incorporado |
| **Esquema de dados** | FDM, Personalizado | Personalizado | Baseado em formulário incorporado |
| **Preenchimento prévio** | 💡 (via Assistente) | ✅ | Depende do formulário incorporado |
| **Fragmentos** | ✅ | ✅ | Depende do formulário incorporado |
| **Editor de regras visuais** | ✅ |                              |                              |
| **Localização** | 💡 (via Sites) | ℹ️ (Excel/Sheets manual) | Depende do formulário incorporado |
| **Esquema de Dados (Árvore de Dados)** | 💡 (via Extensão da Interface do Usuário) |                              |                              |
| **Suporte a modelos** | Somente conteúdo inicial |                              |                              |
| **Portal** |                               |                              |                              |
| **Tema** | ℹ️ (a nível do projeto) | ℹ️ (a nível do projeto) | ℹ️ (com base no site de hospedagem) |
| **Componente personalizado** | ✅ | ✅ | ✅ (se o componente inserido suportar) |
| **OOTB e funções personalizadas** | ✅ | ✅ | ✅ (em formato incorporado) |
| **Referência do fragmento** |                               |                              |                              |
| **Assinar Integração** |                               |                              |                              |
| **Experimentação** | ✅ | ✅ | Depende do contexto incorporado |
| **Gerenciamento de tarefas via Workfront** | ✅ |                              |                              |
| **Extensão do Personalization** | 💡 |                              |                              |
| **Personalização do editor** | ✅ (via Extensão da Interface do Usuário) |                              |                              |
| **Enviar ação** | ✅ | Somente planilha | Baseado em formulário incorporado |

<!--

## Best Practices for Creating Forms

Building great forms goes beyond just the technology. Here's how to ensure your forms are user-friendly and achieve their goals:

* **Designing User-Friendly and Accessible Forms**

  *   **Use Clear, Visible Labels:** Every form field needs a `<label>`. Don't rely only on placeholder text (text inside the input field), as it disappears when users type and is bad for accessibility.
        *   *Good:* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
        *   *Bad:* `<input type="email" placeholder="Email Address">`
  *   **Keep it Simple:** Use standard HTML input types (`<input type="date">`, `<input type="tel">`) where possible. They often have better mobile support and accessibility than complex custom widgets.
  *   **Logical Order and Grouping:** Arrange fields in a way that makes sense to the user. Group related fields together using `<fieldset>` and `<legend>`.
  *   **Provide Clear Instructions:** For any fields that might be confusing, offer concise help text or tooltips.
  *   **Keyboard Navigation:** Ensure users can navigate through your entire form using only the keyboard (Tab, Shift+Tab, Enter, Spacebar).
  *   **Error Handling:** Make errors obvious and easy to correct. Display error messages next to the relevant field and explain what needs to be fixed.

* **Ensuring Your Forms Load Quickly and Are Visible**

  *   **Place Forms Prominently:** If a form is important, make sure users can see it easily without too much scrolling ("above the fold" if possible). Adobe's research shows many forms get low interaction because they are hidden.
  *   **Optimize Assets:** Keep any custom JavaScript or CSS for your forms as small as possible to ensure fast load times. Edge Delivery Services helps with the base page load, but heavy form scripts can still slow things down.

* **Handling User Data Responsibly**
  *   **Ask Only What You Need:** The less Personal Identifiable Information (PII) you ask for, the better. Every field is a potential reason for a user to abandon the form.
  *   **Be Transparent:** Clearly explain *why* you need certain information and *how it will be used*. Link to your privacy policy. This builds trust.

* **Improving User Experience: Captcha Alternatives**

  * **Rethink Visible Captchas:** Those "type the wavy text" or "click all the traffic lights" tests can be very frustrating for users, especially those with disabilities, and often lead to high drop-off rates.

*   **Consider Alternatives:**
    *   **Honeypot Fields:** Add a hidden field that only bots would fill out. If it has data, the submission is likely spam.
    *   **Time-Based Checks:** Measure how quickly a form is submitted. Submissions that are too fast are often bots.
    *   **Invisible reCAPTCHA (v3):** This Google service analyzes user behavior in the background and only presents a challenge if the user seems suspicious. This is often a much better user experience.

**Form Design Do's and Don'ts**

```mermaid
    graph LR
subgraph GoodFormUX [Do ✅ - For Better Forms]
    direction LR
    ClearLabels[Use Visible <label> Tags for All Fields]
    SimpleInputs[Prefer Standard HTML Input Types]
    KeyboardNav[Ensure Full Keyboard Navigation]
    ClearErrors[Show Clear, Actionable Error Messages]
    MinimalPII[Ask Only for Necessary Information]
    TransparentUse[Explain How Data is Used - Privacy Info]
    InvisibleCaptcha[Use Invisible or Behavioral CAPTCHA]
    ProminentPlacement[Make Form Easy to Find on Page]
end

subgraph BadFormUX [Don't ❌ - Avoid These]
    direction LR
    PlaceholderOnly[Only Use Placeholder Text for Labels]
    ComplexWidgets[Use Overly Complex Custom Widgets]
    PoorErrors[Vague or Missing Error Messages]
    ExcessivePII[Request Excessive Personal Data]
    VisibleHardCaptcha[Use Hard-to-Solve Visible CAPTCHAs]
    HiddenForm[Hide the Form Deep in the Page]
end

style GoodFormUX fill:#e6ffe6,stroke:#333
style BadFormUX fill:#ffe6e6,stroke:#333
```

## Quick Decision Guide: Choosing the Right Form Strategy

Let's bring it all together to help you decide on the best approach for your forms.

*   **Matching Form Features to Your Project Goals**
    *   **For speed and simplicity with basic data capture (to spreadsheets/email):** Document-Based Authoring with the Forms Submission Service is often your fastest route.
    *   **For visually rich forms with potential for AEM backend integration:** Universal Editor is your tool. You can start with the Forms Submission Service for simple needs and scale to full AEM Publish submissions for complex workflows.
    *   **If your site content is managed in Document Authoring (DA):** You'll create forms using one of the above methods and then embed them into your DA pages. The submission logic will be tied to how the original embedded form was configured.-->

Para desenvolver o que você aprendeu, veja como seguir em frente:

[Escolha sua estratégia de envio](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) e decida se seu projeto requer a simplicidade do Serviço de Envio do Forms (ideal para saída de planilha/email) ou a flexibilidade e integração de back-end oferecidas pelas Ações de Envio de Publicação do AEM.

Consulte o artigo [Práticas recomendadas para a criação de Forms](/help/edge/docs/forms/universal-editor/best-pratices-eds-forms.md) para saber como criar formulários eficazes, acessíveis e fáceis de usar.

## Próximas etapas

Este guia fornece uma visão geral do uso de formulários com o AEM Edge Delivery Services. Para obter instruções passo a passo mais detalhadas sobre configurações específicas, consulte a documentação oficial do Adobe Experience Manager:

* [Criação baseada em documento com o Edge Delivery Services Forms](/help/edge/docs/forms/tutorial.md)
* [Editor universal com o Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Criação de Documentos (DA) e Incorporação de Conteúdo](https://www.aem.live/developer/da-tutorial)
* [Serviço de envio de AEM Forms](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)


<!-- 
# Edge Delivery Services for AEM Forms
 

Edge Delivery Services for AEM Forms is a composable set of services that enables a rapid development environment where authors can update, publish, and launch new forms rapidly. These services deliver exceptional and high impact forms experiences that drive engagement and conversions. These forms experiences are easy to author and develop.

These services enable you to:

* **Create enrolment experiences with tools of your choice:** Increase authoring efficiency by decoupling content sources. Out of the box you can use Document-based Authoring (Microsoft SharePoint or Google Drive), WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor). You can work with multiple content sources on the same forms site and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, Universal Editor, or Adaptive Forms Editor.

* **Deliver exceptional Digital Enrolment experiences:** Deliver Digital Enrolment experiences that load and render quickly and continuously monitor your forms performance through Operational Telemetry. Faster loading times and optimized user experience contribute to higher form completion and conversion rates. 

* **Use developer friendly toolset:** Edge Delivery Services for AEM Forms
 uses plain HTML, modern CSS, and vanilla JavaScript to create exceptional experiences, avoiding the steep learning curve of a specific framework. A developer with basic web development skills can customize and easily build form components and experiences. There is no need to wait for a pipeline to run, just check-in your code into GitHub and your changes are live.

## Edge Delivery Services for AEM Forms Overview {#edge-overview}

Edge Delivery Services for AEM Forms allows for a high degree of flexibility in how you author forms on your website. You can author content and forms with [WYSIWYG Authoring](/help/forms/creating-adaptive-form-core-components.md) as well as [Document-based Authoring](/help/edge/docs/forms/create-forms.md). Edge Delivery Services for AEM Forms
 provide a forms block, known as [Adaptive Forms Block](/help/edge/docs/forms/create-forms.md) to add a form to your Edge Delivery Services site.

For example, you author forms directly in Microsoft Excel or Google Sheets and these spreadsheets are transformed into forms for your website. Any new form or form content, such as a new form field, is instantly available on your website without requiring a rebuild process.

The following diagram illustrates how you can edit forms in Microsoft Excel or Google Sheets (Document-based Authoring) and publish to Edge Delivery Services. It also shows the AEM publishing method using the WYSIWYG Authoring (Universal Editor or Adaptive Forms Editor).

![Publish to Edge Delivery Services and AEM](/help/edge/docs/forms/assets/AEM-forms-with-EDS-publishing.png)

Edge Delivery Services for AEM Forms uses GitHub so customers can manage and deploy code directly from their GitHub repository. For example, you can write forms in either [Google Sheets](/help/edge/docs/forms/create-forms.md) or [Microsoft Excel](/help/edge/docs/forms/create-forms.md) and the components of your forms can be developed by using CSS and JavaScript in a GitHub repository.

When your forms are ready, you can use the [AEM Sidekick](/help/edge/docs/forms/tutorial.md#preview-and-publish-your-content), a chrome browser extension, to preview and publish content updates.

![Install AEM SideKick](/help/edge/assets/aem-sidekick-preview-publish-forms.png)

The choice between the [Document-based Authoring ](#document-based-authoring-features) and [WYSIWYG Authoring](#wysiwyg-authoring-features) depends on your specific requirements:

* For simple forms that just collect basic information with a few fields (think contact us forms, lead generation forms, or service request forms), and where you need quick data connectivity using a spreadsheet, the [Document-based Authoring](#document-based-authoring-features) is a good fit. You can build these forms like you would build a document in Google Sheets or Microsoft Excel. 

* For complex forms, like forms requiring multiple panels, complex rules and business logic, data manipulation, integration with external systems, or streamlined workflows using AEM features, then [WYSIWYG Authoring](#wysiwyg-authoring-features) is a better option. 


### Key Features of Document-based Authoring and WYSIWYG Authoring

Document-based Authoring offers a basic set of features and WYSIWYG Authoring unlocks additional capabilities beyond the Document-based Authoring, empowering you to build more complex and interactive forms. The key features of both Document-based Authoring and WYSIWYG Authoring are:

#### Document-based Authoring features

Document-based Authoring  allows you to create forms using familiar tools like Microsoft Excel or Google Sheets. These forms offer the following functionalities:

* Accessible components for a user-friendly experience.
* Standardized HTML structure for consistent rendering.
* Rules and validations to ensure data accuracy.
* File attachment options for collecting additional information.
* Google reCAPTCHA integration for spam protection.
* Ability to create custom form components for specific needs.
* Submit form data directly to Microsoft Excel or Google Sheets or email addresses.
* Monitor your forms performance through Operational Telemetry

#### WYSIWYG Authoring features

WYSIWYG Authoring provides WYSIWYG interfaces (Universal Editor and Adaptive Forms Editor) for building forms and offers all the capabilities of Document-based Authoring, plus a wide range of additional features:

* Advanced rules editor for creating complex logic.
* Server-side extensibility for custom functionalities.
* WYSIWYG editing experience for easy form creation and visualization.
* Document of record functionality to create tamper-proof archives of submitted data.
* Integration with Adobe Sign for electronic signatures.
* Integration with Adobe Workfront Fusion to triggering Adobe Workfront Fusion scenarios upon form submission.
* Integration with various data sources for pre-populating forms and submitting data.
* Form Data Model (FDM) for defining data structure and interactions with various data sources.
* Ability to choose from multiple submit actions for handling form submissions, including submitting data to Microsoft SharePoint, Microsoft OneDrive, Adobe Workfront Fusion, Salesforce, Microsoft Dynamics, many more data sources.

The all above features are also available via Adaptive Forms Editor. 

In essence, WYSIWYG Authoring (Universal Editor and [Adaptive Forms Editor](/help/forms/creating-adaptive-form-core-components.md)) builds upon the foundation of [Document-based Authoring](/help/edge/docs/forms/create-forms.md), providing a more advanced toolkit for creating and managing complex forms. 

>[!NOTE]
>
>
> The WYSIWYG Authoring capability is available under the early-adopter program. If you are interested, send a quick email from your work address to aem-forms-ea@adobe.com to request access to the capability.

### Edge Delivery Services for AEM Forms

: Authoring, Publishing, and Submission of Forms  

The following diagrams illustrate the process of creating, publishing, and submitting forms using Document-based Authoring and WYSIWYG Authoring.

![Document-based Authoring](/help/edge/assets/document-based-authoring-workflow.png)

![WYSIWYG Authoring](/help/edge/assets/wysiwyg-authoring-workflow.png)

## Start creating forms

* [Get started with Edge Delivery Services for AEM Forms](/help/edge/docs/forms/tutorial.md)
* [Create a form using Google Sheets or Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Set up your Google Sheets or Microsoft Excel files to start accepting data​](/help/edge/docs/forms/submit-forms.md)
* [Publish your form and start collecting data](/help/edge/docs/forms/publish-forms.md)
* [Customize the look of your forms​](/help/edge/docs/forms/style-theme-forms.md)
* [Add repeatable sections to a form​](/help/edge/docs/forms/repeatable-forms.md)
* [Show a custom thank you message after form submission​](/help/edge/docs/forms/thank-you-page-form.md)
* [Adaptive Form Block components and their properties](/help/edge/docs/forms/form-components.md)
* [Real Use Monitoring](https://www.aem.live/developer/rum#authentication)

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
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Create a form using Edge Delivery Services forms" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Create a form using Google Sheets or Microsoft Excel</b>
        </a>
        <p>Create forms that load and render quickly and automatically reflows on mobile devices.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Submit form" alt="Use Form Fragments in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Submit form to spreadsheet</b>
        </a>
        <p>Submit forms directly to your Microsoft Excel or Google Sheets.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Apply styles or themes to an Edge Delivery Services form" style="border-radius: 5px;"> </b>
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
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Translate an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Translate a form</b>
        </a>
        <p>Extend the reach of your forms while keeping costs in check.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Add repeatable sections to an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
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
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Use reCAPTCHA in an Edge Delivery Services Form" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Use reCAPTCHA</b>
        </a>
        <p>Use OOTB reCAPTCHA integration for robust spam and bot protection.</p>
    </div>


</div>


</br>


-->
