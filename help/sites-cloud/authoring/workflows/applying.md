---
title: Aplicação de fluxos de trabalho a páginas
description: Ao criar, você pode invocar fluxos de trabalho para realizar ações em suas páginas. Também é possível aplicar mais de um fluxo de trabalho.
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Aplicação de fluxos de trabalho a páginas {#applying-workflows-to-pages}

Ao criar, você pode chamar fluxos de trabalho para executar ações em suas páginas; também é possível aplicar mais de um fluxo de trabalho.

Ao aplicar o fluxo de trabalho, você especifica as seguintes informações:

* O fluxo de trabalho que será aplicado.
   * É possível aplicar qualquer fluxo de trabalho (ao qual você tenha acesso, conforme atribuído pelo administrador do AEM).
* Opcionalmente, um título que ajude a identificar a instância de fluxo de trabalho na Caixa de entrada de um usuário..
* A carga útil do fluxo de trabalho. Pode ser uma ou mais páginas.

Fluxos de trabalho podem ser iniciados a partir de:

* [o console **Sites**.](#starting-a-workflow-from-the-sites-console)
* [ao editar uma página, em **Informações da página **](#starting-a-workflow-from-the-page-editor).

>[!NOTE]
>
>Consulte também:
>
>* Como aplicar fluxos de trabalho a ativos do DAM.
>* [Trabalhar com fluxos de trabalho de projeto](/help/sites-cloud/authoring/projects/workflows.md).

<!--
>* [How to apply workflows to DAM assets](/help/assets/assets-workflow.md).
>* [Working with Project Workflows](/help/sites-cloud/authoring/projects/workflows.md).
-->

>[!NOTE]
>
>Os administradores do AEM podem iniciar fluxos de trabalho usando vários outros métodos.
<!--
>AEM administrators can [start workflows using several other methods](/help/sites-administering/workflows-starting.md).
-->

## Início de um fluxo de trabalho no console Sites {#starting-a-workflow-from-the-sites-console}

Você pode iniciar um fluxo de trabalho com:

* [a opção **Criar** da barra de ferramentas Sites](#starting-a-workflow-from-the-sites-toolbar).
* [o painel **Linha do tempo** do console Sites](#starting-a-workflow-from-the-timeline).

Em ambos os casos, é necessário:

* [Especificar os Detalhes do fluxo de trabalho no assistente Criar fluxo de trabalho](#specifying-workflow-details-in-the-create-workflow-wizard).

### Início de um fluxo de trabalho na barra de ferramentas de Sites {#starting-a-workflow-from-the-sites-toolbar}

You can start a workflow from the toolbar of the **Sites** console:

1. Navegue até página desejada e selecione-a.

1. From the **Create** option in the toolbar you can now select **Workflow**.

   ![Criar fluxo de trabalho na barra de ferramentas](/help/sites-cloud/authoring/assets/workflows-create-from-toolbar.png)

1. O assistente **Criar fluxo de trabalho** ajudará você a [especificar os detalhes do fluxo de trabalho](#specifying-workflow-details-in-the-create-workflow-wizard).

### Início de um fluxo de trabalho na Linha do tempo {#starting-a-workflow-from-the-timeline}

Na **Linha do tempo**, você pode iniciar um fluxo de trabalho a ser aplicado ao seu recurso selecionado.

1. [Selecione o recurso](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) e abra a [Linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) (ou abra a Linha do tempo e selecione o recurso).
1. A ponta da seta no campo de comentário pode ser usada para revelar a opção **Iniciar fluxo de trabalho**:

   ![Criar fluxo de trabalho a partir da linha do tempo](/help/sites-cloud/authoring/assets/workflows-create-from-timeline.png)

1. O assistente **Criar fluxo de trabalho** ajudará você a [especificar os detalhes do fluxo de trabalho](#specifying-workflow-details-in-the-create-workflow-wizard).

### Especificar detalhes do fluxo de trabalho no assistente Criar fluxo de trabalho {#specifying-workflow-details-in-the-create-workflow-wizard}

O assistente **Criar fluxo de trabalho** ajudará você a selecionar o fluxo de trabalho e a especificar os detalhes necessários.

Depois de abrir o assistente **Criar fluxo de trabalho** em um destes locais:

* [a opção **Criar** da barra de ferramentas Sites](#starting-a-workflow-from-the-sites-toolbar).
* [o painel **Linha do tempo** do console Sites](#starting-a-workflow-from-the-timeline).

Você pode especificar os detalhes:

1. Na etapa **Propriedades**, as opções básicas do fluxo de trabalho são definidas:

   * **Modelo de fluxo de trabalho**
   * **Título do fluxo de trabalho**

      * Você pode especificar um título para essa instância, para que ele possa ser identificado em um estágio posterior.
   Dependendo do modelo de fluxo de trabalho, as seguintes opções também estão disponíveis. Isso permite que o pacote criado como carga seja mantido após a conclusão do fluxo de trabalho.

   * **Manter o pacote do fluxo de trabalho**
   * **Título do pacote**

      * Você pode especificar um título para o pacote, para ajudar na identificação.
   >[!NOTE]
   >
   >A opção **Manter o pacote do fluxo de trabalho** está disponível quando o fluxo de trabalho foi configurado para Suporte a vários recursos e vários recursos foram selecionados.
   <!--
   >The **Keep workflow package** option is available when the workflow has been configured for [Multi Resource Support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) and multiple resources have been selected.
   -->

   Quando terminar, use **Próximo** para prosseguir.

   ![Especificação das propriedades do fluxo de trabalho](/help/sites-cloud/authoring/assets/workflows-properties.png)

1. Na etapa **Escopo**, você pode selecionar:

   * **Adicionar conteúdo** para abrir o navegador [de](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) caminho e selecionar recursos adicionais; quando estiver no navegador, clique/toque em **Selecionar** para adicionar o conteúdo à instância do fluxo de trabalho.

   * Um recurso existente para ver ações adicionais:

      * **Incluir filhos** para especificar que os filhos desse recurso serão incluídos no fluxo de trabalho.
Uma caixa de diálogo será aberta, permitindo que você refine a seleção de acordo com:

         * Incluir somente filhos imediatos.
         * Incluir somente as páginas modificadas.
         * Incluir somente páginas já publicadas.
         Qualquer filho especificado é adicionado à lista de recursos aos quais o fluxo de trabalho será aplicado.

      * **Remover seleção** para remover esse recurso do fluxo de trabalho.
   ![Definir escopo do fluxo de trabalho](/help/sites-cloud/authoring/assets/workflows-scope.png)

   >[!NOTE]
   >
   >Se você adicionar outros recursos, poderá usar **Voltar** para ajustar a configuração para **Manter o pacote do fluxo de trabalho** na etapa **Propriedades**.

1. Use **Create** to close the wizard and create the workflow instance. Uma notificação é exibida no console Sites.

## Iniciar um fluxo de trabalho no editor de páginas {#starting-a-workflow-from-the-page-editor}

Ao editar uma página, você pode selecionar **Informações da página** na barra de ferramentas. O menu suspenso tem a opção **Iniciar no fluxo de trabalho**. Isso abrirá uma caixa de diálogo na qual você pode especificar o fluxo de trabalho necessário, juntamente com um título, se necessário:

![Iniciar um fluxo de trabalho a partir do editor de páginas](/help/sites-cloud/authoring/assets/workflows-create-page-editor.png)
