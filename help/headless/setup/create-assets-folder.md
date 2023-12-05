---
title: Criação de uma pasta de ativos - Configuração do headless
description: Use os modelos de fragmento de conteúdo do AEM para definir a estrutura dos fragmentos de conteúdo, a base do seu conteúdo headless.
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 82%

---

# Criação de uma pasta de ativos - Configuração do headless {#creating-an-assets-folder}

Use os modelos de fragmento de conteúdo do AEM para definir a estrutura dos fragmentos de conteúdo, a base do seu conteúdo headless. Os fragmentos de conteúdo são armazenados nas pastas de ativos.

## O que é uma pasta de ativos? {#what-is-an-assets-folder}

[Agora que você criou modelos de fragmento de conteúdo](create-content-model.md) que definem a estrutura desejada para os fragmentos de conteúdo futuros, você provavelmente está animado para criar alguns fragmentos.

No entanto, primeiro será necessário criar uma pasta de ativos na qual você os armazenará.

As pastas de ativos são usadas para [organizar ativos de conteúdo tradicionais](/help/assets/manage-digital-assets.md), como imagens e vídeos, juntamente com fragmentos de conteúdo.

## Como criar uma pasta de ativos {#how-to-create-an-assets-folder}

Um administrador só precisaria criar pastas ocasionalmente para organizar o conteúdo, conforme ele fosse criado. Para os propósitos deste guia de introdução, precisamos criar apenas uma pasta.

1. Faça logon no AEM as a Cloud Service e, no menu principal, selecione **Navegação > Ativos > Arquivos**.
1. Selecionar **Criar > Pasta**.
1. Forneça um **Título** e um **Nome** para sua pasta.
   * O **Título** deve ser descritivo.
   * O **Nome** se tornará o nome do nó no repositório.
      * Ele será gerado automaticamente com base no título e ajustado conforme as [convenções de nomenclatura do AEM](/help/implementing/developing/introduction/naming-conventions.md).
      * Ele pode ser ajustado, se necessário.

   ![Criar pasta](../assets/assets-folder-create.png)
1. Selecione a pasta criada passando o mouse sobre ela e tocando na marca de seleção. Em seguida, selecione **Propriedades** na barra de ferramentas (ou use o [atalho de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `p`).
1. Na janela **Propriedades**, selecione a guia **Serviços em nuvem**.
1. Para a **Configuração na nuvem**, selecione a [configuração criada anteriormente.](create-configuration.md)
   ![Configurar pasta de ativos](../assets/assets-folder-configure.png)
1. Selecionar **Salvar e fechar**.
1. Selecionar **OK** na janela de confirmação.

   ![Janela de confirmação](../assets/assets-folder-confirmation.png)

É possível criar subpastas adicionais dentro da pasta criada. As subpastas herdarão a **Configuração na nuvem** da pasta principal. Isso pode ser alterado, no entanto, se você quiser usar modelos de outra configuração.

Se estiver usando uma estrutura de site localizada, é possível [criar uma raiz de idioma](/help/assets/translate-assets.md) abaixo da nova pasta.

## Próximas etapas {#next-steps}

Depois de criar uma pasta para os fragmentos de conteúdo, você pode seguir para a quarta parte do guia de introdução e [criar fragmentos de conteúdo](create-content-fragment.md).

>[!TIP]
>
>Para obter detalhes completos sobre o gerenciamento de fragmentos de conteúdo, consulte a [documentação dos Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)
