---
title: Quais etapas de fluxo de trabalho estão disponíveis para o AEM Forms Cloud Service criar um fluxo de trabalho ou para a automação de processos de negócios (BPM)?
description: Fluxos de trabalho centrados no Forms permitem criar rapidamente fluxos de trabalho adaptáveis baseados no Forms. Você pode usar o Adobe Sign para assinar documentos eletronicamente, criar processos de negócios baseados em formulários, recuperar e enviar dados para várias fontes de dados e enviar notificações por email
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
keywords: Usar fluxos de trabalho de AEM, usando etapas atribuir tarefa, converter em PDF/A etapa, Gerar documento da etapa gravada, usar fluxos de trabalho, etapa Assinar documento, etapa Gerar saída impressa, Gerar saída de PDF não interativa
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '7444'
ht-degree: 1%

---


# Usar workflows AEM centrados na Forms - referência de etapa para automatizar processos de negócios {#forms-centric-workflow-on-osgi-step-reference}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html) |
| AEM as a Cloud Service | Este artigo |

Você usa modelos de fluxo de trabalho. Um modelo ajuda a definir e executar uma série de etapas. Você também pode definir propriedades do modelo, como se o fluxo de trabalho é transitório ou usa vários recursos. Você pode [incluir várias etapas do fluxo de trabalho do AEM em um modelo para atingir a lógica de negócios](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem).

## Etapas centradas no Forms {#forms-workflow-steps}

As etapas de fluxo de trabalho centradas no Forms executam operações específicas do AEM Forms em um fluxo de trabalho do AEM. Forms Essas etapas permitem criar rapidamente um fluxo de trabalho adaptável baseado em Forms no OSGi. Esses workflows podem ser usados para desenvolver workflows básicos de revisão e aprovação, processos comerciais internos e entre firewalls. Também é possível usar as etapas Forms Workflow para:

* Crie processos de negócios, fluxos de trabalho pós-envio e fluxos de trabalho de back-end para gerenciar processos de inscrição.

* Criar e atribuir tarefas a um usuário ou grupo.

* Uso [!DNL Adobe Sign] em um fluxo de trabalho AEM para enviar um documento para assinatura.

* Gerar um documento de registro sob demanda ou no envio de um formulário.

* Conecte um modelo de fluxo de trabalho com várias fontes de dados para salvar e recuperar dados facilmente.

* Use a etapa de e-mail para enviar e-mails de notificação e outros anexos ao concluir uma ação e no início ou conclusão de um workflow.

>[!NOTE]
>
>Se o modelo de fluxo de trabalho estiver marcado para um armazenamento externo, para todas as etapas de Forms Workflow, será possível selecionar apenas a opção de variável para armazenar ou recuperar arquivos de dados e anexos.

## Atribuir etapa de tarefa {#assign-task-step}

A etapa de atribuição de tarefa cria um item de trabalho e o atribui a um usuário ou grupo. Junto com a atribuição da tarefa, o componente também especifica o Formulário adaptável ou PDF não interativo para a tarefa. O Formulário adaptável é necessário para aceitar entradas de usuários e PDF não interativo, ou um Formulário adaptável somente leitura é usado para workflows somente para revisão.

Você também pode usar o componente para controlar o comportamento da tarefa. Por exemplo, criar um Documento de registro automático, atribuir a tarefa a um usuário ou grupo específico, especificar o caminho dos dados enviados, especificar o caminho dos dados a serem pré-preenchidos e especificar ações padrão. A etapa Atribuir tarefa tem as seguintes propriedades:

* **[!UICONTROL Título]**: Título da tarefa. O título é exibido na Caixa de entrada do AEM.
* **[!UICONTROL Descrição]**: Explicação das operações que estão sendo executadas na tarefa. Essas informações são úteis para outros desenvolvedores de processos quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

* **[!UICONTROL Caminho da miniatura]**: Caminho da miniatura da tarefa. Se nenhum caminho for especificado, para um Formulário adaptável, uma miniatura padrão será exibida, e para o Documento de registro, um ícone padrão será exibido.
* **[!UICONTROL Estágio do fluxo de trabalho]**: um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada do AEM. É possível definir esses estágios nas propriedades do modelo (Sidekick > Página > Propriedades da página > Estágios).
* **[!UICONTROL Prioridade]**: A prioridade selecionada é exibida na Caixa de entrada do AEM. As opções disponíveis são Alta, Média e Baixa. O valor padrão é Médio.
* **[!UICONTROL Prazo]**: especifique o número de dias ou horas após o qual a tarefa será marcada como vencida. Se você selecionar **[!UICONTROL Desligado]**, a tarefa nunca será marcada como vencida. Você também pode especificar um manipulador de tempo limite para executar tarefas específicas depois que a tarefa estiver vencida.

* **[!UICONTROL Dias]**: O número de dias antes dos quais a tarefa deve ser concluída. O número de dias é contado depois que a tarefa é atribuída a um usuário. Se uma tarefa não estiver concluída e ultrapassar o número de dias especificado no campo Dias, então, se selecionado, um manipulador de tempo limite será acionado após a data de vencimento.
* **[!UICONTROL Horas]**: O número de horas antes das quais a tarefa deve ser concluída. O número de horas é contado depois que a tarefa é atribuída a um usuário. Se uma tarefa não estiver concluída e ultrapassar o número de horas especificado no campo Horas, então, se selecionado, um manipulador de tempo limite será acionado após as horas de vencimento.
* **[!UICONTROL Tempo limite após a data de vencimento]**: selecione esta opção para ativar o campo de seleção Manipulador de tempo limite.
* **[!UICONTROL Manipulador de tempo limite]**: selecione o script a ser executado quando a etapa atribuir tarefa ultrapassar a data de vencimento. Scripts colocados no repositório CRX em [aplicativos]/fd/dashboard/scripts/timeoutHandler estão disponíveis para seleção. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo.
* **[!UICONTROL Realçar a ação e o comentário da última tarefa em Detalhes da tarefa]**: selecione essa opção para exibir a última ação executada e o comentário recebido na seção de detalhes da tarefa de uma tarefa.
* **[!UICONTROL Tipo]**: escolha o tipo de documento a ser preenchido quando o workflow for iniciado. Você pode escolher um Formulário adaptável, Formulário adaptável somente leitura, um documento PDF não interativo.

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL Usar formulário adaptável]**: especifique o método para localizar o Formulário adaptável de entrada. Essa opção estará disponível se você selecionar Formulário adaptável ou Formulário adaptável somente leitura na lista suspensa Tipo. Você pode usar o Formulário adaptável enviado ao fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo String para especificar o caminho.\
  É possível associar várias Forms adaptáveis a um fluxo de trabalho. Como resultado, você pode especificar um Formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL Caminho do formulário adaptável]**: especifique o caminho do Formulário adaptável. Você pode usar o formulário adaptável enviado ao fluxo de trabalho, disponível em um caminho absoluto ou recuperar o formulário adaptável de um caminho armazenado em uma variável do tipo de dados da cadeia de caracteres.
