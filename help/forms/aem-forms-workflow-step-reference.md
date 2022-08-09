---
title: 'Como atribuir um fluxo de trabalho a outro usuário, enviar email, usar o Adobe Sign em um fluxo de trabalho? '
description: Os fluxos de trabalho centrados no Forms permitem que você crie rapidamente os fluxos de trabalho baseados no Adaptive Forms. Você pode usar o Adobe Sign para assinar documentos por email, criar processos comerciais baseados em formulários, recuperar e enviar dados para várias fontes de dados e enviar notificações por email
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
source-git-commit: ebd7942cfaa7717d68ad039f3e0301cb52cbcec7
workflow-type: tm+mt
source-wordcount: '6098'
ht-degree: 0%

---

# Fluxos de trabalho de AEM centrados na Forms - Referência em etapas {#forms-centric-workflow-on-osgi-step-reference}

Você usa modelos de fluxo de trabalho para converter uma lógica de negócios em um processo repetitivo automatizado. Um modelo ajuda você a definir e executar uma série de etapas. Você também pode definir propriedades de modelo, como se o fluxo de trabalho é transitório ou usa vários recursos. Você pode [incluir várias etapas do fluxo de trabalho AEM em um modelo para atingir a lógica de negócios](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem).

## Etapas centradas na Forms {#forms-workflow-steps}

As etapas do fluxo de trabalho centradas no Forms executam operações específicas do AEM Forms em um Fluxo de trabalho AEM. Essas etapas permitem que você crie rapidamente um fluxo de trabalho adaptável, baseado no Forms e centrado no OSGi. Esses fluxos de trabalho podem ser usados para desenvolver fluxos de trabalho básicos de revisão e aprovação, processos de negócios internos e entre firewall. Você também pode usar as etapas do Forms Workflow para:

* Crie processos de negócios, fluxos de trabalho pós-envio e fluxos de trabalho de backend para gerenciar processos de inscrição.

* Crie e atribua tarefas a um usuário ou grupo.

* Use [!DNL Adobe Sign] em um fluxo de trabalho AEM para enviar um documento para assinatura.

* Gere um Documento de registro sob demanda ou no envio do formulário.

* Conecte um modelo de fluxo de trabalho a várias fontes de dados para salvar e recuperar dados facilmente.

* Use a etapa de email para enviar emails de notificação e outros anexos ao concluir uma ação e no início ou na conclusão de um workflow.

>[!NOTE]
>
>Se o modelo de fluxo de trabalho estiver marcado para um armazenamento externo, em seguida, para todas as etapas do fluxo de trabalho do Forms, você poderá selecionar apenas a opção de variável para armazenar ou recuperar arquivos de dados e anexos.


## Atribuir etapa da tarefa {#assign-task-step}

A etapa Atribuir tarefa cria um item de trabalho e o atribui a um usuário ou grupo. Ao atribuir a tarefa, o componente também especifica o Formulário adaptativo ou o PDF não interativo para a tarefa. O formulário adaptável é necessário para aceitar a entrada de usuários e o PDF não interativo ou um formulário adaptável somente leitura é usado para fluxos de trabalho de revisão somente.

Você também pode usar o componente para controlar o comportamento da tarefa. Por exemplo, criar um Documento de registro automático, atribuir a tarefa a um usuário ou grupo específico, especificar o caminho dos dados enviados, especificar o caminho dos dados a serem preenchidos previamente e especificar ações padrão. A etapa Atribuir tarefa tem as seguintes propriedades:

* **[!UICONTROL Título]**: Título da tarefa. O título é exibido AEM Caixa de entrada.
* **[!UICONTROL Descrição]**: Explicação das operações que estão sendo executadas na tarefa. Essas informações são úteis para outros desenvolvedores de processos quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

* **[!UICONTROL Caminho da miniatura]**: Caminho da miniatura da tarefa. Se nenhum caminho for especificado, para uma miniatura padrão do Formulário adaptável será exibida e para Documento de registro, um ícone padrão será exibido.
* **[!UICONTROL Estágio do fluxo de trabalho]**: Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada de AEM. É possível definir esses estágios nas propriedades do modelo (Sidekick > Página > Propriedades da página > Estágios).
* **[!UICONTROL Prioridade]**: A prioridade selecionada é exibida na Caixa de entrada de AEM. As opções disponíveis são Alto, Médio e Baixo. O valor padrão é Médio.
* **[!UICONTROL Data de vencimento]**: Especifique o número de dias ou horas após as quais a tarefa está marcada vencida. Se você selecionar **[!UICONTROL Desligado]**, a tarefa nunca será marcada como atrasada. Você também pode especificar um manipulador de tempo limite para executar tarefas específicas depois que a tarefa estiver vencida.

* **[!UICONTROL Dias]**: O número de dias antes do qual a tarefa deve ser concluída. O número de dias é contado após a tarefa ser atribuída a um usuário. Se uma tarefa não estiver concluída e cruzar o número de dias especificado no campo Dias , então, se selecionado, um manipulador de tempo limite será acionado após a data de vencimento.
* **[!UICONTROL Horas]**: O número de horas antes do qual a tarefa deve ser concluída. O número de horas é contado após a tarefa ser atribuída a um usuário. Se uma tarefa não estiver concluída e cruzar o número de horas especificado no campo Horas , então, se selecionado, um manipulador de tempo limite será acionado após as horas de vencimento.
* **[!UICONTROL Tempo limite após a data de vencimento]**: Selecione esta opção para ativar o campo de seleção Manipulador de tempo limite.
* **[!UICONTROL Manipulador de tempo limite]**: Selecione o script a ser executado quando a etapa Atribuir tarefa atravessar a data de vencimento. Scripts colocados no repositório CRX em [aplicativos]/fd/dashboard/scripts/timeoutHandler estão disponíveis para seleção. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo.
* **[!UICONTROL Destaque a ação e o comentário da última tarefa em Detalhes da Tarefa]**: Selecione esta opção para exibir a última ação executada e o comentário recebido na seção de detalhes da tarefa de uma tarefa.
* **[!UICONTROL Tipo]**: Escolha o tipo de documento a ser preenchido quando o workflow for iniciado. Você pode escolher um formulário adaptável, formulário adaptável somente leitura, um documento PDF não interativo.

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL Usar formulário adaptável]**: Especifique o método para localizar o Formulário adaptável de entrada. Essa opção estará disponível se você selecionar Formulário adaptável ou Formulário adaptável somente leitura na lista suspensa Tipo . É possível usar o formulário adaptável enviado para o fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo String para especificar o caminho.\
   Você pode associar vários adaptadores Forms a um fluxo de trabalho. Como resultado, você pode especificar um formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL Caminho do formulário adaptável]**: Especifique o caminho do formulário adaptável. É possível usar o formulário adaptável enviado para o fluxo de trabalho, disponível em um caminho absoluto, ou recuperar o formulário adaptável de um caminho armazenado em uma variável do tipo de dados da string.
