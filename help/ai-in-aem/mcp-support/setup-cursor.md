---
title: Configurando o Cursor com o AEM MCP
description: Saiba como configurar o Cursor para se conectar aos servidores MCP do AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: f0897898-cb1d-4af6-859c-f5a1c0ec6168
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Configurando o Cursor com o AEM MCP {#setup-cursor}

Siga estas etapas para conectar o Cursor aos servidores MCP da AEM.

* Nas configurações de MCP do cursor, crie uma nova entrada de servidor MCP com um ou mais URLs MCP do AEM.
* Autentique com seu Adobe ID quando solicitado.
* Como opção, ative ou desative ferramentas individuais clicando nos nomes das ferramentas. Todas as ferramentas são ativadas por padrão.
* Use o editor ou o chat do cursor para chamar as Ferramentas do AEM como parte dos fluxos de trabalho de desenvolvimento ou conteúdo.

>[!NOTE]
>
>A interface do usuário do Cursor está sujeita a alterações e não é definitiva. Estas instruções são para fins ilustrativos.

1. Abra **Configurações do Cursor** para que você possa configurar como o Cursor se conecta aos servidores MCP.

   ![A caixa de diálogo Configurações do Cursor.](assets/cursor-1.png)

1. Abra **Ferramentas e MCP** e escolha **Adicionar MCP personalizado** para iniciar uma entrada de servidor MCP personalizado.

   ![O painel Ferramentas e MCP com a opção de adicionar um servidor MCP personalizado.](assets/cursor-2.png)

1. No formulário de servidor MCP personalizado, insira o **Nome**, a **URL** (ou URLs) do MCP do AEM e quaisquer outros campos obrigatórios, depois **Salvar**.

   ![Formulário de configurações personalizadas do servidor MCP no Cursor.](assets/cursor-3.png)

1. Quando a caixa de diálogo de conexão for exibida, conclua o logon pressionando **Conectar** para que o novo servidor MCP seja autorizado.

   ![A caixa de diálogo de conexão para o novo servidor MCP no Cursor.](assets/cursor-4.png)

1. No **Chat** ou no editor, escreva prompts que invoquem as **Ferramentas do AEM** para que o servidor MCP configurado participe do seu fluxo de trabalho.

   ![Solicitando que o cursor use o novo serviço AEM MCP.](assets/cursor-5.png)
