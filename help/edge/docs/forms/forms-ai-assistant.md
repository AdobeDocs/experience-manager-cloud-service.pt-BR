---
title: Assistente de IA para o AEM Forms (Forms Experience Builder)
description: Crie formulários avançados mais rapidamente usando os Fragmentos de formulário
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 0%

---


# Introdução ao Assistente de IA para AEM Forms (Forms Experience Builder)

>[!NOTE]
>
>
> O recurso Assistente de IA para o AEM Forms (Forms Experience Builder) está disponível no **programa de usuários iniciais**. Se estiver interessado, envie um email rápido do seu endereço comercial para mailto:aem-forms-ea@adobe.com para solicitar acesso ao recurso.

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta documentação está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os recursos, comandos e exemplos podem mudar à medida que o Assistente de IA do AEM Forms continua a evoluir durante o programa que adotou precocemente.

O Assistente de IA para o AEM Forms transforma a maneira como você cria formulários — descreva o que você precisa em linguagem natural e veja seus formulários ganharem vida. Disponível na interface do Forms Management, no Editor Forms adaptável e no Editor universal, ele entende sua intenção e cria exatamente o que você está procurando.

## Introdução: Fale com ele

O Assistente de IA funciona como uma conversa com um colega especialista. Em vez de aprender menus e configurações complexas, você simplesmente descreve o que deseja criar.

### Início rápido

Comece a trabalhar rapidamente assistindo ao nosso vídeo introdutório:

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### Acessar o assistente de IA

Você pode acessar o Assistente de IA em três locais diferentes no AEM Forms:

