---
title: Publicar páginas
description: Como publicar e desfazer a publicação de páginas usando o AEM
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1802'
ht-degree: 71%

---

# Publicar páginas {#publishing-pages}

Depois de criar e revisar seu conteúdo no ambiente de criação, o objetivo é [disponibilizá-lo em seu site público](/help/sites-cloud/authoring/getting-started/concepts.md) (seu ambiente de publicação).

Isso é conhecido como publicação de uma página. Quando você deseja remover uma página do ambiente de publicação, este é o processo de desfazer a publicação. Ao publicar e desfazer a publicação, a página permanece disponível no ambiente do autor para mais alterações até que você a exclua.

Você pode publicar/desfazer a publicação de uma página imediatamente ou em uma data/hora predefinida posteriormente.

>[!NOTE]
>
>A publicação de um fragmento de experiência segue basicamente o mesmo procedimento de publicação de uma página, mas a partir do console ou do editor de fragmentos de experiência.

## Terminologia {#terminology}

É possível encontrar termos diferentes relacionados à publicação ao trabalhar com o Adobe Experience Manager (AEM) as a Cloud Service.

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

Dependendo do local, você pode publicar:

* [No editor de páginas](#publishing-from-the-editor)
* [No console do Sites](#publishing-from-the-console)

>[!NOTE]
>
>Se você não tiver os privilégios necessários para publicar uma página específica:
>
>* Um fluxo de trabalho é acionado para notificar a pessoa apropriada sobre sua solicitação de publicação.
>* Esse fluxo de trabalho pode ter sido personalizado pela sua equipe de desenvolvimento.
>* Uma mensagem é exibida brevemente para notificar que o fluxo de trabalho foi acionado.

>[!NOTE]
>
> Para ver outras possibilidades, consulte **Momento da ativação** e **Momento da desativação** na [guia Básico das Propriedades da página](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)

### Publicação por meio do Editor {#publishing-from-the-editor}

Se você estiver editando uma página, ela poderá ser publicada diretamente do editor.

1. Selecione o ícone **Informações da página** para abrir o menu e depois a opção **Publicar página**.

   ![Publicação de uma página por meio das opções de página](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. Se a página tiver referências que precisam de publicação:

   * A página será publicada diretamente se não houver referências a serem publicadas.
   * Se a página tiver referências que precisam ser publicadas, elas serão listadas no **Publish** assistente, onde é possível:
      * Especificar qual dos ativos/tags/etc. você deseja publicar junto com a página. Em seguida, use **Publicar** para concluir o processo.
      * Usar a opção **Cancelar** para suspender a ação.

   ![Publicação de referências com a página](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Se você selecionar **Publicar**, replicará a página no ambiente de publicação. No editor de páginas, um banner de informações é mostrado confirmando a ação de publicação.

   ![Banner de informações do status de publicação](/help/sites-cloud/authoring/assets/publishing-info.png)

   Ao visualizar a mesma página no console, o status da publicação atualizada estará visível.

   ![Status de publicação da página na exibição de coluna no console Sites](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>A publicação por meio do editor é um processo superficial, ou seja, somente as páginas selecionadas são publicadas, sem incluir páginas filhas.

>[!NOTE]
>
>Páginas acessadas por [pseudônimos](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced) no editor não podem ser publicadas. As opções de publicação no editor só estão disponíveis para páginas acessadas por meio de seus caminhos reais.

### Publicação por meio do Console {#publishing-from-the-console}

No console Sites, há duas opções para publicação:

* [Publicação rápida   ](#quick-publish)
* [Gerenciar publicação   ](#manage-publication)

#### Publicação rápida    {#quick-publish}

A **Publicação rápida** serve para casos simples e publica as páginas selecionadas imediatamente, sem qualquer outra interação. Por esse motivo, todas as referências não publicadas também serão publicadas automaticamente.

Para publicar uma página com a Publicação rápida:

1. Selecione as páginas no console de sites e clique no botão **Publicação rápida**.

   ![Seleção de páginas para publicação](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Na caixa de diálogo Publicação rápida, confirme a publicação clicando em **Publicar** ou cancele clicando em **Cancelar**. Lembre-se de que todas as referências não publicadas também serão publicadas automaticamente.

   ![Confirmação de publicação rápida](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. Quando a página é publicada, um alerta é exibido confirmando a publicação.

>[!NOTE]
>
>A Publicação rápida é uma publicação superficial, ou seja, somente as páginas selecionadas são publicadas, sem incluir páginas secundárias.

#### Gerenciar publicação    {#manage-publication}

**Gerenciar publicação** oferece mais opções do que **Publicação rápida**, permitindo a inclusão de páginas secundárias, a personalização das referências, o início de qualquer fluxo de trabalho aplicável e a oferta da opção de publicação em uma data posterior.

Para publicar ou desfazer a publicação de uma página usando Gerenciar publicação:

1. Selecione as páginas no console Sites e clique no botão **Gerenciar publicação**.

   ![Seleção de páginas para publicação](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. O assistente para **Gerenciar publicação** é iniciado. A primeira etapa, **Opções**, permite fazer o seguinte:

   * **Ação**

     Optar por publicar ou desfazer a publicação de páginas selecionadas.

   * **Programação**

     Escolha executar essa ação agora ou em uma data posterior.

     Publicar mais tarde inicia um fluxo de trabalho para publicar a(s) página(s) selecionada(s) no horário especificado. Por outro lado, desfazer a publicação mais tarde inicia um fluxo de trabalho para desfazer a publicação das páginas selecionadas em um momento específico.

     >[!NOTE]
     >
     >Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o [Console do Fluxo de trabalhos](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) para encerrar o fluxo de trabalho correspondente.

   ![Gerenciar opções de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. Clique em **Avançar** para continuar.

1. Na próxima etapa do assistente Gerenciar publicação, **Escopo**, você pode definir o escopo da publicação ou do cancelamento da publicação, por exemplo, incluindo páginas filhas e/ou referências.

   ![Gerenciar escopo de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **Adicionar conteúdo**

   Você pode usar o botão **Adicionar conteúdo** para adicionar outras páginas à lista de páginas a serem publicadas caso tenha se esquecido de selecionar uma antes de iniciar o assistente para Gerenciar publicação.

   Selecionar o botão **Adicionar conteúdo** inicia o [navegador de caminho](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) para permitir a seleção de conteúdo.

   Escolha as páginas desejadas e clique em **Selecionar** para adicionar o conteúdo ao assistente ou em **Cancelar** para cancelar a seleção e retornar ao assistente.

   **Remover seleção**

   De volta ao assistente, é possível selecionar um item na lista para removê-lo da seleção.

   ![Gerenciar páginas de seleção de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Referências publicadas**

   É possível visualizar e modificar as referências a serem publicadas ou não para uma página. Basta selecionar a referência desejada e clicar no botão **Referências publicadas**.

   ![Gerenciar opções de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   A caixa de diálogo **Referências publicadas** exibe as referências para o conteúdo selecionado. Por padrão, todas elas são selecionadas e publicadas/não publicadas, mas você pode desmarcá-las para desmarcá-las e evitar que elas sejam incluídas na ação.

   Clique em **Concluído** para salvar suas alterações ou em **Cancelar** para cancelar a seleção e retornar ao assistente.

   De volta ao assistente, o **Referências** A coluna é atualizada para refletir sua seleção de referências a serem publicadas ou não publicadas.

   ![Gerenciar páginas de seleção de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Incluir secundárias**

   >[!NOTE]
   >
   >Consulte [Publicar e desfazer publicação de uma árvore](#publishing-and-unpublishing-a-tree)

   Clicar em **Incluir secundárias** abre uma caixa de diálogo que permite:

   * **Incluir secundárias**
   * **Incluir somente secundárias imediatas**
   * **Incluir somente as páginas modificadas**
   * **Incluir somente páginas já publicadas**

   Ative as opções necessárias e confirme com **OK** para adicionar as páginas secundárias à lista de páginas a serem publicadas ou não, com base nas opções de seleção. Clique em **Cancelar** para cancelar a seleção e retornar ao assistente.

   ![Gerenciar publicação incluindo filhos](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. Clique em **Publicar** para concluir.

   De volta ao console de sites, uma mensagem de notificação confirmará a publicação.

1. Se as páginas publicadas estiverem associadas a fluxos de trabalho, elas poderão ser exibidas em uma etapa final de **Fluxos de trabalho** do assistente de publicação.

   ![Gerenciar páginas de seleção de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >A variável **Fluxos de trabalho** A etapa é mostrada com base em quais direitos seu usuário pode ou não ter. Consulte a observação anterior nesta página sobre privilégios de publicação e Gerenciamento de acesso a fluxos de trabalho e [Aplicação de fluxos de trabalho a páginas](/help/sites-cloud/authoring/workflows/applying.md) para obter detalhes.

   Os recursos são agrupados pelos workflows acionados e cada opção fornecida para:

   * Defina o título do workflow.
   * Manter o pacote de fluxo de trabalho, desde que o fluxo de trabalho tenha suporte para vários recursos.
   * Definir um título do pacote de fluxo de trabalho se a opção para manter esse pacote tiver sido escolhida.

1. Clique em **Publicar** ou **Publicar mais tarde** para concluir a publicação.

## Desfazer a publicação de páginas {#unpublishing-pages}

Desfazer a publicação de uma página fará com que ela seja removida do seu ambiente de publicação ou [pré-visualização](/help/sites-cloud/authoring/fundamentals/previewing-content.md), deixando de estar disponível aos seus leitores.

De uma [maneira semelhante à publicação](#publishing-pages), uma ou mais páginas podem ter a publicação desfeita do destino desejado:

* [No editor de páginas](#unpublishing-from-the-editor)
* [Do console do Sites](#unpublishing-from-the-console)

### Desfazer a publicação por meio do editor    {#unpublishing-from-the-editor}

Ao editar uma página, se quiser desfazer a publicação, selecione **Desfazer a publicação da página** no menu **Informações da página**, da mesma maneira que faria para [publicar essa página](#publishing-from-the-editor).

>[!NOTE]
>
>Páginas acessadas por [pseudônimos](/help/sites-cloud/authoring/fundamentals/page-properties.md#advanced) no editor não podem ter a publicação desfeita. As opções de publicação no editor só estão disponíveis para páginas acessadas por meio de seus caminhos reais.

### Desfazer a publicação por meio do Console  {#unpublishing-from-the-console}

Da mesma forma que você [usa a opção Gerenciar publicação para publicar](#manage-publication), também pode usá-la para desfazer a publicação.

1. Selecione as páginas no console Sites e clique no botão **Gerenciar publicação**.
1. O assistente para **Gerenciar publicação** é iniciado. Na primeira etapa, **Opções**, selecione **Desfazer a publicação** em vez da opção padrão **Publicar**.

   ![Desfazer publicação - Opções](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   Da mesma forma que a opção para publicar mais tarde inicia um fluxo de trabalho para publicar essa versão de página no horário especificado, a opção para desativar mais tarde inicia um fluxo de trabalho para desfazer a publicação das páginas selecionadas em um momento específico.

   >[!NOTE]
   >
   >Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o [Console de Fluxos de trabalho](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) para encerrar o fluxo de trabalho correspondente.

   >[!NOTE]
   >Se você tiver um ambiente de [Pré-visualização](/help/sites-cloud/authoring/fundamentals/previewing-content.md), você pode selecionar o **Destino** durante Gerenciar Publicação.

1. Para concluir o cancelamento da publicação, prossiga com o assistente como faria para [publicar a página](#manage-publication).

   ![Desfazer publicação - Escopo](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## Publicar e desfazer a publicação de uma Árvore {#publishing-and-unpublishing-a-tree}

Quando você tiver inserido ou atualizado um número considerável de páginas de conteúdo, todas as quais residem na mesma página raiz, pode ser mais fácil publicar a árvore inteira em uma ação.

Você pode usar o [Gerenciar publicação](#manage-publication) no console de sites para fazer isso.

1. No console Sites, selecione a página raiz da árvore que deseja publicar ou desfazer a publicação e selecione **Gerenciar publicação**.
1. O assistente para **Gerenciar publicação** é iniciado. Opte por publicar ou desfazer a publicação e quando deveria ocorrer e selecione **Próxima** para continuar.
1. No **Escopo** , selecione a página raiz e selecione **Incluir filhos**.

   ![Gerenciar páginas de seleção de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Na caixa de diálogo **Incluir secundárias**:

   * selecione **Incluir secundárias**
   * desmarque **Incluir somente secundárias imediatas**
   * desmarque **Incluir somente páginas já publicadas**
   * configure **Incluir somente as páginas modificadas** como obrigatório

   Essas opções são selecionadas por padrão e, portanto, você deve se lembrar de configurá-las. Confirme a seleção com **OK** para adicionar o conteúdo à publicação ou ao cancelamento da publicação.

   ![Inclusão de secundárias para publicação em árvore](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. No assistente do **Gerenciar publicação**, é possível personalizar ainda mais a seleção adicionando outras páginas ou removendo as selecionadas.

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