* **[!UICONTROL Selecione o PDF de entrada usando]**: especifique o caminho de um documento PDF não interativo. O campo está disponível ao escolher um documento PDF não interativo no campo Tipo. Você pode selecionar o PDF de entrada usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Payload_Diretory]/Workflow/PDF/credit-card.pdf. O caminho não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. Você precisa de uma opção Documento de registro ativada ou de um modelo de formulário do Adaptive Forms para usar a opção Caminho do PDF.
* **[!UICONTROL Na tarefa concluída, renderize o Formulário adaptável como]**: Quando uma tarefa é marcada como concluída, você pode renderizar o Formulário adaptável como um Formulário adaptável somente leitura ou um documento PDF. Você precisa de uma opção Documento de registro ativada ou modelo de formulário baseado no Forms adaptável para renderizar o Formulário adaptável como Documento de registro.
* **[!UICONTROL Preenchido]**: os seguintes campos listados abaixo servem como entradas para a tarefa:

   * **[!UICONTROL Selecione o arquivo de dados de entrada usando]**: caminho do arquivo de dados de entrada (.json, .xml, .doc ou modelo de dados de formulário). Você pode recuperar o arquivo de dados de entrada usando um caminho relativo à carga útil ou recuperar o arquivo armazenado em uma variável do tipo de dados Documento, XML ou JSON. Por exemplo, o arquivo contém os dados enviados para o formulário por meio de um aplicativo Caixa de entrada AEM. Um exemplo de caminho é [Payload_Diretory]/workflow/data.
   * **[!UICONTROL Selecione os anexos de entrada usando]**: os anexos disponíveis no local são anexados ao formulário associado à tarefa. O caminho pode ser relativo à carga ou recuperar o anexo armazenado em uma variável de um documento. Um exemplo de caminho é [Payload_Diretory]/attachments/. Você pode especificar anexos colocados em relação à carga ou usar uma variável do tipo de documento (Lista de matriz > Documento) para especificar um anexo de entrada para o Formulário adaptável.

  <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL Mapeamento de atributo de solicitação]**: Use a seção Mapeamento de atributos de solicitação para definir o [nome e valor do atributo de solicitação](work-with-form-data-model.md#bindargument). Recupere os detalhes da fonte de dados com base no nome e valor do atributo especificado na solicitação. Você pode definir um valor de atributo de solicitação usando um valor literal ou uma variável do tipo de dados String.

  <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL Informações enviadas]**: os seguintes campos listados abaixo servem como locais de saída para a tarefa:

   * **[!UICONTROL Salvar arquivo de dados de saída usando]**: salve o arquivo de dados (.json, .xml, .doc ou modelo de dados de formulário). O arquivo de dados contém informações enviadas por meio do formulário associado. Você pode salvar o arquivo de dados de saída usando um caminho relativo à carga útil ou armazená-lo em uma variável do tipo de dados Documento, XML ou JSON. Por exemplo, [Payload_Diretory]/Workflow/data, onde os dados são um arquivo.
   * **[!UICONTROL Salvar anexos usando]**: Salve os anexos de formulário fornecidos em uma tarefa. Você pode salvar os anexos usando um caminho relativo à carga ou armazená-lo em uma variável da lista de matriz do tipo de dados Documento.
   * **[!UICONTROL Salvar documento de registro usando]**: caminho para salvar um arquivo de documento de registro. Por exemplo, [Payload_Diretory]/DocumentofRecord/credit-card.pdf. Você pode salvar o documento de registro usando um caminho relativo à carga útil ou armazená-lo em uma variável do tipo de dados Documento. Se você selecionar a variável **[!UICONTROL Relativo à carga útil]** , o documento de registro não será gerado se o campo de caminho estiver vazio. Essa opção estará disponível somente se você selecionar Formulário adaptável na lista suspensa Tipo.

  <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL Destinatário]** > **[!UICONTROL Opções de atribuição]**: especifique o método para atribuir a tarefa a um usuário. Você pode atribuir dinamicamente a tarefa a um usuário ou grupo usando o script Seletor de participante ou atribuir a tarefa a um usuário ou grupo AEM específico.
