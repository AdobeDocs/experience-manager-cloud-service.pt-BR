---
title: Forms Experience Builder
description: Crie formulários avançados mais rapidamente usando os Fragmentos de formulário
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---


# Introdução ao Forms Experience Builder

>[!IMPORTANT]
>
> **Documentação sujeita a alterações**: esta documentação está sendo testada no momento em relação ao produto e está sujeita a atualizações e revisões. Os recursos, os comandos e os exemplos podem mudar à medida que o Forms Experience Builder continua a evoluir durante o programa de adoção inicial.

O AEM Forms Experience Builder aproveita o poder da IA gerativa para democratizar e acelerar a criação e a atualização de experiências de formulário digital. Ao permitir fluxos de trabalho baseados em intenção e impulsionados por interações de linguagem natural, ele permite que os usuários projetem, modifiquem e otimizem formulários com velocidade e simplicidade.

Desenvolvido com tecnologias modernas da Web e alimentado por serviços avançados de IA, o Forms Experience Builder permite que usuários técnicos e não técnicos criem formulários sofisticados de nível profissional por meio de interfaces conversacionais. Essa abordagem revolucionária reduz o tempo de implantação de dias para horas, elimina barreiras técnicas por meio da simplicidade da interface e dimensiona os esforços de modernização em todo o seu ecossistema de formulários.



## Principais recursos

O Forms Experience Builder oferece dois fluxos de trabalho principais para a criação de formulários digitais avançados:

### &#x200B;1. Criação de formulários alimentados por IA

**Geração de formulário de linguagem natural**

Crie formulários completos do zero usando descrições em inglês simples. Basta descrever seus requisitos, como &quot;Criar um formulário de feedback do cliente com escalas de classificação e campos de comentário&quot;, e o Forms Experience Builder gera a estrutura de formulário apropriada. Use o construtor de experiências de editores visuais para adicionar mais campos, regras de validação e lógica de envio.

**Gerenciamento dinâmico de campos**

Adicione, modifique ou remova campos de formulário por meio de comandos conversacionais. A IA entende o contexto e pode sugerir de forma inteligente tipos de campo, regras de validação e melhorias na interface do usuário com base em seus requisitos.

**Otimização de layout**

Atualizar layouts e configurações de formulário por meio do idioma natural. Solicite alterações como &quot;Alterar o layout do formulário para o layout do assistente&quot; e o Forms Experience Builder aplica ajustes de estilo e layout apropriados.

**Configuração Abrangente da Ação de Envio**

Configurar envios de formulários para integrar aos sistemas comerciais existentes:

- **Integração de email**: configurar notificações e confirmações automatizadas por email
- **Pontos de Extremidade da API REST**: Conectar a aplicativos e serviços personalizados
- **Armazenamento na nuvem**: integre-se ao Azure Blob Storage, SharePoint e OneDrive
- **Automação de Fluxo de Trabalho**: Conectar ao Power Automate e ao Workfront Fusion
- **Plataformas de marketing**: integração direta com a Marketo para gerenciamento de clientes potenciais
- **Fluxos de trabalho do AEM**: aproveitar os recursos de fluxo de trabalho existentes do AEM


### &#x200B;2. Importação e conversão inteligentes

**Formatos de Importação com Suporte**

Transforme formulários e documentos existentes em experiências digitais interativas. O Forms Experience Builder é compatível com:

- **Acroforms**: PDF forms interativo com estruturas de campo existentes
- **PDFs XFA**: arquiteturas de formulário complexas baseadas em XML
- **PDFs simples**: documentos estáticos convertidos em formulários interativos
- **Imagens e capturas de tela**: formatos JPG, PNG (verifique limitações de tamanho com a equipe)
- **Forms desenhado à mão**: esboços e fotografias em papel


**Processo de conversão inteligente**

O conteúdo carregado é analisado para:

- Detectar tipos e relacionamentos de campo
- Preservar layout na medida do possível
- Aprimorar com design responsivo moderno
- Adicionar validação avançada e lógica condicional
- Otimizar para acessibilidade e experiência móvel

## Como funciona

O Forms Experience Builder segue uma abordagem simples e conversacional:

    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │ 1. Descrever    │───▶│ 2. A IA cria │───▶│ 3. Refinar e    │
    │ Seu formulário      │    Formulário inicial │   │    │ Configurar      │
    │ requisitos   │    │                 │    │                 │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
    │                       │                       │
    │                       │                       │
    ▼                       ▼                       ▼
    ┌───────────────────────────────────────────────────────────────────────────┐
    │ &quot;Criar um formulário de pedido de empréstimo&quot; → Formulário com informações relevantes                  │
    │ &quot;Adicionar campo de email&quot;           → Campos e base                          │
    │ &quot;Definir valor de email arquivado em @firstname@gmail.com&quot; → regras de validação   │
    └───────────────────────────────────────────────────────────────────────────┘

## Exemplos de cenários

