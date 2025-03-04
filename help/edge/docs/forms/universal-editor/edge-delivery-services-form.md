---
Title: How Edge Delivery Services Forms work?
Description: This article provides information on how Edge Delivery Services Forms work. It also provides information on various form authoring platforms, including the Universal Editor and document-based authoring.
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Working of Edge Delivery Services Forms, How Edge Delivery Services Forms work?
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
exl-id: db58ce85-139a-4cc1-8e18-73da76357299
source-git-commit: bb01a76ae2bfd78ae648e91545f34f20fabebd10
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---


# Edge Delivery Services Forms

O Adobe Edge Delivery Services Forms transforma a forma como os formulários são criados, executados e processados. Ao utilizar o Edge Delivery Services, as organizações podem criar formulários digitais rápidos, seguros e altamente disponíveis, aprimorando a experiência do usuário e a eficiência operacional com um ambiente de desenvolvimento rápido. Com o Edge Delivery Services Forms, você pode aumentar as conversões, reduzir custos e acelerar a entrega de conteúdo.

## Benefícios do Edge Delivery Services Forms

* **Criação de formulários mais rápida**: crie formulários de alto desempenho com uma pontuação Lighthouse perfeita e monitore continuamente seu desempenho real usando o RUM (Monitoramento de usuário real).

* **Processo de criação simplificado**: gerencie facilmente o conteúdo de várias fontes para obter maior flexibilidade. Você pode criar formulários imediatamente usando o WYSIWYG e a criação baseada em documentos, permitindo a integração perfeita de vários formatos de conteúdo.

* **Facilidade de Uso para Usuários Não Técnicos**: o Edge Delivery Services permite que não programadores gerenciem e publiquem formulários facilmente, sem exigir amplo conhecimento de programação.

* **Experiência de usuário aprimorada**: garanta tempos de carregamento rápidos e interações suaves, proporcionando aos usuários tempos de espera mínimos e uma experiência intuitiva de preenchimento de formulário.

* **Execução sem Servidor**: o Edge Delivery Services habilita a execução sem servidor da lógica de formulário. Isso inclui:

   * **Validação no lado do cliente**: a validação do campo de formulário ocorre no lado do cliente, reduzindo os atrasos de ida e volta.

   * **Pré-preenchimento e Personalization**: o pré-preenchimento de dados de formulário é tratado no lado do cliente para proporcionar uma experiência perfeita ao usuário.

   * **Processamento de Envio**: Os envios de formulários são validados e encaminhados com segurança sem o servidor central

## Como funciona o Edge Delivery Services Forms?

Os usuários podem criar Edge Delivery Services Forms usando ferramentas de criação baseadas em documentos, como Google Drive, SharePoint ou o Editor universal (criação no WYSIWYG), enquanto aproveitam o estilo, o comportamento e os componentes básicos disponíveis no repositório GitHub. Depois de criado, o Edge Delivery Services Forms pode enviar dados para qualquer plataforma usando o Serviço de envio do Forms.

![Como o Edge Delivery Services Forms funciona](/help/edge/docs/forms/assets/eds-forms-working.png)

### Principais componentes do Edge Delivery Services Forms

Os principais componentes do Edge Delivery Services Forms são:

* **Repositório do GitHub**: o repositório do GitHub serve como modelo para a criação do Edge Delivery Services Forms. Os formulários aproveitam o estilo e a funcionalidade básicos do repositório e permitem que os usuários adicionem personalizações e componentes personalizados ao Edge Delivery Services Forms.

* **Criação de formulário**: o Edge Delivery Services Forms oferece suporte a dois tipos de criação: WYSIWYG e criação baseada em documento. A criação baseada em documentos permite que os usuários criem formulários usando ferramentas familiares como o Google Docs e o Microsoft Office. A criação do WYSIWYG permite que os usuários projetem formulários visualmente usando o Editor universal, facilitando a criação e o gerenciamento de formulários para usuários não técnicos. O Universal Editor oferece uma experiência de criação de formulário intuitiva e fornece acesso a vários recursos de formulário.

* **Serviço de Envio do Forms**: o Serviço de Envio do Forms permite armazenar dados de envios de formulários em qualquer plataforma, como OneDrive, SharePoint ou Google Sheets, facilitando o acesso e o gerenciamento de dados de formulário no seu sistema preferido.

## Criação de um formulário

