---
title: Publicar páginas
description: Como publicar e desfazer a publicação de páginas usando o AEM
translation-type: tm+mt
source-git-commit: e88a814a901d7fa0da2675fa6017c66d61a73445

---


# Publicar páginas {#publishing-pages}

Depois de criar (e revisar) seu conteúdo no ambiente de criação, o objetivo é [disponibilizá-lo em seu site público ](/help/sites-cloud/authoring/getting-started/concepts.md)(seu ambiente de publicação).

Isso é referido como a publicação de uma página. Quando você deseja remover uma página do ambiente de publicação, este é o processo de desfazer publicação. Ao publicar e desfazer a publicação, a página permanece disponível no ambiente de criação para modificações adicionais até que você a exclua.

Você pode publicar/cancelar a publicação de uma página imediatamente ou em uma data/hora predefinida no futuro.

## Terminologia {#terminology}

Você pode encontrar termos diferentes relacionados à publicação enquanto trabalha com o AEM.

* **Publicar / Não publicar**
   * Esses são os termos principais das ações que tornam o conteúdo publicamente disponível no ambiente de publicação (ou não).
   * Esses são os termos usados na documentação do AEM.
* **Ativar / Desativar**
   * Esses termos são sinônimos de publicar/desfazer a publicação.
   * Esses termos foram usados em versões anteriores do AEM.
* **Replicar / Replicação**
   * Esses são os termos técnicos que descrevem a movimentação de dados (por exemplo, conteúdo da página, arquivos, código, comentários do usuário) de um ambiente para outro ao publicar uma página.
   * Esses termos são usados principalmente por desenvolvedores.

## Publicar páginas {#publishing-pages-1}

Dependendo da sua localização, você pode publicar:

