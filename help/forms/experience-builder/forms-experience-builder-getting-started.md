---
title: Introdução ao Forms Experience Builder
description: Aprenda os conceitos básicos para criar seu primeiro formulário alimentado por IA com o Forms Experience Builder. Tutorial detalhado com exemplos e práticas recomendadas.
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: c4f838bc-a001-48e7-afaa-c2ff9034f5d4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---

# Introdução ao Forms Experience Builder {#getting-started-forms-experience-builder}

O Forms Experience Builder revoluciona a criação de formulários aproveitando a IA para transformar descrições de linguagem natural em formulários digitais totalmente funcionais. Este guia ajudará você a criar seu primeiro formulário e entender os conceitos principais que tornam o Forms Experience Builder eficiente.

## O que é o Forms Experience Builder? {#what-is-forms-experience-builder}

O Forms Experience Builder é uma ferramenta de criação de formulários habilitada por IA que permite criar formulários digitais sofisticados usando linguagem conversacional. Em vez das interfaces tradicionais de arrastar e soltar ou de codificação complexa, você simplesmente descreve o que deseja, e a IA cria o formulário para você.

**Principais recursos:**

* **Criação de formulário em linguagem natural** - Descreva seus requisitos de formulário em inglês simples

* **Importação e conversão inteligentes** - Transforme documentos existentes em formulários interativos

* **Geração de campo inteligente** - Campos alimentados por IA com opções preenchidas previamente

* **Automação da lógica de negócios** - Criar regras condicionais e validação por meio de conversa

* **Integração do sistema** - Conectar formulários aos fluxos de trabalho de negócios existentes

## Pré-requisitos {#prerequisites-getting-started}

Antes de começar, verifique se você tem:

* **Acesso ao Forms Experience Builder** - Disponível por meio do Programa de acesso antecipado
* **AEM Forms as a Cloud Service** - Ambiente de produção do autor com os Componentes principais adaptáveis do Forms
* **Noções básicas** - Familiaridade com conceitos de formulário e requisitos comerciais

Para obter requisitos técnicos detalhados e configuração de ambiente, consulte [Implantar e configurar o Forms Experience Builder](deploy-forms-experience-builder.md).

## Maneiras de criar formulários {#two-ways-to-create-forms}

Depois de usar o Assistente do Forms para selecionar um [modelo de Componentes principais](/help/forms/creating-adaptive-form-core-components.md) ou [modelo do Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md), tema e outras opções, o Forms Experience Builder oferece duas abordagens principais para a criação de formulários:

### &#x200B;1. Criar do zero {#create-from-scratch}

Crie formulários usando descrições de linguagem natural de seus requisitos.

**Quando usar:**

* Criação de novos formulários a partir das necessidades

* Criação de formulários para novos processos de negócios

* Quando você tem especificações claras, mas não tem documentos existentes

**Exemplo:**

    Crie um formulário de feedback de cliente com:
    &#x200B;- Classificação do produto (1-5 estrelas)
    &#x200B;- Campo Comentário para feedback detalhado
    &#x200B;- Email de cliente (opcional)
    &#x200B;- Enviar notificação por email

