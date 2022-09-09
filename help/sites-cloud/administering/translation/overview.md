---
title: Tradução de conteúdo para sites multilíngues
description: Obtenha uma visão geral de como traduzir conteúdo para sites multilíngues.
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 100%

---

# Tradução de conteúdo para sites multilíngues {#translating-content-for-multilingual-sites}

Automatize a tradução de conteúdo e ativos da página para criar e manter sites multilíngues. Para automatizar workflows de tradução, você integra provedores de serviços de tradução ao AEM e cria projetos para traduzir o conteúdo em vários idiomas. O AEM permite workflows de tradução humana e de máquina.

* **Tradução humana:** o conteúdo é enviado para seu provedor de tradução e traduzido por tradutores profissionais. Quando concluído, o conteúdo traduzido é retornado e importado para o AEM. Quando seu provedor de tradução é integrado ao AEM, o conteúdo é enviado automaticamente entre o AEM e o provedor de tradução.
* **Tradução automática:** o serviço de tradução automática traduz imediatamente seu conteúdo.

>[!TIP]
>
>Se você é novo na tradução de conteúdo, consulte nossa [Jornada de tradução de sites,](/help/journey-sites/translation/overview.md) que é um caminho guiado pela tradução de conteúdo do AEM Sites usando as ferramentas de tradução avançadas do AEM, ideais para aqueles sem experiência no AEM ou em tradução.

A tradução de conteúdo envolve as seguintes etapas:

1. [Conecte o AEM com seu provedor de serviços de tradução](integration-framework.md#connecting-to-a-translation-service-provider) e [crie configurações da estrutura de integração de tradução](integration-framework.md).
1. [Associe as páginas do seu idioma principal](integration-framework.md#configuring-pages-for-translation) com o serviço de tradução e as configurações da estrutura.
1. [Identifique o tipo de conteúdo](rules.md) para traduzir.
1. [Prepare o conteúdo para tradução](preparation.md) criando o idioma principal e as páginas raiz das cópias de idioma.
1. [Crie projetos de tradução](managing-projects.md) para coletar o conteúdo para traduzir e para preparar o processo de tradução.
1. Use os projetos de tradução para [gerenciar o processo de tradução de conteúdo](managing-projects.md).

Se o seu provedor de serviços de tradução não fornecer um conector para integração com o AEM, o AEM oferecerá suporte à extração manual e à reinserção do conteúdo de tradução no formato XML.

>[!NOTE]
>
>Seu usuário precisa ser membro do grupo `project-administrators` para usar os recursos de Cópia de idioma.

## Práticas recomendadas     {#best-practices}

A página [Práticas recomendadas de tradução](best-practices.md) contém informações importantes sobre a implementação.
