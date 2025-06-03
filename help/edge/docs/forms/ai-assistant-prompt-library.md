---
title: Assistente do AEM Forms AI - Biblioteca de prompts
description: Coleção de padrões de prompt comprovados e exemplos para criar formulários com assistência de IA na interface do usuário do Forms Management, no Editor adaptável do Forms e no Editor universal.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: d3ade6ee9216b44b55d6808d8acffe83f1e263c9
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 0%

---



# Assistente do AEM Forms AI - Biblioteca de prompts

Coleção de padrões de prompt reutilizáveis e exemplos de cenários comuns de criação de formulários. Pense nisso como modelos que podem ser adaptados às suas necessidades específicas. Cada seção aborda um caso de uso específico com orientações sobre quando usá-lo e exemplos comprovados.

>[!NOTE]
>
> O Assistente de IA para o AEM Forms está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para mailto:aem-forms-ea@adobe.com para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem ser alterados à medida que o Assistente de IA do AEM Forms continua a evoluir durante o programa de adoção antecipada.

## Práticas recomendadas para resultados ideais

Para aproveitar ao máximo o Assistente de IA, lembre-se das seguintes dicas:

### Comece de forma simples e incremental

Comece com comandos menores e específicos (por exemplo, &quot;Adicionar uma entrada de texto para &#39;Nome&#39;&quot;) em vez de solicitações muito complexas de várias etapas inicialmente. Essa abordagem ajuda a garantir a precisão e facilita a solução de problemas se algo não funcionar conforme o esperado.

**Exemplo de Início Simples:**

```
Add a text input field for "First Name" with placeholder "Enter your first name"
```

**Em Seguida, Criar Incrementalmente:**

```
Make @firstName mandatory and add validation message "First name is mandatory"
```

### Usar a terminologia do AEM Forms

Empregue termos como &quot;painel&quot;, &quot;campo de entrada de texto&quot;, &quot;grupo de caixas de seleção&quot;, &quot;enviar ação&quot;, &quot;regra&quot; etc. para melhor compreensão pelo assistente. Isso garante que a IA interprete as solicitações corretamente no contexto do AEM Forms.

**Termos Preferenciais:**

- &quot;campo de entrada de texto&quot; em vez de &quot;caixa de texto&quot;
- &quot;grupo de caixas de seleção&quot; em vez de &quot;caixas de seleção&quot;
- &quot;lista suspensa&quot; em vez de &quot;lista de seleção&quot;
- &quot;painel&quot; em vez de &quot;seção&quot; ou &quot;container&quot;
- &quot;enviar ação&quot; em vez de &quot;envio de formulário&quot;
- &quot;rule&quot; em vez de &quot;logic&quot; ou &quot;condition&quot;

### Campos de referência claramente

Ao configurar campos existentes, use a notação @fieldName (por exemplo, &quot;Tornar @firstName obrigatório&quot;). Isso ajuda a IA a identificar exatamente a qual campo você está se referindo, especialmente em formulários complexos com muitos campos.

**Exemplos:**

- `Make @email mandatory with real-time validation`
- `Show @spouseInfo panel when @maritalStatus equals "Married"`
- `Set @country default value to "United States"`

### Revisar sempre os planos

Sempre revise cuidadosamente os planos para alterações propostas pelo assistente no Universal Editor antes de clicar em &quot;Aplicar&quot;. A IA mostrará o que ela planeja fazer: reserve um momento para verificar se isso corresponde às suas expectativas.

### Validar manualmente

Depois que o assistente fizer alterações, sempre visualize e teste o formulário para garantir que ele se comporte e tenha a aparência esperada. A IA é uma ferramenta poderosa, mas a validação final é fundamental para garantir a qualidade.

**Lista de Verificação de Validação:**

- Testar a funcionalidade do formulário no modo de visualização
- Verifique se a lógica condicional funciona corretamente
- Verifique a agilidade móvel
- Envio de formulário de teste
- Validar recursos de acessibilidade

### Iterar e refinar

Se o primeiro prompt não fornecer o resultado exato, tente reformular a frase ou dividir a solicitação em etapas menores. A IA aprende com o contexto, portanto, fornecer detalhes mais específicos geralmente melhora os resultados.

**Exemplo de Iteração:**

1. Primeira tentativa: &quot;Tornar o formulário compatível com dispositivos móveis&quot;
2. Refinado: &quot;Otimizar o layout de formulário para telas móveis em 768px com layout de coluna única e destinos de toque maiores&quot;

### Fornecer feedback

Use o mecanismo de feedback integrado para ajudar o assistente a aprender e melhorar o. Seus comentários ajudam a melhorar a IA para todos.


## Exemplos de desenvolvimento incremental

Esses exemplos mostram como criar formulários passo a passo, começando simples e adicionando complexidade gradualmente:

### Exemplo 1: Criando um Formulário de Contato Incrementalmente

**Etapa 1 - Início Simples:**

```
Create a basic contact form with name, email, and message fields
```

**Etapa 2 - Adicionar validação:**

```
Make @name and @email mandatory fields with appropriate validation
```

**Etapa 3 - Aprimorar a Experiência do Usuário:**

```
Add placeholder text: @name "Your full name", @email "your.email@company.com", @message "Tell us how we can help"
```

**Etapa 4 - Adicionar Recursos Avançados:**

```
Add a dropdown @inquiryType with options: "General Question", "Support Request", "Sales Inquiry", "Partnership"
```

**Etapa 5 - Implementar Lógica Condicional:**

```
Show @urgencyLevel dropdown (Low, Medium, High) only when @inquiryType equals "Support Request"
```

### Exemplo 2: Criação incremental de um formulário de registro

**Etapa 1 - Estrutura Básica:**

```
Create a user registration form with personal information panel
```

**Etapa 2 - Adicionar Campos Principais:**

```
Add text input fields: @firstName, @lastName, @email, @phone to the personal information panel
```

**Etapa 3 - Adicionar validação:**

```
Make @firstName, @lastName, and @email mandatory with real-time validation
```

**Etapa 4 - Adicionar Informações da Conta:**

```
Create a new panel "Account Information" with @username and @password fields
```

**Etapa 5 - Aprimorar Segurança:**

```
Add password confirmation field @confirmPassword with validation to match @password
```

**Etapa 6 - Adicionar Preferências:**

```
Create "Preferences" panel with @newsletter checkbox and @communicationMethod radio group (Email, SMS, Phone)
```

Essa abordagem incremental ajuda a:

- Problemas de captura antes da composição
- Teste cada recurso completamente
- Fazer ajustes com base no feedback dos usuários
- Manter melhor controle sobre o processo de desenvolvimento

## Início do novo Forms

**Quando usar:** No início de qualquer projeto de formulário. Esse prompt ajuda a IA a entender seus requisitos e criar a estrutura de base.

**Como usar:** comece com a estrutura básica e os requisitos principais. Especifique o tipo de formulário, o público-alvo e a finalidade principal. Adicione complexidade em prompts subsequentes.

**Exemplo de Prompt - Iniciando Simples:**

```
Create a **customer onboarding form** for new bank account applications with:

**Purpose:** Collect personal information for account setup
**Target Users:** New customers applying for checking/savings accounts
**Basic Structure:** Single panel with essential fields
**Core Fields:** Name, email, phone, account type selection

Start with a simple layout that we can enhance step by step.
```

**Em Seguida, Criar Incrementalmente:**

```
Add an address panel to @customerOnboardingForm with street address, city, state, and zip code fields
```

```
Add employment information panel with @employer, @jobTitle, and @annualIncome fields
```

```
Add file upload field @identityDocuments for identity verification (Accept: .pdf,.jpg,.png)
```

**Prompts de Início Simples Alternativos:**

```
Create a basic **event registration form** with name, email, and event selection fields
```

```
Build a simple **contact form** with name, email, and message fields
```

```
Design a basic **feedback survey** with rating scale and comments field
```

## Estrutura e layout do formulário

**Quando usar:** quando precisar organizar formulários complexos ou melhorar a experiência do usuário através de um melhor design de layout.

**Como usar:** Concentre-se na jornada do usuário e no agrupamento lógico de informações. Especifique preferências de layout e padrões de navegação.

**Exemplo de Prompt - Estrutura de Formulário de Várias Etapas:**

```
Convert this single-page form into a **3-step wizard** with:

**Step 1: Personal Information**
- Name, email, phone, address fields
- Progress indicator showing "Step 1 of 3"
- "Next" button (validate mandatory fields before proceeding)

**Step 2: Preferences & Requirements** 
- Service selection (checkbox group)
- Budget range (dropdown)
- Timeline preferences (radio group)
- Special requirements (text input field)

**Step 3: Review & Submit**
- Summary of all entered information
- Edit links to go back to specific steps
- Terms and conditions checkbox
- Submit button with confirmation

Include "Previous" and "Next" buttons, allow users to jump between completed steps, save progress automatically.
```

**Prompts de Otimização de Layout:**

```
Reorganize this form using a **wizard layout** for desktop and single column for mobile. 
```

```
Convert this long form into an **accordion layout** where users can expand/collapse sections.
```

```
Create a **vertical tabbed interface** for this form with tabs for: Basic Info, Contact Details, Preferences, and Review.
```

## Gerenciamento e validação de campo

**Quando usar:** quando precisar adicionar, modificar ou aprimorar campos de formulário com regras de validação e comportamentos específicos.

**Como usar:** seja específico quanto aos tipos de campo, aos requisitos de validação e às expectativas da experiência do usuário. Faça referência a campos existentes usando a sintaxe @fieldName.

**Exemplo de Prompt - Aprimoramento de Campo:**

```
Enhance the form fields with these specific requirements:

**Email Field (@email):**
- Make mandatory with real-time validation
- Show green checkmark when valid format entered
- Display helpful error message: "Please enter a valid email address"
- Add placeholder: "your.email@company.com"

**Phone Number (@phone):**
- Type: tel for mobile optimization
- Make mandatory for business customers, optional for personal
- Add placeholder: "Enter your phone number"

**Date of Birth (@dateOfBirth):**
- Type: date with date picker
- Validate age is 18+ for account opening
- Show error if under 18: "Must be 18 or older to open account"

**File Upload (@documents):**
- Accept: .pdf,.doc,.docx
- Multiple: true for multiple document upload
- Show upload progress and file names after upload
```

**Prompts Específicos de Campo:**

```
Add a **file upload field** for resume with these specs: Accept only PDF/DOC/DOCX files, allow multiple files, show upload progress, display file names after upload.
```

```
Create a **dropdown field** for country selection with all countries listed. Set default value based on user's location if available.
```

```
Build a **repeatable panel** for work experience where users can add/remove multiple jobs. Each entry needs: company, title, start date, end date, description.
```

## Lógica e regras condicionais

**Quando usar:** Quando você precisar de um comportamento de formulário dinâmico com base na entrada do usuário ou nas regras de negócios.

**Como usar:** defina claramente as condições e as ações resultantes. Use referências de campo específicas e operadores lógicos.

**Exemplo de Prompt - Lógica Condicional Complexa:**

```
Implement these conditional rules for the application form:

**Business vs Personal Account Logic:**
- If @accountType equals "Business", show:
  - Business name field (mandatory)
  - Tax ID field (mandatory)
  - Business address section
  - Number of employees dropdown
- If @accountType equals "Personal", hide all business fields

**Income-Based Requirements:**
- If @annualIncome is less than 25000:
  - Show additional verification section
  - Make co-signer information mandatory
  - Display message: "Additional documentation may be required"
- If @annualIncome is greater than 100000:
  - Show premium services options
  - Enable priority processing checkbox

**Age-Based Validation:**
- If @age is under 18:
  - Show parent/guardian information section
  - Make parent signature upload mandatory
  - Change submit button text to "Submit for Review"
- If @age is 65 or older:
  - Show senior discount options
  - Add accessibility preferences section
```

**Prompts Específicos de Regra:**

```
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership".
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups.
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override.
```

## Integração e envio de dados

**Quando usar:** Quando precisar conectar formulários a sistemas de back-end, bancos de dados ou serviços externos.

**Como usar:** comece com a configuração básica de envio e acrescente integrações adicionais de forma incremental. Especifique o tipo de integração, os requisitos de formato de dados e as preferências de tratamento de erros.

**Exemplo de Prompt - Iniciar com Envio Básico:**

```
Configure basic form submission for @applicationForm:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Format data as JSON
- Show success message: "Application submitted successfully"
- Show error message if submission fails: "Submission failed, please try again"
```

**Em Seguida, Adicionar Ações Secundárias Incrementalmente:**

```
Add email notification to @applicationForm: Send confirmation email to @email address with application reference number
```

```
Add CRM integration to @applicationForm: Create new lead record with @firstName, @lastName, @email, and set Status to "New Application"
```

**Exemplo de Prompt - Envio Multicanal Avançado:**

```
Configure form submission with multiple data destinations:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Include authentication header with API key
- Format data as JSON with nested objects for address and employment
- Handle success response (201) by showing thank you message

**Secondary Actions:**
- Send notification email to applicant at @email address
- Copy application data to tracking system
- Trigger workflow for approval process
- Create record in CRM with lead status "New Application"

**Error Handling:**
- If primary submission fails, save data locally and retry
- Show user-friendly error message: "Submission temporarily unavailable"
- Provide option to download form data as backup
- Send alert email to admin team about failed submission

**Success Flow:**
- Redirect to confirmation page with application reference number
- Send confirmation email with next steps
- Display estimated processing timeline
```

**Prompts Específicos de Integração:**

```
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New".
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification.
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents.
```

## Design - Importação e Conversão

**Quando usar:** Quando você tiver designs de formulário existentes (PDF, Figma, imagens) que precisam ser convertidos para formulários funcionais do AEM.

**Como usar:** forneça um contexto claro sobre o design de origem e especifique quaisquer modificações ou aprimoramentos necessários.

**Exemplo de Prompt - Conversão de Formulário do PDF:**

```
Convert this uploaded **PDF application form** into a functional AEM adaptive form:

**Source Analysis:**
- Analyze the PDF layout and identify all form fields
- Preserve the visual hierarchy and grouping
- Maintain the professional appearance and branding

**Field Mapping:**
- Convert PDF text fields to adaptive form text inputs
- Transform checkboxes to checkbox components
- Convert dropdown lists to AEM dropdown components
- Map signature areas to digital signature fields

**Enhancements:**
- Add real-time validation that wasn't possible in PDF
- Implement conditional logic for dependent fields
- Make the form responsive for mobile devices
- Add progress saving capability
- Include accessibility improvements (ARIA labels, keyboard navigation)

**Styling:**
- Match the original color scheme and fonts
- Maintain professional business appearance
- Ensure consistent spacing and alignment
- Add subtle animations for better user experience

Preserve all original field labels and help text, but improve the user experience with modern form interactions.
```

**Criar Prompts de Importação:**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness.
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields.
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes.
```

## Otimização e capacidade de resposta para portáteis

**Quando usar:** quando os formulários precisarem funcionar perfeitamente em todos os tipos de dispositivos e tamanhos de tela.

**Como usar:** comece com a otimização móvel básica e, em seguida, aprimore com recursos avançados. Enfatize a abordagem móvel e especifique os comportamentos do ponto de interrupção de forma incremental.

**Exemplo de Prompt - Iniciar com Otimização Móvel Básica:**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**Em Seguida, Adicione Recursos Avançados Para Dispositivos Móveis:**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**Exemplo de Prompt - Otimização Abrangente do Mobile First:**

```
Optimize this form for **mobile-first responsive design**:

**Mobile Layout (320px - 768px):**
- Single column layout for all form sections
- Larger touch targets (minimum 44px height)
- Simplified navigation with collapsible sections
- Sticky submit button at bottom of screen
- Auto-zoom disabled on input focus

**Tablet Layout (768px - 1024px):**
- Two-column layout for shorter fields (name, email)
- Single column for complex fields (address, comments)
- Side navigation for multi-step forms
- Optimized for both portrait and landscape

**Desktop Layout (1024px+):**
- Multi-column layouts where appropriate
- Horizontal form sections for related fields
- Sidebar navigation for long forms
- Hover states and advanced interactions

**Touch Optimization:**
- Larger checkbox and radio button targets
- Swipe gestures for multi-step navigation
- Pull-to-refresh for saved drafts
- Touch-friendly date/time pickers

**Performance:**
- Lazy load non-critical form sections
- Optimize images and icons for mobile
- Minimize JavaScript for faster loading
- Progressive enhancement approach
```

**Avisos Simples Específicos para Dispositivos Móveis:**

```
Make @checkoutForm mobile-optimized with large buttons and one-thumb navigation
```

```
Add touch-friendly controls to @surveyForm for tablet users
```

```
Enable offline functionality for @applicationForm with local data saving
```

## Acessibilidade e conformidade

**Quando usar:** Quando os formulários devem atender aos padrões de acessibilidade (WCAG 2.1 AA) ou aos requisitos de conformidade.

**Como usar:** especifique os requisitos de acessibilidade e os padrões de conformidade que devem ser atendidos.

**Exemplo de Prompt - Implementação de Acessibilidade:**

```
Make this form **WCAG 2.1 AA compliant** with these accessibility features:

**Keyboard Navigation:**
- Logical tab order through all form elements
- Skip links to main content and form sections
- Keyboard shortcuts for common actions
- Focus indicators clearly visible on all interactive elements

**Screen Reader Support:**
- Proper ARIA labels for all form fields
- Descriptive error messages announced to screen readers
- Form section headings with proper hierarchy (h1, h2, h3)
- Progress announcements for multi-step forms

**Visual Accessibility:**
- Color contrast ratio minimum 4.5:1 for text
- Don't rely solely on color to convey information
- Text size minimum 16px for body text
- Scalable up to 200% without horizontal scrolling

**Motor Accessibility:**
- Large click targets (minimum 44x44px)
- Generous spacing between interactive elements
- No time limits or provide extension options
- Alternative input methods support

**Cognitive Accessibility:**
- Clear, simple language in all instructions
- Consistent navigation and layout patterns
- Error prevention and clear error recovery
- Help text and examples for complex fields

**Testing Requirements:**
- Test with screen readers (NVDA, JAWS, VoiceOver)
- Verify keyboard-only navigation
- Check color contrast with automated tools
- Validate HTML for semantic correctness
```

**Prompts Específicos de Conformidade:**

```
Ensure this **healthcare form meets HIPAA requirements** with proper data encryption, audit logging, and privacy controls.
```

```
Make this **financial form PCI DSS compliant** with secure payment field handling and data protection measures.
```

```
Create a **government form meeting Section 508 standards** with full accessibility and plain language requirements.
```

## Assurance de teste e qualidade

**Quando usar:** quando precisar validar a funcionalidade do formulário, a experiência do usuário e o desempenho técnico.

**Como usar:** especifique cenários de teste, casos de borda e critérios de qualidade que devem ser verificados.

**Exemplo de Prompt - Teste de Formulário Abrangente:**

```
Create a **comprehensive testing plan** for this application form:

**Functional Testing:**
- Test all field validations with valid and invalid data
- Verify conditional logic shows/hides fields correctly
- Test file upload with various file types and sizes
- Validate calculation fields update correctly
- Test form submission with complete and incomplete data

**User Experience Testing:**
- Test form completion time (target: under 10 minutes)
- Verify error messages are helpful and actionable
- Test progress saving and restoration
- Validate mobile touch interactions
- Check form accessibility with assistive technologies

**Edge Case Testing:**
- Test with extremely long text inputs
- Verify behavior with special characters and emojis
- Test with slow internet connections
- Validate offline functionality if applicable
- Test browser back/forward button behavior

**Performance Testing:**
- Measure form load time (target: under 3 seconds)
- Test with large file uploads
- Verify memory usage with long form sessions
- Test concurrent user submissions
- Validate database performance under load

**Security Testing:**
- Test input sanitization and XSS prevention
- Verify CSRF protection is working
- Test file upload security restrictions
- Validate data encryption in transit and at rest
- Check authentication and authorization controls

**Cross-Browser Testing:**
- Test on Chrome, Firefox, Safari, Edge
- Verify mobile browsers (iOS Safari, Chrome Mobile)
- Test on different operating systems
- Validate older browser fallbacks
- Check print functionality across browsers
```

**Prompts Específicos de Teste:**

```
Create **automated test scripts** for this form's critical user paths: successful submission, validation errors, and conditional logic.
```

```
Design a **user acceptance testing plan** with realistic scenarios and success criteria for business stakeholders.
```

```
Set up **performance monitoring** to track form completion rates, abandonment points, and submission success rates.
```

## Recursos avançados e integrações

**Quando usar:** quando precisar de recursos de formulário sofisticados, como assistência de IA, fluxos de trabalho avançados ou integrações complexas.

**Como usar:** defina claramente os requisitos avançados de funcionalidade e integração.

**Exemplo de prompt - Formulário com IA aprimorada:**

```
Add **AI-powered features** to enhance this application form:

**Smart Auto-Complete:**
- Use AI to suggest company names as user types
- Auto-populate address fields from partial input
- Suggest job titles based on industry selection
- Provide intelligent form completion suggestions

**Dynamic Question Generation:**
- Generate follow-up questions based on previous answers
- Adapt form complexity to user's experience level
- Show relevant optional fields based on user profile
- Personalize form sections for different user types

**Intelligent Validation:**
- Use AI to detect potentially incorrect information
- Suggest corrections for common data entry errors
- Validate business information against public databases
- Flag suspicious or inconsistent responses

**Content Optimization:**
- A/B test different form layouts automatically
- Optimize field order based on completion patterns
- Adjust form length based on user engagement
- Personalize help text based on user behavior

**Predictive Analytics:**
- Predict likelihood of form completion
- Identify users who might need assistance
- Suggest optimal times for form completion reminders
- Analyze drop-off points and suggest improvements

**Natural Language Processing:**
- Allow voice input for text fields
- Convert speech to text for accessibility
- Analyze open-text responses for sentiment
- Extract structured data from unstructured input
```

**Prompts de Integração Avançada:**

```
Integrate with **CRM system** to pre-populate known customer data, update records in real-time, and trigger automated follow-up sequences.
```

```
Connect to **payment gateway** for secure transaction processing with PCI compliance, fraud detection, and multiple payment methods.
```

```
Implement **blockchain verification** for document authenticity, immutable audit trails, and decentralized identity verification.
```

## Solução de problemas e otimização

**Quando usar:** quando os formulários tiverem problemas de desempenho, problemas de experiência do usuário ou dificuldades técnicas.

**Como usar:** descreva claramente o problema específico e o resultado desejado.

**Exemplo de Prompt - Otimização de Desempenho:**

```
Optimize this form for **better performance and user experience**:

**Current Issues:**
- Form takes 8+ seconds to load on mobile
- Users are abandoning at the address section (60% drop-off)
- File uploads frequently fail or timeout
- Validation errors are confusing users

**Performance Improvements:**
- Implement lazy loading for non-critical form sections
- Optimize images and reduce bundle size
- Add progressive loading indicators
- Cache frequently used data (country lists, etc.)
- Minimize JavaScript execution time

**User Experience Fixes:**
- Simplify the address section with auto-complete
- Add inline validation with helpful error messages
- Implement smart defaults based on user location
- Add progress saving every 30 seconds
- Provide clear instructions for each section

**Technical Optimizations:**
- Implement chunked file uploads with resume capability
- Add client-side validation before server submission
- Optimize database queries for faster responses
- Implement proper error handling and retry logic
- Add comprehensive logging for debugging

**Monitoring & Analytics:**
- Set up form analytics to track user behavior
- Monitor completion rates by section
- Track error rates and types
- Measure performance metrics continuously
- A/B test improvements with real users
```

**Avisos de Solução de Problemas:**

```
**Debug this form submission error:** Users report getting "500 Internal Server Error" when submitting. Check validation logic, server endpoints, and data formatting.
```

```
**Fix mobile layout issues:** Form fields are overlapping on iPhone screens and submit button is not visible. Ensure proper responsive design.
```

```
**Resolve validation conflicts:** Some users can't submit even with valid data. Review validation rules for conflicts and edge cases.
```

## Práticas recomendadas específicas do ambiente

### Interface de gerenciamento do Forms

**Quando usar:** para tarefas de criação e gerenciamento de formulários de alto nível.

```
In Forms Management UI, create a new **customer survey template** that can be reused across different departments. Include standard branding, common field types, and configurable sections.
```

### Editor Forms adaptável

**Quando usar:** Para obter a configuração detalhada do formulário e a criação de regras complexas.

```
In the Adaptive Forms Editor, configure **advanced business rules** for this loan application: calculate debt-to-income ratio, determine eligibility, and show appropriate next steps.
```

### Editor universal

**Quando usar:** Para formulários do Edge Delivery Services com edição visual.

```
In Universal Editor, create a **responsive contact form** for the company website. Ensure it matches the site design and integrates with the existing content management workflow.
```

## Guia rápido de referência de comandos

| Comando | Melhor caso de uso | Exemplo |
|---------|---------------|---------|
| `/create-form` | Início de novos formulários | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | Adição de formulários a páginas | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | Alteração da estrutura do formulário | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | Modificação de propriedades de campo | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | Adição de comportamento dinâmico | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | Organizar seções de formulário | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | Conversão de designs | `/add-panel from uploaded form image with field recognition` |
| `/configure-submit` | Configuração do manuseio de dados | `/configure-submit to CRM and send confirmation email` |
| `/help` | Obtendo assistência | `/help how to implement multi-step validation?` |

## Referência das propriedades do componente suportado

### Propriedades Universais (Todos os Componentes)

- **Tipo**: tipo de componente (texto, email, número, tel, data, caixa de seleção, rádio, lista suspensa, arquivo, etc.)
- **Nome**: identificador de campo para envio de formulário
- **Rótulo**: exibir texto para o campo
- **Descrição**: texto de ajuda para o campo
- **Visível**: booleano para visibilidade inicial
- **Obrigatório**: booleano para campos obrigatórios

### Propriedades do campo de entrada

- **Valor**: valor padrão/inicial
- **Espaço reservado**: texto de dica para campos de entrada
- **Min**: valor mínimo (para números/datas)
- **Max**: valor máximo (para números/datas)

### Propriedades de upload de arquivo

- **Aceitar**: tipos de arquivos (.pdf, .doc, .docx, .jpg, .png etc.)
- **Vários**: Booleano para seleção de vários arquivos

### Propriedades do controle de seleção

- **Opções**: Opções para listas suspensas (lista separada por vírgulas)
- **Marcado**: seleção padrão para caixas de seleção/rádio

### Propriedades do contêiner

- **Fieldset**: agrupando campos relacionados
- **Repetível**: booleano para seções que podem ser repetidas

### Propriedades avançadas

- **Expressão Visível**: fórmula para visibilidade condicional (=formula)
- **Expressão de Valor**: fórmula para valores calculados (=formula)

## Resumo de práticas recomendadas

### Diretrizes técnicas

- **Usar somente propriedades com suporte** da especificação oficial de componente do AEM Forms
- **Siga a sintaxe adequada** para referências de campo (@fieldName) e expressões (=formula)
- **Testar incrementalmente** após cada alteração para capturar problemas antecipadamente
- **Planeje a acessibilidade** desde o início, não como uma reflexão posterior
- **Considere usuários móveis** em cada decisão de design
- **Regras complexas de documentos** para manutenção futura e colaboração em equipe

### Abordagem estratégica

- **Comece com as necessidades do usuário** - Concentre-se no que os usuários precisam realizar, não apenas em recursos técnicos
- **Design para conclusão** - Minimize o atrito e a carga cognitiva no design do formulário
- **Planejar fluxo de dados** antecipadamente - Considere como os dados serão processados, armazenados e usados
- **Compilação para escala** - Formulários de design que podem lidar com o volume de usuários esperado e o crescimento de dados
- **Implemente o aprimoramento progressivo** - Verifique se a funcionalidade básica funciona e adicione recursos avançados

### Armadilhas comuns a serem evitadas

- **Solicitações iniciais muito complexas** - Divida tarefas grandes em etapas menores e gerenciáveis
- **O uso de propriedades sem suporte** não está na especificação do AEM Forms
- **Ignorando experiência móvel** até tarde no processo de desenvolvimento
- **Ignorando teste de usuário** com cenários reais e casos de borda
- **Presumindo que a IA entenda o contexto** sem fornecer instruções claras e específicas
- **Ignorando acessibilidade** e requisitos de conformidade
- **Não validando as alterações** antes de passar para a próxima etapa

### Abordagem do Quality Assurance

1. **Visualizar com frequência** - Verifique seu trabalho no modo de visualização após cada alteração significativa
2. **Casos de borda de teste** - Tente entradas incomuns, texto longo, caracteres especiais
3. **Validar entre dispositivos** - Testar em dispositivos móveis, tablets e áreas de trabalho
4. **Verificar acessibilidade** - Verificar a navegação pelo teclado e a compatibilidade com o leitor de tela
5. **Teste de desempenho** - Garantir que os formulários sejam carregados rapidamente e respondam sem problemas
6. **Teste de aceitação do usuário** - Faça com que usuários reais testem o formulário antes da implantação


*Esta biblioteca de prompts é atualizada continuamente com base no feedback dos usuários e nos novos recursos do Assistente de IA. Para obter os recursos e exemplos mais recentes, verifique a [documentação do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=pt-BR).*
