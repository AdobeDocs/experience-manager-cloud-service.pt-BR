---
title: 'Construtor de formulários: escolha sua abordagem'
description: Compare os construtores de formulários e encontre a abordagem certa para criar formulários adaptáveis. Seja você um criador de formulários que precisa de modelos ou de formulários complexos, escolha o melhor construtor de formulários para suas necessidades.
keywords: construtor de formulários, AEM forms, criador de formulários, criar formulários, criador de formulários, formulários adaptáveis, componentes principais, componentes de base, serviços de entrega de borda, criar formulários
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: choose-form-builder-guide
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 3%

---


# Construtor de formulários: escolha sua abordagem {#choose-your-form-builder}

O Adobe Experience Manager (AEM) Forms fornece três abordagens avançadas de criação de formulários, cada uma projetada para casos de uso diferentes, requisitos técnicos e destinos de publicação. Seja você um criador de formulários procurando modelos ou um desenvolvedor criando formulários complexos, este guia ajuda você a escolher o construtor de formulários correto para seu projeto.

## Guia de decisão rápida

Use esta referência rápida para identificar o melhor construtor de formulários para suas necessidades:

| **Se você precisar...** | **Escolher** |
|-------------------|------------|
| **Formulários modernos e escalonáveis com os recursos mais recentes** | Componentes principais |
| **Formulários com velocidade surpreendente para sites de alto tráfego** | Editor universal |
| **Manter formulários existentes ou integrações herdadas** | Componentes de fundação |
| **Criação visual de arrastar e soltar** | Componentes principais ou editor universal |
| **Criação de formulário com base em planilha** | Criação baseada em documento |
| **Entrega omnicanal (Web, celular, quiosques)** | Componentes principais (com APIs headless) |
| **Aplicativos de front-end personalizados (React, Angular)** | Componentes principais (com APIs headless) |
| **Controle total sobre a renderização do formulário** | Componentes principais (com APIs headless) |

## Noções básicas sobre as opções do construtor de formulários

O AEM Forms oferece três abordagens principais de criação de formulário, cada uma projetada para diferentes tipos de criadores de formulário e casos de uso. Não importa se você precisa de um criador de formulários simples para tarefas rápidas ou de recursos avançados de construtor de formulários para projetos complexos, há uma abordagem que atenda às suas necessidades:

### Construtor de formulários do componente de Fundação

Os Componentes de base representam a experiência clássica de criação do AEM Forms. Embora ainda sejam compatíveis, eles são recomendados principalmente para manter formulários existentes em vez de criar novos.

**Características-chave:**

- Interface de criação tradicional do AEM
- Estabilidade comprovada para workflows existentes
- Limitado à publicação somente no AEM
- Biblioteca básica de componentes

### Construtor de formulários do componente principal

Os Componentes principais fornecem os recursos mais recentes do AEM Forms com desempenho, acessibilidade e flexibilidade aprimorados. Este construtor de formulários é ideal para criadores de formulários que precisam de resultados profissionais com recursos modernos. Ela é compatível com a publicação no AEM e no Edge Delivery Services e produz automaticamente formulários headless para entrega orientada por API em várias plataformas.

**Características-chave:**

- Componentes modernos e padronizados
- Melhor desempenho e acessibilidade
- Opções de publicação flexíveis (AEM + Edge Delivery)
- Recursos avançados de personalização
- Arquitetura que não se torna obsoleta
- Geração automática de formulário headless para entrega omnicanal

### Editor universal (Edge Delivery Services)

O Universal Editor oferece duas abordagens de criação avançadas para o Edge Delivery Services: a criação visual do WYSIWYG e a criação baseada em documentos usando planilhas. Essa abordagem do criador de formulários é perfeita para usuários que desejam criar formulários rapidamente com desempenho excepcional.

**Características-chave:**

- Desempenho excepcional (altas pontuações do Lighthouse)
- Dois métodos de criação: WYSIWYG e baseado em documento
- Otimizado para o Edge Delivery Services
- Desempenho excepcional e SEO
- Desenvolvimento e implantação rápidos


## Comparação detalhada

### Capacidades técnicas

| **Recurso** | **Fundação** | **Núcleo** | **Editor Universal** | **Baseado em documento** |
|----------------|----------------|----------|---------------------|-------------------|
| **Complexidade do formulário** | Básico | Avançado | Avançado | Simples a moderado |
| **Mecanismo de regras** | Avançado | Avançado | Avançado | Limitado |
| **Componentes personalizados** | ✅ | ✅ | ✅ | ✅ |
| **Temas** | ✅ | ✅ | Nível do projeto | Nível do projeto |
| **Modelos** | ✅ | ✅ | Somente conteúdo inicial |  |
| **Fragmentos** | ✅ | ✅ | ✅ | ✅ |
| **Localização** | ✅ | ✅ | Via AEM Sites | Manual/Funções |

### Integração e envio

