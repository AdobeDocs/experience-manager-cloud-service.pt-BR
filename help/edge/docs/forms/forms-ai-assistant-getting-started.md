---
title: Introdução ao Forms Experience Builder
description: Saiba como usar o Forms Experience Builder para criar e gerenciar formulários com divulgação progressiva para todos os tipos de usuários
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 2%

---


# Introdução ao Forms Experience Builder

>[!NOTE]
>
> O recurso Forms Experience Builder está disponível no **programa de usuários iniciais**. Se estiver interessado, envie um email rápido do seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso ao recurso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta documentação está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os recursos, os comandos e os exemplos podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção inicial.

Este guia abrangente ajuda você a começar a criar e gerenciar formulários usando a tecnologia de IA de conversação. Seja você um iniciante procurando criar seu primeiro formulário ou um usuário avançado procurando aproveitar recursos sofisticados, você encontrará informações detalhadas e exemplos práticos para orientar sua jornada pelos recursos do Forms Experience Builder.

## Pré-requisitos e configuração

### &#x200B;1. Solicitar acesso

Se você não tiver acesso ao Forms Experience Builder:

1. **Solicitar Acesso**: Enviar um email para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) a partir do seu email comercial
2. **Incluir Informações**: nome da organização e detalhes do projeto
3. **Aguardar Aprovação**: a Adobe revisará e fornecerá instruções de integração

### &#x200B;2. Verifique se o Forms está ativado

Antes de usar o Forms Experience Builder, verifique se o [AEM Forms está habilitado para o seu ambiente](/help/forms/setup-forms-cloud-service.md).


### &#x200B;3. Configurar o ambiente


