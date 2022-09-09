---
title: Fluxo de trabalho centrado no Forms no OSGi
seo-title: Rapidly build Adaptive Forms-based processes, automate document services operations, and use Adobe Sign with AEM workflows
description: Use [!DNL AEM Forms] Fluxo de trabalho para automatizar e criar rapidamente revisões e aprovações, para iniciar serviços de documento
seo-description: Use [!DNL AEM Forms] Workflow to automate and rapidly build review and approvals, to start document services (For example, to convert a PDF document to another format), integrate with Adobe Sign signature workflow, and more.
uuid: 797ba0f7-a378-45ac-9f82-fa9a952027be
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 73e63493-e821-443f-b50d-10797360f5d1
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 2%

---


# Fluxo de trabalho centrado no Forms no OSGi{#forms-centric-workflow-on-osgi}

![](do-not-localize/header.png)

As empresas coletam dados de centenas e milhares de formulários, vários sistemas back-end e fontes de dados online ou offline. Eles também têm um conjunto dinâmico de usuários para tomar decisões sobre os dados, o que envolve processos iterativos de revisão e aprovação.

Juntamente com fluxos de trabalho de revisão e aprovação para públicos internos e externos, grandes organizações e empresas têm tarefas repetitivas. Por exemplo, converter um documento PDF para outro formato. Quando realizadas manualmente, essas tarefas demoram muito tempo e recursos. As empresas também têm requisitos legais para assinar digitalmente um documento e arquivar dados de formulário para uso posterior em formatos predefinidos.

## Introdução ao fluxo de trabalho centrado no Forms no OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Você pode usar fluxos de trabalho AEM para criar rapidamente fluxos de trabalho baseados em Forms adaptáveis. Esses fluxos de trabalho podem ser usados para revisão e aprovações, fluxos de processos comerciais, para iniciar serviços de documento, integrar com o fluxo de trabalho de assinatura do Adobe Sign e operações semelhantes. Por exemplo, processamento de aplicativos de cartão de crédito, fluxo de trabalho de aprovação de licença de funcionário, salvando um formulário como um documento PDF. Além disso, esses fluxos de trabalho podem ser usados em uma organização ou por meio de um firewall de rede.

Com o fluxo de trabalho centrado na Forms no OSGi, você pode criar e implantar rapidamente fluxos de trabalho para várias tarefas na pilha OSGi, sem precisar instalar o recurso completo de Gerenciamento de processos na pilha JEE. O desenvolvimento e o gerenciamento de workflows usam os recursos conhecidos AEM Fluxo de trabalho e AEM Caixa de entrada. Os fluxos de trabalho são a base para automatizar processos de negócios reais que abrangem vários sistemas de software, redes, departamentos e até mesmo organizações.

