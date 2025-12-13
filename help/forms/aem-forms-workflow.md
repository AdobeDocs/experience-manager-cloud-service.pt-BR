---
title: Como usar o AEM Forms para BPM (Business Process Automation, automação de processos de negócios)?
seo-title: Rapidly build Adaptive Forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: Use o AEM Forms Workflow para automatizar e criar rapidamente workflows de processos de negócios. Por exemplo, análise e aprovação, geração de PDF, fluxos de trabalho do Adobe Sign.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f0fec4a9-b214-4931-bf09-5898b082481e
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2489'
ht-degree: 1%

---

# Fluxo de trabalho centrado no Forms no OSGi {#forms-centric-workflow-on-osgi}

![Imagem Principal](do-not-localize/header.png)

As empresas coletam dados de centenas e milhares de formulários, vários sistemas de back-end e fontes de dados online ou offline. Eles também têm um conjunto dinâmico de usuários para tomar decisões sobre os dados, o que envolve processos iterativos de revisão e aprovação.

Juntamente com os fluxos de trabalho de revisão e aprovação para públicos internos e externos, grandes organizações e empresas têm tarefas repetitivas. Por exemplo, converter um documento do PDF em outro formato. Quando realizadas manualmente, essas tarefas consomem muito tempo e recursos. As empresas também têm requisitos legais para assinar digitalmente um documento e arquivar dados de formulário para uso posterior em formatos predefinidos.

## Introdução ao fluxo de trabalho centrado no Forms no OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Você pode usar fluxos de trabalho do AEM para criar rapidamente fluxos de trabalho baseados no Forms adaptável. Esses workflows podem ser usados para revisão e aprovações, fluxos de processo comercial, para iniciar serviços de documentos, integrar ao fluxo de trabalho de assinatura do Adobe Sign e operações semelhantes. Por exemplo, processamento de aplicativo de cartão de crédito, fluxos de trabalho de aprovação de saída de funcionário, salvamento de um formulário como um documento do PDF. Além disso, esses workflows podem ser usados em uma organização ou através do firewall de rede.

Com um fluxo de trabalho centrado na Forms no OSGi, você pode criar e implantar rapidamente fluxos de trabalho para várias tarefas na pilha do OSGi, sem precisar instalar o recurso completo de Gerenciamento de processos na pilha do JEE. O desenvolvimento e o gerenciamento de workflows usam os recursos familiares do fluxo de trabalho do AEM e da caixa de entrada do AEM. Os fluxos de trabalho formam a base da automatização de processos de negócios reais que abrangem vários sistemas de software, redes, departamentos e até mesmo organizações.

