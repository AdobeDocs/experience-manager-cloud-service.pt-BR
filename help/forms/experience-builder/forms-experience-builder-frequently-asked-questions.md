---
title: Forms Experience Builder - Perguntas frequentes
description: Encontre respostas para perguntas comuns sobre o Forms Experience Builder, incluindo configuração, uso, solução de problemas e práticas recomendadas.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---


# Forms Experience Builder - Perguntas frequentes

>[!NOTE]
>
> O Forms Experience Builder está disponível em um programa de acesso antecipado. Antes de começar, verifique se você solicitou e recebeu acesso.

Estas Perguntas frequentes abordam as perguntas mais comuns sobre o Forms Experience Builder, desde a configuração básica até os recursos avançados e a solução de problemas.

## Perguntas gerais

### O que é o Forms Experience Builder?

O Forms Experience Builder é uma ferramenta de criação de formulários habilitada por IA que permite criar formulários digitais sofisticados usando linguagem conversacional. Em vez das interfaces tradicionais de arrastar e soltar ou de codificação complexa, você simplesmente descreve o que deseja, e a IA cria o formulário para você.

### Quem pode usar o Forms Experience Builder?

O Forms Experience Builder foi projetado para:

- **Criadores de formulários** que desejam criar formulários de maneira rápida e eficiente
- **Usuários empresariais** que precisam criar formulários sem conhecimento técnico
- **Desenvolvedores** que desejam aproveitar a IA para a prototipagem rápida de formulários
- **Administradores** que precisam configurar e gerenciar fluxos de trabalho de criação de formulários

### O Forms Experience Builder está disponível para todos os clientes do AEM Forms?

O Forms Experience Builder está disponível atualmente por meio de um Programa de acesso antecipado. Entre em contato com seu representante da Adobe para solicitar acesso e saber mais sobre a disponibilidade para sua organização.

## Instalação e configuração

### Quais são os pré-requisitos para usar o Forms Experience Builder?

Antes de usar o Forms Experience Builder, verifique se você tem:

- Acesso ao Forms Experience Builder por meio do Programa de acesso antecipado
- AEM Forms as a Cloud Service com componentes principais adaptáveis do Forms
- Compreensão básica de conceitos de formulário e requisitos comerciais

Para obter requisitos detalhados de configuração técnica, consulte [Implantar e configurar o Forms Experience Builder](deploy-forms-experience-builder.md).

### Como ativar o Forms Experience Builder no meu ambiente?

A configuração do Forms Experience Builder depende da implementação do AEM Forms:

**Para Edge Delivery Services:**

- Preparar seu projeto para o Edge Delivery Services Forms
- Ativar o Forms Experience Builder no editor universal

**Para formulários baseados em Componentes Principais:**

- Verifique se os Componentes principais adaptáveis do Forms estão ativados
- Configurar o Forms Experience Builder no Editor Forms adaptável

### Posso usar o Forms Experience Builder com formulários existentes?

Sim, o Forms Experience Builder pode trabalhar com formulários existentes de várias maneiras:

- Importar e converter PDF forms existente
- Aprimorar os formulários adaptáveis existentes com recursos alimentados por IA
- Adicionar campos inteligentes às estruturas de formulário atuais

## Criação de formulários

### Como faço para criar meu primeiro formulário?

Comece com uma descrição simples do que você deseja:

    Criar um formulário de contato com campos de nome, email e mensagem

A IA gerará a estrutura básica do formulário, que você pode aprimorar com recursos adicionais, validação e estilo.

### Que tipos de formulários posso criar?

O Forms Experience Builder oferece suporte a vários tipos de formulários:

- Formulários de contato e feedback
- Formulários de registro e integração
- Formulários de pesquisa e avaliação
- Formulários de várias etapas com lógica condicional
- Forms com uploads de arquivos e validação complexa

### Posso criar formulários com várias etapas?

Sim, você pode criar formulários de várias etapas usando a linguagem natural:

    Crie um formulário progressivo com 3 etapas: informações pessoais, preferências, confirmação

A IA configurará automaticamente a estrutura do formulário com navegação entre etapas.

### Como adicionar validação a campos de formulário?

Adicionar validação usando comandos de linguagem natural:

    Tornar @email um campo obrigatório com validação de formato de email
    Adicionar validação de formato de número de telefone dos EUA à @phoneNumber
    Definir validação de idade: deve ter 18 ou mais para @dateOfBirth

## Recursos avançados

### O que são campos inteligentes aprimorados com LLM?

Os campos inteligentes aprimorados com LLM são campos de formulário inteligentes que vêm pré-preenchidos com opções relevantes das bases de conhecimento de IA. Por exemplo:

- Menus suspensos por país com todos os países do mundo
- Classificações de setor com códigos padrão
- Dados geográficos com estados, cidades e códigos postais

### Como importar documentos existentes para formulários?

Você pode importar vários tipos de documentos:

- **PDF forms**: carregar PDFs estáticos ou interativos
- **Imagens**: Carregar fotos de formulários em papel ou capturas de tela
- **Arquivos de design**: importar designs do Figma ou outros formatos de design

Use o ícone de anexo no Forms Experience Builder para fazer upload do documento e descrever seus requisitos de conversão.

### É possível integrar formulários com sistemas externos?

Sim, o Forms Experience Builder oferece suporte a várias opções de integração:

- Envios de email com modelos personalizados
- Integração da API REST com serviços externos
- Integração de armazenamento na nuvem (Azure, AWS, Google Cloud)
- Integração de fluxo de trabalho (Power Automate, fluxo de trabalho do AEM)

## Resolução de problemas

### A IA não entende minha solicitação. O que devo fazer?

Tente estas abordagens:

- Seja mais específico em sua descrição
- Dividir solicitações complexas em etapas menores
- Usar referências de campo (@fieldName) para alterações direcionadas
- Forneça exemplos claros do que você deseja

### Minha validação de formulário não está funcionando. Como corrijo isso?

Verifique estes problemas comuns:

- Verificar se os nomes de campo correspondem exatamente (diferencia maiúsculas de minúsculas)
- Verifique se a sintaxe de validação está correta
- Testar regras de validação individualmente
- Revisar mensagens de erro para problemas específicos

### A lógica condicional não está sendo acionada corretamente. O que há de errado?

Solucionar problemas de lógica condicional por:

- Verificação da referência correta aos nomes de campo
- Verificação da sintaxe e das condições da regra
- Teste com combinações de entrada diferentes
- Verificando se os tipos de campo correspondem aos requisitos da regra

### A interface não está carregando. O que devo fazer?

Experimente estas soluções:

- Atualizar o navegador e limpar o cache
- Verifique sua conexão com a Internet
- Verifique se você tem as permissões de acesso adequadas
- Contate o administrador do sistema se os problemas persistirem

## Práticas recomendadas

### Como posso criar formulários melhores com o Forms Experience Builder?

Siga estas práticas recomendadas:

- **Seja específico**: forneça descrições detalhadas sobre o que você deseja
- **Comece simples**: comece com a estrutura básica e adicione a complexidade gradualmente
- **Testar completamente**: validar toda a funcionalidade do formulário antes da implantação
- **Usar desenvolvimento incremental**: criar formulários passo a passo

### O que devo evitar ao criar formulários?

Evite estes erros comuns:

- Ser muito vago em suas descrições
- Tentando criar tudo de uma só vez
- Ignorando teste e validação
- Sem considerar a agilidade móvel

### Como garantir que meus formulários estejam acessíveis?

O Forms Experience Builder inclui recursos de acessibilidade:

- Verificação automática de conformidade com a WCAG
- Compatibilidade do leitor de tela
- Suporte à navegação por teclado
- Opções de modo de alto contraste

## Integração e implantação

### Como implantar formulários criados com o Forms Experience Builder?

A Forms criada com o Forms Experience Builder segue os processos padrão de implantação do AEM Forms:

- Publicar formulários por meio do ambiente de autor do AEM
- Configurar pontos de extremidade de envio de formulário
- Configurar fluxos de trabalho de processamento de formulário
- Formulários de teste no ambiente de produção

### Posso personalizar as respostas e o comportamento da IA?

Sim, você pode configurar vários aspectos:

- Estilo de resposta (conciso, detalhado, equilibrado)
- Preferências de idioma e terminologia
- Opções de personalização de interface
- Configurações de acessibilidade

### Como posso obter ajuda com o Forms Experience Builder?

Para obter suporte adicional:

- Verifique o [Guia de Introdução](forms-experience-builder-getting-started.md)
- Revise o [Guia de implantação e configuração](deploy-forms-experience-builder.md)
- Entre em contato com o administrador do sistema
- Entre em contato com o suporte da Adobe para resolver problemas técnicos

## Artigos relacionados

- [Visão geral do Forms Experience Builder](product-overview.md)
- [Introdução ao Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Implantar e configurar o Forms Experience Builder](deploy-forms-experience-builder.md)
- [Campos inteligentes aprimorados por LLM](forms-experience-builder-llm-smart-fields.md)
- [Importação e conversão inteligentes](intelligent-import-conversion.md)
- [Envio e integração de formulários](form-submission-integration.md)
