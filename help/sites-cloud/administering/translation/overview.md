---
title: Tradução de conteúdo para sites multilíngues
description: Obtenha uma visão geral de como traduzir conteúdo para sites multilíngues.
feature: Cópia de idioma
role: Administrador
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 1%

---


# Tradução do conteúdo para sites multilíngues {#translating-content-for-multilingual-sites}

Automatize a tradução de conteúdo e ativos da página para criar e manter sites multilíngues. Para automatizar os fluxos de trabalho de tradução, você integra provedores de serviços de tradução ao AEM e cria projetos para traduzir o conteúdo em vários idiomas. AEM suporta fluxos de trabalho de tradução humana e de máquina.

* **Tradução humana:** o conteúdo é enviado para seu provedor de tradução e traduzido por tradutores profissionais. Quando concluído, o conteúdo traduzido é retornado e importado para o AEM. Quando seu provedor de tradução é integrado ao AEM, o conteúdo é enviado automaticamente entre o AEM e o provedor de tradução.
* **Tradução automática:** o serviço de tradução automática traduz imediatamente seu conteúdo.

A tradução de conteúdo envolve as seguintes etapas:

1. [Conecte AEM com seu ](integration-framework.md#connecting-to-a-translation-service-provider) provedor de serviços de tradução e  [crie configurações](integration-framework.md) de estrutura de integração de tradução.
1. [Associe as páginas do ](integration-framework.md#configuring-pages-for-translation) domínio de idioma com o serviço de tradução e as configurações de estrutura.
1. [Identifique o tipo de ](rules.md) conteúdo a ser traduzido.
1. [Prepare o conteúdo para ](preparation.md) tradução criando o idioma principal e criando as páginas raiz das cópias de idioma.
1. [Crie ](managing-projects.md) projetos de tradução para coletar o conteúdo para traduzir e preparar o processo de tradução.
1. Use os projetos de tradução para [gerenciar o processo de tradução de conteúdo](managing-projects.md).

Se o seu provedor de serviços de tradução não fornecer um conector para integração com o AEM, o AEM oferecerá suporte à extração manual e à reinserção do conteúdo de tradução no formato XML.

>[!NOTE]
>
>Seu usuário precisa ser membro do grupo `project-administrators` para usar os recursos da Cópia de idioma.

## Práticas recomendadas     {#best-practices}

A página [Práticas recomendadas de tradução](best-practices.md) contém informações importantes sobre sua implementação.