>[!VIDEO](https://video.tv.adobe.com/v/3473104)



### &#x200B;2. Importar e converter {#import-and-convert}

Transforme documentos existentes em formulários digitais interativos.

Antes de usar essa opção, carregue seu arquivo PDF ou uma imagem do formulário. O PDF pode ser um formulário do PDF baseado no AcroForm ou no XFA. Para [outros tipos de PDF forms](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/forms/document-services/pdf-forms-and-documents), use a opção [Preparar Formulário](https://helpx.adobe.com/in/acrobat/using/creating-distributing-pdf-forms.html) no Adobe Acrobat para convertê-los em um AcroForm

**Quando usar:**

* Conversão de PDF forms existente

* Modernização de processos baseados em papel

* Quando você tiver designs de formulário existentes para aprimorar

**Exemplo:**

    /create-form converter o arquivo PDF anexado em um formulário adaptável

>[!VIDEO](https://video.tv.adobe.com/v/3474042)


## Seu primeiro formulário: Tutorial passo a passo {#first-form-tutorial}

Vamos criar um formulário de contato simples para entender o fluxo de trabalho básico.

### Etapa 1: iniciar com uma descrição simples {#step-1-simple-description}

Comece com uma descrição básica do formulário:

    Criar um formulário básico de contato com campos de nome, email e mensagem

Isso cria um formulário com três campos essenciais.

![Formulário com três campos essenciais - criado usando o prompt de idioma natural](/help/forms/assets/forms-experience-builder-contact-us-form.png)

### Etapa 2: adicionar validação e requisitos {#step-2-add-validation}

Aprimorar o formulário com regras de validação:

    Tornar @name e @email campos obrigatórios com validação adequada

O símbolo `@` faz referência a campos específicos para modificações direcionadas.

![Validação adicionada no construtor de experiências de formulários usando o prompt de linguagem natural](/help/forms/assets/forms-experience-builder-contact-us-form-add-validation.png)


### Etapa 3: melhorar a experiência do usuário {#step-3-improve-ux}

Adicionar texto e orientação úteis sobre o espaço reservado:

    Adicionar texto de espaço reservado: @name &quot;Seu nome completo&quot;, @email &quot;your.email@company.com&quot;, @message &quot;Diga-nos como podemos ajudar&quot;

![Validação adicionada usando prompts de linguagem natural no forms experience builder](/help/forms/assets/forms-experience-builder-contact-us-form-add-placeholder.png)

### Etapa 4: adicionar recursos avançados {#step-4-advanced-features}

Incluir funcionalidade adicional:

    Adicionar dois menus suspensos
    
    &#x200B;- surveyType com opções: &quot;Pergunta Geral&quot;, &quot;Solicitação de Suporte&quot;, &quot;Consulta de Vendas&quot;, &quot;Parceria&quot;
    
    &#x200B;- urgênciaLevel com opções (Baixo, Medium, Alto)


![Adição de componentes suspensos usando prompts de linguagem natural no forms experience builder](/help/forms/assets/forms-experience-builder-contact-us-form-add-dropdown.png)


### Etapa 5: Implementar lógica condicional {#step-5-conditional-logic}

Crie um comportamento inteligente e sensível ao contexto ao adicionar regras como:

    Ocultar a lista suspensa @urgencyLevel no carregamento do formulário
    Mostrar lista suspensa @urgencyLevel (Baixo, Medium, Alto) somente quando @inquiryType for igual a &quot;Solicitação de Suporte&quot;

Essas são duas regras separadas: uma oculta a lista suspensa de nível de urgência quando o formulário é carregado e a outra mostra somente quando o tipo de consulta é &quot;Solicitação de suporte&quot;. É necessário criar cada regra com um prompt separado, apenas uma regra pode ser criada por vez.

## Noções básicas sobre a abordagem de conversação de IA {#ai-conversation-approach}

O Forms Experience Builder usa uma interface conversacional em que você pode:

### Campos de referência com símbolos @ {#reference-fields}

Use `@fieldName` para referenciar campos específicos:

    Tornar @email um campo obrigatório
    Adicionar validação a @phoneNumber para o formato dos EUA
    Alterar texto @submitButton para &quot;Enviar Mensagem&quot;

>[!VIDEO](https://video.tv.adobe.com/v/3474043)


### Usar comandos de linguagem natural {#natural-language-commands}

Descreva o que você deseja em inglês simples:

    &#x200B;- Adicionar uma seção para informações da empresa
    &#x200B;- Criar uma lista suspensa para seleção de departamento
    &#x200B;- Incluir um carregamento de arquivo para retomada
    &#x200B;- Configurar notificações por email quando o formulário for enviado

### Criar de forma incremental {#build-incrementally}

Comece simples e adicione complexidade gradualmente:

1. **Estrutura básica** - Criar os campos essenciais primeiro
2. **Adicionar validação** - Implementar campos obrigatórios e validação de formato
3. **Aprimorar UX** - Adicionar espaços reservados, texto de ajuda e estilo
4. **Implementar lógica** - Adicionar regras condicionais e lógica de negócios
5. **Configurar envio** - Configurar o processamento e as notificações do formulário


## Padrões comuns de formulários {#common-form-patterns}

### Formulários de contato e feedback {#contact-feedback-forms}

**Formulário básico de contato:**

    Criar um formulário de contato com:
    &#x200B;- Nome (obrigatório)
    &#x200B;- Email (obrigatório, validado)
    &#x200B;- Lista suspensa de assunto (Geral, Suporte, Vendas, Parceria)
    &#x200B;- Mensagem (obrigatório, várias linhas)
    &#x200B;- Botão Enviar

**Formulário de feedback do cliente:**

    Crie um formulário de feedback de cliente com:
    &#x200B;- Classificação do produto (1-5 estrelas)
    &#x200B;- Campo Comentário para feedback detalhado
    &#x200B;- Email de cliente (opcional)
    &#x200B;- Enviar notificação por email

### Formulários de registro e integração {#registration-onboarding-forms}

**Registro de usuário:**

    Crie um formulário de registro de usuário com:
    &#x200B;- Informações pessoais (nome, email, telefone)
    &#x200B;- Preferências da conta (boletim informativo, notificações)
    &#x200B;- Aceitação dos termos e condições
    &#x200B;- Criação de senha com validação de força

**Integração de funcionários:**

    Crie um formulário de integração de funcionário com:
    &#x200B;- Detalhes pessoais e informações de contato
    &#x200B;- Informações de emprego e data de início
    &#x200B;- Carregamentos de documentos (currículo, ID, formulários de impostos)
    &#x200B;- Seleção e preferências de benefícios

### Formulários de pesquisa e avaliação {#survey-assessment-forms}

**Pesquisa de satisfação do cliente:**

    Crie uma pesquisa de satisfação do cliente com:
    &#x200B;- Classificação geral (escala 1-10)
    &#x200B;- Classificações de categoria (produto, serviço, suporte)
    &#x200B;- Seções de comentários abertas
    &#x200B;- Informações demográficas (opcional)

**Avaliação de habilidades:**

    Crie um formulário de avaliação de habilidades com:
    &#x200B;- Categorias de habilidades com níveis de proficiência
    &#x200B;- Duração da experiência para cada habilidade
    &#x200B;- Informações de certificação e treinamento
    &#x200B;- Autoavaliação e metas

## Teste e validação {#testing-validation}

### Sempre testar seus formulários {#always-test-forms}

Antes de implantar qualquer formulário:

1. **Testar todos os campos** - Garantir que a validação funcione corretamente

2. **Verificar lógica condicional** - Verifique se as regras disparam corretamente

3. **Envio de teste** - Confirme se os dados estão sendo processados corretamente

4. **Validar em dispositivos diferentes** - Garantir compatibilidade móvel

5. **Análise com participantes** - Obtenha feedback dos usuários finais

### Padrões comuns de validação {#validation-patterns}

**Validação de email:**

    Adicionar validação de formato de email ao campo @email

**Validação do número de telefone:**

    Adicionar validação de formato de número de telefone dos EUA a @phoneNumber

**Validação de idade:**

    Adicionar validação de idade: deve ter 18 anos ou mais para @dateOfBirth

**Validação de carregamento de arquivo:**

    Adicionar validação de tipo de arquivo: somente PDF, DOC, DOCX permitidos para @resume
    Adicionar limite de tamanho de arquivo: máximo de 5 MB para @resume

## Próximas etapas {#next-steps}

Agora que você entende o básico, explore estes tópicos avançados:

* **[Campos inteligentes aprimorados com LLM](forms-experience-builder-llm-smart-fields.md)** - Crie campos com opções pré-preenchidas usando conhecimento de IA
* **[Criação de formulário habilitado por IA](forms-experience-builder-prompt-examples-library.md)** - Padrões de prompt avançados e exemplos
* **[Importação e conversão inteligentes](intelligent-import-conversion.md)** - Transforme documentos existentes em formulários
* **[Envio e integração de formulários](form-submission-integration.md)** - Conecte formulários aos sistemas da sua empresa


## Artigos relacionados

* [Visão geral do Forms Experience Builder](product-overview.md)
* [Campos inteligentes aprimorados por LLM](forms-experience-builder-llm-smart-fields.md)
* [Criação de formulários alimentados por IA](forms-experience-builder-prompt-examples-library.md)
* [Importação e conversão inteligentes](intelligent-import-conversion.md)
* [Envio e integração de formulários](form-submission-integration.md)
* [Perguntas frequentes](forms-experience-builder-frequently-asked-questions.md)
