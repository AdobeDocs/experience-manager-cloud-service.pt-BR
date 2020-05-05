---
title: Publicar páginas
description: Como publicar e desfazer a publicação de páginas usando o AEM
translation-type: ht
source-git-commit: f04dd39a5a22f44f976f2e473689780099f10f9a

---


# Publicar páginas {#publishing-pages}

Depois de criar (e revisar) seu conteúdo no ambiente de criação, o objetivo é [disponibilizá-lo em seu site público ](/help/sites-cloud/authoring/getting-started/concepts.md)(seu ambiente de publicação).

Isso é referido como a publicação de uma página. Quando você deseja remover uma página do ambiente de publicação, este é o processo de desfazer a publicação. Ao publicar e desfazer a publicação, a página permanece disponível no ambiente de criação para modificações adicionais até que você a exclua.

Você pode publicar/desfazer a publicação de uma página imediatamente ou em uma data/hora predefinida posteriormente.

## Terminologia {#terminology}

Você pode encontrar termos diferentes relacionados à publicação enquanto trabalha com o AEM.

* **Publicar/Desfazer a publicação**
   * Esses são os termos principais para as ações que tornam o conteúdo publicamente disponível no ambiente de publicação (ou não).
   * Esses são os termos usados na documentação do AEM.
* **Ativar / Desativar**
   * Estes termos são sinônimos de publicar/desfazer a publicação.
   * Esses termos foram usados nas versões anteriores do AEM.
* **Replicar / Replicação**
   * Esses são os termos técnicos que descrevem a movimentação de dados (por exemplo, conteúdo da página, arquivos, código, comentários do usuário) de um ambiente para outro ao publicar uma página.
   * Esses termos são usados principalmente pelos desenvolvedores.

## Publicar páginas {#publishing-pages-1}

Dependendo da sua localização, você pode publicar:

