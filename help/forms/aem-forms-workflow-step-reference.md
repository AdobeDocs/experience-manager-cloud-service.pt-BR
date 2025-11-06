---
title: Quais etapas de fluxo de trabalho estão disponíveis para o AEM Forms Cloud Service criar um fluxo de trabalho ou para a automação de processos de negócios (BPM)?
description: Fluxos de trabalho centrados no Forms permitem criar rapidamente fluxos de trabalho adaptáveis baseados no Forms. Você pode usar o Adobe Sign para assinar documentos eletronicamente, criar processos de negócios baseados em formulários, recuperar e enviar dados para várias fontes de dados e enviar notificações por email
exl-id: e1403ba6-8158-4961-98a4-2954b2e32e0d
google-site-verification: A1dSvxshSAiaZvk0yHu7-S3hJBb1THj0CZ2Uh8N_ck4
keywords: Usar workflows do AEM, usando etapas atribuir tarefa, converter para etapa PDF/A, Gerar documento da etapa registrada, usar workflows, etapa Assinar documento, etapa Gerar saída impressa, Gerar saída não interativa do PDF
feature: Adaptive Forms, Workflow
role: Admin, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '7409'
ht-degree: 0%

---


# Usar fluxos de trabalho do AEM centrados na Forms - referência de etapa para automatizar processos de negócios {#forms-centric-workflow-on-osgi-step-reference}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

