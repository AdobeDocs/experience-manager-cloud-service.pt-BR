---
title: Criação de uma pasta de ativos - Configuração do headless
description: Use os modelos de fragmento de conteúdo do AEM para definir a estrutura dos fragmentos de conteúdo, a base do seu conteúdo headless.
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 77%

---

# Criação de uma pasta de ativos - Configuração do headless {#creating-an-assets-folder}

Use os modelos de fragmento de conteúdo do AEM para definir a estrutura dos fragmentos de conteúdo, a base do seu conteúdo headless. Os fragmentos de conteúdo são armazenados nas pastas de ativos.

## O que é uma pasta de ativos? {#what-is-an-assets-folder}

[Agora que você criou modelos de fragmento de conteúdo](create-content-model.md) que definem a estrutura desejada para os fragmentos de conteúdo futuros, você provavelmente está animado para criar alguns fragmentos.

No entanto, primeiro será necessário criar uma pasta de ativos na qual você os armazenará.

As pastas de ativos são usadas para [organizar ativos de conteúdo tradicionais](/help/assets/manage-digital-assets.md), como imagens e vídeos, juntamente com fragmentos de conteúdo.

## Criar e configurar uma pasta do Assets {#create-and-configure-an-assets-folder}

Um administrador só precisaria criar pastas ocasionalmente para organizar o conteúdo, conforme ele fosse criado. Use o console Assets para criar a nova pasta.

Depois de criada, você precisa aplicar sua [configuração](/help/headless/setup/create-configuration.md) à pasta. Para obter detalhes, consulte [Aplicar a configuração à sua pasta](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder).

É possível criar subpastas adicionais dentro da pasta criada. As subpastas herdarão a **Configuração na nuvem** da pasta principal. Isso pode ser alterado, no entanto, se você quiser usar modelos de outra configuração.

Se estiver usando uma estrutura de site localizada, é possível [criar uma raiz de idioma](/help/assets/translate-assets.md) abaixo da nova pasta.

## Próximas etapas {#next-steps}

Depois de criar uma pasta para os fragmentos de conteúdo, você pode seguir para a quarta parte do guia de introdução e [criar fragmentos de conteúdo](create-content-fragment.md).

>[!TIP]
>
>Para obter detalhes completos sobre o gerenciamento de fragmentos de conteúdo, consulte a [documentação dos Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)
