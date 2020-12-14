---
title: Criando um Guia de Start Rápido sem Cabeçalho da Pasta de Ativos
description: Modelos de fragmento de conteúdo definem a estrutura dos Fragmentos de conteúdo. Fragmentos de conteúdo são armazenados em pastas de ativos.
translation-type: tm+mt
source-git-commit: 259d54a225f8dee5929f62b784e28f3fc2bb794a
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---


# Criando um Guia de Start Rápido sem Cabeçalho da Pasta de Ativos{#creating-an-assets-folder}

Modelos de fragmento de conteúdo definem a estrutura dos Fragmentos de conteúdo. Fragmentos de conteúdo são armazenados em pastas de ativos.

##  O que é uma pasta Assets? {#what-is-an-assets-folder}

[Agora que você criou ](create-content-model.md) Modelos de fragmento de conteúdo que definem a estrutura desejada para seus futuros Fragmentos de conteúdo, provavelmente está empolgado para criar alguns fragmentos.

No entanto, primeiro será necessário criar uma pasta de ativos na qual você os armazenará.

As pastas de ativos são usadas para [organizar ativos de conteúdo tradicional](/help/assets/manage-digital-assets.md) como imagens e vídeos, bem como Fragmentos de conteúdo.

## Como criar uma pasta de ativos {#how-to-create-an-assets-folder}

Um administrador só precisaria criar pastas ocasionalmente para organizar o conteúdo conforme ele é criado. Para fins deste guia de introdução, precisamos apenas criar uma pasta.

1. Efetue login AEM como um Cloud Service e, no menu principal, selecione **Navegação -> Ativos -> Arquivos**.
1. Toque ou clique em **Criar -> Pasta**.
1. Forneça um **Título** e um **Nome** para a sua pasta.
   * O **Title** deve ser descritivo.
   * O **Name** se tornará o nome do nó no repositório.
      * Será gerado automaticamente com base no título e ajustado de acordo com [AEM convenções de nomenclatura.](/help/implementing/developing/introduction/naming-conventions.md)
      * Pode ser ajustado, se necessário.

   ![Criar pasta](../assets/assets-folder-create.png)
1. Selecione a pasta que você acabou de criar e selecione **Propriedades** na barra de ferramentas (ou use o atalho de teclado `p` [s.](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md))
1. Na janela **Propriedades**, selecione a guia **Cloud Services**.
1. Para a **Configuração da nuvem** selecione a configuração [criada anteriormente.](create-configuration.md)

   ![Configurar pasta de ativos](../assets/assets-folder-configure.png)
1. Toque ou clique em **Salvar e fechar**.
1. Toque ou clique em **OK** na janela de confirmação.

   ![Janela de confirmação](../assets/assets-folder-confirmation.png)

É possível criar subpastas adicionais dentro da pasta que você acabou de criar. As subpastas herdarão **Configuração da nuvem** da pasta pai. Isso pode ser substituído, no entanto, se você quiser usar modelos de outra configuração.

Se estiver usando uma estrutura de site localizada, você pode [criar uma raiz de idioma](/help/assets/translate-assets.md) abaixo da nova pasta.

## Próximas etapas {#next-steps}

Agora que você criou uma pasta para seus Fragmentos de conteúdo, pode seguir para a quarta parte do guia de introdução e [criar fragmentos de conteúdo.](create-content-fragment.md)

>[!TIP]
>
>Para obter detalhes completos sobre o gerenciamento de Fragmentos de conteúdo, consulte a [documentação de Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
