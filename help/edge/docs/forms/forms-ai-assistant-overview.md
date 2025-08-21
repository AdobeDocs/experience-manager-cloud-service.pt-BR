---
title: Forms Experience Builder
description: Crie formulários avançados mais rapidamente usando os Fragmentos de formulário
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 750674bbd29ec1b29388579d77c7c15bd89335ab
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 0%

---


# Introdução ao Forms Experience Builder

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta documentação está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os recursos, os comandos e os exemplos podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção inicial.

O Forms Experience Builder traz o poder da inteligência artificial para o Adobe Experience Manager (AEM) Forms. Essa solução inovadora transforma o modo como as organizações criam, gerenciam e otimizam seus formulários digitais por meio de interações de linguagem natural e automação inteligente.

Desenvolvido com tecnologias modernas da Web e alimentado por serviços avançados de IA, o Forms Experience Builder permite que usuários técnicos e não técnicos criem formulários sofisticados de nível profissional por meio de interfaces conversacionais. Seja você um analista de negócios que precisa de um formulário de registro simples ou um desenvolvedor que cria fluxos de trabalho complexos de várias etapas, o Forms Experience Builder simplifica todo o processo de criação de formulários.

## Interface de conversa

O Forms Experience Builder fornece uma interface intuitiva baseada em bate-papo que torna a criação de formulários tão simples quanto conversar:

```
┌─────────────────────────────────────────────────────────┐
│ Forms Experience Builder                               │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  👤 User: Create a customer feedback form              │
│                                                         │
│  🤖 AI: I'll help you create a feedback form. What    │
│       type of feedback do you want to collect?         │
│                                                         │
│  👤 User: Product reviews with ratings and comments    │
│                                                         │
│  🤖 AI: Perfect! I've created a feedback form with:   │
│       * Product rating (1-5 stars)                     │
│       * Comment field                                   │
│       * Customer email (optional)                       │
│       * Submit to email notification                    │
│                                                         │
│  👤 User: Add a field for product category             │
│                                                         │
│  🤖 AI: Added a dropdown field with common categories  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## Principais recursos

### Criação de formulários alimentados por IA

**Geração de formulário de linguagem natural**

Crie formulários completos do zero usando descrições em inglês simples. Basta descrever seus requisitos, como &quot;Criar um formulário de feedback do cliente com escalas de classificação e campos de comentário&quot;, e o Forms Experience Builder gera a estrutura de formulário, os tipos de campo e as regras de validação apropriados.

**Gerenciamento dinâmico de campos**

Adicione, modifique ou remova campos de formulário por meio de comandos conversacionais. A IA entende o contexto e pode sugerir de forma inteligente tipos de campo, regras de validação e melhorias na interface do usuário com base em seus requisitos.

**Otimização de layout**

Atualizar layouts e configurações de formulário por meio do idioma natural. Solicite alterações como &quot;Tornar o formulário mais móvel&quot; ou &quot;Reorganizar campos em um fluxo lógico&quot; e o Forms Experience Builder aplica ajustes adequados de estilo e layout.

### Importação e conversão inteligente

**Conversão de PDF em Formulário**

Transforme documentos estáticos do PDF em formulários interativos e dinâmicos. Carregue qualquer documento do PDF e o Forms Experience Builder analisa a estrutura para criar um formulário digital correspondente com tipos de campo e validação apropriados.

**URL para conversão de formulário**

Converter formulários ou páginas da Web existentes no AEM Forms. Basta fornecer um URL, e o Forms Experience Builder extrai elementos de formulário e os recria como AEM Forms nativo com funcionalidade aprimorada.

**Suporte a Arquivos com Vários Formatos**

Lide com vários tipos de arquivos para criação de formulários, incluindo PDFs, imagens, capturas de tela e modelos de formulário existentes. O Forms Experience Builder pode processá-los e convertê-los em AEM Forms funcional.

### Lógica e integração avançadas do formulário

**Geração de Regra Inteligente**

Criar validação de formulário complexa e regras de lógica de negócios por meio da linguagem natural. O Forms Experience Builder pode gerar lógica condicional sofisticada, dependências de campo e regras de validação que normalmente exigiriam um amplo conhecimento de codificação.

**Configuração Abrangente da Ação de Envio**

Configurar envios de formulários para integrar aos sistemas comerciais existentes:

- **Integração de email**: configurar notificações e confirmações automatizadas por email
- **Pontos de Extremidade da API REST**: Conectar a aplicativos e serviços personalizados
- **Armazenamento na nuvem**: integre-se ao Azure Blob Storage, SharePoint e OneDrive
- **Automação de Fluxo de Trabalho**: Conectar ao Power Automate e ao Workfront Fusion
- **Plataformas de marketing**: integração direta com a Marketo para gerenciamento de clientes potenciais
- **Fluxos de trabalho do AEM**: aproveitar os recursos de fluxo de trabalho existentes do AEM

**Análise de desempenho**

Analise o desempenho da conversão de formulários e os padrões de engajamento do usuário. O Forms Experience Builder fornece insights sobre a eficácia do formulário e sugere otimizações para melhorar as taxas de conclusão e a experiência do usuário.

## Como funciona

O Forms Experience Builder segue uma abordagem simples e conversacional:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  1. Describe    │───▶│  2. AI Creates  │───▶│  3. Refine &    │
│  Your Form      │    │  Initial Form   │    │  Configure      │
│  Requirements   │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────────────────────────────────────────────────────┐
│  "Create a loan application form"  →  Form with relevant        │
│  "Add conditional logic"           →  fields and basic          │
│  "Connect to CRM system"           →  validation rules          │
└─────────────────────────────────────────────────────────────────┘
```

