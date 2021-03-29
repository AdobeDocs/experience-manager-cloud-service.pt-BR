---
title: Criação de uma pasta de ativos sem cabeçalho Guia de início rápido
description: Use AEM Modelos de fragmentos do conteúdo para definir a estrutura dos Fragmentos do conteúdo, a base do seu conteúdo sem periféricos.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---


# Criação de uma pasta de ativos sem cabeçalho Guia de início rápido {#creating-an-assets-folder}

Use AEM Modelos de fragmentos do conteúdo para definir a estrutura dos Fragmentos do conteúdo, a base do seu conteúdo sem periféricos. Os Fragmentos de conteúdo são armazenados nas pastas de ativos.

##  O que é uma pasta de ativos? {#what-is-an-assets-folder}

[Agora que você criou ](create-content-model.md) Modelos de fragmento de conteúdo que definem a estrutura desejada para os Fragmentos de conteúdo futuros, provavelmente está animado em criar alguns fragmentos.

No entanto, primeiro será necessário criar uma pasta de ativos na qual você os armazenará.

As pastas de ativos são usadas para [organizar ativos de conteúdo tradicional](/help/assets/manage-digital-assets.md) como imagens e vídeos, bem como Fragmentos de conteúdo.

## Como criar uma pasta de ativos {#how-to-create-an-assets-folder}

Um administrador só precisaria criar pastas ocasionalmente para organizar o conteúdo conforme ele fosse criado. Para o objetivo deste guia de introdução, precisamos apenas criar uma pasta.

1. Faça logon em AEM como um Cloud Service e, no menu principal, selecione **Navigation -> Assets -> Files**.
1. Toque ou clique em **Criar -> Pasta**.
1. Forneça um **Título** e um **Nome** para a sua pasta.
   * O **Title** deve ser descritivo.
   * O **Name** se tornará o nome do nó no repositório.
      * Ele será gerado automaticamente com base no título e ajustado de acordo com [AEM convenções de nomenclatura.](/help/implementing/developing/introduction/naming-conventions.md)
      * Pode ser ajustado, se necessário.

   ![Criar pasta](../assets/assets-folder-create.png)
1. Selecione a pasta que acabou de criar e selecione **Propriedades** na barra de ferramentas (ou utilize o `p` [atalho de teclado.](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md))
1. Na janela **Properties**, selecione a guia **Cloud Services**.
1. Para **Configuração da nuvem** selecione a configuração [criada anteriormente.](create-configuration.md)

   ![Configurar pasta de ativos](../assets/assets-folder-configure.png)
1. Toque ou clique em **Salvar e fechar**.
1. Toque ou clique em **OK** na janela de confirmação.

   ![Janela de confirmação](../assets/assets-folder-confirmation.png)

Você pode criar subpastas adicionais dentro da pasta que acabou de criar. As subpastas herdarão o **Cloud Configuration** da pasta principal. Isso pode ser substituído, no entanto, se você quiser usar modelos de outra configuração.

Se estiver usando uma estrutura de site localizada, você pode [criar uma raiz de idioma](/help/assets/translate-assets.md) abaixo de sua nova pasta.

## Próximas etapas {#next-steps}

Depois de criar uma pasta para os Fragmentos de conteúdo, você pode seguir para a quarta parte do guia de introdução e [criar fragmentos de conteúdo.](create-content-fragment.md)

>[!TIP]
>
>Para obter detalhes completos sobre o gerenciamento dos Fragmentos de conteúdo, consulte a [documentação dos Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
