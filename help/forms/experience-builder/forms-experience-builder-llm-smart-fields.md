---
title: Campos inteligentes aprimorados por LLM no Forms Experience Builder
description: Saiba como criar campos de formulário inteligentes com opções pré-preenchidas usando a base de conhecimento de IA para dados geográficos, classificações comerciais e padrões do setor.
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 0%

---


# Campos inteligentes aprimorados por LLM no Forms Experience Builder {#llm-enhanced-smart-fields}

O Forms Experience Builder aproveita o potencial dos Modelos de linguagem grande (LLMs) para criar campos de formulário inteligentes com opções pré-preenchidas que utilizam bases de conhecimento abrangentes. Esse recurso elimina a necessidade de pesquisar e inserir manualmente grandes conjuntos de dados, melhorando drasticamente a eficiência e a precisão da criação de formulários.

## O que são campos inteligentes aprimorados com LLM? {#what-are-llm-smart-fields}

Os campos inteligentes aprimorados com LLM são campos de formulário que são preenchidos automaticamente com dados abrangentes e precisos usando a base de conhecimento integrada da IA. Em vez de criar listas suspensas ou conjuntos de opções manualmente, você pode solicitar campos que exigem conjuntos de dados extensos, e a IA gerará automaticamente as opções apropriadas.

**Principais benefícios:**

* **Conjuntos de dados abrangentes** - Acesso a informações abrangentes e atualizadas em vários domínios
* **População automática** - Não é necessário pesquisar e inserir dados manualmente
* **Formatos padronizados** - Usa códigos, classificações e convenções de nomenclatura padrão do setor
* **Opções sensíveis ao contexto** - Os campos podem se adaptar com base em outras seleções de formulário
* **Economia de tempo** - Reduz o tempo de criação de formulários de horas para minutos

## Quando usar campos inteligentes aprimorados com LLM {#when-to-use-smart-fields}

Use campos inteligentes aprimorados com LLM quando precisar:

* **Conjuntos de dados abrangentes** - Campos que exigem informações abrangentes e padronizadas
* **Padrões do setor** - Classificações, códigos ou dados normativos
* **Informações geográficas** - Locais, regiões ou divisões administrativas
* **Dados profissionais** - Títulos de trabalho, certificações ou classificações do setor
* **Padrões técnicos** - Formatos de arquivo, protocolos ou especificações do sistema

## Campos geográficos e de localização {#geographic-location-fields}

Crie campos baseados em localização com dados geográficos abrangentes e informações administrativas.

### Aeroportos e transportes

**Aeroportos internacionais com códigos IATA:**

    Adicionar uma lista suspensa para aeroportos de partida com todos os principais aeroportos internacionais
    Adicionar campo de aeroporto de chegada com códigos IATA e nomes completos
    Criar um campo para o aeroporto mais próximo da localização do usuário
    Adicionar uma seleção de estações de trem para cidades europeias

**Prompts de exemplo:**

* &quot;Adicione um campo de aeroporto de partida com todos os principais aeroportos do mundo, incluindo códigos IATA e nomes de cidades&quot;
* &quot;Criar uma lista suspensa de aeroportos de chegada com aeroportos internacionais organizados por continente&quot;
* &quot;Incluir uma seleção de estação de trem para as principais cidades europeias com códigos de estação&quot;

### Regiões administrativas

**Países, estados e províncias:**

    Adicione uma lista completa de estados dos EUA com abreviações
    Crie uma lista suspensa de países com códigos ISO e nomes completos
    Adicione um campo para as principais cidades do mundo com fusos horários
    Inclua uma lista suspensa de províncias e territórios canadenses
    Adicione um campo para condados e áreas postais do Reino Unido

**Prompts de exemplo:**

* &quot;Criar um campo de seleção de país com códigos ISO de país e nomes completos&quot;
* &quot;Adicionar uma lista suspensa de estado dos EUA com abreviações de estado e nomes completos&quot;
* &quot;Incluir um campo de província canadense com territórios e códigos postais&quot;
* &quot;Crie um campo de cidades do mundo com as principais áreas metropolitanas e fusos horários&quot;

## Dados da empresa e do setor {#business-industry-data}

Aproveite classificações de negócios e dados profissionais abrangentes para formulários corporativos.

### Classificações da empresa

**Tipos de entidade de negócio e setor:**

    Adicionar um campo para classificação setorial com códigos NAICS
    Criar uma lista suspensa de tipos de entidades comerciais (LLC, Corporation, Parceria etc.)
    Adicionar um campo para categorias de tamanho de empresa (inicialização, SME, empresa)
    Incluir seleção de departamento para organizações grandes
    Adicionar um campo para tipos de serviço profissional