## Exemplos de caso de uso

### Formulário de pedido de empréstimo

```
┌─────────────────────────────────────────────────────────┐
│ Loan Application - Multi-Step Form                    │
├─────────────────────────────────────────────────────────┤
│ Step 1: Personal Information                           │
│  🏠 Property Type: [Primary] [Investment] [Commercial] │
│  💰 Loan Amount: [$_______] (triggers different paths) │
│  📊 Income Verification: [W2] [Self-Employed] [Other]  │
│                                                         │
│ Step 2: Financial Details (conditional based on above) │
│  ↳ If Self-Employed: Show tax returns, profit/loss     │
│  ↳ If W2: Show employment history, pay stubs           │
│  ↳ Complex debt-to-income calculations                 │
│                                                         │
│ Step 3: Compliance & Review                            │
│  📋 Regulatory disclosures, digital signatures         │
│  🔍 Automated eligibility pre-screening                │
└─────────────────────────────────────────────────────────┘
```

### Formulário de reclamação de seguro

```
┌─────────────────────────────────────────────────────────┐
│ Insurance Claim - Adaptive Form                        │
├─────────────────────────────────────────────────────────┤
│ 🚗 Claim Type: [Auto] [Property] [Health] [Business]   │
│                                                         │
│ ↳ Auto Selected: Shows accident details, police report │
│ ↳ Property: Shows damage assessment, repair estimates  │
│ ↳ Health: Shows medical provider network, pre-auth     │
│                                                         │
│ 📎 Dynamic Document Requirements:                       │
│   * Photos/videos of damage                            │
│   * Police reports (auto only)                         │
│   * Medical records (health only)                      │
│   * Repair estimates (property only)                   │
│                                                         │
│ 🔄 Real-time claim status updates                      │
└─────────────────────────────────────────────────────────┘
```

### Cenários de migração e conversão

Transforme seus formulários existentes em experiências digitais avançadas com a conversão baseada em IA.


### 📄 PDF para Digital

**De documentos estáticos para formulários interativos**

Transforme o PDF forms com mais de 50 campos em experiências digitais dinâmicas com cálculos automatizados e design responsivo para dispositivos móveis.

**Principais benefícios:**

- Cálculos de impostos automatizados e dependências de campo
- Integração de assinaturas digitais e arquivamento eletrônico
- Otimização do layout responsivo para dispositivos móveis
- 95% de redução nos erros de processamento

**Recomendado para:** Formulários de imposto, solicitações do governo, documentos comerciais complexos

**Economia de tempo:** 2-3 horas → 15 minutos por formulário



### Modernização de XFA herdado 🏛️

**Transforme sua nova vida em formulários desatualizados**

Converta aplicativos XFA complexos em assistentes modernos de várias etapas com validação em tempo real e conformidade com acessibilidade.

**Principais benefícios:**

- Interface simplificada do assistente de várias etapas
- Validação em tempo real com ajuda contextual
- Integração de banco de dados governamental
- Conformidade total com a acessibilidade da WCAG 2.1

**Recomendado para:** permissões do governo, aplicativos corporativos, formulários de conformidade

