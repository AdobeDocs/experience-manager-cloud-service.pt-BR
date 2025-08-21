---
title: Forms Experience Builder - Biblioteca de prompts
description: Coleção de padrões de prompt comprovados e exemplos para criar formulários com assistência de IA na interface do usuário do Forms Management, no Editor adaptável do Forms e no Editor universal.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: 750674bbd29ec1b29388579d77c7c15bd89335ab
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 0%

---


# Forms Experience Builder - Biblioteca de prompts

Coleção de padrões de prompt reutilizáveis e exemplos otimizados para o Forms Experience Builder. Esta biblioteca simplificada se concentra nos dois métodos principais de criação: Criar do zero e Importar e converter, com suporte aprimorado para campos inteligentes alimentados por LLM e consistência de marca.

>[!NOTE]
>
> O Forms Experience Builder está disponível no programa dos primeiros usuários. Envie um email de seu endereço comercial para `aem-forms-ea@adobe.com` para solicitar acesso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta biblioteca de prompts está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os prompts, exemplos e práticas recomendadas podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção antecipada.

## Usar Esta Biblioteca De Prompts

Essa biblioteca fornece padrões de prompt reutilizáveis para cenários comuns de criação de formulários. Para obter práticas recomendadas abrangentes, consulte o [Guia de Introdução do Forms Experience Builder](forms-ai-assistant-getting-started.md#best-practices).

### Dicas rápidas para esta biblioteca

- **Comece com exemplos** - Use os prompts fornecidos como modelos e adapte-se às suas necessidades
- **Dois métodos de criação** - Escolher as abordagens Criar do Zero ou Importar e Converter
- **Seja específico** - Adicione seus próprios detalhes a exemplos genéricos
- **Testar completamente** - Sempre validar os resultados em seu ambiente específico

### Modelos e estilos de marca

**Prepare os ativos da marca com antecedência para a criação consistente do formulário:**

- **Modelos de marca** - Crie modelos de formulário padronizados com as cores, fontes e padrões de layout de sua organização
- **Diretrizes de estilo** - Defina um estilo de campo consistente, designs de botão e padrões de espaçamento
- **Biblioteca de componentes** - Crie componentes de formulário reutilizáveis que correspondam à identidade da sua marca
- **Visual Assets** - Prepare logotipos, ícones e elementos de plano de fundo para a integração de formulários

**Exemplo de Prompt do Modelo de Marca:**

```
Create a brand template for financial services forms with:
- Corporate blue (#003366) and silver (#C0C0C0) color scheme
- Open Sans font family for all text
- 16px minimum font size for accessibility
- Consistent 24px spacing between sections
- Corporate logo in header with proper sizing
- Professional button styling with hover effects
```

>[!NOTE]
>
>**Componentes personalizados**: consulte sua equipe de desenvolvimento sobre o uso de componentes específicos da organização e a compatibilidade deles com o Forms Experience Builder antes de implementar elementos de marca personalizados.

>[!NOTE]
>
> Essa biblioteca de prompts foi atualizada para refletir os recursos simplificados do Forms Experience Builder. Alguns recursos avançados de integração e teste mostrados em exemplos podem exigir configuração adicional.



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

**Etapa 2 - Adicionar Campos Obrigatórios:**

```
Add fields for @firstName, @lastName, @email, @phoneNumber with appropriate validation
```

**Etapa 3 - Adicionar Lógica Comercial:**

```
Create a rule: if @age is under 18, show parent/guardian information section
```

**Etapa 4 - Aprimorar com Preferências:**

```
Add a preferences panel with @newsletterSubscription, @marketingConsent, @termsAccepted
```

**Etapa 5 - Adicionar Carregamento de Arquivo:**

```
Include a file upload field for @profilePicture with size limit of 5MB
```

## Criação e gerenciamento de formulários

**Quando usar:** Quando precisar criar novos formulários ou modificar formulários existentes.

**Como usar:** Escolha uma das duas abordagens: Criar do Zero ou Importar e Converter (consulte o [Guia de Introdução](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)).

**Exemplo de Prompt - Criação de Formulário Simples:**

```
Create a customer feedback form with:
- Product rating (1-5 stars)
- Comment field for detailed feedback
- Customer email (optional)
- Submit to email notification
```

**Exemplo de Prompt - Criação de Formulário Complexo:**

```
Create a comprehensive employee onboarding form with:

**Personal Information Section:**
- Full name (first, middle, last)
- Date of birth with age validation
- Contact information (email, phone, address)
- Emergency contact details

**Employment Details:**
- Position and department selection
- Start date with business day validation
- Salary information with confidentiality notice
- Reporting structure

**Document Upload:**
- Resume/CV upload (PDF, DOC, DOCX)
- ID verification documents
- Tax forms and banking information
- Signed employment agreement

**Preferences:**
- Benefits selection with cost calculator
- Work schedule preferences
- Training requirements
- Equipment needs

**Validation Rules:**
- Email format validation
- Phone number format validation
- Age must be 18 or older
- All required documents must be uploaded
- Terms and conditions must be accepted

**Submit Actions:**
- Send confirmation email to new employee
- Notify HR department
- Create employee record in HR system
- Schedule orientation meeting
```

**Prompts de Gerenciamento de Formulário:**

```
Import this PDF application form and convert it to an adaptive form with enhanced validation
```

```
Update the existing contact form to include social media handles and preferred contact method
```

```
Reorganize the registration form into a 3-step wizard: personal info, preferences, confirmation
```

## Gerenciamento e configuração de campo

**Quando usar:** Quando precisar adicionar, modificar ou configurar campos de formulário.

**Como usar:** seja específico quanto aos tipos de campo, regras de validação e requisitos de experiência do usuário.

**Exemplo de Prompt - Adição Básica de Campo:**

```
Add a text input field for "Company Name" with placeholder "Enter your company name"
```

**Exemplo de Prompt - Configuração Avançada de Campo:**

```
Add a comprehensive address section with:

**Street Address:**
- Address line 1 (required, max 100 characters)
- Address line 2 (optional, max 100 characters)
- City (required, dropdown with common cities)
- State/Province (required, dropdown)
- Postal code (required, format validation)
- Country (required, default to "United States")

**Validation Rules:**
- Postal code must match state selection
- Address line 1 cannot be empty
- City must be a valid city for selected state

**User Experience:**
- Auto-complete for address fields
- Clear labels and help text
- Mobile-friendly input fields
- Accessibility compliance
```

**Prompts de Configuração de Campo:**

```
Make @email field required with real-time validation and custom error message
```

```
Add a dropdown for @country with options for USA, Canada, UK, Germany, France, and "Other"
```

```
Configure @phoneNumber field with format (XXX) XXX-XXXX and validation
```

```
Add a file upload field for @resume with PDF and DOC restrictions, max 5MB
```

## Campos inteligentes aprimorados com LLM

**Quando usar:** quando precisar de campos com opções pré-preenchidas que usam a base de dados de conhecimento da IA.

**Como usar:** solicite campos que exigem conjuntos de dados abrangentes; a IA pode preencher opções automaticamente usando seu conhecimento integrado.

### Campos geográficos e de localização

**Aeroportos e Transporte:**

```
Add a dropdown for departure airports with all major international airports
Add arrival airport field with IATA codes and full names
Create a field for nearest airport to user location
Add a selection of train stations for European cities
```

**Regiões Administrativas:**

```
Add a complete list of US states with abbreviations
Create a country dropdown with ISO codes and full names
Add a field for major world cities with time zones
Include a dropdown of Canadian provinces and territories
Add a field for UK counties and postal areas
```

### Dados de negócios e da indústria

**Classificações de Empresa:**

```
Add a field for industry classification with NAICS codes
Create a dropdown of business entity types (LLC, Corporation, Partnership, etc.)
Add a field for company size categories (startup, SME, enterprise)
Include department selection for large organizations
Add a field for professional service types
```

**Classificações profissionais:**

```
Add a field for job titles with common industry roles
Create a dropdown of professional certifications by field
Include education levels with degree types
Add a field for years of experience ranges
Create a selection for programming languages and frameworks
```

### Normas e Normas

**Finanças e assuntos legais:**

```
Add a field for currency codes with symbols and exchange rates
Create a dropdown of tax ID types by country
Include a field for legal document types
Add payment method options with security features
Create a selection for banking institutions by country
```

**Padrões técnicos:**

```
Add a dropdown of file format types with extensions
Include network protocol options
Add a field for database types and versions
Create a selection for API authentication methods
```

### Assistência médica e médica

**Classificações Médicas:**

```
Add a field for medical specialties
Create a dropdown of common medications with generic names
Include a field for insurance provider types
Add a selection for medical emergency contact relationships
Create a field for dietary restrictions and allergies
```

### Inteligência de Tempo e Calendário

**Campos de Data e Hora:**

```
Add a field for business hours with time zone handling
Create a dropdown of public holidays by country
Include seasonal options with date ranges
Add a field for conference room booking with availability
Create a selection for recurring meeting patterns
```

### Categorias de produto e serviço

**Classificações de comércio eletrônico:**

```
Add a field for product categories with subcategories
Create a dropdown of shipping methods with delivery estimates
Include a field for return policy options
Add a selection for customer priority levels
Create a field for subscription billing cycles
```

**Exemplo de Solicitações de Campo Inteligente:**

```
"Add a departure airport field with all major airports worldwide including IATA codes and city names"
```

```
"Create a comprehensive industry field using standard NAICS classification with technology subcategories"
```

```
"Include a professional certification dropdown that adapts based on the selected job field"
```

```
"Add an international phone number field that formats based on the selected country"
```

```
"Create a university selection field with major institutions organized by country and ranking"
```

## Criação de regras e lógica de negócios

**Quando usar:** Quando precisar implementar lógica condicional, regras de validação ou processos comerciais.

**Como usar:** descreva claramente a lógica comercial, especificando condições e ações.

**Exemplo de Prompt - Lógica Condicional Simples:**

```
Create a rule that shows @spouseInformation panel only when @maritalStatus equals "Married"
```

**Exemplo de Prompt - Regras de Negócios Complexas:**

```
Implement comprehensive loan application validation:

**Income Validation:**
- If @annualIncome is less than 30000:
  - Show warning message: "Income may be insufficient for requested loan amount"
  - Require additional income documentation
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
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership"
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override
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

**Exemplo de Prompt - Envio Multicanal Padrão:**

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
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New"
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents
```

## Importar e converter Forms existente

**Quando usar:** Quando você tiver formulários, documentos ou designs existentes para transformar em formulários modernos do AEM.

**Como usar:** carregue seu arquivo de origem e descreva os requisitos de conversão (consulte o [Guia de Importação](forms-ai-assistant-getting-started.md#2-import-and-convert)).

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

Preserve all original field labels and help text, but improve the user experience with modern form interactions
```

**Criar Prompts de Importação:**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes
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
```

**Prompts Específicos para Dispositivos Móveis:**

```
Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users
```

```
Optimize form for **tablet users** with appropriate field sizes and navigation patterns
```

```
Add **swipe gestures** for multi-step form navigation on mobile devices
```

## Acessibilidade e conformidade

**Quando usar:** quando os formulários precisarem atender aos padrões de acessibilidade (WCAG) ou aos requisitos de conformidade.

**Como usar:** especifique o nível de conformidade necessário e os recursos de acessibilidade específicos necessários.

**Exemplo de Prompt - Acessibilidade Básica:**

```
Make @contactForm accessible with:

**Basic Accessibility:**
- Proper ARIA labels for all form fields
- Keyboard navigation support
- High contrast color scheme
- Screen reader compatibility
- Focus indicators for all interactive elements
```

**Exemplo de Prompt - Acessibilidade Avançada:**

```
Implement comprehensive accessibility for @applicationForm:

**WCAG 2.1 AA Compliance:**
- Semantic HTML structure with proper headings
- ARIA landmarks and roles for navigation
- Color contrast ratio of at least 4.5:1
- Keyboard-only navigation support
- Screen reader announcements for dynamic content

**Form-Specific Accessibility:**
- Error messages announced to screen readers
- Field validation with clear error descriptions
- Progress indicators for multi-step forms
- Skip navigation links for keyboard users
- Alternative text for all images and icons

**User Experience:**
- Clear focus indicators on all interactive elements
- Logical tab order through form fields
- Descriptive link text and button labels
- Help text available for complex fields
- Timeout warnings for session expiration
```

**Prompts Específicos de Acessibilidade:**

```
Add **screen reader support** to this form with proper ARIA labels and announcements
```

```
Implement **keyboard navigation** for all form interactions and navigation elements
```

```
Ensure **color contrast** meets WCAG AA standards for all text and interactive elements
```

## Otimização do desempenho

**Quando usar:** Quando os formulários precisarem ser carregados rapidamente e ter bom desempenho sob várias condições.

**Como usar:** especifique requisitos de desempenho e estratégias de otimização.

**Exemplo de Prompt - Desempenho Básico:**

```
Optimize @contactForm for performance:

**Loading Optimization:**
- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
```

**Exemplo de Prompt - Desempenho Avançado:**

```
Implement comprehensive performance optimization for @applicationForm:

**Loading Performance:**
- Progressive loading of form sections
- Optimize images with WebP format
- Minimize JavaScript bundle size
- Enable gzip compression for all assets

**Runtime Performance:**
- Debounce validation calls to reduce API requests
- Optimize conditional logic execution
- Cache frequently used data
- Implement virtual scrolling for long lists

**User Experience:**
- Show loading indicators for async operations
- Provide offline capability for form data
- Auto-save form progress every 30 seconds
- Optimize form submission with retry logic

**Monitoring:**
- Track form load times and user interactions
- Monitor validation performance
- Measure submission success rates
- Alert on performance degradation
```

**Prompts Específicos de Desempenho:**

```
Optimize form **loading speed** by implementing progressive loading and asset optimization
```

```
Add **auto-save functionality** to prevent data loss during form completion
```

```
Implement **offline support** so users can complete forms without internet connection
```

## Assurance de teste e qualidade

**Quando usar:** quando os formulários precisarem de testes abrangentes para garantir confiabilidade e satisfação do usuário.

**Como usar:** especifique cenários de teste, requisitos de validação e métricas de qualidade.

**Exemplo de Prompt - Teste Básico:**

```
Add comprehensive testing for @contactForm:

**Functional Testing:**
- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
```

**Exemplo de Prompt - Teste Avançado:**

```
Implement comprehensive testing strategy for @applicationForm:

**Functional Testing:**
- Unit tests for all validation rules
- Integration tests for submit actions
- End-to-end testing for complete user flows
- Cross-browser compatibility testing

**User Experience Testing:**
- Usability testing with target user groups
- Accessibility testing with screen readers
- Mobile device testing on various screen sizes
- Performance testing under load conditions

**Quality Assurance:**
- Automated testing for regression prevention
- Manual testing for edge cases and scenarios
- Security testing for data protection
- Compliance testing for regulatory requirements

**Monitoring:**
- Track form completion rates and abandonment
- Monitor error rates and user feedback
- Measure performance metrics and load times
- Analyze user behavior and interaction patterns
```

**Prompts Específicos de Teste:**

```
Add **automated testing** for all form validations and submit functionality
```

```
Implement **user acceptance testing** scenarios for complete form workflows
```

```
Set up **performance monitoring** to track form load times and user interactions
```

## Resolução de problemas

Soluções rápidas para problemas comuns do Forms Experience Builder:

| Problema | Correção rápida |
|-------|-----------|
| Formulário não enviado | Verificar regras de validação e configuração da ação de envio |
| Erros de validação não são exibidos | Verificar configurações de validação de campo e posicionamento de mensagem de erro |
| Problemas de layout móvel | Revisar configurações de design responsivo e dimensionamento de campo |
| Campos que não aparecem | Verificar lógica condicional e regras de visibilidade |
| Falhas na importação | Verificar a compatibilidade do formato de arquivo e os limites de tamanho |
| Erros de integração | Validar endpoints de API e credenciais de autenticação |
| Problemas de desempenho | Otimizar a contagem de campos e remover validações desnecessárias |
| Problemas de acessibilidade | Revisar rótulos de campo, atributos ARIA e ordem de tabulação |

**Prompt do Modo de Depuração:**

```
Enable debug mode to identify issues with form submission and field validation
```

**Prompt de Análise de Erro:**

```
Analyze form errors: check validation rules, API responses, and user input patterns
```

## Análises e Insights Avançados

**Quando usar:** quando você precisa entender o desempenho do formulário e o comportamento do usuário.

**Como usar:** especifique os requisitos de análise e os insights necessários.

**Exemplo de prompt - Análise Básica:**

```
Add analytics to @contactForm:

**Basic Metrics:**
- Form completion rates
- Field abandonment rates
- Submit success/failure rates
- User session duration
```

**Exemplo de Prompt - Análises Avançadas:**

```
Implement comprehensive analytics for @applicationForm:

**User Behavior Analytics:**
- Track field completion rates and abandonment
- Monitor user session duration and patterns
- Analyze form navigation and user flow
- Identify bottlenecks and friction points

**Performance Analytics:**
- Measure form load times and performance
- Track API response times and failures
- Monitor validation rule effectiveness
- Analyze submission success rates

**Business Intelligence:**
- Generate reports on form effectiveness
- Track conversion rates and ROI
- Monitor user satisfaction and feedback
- Identify opportunities for optimization

**Predictive Analytics:**
- Predict form completion likelihood
- Identify users likely to abandon
- Recommend form improvements
- Optimize user experience based on data
```

**Prompts específicos do Analytics:**

```
Add **conversion tracking** to measure form completion rates and user behavior
```

```
Implement **A/B testing** to compare different form designs and optimize performance
```

```
Create **analytics dashboard** to monitor form performance and user insights
```

## Segurança e proteção de dados

**Quando usar:** quando os formulários lidam com dados confidenciais e precisam de medidas de segurança.

**Como usar:** especifique requisitos de segurança e medidas de proteção de dados.

**Exemplo de Prompt - Segurança Básica:**

```
Add security measures to @contactForm:

**Basic Security:**
- HTTPS encryption for all data transmission
- Input validation and sanitization
- CSRF protection for form submissions
- Secure session management
```

**Exemplo de Prompt - Segurança Avançada:**

```
Implement comprehensive security for @applicationForm:

**Data Protection:**
- End-to-end encryption for sensitive data
- PII data masking and anonymization
- Secure file upload with virus scanning
- Data retention and deletion policies

**Access Control:**
- Role-based access control for form data
- Multi-factor authentication for admin access
- Audit logging for all data access
- Secure API authentication and authorization

**Compliance:**
- GDPR compliance for data handling
- HIPAA compliance for health information
- PCI DSS compliance for payment data
- SOC 2 compliance for data security

**Monitoring:**
- Real-time security monitoring and alerts
- Intrusion detection and prevention
- Data breach notification systems
- Regular security audits and assessments
```

**Avisos Específicos de Segurança:**

```
Implement **data encryption** for sensitive form submissions and user information
```

```
Add **access control** to restrict form data access based on user roles and permissions
```

```
Set up **security monitoring** to detect and prevent unauthorized access to form data
```

## Referência de comando

### Comandos Essenciais

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

### Referências de campo

Use a sintaxe `@fieldName` para fazer referência a campos existentes em seus prompts:

- `@email` - Campo de email de referência
- `@firstName` - Referenciar campo de nome
- `@maritalStatus` - Campo de estado civil de referência

### Tipos de componentes

**Componentes de Entrada:**

- `text`, `email`, `number`, `tel`, `date`, `checkbox`, `radio`, `dropdown`, `file`, `textarea`

**Componentes de Contêineres:**

- `fieldset`, `panel`, `repeatable`, `wizard`

### Propriedades do componente

**Propriedades Universais (Todos os Componentes):**

- **Tipo**: tipo de componente
- **Nome**: identificador de campo para envio de formulário
- **Rótulo**: exibir texto para o campo
- **Descrição**: texto de ajuda para o campo
- **Visível**: booleano para visibilidade inicial
- **Obrigatório**: booleano para campos obrigatórios

**Propriedades do Campo de Entrada:**

- **Valor**: valor padrão/inicial
- **Espaço reservado**: texto de dica para campos de entrada
- **Min**: valor mínimo (para números/datas)
- **Max**: valor máximo (para números/datas)

**Propriedades de Carregamento de Arquivo:**

- **Aceitar**: tipos de arquivos (.pdf, .doc, .docx, .jpg, .png etc.)
- **Vários**: Booleano para seleção de vários arquivos

**Propriedades do Controle de Seleção:**

- **Opções**: Opções para listas suspensas (lista separada por vírgulas)
- **Marcado**: seleção padrão para caixas de seleção/rádio

**Propriedades do Contêiner:**

- **Fieldset**: agrupando campos relacionados
- **Repetível**: booleano para seções que podem ser repetidas

**Propriedades Avançadas:**

- **Expressão Visível**: fórmula para visibilidade condicional (=formula)
- **Expressão de Valor**: fórmula para valores calculados (=formula)

### Comandos de integração

**Enviar Ações:**

- Notificações por email
- Envios de API REST
- Armazenamento na nuvem (Azure, SharePoint)
- Automação de fluxo de trabalho (Power Automate, Workfront Fusion)
- Plataformas de marketing (Marketo)
- Integrações do CRM

### Diretrizes de sintaxe do prompt

- **Referências de campo**: usar `@fieldName` para campos existentes
- **Comandos**: usar `/command` para ações específicas
- **Linguagem natural**: descrever requisitos de maneira clara e específica

### Lista de verificação de validação

Para obter práticas recomendadas e diretrizes de validação abrangentes, consulte o [Guia de Introdução do Forms Experience Builder](forms-ai-assistant-getting-started.md#best-practices).

*Esta biblioteca de prompts é atualizada continuamente com base no feedback do usuário e nos novos recursos do Forms Experience Builder. Para obter os recursos e exemplos mais recentes, verifique a [documentação do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=pt-BR).*
