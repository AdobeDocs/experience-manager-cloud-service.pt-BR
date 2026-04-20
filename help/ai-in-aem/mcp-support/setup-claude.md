---
title: Configuração de Claude Antrópico com AEM MCP
description: Saiba como configurar o Anthropic Claude para se conectar aos servidores MCP do AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 2b90b2b2-cdd0-4f1e-890f-2f58f578face
source-git-commit: fede808fcd8b082a71273bf9ffceb48b5332f45d
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Configuração de Claude Antrópico com AEM MCP {#setup-claude}

Siga estas etapas para conectar Anthropic Claude aos servidores MCP da AEM.

* Na configuração do MCP do Claude, registre um ou mais URLs do servidor MCP do AEM.
* Complete o fluxo de logon do Adobe.
* Como opção, ative a confirmação automática para determinadas ferramentas na área de configuração. Essa opção é recomendada para operações de pesquisa ou somente leitura.
* Verifique se o servidor MCP está selecionado antes de iniciar a conversa.
* Peça a Claude para executar tarefas relacionadas ao AEM. Claude seleciona as Ferramentas do AEM expostas pelo servidor MCP com base no seu prompt.

Para configurar o Claude para o AEM MCP, siga as etapas abaixo:

>[!NOTE]
>
>A interface do usuário do Claude está sujeita a alterações e não é definitiva. Estas instruções são para fins ilustrativos.

1. Abra o menu de conta no canto inferior esquerdo do aplicativo Web Claude e escolha **Configurações** para abrir a área Configurações.

   ![Menu Conta em Claude com Configurações selecionadas.](assets/claude-1.png)

1. Na barra lateral Configurações, selecione **Conectores**. Na página Conectores, escolha **Adicionar conector personalizado** para registrar um ponto de extremidade MCP personalizado.

   ![Página Conectores em Configurações com Adicionar conector personalizado.](assets/claude-2.png)

1. Na caixa de diálogo **Adicionar conector personalizado**, digite um nome para exibição (por exemplo, **Serviço MCP de Conteúdo do AEM**) e a URL do servidor MCP do AEM e escolha **Adicionar**. Use as **Configurações avançadas** somente quando a implantação exigir opções adicionais.

   ![Adicionar caixa de diálogo de conector personalizado com nome e URL MCP.](assets/claude-3.png)

1. Na lista Conectores, encontre sua entrada de conector personalizado (ela mostra um rótulo **PERSONALIZADO**) e escolha **Conectar** para entrar e vincular o conector à sua conta Claude.

   ![Lista de conectores com Conectar selecionada para o Serviço MCP de Conteúdo do AEM.](assets/claude-4.png)

1. Quando o conector aparecer na lista com sua URL, escolha **Configurar** ao lado de **Serviço MCP de Conteúdo do AEM** para abrir os detalhes do conector e continuar a instalação.

   ![Lista de conectores com Configurar selecionado para o Serviço MCP de Conteúdo do AEM.](assets/claude-5.png)

1. Na página **Permissões de ferramenta**, revise o padrão (por exemplo, **Precisa de aprovação**) e defina cada ferramenta do AEM como **Sempre permitir**, **Solicitar permissão** ou **Nunca permitir** de acordo com sua política de segurança.

   ![Permissões de ferramenta para o Serviço MCP de Conteúdo do AEM.](assets/claude-6.png)

1. Abra uma conversa. Selecione o menu Ferramentas e Modelo (ícone controles deslizantes) à esquerda do campo de mensagem, habilite o **Serviço de MCP de Conteúdo do AEM** em Conectores e, em seguida, insira seu prompt para que Claude possa usar as ferramentas de MCP para esse bate-papo.

   ![Compositor de chat com o Serviço AEM Content MCP habilitado no menu ferramentas.](assets/claude-7.png)

## Adobe Experience Manager Claude Connector {#aem-claude-connector}

Para instalar o **Conector Claude do Adobe Experience Manager**, abra **Configurações** > **Conectores** no Claude. Você também pode abrir a página Conectores diretamente em [https://claude.ai/settings/connectors](https://claude.ai/settings/connectors). O conector registra um servidor MCP que expõe um conjunto crescente de ferramentas para workflows do AEM.

![Instalando o Adobe Experience Manager Claude Connector a partir do diretório de conectores.](assets/claude-connector.png)