---
title: Visão geral do Edge Delivery Services para AEM Forms
description: Saiba como usar o Edge Delivery Services para criar e fornecer formulários de alto desempenho com o AEM Forms, permitindo um desenvolvimento rápido e uma coleta de dados simplificada.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 1ddf97f56e5a9b7c95959da47a748f5a6d128e43
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---


# Edge Delivery Services para AEM Forms


O Edge Delivery Services for AEM Forms é um conjunto combinável de serviços que permite um ambiente de desenvolvimento rápido, em que os autores podem atualizar, publicar e lançar novos formulários rapidamente. Esses serviços oferecem experiências de formulários excepcionais e de alto impacto que impulsionam o engajamento e as conversões. Essas experiências de formulários são fáceis de criar e desenvolver.

* **Experiências mais rápidas**: as Forms são entregues a partir de uma Rede de entrega de conteúdo (CDN) global, garantindo um carregamento rápido para os usuários.
* **Desenvolvimento rápido:** um processo de desenvolvimento simplificado permite atualizações mais rápidas. As alterações podem ser publicadas sem esperar por compilações de pipeline longas.
* **Criação flexível:** escolha entre várias ferramentas para criar formulários, incluindo a criação baseada em documentos (Microsoft Word, Google Docs/Sheets) ou um editor visual do WYSIWYG (Universal Editor).

## Como funciona

Com o Edge Delivery Services, a estrutura e o conteúdo do formulário podem residir em fontes como o AEM as a Cloud Service, o Microsoft SharePoint ou o Google Drive. Esse conteúdo é publicado em um CDN global. Quando um usuário visita o site, o formulário é enviado diretamente do servidor de borda CDN mais próximo para obter o desempenho ideal.

![Diagrama de arquitetura simplificado mostrando fontes de conteúdo, um CDN e o usuário.](/help/forms/assets/eds-simplified-architecture.png)
**Arquitetura simplificada do Edge Delivery Services com o Forms**

Os dados enviados pelos usuários podem ser enviados para vários destinos, de uma planilha simples a um back-end avançado do AEM para processamento adicional.

## Escolha de um método de criação

Há várias maneiras de criar formulários para seus sites do Edge Delivery Services. O melhor método depende das habilidades da equipe, da complexidade do formulário e dos requisitos do projeto.

![Árvore decisória para ajudar a escolher um método de criação de formulário.](/help/forms/assets/eds-authoring-selection.png)
**Árvore de decisão de criação de formulário**

### Criação baseada em documento

Este método permite [criar formulários usando o Microsoft Word ou o Google Docs/Sheets](/help/edge/docs/forms/create-forms.md). Você define campos de formulário, rótulos e tipos em um documento usando um formato de tabela específico. O Edge Delivery Services converte este documento em um formulário interativo do HTML.

**Recursos:**

* Crie em ferramentas familiares: Word, Google Docs ou Google Sheets.
* Defina campos como entradas de texto, email, menus suspensos, caixas de seleção e botões de opção.
* Defina regras básicas de validação, como campos obrigatórios.
* Integre o Google reCAPTCHA para proteção contra spam.
* Suporte para uploads de arquivo.
* Envie dados diretamente para uma planilha ou endereço de email.
* Estenda com código personalizado via GitHub para componentes avançados e estilo.

**Recomendado para:**

* Equipes que usam principalmente editores de documento para criação de conteúdo.
* Criação rápida de formulários simples a moderadamente complexos.
* Coleção de dados simples em uma planilha ou email.

Os envios de formulários baseados em documento geralmente são manipulados pelo [Serviço de Envio do AEM Forms](/help/forms/forms-submission-service.md), que encaminha os dados para uma planilha ou um endereço de email configurado.

### Criação no Editor universal

O [Editor Universal fornece uma interface moderna do WYSIWYG](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) para criar formulários com uma experiência de arrastar e soltar.

**Recursos:**

* Criação visual de formulários do tipo arrastar e soltar com uma biblioteca de componentes pré-construídos.
* Configurar a validação em tempo real e a lógica de negócios complexa (por exemplo, mostrar/ocultar campos com base nas seleções do usuário).
* Visualização ao vivo para diferentes dispositivos.
* Integração profunda com recursos do AEM as a Cloud Service, como Fragmentos de conteúdo, Fluxos de trabalho do AEM e permissões de usuário.
* Criação e edição de formulários assistidos por IA por meio do &quot;Experience Builder&quot;.

**Recomendado para:**

* Criação de formulários complexos com lógica condicional, painéis de várias etapas ou personalização.
* Equipes (por exemplo, profissionais de marketing, usuários empresariais) que preferem ferramentas visuais.
* Projetos que exigem uma forte integração com o back-end do AEM para processamento de dados e fluxos de trabalho.