**Prompts de exemplo:**

* &quot;Criar um campo abrangente do setor usando a classificação NAICS padrão com subcategorias de tecnologia&quot;
* &quot;Adicionar uma lista suspensa de tipo de entidade de negócios com estruturas legais e descrições&quot;
* &quot;Incluir um campo de tamanho da empresa com intervalos de contagem de funcionários e colchetes de receita&quot;

### Classificações profissionais

**Cargos e certificações:**

    Adicione um campo para cargos com funções industriais comuns
    Crie uma lista suspensa de certificações profissionais por campo
    Inclua níveis educacionais com tipos de diploma
    Adicione um campo para anos de intervalos de experiência
    Crie uma seleção para linguagens de programação e estruturas

**Prompts de exemplo:**

* &quot;Inclua uma lista suspensa de certificação profissional que se adapta com base no campo de trabalho selecionado&quot;
* &quot;Criar um campo de cargo com funções comuns em tecnologia, saúde e finanças&quot;
* &quot;Adicione um campo de nível educacional com tipos de diploma e especializações&quot;

## Padrões e dados normativos {#standards-regulatory-data}

Acesse códigos padronizados, classificações e informações normativas para formulários com foco em conformidade.

### Financeiro e legal

**Informações sobre moeda, imposto e pagamento:**

    Adicionar um campo para códigos de moeda com símbolos e taxas de câmbio
    Criar uma lista suspensa de tipos de ID de imposto por país
    Incluir um campo para tipos de documentos legais
    Adicionar opções de método de pagamento com recursos de segurança
    Criar uma seleção para instituições bancárias por país

**Prompts de exemplo:**

* &quot;Criar um campo de seleção de moeda com códigos ISO, símbolos e taxas de câmbio principais&quot;
* &quot;Adicionar um campo de tipo de ID de imposto com formatos de identificação de imposto específicos do país&quot;
* &quot;Incluir uma lista suspensa de método de pagamento com recursos de segurança e tempos de processamento&quot;

### Normas técnicas

**Formatos e protocolos de arquivo:**

    Adicionar uma lista suspensa de tipos de formato de arquivo com extensões
    Incluir opções de protocolo de rede
    Adicionar um campo para tipos e versões de banco de dados
    Criar uma seleção para métodos de autenticação de API

**Prompts de exemplo:**

* &quot;Criar uma lista suspensa de formato de arquivo com extensões comuns e tipos MIME&quot;
* &quot;Adicionar um campo de seleção de banco de dados com comparações de versões e recursos&quot;
* &quot;Incluir um campo de método de autenticação de API com níveis de segurança&quot;

## Saúde e áreas médicas {#healthcare-medical-fields}

Dados médicos e de saúde especializados para formulários específicos do setor.

### Classificações médicas

**Especialidades e dados médicos:**

    Adicionar um campo para especialidades médicas
    Criar uma lista suspensa de medicamentos comuns com nomes genéricos
    Incluir um campo para tipos de provedores de seguro
    Adicionar uma seleção para relações de contato de emergência médica
    Criar um campo para restrições dietéticas e alergias

**Prompts de exemplo:**

* &quot;Crie um campo de especialidade médica com subespecialidades e certificações de placa&quot;
* &quot;Adicione um campo de medicação com nomes genéricos, marcas e formulários de dosagem&quot;
* &quot;Incluir um campo de provedor de seguro com as principais operadoras e tipos de plano&quot;

## Inteligência de hora e calendário {#time-calendar-intelligence}

Campos de data e hora inteligentes com contexto comercial e inteligência de agendamento.

### Campos de data e hora

**Horário comercial e agendamento:**

    Adicionar um campo para horário comercial com tratamento de fuso horário
    Criar uma lista suspensa de feriados por país
    Incluir opções sazonais com intervalos de datas
    Adicionar um campo para reserva de sala de conferência com disponibilidade
    Criar uma seleção para padrões de reunião recorrentes

**Prompts de exemplo:**

* &quot;Criar um campo de horário comercial com fusos horários e exceções de feriado&quot;
* &quot;Adicionar uma seleção de feriado público com observâncias específicas do país&quot;
* &quot;Incluir um campo de padrão de reunião recorrente com opções de frequência&quot;

## Categorias de produtos e serviços {#product-service-categories}

E-commerce e campos orientados a serviços com categorização abrangente.

### Classificações de comércio eletrônico

