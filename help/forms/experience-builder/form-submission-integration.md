---
title: Envio e integração de formulários
description: Saiba como configurar envios de formulários e integrar formulários do Forms Experience Builder a sistemas externos, APIs e fluxos de trabalho de negócios.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: c772556b-dab6-4fa8-b728-1fe52c6596a4
source-git-commit: 1d378e6c8ac714779e77314d3457a14d40cd222f
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---

# Envio e integração de formulários

>[!NOTE]
>
> O Forms Experience Builder está disponível em um programa de acesso antecipado. Antes de começar, verifique se você solicitou e recebeu acesso.

O Forms Experience Builder fornece recursos avançados de integração para conectar seus formulários a sistemas externos, APIs e fluxos de trabalho de negócios. Este guia aborda como configurar envios de formulários e configurar vários cenários de integração.

## Opções de configuração de envio

### Envios por email

Configurar formulários para enviar envios por email:

**Configuração básica de email:**

- Definir endereços de email de destinatários
- Configurar modelos de email
- Adicionar recipients de CC e CCO
- Configurar notificações por email

**Recursos de email avançados:**

- Seleção dinâmica de recipient
- Modelos de email com dados de formulário
- Manuseio de anexo
- Confirmação de entrega de email

### Integração da REST API

Conectar formulários a APIs e serviços externos:

**Configuração de ponto de extremidade de API:**

- Definir URLs da API REST
- Configurar métodos de autenticação
- Definir cabeçalhos e parâmetros de solicitação
- Lidar com dados de resposta

**Mapeamento de dados:**

- Mapear campos de formulário para parâmetros de API
- Transformar formatos de dados
- Manipular estruturas JSON aninhadas
- Gerenciar respostas de erro

### Integração de armazenamento na nuvem

Armazenar envios de formulários nos serviços de armazenamento em nuvem:

**Plataformas com suporte:**

- Armazenamento de blobs do Microsoft Azure
- Amazon S3
- Armazenamento em nuvem Google
- SharePoint Online

**Opções de configuração:**

- Definir credenciais de armazenamento
- Configurar estruturas de pastas
- Definir convenções de nomenclatura de arquivo
- Gerenciar permissões de acesso

### Integração do fluxo de trabalho

Conectar formulários aos fluxos de trabalho do processo empresarial:

**Microsoft Power Automate:**

- Acionar workflows no envio de formulário
- Passar dados do formulário para etapas do fluxo de trabalho
- Lidar com respostas de fluxo de trabalho
- Gerenciar processos de aprovação

**Fluxo de Trabalho do Adobe:**

- Integração com o fluxo de trabalho do AEM
- Configurar cadeias de aprovação
- Configurar etapas de notificação
- Gerenciar processamento de documentos

## Configuração de envios de formulários

### Etapa 1: acessar configuração de envio

1. Abra o formulário no Forms Experience Builder
2. Navegue até as configurações de envio
3. Selecione &quot;Configurar envio de formulário&quot;
4. Escolha seu tipo de integração

### Etapa 2: configurar envios de email

**Configuração básica de email:**

    Configurar o envio de email para hr@company.com com:
    - Assunto: &quot;Inscrição de Novo Funcionário&quot;
    - Incluir dados de formulário no corpo do email
    - Enviar confirmação ao candidato

**Configuração avançada de email:**

    Configurar o roteamento de email dinâmico:
    - Se o departamento for igual a &quot;TI&quot;, enviar para it-hr@company.com
    - Se o departamento for igual a &quot;Vendas&quot;, enviar para sales-hr@company.com
    - Padrão para hr@company.com

### Etapa 3: configurar a integração de API

**Configuração da API REST:**

    Enviar dados de formulário para o ponto de extremidade REST:
    - URL: https://api.company.com/forms/submit
    - Método: POST
    - Autenticação: Token de portador
    - Tipo de Conteúdo: application/json

**Exemplo de mapeamento de dados:**

    Mapear campos de formulário para a API:
    - firstName -> user.first_name
    - lastName -> user.last_name
    - email -> user.email_address
    - department -> user.department_id

### Etapa 4: configurar o armazenamento na nuvem

**Configuração do Armazenamento Azure Blob:**

    Armazenar envios de formulários no Azure:
    - Contêiner: formulários-envios
    - Pasta: /{year}/{month}/{day}/
    - Formato de arquivo: JSON com anexos
    - Nível de acesso: Privado

## Exemplos de integração

### Formulário de feedback do cliente

**Configuração de envio:**

- Notificação por email para a equipe de suporte
- Armazenar dados no sistema CRM por meio da API
- Criar tíquete de suporte automaticamente
- Enviar email de confirmação para o cliente

**Implementação:**
Envie o formulário de feedback do cliente para:
1. Enviar email para <support@company.com> com detalhes do formulário
2. POST na API do CRM para criar registro de cliente
3. Acionar o fluxo de trabalho de criação de tíquete de suporte
4. Envie um e-mail de agradecimento ao cliente