Você usa modelos de fluxo de trabalho. Um modelo ajuda a definir e executar uma série de etapas. Você também pode definir propriedades do modelo, como se o fluxo de trabalho é transitório ou usa vários recursos. Você pode [incluir várias etapas do fluxo de trabalho do AEM em um modelo para obter a lógica de negócios](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=pt-BR#extending-aem).

## Etapas centradas no Forms {#forms-workflow-steps}

As etapas de fluxo de trabalho centradas no Forms executam operações específicas do AEM Forms em um fluxo de trabalho do AEM. Forms Essas etapas permitem criar rapidamente um fluxo de trabalho adaptável baseado em Forms no OSGi. Esses workflows podem ser usados para desenvolver workflows básicos de revisão e aprovação, processos comerciais internos e entre firewalls. Também é possível usar as etapas do Forms Workflow para:

* Crie processos de negócios, fluxos de trabalho pós-envio e fluxos de trabalho de back-end para gerenciar processos de inscrição.

* Criar e atribuir tarefas a um usuário ou grupo.

* Use [!DNL Adobe Sign] em um fluxo de trabalho do AEM para enviar um documento para assinatura.

* Gerar um documento de registro sob demanda ou no envio de um formulário.

* Conecte um modelo de fluxo de trabalho com várias fontes de dados para salvar e recuperar dados facilmente.

* Use a etapa de e-mail para enviar e-mails de notificação e outros anexos ao concluir uma ação e no início ou conclusão de um workflow.

>[!NOTE]
>
>Se o modelo de fluxo de trabalho estiver marcado para um armazenamento externo, para todas as etapas do Forms Workflow, será possível selecionar apenas a opção de variável para armazenar ou recuperar arquivos de dados e anexos.

## Atribuir etapa de tarefa {#assign-task-step}

A etapa de atribuição de tarefa cria um item de trabalho e o atribui a um usuário ou grupo. Junto com a atribuição da tarefa, o componente também especifica o Formulário adaptável ou o PDF não interativo para a tarefa. O Formulário adaptável é necessário para aceitar entradas de usuários e PDF não interativos ou um Formulário adaptável somente leitura é usado para workflows somente revisão.

Você também pode usar o componente para controlar o comportamento da tarefa. Por exemplo, criar um Documento de registro automático, atribuir a tarefa a um usuário ou grupo específico, especificar o caminho dos dados enviados, especificar o caminho dos dados a serem pré-preenchidos e especificar ações padrão. A etapa Atribuir tarefa tem as seguintes propriedades:

* **[!UICONTROL Título]**: título da tarefa. O título é exibido na Caixa de entrada do AEM.
* **[!UICONTROL Descrição]**: Explicação das operações que estão sendo executadas na tarefa. Essas informações são úteis para outros desenvolvedores de processos quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

* **[!UICONTROL Caminho da miniatura]**: caminho da miniatura da tarefa. Se nenhum caminho for especificado, para um Formulário adaptável, uma miniatura padrão será exibida, e para o Documento de registro, um ícone padrão será exibido.
* **[!UICONTROL Estágio do fluxo de trabalho]**: um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada do AEM. É possível definir esses estágios nas propriedades do modelo (Sidekick > Página > Propriedades da página > Estágios).
* **[!UICONTROL Prioridade]**: a prioridade selecionada é exibida na Caixa de Entrada do AEM. As opções disponíveis são Alta, Medium e Baixa. O valor padrão é Medium.
* **[!UICONTROL Data de vencimento]**: especifique o número de dias ou horas após o qual a tarefa será marcada como vencida. Se você selecionar **[!UICONTROL Desativado]**, a tarefa nunca será marcada como vencida. Você também pode especificar um manipulador de tempo limite para executar tarefas específicas depois que a tarefa estiver vencida.

* **[!UICONTROL Dias]**: o número de dias antes dos quais a tarefa deve ser concluída. O número de dias é contado depois que a tarefa é atribuída a um usuário. Se uma tarefa não estiver concluída e ultrapassar o número de dias especificado no campo Dias, em seguida, se for selecionada, um manipulador de tempo limite será acionado após a data de vencimento.
* **[!UICONTROL Horas]**: o número de horas antes das quais a tarefa deve ser concluída. O número de horas é contado depois que a tarefa é atribuída a um usuário. Se uma tarefa não estiver concluída e ultrapassar o número de horas especificado no campo Horas, e se for selecionada, um manipulador de tempo limite será acionado após as horas de vencimento.
* **[!UICONTROL Tempo limite após a Data de Conclusão]**: selecione essa opção para habilitar o campo de seleção Manipulador de Tempo Limite.
* **[!UICONTROL Manipulador de tempo limite]**: selecione o script a ser executado quando a etapa de atribuição de tarefa ultrapassar a data de vencimento. Os scripts colocados no repositório CRX em [apps]/fd/dashboard/scripts/timeoutHandler estão disponíveis para seleção. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo.
* **[!UICONTROL Realçar a ação e o comentário da última tarefa em Detalhes da Tarefa]**: selecione essa opção para exibir a última ação realizada e o comentário recebido na seção de detalhes da tarefa de uma tarefa.
* **[!UICONTROL Tipo]**: escolha o tipo de documento a ser preenchido quando o fluxo de trabalho for iniciado. Você pode escolher um Formulário adaptável, Formulário adaptável somente leitura, um documento não interativo do PDF.

<!-- , Interactive Communication Agent UI, or Interactive Communication Web Channel Document. -->


* **[!UICONTROL Usar formulário adaptável]**: especifique o método para localizar o formulário adaptável de entrada. Essa opção estará disponível se você selecionar Formulário adaptável ou Formulário adaptável somente leitura na lista suspensa Tipo. Você pode usar o Formulário adaptável enviado ao fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo String para especificar o caminho.\
  É possível associar várias Forms adaptáveis a um fluxo de trabalho. Como resultado, você pode especificar um Formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

<!-- 

* **[!UICONTROL Use Interactive Communication]**: Specify the method to locate the input interactive communication. You can use the interactive communication submitted to the workflow, available at an absolute path, or available at a path in a variable. You can use a variable of type String to specify the path. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 

> [!NOTE]
>
>You must have cm-agent-users and workflow-users group assignments to access Interactive Communications Agent UI in AEM inbox.  

-->

* **[!UICONTROL Caminho do formulário adaptável]**: especifique o caminho do formulário adaptável. Você pode usar o formulário adaptável enviado ao fluxo de trabalho, disponível em um caminho absoluto ou recuperar o formulário adaptável de um caminho armazenado em uma variável do tipo de dados da cadeia de caracteres.
* **[!UICONTROL Selecione o PDF de entrada usando]**: especifique o caminho de um documento PDF não interativo. O campo está disponível ao escolher um documento PDF não interativo no campo Tipo. Você pode selecionar o PDF de entrada usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Payload_Diretory]/Workflow/PDF/credit-card.pdf. O caminho não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. Você precisa de uma opção Documento de registro ativada ou de um modelo de formulário baseado no Forms adaptável para usar a opção Caminho do PDF.
* **[!UICONTROL Para tarefas concluídas, renderize o Formulário Adaptável como]**: quando uma tarefa é marcada como concluída, você pode renderizar o Formulário Adaptável como um Formulário Adaptável somente leitura ou um documento do PDF. Você precisa de uma opção Documento de registro ativada ou modelo de formulário baseado no Forms adaptável para renderizar o Formulário adaptável como Documento de registro.
* **[!UICONTROL Pré-preenchido]**: os seguintes campos listados abaixo servem como entradas para a tarefa:

   * **[!UICONTROL Selecione o arquivo de dados de entrada usando]**: Caminho do arquivo de dados de entrada (.json, .xml, .doc ou modelo de dados de formulário (FDM)). Você pode recuperar o arquivo de dados de entrada usando um caminho relativo à carga útil ou recuperar o arquivo armazenado em uma variável do tipo de dados Documento, XML ou JSON. Por exemplo, o arquivo contém os dados enviados para o formulário por meio de um aplicativo Caixa de entrada AEM. Um exemplo de caminho é [Payload_Diretory]/workflow/data.
   * **[!UICONTROL Selecione os anexos de entrada usando]**: os anexos disponíveis no local são anexados ao formulário associado à tarefa. O caminho pode ser relativo à carga ou recuperar o anexo armazenado em uma variável de um documento. Um exemplo de caminho é [Payload_Diretory]/attachments/. Você pode especificar anexos colocados em relação à carga ou usar uma variável do tipo de documento (Lista de matriz > Documento) para especificar um anexo de entrada para o Formulário adaptável.

  <!-- 
    
    * **[!UICONTROL Choose input JSON]**: Select an input JSON file using a path that is relative to payload or stored in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list.

    * **[!UICONTROL Choose a custom prefill service]**: Select the prefill service to retrieve the data and prefill the Interactive Communication Web channel document or the Agent UI.  
    
    * **[!UICONTROL Use the prefill service of the interactive communication selected above]**: Use this option to use the prefill service of the Interactive Communication defined in the Use Interactive Communication drop-down list. 
    
    -->

   * **[!UICONTROL Mapeamento do Atributo de Solicitação]**: Use a seção Mapeamento do Atributo de Solicitação para definir o [nome e o valor do atributo de solicitação](work-with-form-data-model.md#bindargument). Recupere os detalhes da fonte de dados com base no nome e valor do atributo especificado na solicitação. Você pode definir um valor de atributo de solicitação usando um valor literal ou uma variável do tipo de dados String.

  <!--  
     
     The prefill service and request attribute mapping options are available only if you select Interactive Communication Agent UI or Interactive Communication Web Channel Document from the Type drop-down list. 
     
     -->

* **[!UICONTROL Informações enviadas]**: os seguintes campos listados abaixo servem como locais de saída para a tarefa:

   * **[!UICONTROL Salvar arquivo de dados de saída usando]**: salve o arquivo de dados (.json, .xml, .doc ou modelo de dados de formulário (FDM)). O arquivo de dados contém informações enviadas por meio do formulário associado. Você pode salvar o arquivo de dados de saída usando um caminho relativo à carga útil ou armazená-lo em uma variável do tipo de dados Documento, XML ou JSON. Por exemplo, [Payload_Diretory]/Workflow/data, onde os dados são um arquivo.
   * **[!UICONTROL Salvar anexos usando]**: salve os anexos de formulário fornecidos em uma tarefa. Você pode salvar os anexos usando um caminho relativo à carga ou armazená-lo em uma variável da lista de matriz do tipo de dados Documento.
   * **[!UICONTROL Salvar documento de registro usando]**: caminho para salvar um arquivo de documento de registro. Por exemplo, [Payload_Diretory]/DocumentofRecord/credit-card.pdf. Você pode salvar o documento de registro usando um caminho relativo à carga útil ou armazená-lo em uma variável do tipo de dados Documento. Se você selecionar a opção **[!UICONTROL Relativo à carga]**, o documento de registro não será gerado se o campo de caminho estiver vazio. Essa opção estará disponível somente se você selecionar Formulário adaptável na lista suspensa Tipo.

  <!-- 
    
    * **[!UICONTROL Save Web Channel data using]**: Save the Web Channel data file using a path that is relative to the payload or store it in a variable of Document, JSON, or Form Data Model (FDM) data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. c
    * **[!UICONTROL Save PDF document using]**: Save the PDF document using a path that is relative to the payload or store it in a variable of Document data type. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list.
    <!-- * **[!UICONTROL Save layout template using]**: Save the layout template using a path that is relative to the payload or store it in a variable of Document data type. The [layout template](layout-design-details.md) refers to an XDP file that you create using Forms Designer. This option is available only if you select Interactive Communication Agent UI from the Type drop-down list. 
    
    -->

* **[!UICONTROL Atribuído]** > **[!UICONTROL Opções de atribuição]**: especifique o método para atribuir a tarefa a um usuário. Você pode atribuir a tarefa dinamicamente a um usuário ou grupo usando o script Seletor de participante ou atribuir a tarefa a um usuário ou grupo específico da AEM.
* **[!UICONTROL Seletor de participantes]**: a opção estará disponível quando a opção **[!UICONTROL Dinamicamente para um usuário ou grupo]** estiver selecionada no campo Opções de atribuição. Você pode usar um ECMAScript ou um serviço para selecionar dinamicamente um usuário ou grupo. Para obter mais informações, consulte [Criação de uma etapa personalizada de Participante dinâmico do Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR&CID=RedirectAEMCommunityKautuk).

* **[!UICONTROL Participantes]**: o campo está disponível quando a opção **[!UICONTROL com.adobe.granite.workflow.core.process.RandomParticipantChooser]** é selecionada no campo **[!UICONTROL Seletor de Participantes]**. O campo permite selecionar usuários ou grupos para a opção RandomParticipantChooser.

* **[!UICONTROL Atribuído]**: o campo está disponível quando o **[!UICONTROL com.adobe.fd.workspace.step.service.VariableParticipantChooser]** está selecionado no campo **[!UICONTROL Seletor de Participante]**. O campo permite selecionar uma variável de tipo de dados String para definir o destinatário.

* **[!UICONTROL Argumentos]**: o campo está disponível quando um script diferente do script RandomParticipantChoose é selecionado no campo Seletor de Participantes. O campo permite fornecer uma lista de um argumento separado por vírgulas para o script selecionado no campo Seletor de participantes.

* **[!UICONTROL Usuário ou Grupo]**: a tarefa foi atribuída a um usuário ou grupo selecionado. A opção está disponível quando a opção **[!UICONTROL Para um usuário ou grupo específico]** é selecionada no campo **[!UICONTROL Opções de atribuição]**. O campo lista todos os usuários e grupos do grupo [!DNL workflow-users].\
  O menu suspenso **[!UICONTROL Usuário ou Grupo]** lista os usuários e grupos aos quais o usuário conectado tem acesso. A exibição do nome de usuário depende se você tem permissões de acesso no nó **[!UICONTROL usuários]** no repositório crx para esse usuário específico.

* **[!UICONTROL Enviar Email de Notificação]**: selecione esta opção para enviar notificações por email ao destinatário. Essas notificações são enviadas quando uma tarefa é atribuída a um usuário ou grupo. Você pode usar a opção **[!UICONTROL Endereço de email do destinatário]** para especificar o mecanismo para recuperar o endereço de email.

* **[!UICONTROL Endereço de email do destinatário]**: você pode armazenar um endereço de email em uma variável, usar um literal para especificar um endereço de email permanente ou usar o endereço de email padrão do destinatário especificado no perfil do destinatário. Você pode usar o literal ou uma variável para especificar o endereço de email de um grupo. A opção de variável é útil para recuperar e usar dinamicamente um endereço de email. A opção **[!UICONTROL Usar endereço de email padrão do destinatário]** é somente para um único destinatário. Nesse caso, o endereço de email armazenado no perfil de usuário designado é usado.

* **[!UICONTROL Modelo de email do HTML]**: selecione o modelo de email para o email de notificação. Para editar um modelo, modifique o arquivo localizado em /libs/fd/dashboard/templates/email/htmlEmailTemplate.txt no repositório crx.
* **[!UICONTROL Permitir delegação para]**: a Caixa de Entrada do AEM fornece uma opção ao usuário conectado para delegar o fluxo de trabalho atribuído a outro usuário. Você tem permissão para delegar no mesmo grupo ou para o usuário de workflow de outro grupo. Se a tarefa for atribuída a um único usuário e a opção **[!UICONTROL permitir delegação a membros do grupo do destinatário]** for selecionada, não será possível delegar a tarefa a outro usuário ou grupo.
* **[!UICONTROL Configurações de Compartilhamento]**: a Caixa de Entrada do AEM fornece opções para compartilhar uma única tarefa ou todas as tarefas da caixa de entrada com outro usuário:
   * Quando a opção **[!UICONTROL Permitir que o destinatário compartilhe explicitamente na caixa de entrada]** é selecionada, o usuário pode selecionar a tarefa na Caixa de Entrada do AEM e compartilhá-la com outro usuário do AEM.
   * Quando a opção **[!UICONTROL Permitir que o destinatário compartilhe através do compartilhamento da caixa de entrada]** estiver selecionada e os usuários compartilharem seus itens da Caixa de Entrada ou permitir que outros usuários acessem seus itens da Caixa de Entrada, somente as tarefas com a opção mencionada anteriormente habilitada serão compartilhadas com outros usuários.
   * Quando a opção **[!UICONTROL Permitir que o destinatário autorize usando as configurações &#39;Ausente&#39;]** está selecionada. O responsável pode habilitar a opção para delegar a tarefa a outros usuários junto com outras opções de Ausência Temporária. Quaisquer novas tarefas atribuídas ao usuário ausente do escritório são automaticamente delegadas (atribuídas) aos usuários mencionados nas configurações ausentes do escritório.

  Ele permite que outros usuários escolham as tarefas atribuídas enquanto estiver fora do escritório e não puder trabalhar nas tarefas atribuídas.

* **[!UICONTROL Ações]** > **[!UICONTROL Ações padrão]**: as ações Enviar, Salvar e Redefinir prontas para uso estão disponíveis. Todas as ações padrão são ativadas, por padrão.
* **[!UICONTROL Variável de rota]**: nome da variável de rota. A variável de rota captura as ações personalizadas que um usuário seleciona na Caixa de entrada do AEM.
* **[!UICONTROL Rotas]**: uma tarefa pode ramificar para rotas diferentes. Quando selecionado na Caixa de entrada do AEM, o roteiro retorna um valor e o fluxo de trabalho é ramificado com base no roteiro selecionado. Você pode armazenar rotas em uma variável de matriz de tipos de dados String ou selecionar **[!UICONTROL Literal]** para adicionar rotas manualmente.

* **[!UICONTROL Título da Rota]**: especifique o título da rota. Ele é exibido na Caixa de entrada do AEM.
* **[!UICONTROL Ícone Coral]**: especifique um atributo HTML de um ícone coral. A biblioteca Adobe CorelUI fornece um vasto conjunto de ícones de primeiro toque. Você pode escolher e usar um ícone para a rota. Ele é exibido junto com o título na Caixa de entrada do AEM. Se você armazenar as rotas em uma variável, elas usarão um ícone de coral &quot;Tags&quot; padrão.
* **[!UICONTROL Permitir que o destinatário adicione o comentário]**: selecione esta opção para habilitar comentários para a tarefa. Um signatário pode adicionar os comentários de dentro da Caixa de entrada do AEM no momento do envio da tarefa.
* **[!UICONTROL Salvar comentário na variável]**: salve o comentário em uma variável do tipo de dados String. Esta opção é exibida somente se você marcar a caixa de seleção **[!UICONTROL Permitir ao signatário adicionar comentário]**.

* **[!UICONTROL Permitir que o destinatário adicione anexos à tarefa]**: selecione esta opção para habilitar anexos para a tarefa. Um destinatário pode adicionar os anexos da Caixa de entrada do AEM no momento do envio da tarefa. Você também pode limitar o tamanho máximo **[!UICONTROL (Tamanho Máximo do Arquivo)]** de um anexo. O tamanho padrão é 2 MB.

* **[!UICONTROL Salvar anexos de saída da tarefa usando]**: especifique o local da pasta de anexos. Você pode salvar anexos de saída da tarefa usando um caminho relativo à carga útil ou em uma variável de uma matriz de tipos de dados de documento. Esta opção é exibida somente se você marcar a caixa de seleção **[!UICONTROL Permitir ao signatário adicionar anexos à tarefa]** e selecionar **[!UICONTROL Formulário adaptável]**, **[!UICONTROL Formulário adaptável somente leitura]** ou **[!UICONTROL Documento PDF não interativo]** na lista suspensa **[!UICONTROL Tipo]** na guia **[!UICONTROL Formulário/Documento]**.

* **[!UICONTROL Usar metadados personalizados]**: selecione esta opção para habilitar o campo de metadados personalizado. Os metadados personalizados são usados em modelos de email.
* **[!UICONTROL Metadados personalizados]**: selecione um metadado personalizado para os modelos de email. Os metadados personalizados estão disponíveis no repositório crx em apps/fd/dashboard/scripts/metadataScripts. O caminho especificado não existe no repositório crx. Um administrador cria o caminho antes de usá-lo. Você também pode usar um serviço para os metadados personalizados. Você também pode estender a interface `WorkitemUserMetadataService` para fornecer metadados personalizados.
* **[!UICONTROL Mostrar Dados das Etapas Anteriores]**: selecione essa opção para permitir que os atribuídos exibam os atribuídos anteriores, as ações já executadas na tarefa, os comentários adicionados à tarefa e o Documento de Registro da tarefa concluída, se disponível.
* **[!UICONTROL Mostrar dados das etapas subsequentes]**: selecione essa opção para permitir que o destinatário atual visualize a ação executada e os comentários adicionados à tarefa pelos atribuídos subsequentes. Ela também permite que o destinatário atual visualize um documento de registro da tarefa concluída, se disponível.
* **[!UICONTROL Visibilidade do tipo de dados]**: por padrão, um destinatário pode exibir um Documento de Registro, destinatários, ações realizadas e comentários adicionados por destinatários anteriores e subsequentes. Use a opção de visibilidade do tipo de dados para limitar o tipo de dados visível para os atribuídos.

>[!NOTE]
>
>As opções para salvar a etapa Atribuir tarefa como rascunho e recuperar o histórico da etapa Atribuir tarefa são desativadas ao configurar um modelo de fluxo de trabalho do AEM para armazenamento de dados externo. Além disso, na Caixa de entrada, a opção para salvar está desativada.

## Converter em etapa do PDF/A {#convert-pdfa}

O PDF/A é um formato de arquivo que permite preservar o conteúdo do documento a longo prazo, incorporando as fontes e descompactando o arquivo. Como resultado, um documento PDF/A geralmente é maior do que um documento PDF padrão. Você pode usar a etapa ***Converter em PDF/A*** em um fluxo de trabalho do AEM para converter documentos do PDF para o formato PDF/A.

A etapa Converter em PDF/A tem as seguintes propriedades:

**[!UICONTROL Documento de Entrada]**: o documento de entrada pode ser relativo à carga útil, ter um caminho absoluto, pode ser fornecido como uma carga útil ou armazenado em uma variável do tipo de dados Documento.

**[!UICONTROL Opções de Conversão]**: usando esta propriedade, as configurações para converter documentos do PDF em documentos do PDF/A são especificadas. Várias opções disponíveis nessa guia são:

* **[!UICONTROL Conformidade]**: especifica o padrão com o qual o documento PDF/A de saída deve estar em conformidade. Ela é compatível com diferentes padrões da PDF, como PDF/A-1b, PDF/A-2b ou PDF/A-3b.
* **[!UICONTROL Nível de Resultado]**: especifica o nível de resultado como PassFail, Summary ou Detailed para a saída de conversão.
* **[!UICONTROL Espaço de cor]**: especifica o espaço de cor predefinido como S_RGB, COATED_FOGRA27, JAPAN_COLOR_COATED ou SWOP, que pode ser usado para arquivos PDF/A de saída.
* **[!UICONTROL Conteúdo Opcional]**: permitir que objetos gráficos e/ou anotações específicos sejam visíveis no documento PDF/A de saída, somente quando um conjunto especificado de critérios for atendido.

**[!UICONTROL Documentos de saída]**: especifica o local para salvar o arquivo de saída. O arquivo de saída pode ser salvo em um local relativo à carga útil, substitui a carga útil, se a carga útil for um arquivo ou em uma variável do tipo de dados Documento.


## Etapa Enviar email {#send-email-step}

Use a etapa do email para enviar um email, por exemplo, um email com um Documento de Registro, um link de um Formulário Adaptável <!-- , link of an interactive communication--> ou um documento do PDF anexado. A etapa Enviar Email oferece suporte a [email do HTML](https://en.wikipedia.org/wiki/HTML_email). Os emails do HTML são responsivos e se adaptam ao cliente de email dos recipients e ao tamanho da tela. Você pode usar um modelo de email do HTML para definir a aparência, o esquema de cores e o comportamento do email.

A etapa de email usa o Day CQ Mail Service para enviar emails. Antes de usar a etapa de email, verifique se o serviço de email está configurado. Por padrão, o email suporta somente os protocolos HTTP e HTTPs. [Contate a equipe de suporte](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=pt-BR#sending-email) para habilitar as portas para enviar emails e habilitar o protocolo SMTP para o seu ambiente. A restrição ajuda a melhorar a segurança da plataforma.

A etapa de email tem as seguintes propriedades:

**[!UICONTROL Título]**: o título da etapa ajuda a identificar a etapa no editor de fluxo de trabalho.

**[!UICONTROL Descrição]**: a explicação é útil para outros desenvolvedores de processo quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

**[!UICONTROL Assunto do Email]**: o assunto pode ser recuperado de metadados de fluxo de trabalho, especificados manualmente ou recuperados do valor armazenado em uma variável. Selecione entre as seguintes opções:

* **[!UICONTROL Literal]** especifica manualmente um assunto.
* **[!UICONTROL Recuperar metadados de Fluxo de Trabalho]** - Recupere o assunto de uma propriedade de metadados.
* **[!UICONTROL Variável]** - Recupera o assunto do valor armazenado em uma variável do tipo de dados string.

**[!UICONTROL Modelo de email do HTML]**: modelo do HTML para o email. Você pode especificar variáveis em um template de email. A etapa Email extrai e exibe todas as variáveis incluídas em um modelo para entradas.

**[!UICONTROL Metadados do modelo de email]**: o valor das variáveis do modelo de email pode ser um valor especificado pelo usuário, o caminho de um ativo no autor ou no servidor de publicação, imagem ou uma propriedade de metadados de fluxo de trabalho.

* **[!UICONTROL Literal]**: use a opção quando você souber o valor exato a ser especificado. Por exemplo, [example@example.com](mailto:example@example.com).

* **[!UICONTROL Metadados do fluxo de trabalho]**: use a opção quando o valor a ser usado for salvo em uma propriedade de metadados do fluxo de trabalho. Depois de selecionar a opção, insira o nome da propriedade de metadados na caixa de texto vazia abaixo da opção Metadados do fluxo de trabalho. Por exemplo, emailAddress.

<!-- 

* **[!UICONTROL Asset URL]**: Use the option to embed a web link of an interactive communication to the email. After selecting the option, browse and choose the interactive communication to embed. The asset can reside on the author or the publish server. 

-->

* **[!UICONTROL Imagem]**: use a opção para incorporar uma imagem ao email. Depois de selecionar a opção, navegue e escolha a imagem. A opção de imagem está disponível somente para as marcas de imagem (&lt;img src=&quot;&#42;&quot;/>) disponíveis no modelo de email.

**[!UICONTROL Endereço de email do remetente/destinatário]**: selecione a opção **[!UICONTROL Literal]** para especificar manualmente um endereço de email ou selecione a opção **[!UICONTROL Recuperar metadados do fluxo de trabalho]** para recuperar o endereço de email de uma propriedade de metadados. Você também pode especificar uma lista de matrizes de propriedades de metadados para a opção **[!UICONTROL Recuperar dos metadados do fluxo de trabalho]**. Selecione a opção **[!UICONTROL Variável]** para recuperar o endereço de email do valor armazenado em uma variável do tipo de dados string.

* **[!UICONTROL Anexo de Arquivo]**: o ativo disponível no local especificado está anexado ao email. O caminho do ativo pode ser relativo à carga ou ao caminho absoluto. Um exemplo de caminho é [Payload_Diretory]/attachments/.

Selecione a opção **[!UICONTROL Variável]** para recuperar o anexo de arquivo armazenado em uma variável do tipo de dados Documento, XML ou JSON.

**[!UICONTROL Nome do arquivo]**: nome do arquivo de anexo de email. A Etapa Email altera o nome de arquivo original do anexo para o nome de arquivo especificado. O nome pode ser especificado manualmente ou recuperado de uma propriedade de metadados de fluxo de trabalho ou de uma variável. Use a opção **[!UICONTROL Literal]** quando você souber o valor exato a ser especificado. Use a opção **[!UICONTROL Variável]** para recuperar o nome do arquivo do valor armazenado em uma variável do tipo de dados string. Use a opção **[!UICONTROL Recuperar de Metadados de Fluxo de Trabalho]** quando o valor a ser usado for salvo em uma propriedade de metadados de fluxo de trabalho.

## Etapa Gerar documento de registro {#generate-document-of-record-step}

Quando um formulário é preenchido ou enviado, você pode manter um registro do formulário, impresso ou no formato do documento. Esse registro é chamado de Documento de registro (DoR). Você pode usar a etapa Gerar documento de registro para criar uma versão somente leitura ou interativa do PDF de um formulário adaptável. A versão do PDF contém informações preenchidas no formulário junto com o layout do Formulário adaptável.

A etapa Documento de registro tem as seguintes propriedades:

**[!UICONTROL Usar formulário adaptável]**: especifique o método para localizar o formulário adaptável de entrada. Você pode usar o Formulário adaptável enviado ao fluxo de trabalho, disponível em um caminho absoluto ou disponível em um caminho em uma variável. Você pode usar uma variável do tipo de dados String para especificar o caminho no campo **[!UICONTROL Selecionar variável para resolver]**.\
É possível associar várias Forms adaptáveis a um fluxo de trabalho. Como resultado, você pode especificar um Formulário adaptável no tempo de execução usando os métodos de entrada disponíveis.

**[!UICONTROL Caminho do formulário adaptável]**: especifique o caminho do formulário adaptável. O campo está disponível ao selecionar a opção **[!UICONTROL Disponível em um caminho absoluto]** do campo **[!UICONTROL Usar Formulário Adaptável]**.

**[!UICONTROL Selecione os dados de entrada usando]**: Caminho dos dados de entrada para o Formulário adaptável. Você pode manter os dados em um local relativo à carga, especificar um caminho absoluto dos dados ou recuperar dados armazenados em uma variável do tipo de dados Documento, JSON ou XML. Os dados de entrada são mesclados com o Formulário adaptável para criar um Documento de registro.

**[!UICONTROL Selecione o caminho do anexo de entrada usando]**: Caminho dos anexos. Esses anexos são incluídos no documento de registro. Você pode manter os anexos em um local relativo à carga, especificar um caminho absoluto dos anexos ou recuperar anexos armazenados em uma variável de matriz do tipo de dados Documento.

Se você especificar o caminho de uma pasta, por exemplo, anexos, todos os arquivos diretamente disponíveis na pasta serão anexados ao documento de registro. Se houver arquivos disponíveis nas pastas diretamente disponíveis no caminho de anexo especificado, os arquivos serão incluídos no Documento de registro como anexos. Se houver pastas em pastas diretamente disponíveis, elas serão ignoradas.

**[!UICONTROL Salvar documento de registro gerado usando as opções abaixo]**: especifique o local para manter um documento de registro. Você pode optar por substituir a pasta de carga útil, colocar o Documento de registro em um local no diretório da carga útil ou armazenar o Documento de registro em uma variável do tipo de dados Documento.

**[!UICONTROL Localidade]**: especifique o idioma do documento de registro. Selecione **[!UICONTROL Literal]** para selecionar a localidade em uma lista suspensa ou selecione **[!UICONTROL Variável]** para recuperar a localidade do valor armazenado em uma variável do tipo de dados string. Defina o código do local ao armazenar o valor do local em uma variável. Por exemplo, especifique **en_US** para inglês e **fr_FR** para francês.

## Chamar etapa DDX {#invokeddx}

O Document Description XML (DDX) é uma linguagem de marcação declarativa cujos elementos representam os blocos fundamentais de documentos. Esses blocos fundamentais incluem documentos PDF e XDP, além de outros elementos, como comentários, marcadores e texto estilizado. O DDX define um conjunto de operações, que podem ser aplicadas em um ou mais documentos de entrada para gerar um ou mais documentos de saída. Um único DDX pode ser usado com uma variedade de documentos de origem. Você pode usar a ***etapa Invocar DDX*** em um fluxo de trabalho do AEM para executar várias operações, como Montar, Desmontar documentos, Criar e modificar o Acrobat e o XFA Forms, entre outras, descritas na [documentação de Referência do DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf).

A etapa Chamar DDX tem as seguintes propriedades:

**[!UICONTROL Documentos de Entrada]**: usados para definir propriedades de um documento de entrada. Várias opções disponíveis nessa guia são:

* **[!UICONTROL Especificar DDX Usando]**: especifica o documento de entrada relativo à carga útil, tem um caminho absoluto, pode ser fornecido como carga útil ou armazenado em uma variável do tipo de dados Documento.
* **[!UICONTROL Criar Mapa a partir da Carga]**: adicione todos os documentos na pasta da carga ao Mapa do Documento de Entrada para a API de invocação no Assembler. O nome do nó de cada documento é usado como uma chave no mapa.
* **[!UICONTROL Mapa do Documento de Entrada]**: A opção é usada para adicionar várias entradas usando o botão **[!UICONTROL ADICIONAR]**. Cada entrada representa a chave do documento no mapa e a origem do documento.

**[!UICONTROL Opções de Ambiente]**: esta opção é usada para definir as configurações de processamento para invocar API. Várias opções disponíveis nessa guia são:

* **[!UICONTROL Validar Somente]**: verifica a validade do documento DDX de entrada.
* **[!UICONTROL Falha ao errar]**: valor booleano para indicar se o serviço de API de invocação falha, se houver ou não um erro. Por padrão, seu valor é definido como Falso.
* **[!UICONTROL Primeiro número de Bates]**: especifica o número, que é de autoincrementação. Esse número de autoincrementação é exibido em cada página consecutiva automaticamente.
* **[!UICONTROL Estilo padrão]**: define o estilo padrão para o arquivo de saída.

>[!NOTE]
>
>As opções de ambiente são mantidas em sincronia com as APIs HTTP.

**[!UICONTROL Documentos de saída]**: especifica o local para salvar o arquivo de saída. Várias opções disponíveis nessa guia são:

* **[!UICONTROL Salvar Saída na Carga]**: salva os documentos de saída na pasta da carga útil ou substitui a carga útil; caso a carga seja um arquivo.
* **[!UICONTROL Mapa do Documento de Saída]**: especifica o local para salvar explicitamente cada arquivo de documento, adicionando uma entrada por documento. Cada entrada representa o documento e o local onde ele deve ser salvo. Se houver vários documentos de saída, essa opção será usada.

## Chamar a etapa de serviço do Modelo de dados de formulário (FDM) {#invoke-form-data-model-service-step}

Você pode usar a [[!DNL AEM Forms] Integração de Dados](data-integration.md) para configurar e conectar-se a fontes de dados diferentes. Essas fontes de dados podem ser um serviço Web, um serviço REST, um serviço OData e uma solução de CRM. A Integração de Dados do [!DNL AEM Forms] permite criar um Modelo de Dados de Formulário (FDM) que abrange vários serviços para executar operações de recuperação, adição e atualização de dados no banco de dados configurado. Você pode usar a **[!UICONTROL etapa Invocar Serviço de Modelo de Dados]** para selecionar um Modelo de Dados de Formulário (FDM) e usar os serviços do FDM para recuperar, atualizar ou adicionar dados a diferentes fontes de dados.

Para explicar entradas para campos da etapa, a seguinte tabela de banco de dados e arquivo JSON são usados como exemplo:

**[!UICONTROL Tabela CustomerDetails de exemplo]**

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

A etapa Serviço Chamar modelo de dados de formulário (FDM) tem os campos listados abaixo para facilitar as operações do Modelo de dados de formulário (FDM):

* **[!UICONTROL Título]**: título da etapa. Ajuda a identificar as etapas no editor de workflow.
* **[!UICONTROL Descrição]**: explicação útil para outros desenvolvedores de processo quando você está trabalhando em um ambiente de desenvolvimento compartilhado.

* **[!UICONTROL Caminho do modelo de dados de formulário]**: procure e selecione um modelo de dados de formulário (FDM) presente no servidor.

* **[!UICONTROL Erros e Validações]**: a opção permite capturar mensagens de erro e especificar opções de validação para dados recuperados e enviados para fontes de dados. Com essas alterações, você pode garantir que os dados transmitidos para a etapa de serviço Chamar modelo de dados de formulário (FDM) sigam as restrições de dados definidas pela fonte de dados. Para obter mais detalhes, consulte [Validação automatizada dos dados de entrada](work-with-form-data-model.md#automated-validation-of-input-data)

* **[!UICONTROL Nível de validação]**: há três categorias de validações: Básica, Completa e DESATIVADA:

   * Total: todas as restrições são validadas.
   * Básico: somente restrições obrigatórias e anuláveis
   * DESATIVADO: Não ocorre validação.

* **[!UICONTROL Encerrar Fluxo de Trabalho na Falha]**: quando uma restrição não é validada, o fluxo de trabalho é interrompido.

* **[!UICONTROL Armazenar código de erro na variável]**: você pode armazenar um código de erro em uma [variável de tipo String](variable-in-aem-workflows.md).

* **[!UICONTROL Armazenar Mensagem de Erro na Variável]**: Você pode armazenar uma mensagem de erro em uma [variável de tipo de cadeia de caracteres](variable-in-aem-workflows.md).

* **[!UICONTROL Armazenar detalhes do erro na Variável]**: você pode armazenar detalhes do erro em uma [variável de tipo JSON](variable-in-aem-workflows.md).

* **[!UICONTROL Serviço]**: lista dos serviços que o Modelo de Dados de Formulário (FDM) selecionado fornece.
* **[!UICONTROL Entrada para serviços]** > **[!UICONTROL Forneça dados de entrada usando metadados literais, variáveis ou de fluxo de trabalho e um arquivo JSON]**: um serviço pode ter vários argumentos. Selecione a opção para obter o valor dos argumentos de serviço de uma propriedade de metadados do fluxo de trabalho, um objeto JSON, uma variável ou insira o valor diretamente na caixa de texto fornecida:

   * **[!UICONTROL Literal]**: use a opção quando você souber o valor exato a ser especificado. Por exemplo, srose@we.info.
   * **[!UICONTROL Variável]**: use a opção para recuperar o valor armazenado em uma variável.
   * **[!UICONTROL Recuperar dos Metadados de Fluxo de Trabalho]**: use a opção quando o valor a ser usado for salvo em uma propriedade de metadados de fluxo de trabalho. Por exemplo, emailAddress.

   * **[!UICONTROL Relativo à carga]**: use a opção para recuperar o anexo de arquivo salvo em um caminho relativo à carga. Selecione a opção e especifique o nome da pasta que inclui o anexo de arquivo ou especifique o nome do anexo de arquivo na caixa de texto.

     >[!NOTE]
     >
     > A etapa de fluxo de trabalho **Invocar Modelo de Dados de Formulário** dá suporte a metadados do fluxo de trabalho para matrizes de anexo codificadas em Base64 em [Modelos de Dados de Formulário baseados em Lista do SharePoint](/help/forms/connect-forms-to-sharepoint-list.md) e permite que os fluxos de trabalho transmitam, armazenem e recuperem metadados como nome de arquivo, tipo MIME ou propriedades personalizadas para os anexos.
     > ![Anexos da Lista de SPs](/help/edge/docs/forms/assets/workflow-sp-list.png)
     >
     > A pasta Relative to Payload inclui um anexo de arquivo no local `attachment`, especifique `attachment` na caixa de texto depois de selecionar a opção **[!UICONTROL Relative to Payload]**.

   * **[!UICONTROL Anotação JSON Dot]**: use a opção quando o valor a ser usado estiver em um arquivo JSON. Por exemplo, insurance.customerDetails.emailAddress. A opção Anotação JSON Dot estará disponível somente se Mapear campos de entrada da opção JSON de entrada estiver selecionada.
   * **[!UICONTROL Mapear campos de entrada do JSON de entrada]**: especifique o caminho de um arquivo JSON para obter o valor de entrada de alguns argumentos de serviço do arquivo JSON. O caminho do arquivo JSON pode ser relativo à carga, um caminho absoluto ou você pode selecionar um documento JSON de entrada usando uma variável do tipo JSON ou Form Data Model (FDM).

* **[!UICONTROL Entrada para serviços]** > **[!UICONTROL Forneça dados de entrada usando variável ou um arquivo JSON]**: selecione a opção para obter valores para todos os argumentos de um arquivo JSON salvo em um caminho absoluto, em um caminho relativo à carga ou em uma variável.
* **[!UICONTROL Selecione o documento JSON de entrada usando]**: o arquivo JSON que contém valores para todos os argumentos de serviço. O caminho do arquivo JSON pode ser **[!UICONTROL relativo à carga]** ou um **[!UICONTROL caminho absoluto]**. Você também pode recuperar o documento JSON de entrada usando uma variável do tipo de dados JSON ou Form Data Model (FDM).

* **[!UICONTROL Anotação JSON Dot]**: Deixe o campo em branco para usar todos os objetos do arquivo JSON especificado como entrada para argumentos de serviço. Para ler um objeto JSON específico do arquivo JSON especificado como entrada para argumentos de serviço, especifique a notação de pontos para o objeto JSON. Por exemplo, se você tiver um JSON semelhante ao listado no início da seção, especifique insurance.customerDetails para fornecer todos os detalhes de um cliente como entrada para o serviço.
* **[!UICONTROL Saída do serviço]** > **[!UICONTROL Mapear e gravar valores de saída na variável ou nos metadados]**: selecione a opção para salvar os valores de saída como propriedades do nó de metadados da instância do fluxo de trabalho no repositório crx. Especifique o nome da propriedade de metadados e selecione o atributo de saída de serviço correspondente a ser mapeado com a propriedade de metadados, por exemplo, mapeie o phone_number retornado pelo serviço de saída com a propriedade phone_number dos metadados do fluxo de trabalho. Da mesma forma, você pode armazenar a saída em uma variável do tipo de dados Long. Ao selecionar uma propriedade para a opção **[!UICONTROL Atributo de saída de serviço a ser mapeado]**, somente as variáveis capazes de armazenar dados da propriedade selecionada serão preenchidas para a opção **[!UICONTROL Salvar a saída em]**.

* **[!UICONTROL Saída do serviço]** > **[!UICONTROL Salvar saída na variável ou em um arquivo JSON]**: selecione a opção para salvar os valores de saída em um arquivo JSON em um caminho absoluto, em um caminho relativo à carga ou em uma variável.
* **[!UICONTROL Salvar documento JSON de saída usando as opções abaixo]**: Salve o arquivo JSON de saída. O caminho do arquivo JSON de saída pode ser relativo à carga útil ou a um caminho absoluto. Você também pode salvar o arquivo JSON de saída usando uma variável do tipo de dados JSON ou Form Data Model (FDM).



## Etapa Assinar documento {#sign-document-step}

A etapa Assinar Documento permite que você use o [!DNL Adobe Sign] para assinar documentos. Quando você usa a etapa do fluxo de trabalho [!DNL Adobe Sign] para assinar um formulário adaptável, o formulário pode ser passado entre os destinatários um após o outro ou pode ser enviado para todos os destinatários simultaneamente, dependendo da configuração da etapa do fluxo de trabalho. O Adaptive Forms habilitado para [!DNL Adobe Sign] é enviado ao Experience Manager Forms Server somente depois que todos os destinatários concluírem o processo de assinatura.

Por padrão, o serviço Agendador do [!DNL Adobe Sign] verifica (pesquisa) a resposta do recipient a cada 24 horas. Você pode [alterar o intervalo padrão do seu ambiente](adobe-sign-integration-adaptive-forms.md#for-aem-workflows-only-configure-dnl-adobe-acrobat-sign-scheduler-to-sync-the-signing-status-configure-adobe-sign-scheduler-to-sync-the-signing-status).

A etapa Assinar documento tem as seguintes propriedades:

* **[!UICONTROL Nome do Contrato]**: especifique o título do contrato. O nome do contrato torna-se parte do assunto e do corpo do texto do email enviado aos signatários. Você pode armazenar o nome em uma variável do tipo de dados String ou selecionar **[!UICONTROL Literal]** para adicionar o nome manualmente.

* **[!UICONTROL Localidade]**: especifique o idioma para as opções de email e verificação. Você pode armazenar a localidade em uma variável do tipo de dados String ou selecionar **[!UICONTROL Literal]** para escolher a localidade na lista de opções disponíveis. Você deve definir o código do local ao armazenar o valor do local em uma variável. Por exemplo, especifique **[!UICONTROL en_US]** para inglês e **[!UICONTROL fr_FR]** para francês.

* **[!UICONTROL Configuração da nuvem do Adobe Sign]**: escolha uma configuração da nuvem [!DNL Adobe Sign]. Se você não tiver configurado o [!DNL Adobe Sign] para [!DNL AEM Forms], consulte [Integrar o Adobe Sign com [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

* **[!UICONTROL Selecione o Documento a ser assinado usando]**: você pode escolher um documento de um local relativo à carga útil, usar a carga útil como o documento, especificar um caminho absoluto do documento ou recuperar o documento armazenado em uma variável do tipo de dados Documento.
* **[!UICONTROL Dias até o prazo]**: um documento está marcado como vencido (ultrapassou o prazo) depois que não há nenhuma atividade na tarefa para o número de dias especificado no campo **[!UICONTROL Dias até o prazo]**. O número de dias é contado depois que a documentação é atribuída a um usuário para assinatura.
* **[!UICONTROL Frequência de Email de Lembrete]**: você pode enviar um email de lembrete em um intervalo diário ou semanal. A semana é contada a partir do dia em que a documentação é atribuída a um usuário para assinatura.
* **[!UICONTROL Processo de assinatura]**: você pode optar por assinar um documento em ordem sequencial ou paralela. Em ordem sequencial, um signatário recebe o documento de cada vez para assinar. Depois que o primeiro signatário terminar de assinar o documento, ele será enviado ao segundo signatário e assim por diante. Em ordem paralela, vários signatários podem assinar um documento de cada vez.
* **[!UICONTROL URL de redirecionamento]**: especifique uma URL de redirecionamento. Depois que o documento for assinado, você poderá redirecionar o destinatário para um URL. Normalmente, este URL contém uma mensagem de agradecimento ou mais instruções.
* **[!UICONTROL Estágio do fluxo de trabalho]**: um fluxo de trabalho pode ter vários estágios. Esses estágios são exibidos na Caixa de entrada do AEM. Você pode definir esses estágios nas propriedades do modelo ( **[!UICONTROL Sidekick]** > **[!UICONTROL Página]** > **[!UICONTROL Propriedades da Página]** > **[!UICONTROL Estágios]**).
* **[!UICONTROL Selecionar Destinatários]**: especifique o método para escolher os destinatários do documento. Você pode atribuir o fluxo de trabalho de maneira dinâmica a um usuário ou grupo ou adicionar manualmente os detalhes de um recipient. Ao selecionar Manually na lista suspensa, você adiciona detalhes do recipient, como email, função e método de autenticação.

  >[!NOTE]
  >
  >* Na seção Função, você pode especificar a função do destinatário como Signatário, Aprovador, Aceitador, Destinatário certificado, Preenchedor de formulário e Delegador.
  >* Se você selecionar Delegator na opção Role, o Delegator poderá atribuir a tarefa de assinatura a outro recipient.
  >* Se você tiver configurado um método de autenticação para [!DNL Adobe Sign], com base na sua configuração, selecione um método de autenticação, como autenticação com base no Telefone, autenticação com base na Identidade Social, autenticação com base no Conhecimento, autenticação com base na Identidade do Governo.

* **[!UICONTROL Script ou serviço para selecionar destinatários]**: a opção estará disponível somente se você selecionar a opção Dinamicamente no campo Selecionar destinatários. Você pode especificar um ECMAScript ou um serviço para escolher assinantes e opções de verificação para um documento.
* **[!UICONTROL Detalhes do destinatário]**: a opção só estará disponível se a opção Manually estiver selecionada no campo Select Recipients. Especifique um endereço de email e escolha um mecanismo de verificação opcional. Antes de selecionar um mecanismo de verificação de duas etapas, verifique se a opção de verificação correspondente está habilitada para a conta [!DNL Adobe Sign] configurada. Você pode usar uma variável do tipo de dados String para definir valores para os campos Email, Código do país e Número de telefone. Os campos Código do país e Número de telefone serão exibidos somente se você selecionar Verificação de telefone na lista suspensa de verificação de duas etapas.
* **[!UICONTROL Documento assinado]**: você pode salvar o status do documento assinado na variável. Para adicionar uma trilha de auditoria de assinatura eletrônica para maior segurança e legalidade ao Documento assinado, você pode Incluir o Relatório de auditoria. Você pode salvar o Documento assinado usando a pasta Variável ou Carga.

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

* **[!UICONTROL Selecionar arquivo de modelo usando]**: especifique o caminho do arquivo de modelo. Você pode selecionar o arquivo de modelo usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Payload_Diretory]/Workflow/data.xml. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo. Além disso, você também pode aceitar a carga como o arquivo de dados de entrada.

* **[!UICONTROL Selecionar documento de dados usando]**: especifique o caminho de um arquivo de dados de entrada. Você pode selecionar o arquivo de dados de entrada usando o caminho relativo à carga útil, salvo em um caminho absoluto ou usando uma variável do tipo de dados Documento. Por exemplo, [Payload_Diretory]/Workflow/data.xml. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo.

* **[!UICONTROL Formato da Impressora]**: um valor de Formato de Impressão que especifica a linguagem de descrição da página a ser usada, quando um arquivo XDC não for fornecido, para gerar o fluxo de saída. Se você fornecer um valor literal, selecione um destes valores:

   * **[!UICONTROL PCL de cor]**: use a opção para especificar um arquivo XDC para PCL.
   * **[!UICONTROL PostScript genérico]**: use a opção para especificar um arquivo XDC genérico para o PostScript.
   * **[!UICONTROL ZPL 300 DPI]**: use ZPL 300 DPI. O zpl300.xdc é usado.
   * **[!UICONTROL ZPL 600 DPI]**: usar ZPL 600 DPI. O arquivo zpl600.xdc é usado.
   * **[!UICONTROL IPL 300 DPI]**: usar IPL 300 DPI. O ipl300.xdc é usado.
   * **[!UICONTROL IPL 400 DPI]**: usar IPL 400 DPI. O arquivo ipl400.xdc é usado.
   * **[!UICONTROL TPCL 600 DPI]**: Use TPCL 600 DPI. O arquivo tpcl600.xdc é usado.
   * **[!UICONTROL PostScript Plain]**: use a opção para especificar um arquivo XDC de texto simples para o PostScript.
   * **[!UICONTROL DPL300DPI]**: use DPL 300 DPI. A dpl300.xdc é usada.
   * **[!UICONTROL DPL400DPI]**: usar DPL 400 DPI. A dpl400.xdc é usada.
   * **[!UICONTROL DPL600DPI]**: usar DPL 600 DPI. A dpl600.xdc é usada.
   * **[!UICONTROL HP_PCL_5e]**: use a opção para suportar vários dispositivos Canon.


**[!UICONTROL Propriedades de Saída]**

* **[!UICONTROL Salvar documento de saída usando]**: especifique o local para salvar o arquivo de saída. Você pode salvar o arquivo de saída em um local relativo à carga útil, em uma variável ou especificar um local absoluto para salvar o arquivo de saída. Se o caminho não existir no repositório crx, um administrador poderá criar o caminho antes de usá-lo.

**[!UICONTROL Propriedades Avançadas]**

* **[!UICONTROL Selecione o local da Raiz de Conteúdo usando]**: a raiz de conteúdo é um valor de cadeia de caracteres que especifica o URI, a referência absoluta ou o local no repositório para recuperar ativos relativos usados pelo design do formulário. Por exemplo, se o design do formulário referenciar uma imagem relativamente, como `../myImage.gif`, `myImage.gif` deve estar em `repository://`. O valor padrão é `repository://`, que aponta para o nível raiz do repositório.

  Quando você seleciona um ativo do aplicativo, o caminho do URI da raiz do conteúdo deve ter a estrutura correta. Por exemplo, se um formulário for retirado de um aplicativo chamado SampleApp e for colocado em `SampleApp/1.0/forms/Test.xdp`, o URI da Raiz de Conteúdo deverá ser especificado como `repository://administrator@password/Applications/SampleApp/1.0/forms/` ou `repository:/Applications/SampleApp/1.0/forms/` (quando a autoridade for nula). Quando o URI da raiz do conteúdo é especificado dessa maneira, os caminhos de todos os ativos referenciados no formulário são resolvidos em relação a esse URI.

* **[!UICONTROL Selecionar arquivo XCI usando]**: os arquivos XCI são usados para descrever fontes e outras propriedades usadas para elementos de design de formulário. Você pode manter um arquivo XCI relativo à carga útil, em um caminho absoluto ou usando uma variável do tipo de dados Documento.

* **[!UICONTROL Localidade]**: especifica a linguagem usada para gerar o documento PDF. Se você fornecer um valor literal, selecione um idioma na lista ou selecione um destes valores:
   * **[!UICONTROL Para usar o padrão do servidor]**:
(Padrão) Use a configuração de Local definida no Servidor [!DNL AEM Forms]. A configuração Local é definida usando o Console de administração. (Consulte a [Ajuda do Designer](https://helpx.adobe.com/content/dam/help/pt-br/experience-manager/6-5/forms/pdf/using-designer.pdf).)

   * **[!UICONTROL Para usar o valor personalizado]**:
Digite o código de localidade na caixa literal ou selecione uma variável de cadeia de caracteres que contenha o código de localidade. Para obter uma lista completa de códigos de localidade compatíveis, consulte https://docs.oracle.com/javase/1.5.0/docs/guide/intl/locale.doc.html.

* **[!UICONTROL Cópias]**: um valor inteiro que especifica o número de cópias a serem geradas para a saída. O valor padrão é 1.

* **[!UICONTROL Impressão frente e verso]**: um valor de Paginação que especifica se deve ser usada impressão frente e verso ou frente e verso. As impressoras que suportam PostScript e PCL usam este valor. Se você fornecer um valor literal, selecione um destes valores:
   * **[!UICONTROL Edge Longo Duplex]**: usar impressão frente e verso e impressão com paginação de borda longa.
   * **[!UICONTROL Edge curto duplex]**: use impressão frente e verso e impressão usando paginação de borda curta.
   * **[!UICONTROL Simplex]**: usar impressão em frente e verso.

## Etapa Gerar saída do PDF não interativa   {#generatePDFdocuments}

1. Arraste o workflow Gerar saída do PDF não interativa para a guia Forms Workflow no Sidekick.
1. Clique duas vezes na etapa de fluxo de trabalho adicionada para editar o componente.
1. Na caixa de diálogo Editar componente, configure documentos de entrada, documentos de saída e parâmetros adicionais e clique em **[!UICONTROL OK]**.

### Documentos de entrada {#input-documents-3}

* **Arquivo de modelo**: especifica o local do modelo XDP. É um campo obrigatório.

* **Documento de Dados**: especifica o local do xml de dados que deve ser mesclado com o modelo.

### Documento de saída {#output-document}

**Documento de saída**: especifica o nome do formulário PDF gerado.

### Parâmetros adicionais {#additional-parameters-1}

* **Raiz de Conteúdo**: especifica o caminho para a pasta no repositório onde os fragmentos ou imagens usados no modelo XDP de entrada são armazenados.
* **Localidade**: especifica a localidade padrão para o formulário PDF gerado.
* **Versão do Acrobat**: especifica a versão do Acrobat de destino para o formulário do PDF gerado.
* **PDF linearizada**: especifica se o PDF gerado deve ser otimizado para exibição na Web.
* **PDF Marcado**: especifica se o PDF gerado deve ficar acessível.
* **Documento XCI**: especifica o caminho para o arquivo XCI.

## Consulte também {#see-also}

* [Variáveis em fluxos de trabalho do AEM centrados no Forms](/help/forms/variable-in-aem-workflows.md)
* [Definir configuração de Ausência Temporária](/help/forms/configure-out-of-office-settings.md)

<!--

>[!MORELIKETHIS]
>
>* [Forms-centric workflow on OSGi](/help/forms/aem-forms-workflow.md)
>* [Use AEM translation workflow to localize Adaptive Forms and Document of Record](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms.md)

-->