1. **Interface de Gerenciamento do Forms**
   - Navegue até: Adobe Experience Manager > Forms > Forms e documentos
   - Procure o ícone do Assistente do AI no lado esquerdo da interface
   - Clique no ícone para abrir o painel Assistente de IA

   ![Ícone do Assistente de IA*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **Editor Forms adaptável**
   - Navegue até: Adobe Experience Manager > Forms > Forms e documentos
   - Selecionar e abrir um formulário para edição
   - Clique no ícone do Assistente de IA na interface do editor

   ![Ícone do Assistente de IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **Universal Editor**

   - Navegue até: Adobe Experience Manager > Forms > Forms e documentos
   - Procure o ícone do Assistente do AI no lado esquerdo da interface
   - Clique no ícone do Assistente de IA na interface do editor

### Como começar: conversas simples

A melhor maneira de começar com o Assistente de IA é por meio da linguagem natural. Veja como:

**Descreva apenas o que você precisa:**

- &quot;Criar um formulário de contato para meu site&quot;
- &quot;Preciso de um formulário de feedback do cliente com escalas de classificação&quot;
- &quot;Criar um formulário de inscrição para o meu evento futuro&quot;
- &quot;Faça uma pesquisa simples sobre a satisfação do produto&quot;

**Adicionar detalhes à medida que você vai:**

- &quot;Criar um formulário de contato com campos de nome, email, telefone e mensagem&quot;
- &quot;Preciso de um formulário de inscrição em várias etapas para uma conferência&quot;
- &quot;Crie um formulário de feedback do cliente com classificações de 5 estrelas e seções de comentários&quot;

**Referencie seus campos existentes:**

- &quot;Tornar o campo de email obrigatório&quot; (para @email)
- &quot;Adicionar validação ao campo de número de telefone&quot; (para @phoneNumber)
- &quot;Mostrar as informações do cônjuge somente se casado estiver selecionado&quot; (para @spouseInfo e @maritalStatus)

### O que você também pode fazer

Além da linguagem natural, o Assistente de IA oferece maneiras adicionais de interagir:

- **Carregar arquivos**: anexe imagens, PDFs ou designs do Figma para mostrar à IA o que você está prevendo
- **Usar comandos rápidos**: Digite `/` para ver os atalhos disponíveis para ações comuns
- **Referenciar campos específicos**: Use `@fieldName` para modificar campos de formulário existentes (por exemplo, `@firstName`, `@emailAddress`)

## O Que Você Pode Criar: Exemplos Que Funcionam

Estes são exemplos reais do que você pode fazer com uma linguagem simples e natural:

### Iniciar um novo formulário

**Abordagem simples:**

```
"Create a contact form"
```

**Abordagem mais detalhada:**

```
"Create a professional contact form for a law firm with fields for name, email, phone, case type, and message. Make it mobile-friendly."
```

**Com referência de design:**

```
"Create a contact form based on the attached design mockup. Include all the fields shown in the layout."
```

### Adição de elementos de formulário

**Adições básicas:**

```
"Add a section for personal information"
"Include a file upload for resume"
"Add a dropdown for country selection"
```

**Especificações detalhadas:**

```
"Add a personal information panel with fields for full name, date of birth, phone number, and email address"
"Include a secure file upload component for documents, limited to PDF files under 5MB"
"Add a country dropdown with options for USA, Canada, UK, and Germany"
```

### Criar comportamento dinâmico

**Lógica simples:**

```
"Show additional fields when 'Other' is selected"
"Make the email field required"
"Calculate the total automatically"
```

**Regras de negócio complexas:**

```
"Show the spouse information fields only when marital status is set to 'Married'"
"Calculate the total cost by multiplying quantity and price, then add 10% tax"
"Enable the submit button only when all required fields are completed and terms are accepted"
```

### Layout e design do formulário

**Alterações de layout:**

```
"Make this a multi-step form"
"Organize fields in two columns"
"Convert to an accordion layout"
```

**Melhorias de design:**

```
"Create a wizard-style form with 3 steps: personal info, preferences, and review"
"Arrange the address fields in a compact two-column layout"
"Update the layout to match the attached wireframe"
```

### Envio e integração

**Envio básico:**

```
"Send form data to our email"
"Save responses to a spreadsheet"
"Redirect to a thank you page"
```

**Integração avançada:**

```
"Send form submissions to hr@company.com and create a case in our CRM system"
"Submit data to our REST API endpoint and trigger the new customer workflow"
"Email responses to the sales team and add the lead to our marketing automation platform"
```

## Trabalhar com anexos

Faça upload de arquivos para ajudar a IA a entender exatamente o que você está procurando:

### Tipos de arquivo suportados

| Tipo de arquivo | Melhor para | Exemplo de uso |
|-----------|----------|-------------|
| **Imagens** (PNG, JPG, GIF) | Layouts de formulários, modelos de interface do usuário, digitalizações de formulários em papel | &quot;Criar um formulário correspondente a este layout&quot; |
| **Arquivos PDF** | Formulários existentes para conversão, especificações | &quot;Converter este formulário do PDF em digital&quot; |
| **Arquivos Figma** | Protótipos de design, diretrizes da marca | &quot;Criar este formulário a partir do meu design do Figma&quot; |
| **Arquivos de Design** | Referências visuais, guias de estilo | &quot;Corresponder ao estilo neste design&quot; |

### Como usar anexos

1. **Clique no ícone de anexo** na interface do Assistente de IA
2. **Selecione seu arquivo** no dispositivo
3. **Descreva o que você deseja** fazendo referência ao arquivo anexado:
   - &quot;Criar um formulário com base neste PDF anexado&quot;
   - &quot;Criar um formulário de contato correspondente ao layout nesta imagem&quot;
   - &quot;Converter este formulário em papel em uma versão digital&quot;

### Práticas recomendadas com anexos

- **Use imagens claras e de alta qualidade** para melhorar a análise de IA
- **Concentre-se em um conceito por anexo** (layout, estilo etc.)
- **Descreva o que você deseja** junto com o anexo
- **Manter arquivos abaixo de 10MB** para processamento ideal

## Dicas para obter melhores resultados

### Comece Simples E Acrescente

- Comece com solicitações básicas: &quot;Criar um formulário de contato&quot;
- Adicione detalhes gradualmente: &quot;Adicionar validação ao campo de email&quot;
- Teste e refine: &quot;Torne o campo do telefone opcional&quot;

### Ser Específico Quando Necessário

- Em vez de: &quot;Faça parecer bom&quot;
- Tente: &quot;Usar cores profissionais e tipografia limpa&quot;

### Usar linguagem natural

- Em vez de: &quot;Adicionar componente de entrada de texto&quot;
- Tente: &quot;Adicionar um campo para o nome&quot;

### Referenciar elementos existentes

- Use `@fieldName` para campos existentes: &quot;Tornar @email obrigatório&quot;
- Seja específico quanto aos nomes de campo: &quot;Atualize o campo @phoneNumber&quot;

### Analisar solicitações complexas

- Em vez de uma solicitação grande, tente várias solicitações menores
- Crie o formulário passo a passo
- Teste cada alteração antes de passar para a seguinte

## Ajuda e aprendizado do produto

O Assistente de IA também pode ensiná-lo sobre os recursos do AEM Forms:

### Faça Perguntas Como:

- &quot;Como criar um formulário de várias etapas?&quot;
- &quot;Qual é a diferença entre painéis e seções?&quot;
- &quot;Como configurar notificações por email?&quot;
- &quot;Quais são as práticas recomendadas para formulários móveis?&quot;
- &quot;Como aplicar temas às minhas formas?&quot;

### Obter Ajuda Sobre:

- Conceitos e terminologia do AEM Forms
- Instruções passo a passo para recursos complexos
- Práticas recomendadas
- Solução de problemas comuns

## Referência de recursos avançados

Para usuários que desejam explorar recursos avançados:

### Comandos rápidos

Digite `/` para ver os atalhos disponíveis:

| Comando | Propósito | Exemplo |
|---------|---------|---------|
| `/create-form` | Iniciar um novo formulário | `/create-form customer survey` |
| `/add-form` | Adicionar formulário no Editor Universal | `/add-form contact form` |
| `/update-layout` | Alterar estrutura do formulário | `/update-layout wizard with 3 steps` |
| `/update-field` | Modificar propriedades do campo | `/update-field @email to be required` |
| `/create-rule` | Adicionar comportamento dinâmico | `/create-rule show @spouse if married` |
| `/create-panel` | Adicionar contêineres de campo | `/create-panel Personal Information` |
| `/configure-submit` | Configurar envio de formulário | `/configure-submit to email support` |
| `/help` | Obter assistência | `/help multi-step forms` |

### Sintaxe de referência de campo

Use `@fieldName` para referenciar campos existentes:

- `@firstName` - Campo de nome
- `@email` - Campo de email
- `@phoneNumber` - Campo de número de telefone
- `@dateOfBirth` - Campo de data de nascimento

### Tipos de componentes

Use estes termos para obter melhores resultados:

- `text input` - Campo de texto de linha única
- `text area` - Campo de texto multilinha
- `dropdown` - Selecionar lista
- `checkbox` - Caixa de seleção única
- `checkbox group` - Várias caixas de seleção
- `radio group` - Grupo de botões de opção
- `date picker` - Seleção de data
- `file upload` - Anexo de arquivo
- `panel` - Contêiner de campos de agrupamento

## Resolução de problemas

### Problemas comuns e soluções

**O Assistente de IA não está respondendo:**

- Verifique sua conexão com a Internet
- Verifique se você está em um ambiente compatível
- Feche e abra novamente o painel Assistente de IA

**Resultados Inesperados:**

- Tente reformular sua solicitação mais especificamente
- Dividir solicitações complexas em etapas menores
- Usar a terminologia padrão do AEM Forms

**As Referências De Campo Não Estão Funcionando:**

- Verifique se os nomes dos campos são escritos exatamente como aparecem
- Usar a sintaxe `@fieldName` para campos existentes
- Verifique se o campo existe antes de referenciá-lo

**Problemas de Importação de Design:**

- Verificar se os arquivos estão claros e bem estruturados
- Usar formatos compatíveis (PDF, PNG, JPG, Figma)
- Verificar se o tamanho do arquivo é inferior a 10 MB

## Feedback e suporte

Ajude-nos a melhorar o Assistente de IA:

- **Fornecer feedback**: Use o botão de feedback na interface do Assistente de IA
- **Relatar Problemas**: Entre em contato com o suporte da Adobe pelos canais oficiais
- **Compartilhar experiências**: sua entrada ajuda a melhorar o assistente para todos

## Recursos relacionados

[Assistente do AEM Forms AI - Biblioteca de prompts](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md)
