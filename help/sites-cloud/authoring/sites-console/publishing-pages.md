---
title: Publicar páginas por meio do console Sites
description: Saiba como publicar e desfazer a publicação de suas páginas usando o Console Sites.
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5ad91a32d705ef61e8b9799bf7fb1e136bb8bfa0
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 73%

---


# Publicar páginas por meio do console Sites {#publishing-pages}

Após criar e revisar seu conteúdo no ambiente do autor, o objetivo é [disponibilizá-lo em seu site público](/help/sites-cloud/authoring/author-publish.md) (seu ambiente de publicação).

Isso é chamado de publicação de uma página. Quando você deseja remover uma página do ambiente de publicação, este é o processo de desfazer a publicação. Ao publicar e desfazer a publicação, a página permanece disponível no ambiente do autor para mais alterações até que você a exclua.

Você pode usar o console [**Sites**](/help/sites-cloud/authoring/sites-console/introduction.md) para publicar/desfazer a publicação de uma página imediatamente ou em uma data/hora predefinida no futuro.

>[!TIP]
>
>Você pode publicar de locais diferentes do console Sites.
>
>* [No Editor de Página](/help/sites-cloud/authoring/page-editor/publishing.md)
>* [Do Editor Universal](/help/sites-cloud/authoring/universal-editor/publishing.md)
>* [No console ou editor de Fragmento de Experiência](/help/sites-cloud/authoring/fragments/experience-fragments.md)
>
>A publicação a partir desses locais oferece opções diferentes, mas segue procedimentos semelhantes e ideias gerais descritas aqui.

## Terminologia {#terminology}

É possível encontrar termos diferentes relacionados à publicação ao trabalhar com o Adobe Experience Manager (AEM) as a Cloud Service.

* **Publicar/Desfazer a publicação**
   * Esses são os termos principais para as ações que tornam o conteúdo publicamente disponível nos ambientes de publicação e/ou visualização (ou não).
   * Esses são os termos usados na documentação do AEM.
* **Ativar / Desativar**
   * Estes termos são sinônimos de publicar/desfazer a publicação.
   * Esses termos foram usados nas versões anteriores do AEM.
* **Replicar / Replicação**
   * Esses são os termos técnicos que descrevem a movimentação de dados (por exemplo, conteúdo da página, arquivos, código, comentários do usuário) de um serviço para outro ao publicar uma página (por exemplo, do autor para a pré-visualização).
   * Esses termos são usados principalmente pelos desenvolvedores.

>[!NOTE]
>
>Se você não tiver os privilégios necessários para publicar uma página específica:
>
>* Um fluxo de trabalho é acionado para notificar a pessoa apropriada sobre sua solicitação de publicação.
>* Esse fluxo de trabalho pode ter sido personalizado pela sua equipe de desenvolvimento.
>* Uma mensagem é exibida brevemente para notificá-lo de que o fluxo de trabalho foi acionado.

