---
title: Como configurar uma ação enviar para um formulário adaptável?
description: Um Formulário adaptável fornece várias Ações de envio. Uma Ação de envio define como um Formulário adaptável é processado após o envio. Você pode usar as Ações de envio integradas ou criar as suas próprias ações.
feature: Adaptive Forms, Foundation Components
exl-id: a4ebedeb-920a-4ed4-98b3-2c4aad8e5f78
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '3914'
ht-degree: 2%

---

# Ação de envio do formulário adaptável {#configuring-the-submit-action}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service | Este artigo |

**Aplica-se a**: ✔️ componentes de base do formulário adaptável. [Componentes principais do formulário adaptável](/help/forms/configure-submit-actions-core-components.md). A Adobe recomenda usar os Componentes principais para [adicionar o Adaptive Forms a uma Página do AEM Sites](create-or-add-an-adaptive-form-to-aem-sites-page.md) ou para [criar o Adaptive Forms](creating-adaptive-form-core-components.md) independente.

Uma Ação de Envio é acionada quando um usuário clica no botão **[!UICONTROL Enviar]** em um Formulário adaptável. O Forms as a Cloud Service fornece as seguintes ações de envio prontas para uso.

* [Enviar para endpoint REST](#submit-to-rest-endpoint)
* [Enviar e-mail](#send-email)
* [Enviar usando o Modo de dados de formulário (FDM)l](#submit-using-form-data-model)
* [Chamar um fluxo de trabalho de AEM](#invoke-an-aem-workflow)
* [Enviar para o SharePoint](#submit-to-sharedrive)
* [Enviar para o OneDrive](#submit-to-onedrive)
* [Enviar para o Armazenamento de blob do Azure](#azure-blob-storage)
* [Enviar para o Power Automate](#microsoft-power-automate)
* [Enviar para o Workfront Fusion](#workfront-fusion)

Você também pode [estender as Ações de Envio padrão](custom-submit-action-form.md) para criar sua própria Ação de Envio.

Você pode configurar uma Ação de envio na seção **[!UICONTROL Envio]** das propriedades do Contêiner de formulário adaptável, na barra lateral.

![Configurar Ação de Envio](assets/submission.png)


<!-- [!NOTE]
>
>Send PDF via Email Submit Action is applicable only to Adaptive Forms that use XFA template as form model. 

>[!NOTE]
>
>Ensure that the [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>exists. The directory is required to temporarily store attachments. If the directory does not exist, create it. -->

<!--

>[!CAUTION]
>
>If you  [prefill](prepopulate-adaptive-form-fields.md) a form template,  a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema , form template, or form data model) that is data does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost. 

>[!CAUTION]
>
>If you [prefill](prepopulate-adaptive-form-fields.md) a form template, a Form Data Model or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema, or form data model) that does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost.
-->

## Enviar para endpoint REST {#submit-to-rest-endpoint}

Use a ação **[!UICONTROL Enviar para o Ponto de Extremidade REST]** para postar os dados enviados em uma URL restante. A URL pode ser de um servidor interno (o servidor no qual o formulário é renderizado) ou externo.

Para publicar dados em um servidor interno, forneça o caminho do recurso. Os dados são publicados no caminho do recurso. Por exemplo, /content/restEndPoint. Para essas solicitações de publicação, as informações de autenticação da solicitação de envio são usadas.

Para publicar dados em um servidor externo, forneça um URL. O formato da URL é `https://host:port/path_to_rest_end_point`. Configure o caminho para lidar com a solicitação POST de forma anônima.

![Mapeamento para valores de campo passados como parâmetros da Página de Agradecimento](assets/post-enabled-actionconfig.png)

No exemplo acima, as informações inseridas pelo usuário em `textbox` são capturadas usando o parâmetro `param1`. A sintaxe para publicar dados capturados usando `param1` é:

`String data=request.getParameter("param1");`

Da mesma forma, os parâmetros que você usa para lançar dados XML e anexos são `dataXml` e `attachments`.

Por exemplo, você usa esses dois parâmetros no script para analisar dados para um ponto final rest. Você usa a seguinte sintaxe para armazenar e analisar os dados:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

Neste exemplo, `data` armazena os dados XML e `att` armazena os dados de anexo.

A Ação de Envio **[!UICONTROL Enviar para o ponto de extremidade REST]** envia os dados preenchidos no formulário para uma página de confirmação configurada como parte da solicitação HTTP GET. Você pode adicionar o nome dos campos a serem solicitados. O formato da solicitação é:

`{fieldName}={request parameter name}`

Como mostrado na imagem abaixo, `param1` e `param2` são passados como parâmetros com valores copiados dos campos **caixa de texto** e **caixa numérica** para a próxima ação.

![Configurando Ação De Envio De Ponto De Extremidade Rest](assets/action-config.png)

Você também pode **[!UICONTROL Habilitar a solicitação POST]** e fornecer uma URL para publicar a solicitação. Para enviar dados ao servidor AEM que hospeda o formulário, use um caminho relativo correspondente ao caminho raiz do servidor AEM. Por exemplo, `/content/forms/af/SampleForm.html`. Para enviar dados para qualquer outro servidor, use o caminho absoluto.

>[!NOTE]
>
>Para passar os campos como parâmetros em um URL REST, todos os campos devem ter nomes de elemento diferentes, mesmo se os campos forem colocados em painéis diferentes.

## Enviar e-mail {#send-email}

Você pode usar a Ação Enviar **[!UICONTROL Email]** para enviar um email para um ou mais destinatários após o envio bem-sucedido do formulário. O email gerado pode conter dados de formulário em um formato predefinido. Por exemplo, no modelo a seguir, o nome do cliente, o endereço de entrega, o nome do estado e o CEP são recuperados dos dados de formulário enviados.

    &quot;
    
    Olá, ${customer_Name},
    
    Os itens a seguir estão definidos como seu endereço de entrega padrão:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Atenciosamente,
    WKND
    
    &quot;

>[!NOTE]
>
> * Todos os campos de formulário devem ter nomes de elementos diferentes, mesmo que os campos sejam colocados em painéis diferentes de um formulário adaptável.
> * O AEM as a Cloud Service exige que o email de saída seja criptografado. Por padrão, o email de saída é desativado. Para ativá-lo, envie um tíquete de suporte para [Solicitando Acesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).

Também é possível incluir anexos e um Documento de registro (DoR) no email. Para habilitar a opção **[!UICONTROL Anexar documento de registro]**, configure o formulário adaptável para gerar um Documento de registro (DoR). Você pode ativar a opção para gerar um Documento de registro a partir das propriedades do Formulário adaptável.



<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->

## Enviar usando o Modelo de dados de formulário (FDM) {#submit-using-form-data-model}

A Ação de Envio **[!UICONTROL Enviar usando o Modelo de Dados de Formulário]** grava dados de Formulário adaptável enviados para o objeto de modelo de dados especificado em um Modelo de Dados de Formulário (FDM) para sua fonte de dados. Ao configurar a Ação Submeter, você pode escolher um objeto de modelo de dados cujos dados submetidos você deseja gravar na origem de dados.

Além disso, você pode enviar um anexo de formulário usando um Modelo de dados de formulário (FDM) e um Documento de registro (DoR) para a fonte de dados. Para obter informações sobre o modelo de dados de formulário (FDM), consulte [[!DNL AEM Forms] Integração de Dados](data-integration.md).

<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## Chamar um fluxo de trabalho de AEM {#invoke-an-aem-workflow}

A Ação de Envio **[!UICONTROL Chamar um Fluxo de Trabalho de AEM]** associa um Formulário Adaptável a um [Fluxo de Trabalho de AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). Quando um formulário é enviado, o fluxo de trabalho associado é iniciado automaticamente na instância do Autor. Você pode salvar o arquivo de dados, os anexos e o Documento de registro no local da carga útil do fluxo de trabalho ou em uma variável. Se o workflow estiver marcado para armazenamento de dados externo e configurado para um armazenamento de dados externo, então somente a opção de variável estará disponível. É possível selecionar na lista de variáveis disponíveis para o modelo de fluxo de trabalho. Se o workflow estiver marcado para armazenamento de dados externo em um estágio posterior e não no momento da criação do workflow, verifique se as configurações de variável necessárias estão em vigor.

A ação enviar coloca o seguinte no local da carga do fluxo de trabalho, ou a variável se o fluxo de trabalho estiver marcado para armazenamento de dados externo:

* **Arquivo de dados**: contém dados enviados para o Formulário adaptável. Você pode usar a opção **[!UICONTROL Caminho do Arquivo de Dados]** para especificar o nome do arquivo e o caminho do arquivo relativo à carga. Por exemplo, o caminho `/addresschange/data.xml` cria uma pasta chamada `addresschange` e a coloca em relação à carga. Você também pode especificar apenas `data.xml` para enviar apenas dados enviados sem criar uma hierarquia de pastas. Se o workflow estiver marcado para armazenamento de dados externo, use a opção variable e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

* **Anexos**: você pode usar a opção **[!UICONTROL Caminho do Anexo]** para especificar o nome da pasta para armazenar os anexos carregados no Formulário Adaptável. A pasta é criada em relação à carga útil. Se o workflow estiver marcado para armazenamento de dados externo, use a opção variable e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

* **Documento de Registro**: contém o Documento de Registro gerado para o Formulário Adaptável. Você pode usar a opção **[!UICONTROL Caminho do Documento de Registro]** para especificar o nome do arquivo do Documento de Registro e o caminho do arquivo relativo à carga útil. Por exemplo, o caminho `/addresschange/DoR.pdf` cria uma pasta chamada `addresschange` relativa à carga e coloca a `DoR.pdf` relativa à carga. Você também pode especificar apenas `DoR.pdf` para salvar apenas o documento de registro sem criar uma hierarquia de pastas. Se o workflow estiver marcado para armazenamento de dados externo, use a opção variable e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

Antes de usar a ação enviar **[!UICONTROL Invocar um fluxo de trabalho de AEM]**, configure o seguinte para a configuração do **[!UICONTROL serviço de configurações do AEM]**:

* **[!UICONTROL URL do Servidor de Processamento]**: o Servidor de Processamento é o servidor onde o Fluxo de Trabalho do Forms ou AEM é disparado. Pode ser o mesmo que o URL da instância do autor do AEM ou outro servidor.

* **[!UICONTROL Nome de Usuário do Servidor de Processamento]**: nome de usuário do usuário do fluxo de trabalho

* **[!UICONTROL Processando a senha do servidor]**: senha do usuário do fluxo de trabalho

## Enviar para o SharePoint {#submit-to-sharedrive}

A ação enviar **[!UICONTROL Enviar para o SharePoint]** conecta um formulário adaptável com um armazenamento Microsoft® SharePoint. É possível enviar o arquivo de dados de formulário, os anexos ou o Documento de Registro para o Armazenamento do Microsoft® Sharepoint conectado.

Usando a opção Enviar para o SharePoint, você pode:
* [Conectar um formulário adaptável à biblioteca de documentos do SharePoint](#connect-af-sharepoint-doc-library)
* [Conectar um Formulário Adaptável à Lista do SharePoint](#connect-af-sharepoint-list)


### Conectar um formulário adaptável à biblioteca de documentos do SharePoint {#connect-af-sharepoint-doc-library}

Para usar a Ação Enviar **[!UICONTROL Enviar para a Biblioteca de Documentos do SharePoint]** em um Formulário adaptável:

1. [Criar uma Configuração da Biblioteca de Documentos da SharePoint](#create-a-sharepoint-configuration-create-sharepoint-configuration): ela conecta o AEM Forms ao Armazenamento do Microsoft® Sharepoint.
2. [Use a ação enviar para o SharePoint em um Formulário adaptável](#use-sharepoint-configuartion-in-af): ele conecta seu Formulário adaptável ao Microsoft® SharePoint configurado.

#### Criar uma configuração da Biblioteca de documentos da SharePoint {#create-sharepoint-configuration}

Para conectar o AEM Forms ao seu Microsoft® Sharepoint Document Library Storage:

1. Vá para sua instância do **AEM Forms Author** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Após selecionar o **[!UICONTROL Microsoft® SharePoint]**, você será redirecionado para o **[!UICONTROL Navegador SharePoint]**.
1. Selecione um **Contêiner de Configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]** > **[!UICONTROL Biblioteca de Documentos da SharePoint]** na lista suspensa. O assistente de configuração do SharePoint é exibido.

   ![Configuração do SharePoint](/help/forms/assets/sharepoint_configuration.png)
1. Especifique o **[!UICONTROL Título]**, **[!UICONTROL ID do Cliente]**, **[!UICONTROL Segredo do Cliente]** e **[!UICONTROL URL do OAuth]**. Para obter informações sobre como recuperar a ID do cliente, o Segredo do cliente e a ID do locatário para a URL do OAuth, consulte a [Documentação da Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Você pode recuperar os `Client ID` e `Client Secret` de seu aplicativo do portal do Microsoft® Azure.
   * No portal do Microsoft® Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Substitua `[author-instance]` pela URL da sua instância de Autor.
   * Adicione as permissões de API `offline_access` e `Sites.Manage.All` para fornecer permissões de leitura/gravação.
   * Usar URL do OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substitua `<tenant-id>` pelo `tenant-id` do seu aplicativo no portal do Microsoft® Azure.

   >[!NOTE]
   >
   > O campo **segredo do cliente** é obrigatório ou opcional, depende da configuração do aplicativo do Azure Ative Diretory. Se o aplicativo estiver configurado para usar um segredo do cliente, é obrigatório fornecer o segredo do cliente.

1. Clique em **[!UICONTROL Conectar]**. Em uma conexão bem-sucedida, a mensagem `Connection Successful` é exibida.

1. Agora, selecione **Site do SharePoint** > **Biblioteca de Documentos** > **Pasta do SharePoint** para salvar os dados.

   >[!NOTE]
   >
   >* Por padrão, `forms-ootb-storage-adaptive-forms-submission` está presente no site do SharePoint selecionado.
   >* Crie uma pasta como `forms-ootb-storage-adaptive-forms-submission`, se ainda não estiver presente na biblioteca `Documents` do Site do SharePoint selecionado clicando em **Criar Pasta**.

Agora, você pode usar essa configuração do SharePoint Sites para a ação enviar em um Formulário adaptável.

#### Usar a configuração da biblioteca de documentos SharePoint em um formulário adaptável {#use-sharepoint-configuartion-in-af}

Você pode usar a configuração criada da Biblioteca de documentos da SharePoint em um Formulário adaptável para salvar dados ou o Documento de registro gerado em uma pasta do SharePoint. Execute as seguintes etapas para usar uma configuração de armazenamento da Biblioteca de documentos da SharePoint em um Formulário adaptável como:

1. Crie um [Formulário adaptável](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Selecione o mesmo [!UICONTROL Contêiner de configuração] para um Formulário adaptável, onde você criou seu armazenamento da Biblioteca de documentos da SharePoint.
   > * Se nenhum [!UICONTROL Contêiner de Configuração] for selecionado, as pastas de [!UICONTROL Configuração de Armazenamento] globais serão exibidas na janela de propriedades da Ação de Envio.

1. Selecione **Enviar Ação** como **[!UICONTROL Enviar para o SharePoint]**.
   ![GIF do Sharepoint](/help/forms/assets/sharedrive-video.gif)
1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

Ao enviar o formulário, os dados são salvos no Armazenamento da Biblioteca de Documentos do Microsoft® Sharepoint especificado.
A estrutura de pasta para salvar dados é `/folder_name/form_name/year/month/date/submission_id/data`.

### Conectar um formulário adaptável à lista Microsoft® SharePoint {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

Para usar a ação enviar [!UICONTROL Enviar para a Lista do SharePoint] em um formulário adaptável:

1. [Criar uma Configuração de Lista do SharePoint](#create-sharepoint-list-configuration): ela conecta o AEM Forms ao Armazenamento de Lista do Microsoft® Sharepoint.
1. [Usar o Enviar usando o Modelo de Dados de Formulário (FDM) em um Formulário Adaptável](#use-submit-using-fdm): ele conecta seu Formulário Adaptável ao Microsoft® SharePoint configurado.

#### Criar uma configuração de lista do SharePoint {#create-sharepoint-list-configuration}

Para conectar o AEM Forms à sua lista do Microsoft® Sharepoint:

1. Vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Selecione um **Contêiner de Configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]** > **[!UICONTROL Lista do SharePoint]** na lista suspensa. O assistente de configuração do SharePoint é exibido.
1. Especifique o **[!UICONTROL Título]**, **[!UICONTROL ID do Cliente]**, **[!UICONTROL Segredo do Cliente]** e **[!UICONTROL URL do OAuth]**. Para obter informações sobre como recuperar a ID do cliente, o Segredo do cliente e a ID do locatário para a URL do OAuth, consulte a [Documentação da Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Você pode recuperar os `Client ID` e `Client Secret` de seu aplicativo do portal do Microsoft® Azure.
   * No portal do Microsoft® Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Substitua `[author-instance]` pela URL da sua instância de Autor.
   * Adicione as permissões de API `offline_access` e `Sites.Manage.All` na guia **Microsoft® Graph** para fornecer permissões de leitura/gravação. Adicione a permissão `AllSites.Manage` na guia **Sharepoint** para interagir remotamente com os dados do SharePoint.
   * Usar URL do OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substitua `<tenant-id>` pelo `tenant-id` do seu aplicativo no portal do Microsoft® Azure.

     >[!NOTE]
     >
     > O campo **segredo do cliente** é obrigatório ou opcional, depende da configuração do aplicativo do Azure Ative Diretory. Se o aplicativo estiver configurado para usar um segredo do cliente, é obrigatório fornecer o segredo do cliente.

1. Clique em **[!UICONTROL Conectar]**. Em uma conexão bem-sucedida, a mensagem `Connection Successful` é exibida.
1. Selecione **[!UICONTROL Site do SharePoint]** e **[!UICONTROL Lista do SharePoint]** na lista suspensa.
1. Selecione **[!UICONTROL Criar]** para criar a configuração de nuvem do Microsoft® SharePointList.


#### Usar o Enviar usando o Modelo de dados de formulário (FDM) em um formulário adaptável {#use-submit-using-fdm}

Você pode usar a configuração da Lista do SharePoint criada em um Formulário adaptável para salvar dados ou o Documento de registro gerado em uma Lista do SharePoint. Execute as seguintes etapas para usar uma configuração de armazenamento de Lista do SharePoint em um Formulário adaptável como:

1. [Criar um modelo de dados de formulário (FDM) usando a configuração da Lista do Microsoft® SharePoint](/help/forms/create-form-data-models.md)
1. [Configurar o Modelo de dados de formulário (FDM) para recuperar e enviar dados](/help/forms/work-with-form-data-model.md#configure-services)
1. [Criação de um Formulário adaptável](/help/forms/creating-adaptive-form.md)
1. [Configurar a ação Enviar usando um Modelo de dados de formulário (FDM)](/help/forms/configuring-submit-actions.md#submit-using-form-data-model)

Ao enviar o formulário, os dados são salvos no Armazenamento de Lista do Microsoft® Sharepoint especificado.

>[!NOTE]
>
> Na Lista do Microsoft® SharePoint, os seguintes tipos de coluna não são suportados:
> * coluna de imagem
> * coluna de metadados
> * coluna de pessoa
> * coluna de dados externos


## Enviar para o OneDrive {#submit-to-onedrive}

A Ação de Envio **[!UICONTROL Enviar para o OneDrive]** conecta um Formulário adaptável com um Microsoft® OneDrive. Você pode enviar os dados do formulário, arquivo, anexos ou Documento de registro para o Microsoft® OneDrive Storage conectado. Para usar a Ação de Envio [!UICONTROL Enviar para o OneDrive] em um Formulário Adaptável:

1. [Criar uma Configuração do OneDrive](#create-a-onedrive-configuration-create-onedrive-configuration): ela conecta o AEM Forms ao seu Microsoft® OneDrive Storage.
2. [Use a ação de envio Enviar para o OneDrive em um Formulário Adaptável](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): ele conecta seu Formulário Adaptável a
Microsoft® OneDrive configurado.

### Criar uma Configuração do OneDrive {#create-onedrice-configuration}

Para conectar o AEM Forms ao seu Microsoft® OneDrive Storage:

1. Vá para sua instância do **AEM Forms Author** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® OneDrive]**.
1. Depois de selecionar o **[!UICONTROL Microsoft® OneDrive]**, você será redirecionado para o **[!UICONTROL OneDrive Browser]**.
1. Selecione um **Contêiner de Configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]**. O assistente de configuração do OneDrive é exibido.

   ![Tela de Configuração do OneDrive](/help/forms/assets/onedrive-configuration.png)

1. Especifique o **[!UICONTROL Título]**, **[!UICONTROL ID do Cliente]**, **[!UICONTROL Segredo do Cliente]** e **[!UICONTROL URL do OAuth]**. Para obter informações sobre como recuperar a ID do cliente, o Segredo do cliente e a ID do locatário para a URL do OAuth, consulte a [Documentação da Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Você pode recuperar os `Client ID` e `Client Secret` de seu aplicativo do portal do Microsoft® Azure.
   * No portal do Microsoft® Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`. Substitua `[author-instance]` pela URL da sua instância de Autor.
   * Adicione as permissões de API `offline_access` e `Files.ReadWrite.All` para fornecer permissões de leitura/gravação.
   * Usar URL do OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substitua `<tenant-id>` pelo `tenant-id` do seu aplicativo no portal do Microsoft® Azure.

   >[!NOTE]
   >
   > O campo **segredo do cliente** é obrigatório ou opcional, depende da configuração do aplicativo do Azure Ative Diretory. Se o aplicativo estiver configurado para usar um segredo do cliente, é obrigatório fornecer o segredo do cliente.

1. Clique em **[!UICONTROL Conectar]**. Em uma conexão bem-sucedida, a mensagem `Connection Successful` é exibida.

1. Agora, selecione **[!UICONTROL OneDrive Container]** > **[OneDrive Folder]** para salvar os dados.

   >[!NOTE]
   >
   >* Por padrão, `forms-ootb-storage-adaptive-forms-submission` está presente no OneDrive Container.
   > * Crie uma pasta como `forms-ootb-storage-adaptive-forms-submission`, se ainda não estiver presente, clicando em **Criar Pasta**.

Agora, você pode usar esta configuração de armazenamento do OneDrive para a ação de envio em um Formulário adaptável.

### Usar a configuração do OneDrive em um formulário adaptável {#use-onedrive-configuartion-in-af}

Você pode usar a configuração de armazenamento do OneDrive criada em um Formulário adaptável para salvar dados ou o Documento de Registro gerado em uma pasta do OneDrive. Execute as seguintes etapas para usar a configuração de armazenamento do OneDrive em um Formulário adaptável como:
1. Crie um [Formulário adaptável](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Selecione o mesmo [!UICONTROL Contêiner de Configuração] para um Formulário Adaptável, onde você criou seu armazenamento do OneDrive.
   > * Se nenhum [!UICONTROL Contêiner de Configuração] for selecionado, as pastas de [!UICONTROL Configuração de Armazenamento] globais serão exibidas na janela de propriedades da Ação de Envio.

1. Selecione **Enviar Ação** como **[!UICONTROL Enviar para o OneDrive]**.
   ![GIF do OneDrive](/help/forms/assets/onedrive-video.gif)
1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

Ao enviar o formulário, os dados são salvos no Armazenamento do Microsoft® OneDrive especificado.
A estrutura de pasta para salvar dados é `/folder_name/form_name/year/month/date/submission_id/data`.

## Enviar para o Armazenamento de blob do Azure {#submit-to-azure-blob-storage}

A Ação de envio **[!UICONTROL Enviar para o Armazenamento de Blobs do Azure]** conecta um Formulário adaptável a um portal do Microsoft® Azure. Você pode enviar os dados do formulário, o arquivo, os anexos ou o Documento de registro para os contêineres conectados do Armazenamento do Azure. Para usar a ação Enviar para o Armazenamento de blobs do Azure:

1. [Criar um Contêiner de Armazenamento Azure Blob](#create-a-azure-blob-storage-container-create-azure-configuration): ele conecta o AEM Forms aos contêineres de Armazenamento Azure.
2. [Usar a Configuração de Armazenamento do Azure em um Formulário Adaptável](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): ela conecta seu Formulário Adaptável a contêineres de Armazenamento do Azure configurados.

### Criar um contêiner de armazenamento do Azure Blob {#create-azure-configuration}

Para conectar o AEM Forms aos seus contêineres de Armazenamento do Azure:
1. Vá para sua instância do **AEM Forms Author** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Armazenamento do Azure]**.
1. Depois de selecionar o **[!UICONTROL Armazenamento do Azure]**, você será redirecionado para o **[!UICONTROL Navegador de Armazenamento do Azure]**.
1. Selecione um **Contêiner de Configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]**. O assistente Criar configuração de armazenamento do Azure é exibido.

   ![Configuração de Armazenamento do Azure](/help/forms/assets/azure-storage-configuration.png)

1. Especifique o **[!UICONTROL Título]**, a **[!UICONTROL Conta de Armazenamento do Azure]** e a **[!UICONTROL Chave de Acesso do Azure]**.

   * Você pode recuperar o nome de `Azure Storage Account` e `Azure Access key` das Contas de Armazenamento no portal do Microsoft® Azure.

1. Clique em **[!UICONTROL Salvar]**.

Agora, você pode usar essa configuração do contêiner de Armazenamento do Azure para a ação de envio em um Formulário adaptável.

### Usar a configuração de armazenamento do Azure em um formulário adaptável {#use-azure-storage-configuartion-in-af}

Você pode usar a configuração do contêiner de Armazenamento do Azure criada em um Formulário adaptável, para salvar dados ou o Documento de registro gerado no contêiner de Armazenamento do Azure. Execute as seguintes etapas para usar a configuração do contêiner de Armazenamento do Azure em um Formulário adaptável como:
1. Crie um [Formulário adaptável](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Selecione o mesmo [!UICONTROL Contêiner de Configuração] para um Formulário Adaptável, onde você criou seu armazenamento do OneDrive.
   > * Se nenhum [!UICONTROL Contêiner de Configuração] for selecionado, as pastas de [!UICONTROL Configuração de Armazenamento] globais serão exibidas na janela de propriedades da Ação de Envio.

1. Selecione **Enviar Ação** como **[!UICONTROL Enviar para o Armazenamento de Blob do Azure]**.
   ![GIF de Armazenamento Azure Blob](/help/forms/assets/azure-submit-video.gif)

1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

Ao enviar o formulário, os dados são salvos na configuração especificada do contêiner de Armazenamento do Azure.
A estrutura de pasta para salvar dados é `/configuration_container/form_name/year/month/date/submission_id/data`.

Para definir valores de uma configuração, [Gere Configurações OSGi usando o SDK do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [implante a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) na instância do Cloud Service.


## Enviar para o Power Automate {#microsoft-power-automate}

Você pode configurar um Formulário adaptável para executar um fluxo da nuvem do Microsoft® Power Automate no envio. O formulário adaptável configurado envia dados capturados, anexos e documentos de registro para processamento no fluxo da nuvem do Power Automate. Ele ajuda você a criar uma experiência personalizada de captura de dados, aproveitando o poder do Microsoft® Power Automate para criar lógicas comerciais sobre dados capturados e automatizar os fluxos de trabalho do cliente. Estes são alguns exemplos do que você pode fazer após integrar um formulário adaptável ao Microsoft® Power Automate:

* Usar dados adaptáveis do Forms em processos de negócios do Power Automate
* Use o Power Automate para enviar dados capturados para mais de 500 fontes de dados ou qualquer API disponível publicamente
* Realizar cálculos complexos em dados capturados
* Salve os dados do Forms adaptável em sistemas de armazenamento em uma programação predefinida

O editor Forms adaptável fornece a **ação de envio Chamar um fluxo do Microsoft® Power Automate** para enviar dados de formulários adaptáveis, anexos e Documentos de Registro para o fluxo da nuvem do Power Automate. Para usar a ação Enviar para enviar dados capturados para o Microsoft® Power Automate, [Conecte sua as a Cloud Service do Forms com o Microsoft® Power Automate](forms-microsoft-power-automate-integration.md)

Após uma configuração bem-sucedida, use a ação de envio [Chamar um fluxo do Microsoft® Power Automate](forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action) para enviar dados a um Fluxo do Power Automate.

## Enviar para o Workfront Fusion {#workfront-fusion}

Você pode configurar um Formulário adaptável para enviar dados ao Workfront Fusion no envio. O Workfront Fusion permite a automação de processos para que o usuário possa se concentrar em novas tarefas, em vez de repetir as mesmas tarefas repetidamente. Ele automatiza tarefas simples e complexas, economizando tempo e garantindo uma execução consistente do processo.

O editor do Adaptive Forms fornece a ação de envio **Chamar um Cenário do Workfront Fusion** para enviar dados ou anexos do Adaptive Forms para um cenário do Workfront Fusion. Para usar a ação de envio para enviar dados capturados para um cenário do Workfront Fusion, consulte [Enviar um Formulário adaptável para o Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md).

## Usar envio síncrono ou assíncrono {#use-synchronous-or-asynchronous-submission}

Uma Ação de envio pode usar envio síncrono ou assíncrono.

**Envio síncrono**: tradicionalmente, os formulários web são configurados para enviar de forma síncrona. Em um envio síncrono, quando os usuários enviam um formulário, eles são redirecionados para uma página de confirmação, uma página de agradecimento ou, se houver falha de envio, uma página de erro. Você pode selecionar a opção **[!UICONTROL Usar envio assíncrono]** para redirecionar os usuários para uma página da Web ou mostrar uma mensagem no envio.

![Configurar Ação de Envio](assets/thank-you-setting.png)

**Envio assíncrono**: experiências da Web modernas, como aplicativos de página única, estão ganhando popularidade, onde a página da Web permanece estática enquanto a interação cliente-servidor ocorre em segundo plano. Agora você pode fornecer essa experiência com o Adaptive Forms ao [configurar o envio assíncrono](asynchronous-submissions-adaptive-forms.md).

## Revalidação do lado do servidor no formulário adaptável {#server-side-revalidation-in-adaptive-form}

Normalmente, em qualquer sistema de captura de dados online, os desenvolvedores colocam algumas validações do JavaScript no lado do cliente para aplicar algumas regras de negócios. Mas em navegadores modernos, os usuários finais têm uma maneira de ignorar essas validações e fazer envios manualmente usando várias técnicas, como o Console DevTools do navegador da Web. Essas técnicas também são válidas para o Adaptive Forms. Um desenvolvedor de formulários pode criar várias lógicas de validação, mas tecnicamente, os usuários finais podem ignorar essas lógicas de validação e enviar dados inválidos para o servidor. Dados inválidos violariam as regras de negócios aplicadas por um autor de formulários.

O recurso de revalidação do lado do servidor também permite executar as validações que um autor do Adaptive Forms forneceu ao criar um Formulário adaptável no servidor. Isso evita qualquer possível comprometimento dos envios de dados e violações das regras de negócios representadas em termos de validações de formulário.

### O que validar no servidor? {#what-to-validate-on-server-br}

Todas as validações de campo prontas para uso (OOTB) de um Formulário adaptável que são executadas novamente no servidor são:

* Obrigatório
* Cláusula de Imagem de Validação
* Expressão de validação

### Ativar a validação do lado do servidor {#enabling-server-side-validation-br}

Use a **[!UICONTROL Revalidar no servidor]** em Contêiner de Formulário Adaptável na barra lateral para habilitar ou desabilitar a validação no servidor para o formulário atual.

![Habilitando A Validação No Lado Do Servidor](assets/revalidate-on-server.png)

Ativar a validação do lado do servidor

Se o usuário final ignorar essas validações e enviar os formulários, o servidor executará novamente a validação. Se a validação falhar no final do servidor, a transação de envio será interrompida. O formulário original é apresentado ao usuário novamente. Os dados capturados e os dados enviados são apresentados ao usuário como um erro.

>[!NOTE]
>
>A validação do lado do servidor valida o modelo de formulário. É recomendável criar uma biblioteca do cliente separada para validações e não misturá-la com outras coisas, como estilo de HTML e manipulação de DOM na mesma biblioteca do cliente.

### Suporte a funções personalizadas em expressões de validação {#supporting-custom-functions-in-validation-expressions-br}

Às vezes, se houver **regras de validação complexas**, o script de validação exato residirá em funções personalizadas e o autor chamará essas funções personalizadas da expressão de validação de campo. Para tornar esta biblioteca de funções personalizada conhecida e disponível durante a execução de validações no lado do servidor, o autor do formulário pode configurar o nome da biblioteca do cliente AEM na guia **[!UICONTROL Básico]** das propriedades do Contêiner de formulário adaptável, conforme mostrado abaixo.

![Dando suporte a funções personalizadas em Expressões de Validação](assets/clientlib-cat.png)

Suporte a funções personalizadas em expressões de validação

O autor pode configurar a biblioteca JavaScript personalizada por formulário adaptável. Na biblioteca, mantenha somente as funções reutilizáveis, que dependem de bibliotecas de terceiros de jquery e underscore.js.

## Tratamento de erros na ação enviar {#error-handling-on-submit-action}

Como parte das diretrizes de segurança e proteção contra AEM, configure páginas de erro personalizadas como 400.jsp, 404.jsp e 500.jsp. Esses manipuladores são chamados quando ao enviar um formulário 400, 404 ou 500 erros são exibidos. Os manipuladores também são chamados quando esses códigos de erro são acionados no nó do Publish. Você também pode criar páginas JSP para outros códigos de erro HTTP.

Quando você preenche um modelo de dados de formulário (FDM) ou um formulário adaptável baseado em esquema com reclamação de dados XML ou JSON para um esquema cujos dados não contêm as tags `<afData>`, `<afBoundData>` e `</afUnboundData>`, os dados de campos não vinculados do formulário adaptável são perdidos. O esquema pode ser um esquema XML, esquema JSON ou um Modelo de dados de formulário (FDM). Campos não limitados são campos de Formulário adaptável sem a propriedade `bindref`.

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->

>[!MORELIKETHIS]
>
>* [Criar uma Ação de Envio personalizada para o Forms Adaptável](/help/forms/custom-submit-action-form.md)