Após a configuração, esses workflows podem ser acionados manualmente para concluir um processo definido ou serem executados de forma programática quando os usuários enviam um formulário <!-- or [correspondence management](cm-overview.md) letter-->. <!-- With this enhanced AEM Workflow capabilities, [!DNL AEM Forms] offers two distinct, yet similar, capabilities. As part of your deployment strategy, you need to decide which one works for you. See a [comparison](capabilities-osgi-jee-workflows.md) of the Forms-centric AEM Workflows on OSGi and Process Management on JEE. Moreover, for the deployment topology see, [Architecture and deployment topologies for [!DNL AEM Forms]]((aem-forms-architecture-deployment.md). -->

O fluxo de trabalho centrado no Forms no OSGi estende [Caixa de entrada AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html#authoring) e fornece componentes extras (etapas) para AEM editor de fluxo de trabalho para adicionar suporte ao [!DNL AEM Forms]Fluxos de trabalho centrados em . <!-- The extended AEM Inbox has functionalities similar to [[!DNL AEM Forms] Workspace](introduction-html-workspace.md). Along with managing human-centric workflows (Approval, Review, and so on), you can use AEM workflows to automate [document services](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem)-related operations (for example, Generate PDF) and electronically signing (Adobe Sign) documents. -->

Todos [!DNL AEM Forms] as etapas do fluxo de trabalho oferecem suporte para o uso de variáveis. As variáveis permitem que as etapas do fluxo de trabalho mantenham e transmitam metadados pelas etapas no tempo de execução. Você pode criar diferentes tipos de variáveis para armazenar diferentes tipos de dados. Você também pode criar coleções variáveis (matriz) para armazenar várias instâncias de dados relacionados do mesmo tipo. Normalmente, você usa uma variável ou uma coleção de variáveis quando precisa tomar uma decisão com base no valor que ela contém ou armazenar informações necessárias posteriormente em um processo. Para obter mais informações sobre como usar variáveis nesses componentes de fluxo de trabalho centrados no Forms (etapas), consulte [Fluxo de trabalho centrado na Forms no OSGi - Referência em etapas](aem-forms-workflow-step-reference.md). Para obter informações sobre como criar e gerenciar variáveis, consulte [Variáveis em workflows AEM](variable-in-aem-workflows.md).

O diagrama a seguir descreve o procedimento completo para criar, executar e monitorar um fluxo de trabalho centrado na Forms no OSGi.

![fluxo de trabalho de introdução ao aem-forms](assets/introduction-to-aem-forms-workflow.jpg)

## Antes de você iniciar {#before-you-start}

* Um fluxo de trabalho é uma representação de um processo de negócios do mundo real. Mantenha seu processo de negócios real e a lista dos participantes do processo de negócios prontos. Além disso, mantenha o material adicional (Adaptive Forms, PDF Documents e muito mais) pronto antes de começar a criar um fluxo de trabalho.
* Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada de AEM e no relatório de ajuda sobre o progresso do fluxo de trabalho. Divida seu processo de negócios em estágios lógicos.
* Você pode configurar a etapa de atribuição de fluxos de trabalho AEM para enviar notificações por email aos usuários ou destinatários. Então, [ativar notificações por email](#configure-email-service).
* Um fluxo de trabalho também pode usar o sinal de Adobe para assinaturas digitais. Se você planeja usar o Adobe Sign em um workflow, a variável [configurar o Adobe Sign para [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) antes de usá-lo em um workflow.

## Criar um modelo de fluxo de trabalho {#create-a-workflow-model}

Um modelo de fluxo de trabalho consiste em lógica e fluxo de um processo de negócios. Ele é composto por uma série de etapas. Essas etapas são componentes AEM. É possível estender as etapas do fluxo de trabalho com parâmetros e scripts para fornecer mais funcionalidade e controle, conforme necessário. [!DNL AEM Forms] O fornece algumas etapas além AEM etapas disponíveis para uso imediato. Para obter uma lista detalhada de AEM e [!DNL AEM Forms] etapas, consulte [Referência em etapas do fluxo de trabalho AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) e [Fluxo de trabalho centrado na Forms no OSGi - Referência em etapas](aem-forms-workflow.md).

O AEM oferece uma interface de usuário intuitiva para criar um modelo de fluxo de trabalho usando as etapas de fluxo de trabalho fornecidas. Para obter instruções passo a passo para criar um modelo de fluxo de trabalho, consulte [Criação de modelos de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/workflows/overview.html#workflows). O exemplo a seguir fornece instruções passo a passo para criar um modelo de fluxo de trabalho para um fluxo de trabalho de aprovação e revisão:

>[!NOTE]
>
>Você deve ser um membro do grupo editor de fluxo de trabalho para criar ou editar um modelo de fluxo de trabalho.

### Criar um modelo para um fluxo de trabalho de aprovação e revisão {#create-a-model-for-an-approval-and-review-workflow}

O fluxo de trabalho de aprovação e revisão é para as tarefas que exigem intervenção humana para tomar decisões. O exemplo a seguir cria um modelo de fluxo de trabalho para um pedido de empréstimo hipotecário ser preenchido por um agente bancário de front office. Depois que o aplicativo é preenchido, ele é enviado para aprovação. Posteriormente, o pedido aprovado é enviado ao requerente para assinatura eletrônica através da Adobe Sign.

O exemplo está disponível como um pacote anexado abaixo. Importe e instale o exemplo usando o gerenciador de pacotes. Você também pode executar as seguintes etapas para criar manualmente o modelo de fluxo de trabalho para o aplicativo:

O exemplo cria um modelo de fluxo de trabalho para um aplicativo de hipoteca ser preenchido por um agente bancário de front-office. Uma vez preenchido, o aplicativo é enviado para aprovação. Posteriormente, o aplicativo aprovado será enviado ao cliente para assinatura eletrônica usando o Adobe Sign. Você pode importar e instalar o exemplo usando o gerenciador de pacotes.

[Obter arquivo](assets/example-mortgage-loan-application.zip)

1. Abra o console Modelos de fluxo de trabalho . O URL padrão é `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Selecionar **Criar**, em seguida **Criar modelo**. A caixa de diálogo Adicionar modelo de fluxo de trabalho é exibida.
1. Insira o **Título** e **Nome** (opcional). Por exemplo, um aplicativo de hipoteca. Toque **Concluído**.
1. Selecione o modelo de fluxo de trabalho recém-criado e toque em **Editar**. Agora, você pode adicionar etapas de fluxo de trabalho para criar lógica de negócios. Ao criar um modelo de fluxo de trabalho pela primeira vez, ele contém:

   * As etapas: Início e Fim do Fluxo. Essas etapas representam o início e o fim do workflow. Essas etapas são obrigatórias e não podem ser editadas ou removidas.
   * Um exemplo de Etapa do participante chamada Etapa 1. Essa etapa é configurada para atribuir um item de trabalho ao usuário administrador. Remova esta etapa.

1. Habilite notificações por email. Você pode configurar o fluxo de trabalho centrado no Forms no OSGi para enviar notificações por email aos usuários ou destinatários. Execute as seguintes configurações para ativar notificações por email:

   1. Vá para AEM gerenciador de configuração em `https://[server]:[port]/system/console/configMgr`.
   1. Abra o **[!UICONTROL Day CQ Mail Service]** configuração. Especifique um valor para a variável **[!UICONTROL Nome do host do servidor SMTP]**, **[!UICONTROL porta do servidor SMTP,]** e **[!UICONTROL Endereço &quot;De&quot;]** campos. Clique em **[!UICONTROL Salvar]**.
   1. Abra o **[!UICONTROL Externalizador de links CQ do dia]** configuração. No **[!UICONTROL Domínios]** , especifique o nome do host/endereço IP real e o número da porta para instâncias locais, de autor e de publicação. Clique em **[!UICONTROL Salvar]**.

1. Crie estágios do fluxo de trabalho. Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada de AEM e no progresso do relatório do fluxo de trabalho.

   Para definir um estágio, toque no ![info-círculo](assets/info-circle.png) ícone para abrir as propriedades do modelo de fluxo de trabalho, abra o **Estágios** , adicione estágios para o modelo de fluxo de trabalho e toque em **Salvar e fechar**. Para o exemplo de aplicativo de hipoteca, crie estágios: solicitação de empréstimo, status de solicitação de empréstimo, para ser assinado e documento de empréstimo assinado.

1. Arraste e solte a **Atribuir tarefa** etapas do navegador para o modelo de fluxo de trabalho. Faça dele o primeiro passo do modelo.

   O componente Atribuir tarefa atribui a tarefa, criada por workflow, a um usuário ou grupo. Ao atribuir a tarefa, você pode usar o componente para especificar um Formulário adaptável ou um PDF não interativo para a tarefa. O formulário adaptável é necessário para aceitar a entrada de usuários e o PDF não interativo ou um formulário adaptável somente leitura é usado para fluxos de trabalho de revisão somente.

   Você também pode usar a etapa para controlar o comportamento da tarefa. Por exemplo, criar um Documento de registro automático, atribuir a tarefa a um usuário ou grupo específico, o caminho dos dados enviados, o caminho dos dados a serem preenchidos previamente e as ações padrão. Para obter informações detalhadas sobre as opções da etapa de atribuição de tarefa, consulte [Fluxo de trabalho centrado na Forms no OSGi - Referência em etapas](aem-forms-workflow.md) documento.

   ![editor de fluxo de trabalho](assets/workflow-editor.png)

   Para o exemplo do aplicativo de hipoteca, configure a etapa de atribuição de tarefa para usar um Formulário adaptável somente leitura e exibir Documento PDF após a conclusão da tarefa. Além disso, selecione para o grupo de usuários com permissão para aprovar a solicitação de empréstimo. No **Ações** , desative o **Enviar** opção. Crie um **actionTaken** variável do tipo de dados String e especifique a variável como **Variável de rota**. Por exemplo, actionTaken. Além disso, adicione as rotas Approve e Reject . As rotas são exibidas como ações separadas (botões) AEM Caixa de entrada. O workflow seleciona uma ramificação com base na ação (botão) que um usuário toca.

   É possível importar o pacote de exemplo, disponível para download no início da seção, para o conjunto completo de valores de todos os campos da etapa de tarefa de atribuição configurada, por exemplo, aplicativo de hipoteca.

1. Arraste e solte o componente OU Dividir do navegador da etapa para o modelo de fluxo de trabalho. A divisão OR cria uma divisão no fluxo de trabalho, após a qual apenas uma ramificação está ativa. Essa etapa permite introduzir caminhos de processamento condicional no fluxo de trabalho. Adicione etapas de fluxo de trabalho a cada ramificação, conforme necessário.

   Você pode definir uma expressão de roteamento para uma ramificação usando uma definição de regra, um script ECMA ou um script externo.

   Use o editor de expressão para criar expressões de roteamento para Ramificação 1 e Ramificação 2. Essas expressões de roteamento ajudam a escolher uma ramificação com base na ação do usuário AEM Caixa de entrada.

   **Expressão de roteamento para Ramificação 1**

   Quando um usuário toca **Aprovar** AEM Caixa de entrada, a Ramificação 1 é ativada.

   ![OU Exemplo de divisão](assets/orsplit_branch1_active_new.png)

   **Expressão de roteamento para Ramificação 2**

   Quando um usuário toca **Rejeitar** AEM Caixa de entrada, a Ramificação 2 é ativada.

   ![OU Exemplo de divisão](assets/orsplit_branch2_active_new.png)

   Para obter informações sobre como criar expressões de roteamento usando variáveis, consulte [Variáveis em [!DNL AEM Forms] workflows](variable-in-aem-workflows.md).

1. Adicione outras etapas do fluxo de trabalho para criar a lógica de negócios.

   Para o exemplo de hipoteca, adicione um Documento de Registro gerado, duas etapas de tarefa de atribuição e uma etapa de documento de assinatura à Ramificação 1 do modelo, conforme exibido na imagem abaixo. Uma etapa de tarefa Atribuir é exibir e enviar **ser assinados documentos de empréstimo ao candidato** e outro componente de atribuição de tarefa é **para exibir documentos assinados**. Além disso, adicione um componente de tarefa à ramificação 2. Ela é ativada, quando um usuário toca em Rejeitar AEM Caixa de entrada.

   Para o conjunto completo de valores de todos os campos das etapas da tarefa de atribuição, etapa Documento de registro e etapa de assinatura de documento configuradas por exemplo aplicativo de hipoteca, importe o pacote de exemplo, disponível para download no início desta seção.

   O modelo de fluxo de trabalho está pronto. Você pode iniciar o workflow por meio de vários métodos. Para obter detalhes, consulte [Iniciar um fluxo de trabalho centrado na Forms no OSGi](#launch).

   ![workflow-editor-hipoteca](assets/workflow-editor-mortgage.png)

## Criar um aplicativo de fluxo de trabalho centrado no Forms {#create-a-forms-centric-workflow-application}

O aplicativo é o formulário adaptável associado ao fluxo de trabalho. Quando um aplicativo é enviado por meio da Caixa de entrada, ele inicia o fluxo de trabalho associado. Para disponibilizar um fluxo de trabalho do Forms como um aplicativo na Caixa de entrada AEM e [!DNL AEM Forms] Aplicativo, faça o seguinte para criar um aplicativo de fluxo de trabalho:

>[!NOTE]
>
>Você deve ser um membro do grupo fd-administrators para poder criar e gerenciar aplicativos de fluxo de trabalho.

1. Na instância do autor do AEM, acesse ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Gerenciar aplicativo de fluxo de trabalho]** e torneiras **[!UICONTROL Criar]**.
1. Na janela Criar aplicativo de fluxo de trabalho , forneça entradas para os seguintes campos e toque em **Criar**. Um novo aplicativo é criado e é listado na tela Aplicativos de fluxo de trabalho .

<table>
 <tbody>
  <tr>
   <td>Texto</td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td>Título</td>
   <td>O título é visível AEM Caixa de entrada e ajuda os usuários a escolher um aplicativo. Mantenha-o descritivo. Por exemplo, Salvar Conta Abrindo Aplicativo.<br /> </td>
  </tr>
  <tr>
   <td>Nome </td>
   <td>Especifique o nome do aplicativo. Todos os caracteres, exceto alfabetos, números, hifens e sublinhados, são substituídos por hifens. </td>
  </tr>
  <tr>
   <td>Descrição</td>
   <td>A descrição é visível AEM Caixa de entrada. Forneça informações detalhadas sobre o aplicativo nos campos de descrição. Por exemplo, Finalidade do aplicativo.<br /> </td>
  </tr>
  <tr>
   <td>Formulário adaptativo</td>
   <td><p>Especifique o caminho de um formulário adaptável. Quando um usuário inicia um aplicativo, o formulário adaptável especificado é exibido.</p> <p><strong>Observação</strong>: Os aplicativos de fluxo de trabalho não suportam formulários e documentos PDF que sejam maiores que uma página ou que exijam rolagem no Apple iPad. Quando um aplicativo é aberto no Apple iPad e o formulário adaptável ou o documento PDF é maior que uma página, os campos do formulário e o conteúdo da segunda página são perdidos.</p> </td>
  </tr>
  <tr>
   <td>Grupo de acesso</td>
   <td><p>Selecione um grupo. O aplicativo é visível AEM Caixa de entrada somente para os membros do grupo selecionado. A opção de grupo de acesso torna todos os grupos do [!DNL workflow-users] grupo disponível para seleção. </p> <br /> </td>
  </tr>
  <tr>
   <td>Preencher Serviço</td>
   <td>Selecione um <a href="prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">serviço de preenchimento prévio</a> para o formulário adaptável.<br /> </td>
  </tr>
  <tr>
   <td>Modelo de fluxo de trabalho</td>
   <td>Selecione um <a href="aem-forms-workflow.md#create-a-workflow-model">modelo de fluxo de trabalho</a> para o aplicativo. Um modelo de fluxo de trabalho consiste em lógica e fluxo do processo de negócios. </td>
  </tr>
  <tr>
   <td>Caminho do arquivo de dados</td>
   <td>Especifique o caminho do arquivo de dados no repositório crx. O caminho é relativo à carga do formulário adaptável e contém o nome do arquivo de dados. Sempre inclua o nome completo do arquivo, incluindo a extensão, se aplicável. Por exemplo, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Caminho do anexo</td>
   <td>Especifique o caminho da pasta de anexos no repositório crx. O caminho do anexo é relativo ao local da carga útil. Por exemplo, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Caminho do documento de registro</td>
   <td>Especifique o caminho do arquivo Documento de registro no repositório crx. O caminho é relativo ao local da carga do formulário adaptável. Sempre inclua o nome completo do arquivo, incluindo a extensão, se aplicável. Por exemplo, [payload]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Iniciar um fluxo de trabalho centrado na Forms no OSGi {#launch}

Você pode iniciar ou acionar um fluxo de trabalho centrado no Forms ao:

* [Envio de um aplicativo AEM Caixa de entrada](#inbox)
* [Apresentação de um pedido a partir de [!DNL AEM Forms] Aplicativo](#afa)

* [Envio de um formulário adaptável](#af)
* [Usar pasta assistida](#watched)

* [Envio de uma comunicação interativa ou uma carta](#letter)

### Envio de um aplicativo AEM Caixa de entrada {#inbox}

O aplicativo de fluxo de trabalho criado está disponível como um aplicativo na Caixa de entrada. Usuários que são membros de [!DNL workflow-users] pode preencher e enviar o aplicativo que aciona o fluxo de trabalho associado. Para obter informações sobre como usar AEM Caixa de entrada para enviar aplicativos e gerenciar tarefas, consulte [Gerenciar aplicativos e tarefas do Forms na Caixa de entrada AEM](manage-applications-inbox.md).

<!-- ### Submitting an application from [!DNL AEM Forms] App {#afa}

The [!DNL AEM Forms] app syncs with an [!DNL AEM Forms] server and allows you to make changes to the form data, tasks, workflow applications, and saved information (drafts/templates) in your account. For more information, see [[!DNL AEM Forms] app]((aem-forms-app.md) and related articles.-->

### Envio de um formulário adaptável {#af}

É possível configurar as ações de envio de um formulário adaptável para iniciar um fluxo de trabalho no envio do formulário adaptável. O Adaptive Forms fornece o **Chamar um fluxo de trabalho AEM** Enviar ação para iniciar um fluxo de trabalho após o envio de um formulário adaptável. Para obter informações detalhadas sobre a Ação de envio, consulte [Configurar a ação de envio](configuring-submit-actions.md). Para enviar um formulário adaptável por meio do [!DNL AEM Forms] aplicativo, habilite Sincronizar com [!DNL AEM Forms] Aplicativo nas propriedades do formulário adaptável.

<!-- You can configure an Adaptive Form to sync, submit, and trigger a workflow from [!DNL AEM Forms] app. For details, see [working with a form]((working-with-form.md). -->

<!-- ### Using a watched folder {#watched}

An administrator (a member of fd-administrators group) can configure a network folder to run a pre-configured workflow when a user places a file (such as a PDF file) in the folder. After the workflow completes, it can save the result file to a specified output folder. Such a folder is known as [Watched Folder](watched-folder-in-aem-forms.md). Perform the following procedure to configure a watched folder to launch a workflow:

1. On your AEM author instance, go to ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. A list of already configured watched folders is displayed.
1. Tap **[!UICONTROL New]**. A list of fields is displayed. Specify a value for the following fields to configure a Watched Folder for a workflow:

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

1. Tap **Advanced**. Specify a value for the following field and taps **Create**. The Watched Folder is configured to launch a workflow. Now, whenever a file is placed in the input directory of the Watched Folder, the specified workflow is triggered.

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
1. Open the **[!UICONTROL Day CQ Mail Service]** configuration. Specify a value for the **[!UICONTROL SMTP server host name]**, **[!UICONTROL SMTP server port,]** and **[!UICONTROL "From" address]** fields. Click **[!UICONTROL Save]**.
1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration. In the **[!UICONTROL Domains]** field, specify the actual hostname/IP address and port number for local, author, and publish instances. Click **[!UICONTROL Save]**. -->

### Limpar instâncias do fluxo de trabalho {#purge-workflow-instances}

Minimizar o número de instâncias de fluxo de trabalho aumenta o desempenho do motor de workflow. Portanto, você pode remover regularmente do repositório as instâncias de fluxo de trabalho concluídas ou em execução. Para obter informações detalhadas, consulte [Limpeza regular de instâncias de fluxo de trabalho](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=pt-BR) limpeza de instâncias de fluxo de trabalho
