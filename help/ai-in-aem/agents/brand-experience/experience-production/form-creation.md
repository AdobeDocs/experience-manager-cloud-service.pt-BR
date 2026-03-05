---
title: Trabalho de Criação de Formulário
description: Saiba mais sobre o trabalho de criação de formulários do Brand Experience Agent e como usar a linguagem natural para criar formulários do zero.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 24ad5f36-405b-4ea2-9819-de6aea856a7a
source-git-commit: baf12e49dadc7b25f5169279a52d5712380445de
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---


# Trabalho de Criação de Formulário {#form-creation-job}

O trabalho de criação de formulários faz parte do [Agente de Produção de Experiência](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md), que foi projetado para desenvolver formulários usando prompts de linguagem natural. Esse trabalho gera automaticamente a estrutura de formulário e os tipos de campo apropriados. O trabalho é revelado pelo Assistente de IA.

Alguns dos principais benefícios do trabalho de criação de formulários incluem:

* **Desenvolvimento de formulários acelerado**: crie formulários rapidamente usando comandos de linguagem natural simples, eliminando a necessidade de aprender interfaces de produtos tradicionais.
* **Experiências consistentes e sob marca**: crie formulários que sigam as diretrizes de marca, modelos e estilo de sua organização usando modelos e estilos aprovados.
* **Barreira técnica mais baixa**: permite que os usuários empresariais criem formulários facilmente, sem precisar de conhecimento técnico avançado ou de produtos aprofundados.

## Recursos {#capabilities}

* **Criar um novo formulário com prompt de texto sem formatação**: você pode criar um formulário enviando seus requisitos em linguagem sem formatação. A habilidade gera automaticamente a estrutura de formulário, os tipos de campo e as experiências na marca apropriadas com base na descrição do idioma natural e no modelo especificado. Esse recurso acelera a criação de formulários, garantindo ao mesmo tempo a manutenção dos padrões de marca e conformidade.

* **Importar um documento do PDF e convertê-lo em um formulário**: você pode importar e transformar documentos existentes do PDF em formulários. A habilidade analisa o conteúdo carregado para detectar tipos de campo, preservar layouts e aprimorar os formulários com design responsivo e lógica de validação enquanto garante que os padrões de marca e conformidade sejam mantidos.

Ao usar qualquer um desses recursos, você será solicitado a escolher o tipo de formulário a ser criado. Especifique um modelo de formulários adaptáveis com base em Componentes principais ou um modelo de formulários adaptáveis com base em Edge Delivery Services e indique o caminho de sua preferência para salvar o formulário. Se você estiver criando um formulário com base no Edge Delivery Services, também poderá especificar a URL do GitHub do seu repositório.


### Exemplos de Prompts {#sample-prompts}

* *Crie um formulário para a coleção de comentários com campos de nome, email e mensagem*
* *Crie um formulário de feedback do cliente com classificação de produto (1-5 estrelas), campo de comentário e email opcional*
* *Criar um formulário de contato com nome, email, lista suspensa de assunto e campos de mensagem*
* *Crie um formulário de registro com informações pessoais, preferências de conta e aceitação de termos*
* *Crie um formulário de solicitação de cartão de crédito importando o arquivo do PDF disponível em`https://[aem-author-url]/path/to/pdf/file`*
* *Criar um formulário de comentários usando o modelo padrão em`https://github.com/wkndforms/wesecure`*

## Refinar o formulário {#refine-with-forms-experience-builder}

Depois de criar a estrutura do formulário inicial usando o Assistente de IA, é possível usar o Forms Experience Builder para:

* **Atualizar formulários**: adicione ou modifique campos, ajuste tipos de campos e atualize o estilo conforme necessário por meio do editor visual.

* **Atualizar layout**: reorganize seções, grupos ou campos, ajuste o espaçamento e modifique a hierarquia visual para aprimorar a usabilidade e garantir que o formulário seja claro e intuitivo para o público-alvo.

* **Adicionar lógica de negócios**: criar lógica condicional, mostrar/ocultar regras, dependências de campo e definir regras de validação.

* **Configurar envio**: configure para onde os dados do formulário são enviados, incluindo a configuração de notificações por email, integrações com fluxos de trabalho ou conexões com sistemas externos.

Para obter mais informações, consulte a [documentação do Forms Experience Builder.](/help/forms/experience-builder/product-overview.md)

## Ativação {#activation}

Você pode explorar os Agentes da AEM por meio do [Playground](https://www.aem.live/developer/aem-playground) ou conectar-se com seu CSM ou TAM para discutir o acesso por meio da SKU do Agente.

<!-- 
#### Import and convert {#import-and-convert}

Transform existing documents into interactive digital forms. The agent analyzes uploaded content to detect field types, preserve layouts, and enhance forms with responsive design and validation logic. Supported formats include Acroforms, XFA PDFs, flat PDFs, images (JPG, PNG), and hand-drawn form photographs.

>[!VIDEO](https://video.tv.adobe.com/v/3474042)

**Prompt examples:**

* *Convert the attached PDF file to an adaptive form*
* *Transform this scanned form image into an interactive digital form*
* *Import the employee onboarding PDF and create an editable form*
* *Convert this paper form photograph into a digital form with validation*
-->

<!-- 
### Embed an existing form to a sites page {#embed-existing-form}

The form creation skill enables seamless integration of existing forms into any sites page through natural language commands. Rather than manually locating, copying, and embedding form components, users can simply specify which form to add and where to place it. The agent handles the technical implementation, ensuring proper rendering and functionality.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Embed the contact form to the homepage*
* *Add the existing customer feedback form to the support page*
* *Insert the newsletter signup form into the footer section*
* *Place the registration form on /content/site/signup*
* *Add form "contact-us-2024" to the current page*
-->

<!-- 
### Build and add a form to an existing sites page {#build-and-add-form}

The form creation skill combines form creation and site integration in a single conversational workflow. Users can describe the form they need and specify where to add it, and the agent creates the form and embeds it into the specified page automatically. This eliminates the traditional multi-step process of creating a form separately and then manually adding it to a page.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Create a newsletter signup form with email field and add it to the footer*
* *Build a quick contact form with name, email, and message, then add it to /content/about-us*
* *Add a feedback form with rating stars and comment field to this page*
* *Create a simple survey form with 5 questions and embed it on the customer portal homepage*
* *Build an event registration form with name, email, and date selection, then add it to /content/events/conference-2025*
-->