### Formulário de integração de funcionários

**Configuração de envio:**

- Enviar email para a equipe de RH com novas informações de contratação
- Armazenar documentos no SharePoint
- Acionar o fluxo de trabalho de integração
- Criar contas de usuário em vários sistemas

**Implementação:**
Processar integração de funcionários:
1. Email <hr@company.com> com detalhes do funcionário
2. Fazer upload de documentos para a pasta de funcionários da SharePoint
3. Iniciar o fluxo de trabalho de integração no Power Automate
4. Criar contas no sistema de RH, email e outras ferramentas

### Formulário de geração de clientes potenciais

**Configuração de envio:**

- Armazenar dados de clientes potenciais na plataforma de automação de marketing
- Enviar notificação para a equipe de vendas
- Adicionar cliente em potencial ao sistema CRM
- Acionar sequência de email de acompanhamento

**Implementação:**
Geração de leads de processo:
1. PUBLICAR dados de clientes potenciais na API do Marketo
2. Criar registro de cliente potencial no Salesforce
3. Enviar email à equipe de vendas com detalhes do cliente potencial
4. Iniciar sequência automatizada de criação de email

## Cenários de integração avançada

### Processamento de formulário em várias etapas

**Integração de fluxo de trabalho complexo:**

- Validar dados de formulário em relação a sistemas externos
- Processar pagamentos por meio de gateways de pagamento
- Gerar documentos e contratos
- Enviar notificações a vários participantes

### Validação de dados em tempo real

**Validação baseada em API:**

- Validar endereços de email em relação ao diretório da empresa
- Verificar a disponibilidade do produto no sistema de estoque
- Verificar informações do cliente no CRM
- Validar informações de pagamento

### Roteamento de envio condicional

**Roteamento dinâmico baseado em dados de formulário:**

- Roteamento para diferentes departamentos com base no tipo de consulta
- Enviar para diferentes sistemas com base na camada do cliente
- Processar de forma diferente com base no status de conclusão do formulário
- Lidar com diferentes regras de negócios por região

## Segurança e conformidade

### Proteção de dados

**Criptografia e segurança:**

- Criptografar dados confidenciais em trânsito
- Tokens e credenciais de API seguras
- Implementar controles de acesso adequados
- Seguir políticas de retenção de dados

### Requisitos de conformidade

**GDPR e privacidade:**

- Implementar o gerenciamento de consentimento
- Fornecer recursos de exportação de dados
- Habilitar solicitações de exclusão de dados
- Manter trilhas de auditoria

**Padrões do setor:**

- Conformidade com a HIPAA para formulários de saúde
- PCI DSS para processamento de pagamento
- Conformidade com SOX para formulários financeiros
- Normas específicas do setor

## Teste e validação

### Teste de envio

**Cenários de teste:**

- Verificar entrega e formatação de email
- Testar a conectividade da API e o mapeamento de dados
- Validar uploads de armazenamento na nuvem
- Verificar a funcionalidade do acionador de fluxo de trabalho

**Tratamento de erros:**

- Testar cenários de falha de rede
- Exibição da mensagem de erro de validação
- Verificar mecanismos de repetição
- Verificar opções de fallback

### Otimização do desempenho

**Estratégias de otimização:**

- Implementar processamento assíncrono
- Usar operações em lote para dados em massa
- Otimizar a frequência de chamada da API
- Armazenar dados acessados com frequência em cache

## Solução de problemas de integração

### Problemas comuns

**Problemas de entrega de email:**

- Verificar a configuração do servidor SMTP
- Verificar endereços de email de destinatários
- Revisar configurações de filtro de spam
- Testar formatação do modelo de email

**Problemas de integração de API:**

- Verificar URLs de ponto de extremidade de API
- Verificar credenciais de autenticação
- Validar formato de solicitação e cabeçalhos
- Revisar manipulação de resposta da API

**Problemas de integração de armazenamento:**

- Confirmar credenciais de armazenamento
- Verificar permissões da pasta
- Verificar limites de upload de arquivo
- Testar conectividade de rede

### Obtendo ajuda

Para problemas de integração:

- Verifique as [Perguntas frequentes sobre o Forms Experience Builder](forms-experience-builder-frequently-asked-questions.md)
- Revise o [Guia de Introdução](forms-experience-builder-getting-started.md)
- Entre em contato com o administrador do sistema para obter assistência técnica
- Consulte a documentação da API para serviços externos

<!-- 
## Related articles

- [Forms Experience Builder Overview](product-overview.md)
- [Getting started with Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Deploy and configure Forms Experience Builder](deploy-forms-experience-builder.md)
- [Intelligent import and conversion](intelligent-import-conversion.md)
- [Frequently asked questions](forms-experience-builder-frequently-asked-questions.md)

-->


