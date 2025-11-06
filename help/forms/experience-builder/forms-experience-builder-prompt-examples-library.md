---
title: Forms Experience Builder - Biblioteca de prompts
description: Coleção de padrões de prompt comprovados e exemplos para criar formulários com assistência de IA na interface do usuário do Forms Management, no Editor adaptável do Forms e no Editor universal.
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: 48eb137c-fe12-4e4f-b845-3321ca8b6075
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2193'
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

Essa biblioteca fornece padrões de prompt reutilizáveis para cenários comuns de criação de formulários. Para obter práticas recomendadas abrangentes, consulte o [Guia de Introdução do Forms Experience Builder](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

### Dicas rápidas para esta biblioteca

- **Comece com exemplos** - Use os prompts fornecidos como modelos e adapte-se às suas necessidades
- **Dois métodos de criação** - Escolher as abordagens Criar do Zero ou Importar e Converter
- **Seja específico** - Adicione seus próprios detalhes a exemplos genéricos
- **Testar completamente** - Sempre validar os resultados em seu ambiente específico

### Modelos e estilos de marca

**Prepare os ativos da marca com antecedência para a criação consistente do formulário:**

- **Modelos de marca** - Prepare modelos de formulário padronizados com as cores, fontes e padrões de layout da sua organização
- **Diretrizes de estilo** - Defina um estilo de campo consistente, designs de botão e padrões de espaçamento que o Forms Experience Builder pode aplicar
- **Biblioteca de componentes** - Trabalhe com sua equipe de desenvolvimento para preparar componentes de formulário reutilizáveis que correspondam à identidade da sua marca
- **Visual Assets** - Prepare logotipos, ícones e elementos de plano de fundo para a integração de formulários


## Exemplos de desenvolvimento incremental

Esses exemplos mostram como criar formulários passo a passo, começando simples e adicionando complexidade gradualmente:

### Exemplo 1: Criando um Formulário de Contato Incrementalmente

**Etapa 1 - Início Simples:**

    Criar um formulário básico de contato com campos de nome, email e mensagem

**Etapa 2 - Adicionar validação:**

    Tornar @name e @email campos obrigatórios com validação adequada

**Etapa 3 - Aprimorar a Experiência do Usuário:**

    Adicionar texto de espaço reservado: @name &quot;Seu nome completo&quot;, @email &quot;your.email@company.com&quot;, @message &quot;Diga-nos como podemos ajudar&quot;

**Etapa 4 - Adicionar Recursos Avançados:**

    Adicione um tipo de consulta suspensa com opções: &quot;Pergunta Geral&quot;, &quot;Solicitação de Suporte&quot;, &quot;Consulta de Vendas&quot;, &quot;Parceria&quot;

**Etapa 5 - Implementar Lógica Condicional:**

    /create-rule mostrar lista suspensa @urgencyLevel (baixo, Medium, alto) somente quando @inquiryType for igual a &quot;Solicitação de suporte&quot;

### Exemplo 2: Criação incremental de um formulário de registro

**Etapa 1 - Estrutura Básica:**

    Criar um formulário de registro do usuário com o painel de informações pessoais

**Etapa 2 - Adicionar Campos Obrigatórios:**

    Adicionar campos para @firstName, @lastName, @email, @phoneNumber com validação apropriada

**Etapa 3 - Adicionar Lógica Comercial:**

    Criar uma regra: se @age estiver abaixo de 18, mostrar a seção de informações pai/responsável

**Etapa 4 - Aprimorar com Preferências:**

    Adicionar um painel de preferências com @newsletterSubscription, @marketingConsent, @termsAccepted

**Etapa 5 - Adicionar Carregamento de Arquivo:**

    Incluir um campo de carregamento de arquivo para @profilePicture com limite de tamanho de 5 MB

## Criação e gerenciamento de formulários

**Quando usar:** Quando precisar criar novos formulários ou modificar formulários existentes.

**Como usar:** Escolha uma das duas abordagens: Criar do Zero ou Importar e Converter (consulte o [Guia de Introdução](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

**Exemplo de Prompt - Criação de Formulário Simples:**

    Crie um formulário de feedback de cliente com:
    - Classificação do produto (1-5 estrelas)
    - Campo Comentário para feedback detalhado
    - Email de cliente (opcional)
    - Enviar notificação por email

**Exemplo de Prompt - Criação de Formulário Complexo:**

    Crie um formulário abrangente de integração de funcionários com:
    
    **Seção de Informações Pessoais:**
    - Nome completo (primeiro, meio, último)
    - Data de nascimento com validação de idade
    - Informações de contato (email, telefone, endereço)
    - Detalhes do contato de emergência
    
    **Detalhes do emprego:**
    - Seleção de cargo e departamento
    - Data de início com validação de dia útil
    - Informações de salário com aviso de confidencialidade
    - Estrutura de relatório
    
    **Carregamento de documento:**
    - Retomar/Carregamento de CV (PDF, DOC, DOCX)
    - Documentos de verificação de ID
    - Formulários fiscais e informações bancárias
    - Contrato de trabalho assinado
    
    **Preferências:**
    - Seleção de benefícios com calculadora de custos
    - Preferências de cronograma de trabalho
    - Requisitos de treinamento
    - Necessidades de equipamentos
    
    **Regras de validação:**
    - Validação de formato de email
    - Validação de formato de número de telefone
    - Idade deve ter 18 anos ou mais 
    - Todos os documentos necessários ser carregado
    - Os termos e as condições devem ser aceitos
    
    **Enviar Ações:**
    - Enviar email de confirmação para o novo funcionário
    - Notificar o departamento de RH
    - Criar registro de funcionário no sistema de RH
    - Agendar reunião de orientação

**Prompts de Gerenciamento de Formulário:**

    Importe este formulário de aplicativo do PDF e converta-o em um formulário adaptável com validação aprimorada
    
    Atualize o formulário de contato existente para incluir identificadores de redes sociais e o método de contato preferido
    
    Reorganize o formulário de registro em um assistente de 3 etapas: informações pessoais, preferências, confirmação

## Gerenciamento e configuração de campo

**Quando usar:** Quando precisar adicionar, modificar ou configurar campos de formulário.

**Como usar:** seja específico quanto aos tipos de campo, regras de validação e requisitos de experiência do usuário.

**Exemplo de Prompt - Adição Básica de Campo:**

    Adicione um campo de entrada de texto para &quot;Nome da Empresa&quot; com o espaço reservado &quot;Insira o nome da sua empresa&quot;

**Exemplo de Prompt - Configuração Avançada de Campo:**

    Adicione uma seção de endereço abrangente com:
    
    **Endereço:**
    - Linha de endereço 1 (obrigatório, máx. 100 caracteres)
    - Linha de endereço 2 (opcional, máx. 100 caracteres)
    - Cidade (obrigatório, lista suspensa com cidades comuns)
    - Estado/Província (obrigatório, lista suspensa)
    - Código postal (obrigatório, validação de formato)
    - País (obrigatório, padrão para &quot;Estados Unidos&quot;)
    
    **Regras de validação:**
    - Código postal deve corresponder ao estado seleção
    - A linha de endereço 1 não pode ficar vazia
    - A cidade deve ser uma cidade válida para o estado selecionado
    
    **Experiência do usuário:**
    - Preenchimento automático para campos de endereço
    - Limpar rótulos e texto de ajuda
    - Campos de entrada para dispositivos móveis
    - Conformidade com acessibilidade

**Prompts de Configuração de Campo:**

    Tornar o campo @email obrigatório com validação em tempo real e mensagem de erro personalizada
    
    Adicionar uma lista suspensa para @country com opções para EUA, Canadá, Reino Unido, Alemanha, França e &quot;Outros&quot;
    
    Configurar o campo @phoneNumber com formato (XXX) XXX-XXXX e validação
    
    Adicionar um campo de carregamento de arquivo para @resume com restrições de PDF e DOC, máx. 5MB

## Campos inteligentes aprimorados com LLM

**Quando usar:** quando precisar de campos com opções pré-preenchidas que usam a base de dados de conhecimento da IA.

**Como usar:** solicite campos que exigem conjuntos de dados abrangentes; a IA pode preencher opções automaticamente usando seu conhecimento integrado.

### Campos geográficos e de localização

**Aeroportos e Transporte:**

    Adicionar uma lista suspensa para aeroportos de partida com todos os principais aeroportos internacionais
    Adicionar campo de aeroporto de chegada com códigos IATA e nomes completos
    Criar um campo para o aeroporto mais próximo da localização do usuário
    Adicionar uma seleção de estações de trem para cidades europeias

**Regiões Administrativas:**

    Adicione uma lista completa de estados dos EUA com abreviações
    Crie uma lista suspensa de países com códigos ISO e nomes completos
    Adicione um campo para as principais cidades do mundo com fusos horários
    Inclua uma lista suspensa de províncias e territórios canadenses
    Adicione um campo para condados e áreas postais do Reino Unido

### Dados de negócios e da indústria

**Classificações de Empresa:**

    Adicionar um campo para classificação setorial com códigos NAICS
    Criar uma lista suspensa de tipos de entidades comerciais (LLC, Corporation, Parceria etc.)
    Adicionar um campo para categorias de tamanho de empresa (inicialização, SME, empresa)
    Incluir seleção de departamento para organizações grandes
    Adicionar um campo para tipos de serviço profissional

**Classificações profissionais:**

    Adicione um campo para cargos com funções industriais comuns
    Crie uma lista suspensa de certificações profissionais por campo
    Inclua níveis educacionais com tipos de diploma
    Adicione um campo para anos de intervalos de experiência
    Crie uma seleção para linguagens de programação e estruturas

### Normas e Normas

**Finanças e assuntos legais:**

    Adicionar um campo para códigos de moeda com símbolos e taxas de câmbio
    Criar uma lista suspensa de tipos de ID de imposto por país
    Incluir um campo para tipos de documentos legais
    Adicionar opções de método de pagamento com recursos de segurança
    Criar uma seleção para instituições bancárias por país

**Padrões técnicos:**

    Adicionar uma lista suspensa de tipos de formato de arquivo com extensões
    Incluir opções de protocolo de rede
    Adicionar um campo para tipos e versões de banco de dados
    Criar uma seleção para métodos de autenticação de API

### Assistência médica e médica

**Classificações Médicas:**

    Adicionar um campo para especialidades médicas
    Criar uma lista suspensa de medicamentos comuns com nomes genéricos
    Incluir um campo para tipos de provedores de seguro
    Adicionar uma seleção para relações de contato de emergência médica
    Criar um campo para restrições dietéticas e alergias

### Inteligência de Tempo e Calendário

**Campos de Data e Hora:**

    Adicionar um campo para horário comercial com tratamento de fuso horário
    Criar uma lista suspensa de feriados por país
    Incluir opções sazonais com intervalos de datas
    Adicionar um campo para reserva de sala de conferência com disponibilidade
    Criar uma seleção para padrões de reunião recorrentes

### Categorias de produto e serviço

**Classificações de comércio eletrônico:**

    Adicionar um campo para categorias de produto com subcategorias
    Criar uma lista suspensa de métodos de envio com estimativas de entrega
    Incluir um campo para opções de política de devolução
    Adicionar uma seleção para níveis de prioridade de cliente
    Criar um campo para ciclos de cobrança de assinatura

**Exemplo de Solicitações de Campo Inteligente:**

    &quot;Adicionar um campo de aeroporto de partida com todos os principais aeroportos do mundo inteiro, incluindo códigos IATA e nomes de cidades&quot;
    
    &quot;Criar um campo de setor abrangente usando a classificação NAICS padrão com subcategorias de tecnologia&quot;
    
    &quot;Incluir uma lista suspensa de certificação profissional que se adapta com base no campo de trabalho selecionado&quot;
    
    &quot;Adicionar um campo de número de telefone internacional que formata com base no país selecionado&quot;
    
    &quot;Criar um campo de seleção de universidade com as principais instituições organizadas por país e classificação&quot;

## Criação de regras e lógica de negócios

**Quando usar:** Quando precisar implementar lógica condicional, regras de validação ou processos comerciais.

**Como usar:** descreva claramente a lógica comercial, especificando condições e ações.

**Exemplo de Prompt - Lógica Condicional Simples:**

    Crie uma regra que mostre o painel @spouseInformation somente quando @maritalStatus for igual a &quot;Casado&quot;

**Exemplo de Prompt - Regras de Negócios Complexas:**

    Implementar validação abrangente de aplicativo de empréstimo:
    
    **Validação de Renda:**
    - Se @annualIncome for menor que 30000:
    - Mostrar mensagem de aviso: &quot;A renda pode ser insuficiente para o valor do empréstimo solicitado&quot;
    - Exigir documentação de renda adicional
    - Exibir mensagem: &quot;Documentação adicional pode ser necessária&quot;
    - Se @annualIncome for maior que 100000:
    - Mostrar opções de serviços premium
    - Habilitar caixa de seleção de processamento de prioridade
    
    **Validação Baseada em Idade:*
    - Se @age estiver abaixo de 18:
    - Mostrar seção de informações de pai/responsável
    - Tornar o carregamento de assinatura pai obrigatório
    - Alterar texto do botão de envio para &quot;Enviar para Revisão&quot;
    - Se @age tiver 65 anos ou mais:
    - Mostrar opções de desconto sênior
    - Adicionar seção de preferências de acessibilidade

**Prompts Específicos de Regra:**

    Crie uma **regra de visibilidade** que mostre o painel @spouseInformation somente quando @maritalStatus for igual a &quot;Casado&quot; ou &quot;Parceria Doméstica&quot;
    
    Adicione **divulgação progressiva** quando aparecerem perguntas adicionais com base em respostas anteriores. Comece com informações básicas e, em seguida, mostre acompanhamentos relevantes
    
    Implementar **padrões inteligentes** onde a seleção @country define automaticamente campos relacionados. Permitir substituição manual

## Integração e envio de dados

**Quando usar:** Quando precisar conectar formulários a sistemas de back-end, bancos de dados ou serviços externos.

**Como usar:** comece com a configuração básica de envio e acrescente integrações adicionais de forma incremental. Especifique o tipo de integração, os requisitos de formato de dados e as preferências de tratamento de erros.

**Exemplo de Prompt - Iniciar com Envio Básico:**

    Configurar envio de formulário básico para @applicationForm:
    
    **Envio primário:**
    - Enviar dados de formulário para o ponto de extremidade REST: `/api/v1/applications`
    - Formatar dados como JSON
    - Mostrar mensagem de sucesso: &quot;Aplicativo enviado com êxito&quot;
    - Mostrar mensagem de erro se o envio falhar: &quot;Falha no envio, tente novamente&quot;

**Em Seguida, Adicionar Ações Secundárias Incrementalmente:**

    Adicionar notificação por email a @applicationForm: enviar email de confirmação para o endereço @email com o número de referência do aplicativo
    
    Adicionar integração do CRM a @applicationForm: criar novo registro de cliente potencial com @firstName, @lastName, @email e definir o Status como &quot;Novo Aplicativo&quot;

**Exemplo de Prompt - Envio Multicanal Padrão:**

    Configurar o envio do formulário com vários destinos de dados:
    
    **Envio principal:**
    - Enviar dados do formulário para o ponto de extremidade REST: `/api/v1/applications`
    - Incluir cabeçalho de autenticação com chave de API
    - Formatar dados como JSON com objetos aninhados para endereço e emprego
    - Lidar com a resposta de sucesso (201) ao mostrar a mensagem de agradecimento
    
    **Ações secundárias:**
    - Enviar email de notificação ao candidato em @email address
    - Copiar dados do aplicativo para o sistema de rastreamento
    - Acionar fluxo de trabalho para aprovação processo
    - Criar registro no CRM com status de cliente potencial &quot;Novo Aplicativo&quot;
    
    **Tratamento de Erros:**
    - Se o envio principal falhar, salvar dados localmente e tentar novamente
    - Mostrar mensagem de erro amigável: &quot;Envio temporariamente indisponível&quot;
    - Fornecer opção para baixar dados de formulário como backup
    - Enviar email de alerta para a equipe administrativa sobre envio com falha
    
    **Fluxo de Sucesso:**
    - Redirecionar para página de confirmação com número de referência de aplicativo
    - Enviar email de confirmação com o próximo etapas
    - Exibir linha do tempo de processamento estimada

**Prompts Específicos de Integração:**

    Conecte este formulário ao **sistema do CRM** para criar novos clientes potenciais. Mapeie @firstName para FirstName, @email para Email, defina LeadSource como &quot;Formulário da Web&quot; e Status como &quot;Novo&quot;
    
    Configure **acionador de fluxo de trabalho** quando o formulário for enviado. Passar todos os dados de formulário e acionar o fluxo de trabalho de aprovação com notificação do gerente
    
    Configurar **integração do banco de dados** para salvar os envios de formulário como registros. Criar nova pasta para cada envio com documentos carregados



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

Para obter práticas recomendadas e diretrizes de validação abrangentes, consulte o [Guia de Introdução do Forms Experience Builder](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

*Esta biblioteca de prompts é atualizada continuamente com base no feedback do usuário e nos novos recursos do Forms Experience Builder. Para obter os recursos e exemplos mais recentes, verifique a [documentação do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=pt-BR).*
