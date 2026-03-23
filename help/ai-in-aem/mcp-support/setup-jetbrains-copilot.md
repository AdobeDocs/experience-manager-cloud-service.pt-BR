---
title: Configuração do JetBrains com o Copilot do GitHub e o MCP do AEM
description: Saiba como configurar o GitHub Copilot em IDEs JetBrains para se conectar aos servidores MCP do AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: c5b46aff5b4ccffa60e8bebf7341935b435079e3
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Configuração do JetBrains com o Copilot do GitHub e o MCP do AEM {#setup-jetbrains-copilot}

Siga estas etapas para conectar o GitHub Copilot em um JetBrains IDE (como IntelliJ IDEA, WebStorm ou PyCharm) aos servidores MCP da AEM.

1. Abra o GitHub Copilot Chat no JetBrains IDE clicando no ícone do **GitHub Copilot Chat** no lado direito do editor.

   ![O JetBrains IDE com o GitHub Copilot Chat está aberto.](assets/jetbrains-copilot-1.png)

1. Clique no ícone **settings** no painel Copilot Chat para abrir a configuração do MCP.

   ![O painel GitHub Copilot Chat com o ícone de configurações realçado.](assets/jetbrains-copilot-2.png)

1. Em **Configurações**, navegue até **Ferramentas > GitHub Copilot > Protocolo de Contexto de Modelo (MCP)** e clique em **Configurar** para abrir o arquivo de configuração `mcp.json`.

   ![A caixa de diálogo Configurações do JetBrains mostrando a configuração do Protocolo de Contexto de Modelo (MCP) no GitHub Copilot.](assets/jetbrains-copilot-3.png)

1. Adicione uma ou mais URLs do servidor AEM MCP ao arquivo `mcp.json`. Por exemplo:

   ```json
   {
     "servers": {
       "aem": {
         "url": "https://mcp.adobeaemcloud.com/adobe/mcp/content"
       }
     }
   }
   ```


   ![O arquivo de configuração mcp.json com a URL do servidor MCP do AEM.](assets/jetbrains-copilot-4.png)


1. Salve o arquivo. O GitHub Copilot detecta a nova configuração do servidor automaticamente e mostra uma ação **Start**.

   ![O arquivo mcp.json mostrando o servidor AEM configurado com ferramentas detectadas.](assets/jetbrains-copilot-5.png)

1. Clique na ação **Iniciar** e, quando solicitado, entre com a Adobe ID para concluir o fluxo de autenticação.

1. Você pode revisar e gerenciar as ferramentas descobertas clicando no indicador **ferramentas** que aparece no painel do Copilot Chat. Como opção, ative ou desative ferramentas individuais.


   ![A caixa de diálogo Configurar Ferramentas mostra as ferramentas MCP do AEM disponíveis.](assets/jetbrains-copilot-6.png)

1. Use o GitHub Copilot Chat para chamar as ferramentas do AEM como parte de seus fluxos de trabalho de desenvolvimento ou conteúdo.