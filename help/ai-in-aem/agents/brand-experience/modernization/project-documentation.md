---
title: Habilidade de documentação do projeto
description: Saiba como a habilidade da documentação do Agente de modernização de experiência pode ajudar você a acelerar as entregas de projetos.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 90fb75c7febc8a8138e13a2f3ff872f38eeb3baa
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Habilidade de documentação do projeto {#project-documentation}

Saiba como a habilidade da documentação do Agente de modernização de experiência pode ajudar você a acelerar as entregas de projetos.

## Acelerando as transferências de projetos {#project-handovers}

[O Agente de Modernização de Experiência](/help/ai-in-aem/agents/brand-experience/modernization/overview.md) pode gerar automaticamente guias de documentação de projeto para projetos do AEM Edge Delivery Services, apresentando:

* **Apresentação do projeto** - Explicação da configuração, estrutura e convenções do projeto, geradas sem esforço manual
* **Organização de módulos e componentes** - Documentação clara de como os blocos, módulos e componentes são organizados e como eles se relacionam entre si
* **Guias com base em funções** - Documentação direcionada para autores, desenvolvedores e administradores; portanto, cada membro da equipe recebe exatamente o que precisa

Isso simplifica as transferências de projetos do AEM Edge Delivery Services.

## Pré-requisitos {#prerequisites}

Certifique-se do seguinte antes de usar esta habilidade.

* Seu projeto deve ser submetido a check-out no espaço de trabalho no console.
* Você deve ter permissões de administrador para o projeto para o qual está criando a documentação.
* Permissões de agente devem ser permitidas no console.
   * Selecione a opção **Permitir que o LLM acesse admin.hlx.page em meu nome** [nas configurações do console.](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view)
   * Se essa opção não estiver ativada, o agente gerará a documentação com base na base de código acessível a ele.

## Criando documentação do projeto {#creating-documentation}

Depois que os pré-requisitos forem atendidos, basta solicitar que o agente crie a documentação do projeto.

1. No bate-papo, pergunte &quot;Criar documentação deste projeto&quot;.
1. Forneça o nome da organização do projeto se o agente solicitar.
1. O agente perguntará qual documentação você deseja criar. Normalmente, você selecionaria **Todos**.

   ![Criar documentação](assets/select-documentation.png)

1. Depois de criadas, as guias são colocadas em seu espaço de trabalho. Selecione um para exibir uma descrição e clique no link para baixar a PDF completa.

   ![Documentação criada](assets/documentation-created.png)

Você pode salvar a PDF diretamente para fornecê-la às suas equipes ou carregá-la como parte do restante do conteúdo do DA.

![Guia do administrador](assets/admin-guide.png)

>[!NOTE]
>
>Se você não estiver autorizado a acessar a API de administrador do Edge Delivery Services ou a opção **Permitir que o LLM acesse admin.hlx.page em meu nome** [nas configurações do console.](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view) não está habilitado, o agente gerará a documentação com base na base de código acessível a ele.

## Resolução de problemas {#troubleshooting}

A seguir estão mensagens de erro comuns encontradas ao usar a habilidade de documentação do projeto e como resolvê-las.

### &quot;Acesso negado&quot; ou &quot;Não autorizado&quot; {#unauthorized}

* **Causa:** Permissões de administrador ou de agente ausentes não habilitadas
* **Solução:**
   1. Verifique se você tem acesso de administrador ao projeto
   1. Selecione a opção **Permitir que o LLM acesse admin.hlx.page em meu nome** [nas configurações do console.](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view)

### &quot;Projeto não encontrado&quot; {#not-found}

* **Causa:** repositório não foi verificado no espaço de trabalho
* **Solução:**
   1. Confira o repositório do projeto
   1. Verifique se você está no espaço de trabalho correto

### &quot;Erro de API de configuração&quot; {#api-error}

* **Causa:** não é possível acessar a API do serviço de configuração do Edge Delivery Services
* **Solução:**
   1. Selecione a opção **Permitir que o LLM acesse admin.hlx.page em meu nome** [nas configurações do console.](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view)
   1. Verifique sua conexão de rede/VPN
   1. Confirmar acesso de administrador ao projeto