:::: landing-cards-container
:::
![icon](https://cdn.experienceleague.adobe.com/icons/file-pdf.svg?lang=pt-BR)

**Transformar o PDF forms em Forms Digital**

Converta Acroforms, PDFs XFA ou documentos simples do PDF em formulários digitais responsivos e interativos com funcionalidade aprimorada.
:::

:::
![icon](https://cdn.experienceleague.adobe.com/icons/data-transfer-up.svg)

**Modernizar Forms XFA herdado**

Transforme aplicativos XFA complexos em experiências digitais modernas e acessíveis com fluxos de trabalho de usuário aprimorados.
:::

:::
![icon](https://cdn.experienceleague.adobe.com/icons/image.svg?lang=pt-BR)

**Converter Capturas de Tela em Forms Digital**

Transforme imagens, capturas de tela ou formulários desenhados à mão em experiências digitais totalmente funcionais.
:::
::::

<!-- #### Import and Enhance Web Forms

Import existing HTML forms and enhance them with advanced features while preserving existing functionality.

**Key benefits:**

- Advanced validation and business logic
- Conditional field behaviors
- Multi-channel submission options
- Enhanced user experience design -->

## Forms Experience Builder versus desenvolvimento tradicional

| Aspecto | Criação de formulário tradicional | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **Hora de criação** | 2 a 3 dias | 2 a 3 horas |
| **Conhecimento Técnico** | Obrigatório | Não obrigatório |
| **Regras de validação** | Codificação manual | Linguagem natural |
| **Acessibilidade** | Implementação manual | Conformidade integrada |


## Benefícios para organizações

:::: landing-cards-container
:::
![icon](https://cdn.experienceleague.adobe.com/icons/users.svg?lang=pt-BR)

**Criação de formulário democratizada**

Capacite usuários não técnicos a criar formulários sofisticados sem programar o conhecimento por meio de conversas em linguagem natural.
:::

:::
![icon](https://cdn.experienceleague.adobe.com/icons/bolt.svg?lang=pt-BR)

**Tempo de Implantação Reduzido (TTV)**

Acelere drasticamente o desenvolvimento de formulários, de dias para horas, permitindo uma entrada mais rápida no mercado para iniciativas digitais.
:::

:::
![icon](https://cdn.experienceleague.adobe.com/icons/lightbulb.svg?lang=pt-BR)

**Simplicidade da interface**

Elimine a curva de aprendizado com uma interface de conversação intuitiva, reduzindo o tempo de treinamento e aumentando a adoção.
:::

:::
![icon](https://cdn.experienceleague.adobe.com/icons/layers.svg)

**Esforços de Modernização de Escala**

Modernize portfólios de formulários herdados com eficiência, preservando a lógica de negócios e aprimorando a experiência do usuário em todo o seu ecossistema de formulários.
:::
::::

## Integração

O Forms Experience Builder está disponível no momento como parte do programa de Acesso antecipado (EA). Para participar e obter acesso, você precisará das seguintes informações:

### Informações necessárias

- **IMS Organization ID**: o identificador da sua organização da Adobe
- **ID do programa**: o identificador específico de seu programa no Adobe Experience Cloud
- **Detalhes do projeto**: linha do tempo, escopo e casos de uso pretendidos
- **Email Comercial Oficial**: associado à conta da Adobe da sua organização


### Como obter a ID da organização IMS e a ID do programa

Para obter etapas detalhadas para localizar sua IMS Organization ID e ID do Programa, consulte:

- [Guia de configuração da organização da Adobe Experience Cloud](/help/onboarding/cloud-manager-introduction.md)
- [Gerenciamento de Programa e Ambiente](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

### Solicitar acesso

1. Obtenha a ID da organização IMS e a ID do programa usando os guias acima
2. Enviar um email para [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) solicitando acesso
3. Inclua em sua solicitação:
   - Nome da organização e IMS Organization ID
   - ID do programa
   - Cronograma e escopo do projeto
   - Casos de uso pretendidos e objetivos de negócios

>[!IMPORTANT]
>
> **Programa de Disponibilidade Limitada**: o acesso ao Forms Experience Builder está sujeito à aprovação dos participantes internos. A Adobe analisará sua solicitação com base na capacidade do programa e no alinhamento com os critérios de acesso antecipado. A aprovação não é garantida e depende da disponibilidade atual do programa.

Para obter mais informações sobre o programa de Acesso Antecipado e seus recursos, consulte a [documentação de Acesso Antecipado do AEM Forms](/help/forms/early-access-ea-features.md).


## Introdução

Para começar a usar o Forms Experience Builder, visite a [documentação do Forms Experience Builder](forms-ai-assistant-getting-started.md). Você pode acessar o Forms Experience Builder por meio do Editor do AEM Forms ou do Editor universal, dependendo do seu fluxo de trabalho preferido.

Para organizações que desejam transformar seus processos de criação de formulários, o Forms Experience Builder oferece uma solução eficiente e intuitiva que combina a flexibilidade da IA de conversação com a robustez do gerenciamento de formulários de nível empresarial.