**Impacto:** conclusão 70% mais rápida, 90% menos erros




### 📱 captura de tela para digital

**Transforme qualquer formulário em papel em uma experiência digital**

Carregue uma imagem de qualquer formulário em papel e assista aos campos de extração de IA, otimize o layout e crie formulários digitais prontos para integração.

**Principais benefícios:**

- Detecção inteligente de tipo de campo (99% ou mais de precisão)
- Geração de layout responsivo otimizado
- Validação aprimorada além do papel original
- Arquitetura pronta para integração

**Recomendado para:** aplicativos de papel, formulários manuscritos, documentos herdados

**Tempo de processamento:** 2 horas → 5 minutos por formulário



### Aprimoramento do HTML 🌐

**Turbine seus formulários web existentes**

Adicione validação avançada, lógica condicional e envio de vários canais aos formulários básicos do HTML sem romper a funcionalidade existente.

**Principais benefícios:**

- Lógica e regras de validação avançadas
- Comportamentos e fluxos de trabalho de campo condicionais
- Opções de envio de vários canais
- Análise integrada e rastreamento de desempenho

**Recomendado para:** Formulários de contato, formulários de registro, aplicativos web simples

**Aperfeiçoamento de conversão:** +40% com experiência aprimorada do usuário


## Forms Experience Builder versus desenvolvimento tradicional

| Aspecto | Criação de formulário tradicional | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **Hora de criação** | 2 a 3 dias | 2 a 3 horas |
| **Conhecimento Técnico** | Obrigatório | Não obrigatório |
| **Regras de validação** | Codificação manual | Linguagem natural |
| **Otimização móvel** | CSS/JS manual | Automático |
| **Acessibilidade** | Implementação manual | Conformidade integrada |
| **Atualizações** | Alterações de código necessárias | Linguagem natural |


## Benefícios para organizações

### Criação democratizada de formulários

Capacite usuários não técnicos a criar formulários sofisticados sem conhecimento de programação. Analistas de negócios, especialistas no assunto e criadores de conteúdo podem traduzir diretamente seus requisitos em formulários funcionais por meio de conversas em linguagem natural.

### Tempo de implantação reduzido (TTV)

Acelere drasticamente o desenvolvimento de formulários, de dias para horas. O que antes exigia amplos ciclos de desenvolvimento agora pode ser realizado em uma única sessão por meio de IA conversacional, permitindo uma entrada mais rápida no mercado de iniciativas digitais.

### Simplicidade da interface

Elimine a curva de aprendizado com uma interface de conversação intuitiva. Os usuários podem criar formulários complexos usando a linguagem natural em vez de aprender ferramentas técnicas de construção de formulários, reduzindo o tempo de treinamento e aumentando a adoção.

### Dimensionar esforços de modernização

Modernize portfólios de formulários herdados com eficiência. Converta formulários PDF, XFA e HTML existentes em experiências digitais responsivas, preservando a lógica de negócios e aprimorando a experiência do usuário em todo o seu ecossistema de formulários.

## Introdução

Para começar a usar o Forms Experience Builder, visite a [documentação do Forms Experience Builder](forms-ai-assistant-getting-started.md). Você pode acessar o Forms Experience Builder por meio do Editor do AEM Forms ou do Editor universal, dependendo do seu fluxo de trabalho preferido.

Para organizações que desejam transformar seus processos de criação de formulários, o Forms Experience Builder oferece uma solução eficiente e intuitiva que combina a flexibilidade da IA de conversação com a robustez do gerenciamento de formulários de nível empresarial.

## Integração e acesso antecipado

O Forms Experience Builder está disponível no momento como parte do programa de Acesso antecipado (EA). Para participar e obter acesso, siga estas etapas:

1. Verifique se você está usando seu endereço de email comercial oficial associado à sua organização.
2. Envie um email para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) solicitando acesso ao Forms Experience Builder.
3. Inclua o nome da organização e todos os detalhes relevantes do projeto em sua solicitação para ajudar a agilizar o processo de integração.

>[!NOTE]
>
> O acesso ao Forms Experience Builder é limitado aos participantes aprovados no programa Acesso antecipado. A Adobe analisará sua solicitação e fornecerá mais instruções para integração, se você estiver qualificado.

Para obter mais informações sobre o programa de Acesso Antecipado e seus recursos, consulte a [documentação de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).

