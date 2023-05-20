---
title: Participar de fluxos de trabalho
description: Os fluxos de trabalho normalmente incluem etapas que exigem que uma pessoa execute uma atividade em uma página ou ativo.
exl-id: 62192da9-0b5b-4997-9c2b-d1aee04b01f9
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 40%

---

# Participar de fluxos de trabalho {#participating-in-workflows}

Os fluxos de trabalho normalmente incluem etapas que exigem que uma pessoa execute uma atividade em uma página ou ativo. O fluxo de trabalho seleciona um usuário ou grupo para executar a atividade e atribui um item de trabalho a essa pessoa ou grupo. O usuário recebe a notificação e pode realizar a ação apropriada:

* [Visualizar notificações](#notifications-of-available-workflow-actions)
* [Concluir uma etapa do participante](#completing-a-participant-step)
* [Delegar uma etapa do participante](#delegating-a-participant-step)
* [Realizar um retrocesso em uma etapa do participante](#performing-step-back-on-a-participant-step)
* [Abrir um item de fluxo de trabalho para exibir detalhes (e realizar ações)](#opening-a-workflow-item-to-view-details-and-take-actions)
* [Visualizar a carga do fluxo de trabalho (vários recursos)](#viewing-the-workflow-payload-multiple-resources)

## Notificações de ações de fluxo de trabalho disponíveis {#notifications-of-available-workflow-actions}

Quando um item de trabalho é atribuído a você (por exemplo, **Aprovar conteúdo**), vários alertas e/ou notificações são exibidos:

* Seu [notificação](/help/sites-cloud/authoring/getting-started/inbox.md) O indicador (barra de ferramentas) será incrementado:

   ![Barra de ferramentas Notificação](/help/sites-cloud/authoring/assets/workflows-notifications.png)

* O item será listado na sua [Caixa de entrada](/help/sites-cloud/authoring/getting-started/inbox.md) de notificações:

   ![Notificações na caixa de entrada](/help/sites-cloud/authoring/assets/workflows-inbox.png)

* Quando você estiver usando o editor de páginas, a barra de status mostrará:
   * O nome do(s) fluxo(s) de trabalho que está sendo aplicado(s) à página; por exemplo, Solicitação de ativação.
   * Quaisquer ações disponíveis para o usuário atual para a etapa atual do fluxo de trabalho; por exemplo, Concluir, Delegar, Exibir detalhes.
   * O número de workflows aos quais a página está sujeita. É possível:
      * use as setas para a esquerda/direita para navegar pelas informações de status dos vários workflows.
      * clique/toque no número real para abrir uma lista suspensa de todos os fluxos de trabalho aplicáveis e selecione o fluxo de trabalho que deseja exibir na barra de status.

   ![Página com vários workflows](/help/sites-cloud/authoring/assets/workflows-multiple.png)

   >[!NOTE]
   >
   >A barra de status é visível apenas para usuários com privilégios de fluxo de trabalho, por exemplo, os membros do grupo `workflow-users`.
   >
   >
   >As ações são exibidas quando o usuário atual está diretamente envolvido na etapa atual do fluxo de trabalho.

* Quando **Linha do tempo** estiver aberta para o recurso, a etapa do fluxo de trabalho será mostrada. Ao clicar/tocar no banner do alerta, as ações disponíveis também serão exibidas:

   ![Fluxo de trabalho na linha do tempo](/help/sites-cloud/authoring/assets/workflows-timeline.png)

### Concluindo uma etapa do participante {#completing-a-participant-step}

É possível concluir um item para permitir que o fluxo de trabalho avance para a próxima etapa.

Nesta ação, você pode indicar:

* **Próxima etapa**: a próxima etapa a ser realizada; é possível selecionar em uma lista fornecida
* **Comentário**: se necessário

É possível concluir uma etapa do participante a partir:

* [A caixa de entrada](#completing-a-participant-step-inbox)
* [O editor de páginas](#completing-a-participant-step-page-editor)
* [A linha do tempo](#completing-a-participant-step-timeline)
* Ao [abrir um item do fluxo de trabalho para exibir detalhes](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Concluindo uma etapa do participante - Caixa de entrada {#completing-a-participant-step-inbox}

Use o procedimento a seguir para concluir o item de trabalho:

1. Abra a **[Caixa de entrada do AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Selecione o item do fluxo de trabalho que deseja executar a ação (toque/clique na miniatura).
1. Selecione **Concluído** na barra de ferramentas.
1. A caixa de diálogo **Item de trabalho concluído** será aberta. Selecione a **Próxima etapa** no seletor suspenso e adicione um **Comentário**, se necessário.
1. Use **OK** para concluir a etapa (ou o botão **Cancelar** para cancelar a ação).

#### Concluir uma etapa do participante - Editor de páginas {#completing-a-participant-step-page-editor}

Use o procedimento a seguir para concluir o item de trabalho:

1. Abra o [página para edição](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Selecione **Concluído** na barra de status na parte superior.
1. A caixa de diálogo **Item de trabalho concluído** será aberta. Selecione a **Próxima etapa** no seletor suspenso e adicione um **Comentário**, se necessário.
1. Use **OK** para concluir a etapa (ou o botão **Cancelar** para cancelar a ação).

#### Concluir uma etapa do participante - Linha do tempo {#completing-a-participant-step-timeline}

Você também pode usar a linha do tempo para concluir e avançar uma etapa:

1. Selecione a página desejada e abra a **Linha do tempo** (ou abra a **Linha do tempo** e selecione a página):

   ![Concluir uma etapa](/help/sites-cloud/authoring/assets/workflows-timeline-completing.png)

1. Clique/toque no banner do alerta para mostrar as ações disponíveis. Selecionar **Avançado**:

   ![Avançar a etapa](/help/sites-cloud/authoring/assets/workflows-timeline-advance.png)

1. Dependendo do fluxo de trabalho, você pode selecionar a próxima etapa:

   ![Selecionar a próxima etapa](/help/sites-cloud/authoring/assets/workflows-next-step.png)

1. Selecionar **Avançado** para confirmar a ação

### Delegar uma etapa do participante {#delegating-a-participant-step}

Se uma etapa tiver sido atribuída a você, mas por qualquer motivo você não puder realizar uma ação, será possível delegar a etapa a outro usuário ou grupo.

Os usuários disponíveis para delegação dependem de quem recebeu o item de trabalho:

* Se o item de trabalho foi atribuído a um grupo, os membros do grupo ficam disponíveis.
* Se o item de trabalho tiver sido atribuído a um grupo e depois delegado a um usuário, os membros desse grupo e esse usuário estarão disponíveis.
* Se o item de trabalho foi atribuído a um único usuário, ele não poderá ser delegado.

Nesta ação, você pode indicar:

* **Usuário**: o usuário ao qual você deseja delegar; é possível selecionar de uma lista fornecida
* **Comentário**: se necessário

Você pode delegar uma etapa do participante de:

* [A caixa de entrada](#delegating-a-participant-step-inbox)
* [O editor de páginas](#delegating-a-participant-step-page-editor)
* [A linha do tempo](#delegating-a-participant-step-timeline)
* Ao [abrir um item do fluxo de trabalho para exibir detalhes](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Delegar uma etapa do participante - Caixa de entrada {#delegating-a-participant-step-inbox}

Use o procedimento a seguir para delegar um item de trabalho:

1. Abra a **[Caixa de entrada do AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Selecione o item do fluxo de trabalho que deseja executar a ação (toque/clique na miniatura).
1. Selecione **Delegar** na barra de ferramentas.
1. Uma caixa de diálogo será aberta. Especifique o **Usuário** no seletor suspenso (também pode ser um grupo) e adicione um **Comentário**, se necessário.
1. Use **OK** para concluir a etapa (ou o botão **Cancelar** para cancelar a ação).

#### Delegar uma etapa do participante - Editor de páginas {#delegating-a-participant-step-page-editor}

Use o procedimento a seguir para delegar um item de trabalho:

1. Abra o [página para edição](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Selecione **Delegar** na barra de status na parte superior.
1. Uma caixa de diálogo será aberta. Especifique o **Usuário** no seletor suspenso (também pode ser um grupo) e adicione um **Comentário**, se necessário.
1. Use **OK** para concluir a etapa (ou o botão **Cancelar** para cancelar a ação).

#### Delegar uma etapa do participante - Linha do tempo {#delegating-a-participant-step-timeline}

Também é possível usar a linha do tempo para delegar e/ou atribuir uma etapa:

1. Selecione a página desejada e abra a **Linha do tempo** (ou abra a **Linha do tempo** e selecione a página).
1. Clique/toque no banner do alerta para mostrar as ações disponíveis. Selecionar **Alterar responsável**:

   ![Etapa Delegar](/help/sites-cloud/authoring/assets/workflows-delegate.png)

1. Especifique um novo destinatário:

   ![Alterar responsável](/help/sites-cloud/authoring/assets/workflows-assignee.png)

1. Selecione **Atribuir** para confirmar a ação.

### Executando um retrocesso em uma etapa do participante {#performing-step-back-on-a-participant-step}

Se você descobrir que uma etapa, ou uma série de etapas, precisa ser repetida, poderá retroceder. Isso permite selecionar uma etapa, ocorrida anteriormente no workflow, para reprocessamento. O fluxo de trabalho retorna à etapa especificada e prossegue a partir dessa etapa.

Nesta ação, você pode indicar:

* **Etapa anterior**: a etapa a ser retornada; é possível selecionar de uma lista fornecida
* **Comentário**: se necessário

Você pode executar retroceder uma etapa em uma etapa do participante a partir:

* [A caixa de entrada](#performing-step-back-on-a-participant-step-inbox)
* [O editor de páginas](#performing-step-back-on-a-participant-step-page-editor)
* [A linha do tempo](#performing-step-back-on-a-participant-step-timeline)
* Ao [abrir um item do fluxo de trabalho para exibir detalhes](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Executando um retrocesso em uma etapa do participante - Caixa de entrada {#performing-step-back-on-a-participant-step-inbox}

Use o procedimento a seguir para retroceder:

1. Abra a **[Caixa de entrada do AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Selecione o item do fluxo de trabalho que deseja executar a ação (toque/clique na miniatura).
1. Selecione **Retroceder** para abrir a caixa de diálogo.
1. Especifique a **Etapa anterior** e adicione um **Comentário**, se necessário.
1. Use **OK** para concluir a etapa (ou o botão **Cancelar** para cancelar a ação).

#### Executando um retrocesso em uma etapa do participante - Editor de páginas {#performing-step-back-on-a-participant-step-page-editor}

Use o procedimento a seguir para retroceder:

1. Abra o [página para edição](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Selecione **Retroceder** na barra de status na parte superior.
1. Especifique a **Etapa anterior** e adicione um **Comentário**, se necessário.
1. Use **OK** para concluir a etapa (ou o botão **Cancelar** para cancelar a ação).

#### Executando um retrocesso em uma etapa do participante - Linha do tempo {#performing-step-back-on-a-participant-step-timeline}

Você também pode usar a linha do tempo para reverter (etapa) para uma etapa anterior:

1. Selecione a página desejada e abra a **Linha do tempo** (ou abra a **Linha do tempo** e selecione a página).
1. Clique/toque no banner do alerta para mostrar as ações disponíveis. Selecionar **Reverter**:

   ![Reverter uma etapa](/help/sites-cloud/authoring/assets/workflows-roll-back.png)

1. Especifique a etapa para a qual o fluxo de trabalho deve retornar:

   ![Especificar etapa](/help/sites-cloud/authoring/assets/workflows-roll-back-step.png)

1. Selecione **Reverter** para confirmar a ação.

### Abrir um item do fluxo de trabalho para exibir detalhes (e realizar ações) {#opening-a-workflow-item-to-view-details-and-take-actions}

Exibir detalhes do item de trabalho do fluxo de trabalho e tomar as ações apropriadas.

Os detalhes do workflow são mostrados em guias e as ações apropriadas estão disponíveis na barra de ferramentas:

* Guia **ITEM DE TRABALHO:**

   Guia ![ITEM DE TRABALHO](/help/sites-cloud/authoring/assets/workflows-work-item.png)

* Guia **INFORMAÇÕES DO FLUXO DE TRABALHO**:

   ![Guia FLUXO DE TRABALHO](/help/sites-cloud/authoring/assets/workflows-workflow-info.png)

   Se Estágio do fluxo de trabalho tiverem sido configurados para o modelo, você poderá visualizar o progresso de acordo com estes: <!--If [Workflow Stages](/help/sites-developing/workflows.md#workflow-stages) have been configured for the model, you can view the progress according to these:-->

   ![Estágios do fluxo de trabalho](/help/sites-cloud/authoring/assets/workflows-workflow-stages.png)

* Guia **COMENTÁRIOS**:

   ![Guia COMENTÁRIOS](/help/sites-cloud/authoring/assets/workflows-comments.png)

Você pode abrir os detalhes do item de trabalho nos seguintes locais:

* [A caixa de entrada](#performing-step-back-on-a-participant-step-inbox)
* [O editor de páginas](#performing-step-back-on-a-participant-step-page-editor)

#### Detalhes de abertura do fluxo de trabalho - Caixa de entrada {#opening-workflow-details-inbox}

Para abrir um item do fluxo de trabalho e exibir os detalhes:

1. Abra a **[Caixa de entrada do AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Selecione o item do fluxo de trabalho que deseja executar a ação (toque/clique na miniatura).
1. Selecione **Abrir** para abrir as guias de informações.
1. Se necessário, selecione a ação apropriada, forneça os detalhes e confirme com **OK** (ou **Cancelar**).
1. Use **Salvar** ou **Cancelar** para sair.

#### Abrir detalhes do fluxo de trabalho - Editor de páginas {#opening-workflow-details-page-editor}

Para abrir um item do fluxo de trabalho e exibir os detalhes:

1. Abra o [página para edição](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Selecione **Exibir detalhes** na barra de status para abrir as guias de informações.
1. Se necessário, selecione a ação apropriada, forneça os detalhes e confirme com **OK** (ou **Cancelar**).
1. Use **Salvar** ou **Cancelar** para sair.

### Exibição da carga do fluxo de trabalho (vários recursos) {#viewing-the-workflow-payload-multiple-resources}

Você pode exibir detalhes da carga associada à instância do fluxo de trabalho. Inicialmente, os recursos do pacote são mostrados e, em seguida, você pode fazer drill-down para mostrar as páginas individuais.

Para exibir a carga e os recursos da instância de workflow:

1. Abra a **[Caixa de entrada do AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Selecione o item do fluxo de trabalho que deseja executar a ação (toque/clique na miniatura).
1. Selecione **Exibir carga** na barra de ferramentas para abrir a caixa de diálogo.
   * Como um pacote de fluxo de trabalho é simplesmente uma coleção de ponteiros para caminhos no repositório, você pode adicionar/remover/modificar as entradas aqui para ajustar o que é referenciado pelo pacote de fluxo de trabalho. Use o **Definição de recurso** para adicionar novas entradas.
1. Os links podem ser usados para abrir páginas individuais.
