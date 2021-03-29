---
title: Criação dos modelos de fragmento de conteúdo sem cabeçalho Guia de início rápido
description: Defina a estrutura do conteúdo que será criado e veiculado usando AEM recursos headless usando Modelos de fragmentos de conteúdo.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---


# Criação dos modelos de fragmento de conteúdo sem cabeçalho Guia de início rápido {#creating-content-fragment-models}

Defina a estrutura do conteúdo que será criado e veiculado usando AEM recursos headless usando Modelos de fragmentos de conteúdo.

## O que são modelos de fragmentos de conteúdo? {#what-are-content-fragment-models}

[Depois de criar uma configuração, ](create-configuration.md) você pode usá-la para criar Modelos de fragmento de conteúdo.

Os Modelos de fragmentos de conteúdo definem a estrutura dos dados e do conteúdo que você criará e gerenciará no AEM. Eles servem como uma espécie de scaffolding para o seu conteúdo. Ao optar por criar o conteúdo, os autores selecionarão entre os Modelos de fragmento de conteúdo definidos, que os orientarão na criação do conteúdo.

## Como criar um modelo de fragmento de conteúdo {#how-to-create-a-content-fragment-model}

Um arquiteto de informações executaria essas tarefas apenas esporadicamente, pois novos modelos são necessários. Para o objetivo deste guia de introdução, precisamos apenas criar um modelo.

1. Faça logon em AEM como um Cloud Service e, no menu principal, selecione **Ferramentas -> Ativos -> Modelos de fragmento de conteúdo**.
1. Toque ou clique na pasta que foi feita criando sua configuração.

   ![A pasta de modelos](../assets/models-folder.png)
1. Toque ou clique em **Criar**.
1. Forneça um **Título do modelo**, **Tags** e **Descrição**. Você também pode selecionar/desmarcar **Ativar modelo** para controlar se o modelo é ativado imediatamente após a criação.

   ![Criar um modelo](../assets/models-create.png)
1. Na janela de confirmação, toque ou clique em **Open** para configurar o modelo.

   ![Janela de confirmação](../assets/models-confirmation.png)
1. Usando o **Editor do modelo de fragmento de conteúdo**, crie o modelo de fragmento de conteúdo arrastando e soltando campos da coluna **Tipos de dados**.

   ![Arrastar e soltar campos](../assets/models-drag-and-drop.png)

1. Depois de colocar um campo, você deve configurar suas propriedades. O editor alternará automaticamente para a guia **Properties** do campo adicionado, onde é possível fornecer os campos obrigatórios.

   ![Configurar propriedades](../assets/models-configure-properties.png)
1. Quando terminar de criar o modelo, toque ou clique em **Salvar**. O modelo recém-criado é salvo no modo **Rascunho**.

   ![Modelo no modo de rascunho](../assets/models-draft.png)
1. O modelo deve ser habilitado para usá-lo (se ainda não estiver habilitado). Selecione o modelo que acabou de criar e toque ou clique em **Ativar**.

   ![Ativação do modelo](../assets/models-enable.png)
1. Confirme a ativação do modelo tocando ou clicando em **Ativar** na caixa de diálogo de confirmação.

   ![Caixa de diálogo de confirmação de habilitação](../assets/models-enabling.png)
1. O modelo agora está habilitado e pronto para uso.

   ![Modelo habilitado](../assets/models-enabled.png)

O **Editor do modelo de fragmento de conteúdo** é compatível com vários tipos de dados diferentes, como campos de texto simples, referências de ativos, referências a outros modelos e dados JSON.

Você pode criar vários modelos. Os modelos podem fazer referência a outros fragmentos de conteúdo. Use [configurações](create-configuration.md) para organizar seus modelos.

## Próximas etapas {#next-steps}

Agora que você definiu as estruturas dos Fragmentos de conteúdo criando modelos, poderá seguir para a terceira parte do guia de introdução e [criar pastas onde você armazenará os fragmentos.](create-assets-folder.md)

>[!TIP]
>
>Para obter detalhes completos sobre os Modelos de fragmento de conteúdo, consulte a [documentação dos Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md)