Após configurado, esses fluxos de trabalho podem ser acionados manualmente para concluir um processo definido ou executar programaticamente quando os usuários enviarem um formulário <!-- or [correspondence management](cm-overview.md) letter-->. <!-- With this enhanced AEM Workflow capabilities, [!DNL AEM Forms] offers two distinct, yet similar, capabilities. As part of your deployment strategy, you need to decide which one works for you. See a [comparison](capabilities-osgi-jee-workflows.md) of the Forms-centric AEM Workflows on OSGi and Process Management on JEE. Moreover, for the deployment topology see, [Architecture and deployment topologies for [!DNL AEM Forms]]((aem-forms-architecture-deployment.md). -->

O fluxo de trabalho centrado no Forms no OSGi estende a [Caixa de Entrada do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html?lang=pt-BR#authoring) e fornece componentes extras (etapas) para o editor de fluxo de trabalho do AEM para adicionar suporte a fluxos de trabalho centrados no [!DNL AEM Forms]. <!-- The extended AEM Inbox has functionalities similar to [[!DNL AEM Forms] Workspace](introduction-html-workspace.md). Along with managing human-centric workflows (Approval, Review, and so on), you can use AEM workflows to automate [document services](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html?lang=pt-BR#extending-aem)-related operations (for example, Generate PDF) and electronically signing (Adobe Sign) documents. -->

Todas as etapas do fluxo de trabalho [!DNL AEM Forms] oferecem suporte ao uso de variáveis. As variáveis permitem que as etapas do fluxo de trabalho retenham e transmitam metadados pelas etapas no tempo de execução. É possível criar diferentes tipos de variáveis para armazenar diferentes tipos de dados. Você também pode criar coleções de variáveis (matriz) para armazenar várias instâncias de dados relacionados do mesmo tipo. Normalmente, você usa uma variável ou uma coleção de variáveis quando precisa tomar uma decisão com base no valor que ela contém ou armazenar informações necessárias posteriormente em um processo. Para obter mais informações sobre como usar variáveis nesses componentes de fluxo de trabalho centrados na Forms (etapas), consulte [Fluxo de trabalho centrado na Forms no OSGi - Referência da etapa](aem-forms-workflow-step-reference.md). Para obter informações sobre como criar e gerenciar variáveis, consulte [Variáveis em fluxos de trabalho do AEM](variable-in-aem-workflows.md).

O diagrama a seguir representa um procedimento completo para criar, executar e monitorar um fluxo de trabalho centrado no Forms no OSGi.

![introdução-ao-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## Aplicabilidade e casos de uso

### Seguros

## O AEM Forms oferece suporte a workflows de aprovação de seguros?

Sim. O AEM Forms oferece suporte a revisões e aprovações baseadas em fluxo de trabalho, permitindo a revisão do ajustador, a aprovação do gerente e loops de retrabalho como parte dos processos de seguro.

## A AEM Forms oferece suporte a processos de verificador de fabricante para seguros?

Sim. Os fluxos de trabalho do AEM Forms podem ser configurados para suportar padrões de criador-verificador, garantindo a separação de tarefas entre as funções de entrada de dados e aprovação.

## O AEM Forms pode rastrear o status de solicitações ou solicitações de seguro?

Sim. Os workflows do AEM Forms permitem que as seguradoras rastreiem o envio e o status de processamento de formulários em diferentes estágios do processo de negócios.

## O AEM Forms oferece suporte à subscrições de workflows?

Sim, com fluxos de trabalho e integrações. O AEM Forms oferece suporte a processos orientados por fluxo de trabalho e integrações de back-end que permitem que os dados do aplicativo fluam para sistemas de tomada firme e decisão.

## O AEM Forms oferece suporte a trilhas de auditoria para processos de seguro?

Sim. A AEM Forms oferece suporte à auditoria por meio de histórico de fluxo de trabalho, controles de acesso e logs do sistema, que ajudam as seguradoras a atender às necessidades de auditoria interna e externa.

## Antes de começar {#before-you-start}

* Um fluxo de trabalho é uma representação de um processo de negócios real. Mantenha o processo de negócios real e a lista dos participantes do processo de negócios prontos. Além disso, mantenha o material de apoio (Forms adaptável, Documentos do PDF e muito mais) pronto antes de começar a criar um fluxo de trabalho.
* Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada do AEM e ajudam a relatar o progresso do workflow. Divida o processo de negócios em estágios lógicos.
* Você pode configurar a etapa atribuir tarefa dos fluxos de trabalho do AEM para enviar notificações por email aos usuários ou atribuídos. Portanto, [habilite as notificações por email](#configure-email-service).
* Um fluxo de trabalho também pode usar o Adobe Sign para assinaturas digitais. Se você planeja usar o Adobe Sign em um workflow, a [configure o Adobe Sign para  [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) antes de usá-lo em um workflow.

## Criar um modelo de fluxo de trabalho {#create-a-workflow-model}

Um modelo de fluxo de trabalho consiste na lógica e no fluxo de um processo de negócios. Ele é composto por uma série de etapas. Essas etapas são componentes do AEM. É possível estender as etapas do fluxo de trabalho com parâmetros e scripts para fornecer mais funcionalidade e controle, conforme necessário. O [!DNL AEM Forms] fornece algumas etapas além das etapas do AEM prontas para uso. Para obter uma lista detalhada de etapas do AEM e do [!DNL AEM Forms], consulte a [Referência da etapa do fluxo de trabalho do AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html?lang=pt-BR#extending-aem) e o [fluxo de trabalho centrado no Forms no OSGi - Referência da etapa](aem-forms-workflow.md).

O AEM fornece uma interface de usuário intuitiva para criar um modelo de fluxo de trabalho usando as etapas de fluxo de trabalho fornecidas. Para obter instruções passo a passo sobre como criar um modelo de fluxo de trabalho, consulte [Criando Modelos de Fluxo de Trabalho](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html?lang=pt-BR#workflows). O exemplo a seguir fornece instruções passo a passo para criar um modelo de fluxo de trabalho para um fluxo de trabalho de aprovação e revisão:

>[!NOTE]
>
>Você deve ser membro do grupo do editor de fluxo de trabalho para criar ou editar um modelo de fluxo de trabalho.

### Criar um modelo para um fluxo de trabalho de aprovação e revisão {#create-a-model-for-an-approval-and-review-workflow}

O fluxo de trabalho de aprovação e revisão é para tarefas que exigem intervenção humana para tomar decisões. O exemplo a seguir cria um modelo de fluxo de trabalho para um pedido de empréstimo hipotecário a ser preenchido por um agente bancário de front-office. Depois que o aplicativo é preenchido, ele é enviado para aprovação. Posteriormente, o aplicativo aprovado é enviado ao solicitante para assinatura eletrônica usando o Adobe Sign.

O exemplo está disponível como um pacote anexado abaixo. Importe e instale o exemplo usando o gerenciador de pacotes. Você também pode executar as seguintes etapas para criar manualmente o modelo de fluxo de trabalho para o aplicativo:

O exemplo cria um modelo de fluxo de trabalho para uma solicitação de hipoteca a ser preenchida por um agente bancário de front-office. Uma vez preenchido, o aplicativo é enviado para aprovação. Posteriormente, o aplicativo aprovado é enviado ao cliente para assinaturas eletrônicas usando o Adobe Sign. Você pode importar e instalar o exemplo usando o gerenciador de pacotes.

[Obter arquivo](assets/example-mortgage-loan-application.zip)

1. Abra o console Modelos de fluxo de trabalho. A URL padrão é `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Selecione **Criar** e depois **Criar Modelo**. A caixa de diálogo Adicionar modelo de fluxo de trabalho é exibida.
1. Insira o **Título** e o **Nome** (opcional). Por exemplo, uma solicitação de hipoteca. Selecione **Concluído**.
1. Selecione o modelo de fluxo de trabalho criado e selecione **Editar**. Agora é possível adicionar etapas do fluxo de trabalho para criar uma lógica de negócios. Ao criar um modelo de fluxo de trabalho pela primeira vez, ele contém:

   * As etapas: Início do fluxo e Fim do fluxo. Essas etapas representam o início e o fim do workflow. Essas etapas são obrigatórias e não podem ser editadas ou removidas.
   * Um exemplo de etapa do participante chamada Etapa 1. Esta etapa é configurada para atribuir um item de trabalho ao usuário administrador. Remova esta etapa.

1. Ativar notificações por email. Você pode configurar um fluxo de trabalho centrado no Forms no OSGi para enviar notificações por email aos usuários ou atribuídos. Execute as seguintes configurações para ativar notificações por email:

   1. Vá para o gerenciador de configurações do AEM em `https://[server]:[port]/system/console/configMgr`.
   1. Abra a configuração **[!UICONTROL Day CQ Mail Service]**. Especifique um valor para os campos **[!UICONTROL Nome do host do servidor SMTP]**, **[!UICONTROL Porta do servidor SMTP]** e **[!UICONTROL &quot;Do&quot; endereço]**. Clique em **[!UICONTROL Salvar]**.
   1. Abra a configuração **[!UICONTROL Day CQ Link Externalizer]**. No campo **[!UICONTROL Domínios]**, especifique o nome do host/endereço IP real e o número da porta para as instâncias locais, de criação e de publicação. Clique em **[!UICONTROL Salvar]**.

1. Criar estágios de fluxo de trabalho. Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada do AEM e relatam o progresso do fluxo de trabalho.

   Para definir um estágio, selecione o ícone ![círculo de informações](assets/info-circle.png) para abrir as propriedades do modelo de fluxo de trabalho, abra a guia **Estágios**, adicione estágios para o modelo de fluxo de trabalho e selecione **Salvar e Fechar**. Para o exemplo de aplicativo de hipoteca, crie estágios: solicitação de empréstimo, status da solicitação de empréstimo, documentos a serem assinados e documento de empréstimo assinado.

1. Arraste e solte o navegador de etapas **Atribuir tarefa** no modelo de fluxo de trabalho. Faça dela a primeira etapa do modelo.

   O componente Atribuir tarefa atribui a tarefa, criada por fluxo de trabalho, a um usuário ou grupo. Junto com a atribuição da tarefa, você pode usar o componente para especificar um Formulário adaptável ou um PDF não interativo para a tarefa. O Formulário adaptável é necessário para aceitar entradas de usuários e PDF não interativos ou um Formulário adaptável somente leitura é usado para workflows somente revisão.

   Você também pode usar a etapa para controlar o comportamento da tarefa. Por exemplo, criar um Documento de registro automático, atribuir a tarefa a um usuário ou grupo específico, o caminho dos dados enviados, o caminho dos dados a serem pré-preenchidos e as ações padrão. Para obter informações detalhadas sobre as opções da etapa atribuir tarefa, consulte o [fluxo de trabalho centrado no Forms no OSGi - Referência da etapa](aem-forms-workflow.md).

   ![editor de fluxo de trabalho](assets/workflow-editor.png)

   Para o exemplo de aplicativo de hipoteca, configure a etapa atribuir tarefa para usar um Formulário adaptável somente leitura e exibir o Documento do PDF depois que a tarefa for concluída. Além disso, selecione para o grupo de usuários que tem permissão para aprovar a solicitação de empréstimo. Na guia **Ações**, desabilite a opção **Enviar**. Crie uma variável **actionTaken** do tipo de dados String e especifique a variável como a **Variável de Rota**. Por exemplo, actionTaken. Além disso, adicione as rotas Approve e Reject. As rotas são exibidas como ações separadas (botões) na Caixa de entrada do AEM. O fluxo de trabalho seleciona uma ramificação com base na ação (botão) tocada pelo usuário.

   É possível importar o pacote de exemplo, disponível para download no início da seção, para o conjunto completo de valores de todos os campos da etapa atribuir tarefa configurada, por exemplo, aplicativo de hipoteca.

1. Arraste e solte o componente de Divisão OR do navegador de etapas para o modelo de fluxo de trabalho. A divisão OR cria uma divisão no fluxo de trabalho, depois da qual apenas uma ramificação fica ativa. Essa etapa permite introduzir caminhos de processamento condicional no fluxo de trabalho. Adicione etapas do fluxo de trabalho a cada ramificação, conforme necessário.

   Você pode definir a expressão de roteamento para uma ramificação usando uma definição de regra, um script ECMA ou um script externo.

   Use o editor de expressão para criar expressões de roteamento para Ramificação 1 e Ramificação 2. Essas expressões de roteamento ajudam a escolher uma ramificação com base na ação do usuário na Caixa de entrada do AEM.

   **Expressão de roteamento para a Ramificação 1**

   Quando um usuário toca em **Aprovar** na Caixa de Entrada do AEM, a Ramificação 1 é ativada.

   ![OU Dividir exemplo](assets/orsplit_branch1_active_new.png)

   **Expressão de roteamento para a Ramificação 2**

   Quando um usuário toca em **Rejeitar** na Caixa de Entrada do AEM, a Ramificação 2 é ativada.

   ![OU Dividir exemplo](assets/orsplit_branch2_active_new.png)

   Para obter informações sobre como criar expressões de roteamento usando variáveis, consulte [Variáveis em [!DNL AEM Forms] fluxos de trabalho](variable-in-aem-workflows.md).

1. Adicione outras etapas do fluxo de trabalho para criar a lógica de negócios.

   Para o exemplo de hipoteca, adicione um gerar Documento de registro, duas etapas de atribuição de tarefa e uma etapa de documento de sinal à Ramificação 1 do modelo, conforme exibido na imagem abaixo. Uma etapa da tarefa de atribuição é exibir e enviar **documentos de empréstimo a serem assinados ao candidato** e outra componente da tarefa de atribuição é **exibir documentos assinados**. Além disso, adicione um componente Atribuir tarefa à ramificação 2. Está ativado quando um usuário toca em Rejeitar na Caixa de entrada do AEM.

   Para o conjunto completo de valores de todos os campos das etapas Atribuir tarefa, etapa Documento de registro e etapa assinar documento configurada por exemplo, aplicação de hipoteca, importar o pacote de exemplo, disponível para download no início desta seção.

   O modelo de fluxo de trabalho está pronto. É possível iniciar o workflow por meio de vários métodos. Para obter detalhes, consulte [Iniciar um fluxo de trabalho centrado no Forms no OSGi](#launch).

   ![hipoteca-editor-fluxo-de-trabalho](assets/workflow-editor-mortgage.png)

## Criar um aplicativo de fluxo de trabalho centrado no Forms {#create-a-forms-centric-workflow-application}

O aplicativo é o Formulário adaptável associado ao fluxo de trabalho. Quando um aplicativo é enviado por meio da Caixa de entrada, ele inicia o fluxo de trabalho associado. Para disponibilizar um fluxo de trabalho do Forms como um aplicativo na Caixa de Entrada do AEM e no Aplicativo [!DNL AEM Forms], faça o seguinte para criar um aplicativo de fluxo de trabalho:

>[!NOTE]
>
>Você deve ser membro do grupo fd-administrator para criar e gerenciar aplicativos de workflow.

1. Na instância do autor do AEM, vá para ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Gerenciar aplicativo de fluxo de trabalho]** e toque em **[!UICONTROL Criar]**.
1. Na janela Criar aplicativo de fluxo de trabalho, forneça entradas para os seguintes campos e toque em **Criar**. Um novo aplicativo é criado e listado na tela Workflow Applications.

<table>
 <tbody>
  <tr>
   <td>Texto</td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td>Título</td>
   <td>O título é visível na Caixa de entrada do AEM e ajuda os usuários a escolher um aplicativo. Mantenha-o descritivo. Por exemplo, Aplicativo de Abertura de Conta de Poupança.<br /> </td>
  </tr>
  <tr>
   <td>Nome </td>
   <td>Especifique o nome do aplicativo. Todos os caracteres diferentes das letras, números, hifens e sublinhados são substituídos por hifens. </td>
  </tr>
  <tr>
   <td>Descrição</td>
   <td>A descrição está visível na Caixa de entrada do AEM. Forneça informações detalhadas sobre o aplicativo nos campos de descrição. Por exemplo, Finalidade do aplicativo.<br /> </td>
  </tr>
  <tr>
   <td>Formulário adaptável</td>
   <td><p>Especifique o caminho de um Formulário adaptável. Quando um usuário inicia um aplicativo, o Formulário adaptável especificado é exibido.</p> <p><strong>Observação</strong>: os aplicativos de fluxo de trabalho não oferecem suporte a formulários e documentos do PDF com mais de uma página ou exigem rolagem no Apple iPad. Quando um aplicativo é aberto no Apple iPad e o formulário adaptável ou o documento do PDF é maior que uma página, os campos de formulário e o conteúdo da segunda página são perdidos.</p> </td>
  </tr>
  <tr>
   <td>Grupo de acesso</td>
   <td><p>Selecione um grupo. O aplicativo está visível na Caixa de Entrada do AEM somente para os membros do grupo selecionado. A opção access group disponibiliza todos os grupos do grupo [!DNL workflow-users] para seleção. </p> <br /> </td>
  </tr>
  <tr>
   <td>Preencher Serviço</td>
   <td>Selecione um <a href="prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">serviço de preenchimento prévio</a> para o Formulário adaptável.<br /> </td>
  </tr>
  <tr>
   <td>Modelo de fluxo de trabalho</td>
   <td>Selecione um <a href="aem-forms-workflow.md#create-a-workflow-model">modelo de fluxo de trabalho</a> para o aplicativo. Um modelo de fluxo de trabalho consiste na lógica e no fluxo do processo de negócios. </td>
  </tr>
  <tr>
   <td>Caminho do arquivo de dados</td>
   <td>Especifique o caminho do arquivo de dados no repositório crx. O caminho é relativo à carga do Formulário adaptável e contém o nome do arquivo de dados. Sempre inclua o nome completo do arquivo, incluindo a extensão, se aplicável. Por exemplo, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Caminho do anexo</td>
   <td>Especifique o caminho da pasta de anexos no repositório crx. O caminho do anexo é relativo ao local da carga útil. Por exemplo, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Caminho do documento de registro</td>
   <td>Especifique o caminho do arquivo do documento de registro no repositório crx. O caminho é relativo ao local da carga do formulário adaptável. Sempre inclua o nome completo do arquivo, incluindo a extensão, se aplicável. Por exemplo, [payload]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Inicie um fluxo de trabalho centrado no Forms no OSGi {#launch}

É possível iniciar ou acionar um fluxo de trabalho centrado no Forms ao:

* [Envio de um aplicativo da Caixa de entrada do AEM](#inbox)
* [Enviando um aplicativo do  [!DNL AEM Forms] Aplicativo](#afa)

* [Envio de um formulário adaptável](#af)
* [Usar pasta monitorada](#watched)

* [Enviar uma comunicação interativa ou uma carta](#letter)

### Envio de um aplicativo da Caixa de entrada do AEM {#inbox}

O aplicativo de workflow que você criou está disponível como um aplicativo na Caixa de entrada. Os usuários membros do grupo [!DNL workflow-users] podem preencher e enviar o aplicativo que aciona o fluxo de trabalho associado.

<!-- ### Submitting an application from [!DNL AEM Forms] App {#afa}

The [!DNL AEM Forms] app syncs with an [!DNL AEM Forms] server and lets you change the form data, tasks, workflow applications, and saved information (drafts/templates) in your account. For more information, see [[!DNL AEM Forms] app]((aem-forms-app.md) and related articles.-->

### Envio de um formulário adaptável {#af}

Você pode configurar as Ações enviar de um formulário adaptável para iniciar um fluxo de trabalho no envio do formulário adaptável. O Adaptive Forms fornece a Ação Enviar **Chamar um Fluxo de Trabalho do AEM** para iniciar um fluxo de trabalho no envio de um Formulário Adaptável. Para obter informações detalhadas sobre a Ação de Envio, consulte [Configurando a Ação de Envio](configuring-submit-actions.md). Para enviar um Formulário adaptável por meio do aplicativo [!DNL AEM Forms], habilite Sincronizar com o Aplicativo [!DNL AEM Forms] nas propriedades do Formulário adaptável.

<!-- You can configure an Adaptive Form to sync, submit, and trigger a workflow from [!DNL AEM Forms] app. For details, see [working with a form]((working-with-form.md). -->

<!-- ### Using a watched folder {#watched}

An administrator (a member of fd-administrators group) can configure a network folder to run a pre-configured workflow when a user places a file (such as a PDF file) in the folder. After the workflow completes, it can save the result file to a specified output folder. Such a folder is known as [Watched Folder](watched-folder-in-aem-forms.md). Perform the following procedure to configure a watched folder to launch a workflow:

1. On your AEM author instance, go to ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. A list of already configured watched folders is displayed.
1. Select **[!UICONTROL New]**. A list of fields is displayed. Specify a value for the following fields to configure a Watched Folder for a workflow:

<table>
 <tbody>
  <tr>
   <td>Field</td>
   <td>Description</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Name</code></td>
   <td>Specify the name of the Watched Folder. This field support only alphanumeric.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Path</code></td>
   <td>Specify the physical location of the Watched Folder. In a clustered environment, use a shared network folder that is accessible from AEM cluster node.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Process Files Using</code></td>
   <td>Select the <span class="uicontrol">Workflow </code>option. </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Workflow Model</code></td>
   <td>Select a workflow model.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Output File Pattern</code></td>
   <td>Specify the directory structure for output files and directories. </a>.</td>
  </tr>
 </tbody>
</table>

1. Select **Advanced**. Specify a value for the following field and taps **Create**. The Watched Folder is configured to launch a workflow. Now, whenever a file is placed in the input directory of the Watched Folder, the specified workflow is triggered.

   | Field |Description |
   |---|---|
   | Payload Mapper Filter |When you create a watched folder, it creates a folder structure in the crx-repository. The folder structure can serve as a payload to the workflow. You can write a script to map an AEM Workflow to accept inputs from the watched folder structure. An out of the box implementation is available and listed in the Payload Mapper Filter. If you do not have a custom implementation, select the default implementation. |

   The Advanced tab contains more fields. Most of these fields contain a default value. To learn about all the fields, see the [Create or Configure a watched folder]((admin-help/configuring-watched-folder-endpoints.md) article. -->

<!-- ### Submitting an interactive communication or a letter {#letter}

You can associate and execute a Forms-centric workflow on OSGi on submission of an interactive communication or a letter. In correspondence management workflows are used for post processing interactive communications and letters. For example, emailing, printing, faxing, or archiving final letters. For detailed steps, see [Post processing of interactive communications and letters](submit-letter-topostprocess.md).

## Additional Configurations {#additional-configurations}

### Configure email service {#configure-email-service}

You can use the Assign Task and Send Email steps of AEM Workflows to send an email. Perform the following steps to specify email servers and other configurations required to send email:

1. Go to AEM configuration manager at `https://[server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Day CQ Mail Service]** configuration. Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port]**, and **[!UICONTROL "From" address]** fields. Click **[!UICONTROL Save]**.
1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual hostname/IP address and port number for local, author, and publish instances. Click **[!UICONTROL Save]**. -->

### Limpar instâncias de fluxo de trabalho {#purge-workflow-instances}

Minimizar o número de instâncias de fluxo de trabalho aumenta o desempenho do mecanismo de fluxo de trabalho, para que você possa remover regularmente do repositório as instâncias de fluxo de trabalho concluídas ou em execução. Para obter informações detalhadas, consulte [Limpeza regular de instâncias de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=pt-BR) limpeza de instâncias de fluxo de trabalho