**Dados de produtos e serviços:**

    Adicionar um campo para categorias de produto com subcategorias
    Criar uma lista suspensa de métodos de envio com estimativas de entrega
    Incluir um campo para opções de política de devolução
    Adicionar uma seleção para níveis de prioridade de cliente
    Criar um campo para ciclos de cobrança de assinatura

**Prompts de exemplo:**

* &quot;Criar um campo de categoria de produto com subcategorias de comércio eletrônico e padrões de SKU&quot;
* &quot;Adicionar uma lista suspensa de método de envio com prazos de entrega e estimativas de custo&quot;
* &quot;Incluir um campo de ciclo de faturamento de assinatura com frequências de pagamento&quot;

## Práticas recomendadas para campos inteligentes aprimorados por LLM {#best-practices-smart-fields}

### Seja específico em suas solicitações

**Bons exemplos:**

* &quot;Adicionar uma lista suspensa de países com códigos ISO, nomes completos e informações sobre moeda&quot;
* &quot;Crie um campo de especialidade médica com certificações e subespecialidades de placas&quot;
* &quot;Incluir um campo de linguagem de programação com estruturas e níveis de habilidade&quot;

**Evitar solicitações vagas:**

* &quot;Adicionar um campo de país&quot;
* &quot;Lista suspensa Criar um título de trabalho&quot;
* &quot;Incluir um campo de categoria de produto&quot;

### Combinar com lógica condicional

Campos inteligentes funcionam muito bem com regras condicionais:

    Crie um campo de certificação profissional que mostre opções relevantes com base no setor selecionado
    Adicione um campo cidade que filtre com base no país selecionado
    Inclua um campo universidade que se adapte com base no campo de estudo escolhido

### Validar e personalizar

Embora os campos aprimorados de LLM forneçam dados abrangentes, sempre:

* **Revise as opções geradas** quanto à precisão e relevância
* **Adicionar opções personalizadas** específicas à sua organização
* **Remova as opções irrelevantes** para simplificar a experiência do usuário
* **Testar com usuários reais** para garantir a usabilidade

## Técnicas avançadas de campo inteligente {#advanced-smart-field-techniques}

### Campos sensíveis ao contexto

Crie campos que se adaptam com base em outras seleções de formulário:

    Adicionar um campo de seleção de universidade com instituições importantes organizadas por país e classificação
    Criar uma lista suspensa de certificação profissional que mostre opções relevantes com base no cargo
    Incluir um campo de cidade que filtre com base no país e na região selecionados

### Classificações de vários níveis

Criar estruturas de dados hierárquicos:

    Criar um campo de categoria de produto com categorias principais, subcategorias e tipos de produto
    Adicionar um campo geográfico com níveis de país, estado/província e cidade
    Incluir um campo de avaliação de habilidade com categorias, subcategorias e níveis de proficiência

### Integração com dados externos

Combine o conhecimento sobre LLM com os dados de sua organização:

    Adicione um campo de departamento que inclua departamentos corporativos padrão e divisões específicas de sua organização
    Crie um campo de produto que combine categorias padrão do setor com seu catálogo de produtos
    Inclua um campo de local que mescle dados geográficos com seus locais de escritório

## Solução de problemas de campos inteligentes {#troubleshooting-smart-fields}

### Problemas comuns e soluções

**Problema: muitas opções geradas**

* **Solução**: seja mais específico em sua solicitação ou adicione critérios de filtragem
* **Exemplo**: em vez de &quot;todos os países&quot;, solicite &quot;principais países parceiros comerciais&quot;

**Problema: opções específicas ausentes**

* **Solução**: adicione opções personalizadas ou refine seu prompt
* **Exemplo**: &quot;Incluir os principais países mais [seus países específicos]&quot;

**Problema: informações desatualizadas**

* **Solução**: solicitar dados atuais ou especificar intervalos de datas
* **Exemplo**: &quot;Adicionar feriados públicos atuais para 2024&quot;

### Otimização do desempenho

* **Opções de limite**: use filtros para reduzir o número de opções geradas
* **Divulgação progressiva**: mostre primeiro as opções básicas e depois permita a expansão
* **Armazenamento em cache**: considere armazenar em cache dados de campo inteligente usados com frequência

## Artigos relacionados

* [Introdução ao Forms Experience Builder](forms-experience-builder-getting-started.md)
* [Criação de formulários alimentados por IA](forms-experience-builder-prompt-examples-library.md)
* [Criação de regras e lógica de negócios](forms-experience-builder-prompt-examples-library.md#rule-creation--business-logic)
* [Envio e integração de formulários](form-submission-integration.md)