A Forms criada com o Editor Universal pode usar o [Serviço de Envio do Forms](/help/forms/forms-submission-service.md) ou ser configurada para usar [ações de envio fornecidas para manipulação avançada de dados](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md), como o envio de dados para um Fluxo de Trabalho do AEM, um ponto de extremidade REST ou para um banco de dados.

### Incorporação do Forms nas páginas de criação de documentos

O [Document Authoring (DA)](https://www.aem.live/developer/da-tutorial) é um serviço hospedado pela Adobe para gerenciar conteúdo de sites do Edge Delivery Services. Embora o DA não seja uma ferramenta de criação de formulários em si, você pode usá-la para criar páginas da Web e, em seguida, incorporar formulários criados com outros métodos.

**Como funciona:**

1. **Criar o Formulário:** Crie seu formulário usando a Criação Baseada em Documento ou o Editor Universal.
2. **Publicar o Formulário:** Verifique se o formulário foi publicado e está acessível em sua própria URL.
3. **Incorporar no DA:** Na página Criação de documentos, adicione um bloco que faça referência à URL do formulário para incorporá-lo.

Essa abordagem é para equipes que usam a Criação de documentos como o principal sistema de gerenciamento de conteúdo para sites do Edge Delivery Services.

## Comparação do método de criação

| Critérios | Criação baseada em documento | Editor universal (WYSIWYG) | Forms na criação de documentos (DA) |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **Ferramenta de criação primária** | Word/Google Docs/Planilhas | Navegador (AEM Universal Editor) | N/D (Forms estão *inseridos*) |
| **Nível de habilidade da equipe** | Familiarizar-se com editores de documento | Confortável com as ferramentas visuais da Web | Usa DA para conteúdo da página |
| **Complexidade típica de formulários** | Simples a moderado | Moderado a complexo, nível empresarial | Depende do formulário incorporado |
| **Opções de Envio** | Serviço de envio de Forms (para planilha/e-mail) | Serviço de envio do Forms, Publicação do AEM (fluxo de trabalho, modelo de dados de formulário, integrações de terceiros) | Segue a configuração do formulário incorporado |
| **Integração com o AEM Backend** | Mínimo | Alto (com o envio do AEM Publish) | Indiretamente, por meio do formulário incorporado do Editor universal |
| **Recomendado Para...** | Criação rápida de formulários simples por equipes de conteúdo, captura rápida de dados. | Profissionais de marketing e usuários empresariais que precisam de controle visual, formulários complexos ou integração profunda com o AEM. | Sites onde o conteúdo principal é gerenciado no DA. |

<!-- 
## Detailed Feature Comparison

| **Capability**                        | **Universal Editor (WYSIWYG)** | **Document-based Authoring** | **Document Authoring (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Unified Composition with Sites**    | ✅                            |                              | ✅ (with embedded forms)     |
| **Embedding Form Support**            | ✅                            | ✅                          | ✅ (embed from Universal Editor or Docs)   |
| **Rules (Dynamic Behavior)**          | Advanced rules editor with custom functions | Limited: Show/hide, compute value, custom functions | Depends on embedded form     |
| **Attachment Support**                | ✅                            | ℹ️ (Early Access)           | Depends on embedded form     |
| **CAPTCHA Support**                   | reCAPTCHA Enterprise          | reCAPTCHA Enterprise       | Depends on embedded form     |
| **Submission Features**               | REST, Email, FDM, Workflow, SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion (EA) | Only Spreadsheet            | Follows embedded form's setup |
| **Data Schema**                       | FDM, Custom                   | Custom                      | Based on embedded form       |
| **Pre-fill**                          | 💡 (via Wizard)               | ✅                          | Depends on embedded form     |
| **Fragments**                         | ✅                            | ✅                          | Depends on embedded form     |
| **Visual Rule Editor**                | ✅                            |                              |                              |
| **Localization**                      | 💡 (via Sites)                | ℹ️ (Excel/Sheets manual)    | Depends on embedded form     |
| **Template Support**                  | Only Initial Content          |                              |                              |
| **Theme**                             | ℹ️ (at project level)         | ℹ️ (at project level)        | ℹ️ (based on hosting site)    |
| **Custom Component**                  | ✅                            | ✅                          | ✅ (if embedded component supports it) |
| **Experimentation**                   | ✅                            | ✅                          | Depends on embed context     |
| **Submit Action**                     | ✅                            | Only Spreadsheet            | Based on embedded form       |
-->



## Próximas etapas

* [Criar um formulário com criação baseada em documento](/help/edge/docs/forms/tutorial.md)
* [Saiba mais sobre o Universal Editor para Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Configurar ações de envio de formulário](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
* [Saiba mais sobre a Criação de Documentos (DA)](https://www.aem.live/developer/da-tutorial)