* [No editor de páginas](#publishing-from-the-editor)
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

1. Selecione o ícone **Informações da página** para abrir o menu e depois a opção **Publicar página**.

   ![Publicação de uma página por meio das opções de página](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. Se a página tiver referências que precisam de publicação:

   * A página será publicada diretamente se não existirem referências a serem publicadas.
   * Caso a página tenha referências que precisam ser publicadas, elas serão listadas no **Assistente de publicação,** onde é possível:
      * Especificar qual dos ativos/tags/etc. você deseja publicar junto com a página. Em seguida, use **Publicar** para concluir o processo.
      * Usar a opção **Cancelar** para suspender a ação.
   ![Publicação de referências com a página](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Se você selecionar **Publicar**, replicará a página no ambiente de publicação. No editor de páginas, será mostrado um banner de informações confirmando a ação de publicação.

   ![Banner de informações do status de publicação](/help/sites-cloud/authoring/assets/publishing-info.png)

   Ao visualizar a mesma página no console, o status da publicação atualizada estará visível.

   ![Status de publicação da página na exibição de coluna no console Sites](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>A publicação por meio do Editor é um processo superficial, ou seja, apenas as páginas selecionadas são publicadas, sem incluir páginas filhas.

### Publicação por meio do Console {#publishing-from-the-console}

No console de sites, existem duas opções para publicação:

* [Publicação rápida](#quick-publish)
* [Gerenciar publicação](#manage-publication)

#### Publicação rápida    {#quick-publish}

A **Publicação rápida** serve para casos simples e publica as páginas selecionadas imediatamente, sem qualquer outra interação. Por isso, quaisquer referências não publicadas também serão publicadas automaticamente.

Para publicar uma página com a Publicação rápida:

1. Selecione as páginas no console de sites e clique no botão **Publicação rápida**.

   ![Seleção de páginas para publicação](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Na caixa de diálogo Publicação rápida, confirme a publicação clicando em **Publicar** ou cancele clicando em **Cancelar**. Lembre-se de que todas as referências não publicadas também serão publicadas automaticamente.

   ![Confirmação de publicação rápida](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. Quando a página é publicada, é mostrado um alerta confirmando a publicação.

>[!NOTE]
>
>A Publicação rápida é uma publicação superficial, ou seja, apenas as páginas selecionadas são publicadas, sem incluir páginas filhas.

#### Gerenciar publicação    {#manage-publication}

A opção **Gerenciar publicação** oferece mais opções do que a Publicação rápida, permitindo a inclusão de páginas filhas, a personalização das referências e o início de qualquer fluxo de trabalho aplicável, além de oferecer a opção de publicação em uma data posterior.

Para publicar ou desfazer a publicação de uma página usando Gerenciar publicação:

1. Selecione as páginas no console Sites e clique no botão **Gerenciar publicação**.

   ![Seleção de páginas para publicação](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. O assistente para **Gerenciar publicação** é iniciado. A primeira etapa, **Opções**, permite fazer o seguinte:

   * Optar por publicar ou desfazer a publicação de páginas selecionadas.
   * Optar por realizar a ação agora ou em uma data posterior.
   A publicação posterior inicia um fluxo de trabalho para publicar as páginas selecionadas no horário especificado. Por outro lado, o cancelamento posterior da publicação inicia um fluxo de trabalho para desfazer a publicação das páginas selecionadas em um horário específico.

   Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o console Sites para encerrar o fluxo de trabalho correspondente. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

   ![Gerenciar opções de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

   Clique em **Avançar** para continuar.

1. Na próxima etapa do assistente Gerenciar publicação, **Escopo**, você pode definir o escopo da publicação ou do cancelamento da publicação, por exemplo, incluindo páginas filhas e/ou referências.

   ![Gerenciar escopo de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   Você pode usar o botão **Adicionar conteúdo** para adicionar outras páginas à lista de páginas a serem publicadas caso tenha se esquecido de selecionar uma antes de iniciar o assistente para Gerenciar publicação.

   Clicar no botão Adicionar conteúdo inicia o [navegador de caminho](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) para permitir a seleção de conteúdo.

   Escolha as páginas necessárias e clique em **Selecionar** para adicionar o conteúdo ao assistente ou em **Cancelar** para cancelar a seleção e retornar ao assistente.

   De volta ao assistente, é possível selecionar um item na lista para configurar suas opções adicionais, como:

   * Incluir seus filhos.
   * Removê-lo da seleção.
   * Gerenciar suas referências publicadas.
   ![Gerenciar páginas de seleção de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   Clicar em **Incluir filhos** abre uma caixa de diálogo que permite:

   * Incluir somente filhos imediatos.
   * Incluir somente as páginas modificadas.
   * Incluir somente páginas já publicadas.
   Clique em **Adicionar** para adicionar as páginas filhas à lista de páginas a serem publicadas ou não, com base nas opções de seleção. Clique em **Cancelar** para cancelar a seleção e retornar ao assistente.

   ![Gerenciar publicação incluindo filhos](/help/sites-cloud/authoring/assets/publishing-include-children.png)

   Ao retornar ao assistente, você verá as páginas adicionadas com base na sua escolha de opções na caixa de diálogo Incluir filhos.

   É possível visualizar e modificar as referências a serem publicadas ou não para uma página. Basta selecionar a referência desejada e clicar no botão **Referências publicadas**.

   ![Gerenciar opções de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   A caixa de diálogo **Referências publicadas** exibe as referências para o conteúdo selecionado. Por padrão, todas elas são selecionadas e serão publicadas/não publicadas, mas você pode desmarcá-las para desativá-las e evitar que elas sejam incluídas na ação.

   Clique em **Concluído** para salvar suas alterações ou em **Cancelar** para cancelar a seleção e retornar ao assistente.

   De volta ao assistente, a coluna **Referências** será atualizada para refletir sua seleção de referências a serem publicadas ou não publicadas.

   ![Gerenciar páginas de seleção de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Clique em **Publicar** para concluir.

   De volta ao console de sites, uma mensagem de notificação confirmará a publicação.

1. Se as páginas publicadas estiverem associadas a fluxos de trabalho, elas poderão ser exibidas em uma etapa final de **Fluxos de trabalho** do assistente de publicação.

   >[!NOTE]
   >
   >A etapa **Fluxos de trabalho** será mostrada com base em quais direitos seu usuário pode ou não possuir. Para obter detalhes, consulte a observação anterior nesta página sobre privilégios de publicação, além dos tópicos Gerenciamento do acesso a fluxos de trabalho e [Aplicação de fluxos de trabalho a páginas](/help/sites-cloud/authoring/workflows/applying.md).
   <!--
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the previous note on this page regarding publishing privileges as well as [Managing Access to Workflows](/help/sites-administering/workflows-managing.md) and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   -->

   Os recursos são agrupados pelos fluxos de trabalho acionados e cada uma das opções especificadas para:

   * Definir o título do fluxo de trabalho.
   * Manter o pacote de fluxo de trabalho, desde que o fluxo de trabalho tenha suporte para vários recursos.
   <!--Keep the workflow package, provided that the workflow has [multi-resource support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).
    -->

   * Definir um título do pacote de fluxo de trabalho se a opção para manter esse pacote tiver sido escolhida.
   Clique em **Publicar** ou **Publicar mais tarde** para concluir a publicação.

## Desfazer a publicação de páginas {#unpublishing-pages}

Desfazer a publicação de uma página fará com que ela seja removida do seu ambiente de publicação, deixando de estar disponível aos seus leitores.

De uma [maneira semelhante à publicação](#publishing-pages), uma ou mais páginas podem ter a publicação desfeita:

* [No editor de páginas](#unpublishing-from-the-editor)
* [Do console de sites](#unpublishing-from-the-console)

### Desfazer a publicação por meio do editor    {#unpublishing-from-the-editor}

Ao editar uma página, se quiser desfazer a publicação, selecione **Desfazer a publicação da página** no menu **Informações da página**, da mesma maneira que faria para [publicar essa página](#publishing-from-the-editor).

### Desfazer a publicação por meio do Console  {#unpublishing-from-the-console}

Da mesma forma que você [usa a opção Gerenciar publicação para publicar](#manage-publication), também pode usá-la para desfazer a publicação.

1. Selecione as páginas no console Sites e clique no botão **Gerenciar publicação**.
1. O assistente para **Gerenciar publicação** é iniciado. Na primeira etapa, **Opções**, selecione **Desfazer a publicação** em vez da opção padrão **Publicar**.

   ![Desfazer a publicação](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   Da mesma forma que a opção para publicar mais tarde inicia um fluxo de trabalho para publicar essa versão de página no horário especificado, a opção para desativar mais tarde inicia um fluxo de trabalho para desfazer a publicação das páginas selecionadas em um momento específico.

   Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o console Sites para encerrar o fluxo de trabalho correspondente. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

1. Para concluir o cancelamento da publicação, prossiga com o assistente como faria para [publicar a página](#manage-publication).

## Publicar e desfazer a publicação de uma Arvore {#publishing-and-unpublishing-a-tree}

Ao inserir ou atualizar um número considerável de páginas de conteúdo, todas residentes na mesma página raiz, pode ser mais fácil publicar a árvore inteira em uma única ação.

Você pode usar a opção [Gerenciar publicação](#manage-publication) no console de sites para fazer isso.

1. No console de sites, selecione a página raiz da árvore que você deseja publicar ou desfazer a publicação e depois selecione **Gerenciar publicação**.
1. O assistente para **Gerenciar publicação** é iniciado. Opte por publicar ou desfazer a publicação e quando a ação deve ocorrer. Em seguida, selecione **Próximo** para continuar.
1. Na etapa **Escopo**, selecione a página raiz e selecione **Incluir filhos**.

   ![Gerenciar páginas de seleção de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Na caixa de diálogo **Incluir filhos**, desmarque as opções:

   * Incluir somente filhos imediatos
   * Incluir somente páginas já publicadas
   Essas opções são selecionadas por padrão e, portanto, você deve se lembrar de desmarcá-las. Clique em **Adicionar** para confirmar e adicionar o conteúdo à publicação ou ao cancelamento da publicação.

   ![Inclusão de filhos ao desfazer a publicação](/help/sites-cloud/authoring/assets/publishing-tree-children.png)

1. O assistente para **Gerenciar publicação** lista o conteúdo da árvore para revisão. Você pode personalizar ainda mais a seleção, adicionando outras páginas ou removendo as selecionadas.

   ![Gerenciar opções de publicação](/help/sites-cloud/authoring/assets/publishing-tree-select.png)

   Lembre-se de que você também pode rever as referências a serem publicadas por meio da opção **Referências publicadas**.

1. [Prossiga com o assistente Gerenciar publicação como de costume](#manage-publication) para concluir a publicação ou o cancelamento da publicação da árvore.

## Determinação do status de publicação {#determining-publication-status}

Você pode determinar o status de publicação de uma página:

* Nas [informações de visão geral de recursos do console de sites](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   ![Status da publicação na exibição de cartão](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   O status da publicação é mostrado nas exibições [cartão](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view), [coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) e [lista](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view) do console de sites.

* Na [linha do tempo](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   ![Status da publicação na exibição de linha do tempo](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* No menu [Informações da página](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information), ao editar uma página

   ![Status da publicação no menu Informações da página](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
