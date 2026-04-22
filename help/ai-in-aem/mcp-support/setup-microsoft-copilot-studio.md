---
title: Configuração do Microsoft Copilot Studio com AEM MCP
description: Saiba como configurar o Microsoft Copilot Studio para se conectar aos servidores MCP do AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: c8e96fe6-1a05-47c0-8215-0c28705e5e48
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# Configuração do Microsoft Copilot Studio com AEM MCP {#setup-microsoft-copilot-studio}

Siga estas etapas para conectar o Microsoft Copilot Studio aos servidores MCP da AEM.

>[!NOTE]
>
>A interface do usuário do Microsoft Copilot Studio está sujeita a alterações e não é definitiva. Estas instruções são para fins ilustrativos.

1. Em **Agentes**, inicie o fluxo para adicionar um agente que usará ferramentas MCP do AEM.

   * Crie um novo agente.

   ![O painel Agentes no Microsoft Copilot Studio.](assets/copilot-1.png)

1. Abra a área de ferramentas desse agente para registrar como ele chama recursos externos.

   * Navegue até a seção da ferramenta e clique em **Adicionar ferramenta**.

   ![A caixa de diálogo Adicionar ferramenta no Microsoft Copilot Studio.](assets/copilot-2.png)

1. Decida se reutilizará uma integração existente ou definirá uma nova ferramenta com suporte de MCP.

   * Selecione uma ferramenta existente ou crie uma nova.

   ![Selecionando Protocolo de Contexto de Modelo como o tipo de ferramenta.](assets/copilot-3.png)

1. Ao criar uma nova ferramenta MCP, continue pela etapa do servidor **Protocolo de Contexto de Modelo**, incluindo o modo de visualização quando ele aparecer.

   * Configure uma nova ferramenta MCP apontando para um ou mais **URLs** do servidor MCP do AEM.

   ![Adicionando um servidor de Protocolo de Contexto de Modelo no modo de visualização.](assets/copilot-4.png)

1. Defina como esse endpoint de MCP é acessado pelo agente, incluindo se o acesso é compartilhado ou dedicado.

   * Estabeleça uma conexão, que pode ser **compartilhada** ou **dedicada** entre agentes.

   ![A caixa de diálogo para criar uma nova conexão.](assets/copilot-5.png)

1. Em **Adicionar e configurar**, forneça ou confirme os detalhes da ferramenta MCP para que o agente possa acessar seu ambiente do AEM.

   ![O painel Adicionar e configurar para a ferramenta MCP.](assets/copilot-6.png)

1. Campos de Término no formulário de ferramenta MCP (por exemplo, **URLs** do servidor e opções relacionadas à autenticação).

   * Como opção, habilite o **modo de confirmação automática** ou exija a **confirmação do usuário final** para todas as interações da ferramenta.

   ![O formulário de configuração da ferramenta MCP.](assets/copilot-7.png)

1. Valide a conectividade com o servidor MCP; conclua o logon baseado em navegador quando o Copilot Studio o redirecionar.

   * Entre usando sua **Adobe ID** quando redirecionado.

   ![Testando a conexão com o servidor MCP do AEM.](assets/copilot-8.png)

1. Antes de executar um teste, abra o **Gerenciar Conexões** (ou o **gerenciador de conexões**) e atribua a conexão correta à sua sessão.

   * Ao testar seu agente, abra o **gerenciador de conexões** primeiro para atribuir uma conexão à sua sessão.

   ![O painel Gerenciar Conexões mostra as conexões disponíveis.](assets/copilot-9.png)

1. Na experiência de teste, execute o agente na conexão AEM MCP.

   * Ao testar seu agente, pressione **Repetir** depois de atribuir uma conexão no **gerenciador de conexões**.

   ![Testando o agente com a conexão MCP do AEM.](assets/copilot-10.png)