* **Para Edge Delivery Services (EDS):**

   * [Configurar ambiente para o Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
   * [Criar um novo formulário usando o modelo do Edge Delivery Forms](/help/edge/docs/forms/universal-editor/create-forms.md)

* **Para formulários baseados em Componentes Principais:**

   * Na sua instância do Adobe Experience Manager, acessei Forms > Forms e Documentos
   * [Criar uma nova página usando o modelo dos Componentes principais](/help/forms/creating-adaptive-form-core-components.md)

## Início rápido

### Acessar o Forms Experience Builder

**Editor Universal**

* Abra a página EDS no Editor universal
* Procure o ícone Forms Experience Builder no painel esquerdo
* Clique para abrir a interface conversacional

**Editor Forms adaptável**

* Navegue até: AEM > Forms > Forms e documentos
* Criar ou abrir um formulário baseado em componentes principais para edição
* Clique no ícone do Forms Experience Builder na barra de ferramentas do editor

### Seu primeiro formulário

Tente esta conversa simples para começar:

```
👤 You: "Create a simple contact form"
🤖 AI: "I'll create a contact form with name, email, and message fields for you."

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation."
```

### Comandos Essenciais

| Símbolo | Propósito | Como usar |
|--------|---------|------------|
| `/` | Ações rápidas e atalhos | Digite `/create` para criação de formulário, `/help` para assistência |
| `@` | Fazer referência a campos de formulário existentes | Digite `@fieldName` para modificar campos específicos (por exemplo, `@email`) |
| Texto sem formatação | Conversação natural | Descreva o que você deseja: &quot;Adicionar um campo de número de telefone obrigatório&quot; |

### Dicas para se dar bem

* **Seja específico**: &quot;Adicionar um campo de email necessário com validação&quot; funciona melhor do que &quot;adicionar email&quot;
* **Fazer referência a campos existentes**: usar `@fieldName` ao modificar formulários
* **Solicitar ajuda**: Digite `/help` seguido da sua pergunta
* **Iterar**: fazer uma alteração de cada vez para obter melhores resultados


## Maneiras de começar a criar um Formulário

### &#x200B;1. Comece com prompts de linguagem natural

Descreva os requisitos de formulário em linguagem natural, e o Forms Experience Builder gera a estrutura completa do formulário:

**Exemplos:**

* &quot;Crie um formulário de solicitação de empréstimo com informações pessoais, detalhes financeiros e uploads de documentos&quot;
* &quot;Crie um formulário de feedback do cliente com classificações, comentários e categorias do produto&quot;
* &quot;Preciso de um formulário de inscrição em várias etapas para uma conferência com processamento de pagamento&quot;

### &#x200B;2. Importar e converter

Transforme formulários e documentos existentes em experiências modernas e interativas:

**Fontes com Suporte:**

* **PDF forms**: carregue PDFs estáticos para convertê-los em formulários digitais interativos com validações.
* **Capturas de tela ou Imagens**: carregue fotos de formulários em papel para gerar versões digitais funcionais
* **HTML Forms**: importe e converta formulários Web básicos em AEM Forms aprimorado com recursos avançados
* **XFA Forms**: converter formulários herdados baseados em XFA em formulários responsivos modernos
* **URLs**: converter formulários Web existentes em AEM Forms nativo com UX aprimorado

**Como importar:**

1. Clique no ícone de anexo na interface do Forms Experience Builder
2. Faça upload do seu arquivo (PDF, imagem, design de imagem etc.)
3. Descreva suas necessidades:
   * &quot;Converter este formulário do PDF em uma versão digital&quot;
   * &quot;Criar um formulário correspondente a este layout de captura de tela&quot;
   * &quot;Criar este formulário a partir do meu design do Figma&quot;

**Tipos de Arquivos com Suporte:**

* **Imagens** (PNG, JPG, GIF): layouts de formulário, modelos de interface do usuário, formulários digitalizados
* **Arquivos do PDF**: formulários, especificações, documentos existentes
* **Arquivos Figma**: protótipos de design, diretrizes de marca
* **Arquivos de Design**: referências visuais, guias de estilo

### Interações principais

#### Adição de elementos de formulário

**Adições básicas:**

```
👤 You: "Add a section for personal information"
🤖 AI: "Added a personal information panel with standard fields"

👤 You: "Include a file upload for resume"
🤖 AI: "Added a secure file upload component for documents"

👤 You: "Add a dropdown for country selection"
🤖 AI: "Added a country dropdown with common options"
```

**Especificações detalhadas:**

```
👤 You: "Add a personal information panel with fields for full name, date of birth, phone number, and email address"
🤖 AI: "Created a personal information panel with all requested fields and appropriate validation"

👤 You: "Include a secure file upload component for documents, limited to PDF files under 5MB"
🤖 AI: "Added a file upload field with PDF restriction and 5MB size limit"

👤 You: "Add a country dropdown with options for USA, Canada, UK, and Germany"
🤖 AI: "Added a country dropdown with the specified options"
```

#### Criar comportamento dinâmico

**Lógica simples:**

```
👤 You: "Show additional fields when 'Other' is selected"
🤖 AI: "Created a conditional rule that shows additional fields when 'Other' is chosen"

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation"

👤 You: "Calculate the total automatically"
🤖 AI: "Added calculation logic to automatically compute totals"
```

**Regras de negócio complexas:**

```
👤 You: "Show the spouse information fields only when marital status is set to 'Married'"
🤖 AI: "Created a conditional rule that displays spouse fields based on marital status"

👤 You: "Calculate the total cost by multiplying quantity and price, then add 10% tax"
🤖 AI: "Added calculation logic with quantity, price, and tax computation"

👤 You: "Enable the submit button only when all required fields are completed and terms are accepted"
🤖 AI: "Created validation logic that enables submission only when all conditions are met"
```

#### Layout e design do formulário

**Alterações de layout:**

```
👤 You: "Make this a multi-step form"
🤖 AI: "Converted the form to a progressive layout with navigation"

👤 You: "Organize fields in two columns"
🤖 AI: "Updated the layout to display fields in a two-column arrangement"

👤 You: "Convert to an accordion layout"
🤖 AI: "Transformed the form to use accordion-style sections"
```

**Melhorias de design:**

```
👤 You: "Create a wizard-style form with 3 steps: personal info, preferences, and review"
🤖 AI: "Created a wizard form with three distinct steps and navigation"

👤 You: "Arrange the address fields in a compact two-column layout"
🤖 AI: "Organized address fields in a compact two-column format"

👤 You: "Update the layout to match the attached wireframe"
🤖 AI: "Modified the layout to match the provided design reference"
```

### Configuração da integração

O Forms Experience Builder pode configurar vários endpoints de envio para conectar seus formulários a sistemas e serviços externos:

| Tipo de integração | Comando de configuração | Caso de uso |
|------------------|---------------|----------|
| **Email** | &quot;Enviar formulário para email&quot; | Notificações e confirmações para envios de formulários |
| **REST API** | &quot;Enviar para endpoint REST&quot; | Aplicativos personalizados e sistemas de terceiros |
| **Armazenamento na nuvem** | &quot;Salvar no Azure/SharePoint&quot; | Armazenamento de documentos e gerenciamento de arquivos |
| **Fluxo de trabalho** | &quot;Conexão com o Power Automate&quot; | Automação e aprovações de processos de negócios |
| **Marketing** | &quot;Integrar ao Marketo&quot; | Gerenciamento de clientes potenciais e automação de marketing |

**Exemplos de integração avançada:**

```
👤 You: "Send form submissions to hr@company.com and create a case in our CRM system"
🤖 AI: "Configured email submission and CRM integration"

👤 You: "Submit data to our REST API endpoint and trigger the new customer workflow"
🤖 AI: "Set up REST API submission with workflow triggers"

👤 You: "Email responses to the sales team and add the lead to our marketing automation platform"
🤖 AI: "Configured multi-channel submission with email and marketing automation"
```





## Operações avançadas de formulários


### Criação de regra complexa

Crie validação sofisticada e lógica de negócios que responda às interações do usuário e garanta a integridade dos dados:

```
👤 You: "Show the address section only if the user selects 'Ship to different address'"
🤖 AI: "Created a conditional rule that shows/hides the address panel based on checkbox selection"
```

### Criação de formulário de várias etapas

```
👤 You: "Create a progressive form with 3 steps: personal info, preferences, confirmation"
🤖 AI: "Created a progressive form with navigation between steps and validation at each stage"
```

### Tipos de campo avançados

* Upload de arquivo com restrições de validação e tamanho para gerenciamento de documentos
* Seletores de data com restrições e regras de negócios para agendamento
* Menus suspensos com opções dinâmicas que mudam com base nas seleções do usuário
* Botões de opção com lógica condicional para árvores de decisão complexas


### Conversão do PDF em formulário

```
👤 You: "Convert this PDF into an interactive form"
🤖 AI: "Analyzed the PDF and created a form with appropriate field types and validation"
```

### URL para conversão de formulário

```
👤 You: "Create a form from this website"
🤖 AI: "Extracted form elements and created a native AEM Form with enhanced functionality"
```

### Análise de desempenho

```
👤 You: "Analyze this form's conversion performance"
🤖 AI: "Provided insights on form effectiveness and suggested optimizations"
```

### Personalização avançada

#### Regras de validação personalizadas

* Dependências de campo que criam comportamento de formulário dinâmico com base nas entradas do usuário
* Lógica condicional complexa que adapta a experiência do formulário às necessidades do usuário
* Mensagens de erro personalizadas que fornecem orientação clara aos usuários
* Validação entre campos que garante a consistência dos dados em várias entradas

#### Otimização de layout

* Capacidade de resposta móvel que garante que os formulários funcionem perfeitamente em todos os dispositivos
* Conformidade para acessibilidade que torna os formulários utilizáveis por pessoas com deficiência
* Melhorias no design visual que aumentam as taxas de envolvimento e conclusão do usuário
* Aprimoramentos na experiência do usuário que reduzem o atrito e melhoram a satisfação

#### Fluxos de trabalho de integração

* Processos de aprovação em várias etapas que direcionam envios de formulários por meio de fluxos de trabalho de negócios
* Transformação de dados que converte dados de formulário em formatos exigidos por sistemas externos
* Lógica de negócios personalizada que aplica regras e cálculos específicos aos envios de formulários
* Tratamento de erros avançado que proporciona uma recuperação perfeita de problemas do sistema

## Referência de comando

### Comandos Essenciais

| Símbolo | Propósito | Como usar |
|--------|---------|------------|
| `/` | Ações rápidas e atalhos | Digite `/create` para criação de formulário, `/help` para assistência |
| `@` | Fazer referência a campos de formulário existentes | Digite `@fieldName` para modificar campos específicos (por exemplo, `@email`) |
| Texto sem formatação | Conversação natural | Descreva o que você deseja: &quot;Adicionar um campo de número de telefone obrigatório&quot; |

### Comandos de barra

| Comando | Contexto | Exemplo de uso |
|---------|---------|---------------|
| `/create-form` | Todos os ambientes | `/create-form customer survey` |
| `/add-form` | Editor universal | `/add-form contact form` |
| `/update-layout` | Editor de formulário | `/update-layout wizard with 3 steps` |
| `/update-field` | Editor de formulário | `/update-field @email to be required` |
| `/create-rule` | Editor de formulário | `/create-rule show @spouse if married` |
| `/create-panel` | Editor de formulário | `/create-panel Personal Information` |
| `/configure-submit` | Editor de formulário | `/configure-submit to email support` |
| `/help` | Todos os ambientes | `/help multi-step forms` |

### Referências de campo

Use `@fieldName` para referenciar campos existentes:

* `@firstName`, `@lastName` * Campos de nome
* `@email`, `@phoneNumber` * Campos de contato
* `@address`, `@city`, `@zipCode` * Campos de endereço
* `@dateOfBirth`, `@startDate` * Campos de data

### Tipos de componentes

Use estes termos ao descrever elementos de formulário:

* `text input` * Campo de texto de linha única
* `text area` * Campo de texto de várias linhas
* `dropdown` * Selecionar lista com opções
* `checkbox` * Caixa de seleção única
* `checkbox group` * Várias caixas de seleção
* `radio group` * Grupo de botões de opção
* `date picker` * Campo de seleção de data
* `file upload` * Campo de anexo de arquivo
* `panel` * Contêiner para campos de agrupamento

### Comandos de integração

| Serviço | Comando da linguagem natural | Requisitos |
|---------|--------------------------|--------------|
| Email | &quot;Enviar envios para [email]&quot; | Endereço de email válido |
| REST API | &quot;Enviar para o ponto de extremidade REST [URL]&quot; | Endpoint da API e credenciais |
| Armazenamento do Azure | &quot;Salvar arquivos no armazenamento do Azure&quot; | Configuração da conta de armazenamento |
| SharePoint | &quot;Armazenar no [site] do SharePoint&quot; | Acesso ao site do SharePoint |
| Power Automate | &quot;Acionar o fluxo do Power Automate&quot; | Configuração de fluxo |
| Marketo | &quot;Adicionar clientes em potencial ao Marketo&quot; | Credenciais da API do Marketo |

### Dicas

1. **Usar linguagem natural**: a IA entende solicitações complexas e pode interpretar requisitos detalhados
2. **Seja específico**: descrições detalhadas produzem melhores resultados e uma geração de formulários mais precisa
3. **Iterar**: refinar formulários por meio de conversa para obter a experiência do usuário perfeita
4. **Aproveitar contexto**: faça referência a elementos de formulário existentes para criar com base no que você já tem
5. **Teste completamente**: valide todos os cenários de usuário para garantir que os formulários funcionem conforme o esperado

## Ajuda e aprendizado do produto

O Forms Experience Builder também pode ensiná-lo sobre os recursos do AEM Forms:

### Faça Perguntas Como:

* &quot;Como criar um formulário de várias etapas?&quot;
* &quot;Qual é a diferença entre painéis e seções?&quot;
* &quot;Como configurar notificações por email?&quot;
* &quot;Quais são as práticas recomendadas para formulários móveis?&quot;
* &quot;Como aplicar temas às minhas formas?&quot;

### Obter Ajuda Sobre:

* Conceitos e terminologia do AEM Forms
* Instruções passo a passo para recursos complexos
* Práticas recomendadas
* Solução de problemas comuns

## Práticas recomendadas

### Design do formulário

* **Mantenha a simplicidade**: comece com campos essenciais e adicione complexidade somente quando necessário para evitar sobrecarga de usuários
* **Usar rótulos claros**: torne as finalidades de campo óbvias com rótulos descritivos que orientam os usuários pelo formulário
* **Fornecer texto de ajuda**: orientar os usuários sobre campos complexos com ajuda contextual e exemplos
* **Teste completamente**: valide todos os caminhos de usuário para garantir que os formulários funcionem corretamente em todos os cenários

### Experiência do usuário

* **Divulgação progressiva**: mostra campos relevantes com base no contexto para reduzir a carga cognitiva e melhorar as taxas de conclusão
* **Limpar navegação**: ajude os usuários a entenderem onde eles estão no formulário e quais etapas permanecem
* **Design responsivo**: garanta que os formulários funcionem em todos os dispositivos e tamanhos de tela para acessibilidade máxima
* **Acessibilidade**: siga as diretrizes da WCAG para tornar os formulários utilizáveis por pessoas com deficiência

### Desempenho

* **Otimizar contagem de campos**: solicite apenas as informações necessárias para reduzir o abandono de formulário e melhorar as taxas de conclusão
* **Usar validação apropriada**: evite erros antes do envio para fornecer feedback e orientação imediatos
* **Taxas de conclusão de teste**: monitorar e melhorar a eficácia do formulário por meio de análises e comentários de usuários
* **Atualizações regulares**: mantenha os formulários atualizados com as necessidades dos negócios e as expectativas dos usuários para um desempenho ideal

### Consistência da marca

* **Criar modelos de marca**: prepare modelos de formulários com marcas com as cores, fontes e estilos de sua organização antes de iniciar a criação do formulário
* **Definir padrões de estilo**: estabelecer estilos de botão, layouts de campo e diretrizes de espaçamento consistentes que possam ser referenciados em prompts
* **Usar ativos da marca**: prepare logotipos, códigos de cores e diretrizes de marca para facilitar a referência ao criar formulários
* **Biblioteca de modelos**: crie uma coleção de modelos de formulário com marca para casos de uso comuns (contato, registro, feedback)
* **Prompts de estilo**: inclua instruções específicas da marca: &quot;Use azul da empresa (#1234AB) para botões e fontes corporativas Helvetica&quot;

### Dicas para obter melhores resultados

**Comece Simples, Compilação**

* Comece com solicitações básicas: &quot;Criar um formulário de contato&quot;
* Adicione detalhes gradualmente: &quot;Adicionar validação ao campo de email&quot;
* Teste e refine: &quot;Torne o campo do telefone opcional&quot;

**Ser Específico Quando Necessário**

* Em vez de: &quot;Faça parecer bom&quot;
* Tente: &quot;Usar cores profissionais e tipografia limpa&quot;

**Usar Linguagem Natural**

* Em vez de: &quot;Adicionar componente de entrada de texto&quot;
* Tente: &quot;Adicionar um campo para o nome&quot;

**Referenciar Elementos Existentes**

* Use `@fieldName` para campos existentes: &quot;Tornar @email obrigatório&quot;
* Seja específico quanto aos nomes de campo: &quot;Atualize o campo @phoneNumber&quot;

**Analisar Solicitações Complexas**

* Em vez de uma solicitação grande, tente várias solicitações menores
* Crie o formulário passo a passo
* Teste cada alteração antes de passar para a seguinte

## Resolução de problemas

| Problema | Correção rápida |
|-------|-----------|
| **Interface não carregando** | Atualize o navegador, verifique a conexão com a Internet |
| **Comandos não funcionando** | Experimente `/help` ou use uma linguagem natural |
| **@fieldName não reconhecido** | Verifique a ortografia, certifique-se de que o campo existe primeiro |
| **Falha ao carregar o arquivo** | Usar PDF/JPG/PNG com menos de 10 MB |
| **Aparência incorreta do formulário** | Seja mais específico: &quot;Torná-lo compatível com dispositivos móveis&quot; |
| **Falha na integração** | Verificar credenciais e permissões de API |

**Ainda precisa de ajuda?** Digite `/help` seguido da pergunta específica ou contate o administrador do sistema.

Para obter suporte adicional, consulte a [Biblioteca de Prompts do Forms Experience Builder](ai-assistant-prompt-library.md) principal ou entre em contato com o administrador do sistema para obter assistência técnica.