>[!NOTE]
>
>Para preservar a ordem das páginas, use a opção [Gerenciar publicação](#manage-publication) para publicar a página pai junto com qualquer página filho em uma única ação.
>
>A ordem das páginas não é garantida:
>
>* Se apenas as páginas secundárias forem selecionadas para publicação (já que as informações da ordem são mantidas na página principal)
>* Se as páginas principal e secundária forem publicadas em ações separadas

## Publicar páginas por meio do console Sites {#publishing-from-the-sites-console}

No console **Sites**, há duas opções para publicação:

* [Publicação rápida   &#x200B;](#quick-publish)
* [Gerenciar publicação   &#x200B;](#manage-publication)

### Publicação rápida    {#quick-publish}

A **Publicação rápida** serve para casos simples e publica as páginas selecionadas imediatamente, sem qualquer outra interação. Por esse motivo, qualquer referências que ainda não tiver sido publicada, será automaticamente.

Para publicar uma página com a Publicação rápida:

1. Selecione as páginas no console de sites e clique no botão **Publicação rápida**.

   ![Seleção de páginas para publicação](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Na caixa de diálogo Publicação rápida, confirme a publicação clicando em **Publicar** ou cancele clicando em **Cancelar**. Lembre-se de que todas as referências não publicadas também serão publicadas automaticamente.

   ![Confirmação de publicação rápida](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. Quando a página é publicada, um alerta é exibido confirmando a publicação.

>[!NOTE]
>
>A Publicação rápida é uma publicação superficial, ou seja, somente a(s) página(s) selecionada(s) é(são) publicada(s), mas qualquer página filha que houver não será.

### Gerenciar publicação    {#manage-publication}

**Gerenciar Publicação** oferece mais opções do que **Publicação Rápida**, permitindo a inclusão de páginas secundárias, a personalização das referências, a publicação em um serviço de visualização (se disponível), o início de qualquer fluxo de trabalho aplicável e a opção de publicação em uma data posterior.

Para publicar ou desfazer a publicação de uma página usando Gerenciar publicação:

1. Selecione as páginas no console de sites e clique no botão **Gerenciar publicação**.

   ![Seleção de páginas para publicação](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. O assistente para **Gerenciar publicação** é iniciado. A primeira etapa, **Opções**, permite:

   * **Ação**

     Optar por publicar ou desfazer a publicação de páginas selecionadas.

   * **Destino**

     Escolha se deseja publicar no serviço de publicação (padrão) ou no serviço de visualização. Disponível somente se você tiver um [serviço de visualização configurado.](/help/sites-cloud/authoring/sites-console/previewing-content.md)

   * **Programação**

     Escolha executar essa ação agora ou em uma data posterior.

     Publicar mais tarde inicia um fluxo de trabalho para publicar a(s) página(s) selecionada(s) no horário especificado. Por outro lado, desfazer a publicação mais tarde inicia um fluxo de trabalho para desfazer a publicação da(s) página(s) selecionada(s) no horário especificado.

     >[!TIP]
     >
     >Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o [Console do Fluxo de trabalhos](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) para encerrar o fluxo de trabalho correspondente.

     >[!TIP]
     >
     >O agendamento de conteúdo para publicação replica o conteúdo e respeita os workflows de publicação. Se quiser ocultar temporariamente o conteúdo já publicado sem desfazer a publicação, considere o [**Momento da ativação** e o **Momento da desativação** disponíveis nas propriedades da página.](/help/sites-cloud/authoring/sites-console/page-properties.md#basic)

   ![Gerenciar opções de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. Clique em **Avançar** para continuar.

1. Na próxima etapa do assistente Gerenciar publicação, **Escopo**, você pode definir o escopo da publicação ou do cancelamento da publicação, por exemplo, incluindo páginas filhas e/ou referências.

   ![Gerenciar escopo de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **Adicionar conteúdo**

   Você pode usar o botão **Adicionar conteúdo** para adicionar outras páginas à lista de páginas a serem publicadas caso tenha se esquecido de selecionar uma antes de iniciar o assistente para Gerenciar publicação.

   Selecionar o botão **Adicionar conteúdo** inicia o [navegador de caminho](/help/sites-cloud/authoring/path-selection.md) para permitir a seleção de conteúdo.

   Escolha as páginas desejadas e clique em **Selecionar** para adicionar o conteúdo ao assistente ou em **Cancelar** para cancelar a seleção e retornar ao assistente.

   **Remover seleção**

   De volta ao assistente, é possível selecionar um item na lista para removê-lo da seleção.

   ![Gerenciar páginas de seleção de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Referências publicadas**

   É possível visualizar e modificar as referências a serem publicadas ou não para uma página. Basta selecionar a referência desejada e clicar no botão **Referências publicadas**.

   ![Gerenciar opções de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   A caixa de diálogo **Referências publicadas** exibe as referências para o conteúdo selecionado. Por padrão, todas elas estarão selecionadas e serão publicadas/desfarão a publicação, mas é possível desmarcá-las para que não sejam incluídas na ação.

   Clique em **Concluído** para salvar suas alterações ou em **Cancelar** para cancelar a seleção e retornar ao assistente.

   De volta ao assistente, a coluna **Referências** é atualizada para refletir sua seleção de referências que serão publicadas ou que terão a publicação desfeita.

   ![Gerenciar publicação seleção de páginas](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Incluir filhos**

   >[!NOTE]
   >
   >Consulte [Publicar e desfazer publicação de uma árvore](#publishing-and-unpublishing-a-tree)

   Clicar em **Incluir filhos** abre uma caixa de diálogo que permite:

   * **Incluir filhos**
   * **Incluir somente filhos imediatos**
   * **Incluir somente as páginas modificadas**
   * **Incluir somente páginas já publicadas**

   Ative as opções necessárias e confirme com **OK** para adicionar as páginas filhas à lista de páginas a serem publicadas ou não, com base nas opções de seleção. Clique em **Cancelar** para cancelar a seleção e retornar ao assistente.

   ![Gerenciar publicação incluindo filhos](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. Clique em **Publicar** para concluir.

   De volta ao console de sites, uma mensagem de notificação confirmará a publicação.

1. Se as páginas publicadas estiverem associadas a fluxos de trabalho, elas poderão ser exibidas em uma etapa final de **Fluxos de trabalho** do assistente de publicação.

   ![Gerenciar páginas de seleção de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >A etapa **Fluxos de trabalho** é mostrada com base nos direitos que seu usuário pode ou não ter. Para obter detalhes, consulte a nota anterior nesta página sobre privilégios de publicação e Gerenciamento de acesso a fluxos de trabalho e [Aplicação de fluxos de trabalho a páginas](/help/sites-cloud/authoring/workflows/applying.md).

   Os recursos são agrupados pelos workflows acionados e cada um recebe opções para:

   * Defina o título do fluxo de trabalho.
   * Manter o pacote de fluxo de trabalho, desde que o fluxo de trabalho tenha suporte para vários recursos.
   * Definir um título do pacote de fluxo de trabalho se a opção para manter esse pacote tiver sido escolhida.

1. Clique em **Publicar** ou **Publicar mais tarde** para concluir a publicação.

## Desfazer a publicação de páginas {#unpublishing-pages}

Desfazer a publicação de uma página fará com que ela seja removida do seu ambiente de publicação ou [visualização](/help/sites-cloud/authoring/sites-console/previewing-content.md), deixando de estar disponível aos seus leitores.

Da mesma forma que você [usa a opção Gerenciar publicação para publicar](#manage-publication), também pode usá-la para desfazer a publicação.

1. Selecione as páginas no console de sites e clique no botão **Gerenciar publicação**.
1. O assistente para **Gerenciar publicação** é iniciado. Na primeira etapa, **Opções**, selecione **Desfazer a publicação** em vez da opção padrão **Publicar**.

   ![Desfazer publicação - Opções](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   Da mesma forma que a opção para publicar mais tarde inicia um fluxo de trabalho para publicar essa versão de página no horário especificado, a opção para desativar mais tarde inicia um fluxo de trabalho para desfazer a publicação das páginas selecionadas em um momento específico.

   >[!NOTE]
   >
   >Caso deseje cancelar a publicação/desfazer a publicação mais tarde, acesse o [Console de Fluxos de trabalho](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) para encerrar o fluxo de trabalho correspondente.

   >[!NOTE]
   >Se você tiver um ambiente de [Pré-visualização](/help/sites-cloud/authoring/sites-console/previewing-content.md), você pode selecionar o **Destino** durante Gerenciar Publicação.

1. Para concluir o cancelamento da publicação, prossiga com o assistente como faria para [publicar a página](#manage-publication).

   ![Desfazer publicação - Escopo](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## Publicar e desfazer a publicação de uma Árvore {#publishing-and-unpublishing-a-tree}

Quando você tiver inserido ou atualizado um número considerável de páginas de conteúdo, todas residentes na mesma página raiz, pode ser mais fácil publicar toda a árvore em uma única ação.

É possível usar a opção [Gerenciar publicação](#manage-publication) no console do Sites para fazer isso.

1. No console Sites, selecione a página raiz da árvore que deseja publicar ou desfazer a publicação e selecione **Gerenciar Publicação**.
1. O assistente para **Gerenciar publicação** é iniciado. Escolha publicar ou desfazer a publicação e quando isso deve ocorrer e selecione **Próximo** para continuar.
1. Na etapa **Escopo**, selecione a página raiz e selecione **Incluir filhas**.

   ![Gerenciar páginas de seleção de publicação](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Na caixa de diálogo **Incluir filhos**:

   * selecione **Incluir filhos**
   * desmarque **Incluir somente filhos imediatos**
   * desmarque **Incluir somente páginas já publicadas**
   * configure **Incluir somente as páginas modificadas** como obrigatório

   Essas opções são selecionadas por padrão e, portanto, você deve se lembrar de configurá-las. Confirme a seleção com **OK** para adicionar o conteúdo à publicação ou ao cancelamento da publicação.

   ![Inclusão de filhos para publicação em árvore](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. No assistente do **Gerenciar publicação**, é possível personalizar ainda mais a seleção adicionando outras páginas ou removendo as selecionadas.

   Lembre-se de que você também pode rever as referências a serem publicadas por meio da opção **Referências publicadas**.

1. [Prossiga com o assistente Gerenciar publicação como de costume](#manage-publication) para concluir a publicação ou o cancelamento da publicação da árvore.

## Determinação do status de publicação {#determining-publication-status}

Você pode determinar o status de publicação de uma página:

* Nas [informações de visão geral de recursos do console de sites](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)

  ![Status da publicação na exibição de cartão](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

  O status da publicação é mostrado nas exibições [cartão](/help/sites-cloud/authoring/basic-handling.md#card-view), [coluna](/help/sites-cloud/authoring/basic-handling.md#column-view) e [lista](/help/sites-cloud/authoring/basic-handling.md#list-view) do console de sites.

* Na [linha do tempo](/help/sites-cloud/authoring/basic-handling.md#timeline)

  ![Status da publicação na exibição de linha do tempo](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* No menu [Informações da página](/help/sites-cloud/authoring/page-editor/introduction.md#page-information), ao editar uma página

  ![Status da publicação no menu Informações da página](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
