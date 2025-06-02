---
title: Assistente de IA para o AEM Forms (Forms Experience Builder)
description: Crie formulários avançados mais rapidamente usando os Fragmentos de formulário
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 67416999d068af6350748d610e7c1c7b1d991bc4
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 1%

---

# Assistente de IA para o AEM Forms (Forms Experience Builder)

>[!NOTE]
>
>
> O recurso Assistente de IA para o AEM Forms (Forms Experience Builder) está disponível no programa dos primeiros usuários. Caso esteja interessado, envie um email rápido do seu endereço comercial para mailto:aem-forms-ea@adobe.com para solicitar acesso ao recurso.


O Assistente de IA para o AEM Forms (Forms Experience Builder) aprimora sua experiência de criação simplificando tarefas comuns de criação de formulários por meio de prompts de linguagem natural. Disponível no Forms Manager, no Editor Forms adaptável e no Editor universal, ele permite que você crie de maneira mais inteligente e rápida, oferecendo suporte às ações de criação e configuração. Este guia ajudará você a começar e aproveitar ao máximo seus recursos.

## Introdução

Antes de se aprofundar, abordemos as noções básicas de acesso e interação com o Assistente de IA.

### Acessar o assistente de IA

Você pode acessar o Assistente de IA em três locais diferentes no AEM Forms:

1. **Gerenciador do Forms**
   - Navegue até: Adobe Experience Manager > Forms > Forms e documentos
   - Procure o ícone do Assistente do AI no lado esquerdo da interface
   - Clique no ícone para abrir o painel Assistente de IA

   ![Ícone do Assistente de IA*](/help/edge/docs/forms/assets/forms-manager.gif)

2. **Editor Forms adaptável**
   - Navegue até: Adobe Experience Manager > Forms > Forms e documentos
   - Selecionar e abrir um formulário para edição
   - Clique no ícone do Assistente de IA na interface do editor

   ![Ícone do Assistente de IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif)

3. **Editor Universal**

   - Navegue até: Adobe Experience Manager > Forms > Forms e documentos
   - Procure o ícone do Assistente do AI no lado esquerdo da interface
   - Clique no ícone do Assistente de IA na interface do editor

O Assistente de IA adapta sua funcionalidade com base na localização e tarefa atuais, fornecendo assistência relevante para cada contexto.

### Como interagir:

- Basta digitar a solicitação em linguagem natural.
- Use `/` para exibir uma lista de comandos ou ações rápidas disponíveis.
- Referencie campos de formulário específicos usando `@fieldName` (por exemplo, `@firstName`, `@emailAddress`) quando desejar que o assistente configure ou atualize esse campo específico.


### Início rápido

Comece a trabalhar rapidamente assistindo ao nosso vídeo introdutório:

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)


Este vídeo aborda o lançamento do assistente em todos os ambientes, a interação básica e uma visão geral de seus recursos.

## Referência de comando do assistente de IA

| Comando | Descrição | Propósito | Contexto de uso | Exemplos | Principais recursos |
|---------|-------------|---------|---------------|----------|--------------|
| /create-form | Inicie um novo formulário no Forms Manager ou no Forms Editor | Inicia a criação de um formulário completamente novo do zero | Forms Manager, Editor Forms adaptável | /create-form pesquisa de feedback do cliente | Fornece opções para a estrutura de formulários e cria o formulário |
| /add-form | Adicionar um novo formulário no Editor Universal | Adiciona um novo bloco de formulário ou componente no Universal Editor | Editor universal para Edge Delivery Services | /add-form formulário de contato com nome e email | Insere blocos de formulário, funciona com edição baseada em blocos |
| /update-layout | Alterar o layout do formulário para design responsivo de acordeão, baseado em guia, assistente ou página única | Modifica o layout estrutural geral e o padrão de navegação | Todos os ambientes de edição | Assistente /update-layout com 3 etapas | Opções responsivas de acordeão, guias, assistente e página única |
| /update-field | Modificar propriedades e configuração de campos de formulário existentes | Altera atributos de campo como rótulos, validação, formatação e comportamento | Todos os ambientes de edição | /update-field @email a ser exigido com validação | Rótulos, regras de validação, tipos de campo, padrões, visibilidade |
| /create-rule | Criar comportamento dinâmico e lógica condicional para formulários | Implementa lógica de negócios, cálculos, interações condicionais | Todos os ambientes de edição | /create-rule mostrar @spouseName se @maritalStatus for igual a &quot;Casado&quot; | Visibilidade condicional, cálculos, validação, definição de valor |
| /create-panel | Criar um novo painel (contêiner para agrupar campos relacionados) | Adiciona contêineres estruturais para organizar campos de formulário logicamente | Todos os ambientes de edição | /create-panel Informações pessoais com nome, email, telefone | Agrupamento de campos, títulos, opções de layout, seções que podem ser recolhidas |
| /add-panel | Conversão de uma imagem para o painel de formulário no Editor universal | Usa IA para analisar imagens carregadas e converter em painéis de formulários estruturados | Editor universal | /add-panel da imagem de formulário carregada | Reconhecimento de imagem, conversão de visual em funcional, preservação de layout |
| /configure-submit | Configurar ações de envio de formulário e manipulação de dados | Define o que acontece quando os usuários enviam o formulário preenchido | Todos os ambientes de edição | /configure-submit para enviar email a `support@company.com` | Email, API REST, fluxos de trabalho, planilhas, bancos de dados, Power Automate |
| /help | Acessar a assistência e a documentação no Assistente de IA | Fornece ajuda contextual, orientação e respostas sobre o AEM Forms | Todos os ambientes de edição | /help como criar formulários com várias etapas? | Explicações de recursos, guias, práticas recomendadas, solução de problemas |