O Adobe Experience Manager oferece e oferece suporte a vários editores para criar um Formulário. Você pode usar:
* [Editor universal (para criação no WYSIWYG)](#universal-editor-for-wysiwyg-authoring)
* [Microsoft Excel ou Google Sheets (conhecido como criação baseada em documento)](#microsoft-excel-or-google-sheets-known-as-document-based-authoring)

### Editor universal (para criação no WYSIWYG)

O Universal Editor é um editor visual versátil que oferece um recurso &quot;o que você vê é o que você obtém&quot; (WYSIWYG), garantindo uma experiência intuitiva de criação de formulários. É recomendável usar o Editor universal ao criar novos formulários, pois ele fornece um design moderno e fácil de usar e uma interface conveniente de arrastar e soltar.

Para criar formulários usando o Editor universal, os modelos do Edge Delivery Services disponíveis no ambiente do AEM são usados. Esses formulários herdam sua aparência das configurações no repositório do GitHub da Edge Delivery Services. [Uma conexão entre seu ambiente do AEM e o repositório GitHub da Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) foi estabelecida para habilitar a publicação desses formulários no Edge Delivery Services.

Para obter etapas detalhadas sobre como criar usando o Editor Universal, consulte o artigo [Criação de Conteúdo com o Editor Universal](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring).

### Microsoft Excel ou Google Sheets (conhecido como criação baseada em documento)

Você pode criar formulários usando a criação baseada em documentos com arquivos do Microsoft Excel ou do Google Sheets, permitindo que você aproveite os ecossistemas e as APIs robustos do Google Sheets, do Microsoft Excel e do Microsoft SharePoint. Essa abordagem é particularmente útil para criar formulários simples sem serviços de envio avançados.

Para começar a criar um formulário usando o Microsoft Excel ou o Google Sheets, [configure um projeto do AEM usando a matriz da AEM Forms](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) e clone o repositório GitHub correspondente no computador local. O AEM Forms Edge Delivery fornece um recurso chamado Bloco de Forms adaptável, que simplifica o processo de criação de formulários para capturar e armazenar dados. Para saber como criar e publicar formulários usando o Bloco de Forms adaptável no Edge Delivery Services, consulte [Criar um formulário](/help/edge/docs/forms/create-forms.md).

<!--
## Adaptive Forms editors (for Core Components or foundation components based authoring)

You can author forms that are engaging, responsive and dynamic. The Adaptive Form editor provides a user-friendly wizard that allows you to quickly create Adaptive Forms. The form wizard features easy tab navigation, enabling you to select pre-configured templates for foundation or core components, themes, data models, and submission options to create a form efficiently. 

[Authoring forms with Core Components](/help/forms/creating-adaptive-form-core-components.md) allows you to leverage standardized data capture components that can be customized, reducing development time and lowering maintenance costs for digital enrollment experiences. These forms can be published using the Adaptive Forms Block on Edge Delivery Services or through the AEM Publish instance. 

[Authoring forms with Foundation Components](/help/forms/create-an-adaptive-form.md) uses classic data capture components. These forms can only be published using the AEM Publish instance. 

You can also publish forms created using Adaptive Forms Editors on Edge Delivery Services by establishing [connection between your AEM environment and the Edge Delivery Services GitHub repository](/help/edge/docs/forms/publishing-forms.md).


| **Adaptive Forms editors** | Provides a wizard-driven approach to quickly start forms authoring using templates, styling, and predefined fields. | Use these editors to create Core Components based forms or Foundation Components based forms. | These forms can be published on Edge Delivery Services or via AEM Publish instances.  | Use these editors to create Core Components based forms or Foundation Components based forms. Ideal for scenarios involving complex forms, complex workflows, custom actions, or integrations with external systems. |  



## Types of Publishing for Edge Delivery Services Forms

You can publish Edge Delivery Services Forms on one of the following:

* **Edge Delivery Services Form Submission**: Edge Delivery Services Form Submissions ensure that form interactions, including submission and data processing, are handled efficiently and securely. This enables a faster and more reliable user experience, particularly during high traffic periods. By processing form submissions at the edge, Edge Delivery Services minimizes the reliance on a centralized server.

* **AEM Publish instance**: The AEM Forms server offers a publish instance that manages the forms and related assets available to end users.
-->

### Como escolher entre vários tipos de criação de formulário?

A tabela a seguir descreve os recursos e casos de uso para cada editor de criação, ajudando você a escolher o editor correto com base em seus requisitos e necessidades de envio de formulário.

| **Editor de Criação de Formulário** | **Abordagem principal** | **Recursos** | **Método de Publicação** | **Casos de uso** |
|--------|-----------|-------|-------|------------------------------------------------|
| **Criação baseada em documento** | Aproveita ferramentas familiares, como o Google Docs e o Microsoft Office, para a criação de formulários. | Os Forms são projetados usando planilhas, com dados enviados diretamente para as planilhas do Google Sheets ou do Microsoft Excel. </br> </br> Esses formulários são mais rápidos de criar e implantar. Você não precisa de conhecimento prévio do AEM para desenvolver componentes e estilos personalizados para esses formulários. | Esses formulários são publicados no Edge Delivery Services e têm uma pontuação muito alta no Google Lighthouse. </br> </br> A pontuação mais alta resulta em uma renderização mais rápida e melhor SEO. | Esses formulários são ideais para a prototipagem rápida ou formulários básicos em que não são necessários serviços de envio avançados. </br> </br> Eles são adequados para pesquisas, registros ou formulários de feedback que exigem armazenamento de dados em planilhas. Esses formulários são publicados nos serviços da Edge Delivery |
| **Editor Universal** </br> </br> Se você estiver criando um novo formulário, use o Editor Universal para criar formulários. | Oferece uma interface do WYSIWYG para criação intuitiva de formulários. | Os Forms são projetados usando uma interface intuitiva de arrastar e soltar. </br> </br> Esses formulários emprestam aparência do repositório GitHub da Edge Delivery Services configurado para o formulário correspondente. | Esses formulários são publicados no Edge Delivery Services e têm uma pontuação muito alta no Google Lighthouse. </br> </br> A pontuação mais alta resulta em uma renderização mais rápida e melhor SEO. | Esses formulários são ideais para criar formulários para sites e páginas do Edge Delivery Service. Esses formulários apresentam cenários que envolvem formulários complexos, fluxos de trabalho complexos, ações personalizadas ou integrações com sistemas externos |

>[!NOTE]
>
>
> Caso encontre recursos ausentes no Editor universal que estavam disponíveis anteriormente no editor do Adaptive Forms, você pode solicitá-los enviando um email para mailto:aem-forms-ea@adobe.com usando seu endereço de email oficial.

## Consulte também:

{{see-more-forms-eds}}