| **Recurso** | **Fundação** | **Núcleo** | **Editor Universal** | **Baseado em documento** |
|-------------|----------------|----------|---------------------|-------------------|
| **Modelos de dados** | FDM, Personalizado | FDM, Personalizado | FDM, Personalizado | Personalizado |
| **Enviar ações** | Várias opções | Várias opções | Várias opções | Somente planilha |
| **Preenchimento prévio** | ✅ | ✅ | Através do assistente | ✅ |
| **CAPTCHA** | Vários tipos | reCAPTCHA, hCaptcha | reCAPTCHA Enterprise | reCAPTCHA Enterprise |
| **Anexos** | ✅ | ✅ | ✅ | Acesso antecipado |
| **Assinaturas digitais** | ✅ |  |  |  |

### Publicação e desempenho

| **Aspecto** | **Fundação** | **Núcleo** | **Editor Universal** | **Baseado em documento** |
|------------|----------------|----------|---------------------|-------------------|
| **Publicação** | Somente AEM | AEM + Edge Delivery + APIs headless | Edge Delivery | Edge Delivery |
| **Desempenho** | Padrão | Aprimorado | Pontuações altas de farol | Pontuações altas de farol |
| **Otimização da SEO** | Básico | Bom | Excelente | Excelente |
| **Capacidade de resposta móvel** | Bom | Excelente | Excelente | Excelente |

## Escolher o construtor certo

### Escolha os componentes de base se:

- Você está mantendo formulários com base em Fundação existentes
- Você precisa da integração de assinatura digital
- Seu fluxo de trabalho depende dos recursos fundamentais estabelecidos
- Você está trabalhando dentro dos requisitos de publicação exclusivos do AEM

**Ideal para:** Manutenção de formulários, integração de sistemas herdados, fluxos de trabalho estabelecidos

### Escolher componentes principais se:

- Você está construindo formas novas e modernas
- Você precisa de flexibilidade para publicar no AEM ou no Edge Delivery Services
- Você deseja os recursos mais recentes
- Você precisa de personalização e temas avançados
- Acessibilidade e desempenho são prioridades
- Você quer tecnologia que não se torna obsoleta

**Ideal para:** Novos projetos, soluções escaláveis, experiências modernas na Web

### Escolha o editor universal se:

- Você precisa de desempenho excepcional e SEO
- Você está criando para sites do Edge Delivery Services
- Você precisa de formulários complexos com ações personalizadas
- É necessária a integração com sistemas externos

**Ideal para:** sites de alto desempenho, Edge Delivery Services, fluxos de trabalho de criação visual

### Escolha a criação baseada em documento se:

- Os usuários empresariais preferem a criação baseada em planilhas
- Você precisa de prototipagem e implantação rápidas
- As Forms são relativamente simples (pesquisas, registros, feedback)
- A coleta de dados em planilhas atende às suas necessidades
- Não são necessários workflows de envio avançados

**Ideal para:** Implantação rápida, criação de usuários empresariais, coleta de dados simples


## Considerações sobre migração

### Da base aos componentes principais

- **Abordagem recomendada:** Use a [ferramenta de utilitário de migração](/help/forms/migration-utility-tool-for-af-core-components.md)
- **Vantagens:** recursos modernos, melhor desempenho, recurso de publicação dupla
- **Esforço:** moderado a alto, dependendo da complexidade do formulário

### Do editor tradicional ao editor universal

- **Abordagem:** Recompile formulários usando o WYSIWYG ou a criação com base em documento no Editor Universal
- **Benefícios:** desempenho excepcional, experiência moderna em desenvolvimento, altas pontuações em SEO
- **Esforço:** alto para formulários complexos, baixo para formulários simples

## Introdução

Depois de escolher o construtor de formulários:

### Componentes de base

1. [Criar um formulário adaptável (componentes de base)](/help/forms/creating-adaptive-form.md)
2. [Guia de criação dos Componentes de base](/help/forms/introduction-forms-authoring.md)

### Componentes principais

1. [Criar um formulário adaptável (componentes principais)](/help/forms/creating-adaptive-form-core-components.md)
2. [Visão geral do recurso Componentes principais](/help/forms/adaptive-form-core-components-json-schema-form-model.md)

### Editor universal (Edge Delivery Services)

1. **Criação no WYSIWYG:** [Introdução ao Universal Editor](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
2. **Criação Baseada em Documento:** [Crie seu primeiro formulário com planilhas](/help/edge/docs/forms/tutorial.md)


## Precisa de ajuda para decidir?

Ainda não sabe ao certo qual construtor de formulários escolher? Considere estes fatores:

- **Experiência da equipe:** qual é o nível de habilidade técnica da sua equipe?
- **Linha do tempo do projeto:** Com que rapidez você precisa implantar?
- **Requisitos de desempenho:** Velocidade e SEO são essenciais?
- **Escalabilidade futura:** Você precisará expandir ou modificar formulários com frequência?
- **Destino de publicação:** Onde seus formulários serão publicados?

Para obter orientação personalizada, consulte sua equipe de implementação do AEM Forms ou o suporte da Adobe.

## Artigos relacionados

- [Comparação detalhada da criação de formulários](/help/edge/docs/forms/authoring-a-form.md)
- [Visão geral dos Componentes principais do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR)
- [Visão geral do Edge Delivery Services para Forms](/help/edge/docs/forms/overview.md)
- [Forms adaptável headless com componentes principais](https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service)
