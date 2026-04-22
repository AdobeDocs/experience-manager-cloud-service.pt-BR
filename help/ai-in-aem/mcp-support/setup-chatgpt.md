---
title: Configuração do OpenAI ChatGPT com o AEM MCP
description: Saiba como configurar o OpenAI ChatGPT para se conectar aos servidores MCP do AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 1f116225-168b-483c-9df6-c752a573b57b
source-git-commit: f7a5c43a4a4dd6629225f3628a7c592056d6d144
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Configuração do OpenAI ChatGPT com o AEM MCP {#setup-chatgpt}

Siga estas etapas para conectar o OpenAI ChatGPT aos servidores MCP da AEM.

* Adicione um ou mais URLs do servidor MCP do AEM na área em que as conexões ou ferramentas do MCP estão configuradas.
* Acione a conexão e faça logon com sua Adobe ID quando redirecionado.
* Em um chat, consulte as Ferramentas do AEM configuradas em seus prompts, por exemplo:

  ```
  "Using the configured AEM MCP tools, list all sites in the author environment."
  ```

>[!NOTE]
>
>A interface do usuário do OpenAI ChatGPT está sujeita a alterações e não é definitiva. Estas instruções são para fins ilustrativos.

1. Abra **Configurações** para alcançar a área onde as conexões ou ferramentas do MCP estão configuradas.

   ![A caixa de diálogo Configurações de ChatGPT.](assets/chatgpt-1.png)

1. Em **Aplicativos e Conectores**, abra as **Configurações Avançadas** para gerenciar o conector e as opções relacionadas ao MCP.

   ![O painel Configurações Avançadas de Aplicativos e Conectores no ChatGPT.](assets/chatgpt-2.png)

1. Habilite o **Modo de desenvolvedor** em **Aplicativos e Conectores** para que você possa adicionar e configurar aplicativos ou conectores personalizados.

   ![Habilitando o modo de Desenvolvedor na seção Aplicativos e Conectores.](assets/chatgpt-3.png)

1. Inicie **Criar novo aplicativo** (ou o controle equivalente) para adicionar uma entrada de aplicativo para o servidor MCP do AEM.

   ![A caixa de diálogo para criar um novo aplicativo no ChatGPT.](assets/chatgpt-4.png)

1. Preencha o formulário **Novo aplicativo** — por exemplo, nomeie o aplicativo e insira a URL do servidor MCP do AEM e quaisquer outros campos necessários — e **Salve**.

   ![O formulário de configuração Novo Aplicativo no ChatGPT.](assets/chatgpt-5.png)

1. Confirme se o **Serviço MCP de Conteúdo do AEM** (ou o aplicativo configurado) aparece em **Aplicativos e Conectores** para que o ChatGPT possa usá-lo.

   ![O Serviço MCP de Conteúdo do AEM listado em Aplicativos e Conectores.](assets/chatgpt-6.png)

1. Em um chat, escreva um prompt que informe ao ChatGPT para usar as **Ferramentas do AEM** configuradas (por exemplo, para consultar conteúdo ou sites de autor).

   ![Solicitando que o ChatGPT use o Serviço AEM Content MCP.](assets/chatgpt-7.png)