### Categorias de comando

| Categoria | Comandos | Principais casos de uso |
|----------|----------|-------------------|
| Criação de formulário | /create-form, /add-form | Início de novos formulários, adição de blocos de formulário |
| Estrutura e layout | /update-layout, /create-panel, /add-panel | Organização da estrutura do formulário, design visual |
| Gerenciamento de campo | /update-field | Configuração de elementos de formulário individuais |
| Lógica e regras | /create-rule | Adicionar comportamento e validação dinâmicos |
| Envio | /configure-submit | Configuração do manuseio de dados e workflows |
| Suporte | /help | Obter assistência e documentação |

### Diretrizes de sintaxe

| Elemento | Formato | Exemplo | Notas |
|---------|--------|---------|-------|
| Comandos | /command-name | /create-form | Sempre iniciar com barra |
| Referências de campo | @fieldName | @email, @firstName | Usar o símbolo @ para campos existentes |
| Linguagem natural | Command + description | /create-rule mostrar campo se condição | Combinar comandos com texto descritivo |
| Várias ações | Comandos separados | /create-panel e /update-layout | Aplicar um comando de cada vez |


### Recursos específicos do ambiente

| Ambiente | Comandos disponíveis | Recursos especiais |
|-------------|-------------------|------------------|
| Gerenciador do Forms | /create-form, /help | Criação e gerenciamento de nível de formulário |
| Editor adaptável do Forms e editor universal | Todos os comandos | Conjunto completo de recursos, configuração detalhada |



### Sintaxe de referência de campo (elementos contextuais)

Use `@fieldName` para referenciar campos existentes:

- `@firstName` - Campo de nome
- `@email` - Campo de email
- `@phoneNumber` - Campo de número de telefone
- `@dateOfBirth` - Campo de data de nascimento

### Tipos de componentes

Esta lista abrange tipos de componentes comuns. A IA pode reconhecer variações ou tipos mais especializados, mas usar esses termos precisos produz os melhores resultados:

- `text input` - Campo de texto de linha única
- `text area` - Campo de texto multilinha
- `dropdown` - Selecionar lista
- `checkbox` - Caixa de seleção única
- `checkbox group` - Várias caixas de seleção
- `radio group` - Grupo de botões de opção
- `date picker` - Seleção de data
- `file upload` - Anexo de arquivo
- `panel` - Contêiner de campos de agrupamento


## Principais recursos e exemplos de prompts expandidos

O Assistente de IA entende uma grande variedade de comandos. Aqui estão alguns exemplos para ilustrar seu poder. Lembre-se de usar termos precisos para componentes como &quot;painel&quot;, &quot;entrada de texto&quot;, &quot;caixa de seleção&quot; etc.

