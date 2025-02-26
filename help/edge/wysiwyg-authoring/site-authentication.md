---
title: Configuração da autenticação de site para a criação de conteúdo
description: Saiba como o AEM Live oferece suporte à autenticação baseada em token e como você pode configurar o AEM para usar a autenticação com a criação do WYSIWYG.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 6d28b831fb902173bb5fbadd4aa2a52ba58e0a3b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 2%

---


# Configuração da autenticação de site para a criação de conteúdo {#site-authentication}

Saiba como o AEM Live oferece suporte à autenticação baseada em token e como você pode configurar o AEM para usar a autenticação com a criação do WYSIWYG.

## Visão geral {#overview}

O AEM Live oferece suporte à autenticação baseada em token. Normalmente, a autenticação de site é aplicada aos sites de visualização e publicação, mas também pode ser configurada para proteger apenas um dos sites individualmente.

>[!NOTE]
>
>Se você optar por ativar a autenticação do site, será necessário configurá-la nos ambientes de criação do AEM também

## Requisitos {#requirements}

Para configurar a autenticação do site para uso com a criação de conteúdo, primeiro conclua as seguintes tarefas:

* Este documento supõe que você já tenha criado um site para o seu projeto com base no [Guia de Introdução do Desenvolvedor para Criação no WYSIWYG com o guia do Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* Você já deve ter [habilitado o recurso de resposta para o seu projeto.](/help/edge/wysiwyg-authoring/repoless.md)

## Configurar autenticação do site {#configure-authentication}

Consulte o documento [Configurando a Autenticação do Site](https://www.aem.live/docs/authentication-setup-site) para obter detalhes sobre como configurar a autenticação do site.

Anote as seguintes informações ao configurar a autenticação:

* A ID da conta técnica
* O token de autenticação do site

Esses itens são necessários para concluir a configuração da autenticação do site para o ambiente de criação do AEM.

## Configurar ambiente de criação {#authoring-environment}

Depois que a autenticação do site for configurada, você poderá habilitá-la no ambiente de criação do AEM.

1. Entre na instância do autor do AEM e vá para **Ferramentas** -> **Serviços da Nuvem** -> **Configuração do Edge Delivery Services** e selecione a configuração que foi criada automaticamente para o seu site e toque ou clique em **Propriedades** na barra de ferramentas.
1. Na janela **Configuração do Edge Delivery Services**, selecione a guia **Autenticação** e forneça os seguintes valores, que você anotou ao configurar a autenticação do site.

   * **A ID da conta técnica**
   * **Token de Autenticação do Site**

   ![Configuração do Edge Delivery Services](/help/edge/wysiwyg-authoring/assets/site-authentication/configure-aem-author.png)

1. Toque ou clique em **Salvar e fechar**.
