---
title: Componentes principais do Forms adaptável vs Edge Delivery Services Forms vs Componentes de base
description: Comparação técnica de abordagens de criação do AEM Forms - Componentes principais, Edge Delivery Services Forms e Componentes de base. Arquitetura, renderização, recursos e casos de uso
keywords: comparação de formulários adaptáveis, componentes principais, componentes de base, formulários de serviços de entrega de borda, comparação de formulários do AEM, comparação do construtor de formulários
role: Architect, Developer, Admin
level: Intermediate
feature: Adaptive Forms, Core Components, Edge Delivery Services
exl-id: adaptive-forms-comparison
source-git-commit: 37799555babb15809409ec5cda8a1c46ceff24f2
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 5%

---


# Forms adaptável: componentes principais vs Edge Delivery Services Forms vs Componentes de base

O Adobe Experience Manager (AEM) Forms fornece três abordagens distintas para a criação de experiências de captura de dados: Forms adaptável com base em componentes principais, Edge Delivery Services Forms e Forms adaptável com base em componentes de base. Cada abordagem tem uma arquitetura, um modelo de renderização e um caso de uso de destino diferentes. Este artigo fornece uma comparação técnica para ajudar os arquitetos, desenvolvedores e clientes da AEM a selecionar a abordagem apropriada para seus requisitos.

## Visão geral

Todos os três tipos de formulário atendem à finalidade de capturar dados do usuário e integrar-se a sistemas de back-end. No entanto, eles diferem em sua arquitetura subjacente, onde os formulários são renderizados, como são entregues e quais recursos são compatíveis.

| Abordagem | Status | Caso de uso principal |
|----------|--------|------------------|
| **Componentes principais** | Recomendado para novos formulários | Formulários modernos e escalonáveis que exigem criação no AEM com opções de publicação flexíveis |
| **Edge Delivery Services Forms** | Recomendado para sites de desempenho crítico | Formulários de alto desempenho fornecidos de ponta com implantação rápida |
| **Componentes de base** | Modo de manutenção | Formulários existentes que exigem suporte a recursos herdados |

## Forms adaptável com base nos componentes principais

### Definição

Os Componentes principais adaptáveis do Forms são um conjunto de 30 componentes de código aberto, compatíveis com BEM, criados com base nos Componentes principais do WCM no Adobe Experience Manager. Elas representam a abordagem recomendada pela Adobe para a criação do novo Forms adaptável, fornecendo arquitetura moderna, desempenho aprimorado e geração automática de formulários headless.

### Arquitetura

Os Componentes principais usam uma arquitetura de componentes modular padronizada:

- **Component Foundation**: baseado nos Componentes principais do WCM do AEM
- **Metodologia de Estilo**: Convenções CSS de BEM (Block Element Modifier)
- **Armazenamento de conteúdo**: repositório JCR com nós de conteúdo estruturado
- **Renderização**: renderização do lado do servidor no AEM com renderização headless opcional do lado do cliente
- **Source**: fonte aberta (disponível no [GitHub](https://github.com/adobe/aem-core-forms-components))

### Modelo de renderização

Os Componentes principais são compatíveis com vários modelos de renderização:

1. **Renderização do Servidor (SSR)**: a renderização do Forms no servidor do AEM e a entrega completa do HTML ao navegador
2. **Renderização headless**: o Forms expõe representações JSON por meio de APIs para renderização no lado do cliente em React, Angular ou outras estruturas
3. **Renderização Híbrida**: combinação de renderização de servidor e cliente para obter o desempenho ideal

### Opções de publicação

- Instâncias de publicação do AEM
- Edge Delivery Services (quando configurado)
- APIs headless para aplicativos de front-end personalizados

### Principais recursos

| Categoria | Recursos |
|----------|-------------|
| **Componentes** | 30 componentes padronizados, incluindo caixa de texto, caixa numérica, seletor de data, lista suspensa, grupo de caixas de seleção, botão de opção, anexo de arquivo, assistente, acordeão, guias horizontais/verticais |
| **Modelos de formulário** | Esquema JSON (v4 e 2020-12), modelo de dados de formulário (FDM), modelos XDP/XFA (limitado) |
| **Mecanismo de regras** | Editor visual de regras com lógica condicional, validação, chamada de serviço, funções personalizadas |
| **Enviar Ações** | Endpoint REST, Email, Fluxo de trabalho do AEM, SharePoint, OneDrive, Armazenamento Azure Blob, Power Automate, Workfront Fusion, Modelo de dados de formulário |
| **Preenchimento prévio** | Serviço de preenchimento do modelo de dados de formulário, serviços de preenchimento personalizado |
| **CAPTCHA** | reCAPTCHA, hCaptcha, tartaruga |
| **Documento de registro** | Geração de PDF com modelos personalizados ou OOTB |
| **Acessibilidade** | Compatível com WCAG, rótulos ARIA, navegação pelo teclado, suporte ao leitor de tela |
| **Localização** | Suporte a vários idiomas por meio do fluxo de trabalho de tradução do AEM |
| **Controle de versão** | Controle de versão de conteúdo herdado do AEM Sites |

### Pré-requisitos

- **AEM Forms as a Cloud Service**: Componentes principais habilitados por padrão
- **AEM 6.5 Forms**: exige a habilitação via Arquétipo do AEM
- **Permissões de usuário**: o usuário deve estar no grupo `forms-users`
- **Modelo**: modelo de formulário adaptável (componente principal) necessário
- **Tema**: tema da tela (OOTB) ou tema personalizado

### Limitações  

- **Restrições de Esquema JSON**: tipo nulo, tipos de união (qualquer), construções OneOf/AnyOf/AllOf/NOT sem suporte
- **Lacunas de Componente**: Bloco do Adobe Sign, Assinatura Escrita, Gráfico, Opção de Imagem não disponível (disponível em Componentes do Foundation)
- **Funções personalizadas**: funções geradoras, métodos de classe assíncronos/de espera não suportados
- **Assinaturas Digitais**: não disponível nativamente (ao contrário dos Componentes do Foundation)

### Quando usar

**Recomendado para:**

- Novos projetos de desenvolvimento de formulário
- Organizações que exigem arquitetura moderna e que pode ser mantida
- Projetos que exigem publicação flexível (AEM + Edge Delivery + Headless)
- Aplicativos de front-end personalizados (React, Angular) por meio de APIs headless
- Projetos que priorizam o desempenho e a acessibilidade
- Requisitos de entrega omnicanal (Web, dispositivo móvel, quiosques)

**Não recomendado para:**

- Forms que exige integração com o Adobe Sign (use Componentes de base)
- Formulários simples em que o desempenho do Edge Delivery Services é essencial
- Formulários existentes com base em componentes de base (mantenha no Foundation a menos que você faça a migração)

## Edge Delivery Services Forms

### Definição

O Edge Delivery Services (EDS) Forms é um conjunto combinável de serviços para criar e fornecer formulários por meio do Adobe Experience Manager Edge Delivery Services. Eles permitem o desenvolvimento rápido de formulários com desempenho excepcional por meio de entrega baseada em borda, renderização no lado do cliente e vários métodos de criação.

### Arquitetura

O EDS Forms usa uma arquitetura dissociada e edge-first:

- **Fontes de Conteúdo**: Microsoft SharePoint, Google Drive (Baseado em Documento) ou Universal Editor (WYSIWYG)
- **Repositório de Códigos**: GitHub
- **Entrega de conteúdo**: CDN Edge Delivery Services
- **Renderização**: renderização do lado do cliente usando JavaScript padrão
- **Bloco de Formulário**: o Bloco de Forms Adaptável processa definições de formulário e gera HTML

### Modelo de renderização

O EDS Forms usa a renderização no lado do cliente exclusivamente:

1. Definição de formulário armazenada como JSON (convertida da planilha ou criada no Universal Editor)
2. JSON obtido da borda: `https://<branch>--<repo>--<owner>.aem.live/<form>.json`
3. Forms adaptável Bloquear JavaScript processa JSON
4. Estrutura do HTML gerada dinamicamente no navegador
5. CSS aplicado ao estilo

**Padrão de Estrutura do HTML:**

```html
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required="{Required}">
   <label for="{FieldId}" class="field-label">Label</label>
   <input type="{Type}" id="{FieldId}" name="{Name}">
   <div class="field-description" id="{FieldId}-description">Help text</div>
</div>
```

### Métodos de criação

O EDS Forms oferece suporte a duas abordagens de criação:

#### Editor universal (WYSIWYG)

- Interface visual de arrastar e soltar
- Visualização em tempo real com simulação de dispositivo
- Editor de regras avançado para lógica condicional
- Integração do modelo de dados de formulário (FDM)
- Integração de fluxos de trabalho do AEM
- Suporte a componentes personalizados
- Criação baseada em modelo

#### Criação baseada em documento

- Criação no Microsoft Excel ou no Google Sheets
- Definição de formulário baseado em planilha
- Publicação instantânea (as alterações são refletidas imediatamente)
- Adequado para formas de complexidade simples a moderada

### Opções de envio

**Serviço de Envio de Forms (FSS):**

- Enviar para o Google Sheets
- Enviar para o Microsoft Excel (OneDrive/SharePoint)
- Notificações por email

**Ações de Envio de Publicação do AEM:**

- Endpoint REST
- Serviços de email da AEM
- Modelo de dados de formulário
- Fluxo de trabalho AEM
- SharePoint/OneDrive
- Armazenamento Azure Blob
- Microsoft Power Automate
- Adobe Workfront Fusion
- Adobe Marketo Engage

### Principais recursos

| Categoria | Recursos |
|----------|-------------|
| **Componentes** | Todos os tipos de entrada HTML5, Grupos de caixas de seleção, Grupos de opções, Lista suspensa, Painéis, Seções repetíveis, Anexo de arquivo, Acordeão, Assistente, Modal |
| **Validação** | Validação em nível de campo (obrigatória, mín/máx, padrão), mensagens de validação personalizadas |
| **Regras** | Visibilidade condicional, expressões de valor, regras orientadas por eventos |
| **Integrações** | Adobe Sign, Salesforce, Microsoft Dynamics, teste A/B |
| **Segurança** | Configuração do reCAPTCHA Enterprise, hCaptcha, CORS |
| **Análises** | Adobe Experience Platform Web SDK, exibições de formulário e rastreamento de envio |

### Pré-requisitos

**Para Criação Baseada em Documento:**

- Conta do GitHub
- Conta do Google Drive ou Microsoft SharePoint
- Nó/npm para desenvolvimento local
- Projeto do AEM com bloco adaptável do Forms configurado
- Compartilhar pasta com `forms@adobe.com` (editar permissões)

**Para o Editor Universal:**

- Instância do AEM Forms as a Cloud Service
- Projeto do Edge Delivery Services configurado
- Permissões necessárias para destinos de destino

**Envio de Publicação do AEM:**

- URL da instância do AEM Cloud Service configurado
- Configuração do filtro referenciador OSGi
- Configuração do CORS para domínios de site do Edge Delivery

### Limitações  

**Criação Baseada em Documento:**

- Nomeação de planilha restrita a `helix-default` e `shared-aem`
- Mais adequado para formulários de baixa complexidade
- Recursos de regras limitados
- Nenhum fluxo de trabalho do AEM (sem o envio da publicação do AEM)
- Sem integração do modelo de dados de formulário

**Editor Universal:**

- Importações estáticas/dinâmicas não são suportadas em funções personalizadas
- Fragmentos de formulário só podem ser editados de forma independente
- Funcionalidade de incorporação de formulários no desenvolvimento

**Geral:**

- `shared-aem` folhas não devem conter PII (acessível publicamente)
- Exige a configuração do CORS para envios entre origens
- O Filtro referenciador OSGi é necessário para envios de publicação do AEM

### Quando usar

**Recomendado para:**

- Sites críticos de desempenho que exigem pontuações altas no Lighthouse
- Sites já usando o Edge Delivery Services
- Desenvolvimento e implantação rápidos de formulários
- Captura de dados de complexidade simples a moderada
- Equipes que preferem criação baseada em planilha (baseada em documento)
- Projetos que exigem tempo de entrada no mercado rápido

**Não recomendado para:**

- Forms que requer processamento extensivo no lado do servidor
- Integração profunda com sistemas herdados que não têm APIs REST
- Requisitos de formulário offline
- Organizações que exigem estruturas específicas da JavaScript (React, Angular) com controle total

## Forms adaptável baseado em componentes de base

### Definição

Os Componentes de base representam a abordagem de criação clássica do AEM Forms. Eles são os componentes originais do Adaptive Forms que estão disponíveis no AEM Forms há muitos anos. Embora ainda seja compatível, a Adobe recomenda os Componentes de base principalmente para manter os formulários existentes, em vez de criar novos.

### Arquitetura

Os componentes básicos usam a arquitetura tradicional do AEM:

- **Modelo de Conteúdo**: Componente WCM `cq:Page` com estrutura de conteúdo JCR
- **Estrutura de Raiz**: `guideContainer` (raiz) → `rootPanel` → `items` (campos de formulário)
- **Renderização**: renderização do lado do servidor com JavaScript do lado do cliente
- **Expressões SOM**: modelo de objeto de script para fazer referência a objetos de formulário

### Modelo de renderização

Os Componentes de base usam a renderização do lado do servidor:

1. Conteúdo de formulário armazenado no repositório JCR
2. Estrutura do formulário de processos de servidor do AEM
3. HTML completo renderizado e enviado para o navegador
4. O JavaScript do lado do cliente lida com interatividade e validação

### Principais recursos

| Categoria | Recursos |
|----------|-------------|
| **Componentes** | Mais de 40 componentes, incluindo todos os equivalentes dos Componentes principais, além de: Bloco do Adobe Sign, Gráfico, Assinatura Escrita, Escolha da Imagem, Etapa de Resumo, Listagem de Anexo de Arquivo |
| **Modelos de formulário** | Modelo de dados de formulário (FDM), modelos XDP/XFA, esquema XML (XSD), esquema JSON |
| **Mecanismo de regras** | Editor visual + editor de código (para grupo de formulários-usuários avançados) |
| **Assinaturas Digitais** | Integração com o Adobe Sign, assinatura escritas |
| **Enviar Ações** | Várias ações OOTB semelhantes aos Componentes principais |

### Componentes exclusivos para o Foundation

Os seguintes componentes estão **disponíveis** somente nos Componentes de Base:

- Bloco do Adobe Sign
- Gráfico
- Listagem de anexos de arquivo
- Espaço reservado para nota de rodapé
- Opção de imagem
- Rabiscar a assinatura
- Etapa de resumo
- Captcha Turnstile

### Pré-requisitos

- AEM Forms as a Cloud Service ou AEM 6.5 Forms
- Modelo de formulário adaptável (Foundation)
- Usuário no grupo `forms-users`

### Limitações  

- **Publicação**: somente AEM (sem APIs do Edge Delivery Services ou Headless)
- **Desempenho**: desempenho padrão (não otimizado para pontuações Lighthouse)
- **Arquitetura**: arquitetura herdada sem conformidade com BEM
- **Abrir Source**: não é open-source
- **Desenvolvimento futuro**: modo de manutenção; novos recursos adicionados principalmente aos Componentes principais

### Quando usar

**Recomendado para:**

- Manutenção de formulários existentes com base no Foundation
- Forms que exige a integração do Adobe Sign ou Scribble Signature
- Fluxos de trabalho dependentes de recursos de base estabelecidos
- Projetos com requisitos de publicação exclusivos do AEM
- Forms que exige componentes básicos exclusivos (gráfico, escolha da imagem)

**Não recomendado para:**

- Desenvolvimento de novos formulários (usar os Componentes principais)
- Projetos que exigem publicação no Edge Delivery Services
- APIs de formulário headless
- Implementações críticas para o desempenho
- Projetos que priorizam uma arquitetura sempre atual

## Tabela de comparação

| Parâmetro | Componentes principais | Edge Delivery Services Forms | Componentes de fundação |
|-----------|-----------------|-----------------------------|-----------------------|
| **Status** | Recomendado para novos formulários | Recomendado para sites de alto desempenho | Modo de manutenção |
| **Arquitetura** | Modular, compatível com BEM | Edge-first, dissociado | WCM tradicional |
| **Renderização** | Lado do servidor + headless | Somente no lado do cliente | Lado do servidor |
| **Publicação** | AEM + Edge Delivery + APIs headless | Somente Edge Delivery Services | Somente AEM |
| **Criação** | Editor de AEM Forms | Editor universal ou planilhas | Editor de AEM Forms |
| **Desempenho** | Bom (melhorado em relação à Foundation) | Excelente (altas pontuações no farol) | Padrão |
| **Contagem de Componentes** | 30 | 20+ (todos os tipos de entrada HTML5) | 40+ |
| **Abrir Source** | Sim (GitHub) | Sim | Não |
| **Modelo de dados do formulário** | ✅ | ✅ (somente Editor Universal) | ✅ |
| **Esquema JSON** | ✅ | Limitado | ✅ |
| **Suporte a XDP/XFA** | Limitado | ❌ | ✅ |
| **Esquema XML** | ❌ | ❌ | ✅ |
| **Mecanismo de regras** | Editor visual avançado | Avançado (Editor Universal) / Limitado (Baseado Em Documento) | Visual avançado + editor de código |
| **Assinaturas Digitais** | ❌ | ❌ | ✅ |
| **Adobe Sign** | ❌ | Via integração | ✅ (Bloco nativo) |
| **Documento de registro** | ✅ | ✅ | ✅ |
| **Opções de CAPTCHA** | reCAPTCHA, hCaptcha | reCAPTCHA Enterprise, Captcha | reCAPTCHA, hCaptcha, tartaruga |
| **Fluxo de trabalho do AEM** | ✅ | ✅ (via Publicação do AEM) | ✅ |
| **APIs headless** | ✅ (automático) | ❌ | ❌ |
| **Acessibilidade** | Compatível com WCAG | Compatível com WCAG | Básico |
| **Velocidade de implantação** | Baseado em pipeline | Instantâneo (enviar para o modo ativo) | Baseado em pipeline |
| **Estilo** | BEM CSS, Temas | CSS, temas de nível de projeto | CSS, Temas |
| **Controle de versão** | ✅ (herdado do Sites) | Baseado em Git | ✅ |
| **Localização** | Fluxo de trabalho de tradução do AEM | Fluxo de trabalho manual/AEM Sites | Fluxo de trabalho de tradução do AEM |

## Matriz de decisão

| Requisito | Abordagem recomendada |
|-------------|---------------------|
| Novo desenvolvimento de formulário | Componentes principais |
| Manutenção de formulários existentes | Componentes de base (até a migração) |
| Essencial para o desempenho (altas pontuações de Lighthouse) | Edge Delivery Services Forms |
| Entrega headless/omnicanal | Componentes principais |
| Integração do Adobe Sign | Componentes de fundação |
| Criação baseada em planilhas | Edge Delivery Services (Baseado em Documento) |
| Criação do Visual WYSIWYG com entrega de borda | Edge Delivery Services (Editor universal) |
| Integrações empresariais complexas | Componentes principais ou Componentes de base |
| Protótipo rápido | Edge Delivery Services (Baseado em Documento) |
| Suporte a modelo XFA/XDP | Componentes de fundação |
| Front-end personalizado do React/Angular | Componentes principais (APIs headless) |

## Considerações sobre migração

### Componentes de base para Componentes principais

- **Ferramenta**: Ferramentas de Modernização do AEM (Utilitário de Conversão do Forms)
- **Esforço**: moderado a alto, dependendo da complexidade do formulário
- **Considerações**:
   - As regras exigem recriação manual
   - Os componentes básicos exclusivos (Bloco do Adobe Sign, Assinatura Escrita, Gráfico) são excluídos durante a migração
   - Configurações de tradução não transferidas
   - As funções personalizadas exigem reescrita

### Tradicional para o Edge Delivery Services

- **Abordagem**: recriar formulários usando o Editor Universal ou a criação Baseada em Documento
- **Esforço**: alto para formulários complexos, baixo para formulários simples
- **Benefícios**: melhoria significativa no desempenho, experiência moderna em desenvolvimento

## Lacunas e ambiguidades na documentação

As seguintes áreas têm documentação incompleta ou ambígua:

1. **Suporte a XDP/XFA dos Componentes principais**: a documentação indica suporte &quot;limitado&quot;, mas não especifica limitações exatas
2. **Incorporação do Formulário do Edge Delivery Services**: marcado como &quot;Em breve&quot; na documentação; status atual indefinido
3. **Futuro dos Componentes de Base**: sem linha do tempo de substituição explícita; descrito como &quot;modo de manutenção&quot;
4. **Cobertura de API Headless**: paridade de recursos exata entre formulários headless e renderizados pelo servidor não documentada
5. **Referências de desempenho**: comparações de pontuações específicas do Lighthouse entre abordagens não fornecidas

## Recursos relacionados

- [Criar um formulário adaptável (componentes principais)](/help/forms/creating-adaptive-form-core-components.md)
- [Criar um formulário adaptável (componentes de base)](/help/forms/creating-adaptive-form.md)
- [Visão geral do Edge Delivery Services Forms](/help/edge/docs/forms/overview.md)
- [Introdução ao Universal Editor](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
- [Tutorial de criação baseado em documento](/help/edge/docs/forms/tutorial.md)
- [Ferramenta Utilitário de Migração](/help/forms/migration-utility-tool-for-af-core-components.md)
- [Componentes principais do AEM Forms no GitHub](https://github.com/adobe/aem-core-forms-components)
