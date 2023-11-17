---
title: Como faço para gerenciar formulários, aplicativos e tarefas na Caixa de Entrada do AEM?
description: A Caixa de entrada AEM permite iniciar fluxos de trabalho centrados no Forms enviando aplicativos e gerenciando tarefas.
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: document_services, publish
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 3%

---


# Gerenciar aplicativos e tarefas do Forms na Caixa de entrada AEM{#manage-forms-applications-and-tasks-in-aem-inbox}

Uma das muitas maneiras de iniciar ou acionar um fluxo de trabalho centrado no Forms é por meio de aplicativos na Caixa de entrada AEM. É necessário criar um aplicativo de fluxo de trabalho para disponibilizar um Forms Workflow como um aplicativo na Caixa de entrada. Para obter mais informações sobre o aplicativo de workflow e outras maneiras de iniciar workflows do Forms, consulte [Inicie um fluxo de trabalho centrado no Forms no OSGi](aem-forms-workflow.md#launch).

Além disso, a Caixa de entrada do AEM consolida notificações e tarefas de vários componentes do AEM, incluindo workflows da Forms. Quando um Forms Workflow contendo uma etapa Atribuir tarefa é acionado, o aplicativo associado é listado como uma tarefa na Caixa de entrada do destinatário. Se o destinatário for um grupo, a tarefa aparecerá na Caixa de entrada de todos os membros do grupo até que um indivíduo reclame ou delegue a tarefa.

A interface do usuário da Caixa de entrada fornece exibições de lista e calendário para exibir tarefas. Você também pode definir as configurações de exibição. Você pode filtrar tarefas com base em vários parâmetros. Para obter mais informações sobre visualização e filtros, consulte [Sua Caixa de entrada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html#inbox-in-the-header).

Em resumo, a Caixa de entrada permite criar um aplicativo e gerenciar tarefas atribuídas.

>[!NOTE]
>
>Você deve ser um membro do [!DNL workflow-users] para poder usar a Caixa de entrada AEM.

## Criar aplicativo {#create-application}

1. Acesse a Caixa de entrada do AEM em https://&#39;[server]:[porta]&quot;/aem/inbox.
1. Na interface da Caixa de entrada, toque em **[!UICONTROL Criar > Aplicativo]**. A página Selecionar Aplicativo é exibida.
1. Selecione um aplicativo e clique em **[!UICONTROL Criar]**. O Formulário adaptável associado ao aplicativo é aberto. Preencha as informações no Formulário adaptável e toque em **[!UICONTROL Enviar]**. Ele inicia o fluxo de trabalho associado e cria uma tarefa na Caixa de entrada do destinatário.

## Gerencie tarefas {#manage-tasks}

Quando um fluxo de trabalho do Forms é acionado e você é um destinatário ou parte do grupo de destinatários, uma tarefa é exibida na Caixa de entrada. Você pode exibir os detalhes da tarefa e executar as ações disponíveis na tarefa de dentro da Caixa de entrada.

### Reclamar ou delegar tarefas {#claim-or-delegate-tasks}

As tarefas atribuídas a um grupo aparecem na Caixa de Entrada de todos os membros do grupo. Qualquer membro do grupo pode reivindicar essa tarefa ou delegá-la a outro membro do grupo. Para fazer isso:

1. Toque para selecionar a miniatura da tarefa. As opções para abrir ou delegar a tarefa são exibidas na parte superior.

   ![select-task](assets/select-task.png)

1. Siga uma das seguintes opções:

   * Para delegar a tarefa, toque em **[!UICONTROL Delegar]**. A Caixa De Diálogo Delegar Item É Aberta. Selecione um usuário, opcionalmente adicione um comentário e toque em **[!UICONTROL OK]**.

   ![delegar](assets/delegate.png)

   * Para reivindicar a tarefa, toque em **[!UICONTROL Abertura]**. A caixa de diálogo Atribuir a si mesmo é aberta. Toque **[!UICONTROL Continuar]** para reivindicar a tarefa. A tarefa solicitada aparece com você como o destinatário em sua Caixa de entrada.

   ![declaração](assets/claim.png)

### Exibir detalhes e executar ações em tarefas {#view-details-and-perform-actions-on-tasks}

Ao abrir uma tarefa, você pode exibir os detalhes da tarefa e executar as ações disponíveis. As ações disponíveis para uma tarefa são definidas na etapa Atribuir tarefa do Forms Workflow associado.

1. Toque para selecionar a miniatura da tarefa. As opções para abrir ou delegar a tarefa selecionada aparecem na parte superior.
1. Toque **Abertura** para exibir detalhes da tarefa e realizar ações. A visualização detalhada da tarefa é aberta. Nesta exibição, é possível exibir detalhes da tarefa e realizar ações na tarefa.

   >[!NOTE]
   >
   >Se uma tarefa for atribuída a um grupo, você deverá declará-la para poder abri-la na exibição detalhada.

![detalhes-tarefa](assets/task-details.png)

A exibição de tarefa detalhada compreende as seguintes seções:

* Detalhes da tarefa
* Formulário
* Detalhes do fluxo de trabalho
* Barra de ferramentas Ações

#### Detalhes da tarefa {#task-details}

A seção Detalhes da Tarefa exibe informações sobre a tarefa. As informações exibidas dependem das definições de configuração do [Atribuir etapa de tarefa](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) no workflow. O exemplo acima exibe a descrição, o status, a data de início e o workflow usado para a tarefa. Também permite anexar um arquivo à tarefa.

#### Formulário {#form}

A guia Form na área de conteúdo principal exibe o formulário enviado e os anexos no nível de campo, se houver.

#### Detalhes do fluxo de trabalho {#workflow-details}

A guia Detalhes do fluxo de trabalho na parte superior mostra o progresso da tarefa em vários estágios no fluxo de trabalho. Ela mostra os estágios concluídos, atuais e pendentes da tarefa. Os estágios de um fluxo de trabalho são definidos no [Atribuir etapa de tarefa](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) do fluxo de trabalho associado.

Além disso, a guia exibe o histórico da tarefa para cada estágio concluído no workflow. Você pode tocar em **[!UICONTROL Exibir detalhes]** para que um estágio concluído saiba detalhes sobre esse estágio. Ele exibe comentários, anexos de formulário e tarefa, status, datas de início e término e assim por diante, sobre a tarefa.

![workflow-details](assets/workflow-details.png)

#### Barra de ferramentas Ações {#actions-toolbar}

A barra de ferramentas Ações mostra todas as opções disponíveis para a tarefa. Embora Save, Reset e Delegate sejam ações padrão, outras ações disponíveis são configuradas no [Atribuir etapa de tarefa](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem). No exemplo acima, Aprovar e Rejeitar são configurados no workflow.

À medida que você age na tarefa, ela continua mais no fluxo de trabalho.

### Exibir tarefas concluídas {#view-completed-tasks}

A Caixa de entrada do AEM exibe somente tarefas ativas. Tarefas concluídas não aparecem na lista. No entanto, você pode usar filtros da Caixa de entrada para filtrar tarefas com base em vários parâmetros, como tipo de tarefa, status, datas de início e término. Para exibir tarefas concluídas:

1. Na Caixa de entrada do AEM, toque em ![ativar/desativar painel lateral1](assets/toggle-side-panel1.png) para abrir o seletor de filtros.
1. Toque **[!UICONTROL Status da tarefa]** e selecione **[!UICONTROL Concluído]**. Todas as tarefas concluídas são exibidas.

   ![filter](assets/filter.png)

1. Toque para selecionar uma tarefa e clique em **[!UICONTROL Abertura]**.

A tarefa é aberta para exibir o documento ou o Formulário adaptável associado à tarefa. Para o Formulário adaptável, a tarefa exibe o Formulário adaptável somente leitura ou seu Documento de registro de PDF, conforme configurado na guia Formulário/Documento do [Etapa do fluxo de trabalho Atribuir tarefa](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem).

A seção de detalhes da tarefa exibe informações como ação tomada, status da tarefa, data inicial e data final.

![completed-task](assets/completed-task.png)

A variável **[!UICONTROL Detalhes do fluxo de trabalho]** mostra cada etapa do fluxo de trabalho. Toque **[!UICONTROL Exibir detalhes]** para obter uma etapa para informações detalhadas.

![completed-task-workflow](assets/completed-task-workflow.png)

## Resolução de problemas {#troubleshooting-workflows}

### Não é possível exibir itens relacionados ao fluxo de trabalho do AEM na Caixa de entrada AEM {#unable-to-see-aem-worklow-items}

Um proprietário de modelo de fluxo de trabalho não pode exibir itens relacionados ao Fluxo de trabalho do AEM na Caixa de Entrada do AEM. Para resolver o problema, adicione os índices listados abaixo ao repositório AEM e recrie o índice.

1. Use um dos métodos a seguir para adicionar índices:

   * Crie os seguintes nós em no CRX DE em `/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties` com as respectivas propriedades conforme especificado na tabela a seguir:

     | Nó | Propriedade | Tipo |
     |---|---|---|
     | sharedWith | sharedWith | SEQÜÊNCIA DE CARACTERES |
     | bloqueado | bloqueado | BOOLEANO |
     | retornado | retornado | BOOLEANO |
     | allowInboxSharing | allowInboxSharing | BOOLEANO |
     | allowExplicitSharing | allowExplicitSharing | BOOLEANO |


   * Implante os índices por meio de um pacote AEM. Você pode usar um [Arquétipo AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) projeto para criar um pacote de AEM implantável. Use o seguinte código de amostra para adicionar índices a um projeto do Arquétipo AEM:

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [Criar um índice de propriedade e defini-lo como verdadeiro](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html?lang=en#the-property-index).

1. Após configurar os índices no CRX DE ou implantar por meio de um pacote, [reindexar o repositório](https://helpx.adobe.com/in/experience-manager/kb/HowToCheckLuceneIndex.html#Completelyrebuildtheindex).

