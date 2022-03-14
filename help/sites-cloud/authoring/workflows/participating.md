---
title: Participar de fluxos de trabalho
description: Fluxos de trabalho geralmente incluem etapas que exigem que uma pessoa realize uma atividade em uma página ou ativo.
exl-id: 62192da9-0b5b-4997-9c2b-d1aee04b01f9
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 75%

---

# Participar de fluxos de trabalho {#participating-in-workflows}

Fluxos de trabalho geralmente incluem etapas que exigem que uma pessoa realize uma atividade em uma página ou ativo. O fluxo de trabalho seleciona um usuário ou grupo para realizar a atividade e atribui um item de trabalho a essa pessoa ou grupo. O usuário recebe uma notificação e pode executar a ação apropriada:

* [Visualizar notificações](#notifications-of-available-workflow-actions)
* [Concluir uma etapa do participante](#completing-a-participant-step)
* [Delegar uma etapa do participante](#delegating-a-participant-step)
* [Realizar um retrocesso em uma etapa do participante](#performing-step-back-on-a-participant-step)
* [Abrir um item de fluxo de trabalho para exibir detalhes (e realizar ações)](#opening-a-workflow-item-to-view-details-and-take-actions)
* [Visualizar a carga do fluxo de trabalho (vários recursos)](#viewing-the-workflow-payload-multiple-resources)

## Notificações de ações de fluxo de trabalho disponíveis {#notifications-of-available-workflow-actions}

Quando um item de trabalho é atribuído a você (por exemplo, **Aprovar conteúdo**), vários alertas e/ou notificações são exibidos:

* Seu indicador de [notificação](/help/sites-cloud/authoring/getting-started/inbox.md) (barra de ferramentas) será incrementado:

   ![Barra de ferramentas Notificação](/help/sites-cloud/authoring/assets/workflows-notifications.png)

* O item será listado na sua [Caixa de entrada](/help/sites-cloud/authoring/getting-started/inbox.md) de notificações:

   ![Notificações na caixa de entrada](/help/sites-cloud/authoring/assets/workflows-inbox.png)

* Quando você estiver usando o editor de páginas, a barra de status mostrará:
   * O nome dos fluxos de trabalho que estão sendo aplicados à página, por exemplo, Solicitação para ativação.
   * Quaisquer ações disponíveis ao usuário atual para a etapa atual do fluxo de trabalho, por exemplo, Concluir, Delegar, Exibir detalhes.
   * O número de fluxos de trabalho aos quais a página está sujeita. É possível:
      * usar as setas para a esquerda/direita para navegar pelas informações de status dos vários fluxos de trabalho.
      * clicar/tocar no número real para abrir uma lista suspensa de todos os fluxos de trabalho aplicáveis e, em seguida, selecionar o fluxo de trabalho que deseja exibir na barra de status.

   ![Página com vários fluxos de trabalho](/help/sites-cloud/authoring/assets/workflows-multiple.png)

   >[!NOTE]
   >
   >A barra de status é visível apenas para usuários com privilégios de fluxo de trabalho, por exemplo, os membros do grupo `workflow-users`.
   >
   >
   >As ações são mostradas quando o usuário atual está diretamente envolvido na etapa atual do fluxo de trabalho.

* Quando a **Linha do tempo** estiver aberta para o recurso, a etapa do fluxo de trabalho será mostrada. Quando você clicar/tocar no banner de alerta, as ações disponíveis também serão mostradas:

   ![Fluxo de trabalho na linha do tempo](/help/sites-cloud/authoring/assets/workflows-timeline.png)

### Conclusão de uma etapa do participante {#completing-a-participant-step}

Você pode concluir um item para permitir que o fluxo de trabalho progrida para a próxima etapa.

Nesta ação, você pode indicar:

* **Próxima etapa**: o próximo passo a ser dado; você pode selecionar em uma lista fornecida
* **Comentário**: se necessário

Você pode concluir uma etapa do participante nos seguintes locais:

* [A Caixa de entrada](#completing-a-participant-step-inbox)
* [O Editor de páginas](#completing-a-participant-step-page-editor)
* [A Linha do Tempo](#completing-a-participant-step-timeline)
* When [abrir um item de fluxo de trabalho para exibir detalhes](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Conclusão de uma etapa do participante - Caixa de entrada {#completing-a-participant-step-inbox}

Use o procedimento a seguir para concluir o item de trabalho:

1. Abra a **[Caixa de entrada do AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Selecione o item de fluxo de trabalho com o qual você deseja trabalhar (toque/clique na miniatura).
1. Selecionar **Concluído** na barra de ferramentas.
1. A caixa de diálogo **Item de trabalho concluído** será aberta. Selecione o **Próxima etapa** no seletor suspenso e adicione um **Comentário** se necessário.
1. Use **OK** para concluir a etapa (ou o **Cancelar** para suspender a ação).

#### Conclusão de uma etapa do participante - Editor de páginas {#completing-a-participant-step-page-editor}

Use o procedimento a seguir para concluir o item de trabalho:

1. Abra a [página para edição](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Selecionar **Concluído** na barra de status na parte superior.
1. A caixa de diálogo **Item de trabalho concluído** será aberta. Selecione o **Próxima etapa** no seletor suspenso e adicione um **Comentário** se necessário.
1. Use **OK** para concluir a etapa (ou o **Cancelar** para suspender a ação).

#### Conclusão de uma etapa do participante - Linha do tempo {#completing-a-participant-step-timeline}

Você também pode usar a linha do tempo para concluir e avançar uma etapa:

1. Selecione a página desejada e abra **Linha do tempo** (ou abrir **Linha do tempo** e selecione a página):

   ![Concluir uma etapa](/help/sites-cloud/authoring/assets/workflows-timeline-completing.png)

1. Clique/toque no banner de alerta para mostrar as ações disponíveis. Selecione **Avançar**:

   ![Avançar a etapa](/help/sites-cloud/authoring/assets/workflows-timeline-advance.png)

1. Dependendo do fluxo de trabalho, você pode selecionar a próxima etapa:

   ![Selecionar a próxima etapa](/help/sites-cloud/authoring/assets/workflows-next-step.png)

1. Selecione **Avançar** para confirmar a ação.

### Delegação de uma etapa do participante {#delegating-a-participant-step}

Se uma etapa tiver sido atribuída a você, mas, por algum motivo, você não puder realizar uma ação, será possível delegar a etapa a outro usuário ou grupo.

Os usuários que estão disponíveis para delegação dependem de quem recebeu o item de trabalho:

* Se o item de trabalho tiver sido atribuído a um grupo, os membros desse grupo estarão disponíveis.
* Se o item de trabalho tiver sido atribuído a um grupo e depois delegado a um usuário, os membros desse grupo e esse usuário estarão disponíveis.
* Se o item de trabalho tiver sido atribuído a um único usuário, ele não poderá ser delegado.

Nesta ação, você pode indicar:

* **Usuário**: o usuário ao qual você deseja delegar e que pode ser selecionado na lista fornecida
* **Comentário**: se necessário

Você pode delegar um etapa de participante nos seguintes locais:

* [A Caixa de entrada](#delegating-a-participant-step-inbox)
* [O Editor de páginas](#delegating-a-participant-step-page-editor)
* [A Linha do Tempo](#delegating-a-participant-step-timeline)
* When [abrir um item de fluxo de trabalho para exibir detalhes](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Delegação de uma etapa do participante - Caixa de entrada {#delegating-a-participant-step-inbox}

Use o procedimento a seguir para delegar um item de trabalho:

1. Abra a **[Caixa de entrada do AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Selecione o item de fluxo de trabalho com o qual você deseja trabalhar (toque/clique na miniatura).
1. Selecionar **Delegar** na barra de ferramentas.
1. Uma caixa de diálogo será aberta. Especifique a **Usuário** no seletor suspenso (também pode ser um grupo) e adicione um **Comentário** se necessário.
1. Use **OK** para concluir a etapa (ou o **Cancelar** para suspender a ação).

#### Delegação de uma etapa do participante - Editor de páginas {#delegating-a-participant-step-page-editor}

Use o procedimento a seguir para delegar um item de trabalho:

1. Abra a [página para edição](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Selecionar **Delegar** na barra de status na parte superior.
1. Uma caixa de diálogo será aberta. Especifique a **Usuário** no seletor suspenso (também pode ser um grupo) e adicione um **Comentário** se necessário.
1. Use **OK** para concluir a etapa (ou o **Cancelar** para suspender a ação).

#### Delegação de uma etapa do participante - Linha do tempo {#delegating-a-participant-step-timeline}

Você também pode usar a linha do tempo para delegar e/ou atribuir uma etapa:

1. Selecione a página desejada e abra **Linha do tempo** (ou abrir **Linha do tempo** e selecione a página).
1. Clique/toque no banner de alerta para mostrar as ações disponíveis. Selecione **Alterar administrador**:

   ![Etapa Delegar](/help/sites-cloud/authoring/assets/workflows-delegate.png)

1. Especifique um novo destinatário:

   ![Alterar destinatário](/help/sites-cloud/authoring/assets/workflows-assignee.png)

1. Selecionar **Atribuir** para confirmar a ação.

### Retroceder em uma etapa do participante {#performing-step-back-on-a-participant-step}

Se você descobrir que uma etapa, ou uma série de etapas, precisa ser repetida, será possível retroceder. Essa ação permite selecionar uma etapa, ocorrida anteriormente no fluxo de trabalho, para reprocessamento. O fluxo de trabalho retornará à etapa especificada e prosseguirá a partir daí.

Nesta ação, você pode indicar:

* **Etapa anterior**: a etapa para a qual retornar; você pode selecionar em uma lista fornecida
* **Comentário**: se necessário

Você pode retroceder uma etapa de participante nos seguintes locais:

* [A Caixa de entrada](#performing-step-back-on-a-participant-step-inbox)
* [O Editor de páginas](#performing-step-back-on-a-participant-step-page-editor)
* [A Linha do Tempo](#performing-step-back-on-a-participant-step-timeline)
* When [abrir um item de fluxo de trabalho para exibir detalhes](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Retroceder em uma etapa do participante - Caixa de entrada {#performing-step-back-on-a-participant-step-inbox}

Use o procedimento a seguir para retroceder:

1. Abra a **[Caixa de entrada do AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Selecione o item de fluxo de trabalho com o qual você deseja trabalhar (toque/clique na miniatura).
1. Selecionar **Retroceder** para abrir a caixa de diálogo.
1. Especifique a **Etapa anterior** e adicione um **Comentário**, se necessário.
1. Use **OK** para concluir a etapa (ou o **Cancelar** para suspender a ação).

#### Retroceder em uma etapa do participante - Editor de página {#performing-step-back-on-a-participant-step-page-editor}

Use o procedimento a seguir para retroceder:

1. Abra a [página para edição](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Selecionar **Retroceder** na barra de status na parte superior.
1. Especifique a **Etapa anterior** e adicione um **Comentário**, se necessário.
1. Use **OK** para concluir a etapa (ou o **Cancelar** para suspender a ação).

#### Retroceder em uma etapa do participante - Linha do tempo {#performing-step-back-on-a-participant-step-timeline}

Você também pode usar a linha do tempo para retroceder para uma etapa anterior:

1. Selecione a página desejada e abra **Linha do tempo** (ou abrir **Linha do tempo** e selecione a página).
1. Clique/toque no banner de alerta para mostrar as ações disponíveis. Selecione **Reverter**:

   ![Reverter uma etapa](/help/sites-cloud/authoring/assets/workflows-roll-back.png)

1. Especifique a etapa para a qual o fluxo de trabalho deve retornar:

   ![Especificar etapa](/help/sites-cloud/authoring/assets/workflows-roll-back-step.png)

1. Selecionar **Reverter** para confirmar a ação.

### Abrir um item de fluxo de trabalho para exibir detalhes (e realizar ações) {#opening-a-workflow-item-to-view-details-and-take-actions}

Visualize detalhes do item de trabalho do fluxo de trabalho e tome as ações apropriadas.

Os detalhes do fluxo de trabalho são mostrados nas guias, e as ações apropriadas estão disponíveis na barra de ferramentas:

* Guia **ITEM DE TRABALHO:**

   Guia ![ITEM DE TRABALHO](/help/sites-cloud/authoring/assets/workflows-work-item.png)

* **INFORMAÇÕES DO FLUXO DE TRABALHO** guia :

   ![Guia WORKFLOW](/help/sites-cloud/authoring/assets/workflows-workflow-info.png)

   Se Estágio do fluxo de trabalho tiverem sido configurados para o modelo, você poderá visualizar o progresso de acordo com estes: <!--If [Workflow Stages](/help/sites-developing/workflows.md#workflow-stages) have been configured for the model, you can view the progress according to these:-->

   ![Estágios do workflow](/help/sites-cloud/authoring/assets/workflows-workflow-stages.png)

* **COMENTÁRIOS** guia :

   ![Guia COMENTÁRIOS](/help/sites-cloud/authoring/assets/workflows-comments.png)

Você pode abrir os detalhes do item de trabalho nos seguintes locais:

* [A Caixa de entrada](#performing-step-back-on-a-participant-step-inbox)
* [O Editor de páginas](#performing-step-back-on-a-participant-step-page-editor)

#### Abertura de detalhes do fluxo de trabalho - Caixa de entrada {#opening-workflow-details-inbox}

Para abrir um item de fluxo de trabalho e visualizar os detalhes:

1. Abra a **[Caixa de entrada do AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Selecione o item de fluxo de trabalho com o qual você deseja trabalhar (toque/clique na miniatura).
1. Selecionar **Abrir** para abrir as guias de informações.
1. Se necessário, selecione a ação apropriada, forneça os detalhes e confirme com **OK** (ou **Cancelar**).
1. Use **Salvar** ou **Cancelar** para sair.

#### Abertura de detalhes do fluxo de trabalho - Editor de página {#opening-workflow-details-page-editor}

Para abrir um item de fluxo de trabalho e visualizar os detalhes:

1. Abra a [página para edição](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Selecionar **Exibir detalhes** na barra de status para abrir as guias de informações.
1. Se necessário, selecione a ação apropriada, forneça os detalhes e confirme com **OK** (ou **Cancelar**).
1. Use **Salvar** ou **Cancelar** para sair.

### Visualizar a carga do fluxo de trabalho (vários recursos) {#viewing-the-workflow-payload-multiple-resources}

Você pode visualizar detalhes da carga associada à instância do fluxo de trabalho. Inicialmente, os recursos no pacote são exibidos e, em seguida, você pode detalhar até as páginas individuais.

Para visualizar a carga e os recursos da instância do fluxo de trabalho:

1. Abra a **[Caixa de entrada do AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Selecione o item de fluxo de trabalho com o qual você deseja trabalhar (toque/clique na miniatura).
1. Selecionar **Exibir carga** na barra de ferramentas para abrir a caixa de diálogo.
   * Como um pacote de fluxo de trabalho é simplesmente uma coleção de apontadores de caminhos dentro do repositório, você pode adicionar/remover/modificar as entradas aqui para ajustar o que é referenciado pelo pacote de fluxo de trabalho. Use o componente **Definição do recurso** para adicionar novas entradas.
1. Os links podem ser usados para abrir as páginas individuais.
