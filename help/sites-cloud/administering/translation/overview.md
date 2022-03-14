---
title: Tradução de conteúdo para sites multilíngues
description: Get an overview of how to translate content for multilingual sites.
feature: Language Copy
role: Admin
exl-id: c3e89719-4d08-401b-b9dd-19d1db03d72c
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 4%

---

# Tradução de conteúdo para sites multilíngues {#translating-content-for-multilingual-sites}

Automatize a tradução de conteúdo e ativos da página para criar e manter sites multilíngues. Para automatizar os fluxos de trabalho de tradução, você integra provedores de serviços de tradução ao AEM e cria projetos para traduzir o conteúdo em vários idiomas. AEM supports human and machine translation workflows.

* **Tradução humana:** O conteúdo é enviado para seu provedor de tradução e traduzido por tradutores profissionais. Quando concluído, o conteúdo traduzido é retornado e importado para o AEM. Quando seu provedor de tradução é integrado ao AEM, o conteúdo é enviado automaticamente entre o AEM e o provedor de tradução.
* **Tradução da máquina:** O serviço de tradução automática traduz imediatamente seu conteúdo.

>[!TIP]
>
>If you are new to translating content, please refer to our [Sites Translation Journey,](/help/journey-sites/translation/overview.md) which is guided path through translating your AEM Sites content using AEM’s powerful translation tools, ideal for those with no AEM or translation experience.

A tradução de conteúdo envolve as seguintes etapas:

1. [Connect AEM with your translation service provider](integration-framework.md#connecting-to-a-translation-service-provider) and [create translation integration framework configurations](integration-framework.md).
1. [Associar as páginas do seu idioma principal](integration-framework.md#configuring-pages-for-translation) com o serviço de tradução e as configurações da estrutura.
1. [Identificar o tipo de conteúdo](rules.md) para traduzir.
1. [Preparar o conteúdo para tradução](preparation.md) criando o idioma principal e criando as páginas raiz das cópias de idioma.
1. [Create translation projects](managing-projects.md) to gather the content to translate and to prepare the translation process.
1. Use os projetos de tradução para [gerenciar o processo de tradução de conteúdo](managing-projects.md).

Se o seu provedor de serviços de tradução não fornecer um conector para integração com o AEM, o AEM oferecerá suporte à extração manual e à reinserção do conteúdo de tradução no formato XML.

>[!NOTE]
>
>Seu usuário precisa ser membro do `project-administrators` para usar os recursos da Cópia de idioma.

## Práticas recomendadas     {#best-practices}

The [Translation Best Practices](best-practices.md) page contains important information regarding your implementation.