* **[!UICONTROL Seletor de participantes]**: A opção está disponível quando a variável **[!UICONTROL Dinamicamente para um usuário ou grupo]** for selecionada no campo Assign options. Você pode usar um ECMAScript ou um serviço para selecionar dinamicamente um usuário ou grupo. Para obter mais informações, consulte [Atribuir dinamicamente um fluxo de trabalho aos usuários](https://helpx.adobe.com/experience-manager/kb/HowToAssignAWorkflowDynamicallyToParticipants.html) e [Criação de uma etapa personalizada de Participante dinâmico do Adobe Experience Manager.](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en&amp;CID=RedirectAEMCommunityKautuk)

* **[!UICONTROL Participantes]**: O campo está disponível quando a variável **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** estiver selecionada na caixa **[!UICONTROL Seletor de participantes]** campo. O campo permite selecionar usuários ou grupos para a opção RandomParticipantChooser.

* **[!UICONTROL Destinatário]**: O campo está disponível quando a variável **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** está selecionado no **[!UICONTROL Seletor de participantes]** campo. O campo permite selecionar uma variável de tipo de dados String para definir o destinatário.

* **[!UICONTROL Argumentos]**: o campo fica disponível quando um script diferente do script RandomParticipantChoose é selecionado no campo Seletor de participantes. O campo permite fornecer uma lista de um argumento separado por vírgulas para o script selecionado no campo Seletor de participantes.

* **[!UICONTROL Usuário ou grupo]**: a tarefa é atribuída a um usuário ou grupo selecionado. A opção está disponível quando a variável **[!UICONTROL Para uma opção específica de usuário ou grupo]** está selecionado no **[!UICONTROL Opções de atribuição]** campo. O campo lista todos os usuários e grupos do [!DNL workflow-users] grupo.\
  A variável **[!UICONTROL Usuário ou grupo]** lista os usuários e grupos aos quais o usuário conectado tem acesso. A exibição do nome de usuário depende se você tem permissões de acesso no **[!UICONTROL usuários]** no repositório crx para esse usuário específico.

* **[!UICONTROL Enviar email de notificação]**: selecione essa opção para enviar notificações por email ao signatário. Essas notificações são enviadas quando uma tarefa é atribuída a um usuário ou grupo. Você pode usar o **[!UICONTROL Endereço de email do destinatário]** opção para especificar o mecanismo para recuperar o endereço de email.

* **[!UICONTROL Endereço de email do destinatário]**: você pode armazenar um endereço de email em uma variável, usar um literal para especificar um endereço de email permanente ou usar o endereço de email padrão do destinatário especificado no perfil do destinatário. Você pode usar o literal ou uma variável para especificar o endereço de email de um grupo. A opção de variável é útil para recuperar e usar dinamicamente um endereço de email. A variável **[!UICONTROL Usar endereço de email padrão do destinatário]** A opção é somente para um único destinatário. Nesse caso, o endereço de email armazenado no perfil de usuário designado é usado.

* **[!UICONTROL Modelo de e-mail HTML]**: selecione o template de email para o email de notificação. Para editar um modelo, modifique o arquivo localizado em /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt no repositório crx.
* **[!UICONTROL Permitir delegação para]**: a Caixa de entrada AEM fornece uma opção ao usuário conectado para delegar o fluxo de trabalho atribuído a outro usuário. Você tem permissão para delegar no mesmo grupo ou para o usuário de workflow de outro grupo. Se a tarefa for atribuída a um único usuário e a variável **[!UICONTROL permitir delegação a membros do grupo responsável]** for selecionada, não será possível delegar a tarefa a outro usuário ou grupo.
* **[!UICONTROL Configurações de compartilhamento]**: a Caixa de entrada do AEM fornece opções para compartilhar uma única tarefa ou todas as tarefas na caixa de entrada com outro usuário:
   * Quando a variável **[!UICONTROL Permitir que o destinatário compartilhe explicitamente na caixa de entrada]** for selecionada, o usuário poderá selecionar a tarefa na Caixa de entrada AEM e compartilhá-la com outro usuário AEM.
   * Quando a variável **[!UICONTROL Permitir que o destinatário compartilhe através do compartilhamento da caixa de entrada]** for selecionada e os usuários compartilharem seus itens da Caixa de entrada ou permitir que outros usuários acessem seus itens da Caixa de entrada. Somente as tarefas com a opção mencionada anteriormente ativada serão compartilhadas com outros usuários.
   * Quando a variável **[!UICONTROL Permitir que o destinatário delegue usando as configurações &quot;Ausente&quot;]** está selecionada. O responsável pode habilitar a opção para delegar a tarefa a outros usuários junto com outras opções de Ausência Temporária. Quaisquer novas tarefas atribuídas ao usuário ausente do escritório são automaticamente delegadas (atribuídas) aos usuários mencionados nas configurações ausentes do escritório.

  Ele permite que outros usuários escolham as tarefas atribuídas enquanto estiver fora do escritório e não puder trabalhar nas tarefas atribuídas.

* **[!UICONTROL Ações]** > **[!UICONTROL Ações padrão]**: as ações Enviar, Salvar e Redefinir prontas para uso estão disponíveis. Todas as ações padrão são ativadas, por padrão.
* **[!UICONTROL Variável de rota]**: Nome da variável de rota. A variável de rota captura as ações personalizadas que um usuário seleciona na Caixa de entrada do AEM.
* **[!UICONTROL Rotas]**: uma tarefa pode se ramificar para rotas diferentes. Quando selecionado na Caixa de entrada do AEM, o roteiro retorna um valor e o workflow ramifica com base no roteiro selecionado. Você pode armazenar rotas em uma variável de matriz de tipos de dados String ou selecionar **[!UICONTROL Literal]** para adicionar rotas manualmente.

* **[!UICONTROL Título da rota]**: especifique o título do roteiro. Ele é exibido na Caixa de entrada do AEM.
* **[!UICONTROL Ícone do Coral]**: Especifique um atributo HTML de um ícone de coral. A biblioteca CorelUI do Adobe fornece um vasto conjunto de ícones de primeiro toque. Você pode escolher e usar um ícone para a rota. Ele é exibido junto com o título na Caixa de entrada do AEM. Se você armazenar as rotas em uma variável, elas usarão um ícone de coral &quot;Tags&quot; padrão.
* **[!UICONTROL Permitir ao signatário adicionar comentário]**: selecione essa opção para ativar comentários para a tarefa. Um signatário pode adicionar os comentários de dentro da Caixa de entrada AEM no momento do envio da tarefa.
* **[!UICONTROL Salvar comentário na variável]**: salve o comentário em uma variável do tipo de dados String. Essa opção será exibida somente se você selecionar a opção **[!UICONTROL Permitir ao signatário adicionar comentário]** caixa de seleção

* **[!UICONTROL Permitir ao signatário adicionar anexos à tarefa]**: selecione esta opção para ativar anexos para a tarefa. Um destinatário pode adicionar os anexos da Caixa de entrada AEM no momento do envio da tarefa. Também é possível limitar o tamanho máximo **[!UICONTROL (Tamanho máximo de arquivo)]** de um anexo. O tamanho padrão é 2 MB.

* **[!UICONTROL Salvar anexos de saída da tarefa usando]**: especifique o local da pasta de anexos. Você pode salvar anexos de saída da tarefa usando um caminho relativo à carga útil ou em uma variável de uma matriz de tipos de dados de documento. Essa opção será exibida somente se você selecionar a opção **[!UICONTROL Permitir ao signatário adicionar anexos à tarefa]** e selecione **[!UICONTROL Formulário adaptável]**, **[!UICONTROL Formulário adaptável de somente leitura]** ou **[!UICONTROL Documento PDF não interativo]** do **[!UICONTROL Tipo]** lista suspensa na **[!UICONTROL Formulário/Documento]** guia.

* **[!UICONTROL Usar metadados personalizados]**: selecione essa opção para ativar o campo de metadados personalizado. Os metadados personalizados são usados em modelos de email.
* **[!UICONTROL Metadados personalizados]**: selecione um metadado personalizado para os modelos de email. Os metadados personalizados estão disponíveis no repositório crx em apps/fd/dashboard/scripts/metadataScripts. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. Você também pode usar um serviço para os metadados personalizados. Você também pode estender a variável `WorkitemUserMetadataService` para fornecer metadados personalizados.
* **[!UICONTROL Mostrar dados das etapas anteriores]**: selecione essa opção para permitir que os atribuídos exibam os atribuídos anteriores, a ação já tomada na tarefa, os comentários adicionados à tarefa e o Documento de registro da tarefa concluída, se disponível.
* **[!UICONTROL Mostrar dados das etapas subsequentes]**: selecione essa opção para permitir que o destinatário atual visualize a ação executada e os comentários adicionados à tarefa por atribuídos subsequentes. Ela também permite que o destinatário atual visualize um documento de registro da tarefa concluída, se disponível.
* **[!UICONTROL Visibilidade do tipo de dados]**: por padrão, um destinatário pode exibir um Documento de registro, destinatários, ações executadas e comentários adicionados por destinatários anteriores e subsequentes. Use a opção de visibilidade do tipo de dados para limitar o tipo de dados visível para os atribuídos.

>[!NOTE]
>
>As opções para salvar a etapa Atribuir tarefa como rascunho e recuperar o histórico da etapa Atribuir tarefa são desativadas ao configurar um modelo de fluxo de trabalho AEM para armazenamento de dados externo. Além disso, na Caixa de entrada, a opção para salvar está desativada.

## Converter em etapa PDF/A {#convert-pdfa}

PDF/A é um formato de arquivo que permite preservar o conteúdo do documento a longo prazo, incorporando as fontes e descompactando o arquivo. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Você pode usar o ***Converter em PDF/A*** etapa em um fluxo de trabalho de AEM para converter seus documentos PDF para o formato PDF/A.

A etapa converter em PDF/A tem as seguintes propriedades:

**[!UICONTROL Documento de entrada]**: o documento de entrada pode ser relativo à carga, ter um caminho absoluto, pode ser fornecido como uma carga ou armazenado em uma variável do tipo de dados Documento.

**[!UICONTROL Opções de conversão]**: usando essa propriedade, as configurações para converter documentos PDF em documentos PDF/A são especificadas. Várias opções disponíveis nessa guia são:
* **[!UICONTROL Conformidade]**: especifica o padrão com o qual o PDF/documento de saída deve estar em conformidade. Ele suporta diferentes padrões de PDF, como PDF/A-1b, PDF/A-2b ou PDF/A-3b.
* **[!UICONTROL Nível do resultado]**: Especifica o nível de resultado como PassFail, Summary ou Detailed para a saída de conversão.
* **[!UICONTROL Espaço de cor]**: Especifica o espaço de cores predefinido como S_RGB, COATED_FOGRA27, JAPAN_COLOR_COATED ou SWOP, que pode ser usado para arquivos PDF/A de saída.
* **[!UICONTROL Conteúdo opcional]**: permite que objetos gráficos e/ou anotações específicos sejam visíveis no documento PDF/A de saída somente quando um conjunto especificado de critérios for atendido.

**[!UICONTROL Documentos de saída]**: especifica o local em que o arquivo de saída será salvo. O arquivo de saída pode ser salvo em um local relativo à carga útil, substitui a carga útil, se a carga útil for um arquivo ou em uma variável do tipo de dados Documento.


## Etapa Enviar email {#send-email-step}

Use a etapa do email para enviar um email, por exemplo, um email com um Documento de registro, link de um Formulário adaptável <!-- , link of an interactive communication-->ou com um documento PDF anexado. Suporte à etapa Enviar email [email do HTML](https://en.wikipedia.org/wiki/HTML_email). Os emails de HTML são responsivos e se adaptam ao cliente de email dos recipients e ao tamanho da tela. Você pode usar um template de email HTML para definir a aparência, o esquema de cores e o comportamento do email.

A etapa de email usa o Day CQ Mail Service para enviar emails. Antes de usar a etapa de email, verifique se o serviço de email está configurado. Por padrão, o email suporta somente os protocolos HTTP e HTTPs. [Contate a equipe de suporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en#sending-email) para permitir que as portas enviem emails e habilitem o protocolo SMTP para o seu ambiente. A restrição ajuda a melhorar a segurança da plataforma.

A etapa de email tem as seguintes propriedades:

**[!UICONTROL Título]**: o título da etapa ajuda a identificar a etapa no editor de fluxo de trabalho.

**[!UICONTROL Descrição]**: a explicação é útil para outros desenvolvedores de processo quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

**[!UICONTROL Assunto do email]**: o assunto pode ser recuperado de metadados de fluxo de trabalho, especificados manualmente ou recuperados do valor armazenado em uma variável. Selecione entre as seguintes opções:

* **[!UICONTROL Literal]** Especificar manualmente um assunto.
* **[!UICONTROL Recuperar dos metadados de fluxo de trabalho]** - Recuperar o assunto de uma propriedade de metadados.
* **[!UICONTROL Variável]** - Recupere o assunto do valor armazenado em uma variável do tipo de dados string.

**[!UICONTROL Modelo de e-mail HTML]**: modelo de HTML para o email. Você pode especificar variáveis em um template de email. A etapa Email extrai e exibe todas as variáveis incluídas em um modelo para entradas.

**[!UICONTROL Metadados do modelo de e-mail]**: o valor das variáveis de modelo de email pode ser um valor especificado pelo usuário, o caminho de um ativo no servidor de criação ou publicação, a imagem ou uma propriedade de metadados de fluxo de trabalho.

* **[!UICONTROL Literal]**: use a opção quando souber o valor exato a ser especificado. Por exemplo, [example@example.com](mailto:example@example.com).

* **[!UICONTROL Metadados do fluxo de trabalho]**: use a opção quando o valor a ser usado for salvo em uma propriedade de metadados de workflow. Depois de selecionar a opção, insira o nome da propriedade de metadados na caixa de texto vazia abaixo da opção Metadados do fluxo de trabalho. Por exemplo, emailAddress.

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL Imagem]**: use a opção para incorporar uma imagem ao email. Depois de selecionar a opção, navegue e escolha a imagem. A opção de imagem está disponível somente para as tags de imagem (&lt;img src=&quot;&lt;span id=&quot; translate=&quot;no&quot; />&quot;/>) disponíveis no template de email.&#42;

**[!UICONTROL Endereço de email do remetente/destinatário]**: selecione a variável **[!UICONTROL Literal]** opção para especificar manualmente um endereço de email ou selecionar o **[!UICONTROL Recuperar dos metadados de fluxo de trabalho]** opção para recuperar o endereço de email de uma propriedade de metadados. Você também pode especificar uma lista de matrizes de propriedades de metadados para o **[!UICONTROL Recuperar dos metadados de fluxo de trabalho]** opção. Selecione o **[!UICONTROL Variável]** opção para recuperar o endereço de email do valor armazenado em uma variável do tipo de dados string.

* **[!UICONTROL Anexo de arquivo]**: o ativo disponível no local especificado é anexado ao email. O caminho do ativo pode ser relativo à carga ou ao caminho absoluto. Um exemplo de caminho é [Payload_Diretory]/attachments/.

Selecione o **[!UICONTROL Variável]** opção para recuperar o anexo de arquivo armazenado em uma variável do tipo de dados Documento, XML ou JSON.

**[!UICONTROL Nome do arquivo]**: Nome do arquivo de anexo de email. A Etapa Email altera o nome de arquivo original do anexo para o nome de arquivo especificado. O nome pode ser especificado manualmente ou recuperado de uma propriedade de metadados de fluxo de trabalho ou de uma variável. Use o **[!UICONTROL Literal]** opção quando você souber o valor exato a ser especificado. Use o **[!UICONTROL Variável]** opção para recuperar o nome do arquivo do valor armazenado em uma variável do tipo de dados string. Use o **[!UICONTROL Recuperar de metadados de fluxo de trabalho]** opção quando o valor a ser usado é salvo em uma propriedade de metadados de workflow.

## Etapa Gerar documento de registro {#generate-document-of-record-step}

Quando um formulário é preenchido ou enviado, você pode manter um registro do formulário, impresso ou no formato do documento. Esse registro é chamado de Documento de registro (DoR). Você pode usar a etapa Gerar documento de registro para criar uma versão de PDF somente leitura ou interativa de um formulário adaptável. A versão do PDF contém informações preenchidas no formulário junto com o layout do Formulário adaptável.

A etapa Documento de registro tem as seguintes propriedades:

**[!UICONTROL Usar formulário adaptável]**: especifique o método para localizar o Formulário adaptável de entrada. Você pode usar o Formulário adaptável enviado ao fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo de dados String para especificar o caminho na variável **[!UICONTROL Selecionar variável para resolver]** campo.\
É possível associar várias Forms adaptáveis a um fluxo de trabalho. Como resultado, você pode especificar um Formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

**[!UICONTROL Caminho do formulário adaptável]**: especifique o caminho do Formulário adaptável. O campo está disponível ao selecionar a variável **[!UICONTROL Disponível em um caminho absoluto]** opção no **[!UICONTROL Usar formulário adaptável]** campo.

**[!UICONTROL Selecione os dados de entrada usando]**: Caminho dos dados de entrada para o Formulário adaptável. Você pode manter os dados em um local relativo à carga, especificar um caminho absoluto dos dados ou recuperar dados armazenados em uma variável do tipo de dados Documento, JSON ou XML. Os dados de entrada são mesclados com o Formulário adaptável para criar um Documento de registro.

**[!UICONTROL Selecione o caminho do anexo de entrada usando]**: Caminho dos anexos. Esses anexos são incluídos no documento de registro. Você pode manter os anexos em um local relativo à carga, especificar um caminho absoluto dos anexos ou recuperar anexos armazenados em uma variável de matriz do tipo de dados Documento.

Se você especificar o caminho de uma pasta, por exemplo, anexos, todos os arquivos diretamente disponíveis na pasta serão anexados ao documento de registro. Se houver arquivos disponíveis nas pastas diretamente disponíveis no caminho de anexo especificado, os arquivos serão incluídos no Documento de registro como anexos. Se houver pastas em pastas diretamente disponíveis, elas serão ignoradas.

**[!UICONTROL Salve o documento de registro gerado usando as opções abaixo]**: especifique o local no qual manter um arquivo de documento de registro. Você pode optar por substituir a pasta de carga útil, colocar o Documento de registro em um local no diretório da carga útil ou armazenar o Documento de registro em uma variável do tipo de dados Documento.

**[!UICONTROL Localidade]**: especifique o idioma do documento de registro. Selecionar **[!UICONTROL Literal]** para selecionar o local em uma lista suspensa ou selecione **[!UICONTROL Variável]** para recuperar o local do valor armazenado em uma variável do tipo de dados string. Defina o código do local ao armazenar o valor do local em uma variável. Por exemplo, especifique **pt_BR** para inglês e **fr_FR** para o francês.

## Chamar etapa DDX {#invokeddx}

O Document Description XML (DDX) é uma linguagem de marcação declarativa cujos elementos representam os blocos fundamentais de documentos. Esses blocos fundamentais incluem documentos PDF e XDP, além de outros elementos, como comentários, marcadores e texto estilizado. O DDX define um conjunto de operações, que podem ser aplicadas em um ou mais documentos de entrada para gerar um ou mais documentos de saída. Um único DDX pode ser usado com uma variedade de documentos de origem. Você pode usar o ***Chamar etapa DDX*** em um Workflow do AEM para executar várias operações, como Montar, Desmontar documentos, Criar e modificar Forms do Acrobat e XFA e outras descritas no [Documentação de referência do DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

A etapa Chamar DDX tem as seguintes propriedades:

**[!UICONTROL Documentos de entrada]**: usado para definir propriedades de um documento de entrada. Várias opções disponíveis nessa guia são:
* **[!UICONTROL Especifique o DDX usando]**: especifica o documento de entrada relativo à carga útil, tem um caminho absoluto, pode ser fornecido como carga útil ou armazenado em uma variável do tipo de dados Documento.
* **[!UICONTROL Criar mapa da carga útil]**: adicione todos os documentos na pasta de carga útil ao Mapa do documento de entrada para a API de chamada no Assembler. O nome do nó de cada documento é usado como uma chave no mapa.
* **[!UICONTROL Mapa do documento de entrada]**: A opção é usada para adicionar várias entradas usando o **[!UICONTROL ADICIONAR]** botão. Cada entrada representa a chave do documento no mapa e a origem do documento.

**[!UICONTROL Opções de ambiente]**: essa opção é usada para definir as configurações de processamento para invocar API. Várias opções disponíveis nessa guia são:
* **[!UICONTROL Validar apenas]**: verifica a validade do documento DDX de entrada.
* **[!UICONTROL Falha ao errar]**: valor booleano para indicar se o serviço de invocar API falha, se houver ou não um erro. Por padrão, seu valor é definido como Falso.
* **[!UICONTROL Primeiro número Bates]**: especifica o número que é autoincrementável. Esse número de autoincrementação é exibido em cada página consecutiva automaticamente.
* **[!UICONTROL Estilo padrão]**: define o estilo padrão para o arquivo de saída.

>[!NOTE]
>
>As opções de ambiente são mantidas em sincronia com as APIs HTTP.

**[!UICONTROL Documentos de saída]**: especifica o local em que o arquivo de saída será salvo. Várias opções disponíveis nessa guia são:
* **[!UICONTROL Salvar saída na carga útil]**: salva os documentos de saída na pasta da carga útil, ou substitui a carga útil, caso a carga útil seja um arquivo.
* **[!UICONTROL Mapa do documento de saída]**: Especifica o local para salvar explicitamente cada arquivo de documento, adicionando uma entrada por documento. Cada entrada representa o documento e o local onde ele deve ser salvo. Se houver vários documentos de saída, essa opção será usada.

## Chamar etapa do serviço de modelo de dados de formulário {#invoke-form-data-model-service-step}

Você pode usar [[!DNL AEM Forms] Integração de dados](data-integration.md) para configurar e conectar-se a diferentes fontes de dados. Essas fontes de dados podem ser um serviço Web, um serviço REST, um serviço OData e uma solução de CRM. [!DNL AEM Forms] A Integração de dados permite criar um Modelo de dados de formulário que abrange vários serviços para executar operações de recuperação, adição e atualização de dados no banco de dados configurado. Você pode usar o **[!UICONTROL Chamar etapa de serviço do modelo de dados]** para selecionar um Modelo de Dados de Formulário (FDM) e usar os serviços do FDM para recuperar, atualizar ou adicionar dados a diferentes fontes de dados.

Para explicar entradas para campos da etapa, a seguinte tabela de banco de dados e arquivo JSON são usados como exemplo:

**[!UICONTROL Exemplo de tabela CustomerDetails]**

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
   <td>ID do cliente</td> 
   <td>1</td> 
  </tr> 
  <tr> 
   <td>Endereço de email<br /> </td> 
   <td>srose@we.info</td> 
  </tr> 
 </tbody> 
</table>

**[!UICONTROL Arquivo JSON de amostra]**

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

A etapa Chamar serviço do modelo de dados de formulário tem os campos listados abaixo para facilitar as operações do Modelo de dados de formulário:

* **[!UICONTROL Título]**: Título da etapa. Ajuda a identificar as etapas no editor de workflow.
* **[!UICONTROL Descrição]**: Explicação útil para outros desenvolvedores de processo quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

* **[!UICONTROL Caminho do modelo de dados de formulário]**: procure e selecione um modelo de dados de formulário presente no servidor.

* **[!UICONTROL Erros e validações]**: A opção permite capturar mensagens de erro e especificar opções de validação para dados recuperados e enviados para fontes de dados. Com essas alterações, você pode garantir que os dados transmitidos para a etapa Chamar serviço de modelo de dados de formulário sigam as restrições de dados definidas pela fonte de dados. Para obter mais detalhes, consulte [Validação automatizada dos dados de entrada](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL Nível de validação]**: há três categorias de validações: Básica, Completa e DESATIVADA:

   * Total: todas as restrições são validadas.
   * Básico: somente restrições obrigatórias e anuláveis
   * DESATIVADO: Não ocorre validação.

* **[!UICONTROL Finalizar o fluxo de trabalho na falha]**: quando uma restrição não é validada, o fluxo de trabalho é interrompido.

* **[!UICONTROL Armazenar código de erro na variável]**: Você pode armazenar um código de erro em um [Variável de tipo de string](variable-in-aem-workflows.md).

* **[!UICONTROL Armazenar mensagem de erro na variável]**: Você pode armazenar uma mensagem de erro em um [Variável de tipo de string](variable-in-aem-workflows.md).

* **[!UICONTROL Armazenar detalhes do erro na variável]**: Você pode armazenar um detalhe de erro em um [Variável de tipo JSON](variable-in-aem-workflows.md).

* **[!UICONTROL Serviço]**: lista dos serviços que o Modelo de dados de formulário selecionado fornece.
* **[!UICONTROL Entrada de serviços]** > **[!UICONTROL Forneça dados de entrada usando literal, variável ou metadados de fluxo de trabalho e um arquivo JSON]**: um serviço pode ter vários argumentos. Selecione a opção para obter o valor dos argumentos de serviço de uma propriedade de metadados do fluxo de trabalho, um objeto JSON, uma variável ou insira o valor diretamente na caixa de texto fornecida:

   * **[!UICONTROL Literal]**: use a opção quando souber o valor exato a ser especificado. Por exemplo, srose@we.info.
   * **[!UICONTROL Variável]**: use a opção para recuperar o valor armazenado em uma variável.
   * **[!UICONTROL Recuperar metadados de fluxo de trabalho]**: use a opção quando o valor a ser usado for salvo em uma propriedade de metadados de workflow. Por exemplo, emailAddress.

   * **[!UICONTROL Relativo à carga útil]**: use a opção para recuperar o anexo de arquivo salvo em um caminho relativo à carga. Selecione a opção e especifique o nome da pasta que inclui o anexo de arquivo ou especifique o nome do anexo de arquivo na caixa de texto.

     Por exemplo, se a pasta Relativo à carga no repositório CRX incluir um anexo de arquivo na `attachment\attachment-folder` local, especificar `attachment\attachment-folder` na caixa de texto após selecionar a variável **[!UICONTROL Relativo à carga útil]** opção.

   * **[!UICONTROL Anotação JSON Dot]**: use a opção quando o valor a ser usado estiver em um arquivo JSON. Por exemplo, insurance.customerDetails.emailAddress. A opção Anotação JSON Dot estará disponível somente se Mapear campos de entrada da opção JSON de entrada estiver selecionada.
   * **[!UICONTROL Mapear campos de entrada a partir do JSON de entrada]**: especifique o caminho de um arquivo JSON para obter o valor de entrada de alguns argumentos de serviço do arquivo JSON. O caminho do arquivo JSON pode ser relativo à carga, um caminho absoluto ou você pode selecionar um documento JSON de entrada usando uma variável do tipo JSON ou Modelo de dados de formulário.

* **[!UICONTROL Entrada de serviços]** > **[!UICONTROL Forneça dados de entrada usando variável ou um arquivo JSON]**: selecione a opção para obter valores para todos os argumentos de um arquivo JSON salvo em um caminho absoluto, em um caminho relativo à carga ou em uma variável.
* **[!UICONTROL Selecione o documento JSON de entrada usando]**: o arquivo JSON que contém valores para todos os argumentos de serviço. O caminho do arquivo JSON pode ser **[!UICONTROL relativo à carga útil]** ou um **[!UICONTROL caminho absoluto]**. Você também pode recuperar o documento JSON de entrada usando uma variável do tipo de dados JSON ou Modelo de dados de formulário.

* **[!UICONTROL Anotação JSON Dot]**: deixe o campo em branco para usar todos os objetos do arquivo JSON especificado como entrada para argumentos de serviço. Para ler um objeto JSON específico do arquivo JSON especificado como entrada para argumentos de serviço, especifique a notação de pontos para o objeto JSON. Por exemplo, se você tiver um JSON semelhante ao listado no início da seção, especifique insurance.customerDetails para fornecer todos os detalhes de um cliente como entrada para o serviço.
* **[!UICONTROL Saída do serviço]** > **[!UICONTROL Mapear e gravar valores de saída na variável ou nos metadados]**: selecione a opção para salvar os valores de saída como propriedades do nó de metadados da instância do fluxo de trabalho no repositório crx. Especifique o nome da propriedade de metadados e selecione o atributo de saída de serviço correspondente a ser mapeado com a propriedade de metadados, por exemplo, mapeie o phone_number retornado pelo serviço de saída com a propriedade phone_number dos metadados do fluxo de trabalho. Da mesma forma, você pode armazenar a saída em uma variável do tipo de dados Long. Ao selecionar uma propriedade para a variável **[!UICONTROL Atributo de saída de serviço a ser mapeado]** opção, somente as variáveis capazes de armazenar dados da propriedade selecionada serão preenchidas para o **[!UICONTROL Salvar a saída em]** opção.

* **[!UICONTROL Saída do serviço]** > **[!UICONTROL Salvar saída na variável ou em um arquivo JSON]**: selecione a opção para salvar os valores de saída em um arquivo JSON em um caminho absoluto, em um caminho relativo à carga ou em uma variável.
* **[!UICONTROL Salve o documento JSON de saída usando as opções abaixo]**: salve o arquivo JSON de saída. O caminho do arquivo JSON de saída pode ser relativo à carga útil ou a um caminho absoluto. Você também pode salvar o arquivo JSON de saída usando uma variável do tipo de dados JSON ou Modelo de dados de formulário.



## Etapa Assinar documento {#sign-document-step}

A etapa Assinar documento permite usar [!DNL Adobe Sign] para assinar documentos. Quando você usa o [!DNL Adobe Sign] Etapa do fluxo de trabalho para Assinar um Formulário adaptável, o formulário pode ser passado pelos destinatários um após o outro ou pode ser enviado para todos os destinatários simultaneamente, dependendo da configuração da etapa do fluxo de trabalho. [!DNL Adobe Sign] Os Forms adaptáveis ativados são enviados ao Experience Manager Forms Server somente depois que todos os destinatários concluírem o processo de assinatura.

Por padrão, a variável [!DNL Adobe Sign] O serviço Scheduler verifica (pesquisa) a resposta do recipient a cada 24 horas. Você pode [alterar o intervalo padrão do seu ambiente](adobe-sign-integration-adaptive-forms.md#for-aem-workflows-only-configure-dnl-adobe-acrobat-sign-scheduler-to-sync-the-signing-status-configure-adobe-sign-scheduler-to-sync-the-signing-status).

A etapa Assinar documento tem as seguintes propriedades:

* **[!UICONTROL Nome do Contrato]**: especifique o título do contrato. O nome do contrato torna-se parte do assunto e do corpo do texto do email enviado aos signatários. Você pode armazenar o nome em uma variável do tipo de dados String ou selecionar **[!UICONTROL Literal]** para adicionar o nome manualmente.

* **[!UICONTROL Localidade]**: especifique o idioma para as opções de email e verificação. Você pode armazenar o local em uma variável do tipo de dados String ou selecionar **[!UICONTROL Literal]** para escolher o local na lista de opções disponíveis. Você deve definir o código do local ao armazenar o valor do local em uma variável. Por exemplo, especifique **[!UICONTROL pt_BR]** para inglês e **[!UICONTROL fr_FR]** para o francês.

* **[!UICONTROL Configuração da nuvem do Adobe Sign]**: escolha um [!DNL Adobe Sign] Configuração na nuvem. Se você não tiver configurado [!DNL Adobe Sign] para [!DNL AEM Forms], consulte [Integrar o Adobe Sign com o [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL Selecione o documento a ser assinado usando]**: Você pode escolher um documento de um local relativo à carga útil, usá-lo como o documento, especificar um caminho absoluto para o documento ou recuperar o documento armazenado em uma variável do tipo de dados Documento.
* **[!UICONTROL Dias até o prazo]**: Um documento está marcado como vencido (com prazo excedido) depois que não há nenhuma atividade na tarefa durante o número de dias especificado no **[!UICONTROL Dias até o prazo]** campo. O número de dias é contado depois que a documentação é atribuída a um usuário para assinatura.
* **[!UICONTROL Frequência de e-mails de lembrete]**: você pode enviar um email de lembrete em um intervalo diário ou semanal. A semana é contada a partir do dia em que a documentação é atribuída a um usuário para assinatura.
* **[!UICONTROL Processo de assinatura]**: é possível optar por assinar um documento em uma ordem sequencial ou paralela. Em ordem sequencial, um signatário recebe o documento de cada vez para assinar. Depois que o primeiro signatário terminar de assinar o documento, ele será enviado ao segundo signatário e assim por diante. Em ordem paralela, vários signatários podem assinar um documento de cada vez.
* **[!UICONTROL URL de redirecionamento]**: especifique um URL de redirecionamento. Depois que o documento for assinado, você poderá redirecionar o destinatário para um URL. Normalmente, este URL contém uma mensagem de agradecimento ou mais instruções.
* **[!UICONTROL Estágio do fluxo de trabalho]**: um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada do AEM. É possível definir esses estágios nas propriedades do modelo ( **[!UICONTROL Sidekick]** > **[!UICONTROL Página]** > **[!UICONTROL Propriedades da página]** > **[!UICONTROL Estágios]**).
* **[!UICONTROL Selecionar destinatários]**: especifique o método para escolher os destinatários do documento. Você pode atribuir o fluxo de trabalho de maneira dinâmica a um usuário ou grupo ou adicionar manualmente os detalhes de um recipient. Ao selecionar Manually na lista suspensa, você adiciona detalhes do recipient, como email, função e método de autenticação.

  >[!NOTE]
  >
  >* Na seção Função, você pode especificar a função do destinatário como Signatário, Aprovador, Aceitador, Destinatário certificado, Preenchedor de formulário e Delegador.
  >* Se você selecionar Delegator na opção Role, o Delegator poderá atribuir a tarefa de assinatura a outro recipient.
  >* Se você tiver configurado um método de autenticação para [!DNL Adobe Sign], com base em sua configuração, você seleciona um método de autenticação, como autenticação baseada em telefone, autenticação baseada em identidade social, autenticação baseada em conhecimento, autenticação baseada em identidade governamental.

* **[!UICONTROL Script ou serviço para selecionar recipients]**: a opção estará disponível somente se você selecionar a opção Dynamically no campo Select Recipients. Você pode especificar um ECMAScript ou um serviço para escolher assinantes e opções de verificação para um documento.
* **[!UICONTROL Detalhes do destinatário]**: a opção estará disponível somente se a opção Manually estiver selecionada no campo Select Recipients. Especifique um endereço de email e escolha um mecanismo de verificação opcional. Antes de selecionar um mecanismo de verificação de duas etapas, verifique se a opção de verificação correspondente está habilitada para o configurado [!DNL Adobe Sign] conta. Você pode usar uma variável do tipo de dados String para definir valores para os campos Email, Código do país e Número de telefone. Os campos Código do país e Número de telefone serão exibidos somente se você selecionar Verificação de telefone na lista suspensa de verificação de duas etapas.
* **[!UICONTROL Documento assinado]**: é possível salvar o status do documento assinado na variável. Para adicionar uma trilha de auditoria de assinatura eletrônica para maior segurança e legalidade ao Documento assinado, você pode Incluir o Relatório de auditoria. Você pode salvar o Documento assinado usando a pasta Variável ou Carga.

  >[!NOTE]
  >
  > O relatório de auditoria é anexado à última página do documento assinado.

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
* **[!UICONTROL Indirect accessible printer]**: The printer that is installed on a print server is accessed from other computers. Technologies such as the common UNIX&reg; printing system (CUPS) and the Line Printer Daemon (LPD) protocol are available to connect to a network printer. To access an indirect accessible printer, specify the print server's IP or host name. Using this mechanism, you can send a document to an LPD URI when the network has an LPD running. The mechanism lets you route the document to any printer that is connected to the network that has an LPD running.
    -->

## Etapa Gerar Saída Impressa {#generatePrintedOutput}

A etapa gera uma saída PCL, PostScript, ZPL, IPL, TPCL ou DPL, considerando um design de formulário e um arquivo de dados. O arquivo de dados é mesclado com o design do formulário e formatado para impressão. A saída gerada por essa etapa pode ser enviada diretamente para uma impressora ou salva como um arquivo. É recomendável usar essa etapa quando quiser usar designs de formulário ou dados de um aplicativo. Se os designs de formulário estiverem na rede, no sistema de arquivos local ou no local HTTP, use a operação generatePrintedOutput.

Por exemplo, seu aplicativo exige a mesclagem de um design de formulário com um arquivo de dados. Os dados contêm centenas de registros. Além disso, requer que a saída seja enviada para uma impressora que suporte ZPL. O design do formulário e os dados de entrada estão em um aplicativo. Use a operação generatePrintedOutput para mesclar cada registro com um design de formulário e enviar a saída para uma impressora compatível com ZPL.

A etapa Gerar Saída Impressa tem as seguintes propriedades:

**[!UICONTROL Propriedades de entrada]**

* **[!UICONTROL Selecione o arquivo de modelo usando]**: especifique o caminho do arquivo de modelo. Você pode selecionar o arquivo de modelo usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Payload_Diretory]/Workflow/data.xml. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo. Além disso, você também pode aceitar a carga como o arquivo de dados de entrada.

* **[!UICONTROL Selecione o documento de dados usando]**: especifique o caminho de um arquivo de dados de entrada. Você pode selecionar o arquivo de dados de entrada usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Payload_Diretory]/Workflow/data.xml. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo.

* **[!UICONTROL Formato da impressora]**: um valor de Formato de impressão que especifica a linguagem de descrição de página a ser usada, quando um arquivo XDC não for fornecido, para gerar o fluxo de saída. Se você fornecer um valor literal, selecione um destes valores:

   * **[!UICONTROL PCL colorida]**: use a opção para especificar um arquivo XDC para PCL.
   * **[!UICONTROL PostScript genérico]**: use a opção para especificar um arquivo XDC genérico para PostScript.
   * **[!UICONTROL ZPL 300 DPI]**: Use ZPL 300 DPI. O zpl300.xdc é usado.
   * **[!UICONTROL ZPL 600 DPI]**: Use ZPL 600 DPI. O arquivo zpl600.xdc é usado.
   * **[!UICONTROL IPL 300 DPI]**: Use IPL 300 DPI. O ipl300.xdc é usado.
   * **[!UICONTROL IPL 400 DPI]**: Use IPL 400 DPI. O arquivo ipl400.xdc é usado.
   * **[!UICONTROL TPCL 600 DPI]**: Use TPCL 600 DPI. O arquivo tpcl600.xdc é usado.
   * **[!UICONTROL PostScript simples]**: use a opção para especificar um arquivo XDC de texto sem formatação para PostScript.
   * **[!UICONTROL DPL300DPI]**: Use DPL 300 DPI. A dpl300.xdc é usada.
   * **[!UICONTROL DPL400DPI]**: Use DPL 400 DPI. A dpl400.xdc é usada.
   * **[!UICONTROL DPL600DPI]**: Use DPL 600 DPI. A dpl600.xdc é usada.
   * **[!UICONTROL HP_PCL_5e]**: use a opção para suportar vários dispositivos Canon.


**[!UICONTROL Propriedades de saída]**

* **[!UICONTROL Salvar documento de saída usando]**: especifique o local em que o arquivo de saída será salvo. Você pode salvar o arquivo de saída em um local relativo à carga útil, em uma variável ou especificar um local absoluto para salvar o arquivo de saída. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo.

**[!UICONTROL Propriedades avançadas]**

* **[!UICONTROL Selecione o local da raiz do conteúdo usando]**: raiz de conteúdo é um valor de cadeia de caracteres que especifica o URI, a referência absoluta ou o local no repositório para recuperar ativos relativos usados pelo design do formulário. Por exemplo, se o design do formulário referenciar uma imagem relativamente, como `../myImage.gif`, `myImage.gif` deve estar em `repository://`. O valor padrão é `repository://`, que aponta para o nível raiz do repositório.

  Quando você seleciona um ativo do aplicativo, o caminho do URI da raiz do conteúdo deve ter a estrutura correta. Por exemplo, se um formulário for selecionado de um aplicativo chamado SampleApp e for colocado em `SampleApp/1.0/forms/Test.xdp`, o URI da Raiz de Conteúdo deve ser especificado como `repository://administrator@password/Applications/SampleApp/1.0/forms/`ou `repository:/Applications/SampleApp/1.0/forms/` (quando a autoridade é nula). Quando o URI da raiz do conteúdo é especificado dessa maneira, os caminhos de todos os ativos referenciados no formulário são resolvidos em relação a esse URI.

* **[!UICONTROL Selecione o arquivo XCI usando]**: os arquivos XCI são usados para descrever fontes e outras propriedades usadas para elementos de design de formulário. Você pode manter um arquivo XCI relativo à carga útil, em um caminho absoluto ou usando uma variável do tipo de dados Documento.

* **[!UICONTROL Localidade]**: especifica a linguagem usada para gerar o documento PDF. Se você fornecer um valor literal, selecione um idioma na lista ou selecione um destes valores:
   * **[!UICONTROL Para usar o padrão do servidor]**: (Padrão) Use a configuração de Local definida no [!DNL AEM Forms] Servidor. A configuração Local é definida usando o Console de administração. (Consulte [Ajuda do Designer](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf).)

   * **[!UICONTROL Para usar o valor personalizado]**: digite o código de localidade na caixa literal ou selecione uma variável de cadeia de caracteres que contenha o código de localidade. Para obter uma lista completa de códigos de localidade compatíveis, consulte https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Cópias]**: um valor inteiro que especifica o número de cópias para gerar para a saída. O valor padrão é 1.

* **[!UICONTROL Impressão frente e verso]**: um valor de Paginação que especifica se a impressão em frente e verso ou em verso deve ser usada. As impressoras que suportam PostScript e PCL usam esse valor. Se você fornecer um valor literal, selecione um destes valores:
   * **[!UICONTROL Borda maior frente e verso]**: use a impressão frente e verso e imprima usando a paginação de borda maior.
   * **[!UICONTROL Borda menor frente e verso]**: use a impressão frente e verso e imprima usando a paginação de borda curta.
   * **[!UICONTROL Simples]**: use a impressão de lado único.

## Etapa Gerar saída de PDF não interativa   {#generatePDFdocuments}

1. Arraste o workflow Gerar saída de PDF não interativa para a guia Forms Workflow no Sidekick.
1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, documentos de saída e parâmetros adicionais e clique em **[!UICONTROL OK]**.

### Documentos de entrada {#input-documents-3}

* **Arquivo modelo**: especifica o local do modelo XDP. É um campo obrigatório.

* **Documento de dados**: especifica o local do xml de dados que deve ser mesclado com o modelo.

### Documento de saída {#output-document}

**Documento de saída**: especifica o nome do formulário de PDF gerado.

### Parâmetros adicionais {#additional-parameters-1}

* **Raiz de conteúdo**: especifica o caminho para a pasta no repositório onde os fragmentos ou imagens usados no modelo XDP de entrada são armazenados.
* **Localidade**: especifica a localidade padrão para o formulário de PDF gerado.
* **Versão do Acrobat**: especifica a versão de destino do Acrobat para o formulário de PDF gerado.
* **PDF linearizado**: especifica se o PDF gerado deve ser otimizado para visualização na web.
* **PDF marcado**: especifica se o PDF gerado deve ficar acessível.
* **Documento XCI**: especifica o caminho para o arquivo XCI.

## Consulte também {#see-also}

* [Variáveis em fluxos de trabalho AEM centrados no Forms](/help/forms/variable-in-aem-workflows.md)
* [Definir configuração de Ausência Temporária](/help/forms/configure-out-of-office-settings.md)

<!--

>[!MORELIKETHIS]
>
>* [Forms-centric workflow on OSGi](/help/forms/aem-forms-workflow.md)
>* [Use AEM translation workflow to localize Adaptive Forms and Document of Record](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms.md)

-->