---
title: Implantar e configurar o Forms Experience Builder
description: Saiba como usar o Forms Experience Builder para criar e gerenciar formulários com divulgação progressiva para todos os tipos de usuários
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="Aplicável ao AEM Forms)."
exl-id: 977f227e-e941-4797-ba74-53d5b8c60ca9
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 1%

---

# Implantar e configurar o Forms Experience Builder

>[!NOTE]
>
> O Forms Experience Builder está disponível em um programa de acesso antecipado. Antes de começar, verifique se você solicitou e recebeu acesso. Para obter instruções completas, consulte as informações de [Integração](product-overview.md#onboarding).

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta documentação está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os recursos, comandos e exemplos podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa Acesso antecipado.

Este guia abrangente ajuda você a começar a criar e gerenciar formulários usando a tecnologia de IA de conversação. Seja você um iniciante procurando criar seu primeiro formulário ou um usuário avançado procurando aproveitar recursos sofisticados, você encontrará informações detalhadas e exemplos práticos para orientar sua jornada pelos recursos do Forms Experience Builder.

## Pré-requisitos e configuração

### Requisitos de acesso

Antes de usar o Forms Experience Builder, verifique se você tem:

* **Acesso ao Forms Experience Builder** - Disponível por meio do Programa de acesso antecipado
* **AEM Forms as a Cloud Service** - Ambiente de produção do autor com os Componentes principais adaptáveis do Forms
* **Noções básicas** - Familiaridade com conceitos de formulário e requisitos comerciais

### Verificar se os formulários estão habilitados

Antes de usar o Forms Experience Builder, verifique se o [AEM Forms está habilitado para o seu ambiente](/help/forms/setup-forms-cloud-service.md).

### Configurar o ambiente

Seu processo de configuração depende da implementação do AEM Forms. Escolha o caminho que corresponde ao seu projeto.

**Para Edge Delivery Services**

Se você estiver usando o Edge Delivery Services Forms e usar principalmente o Editor universal. [Prepare seu projeto para o Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md). Essa é uma configuração única para ativar o Forms Experience Builder.

**Para formulários baseados em Componentes Principais**

Se você estiver usando o Forms adaptável com base nos Componentes principais no ambiente de criação do AEM, verifique se os [Componentes principais do Forms adaptável estão habilitados](/help/forms/enable-adaptive-forms-core-components.md) para o seu ambiente.



## Início rápido

### Acessar o construtor de experiências de formulários

Você pode acessar o Forms Experience Builder a partir de três locais principais, dependendo do fluxo de trabalho e do tipo de formulário.


**1. Editor Forms adaptável (para Componentes principais)**

Você pode iniciar o construtor diretamente ao editar um formulário específico.

1. Navegue até **AEM > Forms > Forms e Documentos**.
1. [Crie um novo formulário usando um modelo de Componentes Principais](/help/forms/creating-adaptive-form-core-components.md) ou abra um existente.
1. Selecione o ícone do **Forms Experience Builder** na barra de ferramentas do editor para abrir a interface de conversação.

   ![Ícone do Assistente de IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

**1. Editor Universal (para Edge Delivery Services Forms)**

Para formulários entregues por meio do Edge Delivery Services, o construtor é integrado ao Editor universal.

1. Abra o formulário do Edge Delivery Services no Editor universal.
2. Selecione o ícone do **Forms Experience Builder** no painel direito para iniciar a interface de conversação.

### Seu primeiro formulário

| Exemplo de conversa |   |
|--------------------------------------------------------------------------------------------------------------------------------------------|---|
| **Tente esta conversa para criar um formulário de contato abrangente (com base na demonstração do Summit):**<br><br>**Você:** &quot;Crie um formulário de contato para capturar informações pessoais, incluindo nome completo, endereço de email, número de telefone, nome da empresa, cargo e um campo de mensagem para consultas&quot;<br><br>**IA:** Selecione um modelo<br>    Uma lista suspensa para selecionar um modelo <br><br>**IA:** Selecione um tema<br>    Uma lista suspensa para selecionar um tema <br><br>**IA:** Criar formulário | ![Seu Primeiro Formulário](/help/edge/docs/forms/assets/create-form.png) |
| <br>**IA:** Abrir formulário criado | </br> O formulário é criado e aberto no editor |


### Comandos essenciais

| Símbolo | Propósito | Exemplo de uso |
|--------|---------|---------------|
| `/` | Ações rápidas e atalhos | `/create-form contact form`, `/help validation rules`, `/update-layout wizard` |
| `@` | Fazer referência a campos de formulário existentes | `@email`, `@firstName`, `Make @phoneNumber required` |
| Texto sem formatação | Conversação natural | &quot;Adicionar um campo de número de telefone obrigatório&quot;, &quot;Criar validação para email&quot; |

**Exemplos de Comandos Específicos:**

* `/create-form customer survey` - Cria um novo formulário de pesquisa de cliente
* `/add-field @email validation` - Adiciona validação ao campo de email existente
* `/create-rule show @spouse if @maritalStatus equals married` - Cria uma lógica condicional
* `/configure-submit to email support@company.com` - Configura o envio de email
* `/help multi-step forms` - Obtém ajuda sobre a criação de formulário em várias etapas

### Dicas para se dar bem

* **Seja específico**: &quot;Adicionar um campo de email necessário com validação&quot; funciona melhor do que &quot;adicionar email&quot;
* **Fazer referência a campos existentes**: usar `@fieldName` ao modificar formulários
* **Solicitar ajuda**: Digite `/help` seguido da sua pergunta
* **Iterar**: fazer uma alteração de cada vez para obter melhores resultados


## Maneiras de começar a criar um formulário

### Iniciar com prompts de idioma natural

Descreva os requisitos de formulário em linguagem natural, e o Forms Experience Builder gera a estrutura completa do formulário:

**Exemplos:**

* &quot;Crie um formulário de solicitação de empréstimo com informações pessoais, detalhes financeiros e uploads de documentos&quot;
* &quot;Crie um formulário de feedback do cliente com classificações, comentários e categorias do produto&quot;
* &quot;Preciso de um formulário de inscrição em várias etapas para uma conferência com processamento de pagamento&quot;


### Principais interações

#### Adição de elementos de formulário

**Adições básicas:**

    👤 Você: &quot;Adicionar uma seção para informações pessoais&quot;
    👤 Você: &quot;Incluir um carregamento de arquivo para retomada&quot;
    👤 Você: &quot;Adicionar uma lista suspensa para seleção de país&quot;

**Especificações detalhadas:**

    👤 Você: &quot;Adicionar um painel de informações pessoais com campos para nome completo, data de nascimento, número de telefone e endereço de email&quot;
    👤 Você: &quot;Incluir um componente de carregamento de arquivo seguro para documentos, limitado a arquivos PDF com menos de 5 MB&quot;
    👤 Você: &quot;Adicionar uma lista suspensa de país com opções para EUA, Canadá, Reino Unido e Alemanha&quot;

#### Criar comportamento dinâmico

**Lógica simples:**

    👤 Você: &quot;Mostrar campos adicionais quando &#39;Outro&#39; for selecionado&quot;
    🤖 IA: &quot;Criou uma regra condicional que mostra campos adicionais quando &#39;Outro&#39; for escolhido&quot;
    
    👤 Você: &quot;Tornar o campo de email necessário&quot;
    🤖 IA: &quot;Atualizou o campo de email a ser exigido com validação&quot;
    
    👤 Você: &quot;Calcular o total automaticamente&quot;
    🤖 IA: &quot;Adicionou lógica de cálculo para calcular totais automaticamente&quot;

**Regras de negócio complexas:**

    👤 Você: &quot;Mostrar os campos de informações do cônjuge somente quando o estado civil estiver definido como &#39;Casado&#39;&quot;
    🤖 IA: &quot;Criou uma regra condicional que exibe os campos do cônjuge com base no estado civil&quot;
    
    👤 Você: &quot;Calcular o custo total multiplicando quantidade e preço e adicionar imposto de 10%&quot;
    🤖 IA: &quot;Adição da lógica de cálculo com cálculo de quantidade, preço e imposto&quot;
    
    👤 Você: &quot;Habilitar o botão Enviar somente quando todos os campos obrigatórios estiverem concluídos e os termos forem aceitos&quot;
    🤖 IA: &quot;Lógica de validação criada que habilita o envio somente quando todas as condições forem atendidas&quot;

#### Layout e design do formulário

**Alterações de layout:**

    👤 Você: &quot;Transformar em formulário de várias etapas&quot;
    🤖 AI: &quot;Converter formulário em layout progressivo com navegação&quot;
    
    👤 Você: &quot;Organizar campos em duas colunas&quot;
    🤖 AI: &quot;Atualizar o layout para exibir campos em uma organização de duas colunas&quot;
    
    👤 Você: &quot;Converter em layout de acordeão&quot;
    🤖 AI: &quot;Transformar o formulário para usar seções de estilo acordeão&quot;

**Melhorias de design:**

    👤 Você: &quot;Criar um formulário de estilo assistente com 3 etapas: informações pessoais, preferências e revisão&quot;
    🤖 IA: &quot;Criar um formulário de assistente com três etapas e navegação distintas&quot;
    
    👤 Você: &quot;Organizar os campos de endereço em um layout compacto de duas colunas&quot;
    🤖 IA: &quot;Organizar campos de endereço em um formato compacto de duas colunas&quot;
    
    👤 Você: &quot;Atualizar o layout para corresponder ao wireframe anexado&quot;
    🤖 IA: &quot;Modificar o layout para corresponder à referência de design fornecida&quot;

### Enviar configuração

O Forms Experience Builder pode configurar vários endpoints de envio para conectar seus formulários a sistemas e serviços externos:

| Enviar Tipo de Ação | Comando de configuração | Caso de uso |
|------------------|---------------|----------|
| **Email** | &quot;Enviar formulário para email&quot; | Notificações e confirmações para envios de formulários |
| **REST API** | &quot;Enviar para endpoint REST&quot; | Aplicativos personalizados e sistemas de terceiros |
| **Armazenamento na nuvem** | &quot;Salvar no Azure/SharePoint&quot; | Armazenamento de documentos e gerenciamento de arquivos |
| **Fluxo de trabalho** | &quot;Conexão com o Power Automate&quot; | Automação e aprovações de processos de negócios |
| **Marketing** | &quot;Integrar ao Marketo&quot; | Gerenciamento de clientes potenciais e automação de marketing |

**Exemplos avançados de configuração de envio:**

    👤 Você: &quot;Enviar envios de formulários para hr@company.com e criar um caso em nosso sistema CRM&quot;
    🤖 IA: &quot;Envio de email configurado e ação de envio do CRM&quot;
    
    👤 Você: &quot;Enviar dados para nosso ponto de extremidade da API REST e acionar o novo fluxo de trabalho do cliente&quot;
    🤖 IA: &quot;Configurar o envio da API REST com acionadores de fluxo de trabalho&quot;
    
    👤 Você: &quot;Enviar respostas por email para a equipe de vendas e adicionar o cliente potencial à nossa plataforma de automação de marketing&quot;
    🤖 IA: &quot;Envio multicanal configurado com automação de email e marketing&quot;





## Operações avançadas de formulários


### Criação de regra complexa

Crie validação sofisticada e lógica de negócios que responda às interações do usuário e garanta a integridade dos dados:

    👤 Você: &quot;Mostrar a seção de endereço somente se o usuário selecionar &#39;Enviar para um endereço diferente&#39;&quot;
    🤖 IA: &quot;Criou uma regra condicional que mostra/oculta o painel de endereços com base na seleção da caixa de seleção&quot;

### Criação de formulário em várias etapas

    👤 Você: &quot;Criar um formulário progressivo com 3 etapas: informações pessoais, preferências, confirmação&quot;
    🤖 IA: &quot;Criado um formulário progressivo com navegação entre etapas e validação em cada estágio&quot;

### Tipos de campo avançados

* Upload de arquivo com restrições de validação e tamanho para gerenciamento de documentos
* Seletores de data com restrições e regras de negócios para agendamento
* Menus suspensos com opções dinâmicas que mudam com base nas seleções do usuário
* Botões de opção com lógica condicional para árvores de decisão complexas


### PDF para conversão de formulários

    👤 Você: &quot;Converter este PDF em um formulário interativo&quot;
    🤖 IA: &quot;Analisou o PDF e criou um formulário com tipos de campo e validação apropriados&quot;





## Ajuda e aprendizado do produto

O Forms Experience Builder também pode ensiná-lo sobre os recursos do AEM Forms:

### Faça perguntas como:

* &quot;Como criar um formulário de várias etapas?&quot;
* &quot;Qual é a diferença entre painéis e seções?&quot;
* &quot;Como configurar notificações por email?&quot;
* &quot;Quais são as práticas recomendadas para formulários móveis?&quot;
* &quot;Como aplicar temas às minhas formas?&quot;

### Obter ajuda sobre:

* Conceitos e terminologia do AEM Forms
* Instruções passo a passo para recursos complexos
* Práticas recomendadas
* Solução de problemas comuns


Para obter suporte adicional, consulte a [Biblioteca de Prompts do Forms Experience Builder](/help/forms/experience-builder/forms-experience-builder-prompt-examples-library.md) principal ou entre em contato com o administrador do sistema para obter assistência técnica.
