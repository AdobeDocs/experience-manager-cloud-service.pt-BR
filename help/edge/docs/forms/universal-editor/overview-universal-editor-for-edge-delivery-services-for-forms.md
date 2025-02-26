---
title: Editor universal para Edge Delivery Services para Forms (bloco Forms do EDS)
description: Use o Editor universal para Edge Delivery Services para Forms (bloco Forms do EDS) para criar Forms adaptável.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 3%

---


# Editor universal para Edge Delivery Services para Forms (bloco Forms do EDS)

<span class="preview"> Este recurso está disponível através do programa de acesso antecipado. Para solicitar acesso, envie um email de seu endereço oficial para <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> com o nome da organização do GitHub e o nome do repositório. Por exemplo, se a URL do repositório for https://github.com/adobe/abc, o nome da organização é adobe e o nome do repositório é abc.</span>

O Editor universal revoluciona a criação de formulários para o Adobe Edge Delivery Services (EDS) ao oferecer uma interface simples, visual e intuitiva do What You See Is What You Get (WYSIWYG). Projetado para criadores de conteúdo e autores de formulários, ele elimina a complexidade dos processos tradicionais de criação de formulários, tornando-o acessível até mesmo para usuários não técnicos.

Com o Editor universal, você pode criar rapidamente formulários responsivos e interativos usando componentes pré-criados, como campos de texto, caixas de seleção e botões de opção. Seu conjunto de recursos robusto oferece suporte a regras dinâmicas, integração de dados contínua e personalização avançada, garantindo que cada formulário seja adaptado às suas necessidades.

Quer você esteja gerenciando uma renderização leve do lado do cliente, garantindo compatibilidade entre navegadores ou seguindo padrões de acessibilidade rigorosos, o Universal Editor oferece uma solução simplificada para criar e gerenciar formulários.

![Editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center} —>

## Principais recursos do Universal Editor para EDS Forms



Este é o layout com cartões de igual largura (usando colunas de largura fixa):

| ![Interface do WYSIWYG](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg) | ![Editor de regras](/help/edge/docs/forms/universal-editor/assets/rule-editor.svg) | ![Enviar Ações](/help/edge/docs/forms/universal-editor/assets/submit-actions.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Interface do WYSIWYG**](/help/edge/docs/forms/universal-editor/universal-editor-user-interface.md) | [**Editor de regras**](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) | [**Enviar Ações**](/help/edge/docs/forms/universal-editor/submit-action.md) |
| O Editor universal fornece uma interface do WYSIWYG para design de formulários com uma biblioteca de componentes pré-criada, design responsivo, criação baseada em modelo e modificações de campo em tempo real. | O editor de regras permite que os usuários criem interações de formulário dinâmicas usando regras orientadas por eventos, validação instantânea e tratamento de erros por meio do lightweight JavaScript e do JSON. | As ações enviar oferecem suporte à integração de back-end, lógica de envio condicional, endpoints seguros e pré-processadores, simplificando os fluxos de trabalho de envio. |

| ![Publicando/Desfazendo publicação](/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg) | ![Modo responsivo](/help/edge/docs/forms/universal-editor/assets/responsive.svg) | ![Componentes personalizados](/help/edge/docs/forms/universal-editor/assets/custom-components.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Publicando/Desfazendo publicação**](/help/edge/docs/forms/universal-editor/publish-forms.md) | [**Modo responsivo**](/help/edge/docs/forms/universal-editor/responsive-layout.md) | [**Componentes personalizados**](/help/edge/docs/forms/universal-editor/create-custom-component.md) |
| Controle facilmente a visibilidade de seus formulários — publique ou cancele a publicação diretamente do editor com apenas alguns cliques. | Crie formulários que se adaptam perfeitamente a todos os dispositivos (desktops, tablets e dispositivos móveis). Use o modo responsivo para visualizar e testar formulários para vários tamanhos de tela. | Os componentes personalizados permitem que os desenvolvedores estendam os recursos do formulário criando elementos exclusivos personalizados adaptados a casos de uso organizacional específicos. |

