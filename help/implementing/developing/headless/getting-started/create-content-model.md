---
title: Guia de Start rápido para Criar modelos de fragmento de conteúdo sem cabeçalho
description: Os Modelos de fragmento de conteúdo definem a estrutura do conteúdo que você criará e servirá usando AEM recursos sem cabeçalho.
translation-type: tm+mt
source-git-commit: d37342feb794b9f1385bb5edd38b2d9bb6e7dff9
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# Criando modelos de fragmento de conteúdo Guia de Start rápido sem cabeçalho {#creating-content-fragment-models}

Os Modelos de fragmento de conteúdo definem a estrutura do conteúdo que você criará e servirá usando AEM recursos sem cabeçalho.

## O que são modelos de fragmento de conteúdo? {#what-are-content-fragment-models}

[Agora que você criou uma configuração, ](create-configuration.md) poderá usá-la para criar Modelos de fragmento de conteúdo.

Os Modelos de fragmento de conteúdo definem a estrutura dos dados e do conteúdo que você criará e gerenciará no AEM. Eles servem como uma espécie de andaime para o vosso conteúdo. Ao escolher criar conteúdo, os autores selecionarão entre os Modelos de fragmento de conteúdo que você definir, que os orientará na criação de conteúdo.

## Como criar um modelo de fragmento de conteúdo {#how-to-create-a-content-fragment-model}

Um arquiteto da informação só executaria estas tarefas esporadicamente, uma vez que são necessários novos modelos. Para os fins deste guia de introdução, precisamos apenas criar um modelo.

1. Faça logon AEM como um Cloud Service e, no menu principal, selecione **Ferramentas -> Ativos -> Modelos de fragmento de conteúdo**.
1. Toque ou clique na pasta que foi feita criando sua configuração.

   ![A pasta models](../assets/models-folder.png)
1. Toque ou clique em **Criar**.
1. Forneça um **Título do modelo**, **Tags** e **Descrição**. Você também pode selecionar/desmarcar **Habilitar modelo** para controlar se o modelo é ativado imediatamente após a criação.

   ![Criar um modelo](../assets/models-create.png)
1. Na janela de confirmação, toque ou clique em **Abrir** para configurar o modelo.

   ![Janela de confirmação](../assets/models-confirmation.png)
1. Usando o **Editor do modelo de fragmento de conteúdo**, crie o modelo de fragmento de conteúdo arrastando e soltando campos da coluna **Tipos de dados**.

   ![Arrastar e soltar campos](../assets/models-drag-and-drop.png)

1. Depois de inserir um campo, é necessário configurar suas propriedades. O editor alternará automaticamente para a guia **Propriedades** para o campo adicionado, onde é possível fornecer os campos obrigatórios.

   ![Configurar propriedades](../assets/models-configure-properties.png)
1. Quando terminar de criar seu modelo, toque ou clique em **Salvar**. O modelo recém-criado é salvo no modo **Rascunho**.

   ![Modelo no modo de rascunho](../assets/models-draft.png)
1. O modelo deve ser habilitado para usá-lo (se ainda não estiver ativado). Selecione o modelo que acabou de criar e toque ou clique em **Ativar**.

   ![Ativação do modelo](../assets/models-enable.png)
1. Confirme a habilitação do modelo tocando ou clicando em **Ativar** na caixa de diálogo de confirmação.

   ![Caixa de diálogo de confirmação de ativação](../assets/models-enabling.png)
1. O modelo agora está ativado e pronto para uso.

   ![Modelo habilitado](../assets/models-enabled.png)

O **Editor do modelo de fragmento de conteúdo** oferece suporte a vários tipos de dados diferentes, como campos de texto simples, referências de ativos, referências a outros modelos e dados JSON.

Você pode criar vários modelos. Os modelos podem fazer referência a outros fragmentos de conteúdo. Use [configurações](create-configuration.md) para organizar seus modelos.

## Próximas etapas {#next-steps}

Agora que você definiu as estruturas dos Fragmentos de conteúdo criando modelos, pode seguir para a terceira parte do guia de introdução e [criar pastas onde você armazenará os fragmentos.](create-assets-folder.md)

>[!TIP]
>
>Para obter detalhes completos sobre os Modelos de fragmento de conteúdo, consulte a documentação [Modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md)