* **[!UICONTROL Selecionar PDF de entrada usando]**: Especifique o caminho de um documento PDF não interativo. O campo fica disponível ao escolher um documento de PDF não interativo no campo Tipo. Você pode selecionar o PDF de entrada usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Diretório_de_carga]/Workflow/PDF/credit-card.pdf. O caminho não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. Você precisa ter uma opção Documento de registro ativada ou o modelo de formulário baseado em Adaptive Forms para usar a opção PDF path .
* **[!UICONTROL Para tarefas concluídas, renderize o Formulário adaptável como]**: Quando uma tarefa é marcada como concluída, é possível renderizar o Formulário adaptável como um formulário adaptável somente leitura ou um documento PDF. É necessário ativar uma opção Documento de registro ou Forms adaptável baseado em modelo de formulário para renderizar o Formulário adaptável como Documento de registro.
* **[!UICONTROL Pré-preenchido]**: Os seguintes campos listados abaixo servem como entradas para a tarefa:

   * **[!UICONTROL Selecione o arquivo de dados de entrada usando]**: Caminho do arquivo de dados de entrada (.json, .xml, .doc ou modelo de dados de formulário). Você pode recuperar o arquivo de dados de entrada usando um caminho relativo à carga útil ou recuperar o arquivo armazenado em uma variável do tipo de dados Document, XML ou JSON. Por exemplo, o arquivo contém os dados enviados para o formulário por meio de um aplicativo AEM Caixa de entrada. Um caminho de exemplo é [Diretório_de_carga]/workflow/data.
   * **[!UICONTROL Selecionar anexos de entrada usando]**: Os anexos disponíveis no local são anexados ao formulário associado à tarefa. O caminho pode ser relativo à carga útil ou recuperar o anexo armazenado em uma variável de um documento. Um caminho de exemplo é [Diretório_de_carga]/anexos/. Você pode especificar anexos colocados em relação à carga útil ou usar uma variável do tipo de documento (Lista de matriz > Documento) para especificar um anexo de entrada para o Formulário adaptável.

   <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL Solicitar mapeamento de atributo]**: Use a seção Mapeamento de atributos da solicitação para definir a variável [nome e valor do atributo de solicitação](work-with-form-data-model.md#bindargument). Recupere os detalhes da fonte de dados com base no nome e no valor do atributo especificados na solicitação. Você pode definir um valor de atributo de solicitação usando um valor literal ou uma variável do tipo de dados String.

   <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL Informações enviadas]**: Os seguintes campos listados abaixo servem como locais de saída para a tarefa:

   * **[!UICONTROL Salve o arquivo de dados de saída usando]**: Salve o arquivo de dados (.json, .xml, .doc ou modelo de dados do formulário). O arquivo de dados contém informações enviadas por meio do formulário associado. Você pode salvar o arquivo de dados de saída usando um caminho relativo à carga ou armazená-lo em uma variável do tipo de dados Document, XML ou JSON. Por exemplo, [Diretório_de_carga]/Workflow/data, onde os dados são um arquivo.
   * **[!UICONTROL Salvar anexos usando]**: Salve o formulário fornecido nos anexos em uma tarefa. Você pode salvar os anexos usando um caminho relativo à carga ou armazená-lo em uma variável da lista de matriz do tipo de dados Documento.
   * **[!UICONTROL Salvar documento de registro usando]**: Caminho para salvar um arquivo de Documento de registro. Por exemplo, [Diretório_de_carga]/DocumentofRecord/credit-card.pdf. Você pode salvar o Documento de registro usando um caminho relativo à carga útil ou armazená-lo em uma variável do tipo de dados do Documento. Se você selecionar **[!UICONTROL Em relação à carga]** , o Documento de registro não será gerado se o campo de caminho ficar vazio. Essa opção só estará disponível se você selecionar Formulário adaptável na lista suspensa Tipo .

   <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL Destinatário]** > **[!UICONTROL Atribuir opções]**: Especifique o método para atribuir a tarefa a um usuário. Você pode atribuir dinamicamente a tarefa a um usuário ou grupo usando o script do Seletor de Participante ou atribuir a tarefa a um usuário ou grupo de AEM específico.