| ![Estilo](/help/edge/docs/forms/universal-editor/assets/personalization.svg) | ![Serviços de preenchimento prévio](/help/edge/docs/forms/universal-editor/assets/prefill-services.svg) | ![Teste A/B](/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Estilo**](/help/edge/docs/forms/universal-editor/style-theme-forms.md) | **Preencher Serviços** (Em Breve) | [**Teste A/B**](https://github.com/adobe/aem-experimentation/blob/main/documentation/experiments.md) |
| O estilo com CSS permite que os desenvolvedores personalizem a aparência dos elementos de formulário e criem um design visualmente atraente que se alinhe à estética do site. | Os serviços de pré-preenchimento preenchem automaticamente os campos de formulário com dados relevantes do usuário de várias fontes, reduzindo a entrada manual e aprimorando a experiência do usuário. | O teste A/B permite que as organizações experimentem diferentes designs de formulário, layouts e recursos para identificar as variantes com melhor desempenho. |

| ![Análise e Acompanhamento](/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg) | ![Gerenciamento de tarefas](/help/edge/docs/forms/universal-editor/assets/adobe-workfront.svg) | ![Associação de Dados](/help/edge/docs/forms/universal-editor/assets/data-binding.svg) |
|:-------------:|:-------------:|:-------------:|
| [**Análise e Acompanhamento**](https://www.aem.live/developer/martech-integration) | **Gerenciamento de tarefas** | **Associação de Dados** |
| Obtenha insights sobre o comportamento do usuário, as interações de formulário e as taxas de envio com análises e rastreamento integrados para permitir a otimização de formulários orientados por dados. | A integração com o Adobe Workfront permite que as equipes gerenciem tarefas de criação e manutenção de formulários, garantindo fluxos de trabalho simplificados. | A vinculação de dados permite conexões diretas entre campos de formulário e fontes de dados de back-end, oferecendo suporte a atualizações em tempo real e mapeamento de dados avançado. |

| ![CAPTCHA](/help/edge/docs/forms/universal-editor/assets/captcha.svg) | ![Incorporando o Forms](/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg) | ![Obrigado pela Configuração](/help/edge/docs/forms/universal-editor/assets/thank-you.svg) |
|:-------------:|:-------------:|:-------------:|
| **Personalização do editor** | **Incorporando o Forms** | [**Obrigado pela Configuração**](/help/edge/docs/forms/universal-editor/submit-action.md#show-a-custom-thank-you-message-on-adaptive-form-submission-submit-action-message-ue) |
| Os desenvolvedores podem estender a funcionalidade do editor por meio de extensões de interface do usuário, permitindo soluções personalizadas que se ajustem a necessidades organizacionais específicas. | Incorpore formulários diretamente nas páginas do Edge Delivery Services Sites usando o componente de incorporação integrado do Editor universal. | Personalize facilmente a mensagem ou página de confirmação exibida aos usuários após o envio bem-sucedido do formulário. |


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
      <th></th> 
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

Para ativar o Editor universal e seus recursos avançados, como o Editor de regras, escreva para nós em aem-forms-ea@adobe.com a partir da sua ID de e-mail oficial. A equipe do Adobe está aqui para ajudá-lo a transformar sua experiência de criação de formulários.

## Perguntas frequentes

**T. Quem pode usar o Editor universal?**
O Editor universal foi projetado para um amplo público-alvo, incluindo:

* Criadores de conteúdo que desejam criar formulários visualmente atraentes.
* Desenvolvedores que precisam de recursos avançados de personalização e integração.
* Organizações que buscam soluções de formulários escaláveis, seguras e compatíveis.

**P: Posso integrar formulários criados com o Editor Universal aos meus sistemas existentes?**
Absolutamente. O Editor universal oferece suporte à vinculação de dados contínua com sistemas de back-end, permitindo atualizações em tempo real e mapeamento de dados avançado. Ele também se integra a ferramentas como o Adobe Workfront para gerenciamento de tarefas e oferece suporte a endpoints seguros para workflows de envio de dados.

**P: É possível personalizar os componentes de formulário?**
Sim, o Editor universal permite que os desenvolvedores criem componentes personalizados adaptados às necessidades organizacionais específicas. Além disso, é possível estender a funcionalidade do editor por meio de extensões de interface do usuário e fluxos de trabalho personalizados.

**P: Como o Editor Universal lida com a acessibilidade?**
O Editor universal foi projetado com a rigorosa observância dos padrões de acessibilidade, incluindo as WCAG (Web Content Accessibility Guidelines). Isso garante que os formulários possam ser usados por indivíduos com deficiência, fornecendo uma experiência inclusiva.

**P: Que tipo de análise posso obter dos formulários?**
O Editor universal inclui ferramentas de análise e rastreamento integradas para monitorar interações do usuário, taxas de envio de formulário e métricas de conversão. Esses insights ajudam a otimizar seus formulários para obter melhor desempenho.


## Começar a criar formulários

{{universal-editor-see-also}}