* [Do editor de páginas](#publishing-from-the-editor)
* [Do console de sites](#publishing-from-the-console)

>[!NOTE]
>
>Caso não tenha os privilégios necessários para a publicação de uma página específica:
>
>* Um fluxo de trabalho será acionado para notificar a pessoa adequada sobre a sua solicitação para publicação.
>* Esse fluxo de trabalho pode ter sido personalizado pela sua equipe de desenvolvimento.
>* Uma mensagem será exibida brevemente para notificar que o fluxo de trabalho foi disparado.

<!--
>* This [workflow may have been customized](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) by your development team.
>* A message will be displayed briefly to notify you that the workflow was triggered.
-->

### Publicação por meio do Editor {#publishing-from-the-editor}

Se você estiver editando uma página, ela poderá ser publicada diretamente do editor.

1. Select the **Page Information** icon to open the menu and then the **Publish Page** option.

   ![Publicar uma página por meio de opções de página](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. Se a página tiver referências que precisam de publicação:

   * A página será publicada diretamente se não existirem referências a serem publicadas.
   * Caso a página tenha referências que precisam ser publicadas, elas serão listadas no **Assistente de publicação,** onde é possível:
      * Specify which of the assets/tags/etc. you want to publish together with the page, then use **Publish** to complete the process.
      * Usar a opção **Cancelar** para suspender a ação.
   ![Publicar referências com a página](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Selecting **Publish** will replicate the page to the publish environment. No editor de páginas, será mostrado um banner de informações confirmando a ação de publicação.

   ![Banner de informações de status de publicação](/help/sites-cloud/authoring/assets/publishing-info.png)

   Ao visualizar a mesma página no console, o status da publicação atualizada estará visível.

   ![Status de publicação da página na exibição de coluna no console de sites](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>A publicação do editor é uma publicação superficial, ou seja, somente as páginas selecionadas são publicadas e qualquer página(s) secundária(s) é/não é(são).

### Publicação por meio do Console {#publishing-from-the-console}

No console de sites, existem duas opções para publicação:

* [Publicação rápida](#quick-publish)
* [Gerenciar publicação](#manage-publication)

#### Publicação rápida {#quick-publish}

**A Publicação** rápida é para casos simples e publica as páginas selecionadas imediatamente sem nenhuma interação adicional. Por isso, quaisquer referências não publicadas também serão publicadas automaticamente.

Para publicar uma página com a Publicação rápida:

1. Select the page or pages in the sites console and click on the **Quick Publish** button.

   ![Selecionar páginas para publicação](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. In the Quick Publish dialog, confirm the publication by clicking on **Publish** or cancel by clicking on **Cancel**. Lembre-se de que todas as referências não publicadas também serão publicadas automaticamente.

   ![Confirmação de publicação rápida](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. Quando a página é publicada, é mostrado um alerta confirmando a publicação.

>[!NOTE]
>
>A Publicação rápida é uma publicação superficial, ou seja, apenas as páginas selecionadas são publicadas, sem incluir páginas filhas.

#### Gerenciar publicação {#manage-publication}

**Gerenciar publicação** oferece mais opções do que a Publicação rápida, permitindo a inclusão de páginas secundárias, a personalização das referências e o início de quaisquer fluxos de trabalho aplicáveis, além de oferecer a opção de publicar em uma data posterior.

Para publicar ou desfazer a publicação de uma página usando Gerenciar publicação:

1. Select the page or pages in the sites console and click on the **Manage Publication** button.

   ![Selecionar páginas para publicação](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. The **Manage Publication** wizard starts. The first step, **Options**, allows you to:

   * Optar por publicar ou desfazer a publicação de páginas selecionadas.
   * Optar por realizar a ação agora ou em uma data posterior.
   A publicação posterior inicia um fluxo de trabalho para publicar as páginas selecionadas no horário especificado. Por outro lado, o cancelamento posterior da publicação inicia um fluxo de trabalho para desfazer a publicação das páginas selecionadas em um horário específico.

   Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o console Sites para encerrar o fluxo de trabalho correspondente. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

   ![Gerenciar opções de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

   Clique em **Avançar** para continuar.

1. In the next step of the Manage Publication wizard, **Scope**, you can define the scope of the publication/un-publication such as including to include child pages and/or including references.

   ![Gerenciar escopo de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   You can use the **Add Content** button to add additional pages to the list of pages to be published in case you neglected to select one before starting the Manage Publication wizard.

   Clicar no botão Adicionar conteúdo inicia o [navegador de caminho](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) para permitir a seleção de conteúdo.

   Select the required pages and then click **Select** to add the content to the wizard or **Cancel **to cancel the selection and return to the wizard.

   De volta ao assistente, é possível selecionar um item na lista para configurar suas opções adicionais, como:

   * Incluir seus filhos.
   * Removê-lo da seleção.
   * Gerenciar suas referências publicadas.
   ![Gerenciar publicação selecionando páginas](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   Clicking **Include Children** opens a dialogue allowing you to:

   * Incluir somente filhos imediatos.
   * Incluir somente as páginas modificadas.
   * Incluir somente páginas já publicadas.
   Click **Add** to add the children pages to the list of pages to be published or unpublished based on the selection options. Click **Cancel** to cancel the selection and return to the wizard.

   ![Gerenciar publicação incluindo filhos](/help/sites-cloud/authoring/assets/publishing-include-children.png)

   Ao retornar ao assistente, você verá as páginas adicionadas com base na sua escolha de opções na caixa de diálogo Incluir filhos.

   You can view and modify the references to be published or unpublished for a page by selecting it and then clicking the **Published References** button.

   ![Gerenciar opções de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   The **Published References** dialog displays the references for the selected content. Por padrão, todos estão selecionados e serão publicados/não publicados, mas você pode desmarcá-los para desmarcá-los para que não sejam incluídos na ação.

   Click **Done** to save your changes or **Cancel** to cancel the selection and return to the wizard.

   De volta ao assistente, a coluna **Referências** será atualizada para refletir sua seleção de referências a serem publicadas ou não publicadas.

   ![Gerenciar publicação selecionando páginas](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Click **Publish** to complete.

   De volta ao console de sites, uma mensagem de notificação confirmará a publicação.

1. If the published pages are associated with workflows, they may be shown in a final **Workflows** step of the publication wizard.

   >[!NOTE]
   >
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the previous note on this page regarding publishing privileges as well as Managing Access to Workflows and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   <!--
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the previous note on this page regarding publishing privileges as well as [Managing Access to Workflows](/help/sites-administering/workflows-managing.md) and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   -->

   Os recursos são agrupados pelos fluxos de trabalho acionados e cada uma das opções especificadas para:

   * Definir o título do fluxo de trabalho.
   * Keep the workflow package, provided that the workflow has multi-resource support. <!--Keep the workflow package, provided that the workflow has [multi-resource support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).-->
   * Definir um título do pacote de fluxo de trabalho se a opção para manter esse pacote tiver sido escolhida.
   Click **Publish** or **Publish Later** to complete the publication.

## Desfazer publicação de páginas {#unpublishing-pages}

Desfazer a publicação de uma página fará com que ela seja removida do seu ambiente de publicação, deixando de estar disponível aos seus leitores.

In a [manner similar to publishing](#publishing-pages), one or more pages can be unpublished:

* [Do editor de páginas](#unpublishing-from-the-editor)
* [Do console de sites](#unpublishing-from-the-console)

### Desfazer publicação por meio do editor {#unpublishing-from-the-editor}

Ao editar uma página, se quiser desfazer a sua publicação, selecione **Desfazer publicação da página** no menu **Informações da página**, da mesma maneira que faria para [publicar essa página](#publishing-from-the-editor).

### Desfazer publicação por meio do console {#unpublishing-from-the-console}

Da mesma forma que você [usa a opção Gerenciar publicação para publicar](#manage-publication), também pode usá-la para desfazer a publicação.

1. Select the page or pages in the sites console and click on the **Manage Publication** button.
1. The **Manage Publication** wizard starts. In the first step, **Options**, select to **Unpublish** instead of the default option of **Publish**.

   ![Desfazer publicação](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   Da mesma forma que a opção para publicar mais tarde inicia um fluxo de trabalho para publicar essa versão de página no horário especificado, a opção para desativar mais tarde inicia um fluxo de trabalho para desfazer a publicação das páginas selecionadas em um momento específico.

   Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o console Sites para encerrar o fluxo de trabalho correspondente. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

1. To complete the un-publication, continue through the wizard as you would to [publish the page](#manage-publication).

## Publicar e desfazer publicação de uma árvore {#publishing-and-unpublishing-a-tree}

Ao inserir ou atualizar um número considerável de páginas de conteúdo, todas residentes na mesma página raiz, pode ser mais fácil publicar a árvore inteira em uma única ação.

Você pode usar a opção [Gerenciar publicação](#manage-publication) no console de sites para fazer isso.

1. No console de sites, selecione a página raiz da árvore que você deseja publicar ou desfazer a publicação e depois selecione **Gerenciar publicação**.
1. The **Manage Publication** wizard starts. Opte por publicar ou desfazer a publicação e quando a ação deve ocorrer. Em seguida, selecione **Próximo** para continuar.
1. Na etapa **Escopo**, selecione a página raiz e selecione **Incluir filhos**.

   ![Gerenciar publicação selecionando páginas](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. In the **Include Children** dialogue, un-check the options:

   * Incluir somente filhos imediatos
   * Incluir somente páginas já publicadas
   Essas opções são selecionadas por padrão e, portanto, você deve se lembrar de desmarcá-las. Click **Add** to confirm and add the content to the publication/un-publication.

   ![Incluir filhos ao desfazer a publicação](/help/sites-cloud/authoring/assets/publishing-tree-children.png)

1. O assistente para **Gerenciar publicação** lista o conteúdo da árvore para revisão. Você pode personalizar ainda mais a seleção, adicionando outras páginas ou removendo as selecionadas.

   ![Gerenciar opções de publicação](/help/sites-cloud/authoring/assets/publishing-tree-select.png)

   Remember that you can also review the references to be published via the **Published References** option.

1. [Continue com o assistente Gerenciar publicação como normal](#manage-publication) para concluir a publicação ou desfazer a publicação da árvore.

## Determinação do status de publicação {#determining-publication-status}

Você pode determinar o status de publicação de uma página:

* Nas [informações de visão geral de recursos do console de sites](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   ![Status da publicação na exibição do cartão](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   O status da publicação é mostrado nas exibições [cartão](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view), [coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) e [lista](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view) do console de sites.

* In the [timeline](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   ![Status da publicação na exibição da linha do tempo](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* In the [Page Information menu](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) when editing a page

   ![Status da publicação no menu Informações da página](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