* **[!UICONTROL Seletor de participante]**: A opção está disponível quando a variável **[!UICONTROL Dinamicamente para um usuário ou grupo]** está selecionada no campo Assign options . Você pode usar um ECMAScript ou um serviço para selecionar dinamicamente um usuário ou grupo. Para obter mais informações, consulte [Atribuir dinamicamente um fluxo de trabalho aos usuários](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) e [Criando uma etapa personalizada do Adobe Experience Manager Dynamic Participant.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **[!UICONTROL Participantes]**: O campo está disponível quando a variável **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** é selecionada na variável **[!UICONTROL Seletor de participante]** campo. O campo permite selecionar usuários ou grupos para a opção RandomParticipantChooser.

* **[!UICONTROL Destinatário]**: O campo está disponível quando a variável **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** é selecionado no **[!UICONTROL Seletor de participante]** campo. O campo permite selecionar uma variável do tipo de dados String para definir o destinatário.

* **[!UICONTROL Argumentos]**: O campo fica disponível quando um script diferente do script RandomParticipantChoose é selecionado no campo Seletor de Participante. O campo permite fornecer uma lista de um argumento separado por vírgulas para o script selecionado no campo Seletor de participante.

* **[!UICONTROL Usuário ou grupo]**: A tarefa é atribuída ao usuário ou grupo selecionado. A opção está disponível quando a variável **[!UICONTROL Para um usuário ou grupo específico]** é selecionado no **[!UICONTROL Atribuir opções]** campo. O campo lista todos os usuários e grupos da variável [!DNL workflow-users] grupo.\
   O **[!UICONTROL Usuário ou grupo]** O menu suspenso lista os usuários e grupos aos quais o usuário conectado tem acesso. A exibição do nome de usuário depende de se você tem permissões de acesso no **[!UICONTROL usuários]** no repositório crx para esse usuário específico.

* **[!UICONTROL Enviar email de notificação]**: Selecione essa opção para enviar notificações por email ao destinatário. Essas notificações são enviadas quando uma tarefa é atribuída a um usuário ou grupo. Você pode usar o **[!UICONTROL Endereço de email do destinatário]** para especificar o mecanismo para recuperar o endereço de email.

* **[!UICONTROL Endereço de email do destinatário]**: Você pode armazenar endereço de email em uma variável, usar um literal para especificar um endereço de email permanente ou usar o endereço de email padrão do destinatário especificado no perfil do destinatário. Você pode usar o literal ou uma variável para especificar o endereço de email de um grupo. A opção de variável é útil na recuperação dinâmica e no uso de um endereço de email. O **[!UICONTROL Usar endereço de email padrão do destinatário]** é somente para um único destinatário. Nesse caso, o endereço de email armazenado no perfil de usuário atribuído é usado.

* **[!UICONTROL Modelo de email do HTML]**: Selecione o modelo de email para o email de notificação. Para editar um modelo, modifique o arquivo localizado em /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt no crx-repository.
* **[!UICONTROL Permitir Delegação]**: AEM Caixa de entrada fornece uma opção para o usuário conectado delegar o fluxo de trabalho atribuído a outro usuário. Você pode delegar no mesmo grupo ou no usuário de workflow de outro grupo. Se a tarefa for atribuída a um único usuário e a variável **[!UICONTROL permitir delegação aos membros do grupo de destinatários]** estiver selecionada, então não é possível delegar a tarefa a outro usuário ou grupo.
* **[!UICONTROL Compartilhar configurações]**: AEM Caixa de entrada fornece opções para compartilhar uma única ou todas as tarefas na caixa de entrada com outros usuários:
   * Quando a variável **[!UICONTROL Permitir que o destinatário compartilhe explicitamente na caixa de entrada]** estiver selecionada, o usuário poderá selecionar a tarefa em AEM Caixa de entrada e compartilhá-la com outro usuário AEM.
   * Quando a variável **[!UICONTROL Permitir que o destinatário compartilhe via compartilhamento da caixa de entrada]** estiver selecionada e os usuários compartilharem seus itens da Caixa de entrada ou permitir que outros usuários acessem seus itens da Caixa de entrada, somente as tarefas com a opção mencionada anteriormente ativada serão compartilhadas com outros usuários.
   * Quando a variável **[!UICONTROL Permitir que o destinatário delegue usando configurações &#39;Fora do Escritório&#39;]** está selecionada. O destinatário pode habilitar a opção para delegar a tarefa a outros usuários, juntamente com outras opções fora do escritório. Quaisquer novas tarefas atribuídas ao usuário externo são delegadas automaticamente (atribuídas) aos usuários mencionados em configurações fora do escritório.

   Ele permite que outros usuários selecionem tarefas atribuídas enquanto estiver fora do escritório e não puderem trabalhar em tarefas atribuídas.

* **[!UICONTROL Ações]** > **[!UICONTROL Ações padrão]**: As ações Enviar, Salvar e Redefinir estão disponíveis e estão prontas para uso. Todas as ações padrão são habilitadas, por padrão.
* **[!UICONTROL Variável de rota]**: Nome da variável de rota. A variável de rota captura ações personalizadas que um usuário seleciona AEM Caixa de entrada.
* **[!UICONTROL Rotas]**: Uma tarefa pode ramificar para rotas diferentes. Quando selecionada em AEM Caixa de entrada, a rota retorna um valor e o workflow ramifica com base na rota selecionada. Você pode armazenar rotas em uma variável do tipo de dados String ou selecionar **[!UICONTROL Literal]** para adicionar rotas manualmente.

* **[!UICONTROL Título da Rota]**: Especifique o título da rota. Exibido em AEM Caixa de entrada.
* **[!UICONTROL Ícone Coral]**: Especifique o atributo HTML de um ícone de coral. Adobe A biblioteca CorelUI fornece um vasto conjunto de ícones de toque primeiro. Você pode escolher e usar um ícone para a rota. Ele é exibido junto com o título em AEM Caixa de entrada. Se você armazenar as rotas em uma variável, as rotas usarão um ícone de coral &quot;Tags&quot; padrão.
* **[!UICONTROL Permitir ao destinatário adicionar comentário]**: Selecione esta opção para habilitar comentários para a tarefa. Um destinatário pode adicionar os comentários de dentro AEM Caixa de entrada no momento do envio da tarefa.
* **[!UICONTROL Salvar comentário na variável]**: Salve o comentário em uma variável do tipo de dados String . Essa opção será exibida somente se você selecionar a variável **[!UICONTROL Permitir ao destinatário adicionar comentário]** caixa de seleção.

* **[!UICONTROL Permitir que o destinatário adicione anexos à tarefa]**: Selecione esta opção para ativar anexos para a tarefa. Um destinatário pode adicionar os anexos de dentro AEM Caixa de entrada no momento do envio da tarefa. Você também pode limitar o tamanho máximo **[!UICONTROL (Tamanho máximo do arquivo)]** de um anexo. O tamanho padrão é de 2 MB.

* **[!UICONTROL Salvar anexos de tarefa de saída usando]**: Especifique a localização da pasta de anexos. Você pode salvar anexos de tarefa de saída usando um caminho relativo à carga ou em uma variável de matriz de tipo de dados do documento. Essa opção será exibida somente se você selecionar a variável **[!UICONTROL Permitir que o destinatário adicione anexos à tarefa]** e selecione **[!UICONTROL Formulário adaptável]**, **[!UICONTROL Formulário adaptável somente leitura]** ou **[!UICONTROL Documento de PDF não interativo]** do **[!UICONTROL Tipo]** na lista suspensa na **[!UICONTROL Formulário/Documento]** guia .

* **[!UICONTROL Usar metadados personalizados]**: Selecione essa opção para ativar o campo de metadados personalizado. Os metadados personalizados são usados em modelos de email.
* **[!UICONTROL Metadados personalizados]**: Selecione metadados personalizados para os modelos de email. Os metadados personalizados estão disponíveis no repositório crx em apps/fd/dashboard/scripts/metadataScripts. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. Você também pode usar um serviço para os metadados personalizados. Você também pode estender o `WorkitemUserMetadataService` para fornecer metadados personalizados.
* **[!UICONTROL Mostrar dados das etapas anteriores]**: Selecione essa opção para permitir que os destinatários exibam os destinatários anteriores, a ação já realizada na tarefa, os comentários adicionados à tarefa e o Documento de registro da tarefa concluída, se disponível.
* **[!UICONTROL Mostrar dados de etapas subsequentes]**: Selecione essa opção para permitir que o destinatário atual visualize a ação executada e os comentários adicionados à tarefa pelos destinatários subsequentes. Também permite que o destinatário atual exiba um Documento de registro da tarefa concluída, se disponível.
* **[!UICONTROL Visibilidade do tipo de dados]**: Por padrão, um destinatário pode visualizar um Documento de registro, destinatários, ação tomada e comentários que destinatários anteriores e subsequentes adicionaram. Use a opção visibility of data type para limitar o tipo de dados visível para os destinatários.

>[!NOTE]
>
>As opções para salvar a etapa Atribuir tarefa como rascunho e recuperar o histórico da etapa Atribuir tarefa são desativadas ao configurar um modelo de fluxo de trabalho AEM para armazenamento de dados externo. Além disso, na Caixa de entrada, a opção para salvar está desativada.

## Converter em etapa PDF/A {#convert-pdfa}

PDF/A é um formato de arquivo para a preservação de longo prazo do conteúdo do documento, ao incorporar as fontes e descompactar o arquivo. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Você pode usar o ***Converter em PDF/A*** em um Fluxo de trabalho AEM para converter os documentos do PDF para o formato PDF/A.

A etapa converter em PDF/A tem as seguintes propriedades:

**[!UICONTROL Documento de entrada]**: O documento de entrada pode ser relativo à carga, ter um caminho absoluto, pode ser fornecido como carga ou armazenado em uma variável do tipo de dados Documento.

**[!UICONTROL Opções de conversão]**: Usando essa propriedade, as configurações para converter documentos PDF para documentos PDF/A são especificadas. Várias opções disponíveis nesta guia são:
* **[!UICONTROL Conformidade]**: Especifica os padrões que o documento PDF/A de saída deve atender.
* **[!UICONTROL Nível de Resultado]**: Especifica o nível do resultado como PassFail, Summary ou Detailed, para a saída da conversão.
* **[!UICONTROL Espaço da cor]**: Especifica o espaço de cores predefinido que é usado para arquivos PDF/A de saída.
* **[!UICONTROL Conteúdo opcional]**: Permite que objetos gráficos e/ou anotações específicos sejam visíveis no documento PDF/A de saída, somente quando um conjunto especificado de critérios é atendido.

**[!UICONTROL Documentos de saída]**: Especifica o local para salvar o arquivo de saída. O arquivo de saída pode ser salvo em um local relativo à carga, substitui a carga, se a carga for um arquivo ou em uma variável do tipo de dados Documento.


## Etapa Enviar Email {#send-email-step}

Use a etapa de email para enviar um email, por exemplo, um email com um Documento de registro, um link de um formulário adaptável <!-- , link of an interactive communication-->ou com um documento PDF anexado. Enviar suporte à etapa de email [HTML email](https://en.wikipedia.org/wiki/HTML_email). Os emails do HTML são responsivos e adaptam-se ao cliente de email e ao tamanho da tela dos recipients. Você pode usar um modelo de email do HTML para definir a aparência, o esquema de cores e o comportamento do email.

A etapa de email usa o Day CQ Mail Service para enviar emails. Antes de usar a etapa de email, verifique se o serviço de email está configurado. Por padrão, o suporte a email é compatível somente com protocolos HTTP e HTTPs. [Entre em contato com a equipe de suporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email) para habilitar as portas para enviar emails e habilitar o protocolo SMTP para seu ambiente. A restrição ajuda a melhorar a segurança da plataforma.

A etapa de email tem as seguintes propriedades:

**[!UICONTROL Título]**: O título da etapa ajuda a identificar a etapa no editor de fluxo de trabalho.

**[!UICONTROL Descrição]**: Explicação é útil para outros desenvolvedores de processos quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

**[!UICONTROL Assunto do email]**: O assunto pode ser recuperado de metadados de workflow, especificados manualmente ou recuperados do valor armazenado em uma variável. Selecione dentre as seguintes opções:

* **[!UICONTROL Literal]** Especificar um assunto manualmente.
* **[!UICONTROL Recuperar dos metadados do fluxo de trabalho]** - Recupere o assunto de uma propriedade de metadados.
* **[!UICONTROL Variável]** - Recupere o assunto do valor armazenado em uma variável do tipo de dados da string.

**[!UICONTROL Modelo de email do HTML]**: modelo HTML para o email. Você pode especificar variáveis em um modelo de email. A Etapa de email extrai e exibe todas as variáveis incluídas em um modelo para entradas.

**[!UICONTROL Metadados de modelo de email]**: O valor das variáveis do modelo de email pode ser um valor especificado pelo usuário, o caminho de um ativo no autor ou no servidor de publicação, a imagem ou uma propriedade de metadados de workflow.

* **[!UICONTROL Literal]**: Use a opção quando souber o valor exato a ser especificado. Por exemplo, [example@example.com](mailto:example@example.com).

* **[!UICONTROL Metadados de fluxo de trabalho]**: Use a opção quando o valor a ser usado for salvo em uma propriedade de metadados de workflow. Depois de selecionar a opção , insira o nome da propriedade de metadados na caixa de texto vazia abaixo da opção Metadados do fluxo de trabalho . Por exemplo, emailAddress.

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL Imagem]**: Use a opção para incorporar uma imagem ao email. Depois de selecionar a opção , navegue e escolha a imagem. A opção de imagem está disponível somente para as tags de imagem (&lt;img src=&quot;&lt;span id=&quot; translate=&quot;no&quot; />&quot;/>) disponíveis no modelo de email.&#42;

**[!UICONTROL Endereço de email do remetente/destinatário]**: Selecione o **[!UICONTROL Literal]** para especificar manualmente um endereço de email ou selecionar a opção **[!UICONTROL Recuperar dos metadados do fluxo de trabalho]** para recuperar o endereço de email de uma propriedade de metadados. Também é possível especificar uma lista de matrizes de propriedades de metadados para a variável **[!UICONTROL Recuperar dos metadados do fluxo de trabalho]** opção. Selecione o **[!UICONTROL Variável]** para recuperar o endereço de email do valor armazenado em uma variável do tipo de dados da string.

* **[!UICONTROL Anexo de arquivo]**: O ativo disponível no local especificado é anexado ao email. O caminho do ativo pode ser relativo à carga ou ao caminho absoluto. Um caminho de exemplo é [Diretório_de_carga]/anexos/.

Selecione o **[!UICONTROL Variável]** para recuperar o anexo de arquivo armazenado em uma variável do tipo de dados Document, XML ou JSON.

**[!UICONTROL Nome do arquivo]**: Nome do arquivo de anexo de email. A Etapa de email altera o nome de arquivo original do anexo para o nome de arquivo especificado. O nome pode ser especificado manualmente ou recuperado de uma propriedade de metadados de workflow ou de uma variável. Use o **[!UICONTROL Literal]** quando você souber o valor exato a ser especificado. Use o **[!UICONTROL Variável]** para recuperar o nome do arquivo do valor armazenado em uma variável do tipo de dados da string. Use o **[!UICONTROL Recuperar de metadados de fluxo de trabalho]** quando o valor a ser usado for salvo em uma propriedade de metadados de workflow.

## Etapa Gerar Documento de Registro {#generate-document-of-record-step}

Quando um formulário é preenchido ou enviado, é possível manter um registro do formulário, em formato impresso ou documento. Este registro é conhecido como Documento de Registro (DoR). Você pode usar a etapa Gerar documento de registro para criar uma versão de PDF somente leitura ou interativa de um formulário adaptável. A versão PDF contém informações preenchidas para o formulário, juntamente com o layout do formulário adaptável.

A etapa Documento de registro tem as seguintes propriedades:

**[!UICONTROL Usar formulário adaptável]**: Especifique o método para localizar o Formulário adaptável de entrada. É possível usar o formulário adaptável enviado para o fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo de dados String para especificar o caminho no **[!UICONTROL Selecione a variável a ser resolvida]** campo.\
Você pode associar vários adaptadores Forms a um fluxo de trabalho. Como resultado, você pode especificar um formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

**[!UICONTROL Caminho do formulário adaptável]**: Especifique o caminho do formulário adaptável. O campo fica disponível ao selecionar a variável **[!UICONTROL Disponível em um caminho absoluto]** da **[!UICONTROL Usar formulário adaptável]** campo.

**[!UICONTROL Selecione Input data usando]**: Caminho dos dados de entrada para o Formulário adaptável. Você pode manter os dados em um local relativo à carga, especificar um caminho absoluto dos dados ou recuperar dados armazenados em uma variável do tipo de dados Document, JSON ou XML. Os dados de entrada são unidos ao Formulário adaptável para criar um Documento de registro.

**[!UICONTROL Selecione o caminho do anexo de Entrada usando]**: Caminho dos anexos. Esses anexos estão incluídos no Documento de registro. Você pode manter os anexos em um local relativo à carga, especificar um caminho absoluto dos anexos ou recuperar anexos armazenados em uma variável do tipo de dados Documento.

Se você especificar o caminho de uma pasta, por exemplo, anexos, todos os arquivos diretamente disponíveis na pasta serão anexados ao Documento de registro. Se algum arquivo estiver disponível nas pastas diretamente disponíveis no caminho de anexo especificado, os arquivos serão incluídos no Documento de registro como anexos. Se houver pastas em pastas diretamente disponíveis, essas pastas serão ignoradas.

**[!UICONTROL Salvar Documento Gerado de Registro usando as opções abaixo]**: Especifique o local para manter um arquivo Documento de registro. Você pode optar por substituir a pasta de carga útil, colocar Documento de registro em um local dentro do diretório de carga ou armazenar o Documento de registro em uma variável do tipo de dados Documento.

**[!UICONTROL Localidade]**: Especifique o idioma do Documento de registro. Selecionar **[!UICONTROL Literal]** para selecionar a localidade em uma lista suspensa ou selecione **[!UICONTROL Variável]** para recuperar a localidade do valor armazenado em uma variável do tipo de dados da string. Você deve definir o código local enquanto armazena o valor da localidade em uma variável. Por exemplo, especifique **en_US** em inglês e **fr_FR** para francês.

## Invocar etapa DDX {#invokeddx}

Document Description XML (DDX) é uma linguagem de marcação declarativa cujos elementos representam blocos de construção de documentos. Esses blocos fundamentais incluem documentos PDF e XDP e outros elementos, como comentários, marcadores e texto estilizado. O DDX define um conjunto de operações, que pode ser aplicado em um ou mais documentos de entrada para gerar um ou mais documentos de saída.  Um único DDX pode ser usado com um intervalo de documentos de origem. Você pode usar o ***Invocar etapa DDX*** em um Fluxo de trabalho AEM para executar várias operações, como Assemblagem de documentos de desmontagem, Criação e modificação do Acrobat e XFA Forms, e outras descritas em [Documentação de referência DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

A etapa Chamar DDX tem as seguintes propriedades:

**[!UICONTROL Documentos de entrada]**: Usado para definir as propriedades de um documento de entrada. Várias opções disponíveis nesta guia são:
* **[!UICONTROL Especificar DDX usando]**: Especifica os documentos de entrada relativos à carga, têm um caminho absoluto, podem ser fornecidos como carga ou armazenados em uma variável do tipo de dados Documento.
* **[!UICONTROL Criar mapa a partir da carga]**: Adiciona todos os documentos sob a pasta carga ao Mapa do Documento de Entrada para a API de chamada no Assembler. O nome do nó de cada documento é usado como uma chave no mapa.
* **[!UICONTROL Mapa do Documento de Entrada]**: A opção é usada para adicionar várias entradas usando **[!UICONTROL ADICIONAR]** botão. Cada entrada representa a chave do documento no mapa e a origem do documento.

**[!UICONTROL Opções de ambiente]**: Essa opção é usada para definir configurações de processamento para invocar a API. Várias opções disponíveis nesta guia são:
* **[!UICONTROL Validar somente]**: Verifica a validade do documento DDX de entrada.
* **[!UICONTROL Falha no Erro]**: Verifica se o serviço invocar API falha, em caso de erro. Por padrão, seu valor é definido como False.
* **[!UICONTROL Primeiro Número de Bates]**: Especifica o número, que é o autoincremento. Esse número de autoincremento é exibido em cada página consecutiva automaticamente.
* **[!UICONTROL Estilo padrão]**: Define o estilo padrão do arquivo de saída.

>[!NOTE]
>
>As opções de ambiente são mantidas sincronizadas com as APIs HTTP.

**[!UICONTROL Documentos de saída]**: Especifica o local para salvar o arquivo de saída. Várias opções disponíveis nesta guia são:
* **[!UICONTROL Salvar saída na carga]**: Salva documentos de saída na pasta payload ou substitui a carga, caso a carga seja um arquivo.
* **[!UICONTROL Mapa do Documento de Saída]**: Especifica o local para salvar explicitamente cada arquivo de documento, adicionando uma entrada por documento. Cada entrada representa o documento e o local, onde salvá-lo. Se houver vários documentos de saída, essa opção será usada.

## Invoque a etapa Serviço do Modelo de Dados de Formulário {#invoke-form-data-model-service-step}

Você pode usar [[!DNL AEM Forms] Integração de dados](data-integration.md) para configurar e conectar-se a fontes de dados diferentes. Essas fontes de dados podem ser um serviço da Web, serviço REST, serviço OData e solução CRM. [!DNL AEM Forms] A Integração de dados permite criar um Modelo de dados de formulário que abrange vários serviços para executar operações de recuperação de dados, além de atualizar no banco de dados configurado. Você pode usar o **[!UICONTROL Invoque a etapa Serviço do Modelo de Dados]** para selecionar um FDM (Form Data Model) e usar os serviços do FDM para recuperar, atualizar ou adicionar dados a fontes de dados diferentes.

Para explicar entradas para campos da etapa, a tabela de banco de dados a seguir e o arquivo JSON são usados como exemplo :

**[!UICONTROL Tabela de detalhes do cliente de exemplo]**

<table>
 <tbody> 
  <tr> 
   <td>Propriedade</td> 
   <td>Valor<br /> </td> 
  </tr> 
  <tr> 
   <td>Nome<br /> </td> 
   <td>Sarah<br /> </td> 
  </tr> 
  <tr> 
   <td>Sobrenome</td> 
   <td>Rosa</td> 
  </tr> 
  <tr> 
   <td>Customer ID</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>Endereço de email<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**[!UICONTROL Arquivo JSON de exemplo]**

```json
  { 
    customer: { 
     firstName: "Sarah", 
     lastName:"Rose", 
     customerId: "1", 
     emailAddress:"srose@we.info" 
   }, 
    insurance: {
     customerId: "1", 
    policyType: "Premium,
    policyNumber: "Premium-521499",
    customerDetails: { 
     firstName: "Sarah",
     lastName: "Rose",
     customerId: "1",
     emailAddress: "srose@we.info" 
    }
   }
  }
```

A etapa Invocar serviço de modelo de dados de formulário tem os campos listados abaixo para facilitar as operações do Modelo de dados de formulário:

* **[!UICONTROL Título]**: Título da etapa. Ajuda a identificar a etapa no editor de fluxo de trabalho.
* **[!UICONTROL Descrição]**: Explicação útil para outros desenvolvedores de processos quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

* **[!UICONTROL Caminho do modelo de dados de formulário]**: Procure e selecione um Modelo de dados de formulário presente no servidor.

* **[!UICONTROL Erros e validações]**: A opção permite capturar mensagens de erro e especificar opções de validação para dados recuperados e enviados para fontes de dados. Com essas alterações, você pode garantir que os dados transmitidos para a etapa Invoke Form Data Model Service adiram às restrições de dados definidas pela fonte de dados. Para obter mais detalhes, consulte [Validação automatizada de dados de entrada](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL Nível de validação]**: Há três categorias de validações: Básico, completo e desativado:

   * Total: Todas as restrições são validadas.
   * Básico: Somente restrições necessárias e anuláveis
   * DESATIVADO: Nenhuma validação ocorre.

* **[!UICONTROL Encerrar Fluxo de Trabalho em Falha]**: Quando uma restrição falha na validação, o workflow é interrompido.

* **[!UICONTROL Armazenar código de erro na variável]**: Você pode armazenar um código de erro em um [Variável de tipo de string](variable-in-aem-workflows.md).

* **[!UICONTROL Mensagem de erro de armazenamento na variável]**: Você pode armazenar uma mensagem de erro em um [Variável de tipo de string](variable-in-aem-workflows.md).

* **[!UICONTROL Detalhes do erro de armazenamento na variável]**: Você pode armazenar um detalhe de erro em uma [Variável de tipo JSON](variable-in-aem-workflows.md).

* **[!UICONTROL Serviço]**: Lista dos serviços fornecidos pelo Modelo de dados de formulário selecionado.
* **[!UICONTROL Entrada de serviços]** > **[!UICONTROL Forneça dados de entrada usando metadados literais, variáveis ou de fluxo de trabalho e um arquivo JSON]**: Um serviço pode ter vários argumentos. Selecione a opção para obter o valor dos argumentos de serviço de uma propriedade de metadados de workflow, um objeto JSON, uma variável ou insira diretamente o valor na caixa de texto fornecida:

   * **[!UICONTROL Literal]**: Use a opção quando souber o valor exato a ser especificado. Por exemplo, srose@we.info.
   * **[!UICONTROL Variável]**: Use a opção para recuperar o valor armazenado em uma variável.
   * **[!UICONTROL Recuperar dos metadados do fluxo de trabalho]**: Use a opção quando o valor a ser usado for salvo em uma propriedade de metadados de workflow. Por exemplo, emailAddress.

   * **[!UICONTROL Em relação à carga]**: Use a opção para recuperar o anexo de arquivo salvo em um caminho relativo à carga útil. Selecione a opção e especifique o nome da pasta que inclui o anexo do arquivo ou especifique o nome do anexo do arquivo na caixa de texto.

      Por exemplo, se a pasta Relative to Payload no repositório CRX incluir um anexo de arquivo no `attachment\attachment-folder` local, especifique `attachment\attachment-folder` na caixa de texto depois de selecionar a variável **[!UICONTROL Em relação à carga]** opção.

   * **[!UICONTROL Notação de ponto JSON]**: Use a opção quando o valor a ser usado estiver em um arquivo JSON. Por exemplo, Insurance.customerDetails.emailAddress. A opção Notação de pontos JSON só estará disponível se a opção Mapear campos de entrada do JSON de entrada estiver selecionada.
   * **[!UICONTROL Mapear campos de entrada do JSON de entrada]**: Especifique o caminho de um arquivo JSON para obter o valor de entrada de alguns argumentos de serviço do arquivo JSON. O caminho do arquivo JSON pode ser relativo à carga, um caminho absoluto ou você pode selecionar um documento JSON de entrada usando uma variável do tipo JSON ou Form Data Model.

* **[!UICONTROL Entrada de serviços]** > **[!UICONTROL Fornecer dados de entrada usando uma variável ou um arquivo JSON]**: Selecione a opção para obter valores para todos os argumentos de um arquivo JSON salvo em um caminho absoluto, em um caminho relativo à carga ou em uma variável.
* **[!UICONTROL Selecione o documento JSON de entrada usando]**: O arquivo JSON que contém valores para todos os argumentos de serviço. O caminho do arquivo JSON pode ser **[!UICONTROL relativo à carga]** ou **[!UICONTROL caminho absoluto]**. Também é possível recuperar o documento JSON de entrada usando uma variável do tipo de dados JSON ou Form Data Model.

* **[!UICONTROL Notação de ponto JSON]**: Deixe o campo em branco para usar todos os objetos do arquivo JSON especificado como entrada para argumentos de serviço. Para ler um objeto JSON específico do arquivo JSON especificado como entrada para argumentos de serviço, especifique a notação de pontos para o objeto JSON, por exemplo, Se você tiver um JSON semelhante ao listado no início da seção, especifique Insurance.customerDetails para fornecer todos os detalhes de um cliente como entrada para o serviço.
* **[!UICONTROL Saída de serviço]** > **[!UICONTROL Mapear e gravar valores de saída em variáveis ou metadados]**: Selecione a opção para salvar os valores de saída como propriedades do nó de metadados da instância de fluxo de trabalho no crx-repository. Especifique o nome da propriedade de metadados e selecione o atributo de saída de serviço correspondente a ser mapeado com a propriedade de metadados; por exemplo, mapeie o phone_number retornado pelo serviço de saída com a propriedade phone_number dos metadados do fluxo de trabalho. Da mesma forma, é possível armazenar a saída em uma variável do tipo de dados Long . Ao selecionar uma propriedade para a variável **[!UICONTROL Atributo de saída de serviço a ser mapeado]** , somente as variáveis capazes de armazenar dados da propriedade selecionada são preenchidas para a variável **[!UICONTROL Salve a saída em]** opção.

* **[!UICONTROL Saída de serviço]** > **[!UICONTROL Salvar saída em variável ou um arquivo JSON]**: Selecione a opção para salvar os valores de saída em um arquivo JSON em um caminho absoluto, em um caminho relativo à carga ou em uma variável .
* **[!UICONTROL Salvar documento JSON de saída usando as opções abaixo]**: Salve o arquivo JSON de saída. O caminho do arquivo JSON de saída pode ser relativo à carga ou a um caminho absoluto. Também é possível salvar o arquivo JSON de saída usando uma variável do tipo de dados JSON ou Form Data Model.

## Etapa Assinar documento {#sign-document-step}

A etapa Assinar documento permite usar [!DNL Adobe Sign] para assinar documentos. Ao utilizar [!DNL Adobe Sign] Etapa do fluxo de trabalho para Assinar um formulário adaptável, o formulário pode ser passado entre signatários um após o outro ou pode ser enviado a todos os signatários simultaneamente, dependendo da etapa de configuração do fluxo de trabalho. [!DNL Adobe Sign] ativado O Adaptive Forms é enviado para o Experience Manager Forms Server somente depois que todos os signatários concluírem o processo de assinatura.

Por padrão, a variável [!DNL Adobe Sign] As verificações de serviços do agendador (pesquisas) respondem ao assinante após cada 24 horas. Você pode [alterar o intervalo padrão do seu ambiente](adobe-sign-integration-adaptive-forms.md##configure-adobe-sign-scheduler-to-sync-the-signing-status).

A etapa Assinar documento tem as seguintes propriedades:

* **[!UICONTROL Nome do Contrato]**: Especifique o título do contrato. O nome do contrato se torna parte do assunto e do texto do corpo do email enviado aos signatários. Você pode armazenar o nome em uma variável do tipo de dados String ou selecionar **[!UICONTROL Literal]** para adicionar o nome manualmente.

* **[!UICONTROL Localidade]**: Especifique o idioma para as opções de email e verificação. Você pode armazenar a localidade em uma variável do tipo de dados String ou selecionar **[!UICONTROL Literal]** para escolher a localidade na lista de opções disponíveis. Você deve definir o código local enquanto armazena o valor da localidade em uma variável. Por exemplo, especifique **[!UICONTROL en_US]** em inglês e **[!UICONTROL fr_FR]** para francês.

* **[!UICONTROL Configuração da Adobe Sign Cloud]**: Escolha um [!DNL Adobe Sign] Configuração na nuvem. Se você não tiver configurado [!DNL Adobe Sign] para [!DNL AEM Forms], consulte [Integrar o Adobe Sign com o [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL Selecionar Documento a ser assinado usando]**: Você pode escolher um documento de um local relativo à carga, usar carga como documento, especificar um caminho absoluto do documento ou recuperar o documento armazenado em uma variável do tipo de dados Documento.
* **[!UICONTROL Dias até o final do prazo]**: Um documento é marcado como vencido (prazo vencido) depois que não há atividade na tarefa para o número de dias especificado na **[!UICONTROL Dias até o final do prazo]** campo. O número de dias é contado depois que o documento é atribuído a um usuário para assinatura.
* **[!UICONTROL Frequência de email do lembrete]**: Você pode enviar um email de lembrete diariamente ou semanalmente. A semana é contada a partir do dia em que o documento foi atribuído a um usuário para assinatura.
* **[!UICONTROL Processo de assinatura]**: Você pode optar por assinar um documento em uma ordem sequencial ou paralela. Em ordem sequencial, um assinante recebe o documento por vez para assinatura. Depois que o primeiro assinante concluir a assinatura do documento, o documento será enviado para o segundo assinante e assim por diante. Em ordem paralela, vários signatários podem assinar um documento de cada vez.
* **[!UICONTROL Redirecionar URL]**: Especifique um URL de redirecionamento. Depois que o documento for assinado, você poderá redirecionar o destinatário para um URL. Normalmente, este URL contém uma mensagem de agradecimento ou mais instruções.
* **[!UICONTROL Estágio do fluxo de trabalho]**: Um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada de AEM. É possível definir esses estágios nas propriedades do modelo ( **[!UICONTROL Sidekick]** > **[!UICONTROL Página]** > **[!UICONTROL Propriedades da página]** > **[!UICONTROL Estágios]**).
* **[!UICONTROL Selecionar Assinantes]**: Especifique o método para escolher os signatários do documento. Você pode atribuir dinamicamente o fluxo de trabalho a um usuário ou grupo ou adicionar manualmente detalhes de um assinante.
* **[!UICONTROL Script ou serviço para selecionar signatários]**: A opção estará disponível somente se a opção Dinamicamente estiver selecionada no campo Selecionar signatários . Você pode especificar um ECMAScript ou um serviço para escolher assinantes e opções de verificação para um documento.
* **[!UICONTROL Detalhes do assinante]**: A opção só estará disponível se a opção Manualmente estiver selecionada no campo Selecionar signatários . Especifique o endereço de email e escolha um mecanismo de verificação opcional. Antes de selecionar um mecanismo de verificação em duas etapas, verifique se a opção de verificação correspondente está ativada para o [!DNL Adobe Sign] conta. Você pode usar uma variável do tipo de dados String para definir valores para campos Email, Código do país e Número de telefone. Os campos Código do país e Número de telefone são exibidos somente se você selecionar Verificação de telefone na lista suspensa de verificação de duas etapas.

<!-- 

## Document Services steps {#document-services-steps}

AEM Document services are a set of services for creating, assembling, and securing PDF Documents. [!DNL AEM Forms] provides a separate AEM Workflow step for each document service.

Similar to other [!DNL AEM Forms] workflow steps, such as Assign Task, Send Email, and Sign Document, you can use variables in all AEM Document services steps. For more information on creating and managing variables, see [Variables in AEM workflows](variable-in-aem-workflows.md).

### Apply Document Time Stamp step {#apply-document-time-stamp-step}

Add time stamp to a document. You provide document details such as input document path, input document name, location to store exported data. You may choose to overwrite existing payload file, choose a different file name to store data in a different file under payload folder, provide an absolute path to the data, or store data in a variable of Document data type.

### Convert to image step {#convert-to-image-step}

Converts a PDF document to list of images. Supported image formats are JPEG, JPEG2000, PNG, and TIFF. The following information applies to conversions to TIFF images:

* A multi-page TIFF file is generated.
* Some annotations are not included in TIFF images. Annotations that require Acrobat to generate their appearance are not included.

### Convert to PDF/A step {#convert-to-pdf-a-step}

Converts a PDF document to PDF/A format using the options provided. The PDF/A version of Portable Document Format (PDF) is specialized for archiving and long-term preservation of documents.

### Convert to PS step {#convert-to-ps-step}

Convert PDF documents to PostScript. When converting to PostScript, you can use the conversion operation to specify the source document and whether to convert to PostScript level 2 or 3. The PDF document you convert to a PostScript file must be non-interactive.

### Create PDF from specified type step {#create-pdf-from-specified-type-step}

Generate a PDF document from an input file. The input document can be relative to the payload, have an absolute path, can be payload itself, or stored in a variable of Document data type.

### Create PDF from URL/HTML/ZIP step {#create-pdf-from-url-html-zip-step}

Generates a PDF document from supplied URL, HTML, and ZIP file.

### Export Data step {#export-data-step}

Exports data from a PDF forms or XDP file. It requires you to enter the file path of Input Document and the Export Data Format. The options for Export Data Format are Auto, XDP and XmlData.

### Export PDF to specified type step {#export-pdf-to-specified-type-step}

Converts a PDF document to a selected format.

### Generate Non-Interactive PDF step {#generatenoninteractive}

Generate a Non-Interactive PDF. It provides various customization options.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Import Data step {#import-data-step}

Merges form data into a PDF form. You can import form data into a PDF form.

### Invoke DDX step {#invokeddx}

Executes the DDX file on the specified map of input documents and returns the manipulated PDF documents.

>[!NOTE]
>
>You can use variables to specify the DDX file for input documents. Store the DDX file in a variable of Document or XML data type.

### Optimize PDF step {#optimize-pdf-step}

Optimizes PDF files by reducing their size. The result of this conversion is PDF files that may be smaller than their original versions. This operation also converts PDF documents to the PDF version specified in the optimization parameters.

Optimization settings specify how files are optimized. Here are example settings:

* Target PDF version
* Discarding objects such as JavaScript actions and embedded page thumbnails
* Discarding user data such as comments and file attachments
* Discarding invalid or unused settings
* Compressing uncompressed data or using more efficient compression algorithms
* Removing embedded fonts
* Setting transparency values

### Render PDF Form step {#renderpdf}

Renders a form created in Form Designer (XDP) to a PDF form.

>[!NOTE]
>
>You can use variables to specify the template file for input documents. Store the path of the template file in a variable of String data type.

### Secure Document step {#secure-document-step}

Encrypt, Sign, and certify a document. [!DNL AEM Forms] supports both password based and certificate base encryption. You can also choose between various algorithms for signing documents. For example, SHA-256 and SH-512. You can also use the workflow step to reader extend PDF documents. The workflow step provides option to enable barcode decoding, digital signatures, import and export of PDF data, and other options.

### Send to Printer step {#send-to-printer-step}

Send a document directly to a printer. It supports the following printing access mechanisms:

* **[!UICONTROL Direct accessible printer]**: A printer that is installed on the same computer is called a direct accessible printer, and the computer is named printer host. This type of printer can be a local printer that is connected to the computer directly.
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX® printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server’s IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.

### Generate Printed Output Step {#generatePrintedOutput}

The step generates a PCL, PostScript, ZPL, IPL, TPCL, or DPL output given a form design and data file. The data file is merged with the form design and formatted for printing. The output generated by this step can be sent directly to a printer or saved as file. It is recommended that you use this step when you want to use form designs or data from an application. If your form designs or form designs are located on the network, local file system, or HTTP location, use the generatePrintedOutput operation operation.

For example, your application requires that you merge a form design with a data file. The data contains hundreds of records. In addition, it requires the output is sent to a printer that supports ZPL. The form design and your input data are located in an application. Use the generatePrintedOutput operation to merge each record with a form design and send the output to a printer that supports ZPL.

The Generate Printed Output step has the following properties:

**[!UICONTROL Input properties]**

* **[!UICONTROL Select template file using]**: Specify the path of the template file. You can select the template file using the path that is relative to the payload, saved at an absolute path, or using a variable of Document data type. For example, [Payload_Directory]/Workflow/data.xml. If the path does not exist in crx-repository, an administrator can create the path before using it. Moreover, you can also accept payload as the input data file.

* **[!UICONTROL Select data document using]**: Specify the path of a input data file. You can select the input data file using the path that is relative to the payload, saved at an absolute path, or using a variable of Document data type. For example, [Payload_Directory]/Workflow/data.xml. If the path does not exist in crx-repository, an administrator can create the path before using it.

* **[!UICONTROL Printer Format]**: A Print Format value that specifies the page description language to use, when an XDC file is not provided, to generate the output stream. If you provide a literal value, select one of these values:

  * **[!UICONTROL Custom PCL]**: Use the option to specify a custom XDC file for PCL.
  * **[!UICONTROL Custom PostScript]**: Use the option to specify a custom XDC file for PostScript.
  * **[!UICONTROL Custom ZPL]**: Use the option to specify a custom XDC file file for ZPL.
  * **[!UICONTROL Generic Color PCL (5c)]**: Use a generic color PCL (5c).
  * **[!UICONTROL Generic PostScript Level3]**: Use generic PostScript Level 3.
  * **[!UICONTROL ZPL 300 DPI]**: Use ZPL 300 DPI. The zpl300.xdc is used.
  * **[!UICONTROL ZPL 600 DPI]**: Use ZPL 600 DPI. The zpl600.xdc file is used.
  * **[!UICONTROL Custom IPL]**: Use the option to specify a custom XDC file for IPL.
  * **[!UICONTROL IPL 300 DPI]**: Use IPL 300 DPI. The ipl300.xdc is used.
  * **[!UICONTROL IPL 400 DPI]**: Use IPL 400 DPI. The ipl400.xdc file is used.
  * **[!UICONTROL Custom TPCL]**: Use the option to specify a custom XDC file for TPCL.
  * **[!UICONTROL TPCL 305 DPI]**: Use TPCL 300 DPI. The tpcl305.xdc file is used.
  * **[!UICONTROL PCL 600 DPI]**: Use TPCL 600 DPI. The tpcl600.xdc file is used.
  * **[!UICONTROL Custom DPL]**: Use the option to specify a custom XDC file DPL.
  * **[!UICONTROL DPL300DPI]**: Use DPL 300 DPI. The dpl300.xdc file is used.
  * **[!UICONTROL DPL406DPI]**: Use DPL 400 DPI. The dpl406.xdc is used.
  * **[!UICONTROL DPL600DPI]**: Use DPL 600 DPI. The dpl600.xdc is used.

**[!UICONTROL Output Properties]**

* **[!UICONTROL Save output document using]**: Specify the location to save the output file. You can save the output file at an location  which is relative to the payload, in a variable, or specify an absolute location to save the output file. If the path does not exist in crx-repository, an administrator can create the path before using it.

**[!UICONTROL Advanced Properties]**

* **[!UICONTROL Select Content Root location using]**: Content root is a string value that specifies the URI, absolute reference, or location in the repository to retrieve relative assets used by the form design. For example, if the form design references an image relatively, such as ../myImage.gif, myImage.gif must be located at repository://. The default value is repository://, which points to the root level of the repository.

  When you pick an asset from your application, the Content Root URI path must have the correct structure. For example, if a form is picked from an application named SampleApp, and is placed at SampleApp/1.0/forms/Test.xdp, the Content Root URI must be specified as repository://administrator@password/Applications/SampleApp/1.0/forms/, or repository:/Applications/SampleApp/1.0/forms/ (when authority is null). When the Content Root URI is specified this way, the paths of all of the referenced assets in the form will be resolved against this URI.

* **[!UICONTROL Select XCI file using]**: XCI files are used to describe fonts and other properties that are used for form design elements. You can keep an XCI file relative to the payload, at an absolute path, or using a variable of Document data type.

* **[!UICONTROL Locale]**: Specifies the language used for generating the PDF document. If you provide a literal value, select a language from the list or select one of these values:
  * **[!UICONTROL To use server default]**:
    (Default) Use the Locale setting configured on the [!DNL AEM Forms] Server. The Locale setting is configured using Administration Console. (See [Designer Help](http://www.adobe.com/go/learn_aemforms_designer_65).)

  * **[!UICONTROL To use custom value]**:
    Type the Locale code in the literal box or select a string variable containing the locale code. For a complete list of supported locale codes, see http://java.sun.com/j2se/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Copies]**: An integer value that specifies the number of copies to generate for the output. The default value is 1.

* **[!UICONTROL Duplex Printing]**:  A Pagination value that specifies whether to use two-sided or single-sided printing. Printers that support PostScript and PCL use this value.If you provide a literal value, select one of these values:
    * **[!UICONTROL Duplex Long Edge]**: Use two-sided printing and print using long-edge pagination. 
    * **[!UICONTROL Duplex Short Edge]**: Use two-sided printing and print using short-edge pagination. 
    * **[!UICONTROL Simplex]**: Use single-sided printing.
    
    -->
