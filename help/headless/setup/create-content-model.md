---
title: Criação de modelos de fragmento de conteúdo - Configuração do headless
description: Defina a estrutura do conteúdo que será criado e veiculado usando os recursos headless do AEM, através de modelos de fragmento de conteúdo.
exl-id: 8e3e4d00-34d3-4d4f-bc3a-43b8a322b986
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 88%

---

# Criação de modelos de fragmento de conteúdo - Configuração do headless {#creating-content-fragment-models}

Defina a estrutura do conteúdo que será criado e veiculado usando os recursos headless do AEM, através de modelos de fragmento de conteúdo.

## O que são modelos de fragmento de conteúdo? {#what-are-content-fragment-models}

[Agora que você criou uma configuração,](create-configuration.md) é possível usá-la para criar modelos de fragmento de conteúdo.

Os modelos de fragmento de conteúdo definem a estrutura dos dados e do conteúdo que você irá criar e gerenciar no AEM. Eles servem como uma espécie de andaime para o conteúdo. Ao optar por criar o conteúdo, os autores escolherão entre os modelos de fragmento de conteúdo definidos, que os orientarão na criação do conteúdo.

## Como criar um modelo de fragmento de conteúdo {#how-to-create-a-content-fragment-model}

Um arquiteto de informações executaria essas tarefas apenas esporadicamente, à medida que novos modelos se tornassem necessários. Para os propósitos deste guia de introdução, precisamos criar apenas um modelo.

1. Faça logon no AEM as a Cloud Service e, no menu principal, selecione **Ferramentas** -> **Geral** -> **Modelos de fragmento de conteúdo**.
1. Selecione a pasta que foi criada com sua configuração.

   ![A pasta de modelos](../assets/models-folder.png)
1. Selecione **Criar**.
1. Forneça o **Título do modelo**, as **Tags** e a **Descrição**. Também é possível marcar/desmarcar a opção **Ativar modelo** para controlar se o modelo é habilitado imediatamente após a criação.

   ![Criar um modelo](../assets/models-create.png)
1. Na janela de confirmação, selecione **Abrir** para configurar seu modelo.

   ![Janela de confirmação](../assets/models-confirmation.png)
1. Usando o **Editor de modelos de fragmentos de conteúdo**, crie o modelo de fragmento de conteúdo arrastando e soltando campos da coluna **Tipos de dados**.

   ![Arrastar e soltar campos](../assets/models-drag-and-drop.png)

1. Depois de colocar um campo, você deve configurar suas propriedades. O editor alternará automaticamente para a guia **Propriedades** do campo adicionado, onde é possível fornecer os campos obrigatórios.

   ![Configurar propriedades](../assets/models-configure-properties.png)

1. Quando terminar de criar o modelo, selecione **Salvar**.

1. O modo do modelo criado depende de se você selecionou **Habilitar Modelo** ao criar o modelo:
   * selecionada - o novo modelo já estará **habilitado**
   * não selecionada - o novo modelo será criado em modo de **Rascunho**

1. Se ainda não estiver, o modelo deve ser **habilitado** para ser usado.
   1. Selecione o modelo criado e selecione **Habilitar**.

      ![Habilitação do modelo](../assets/models-enable.png)
   1. Confirme a habilitação do modelo tocando ou clicando em **Habilitar** na caixa de diálogo de confirmação.

      ![Caixa de diálogo de confirmação de habilitação](../assets/models-enabling.png)
1. O modelo agora está habilitado e pronto para uso.

   ![Modelo habilitado](../assets/models-enabled.png)

O **Editor de Modelos de fragmentos de conteúdo** é compatível com vários tipos de dados diferentes, como campos de texto simples, referências de ativos, referências a outros modelos e dados JSON.

É possível criar vários modelos. Os modelos podem fazer referência a outros fragmentos de conteúdo. Use as [configurações](create-configuration.md) para organizar seus modelos.

## Próximas etapas {#next-steps}

Agora que você definiu as estruturas dos fragmentos de conteúdo criando modelos, poderá seguir para a terceira parte do guia de introdução e [criar pastas onde armazenará os fragmentos.](create-assets-folder.md)

>[!TIP]
>
>Para obter detalhes completos sobre os modelos de fragmento de conteúdo, consulte a [documentação dos Modelos de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