| Categoria de recurso | Descrição | Exemplo de Prompts |
| ------------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Criação de formulário** | Inicie um novo formulário do zero ou com base em uma descrição. | `Create a new form titled 'Employee Onboarding'.` <br> `Generate a customer feedback form with fields for name, email, rating (1-5 stars), and comments.` <br> `Start a simple contact form with name, email, and message fields.` <br> `Design a multi-page registration form for an event.` |
| **Importar Design** | Converta um design existente (imagem, Figma, PDF) em um formulário do AEM. | `Import the form design from this uploaded PDF file.` <br> `Convert the uploaded Figma design into an adaptive form, focusing on the 'User Profile' frame.` <br> `Use this JPEG image of our old paper form to create a new digital version.` <br> `Create a form based on the layout of the attached PNG.` |
| **Adicionando componentes e painéis** | Adicione vários campos de formulário e contêineres estruturais (painéis). | `Add a text input field for 'First Name'.` <br> `Add a 'Personal Details' panel with fields for full name, date of birth, and phone number.` <br> `Insert a checkbox group for 'Interests' with options: Technology, Sports, Music.` <br> `Add a file upload component for 'Resume'.` <br> `Create a repeatable panel named 'WorkExperience' with fields for company, title, and dates.` |
| **Ajustes de layout** | Modifique a estrutura e a aparência do layout do formulário. | `Change the 'Personal Details' panel to a two-column layout.` <br> `Set the overall form layout to a wizard (multi-step) navigation.` <br> `Make the header section span the full width of the form.` <br> `Adjust the spacing between fields in the 'Address' panel to be compact.` <br> `Align all field labels to the left.` |
| **Lógica e criação da regra** | Implementar comportamento dinâmico, cálculos e visibilidade condicional. | `Make the 'Spouse Name' field visible only if 'Marital Status' is selected as 'Married'.` <br> `Calculate the 'Total Amount' by multiplying @quantity and @price.` <br> `Enable the submit button only when the @termsAndConditions checkbox is checked.` <br> `Set the value of @countryCode to '+1' if @country is 'United States'.` <br> `If @age is less than 18, show a message 'Must be 18 or older'.` |
| **Atualização de Propriedades do Campo** | Modifique atributos de campos de formulário específicos, como rótulos, espaços reservados etc. | `Change the label of @email to 'Primary Email Address'.` <br> `Set the @comment field to be a multi-line text area.` <br> `Make the @phoneNumber field mandatory.` <br> `Add placeholder text 'Enter your ZIP code' to the @zipCode field.` <br> `Change the @country field to a dropdown and populate it with: USA, Canada, UK, Germany.` <br> `Update the help description for @password to 'Must include an uppercase letter, a number, and be at least 8 characters long.'` <br> `Set the maximum length of the @username field to 15 characters.` <br> `Configure the @dateOfBirth field to use a date picker.` |
| **Enviar Ações** | Defina o que acontece quando um usuário envia o formulário. | `Configure the form to submit data to the REST endpoint /api/v2/application-submit.` <br> `Set up an email submission to hr@example.com and sales@example.com on successful submission.` <br> `Trigger an AEM workflow named 'NewLeadProcessing' when this form is submitted.` <br> `On submit, redirect the user to a thank you page at /content/thankyou.html.` |
| **Tema** | Aplique temas existentes do AEM Forms para estilizar o formulário. | `Apply the 'Modern Business' theme to this form.` <br> `Switch to the 'Accessible Dark' theme.` <br> `Revert to the default canvas theme.` |
| **Navegação e estrutura** | Adicione elementos de navegação ou reorganize partes do formulário. | `Add a 'Next' button to the current panel and a 'Previous' button to the next panel.` <br> `Create a Table of Contents based on the form's panels.` <br> `Move the 'Address' panel to be before the 'Contact Information' panel.` |
| **Validação** | Definir regras de validação específicas para campos. | `Set a regex pattern for the @employeeID field to be 'EMP\d{5}'.` <br> `Ensure the @age field only accepts numeric values between 18 and 99.` <br> `Validate the @email field to ensure it is a valid email format.` |
| **Plano de Revisão** (Editor Universal) | Visualize as alterações propostas pelo assistente antes da execução. | `Add a contact form with fields for name, email, subject, and message.` (O assistente mostrará um plano de componentes e propriedades que ele criará, depois você clicará em &quot;Aplicar&quot;). |

## Práticas recomendadas para resultados ideais

Para aproveitar ao máximo o Assistente de IA, lembre-se das seguintes dicas:

- **Iniciar simples, criar incrementalmente:** comece com comandos menores e específicos (por exemplo, &quot;Adicionar uma entrada de texto para &#39;Nome&#39;&quot;) em vez de solicitações de várias etapas muito complexas inicialmente.
- **Usar terminologia do AEM Forms:** Use termos como &quot;painel&quot;, &quot;campo de entrada de texto&quot;, &quot;grupo de caixas de seleção&quot;, &quot;ação de envio&quot;, &quot;regra&quot; etc. para melhor compreensão pelo assistente.
- **Referenciar Campos Claramente:** Ao configurar campos existentes, use a notação `@fieldName` (por exemplo, `Make @firstName mandatory`).
- **Revisar Planos** Sempre reveja cuidadosamente os planos para alterações propostas pelo assistente no Editor Universal antes de clicar em &quot;Aplicar&quot;.
- **Validar manualmente:** depois que o assistente fizer alterações, sempre visualize e teste o formulário para garantir que ele se comporte e tenha a aparência esperada. A IA é uma ferramenta poderosa, mas a validação final é fundamental.
- **Iterar e Refinar:** Se o primeiro prompt não fornecer o resultado exato, tente reformular a frase ou dividir a solicitação em etapas menores.
- **Fornecer Feedback:** use o mecanismo de feedback integrado para ajudar o assistente a aprender e melhorar (consulte a seção &quot;Feedback &amp; Suporte&quot;).

## Ajuda do produto com o Assistente de IA

O Assistente de IA para o AEM Forms não se destina apenas à criação; também pode ajudá-lo a aprender, entender e usar vários recursos do AEM Forms.

### Tópicos de ajuda suportados

Faça perguntas para o assistente como:

- &quot;Como criar um novo formulário adaptável do zero?&quot;
- &quot;O que é um painel no Adaptive Forms e como ele é usado?&quot;
- &quot;Explique como aplicar um tema a um formulário.&quot;
- &quot;Quais tipos de layout são compatíveis com formulários e painéis?&quot;
- &quot;Como configurar diferentes ações de envio, como enviar um email?&quot;
- &quot;Você pode me orientar sobre como usar um design Figma para criar um formulário?&quot;
- &quot;Qual é a melhor maneira de criar um formulário de várias etapas?&quot;

### Como solicitar ajuda:

1. Abra o Assistente de IA no Forms Manager ou no Editor Forms adaptável.
2. Digite a pergunta em linguagem natural (por exemplo, &quot;Como adicionar um painel repetível?&quot;).
3. O assistente responderá com:
   - Instruções detalhadas.
   - Explicações dos conceitos do AEM Forms.
   - Links para a documentação relevante da Adobe Experience League, se aplicável.

### Dicas para obter ajuda melhor:

- **Seja específico:** faça uma pergunta clara de cada vez.
- **Usar palavras-chave:** Inclua palavras-chave relevantes para recursos do AEM Forms ou elementos da interface do usuário (por exemplo, &quot;editor de formulário adaptável&quot;, &quot;editor de regras&quot;, &quot;tema&quot;).
- **Reformular a frase se necessário:** Se o assistente não entender ou fornecer as informações desejadas, tente simplificar a pergunta ou usar termos diferentes.


## Solução de problemas comuns

- **Assistente Não Está Respondendo:**
   - Verifique se você está trabalhando ativamente em um ambiente compatível (Forms Manager, Editor adaptável do Forms ou Editor universal).
   - Verifique sua conexão com a Internet.
   - Tente fechar e reabrir o painel do Assistente de IA.

- **Respostas Imprecisas ou Inesperadas:**
   - Reescreva sua solicitação para ser mais específico ou mais simples.
   - Divida uma solicitação complexa em comandos individuais menores.
   - Verifique se você está usando a terminologia padrão do AEM Forms.

- **Problemas de Importação do Design (PDF/Figma/Image):**
   - Verifique se o arquivo de design é claro, bem estruturado e legível.
   - Verifique se o formato do arquivo é compatível (PDF, link físico, tipos de imagem comuns, como PNG, JPG).
   - Para o Figma, verifique se o quadro que você está direcionando está claramente definido e acessível.

- **Campo `@fieldName` Não Reconhecido:**
   - Verifique novamente o nome exato do campo no formulário. Os nomes de campos diferenciam maiúsculas de minúsculas e devem corresponder exatamente.
   - Verifique se o campo já existe se você estiver tentando modificá-lo.


## Feedback e suporte

Sua contribuição é inestimável para o aprimoramento contínuo do Assistente de IA.

- **Fornecer Comentários:** Use o comando ou botão **&quot;Fornecer Comentários&quot;** interno na interface do Assistente de IA para compartilhar suas experiências, relatar problemas ou sugerir melhorias. (por exemplo, você pode digitar `/feedback` ou procurar por um ícone de feedback).
- **Suporte Oficial** Para questões críticas ou assistência adicional, entre em contato com os canais oficiais de suporte da Adobe ou com os contatos de suporte designados de sua organização.


## Conteúdo relacionado

[Assistente do AEM Forms AI - Biblioteca de prompts](/help/edge/docs/forms/ai-assistant-prompt-library.md)
