---
title: Como configurar uma ação de envio para um formulário adaptável
description: Um formulário adaptável fornece várias ações de envio. Uma ação de envio define como um formulário adaptável é processado após o envio. Você pode usar as ações de envio incorporadas ou criar as suas próprias.
exl-id: a4ebedeb-920a-4ed4-98b3-2c4aad8e5f78
source-git-commit: 6f6cf5657bf745a2e392a8bfd02572aa864cc69c
workflow-type: tm+mt
source-wordcount: '3065'
ht-degree: 1%

---

# Ação de envio de formulário adaptável {#configuring-the-submit-action}

Uma ação Enviar é acionada quando um usuário clica no botão **[!UICONTROL Enviar]** em um formulário adaptável. O Adaptive Forms fornece algumas ações de envio prontas para uso. As Ações de envio disponíveis prontas para uso são:

* [Enviar para ponto de extremidade REST](#submit-to-rest-endpoint)
* [Enviar e-mail](#send-email)
* [Enviar usando modelo de dados do formulário](#submit-using-form-data-model)
* [Chamar um fluxo de trabalho AEM](#invoke-an-aem-workflow)
* [Enviar para o SharePoint](#submit-to-sharedrive)
* [Enviar para o OneDrive](#submit-to-onedrive)
* [Enviar para o Armazenamento de blob do Azure](#azure-blob-storage)

Você também pode [estender as ações de envio padrão](custom-submit-action-form.md) para criar sua própria Ação de envio.

É possível configurar uma Ação de envio na variável **[!UICONTROL Submissão]** seção das propriedades do Contêiner de formulário adaptável, na barra lateral.

![Configurar ação de envio](assets/submission.png)


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

## Enviar para ponto de extremidade REST {#submit-to-rest-endpoint}

Use o **[!UICONTROL Enviar para Ponto de Extremidade REST]** para postar os dados enviados em um URL restante. O URL pode ser de um servidor interno (o servidor no qual o formulário é renderizado) ou externo.

Para postar dados em um servidor interno, forneça o caminho do recurso. Os dados são postados no caminho do recurso. Por exemplo, /content/restEndPoint. Para essas solicitações de publicação, as informações de autenticação da solicitação de envio são usadas.

Para postar dados em um servidor externo, forneça um URL. O formato do URL é `https://host:port/path_to_rest_end_point`. Certifique-se de configurar o caminho para lidar com a solicitação POST anonimamente.

![Mapeamento para valores de campo passados como parâmetros da Página de agradecimento](assets/post-enabled-actionconfig.png)

No exemplo acima, o usuário inseriu informações em `textbox` é capturado usando o parâmetro `param1`. Sintaxe para postar dados capturados usando `param1` é:

`String data=request.getParameter("param1");`

Da mesma forma, os parâmetros usados para publicar dados e anexos XML são `dataXml` e `attachments`.

Por exemplo, esses dois parâmetros são usados no script para analisar os dados em um ponto de extremidade de repouso. Use a seguinte sintaxe para armazenar e analisar os dados:

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

Neste exemplo, `data` armazena os dados XML, e `att` armazena dados de anexo.

O **[!UICONTROL Enviar para ponto de extremidade REST]** Enviar Ação envia os dados preenchidos no formulário para uma página de confirmação configurada como parte da solicitação HTTP GET. É possível adicionar o nome dos campos a serem solicitados. O formato da solicitação é:

`{fieldName}={request parameter name}`

Conforme mostrado na imagem abaixo, `param1` e `param2` são transmitidos como parâmetros com valores copiados do **caixa de texto** e **numericbox** campos para a próxima ação.

![Configurar a ação de envio do ponto de extremidade restante](assets/action-config.png)

Você também pode **[!UICONTROL Habilitar solicitação de POST]** e forneça um URL para postar a solicitação. Para enviar dados para o servidor AEM que hospeda o formulário, use um caminho relativo correspondente ao caminho raiz do servidor AEM. Por exemplo, `/content/forms/af/SampleForm.html`. Para enviar dados para qualquer outro servidor, use o caminho absoluto.

>[!NOTE]
>
>Para transmitir os campos como parâmetros em um URL REST, todos os campos devem ter nomes de elemento diferentes, mesmo se os campos forem colocados em painéis diferentes.

## Enviar e-mail {#send-email}

Você pode usar o **[!UICONTROL Enviar Email]** Enviar ação para enviar um email para um ou mais recipients após o envio bem-sucedido do formulário. O email gerado pode conter dados de formulário em um formato predefinido. Por exemplo, no modelo a seguir, o nome do cliente, o endereço de envio, o nome do estado e o CEP são recuperados dos dados de formulário enviados.

    &quot;
    
    Olá ${customer_Name},
    
    O seguinte é definido como seu endereço de envio padrão:
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    Atenção,
    WKND
    
    &quot;

>[!NOTE]
>
> * Todos os campos do formulário devem ter nomes de elementos diferentes, mesmo que os campos sejam colocados em painéis diferentes de um formulário adaptável.
> * AEM as a Cloud Service requer que o email de saída seja criptografado. Por padrão, o email de saída é desativado. Para ativá-la, envie um tíquete de suporte para [Solicitar acesso](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#sending-email).


Você também pode incluir anexos e um Documento de registro (DoR) no email. Para ativar **[!UICONTROL Anexar documento de registro]** , configure o formulário adaptável para gerar um documento de registro (DoR). Você pode ativar a opção para gerar um Documento de registro das propriedades do formulário adaptável.



<!-- ## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. -->

<!-- ## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). -->

## Enviar usando modelo de dados do formulário {#submit-using-form-data-model}

O **[!UICONTROL Enviar usando o Modelo de dados de formulário]** Enviar ação grava dados enviados do Formulário adaptável para o objeto de modelo de dados especificado em um Modelo de dados de formulário para a fonte de dados. Ao configurar a Ação de envio, você pode escolher um objeto de modelo de dados cujos dados enviados deseja gravar de volta em sua fonte de dados.

Além disso, é possível enviar um anexo de formulário usando um Modelo de dados de formulário e um Documento de registro (DoR) para a fonte de dados. Para obter informações sobre o modelo de dados de formulário, consulte [[!DNL AEM Forms] Integração de dados](data-integration.md).

<!--
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). -->

## Chamar um fluxo de trabalho AEM {#invoke-an-aem-workflow}

O **[!UICONTROL Chamar um fluxo de trabalho AEM]** Enviar ação associa um Formulário adaptável a um [Fluxo de trabalho AEM](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=en#extending-aem). Quando um formulário é enviado, o fluxo de trabalho associado é iniciado automaticamente na instância do autor. Você pode salvar o arquivo de dados, os anexos e o Documento de registro no local da carga do fluxo de trabalho ou em uma variável. Se o workflow estiver marcado para armazenamento externo de dados e configurado para um armazenamento externo de dados, somente a opção de variável estará disponível. Você pode selecionar na lista de variáveis disponíveis para o modelo de fluxo de trabalho. Se o workflow estiver marcado para armazenamento de dados externo em um estágio posterior e não no momento da criação do workflow, verifique se as configurações de variável necessárias estão em vigor.

A Ação de envio coloca o seguinte no local de carga do fluxo de trabalho ou a variável se o fluxo de trabalho estiver marcado para armazenamento de dados externo:

* **Arquivo de dados**: Ele contém os dados enviados para o formulário adaptável. Você pode usar o **[!UICONTROL Caminho do arquivo de dados]** para especificar o nome do arquivo e o caminho do arquivo em relação à carga útil. Por exemplo, a variável `/addresschange/data.xml` caminho cria uma pasta chamada `addresschange` e o coloca em relação à carga útil. Também é possível especificar somente `data.xml` para enviar apenas dados enviados sem criar uma hierarquia de pastas. Se o workflow estiver marcado para armazenamento externo de dados, use a opção de variável e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

* **Anexos**: Você pode usar o **[!UICONTROL Caminho do anexo]** para especificar o nome da pasta para armazenar os anexos carregados no Formulário adaptável. A pasta é criada em relação à carga. Se o workflow estiver marcado para armazenamento externo de dados, use a opção de variável e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

* **Documento de registro**: Ele contém o Documento de registro gerado para o formulário adaptável. Você pode usar o **[!UICONTROL Documento de caminho de registro]** para especificar o nome do arquivo Documento de registro e o caminho do arquivo em relação à carga útil. Por exemplo, a variável `/addresschange/DoR.pdf` caminho cria uma pasta chamada `addresschange` relativo à carga e posiciona a variável `DoR.pdf` relativo à carga. Também é possível especificar somente `DoR.pdf` para salvar somente o Documento de registro sem criar uma hierarquia de pasta. Se o workflow estiver marcado para armazenamento externo de dados, use a opção de variável e selecione a variável na lista de variáveis disponíveis para o modelo de workflow.

Antes de usar o **[!UICONTROL Chamar um fluxo de trabalho AEM]** Enviar ação configure o seguinte para o **[!UICONTROL Serviço de configurações do AEM DS]** configuração:

* **[!UICONTROL URL do servidor de processamento]**: O Servidor de processamento é o servidor no qual o Forms ou AEM Workflow é acionado. Isso pode ser igual ao URL da instância do autor do AEM ou de outro servidor.

* **[!UICONTROL Nome de usuário do servidor de processamento]**: Nome de usuário do usuário do workflow

* **[!UICONTROL Senha do servidor de processamento]**: Senha do usuário do fluxo de trabalho

## Enviar para o SharePoint {#submit-to-sharedrive}

O **[!UICONTROL Enviar para a SharePoint]** A ação Enviar conecta um formulário adaptável a um armazenamento Microsoft SharePoint. Você pode enviar o arquivo de dados do formulário, os anexos ou o Documento de registro para o Microsoft Sharepoint Storage conectado. Para usar o **[!UICONTROL Enviar para a SharePoint]** Enviar ação em um formulário adaptável:

1. [Criar uma configuração do SharePoint](#create-a-sharepoint-configuration-create-sharepoint-configuration): Ele conecta o AEM Forms ao seu armazenamento do Microsoft Sharepoint.
2. [Use a ação Enviar para o SharePoint em um formulário adaptável](#use-sharepoint-configuartion-in-af): Ele conecta seu formulário adaptável ao Microsoft SharePoint configurado.

### Criar uma configuração do SharePoint {#create-sharepoint-configuration}

Para conectar o AEM Forms ao seu armazenamento do Microsoft Sharepoint:

1. Vá para o **Autor do AEM Forms** instância > **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft SharePoint]**.
1. Depois de selecionar a variável **[!UICONTROL Microsoft SharePoint]**, você será redirecionado para **[!UICONTROL Navegador SharePoint]**.
1. Selecione um **Contêiner de configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]**. O assistente de configuração do SharePoint é exibido.
   ![Configuração do SharePoint](/help/forms/assets/sharepoint_configuration.png)
1. Especifique a **[!UICONTROL Título]**, **[!UICONTROL ID do cliente]**, **[!UICONTROL Segredo do cliente]** e **[!UICONTROL URL de OAuth]**. Para obter informações sobre como recuperar a ID do cliente, o Segredo do cliente, a ID do locatário para o URL OAuth, consulte [Documentação do Microsoft](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Você pode recuperar o `Client ID` e `Client Secret` do seu aplicativo no portal do Microsoft Azure.
   * No portal do Microsoft Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Substituir `[author-instance]` com o URL da instância do autor.
   * Adicionar as permissões da API `offline_access` e `Sites.Manage.All` para fornecer permissões de leitura/gravação.
   * Use o URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substituir `<tenant-id>` com o `tenant-id` do seu aplicativo no portal do Microsoft Azure.

1. Clique em **[!UICONTROL Connect]**. Em uma conexão bem-sucedida, a variável `Connection Successful` será exibida.

1. Agora, selecione **Site do SharePoint** > **Biblioteca de documentos** > **Pasta SharePoint**, para salvar os dados.

   >[!NOTE]
   >
   >* Por padrão, `forms-ootb-storage-adaptive-forms-submission` está presente no Site do SharePoint selecionado.
   >* Criar uma pasta como `forms-ootb-storage-adaptive-forms-submission`, se ainda não estiver presente no `Documents` biblioteca do Site do SharePoint selecionado clicando em **Criar pasta**.


Agora, você pode usar essa configuração do SharePoint Sites para a ação de envio em um Formulário adaptável.

### Usar a configuração do SharePoint em um formulário adaptável {#use-sharepoint-configuartion-in-af}

Você pode usar a configuração do SharePoint criada em um Formulário adaptável, para salvar dados ou o Documento de registro gerado em uma pasta SharePoint. Execute as seguintes etapas para usar uma configuração de armazenamento SharePoint em um Formulário adaptável como:
1. Crie um [Formulário adaptável](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Selecione o mesmo [!UICONTROL Contêiner de configuração] para um formulário adaptável, onde você criou o armazenamento SharePoint.
   > * Se não [!UICONTROL Contêiner de configuração] for selecionada, em seguida, a variável global [!UICONTROL Configuração de armazenamento] As pastas são exibidas na janela de propriedades Enviar Ação.


1. Selecionar **Enviar ação** as **[!UICONTROL Enviar para a SharePoint]**.
   ![GIF do Sharepoint](/help/forms/assets/sharedrive-video.gif)
1. Selecione o **[!UICONTROL Configuração de armazenamento]**, onde deseja salvar os dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Enviar.

Quando você envia o formulário, os dados são salvos no Microsoft Sharepoint Storage especificado.
A estrutura de pastas para salvar dados é `/folder_name/form_name/year/month/date/submission_id/data`.

## Enviar para o OneDrive {#submit-to-onedrive}

O **[!UICONTROL Enviar para o OneDrive]** A ação Enviar conecta um formulário adaptável a um Microsoft OneDrive. Você pode enviar os dados do formulário, o arquivo, os anexos ou o Documento de registro para o armazenamento conectado do Microsoft OneDrive. Para usar o [!UICONTROL Enviar para o OneDrive] Enviar ação em um formulário adaptável:

1. [Criar uma configuração do OneDrive](#create-a-onedrive-configuration-create-onedrive-configuration): Ele conecta o AEM Forms ao seu armazenamento Microsoft OneDrive.
2. [Use a ação Enviar para o OneDrive Submeter em um Formulário Adaptável](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): Ele conecta seu formulário adaptável ao Microsoft OneDrive configurado.

### Criar uma configuração do OneDrive {#create-onedrice-configuration}

Para conectar o AEM Forms ao seu armazenamento Microsoft OneDrive:

1. Vá para o **Autor do AEM Forms** instância > **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft OneDrive]**.
1. Depois de selecionar a variável **[!UICONTROL Microsoft OneDrive]**, você será redirecionado para **[!UICONTROL Navegador OneDrive]**.
1. Selecione um **Contêiner de configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]**. O assistente de configuração do OneDrive é exibido.

   ![Tela de configuração do OneDrive](/help/forms/assets/onedrive-configuration.png)

1. Especifique a **[!UICONTROL Título]**, **[!UICONTROL ID do cliente]**, **[!UICONTROL Segredo do cliente]** e **[!UICONTROL URL de OAuth]**. Para obter informações sobre como recuperar a ID do cliente, o Segredo do cliente, a ID do locatário para o URL OAuth, consulte [Documentação do Microsoft](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Você pode recuperar o `Client ID` e `Client Secret` do seu aplicativo no portal do Microsoft Azure.
   * No portal do Microsoft Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`. Substituir `[author-instance]` com o URL da instância do autor.
   * Adicionar as permissões da API `offline_access` e `Files.ReadWrite.All` para fornecer permissões de leitura/gravação.
   * Use o URL OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substituir `<tenant-id>` com o `tenant-id` do seu aplicativo no portal do Microsoft Azure.

1. Clique em **[!UICONTROL Connect]**. Em uma conexão bem-sucedida, a variável `Connection Successful` será exibida.

1. Agora, selecione **[!UICONTROL Contêiner do OneDrive]** > **[Pasta do OneDrive]**  para salvar os dados.

   >[!NOTE]
   >
   >* Por padrão, `forms-ootb-storage-adaptive-forms-submission` está presente no Contêiner do OneDrive.
   > * Criar uma pasta como `forms-ootb-storage-adaptive-forms-submission`, se ainda não estiver presente, clicando em **Criar pasta**.


Agora, você pode usar essa configuração de armazenamento do OneDrive para a ação de envio em um formulário adaptável.

### Usar a configuração do OneDrive em um formulário adaptável {#use-onedrive-configuartion-in-af}

Você pode usar a configuração de armazenamento do OneDrive criada em um formulário adaptável, para salvar dados ou o Documento de registro gerado em uma pasta do OneDrive. Execute as seguintes etapas para usar a configuração de armazenamento do OneDrive em um Formulário adaptável como:
1. Crie um [Formulário adaptável](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Selecione o mesmo [!UICONTROL Contêiner de configuração] para um formulário adaptável, onde você criou o armazenamento do OneDrive.
   > * Se não [!UICONTROL Contêiner de configuração] for selecionada, em seguida, a variável global [!UICONTROL Configuração de armazenamento] As pastas são exibidas na janela de propriedades Enviar Ação.


1. Selecionar **Enviar ação** as **[!UICONTROL Enviar para o OneDrive]**.
   ![GIF do OneDrive](/help/forms/assets/onedrive-video.gif)
1. Selecione o **[!UICONTROL Configuração de armazenamento]**, onde deseja salvar os dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Enviar.

Quando você envia o formulário, os dados são salvos no Microsoft OneDrive Storage especificado.
A estrutura de pastas para salvar dados é `/folder_name/form_name/year/month/date/submission_id/data`.

## Enviar para o Armazenamento de blob do Azure {#submit-to-azure-blob-storage}

O **[!UICONTROL Enviar para o Armazenamento Azure Blob]**  A ação Enviar conecta um Formulário adaptável a um portal do Microsoft Azure. Você pode enviar os dados do formulário, o arquivo, os anexos ou o Documento de registro para os contêineres de Armazenamento do Azure conectados. Para usar a ação Enviar para o Armazenamento Azure Blob:

1. [Criar um Contêiner de Armazenamento do Azure Blob](#create-a-azure-blob-storage-container-create-azure-configuration): Ele conecta o AEM Forms aos contêineres de Armazenamento do Azure.
2. [Usar a configuração de armazenamento do Azure em um formulário adaptável ](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): Ele conecta seu Formulário adaptativo aos contêineres de armazenamento do Azure configurados.

### Criar um Contêiner de Armazenamento do Azure Blob {#create-azure-configuration}

Para conectar o AEM Forms aos seus contêineres de Armazenamento do Azure:
1. Vá para o seu **Autor do AEM Forms** instância > **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Armazenamento do Azure]**.
1. Depois de selecionar a variável **[!UICONTROL Armazenamento do Azure]**, você será redirecionado para **[!UICONTROL Navegador de Armazenamento do Azure]**.
1. Selecione um **Contêiner de configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]**. O assistente Criar Configuração de Armazenamento do Azure é exibido.

   ![Configuração de Armazenamento do Azure](/help/forms/assets/azure-storage-configuration.png)

1. Especifique a **[!UICONTROL Título]**, **[!UICONTROL Conta de Armazenamento do Azure]** e **[!UICONTROL Chave de acesso do Azure]**.

   * Você pode recuperar `Azure Storage Account` nome e `Azure Access key` nas Contas de Armazenamento no portal do Microsoft Azure.

1. Clique em **[!UICONTROL Salvar]**.

Agora, você pode usar essa configuração do contêiner de Armazenamento do Azure para a ação de envio em um Formulário adaptável.

### Usar a configuração de armazenamento do Azure em um formulário adaptável {#use-azure-storage-configuartion-in-af}

Você pode usar a configuração criada do contêiner de Armazenamento do Azure em um Formulário adaptável, para salvar dados ou o Documento de registro gerado no contêiner de Armazenamento do Azure. Execute as seguintes etapas para usar a configuração do contêiner de Armazenamento do Azure em um Formulário adaptável como:
1. Crie um [Formulário adaptável](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Selecione o mesmo [!UICONTROL Contêiner de configuração] para um formulário adaptável, onde você criou o armazenamento do OneDrive.
   > * Se não [!UICONTROL Contêiner de configuração] for selecionada, em seguida, a variável global [!UICONTROL Configuração de armazenamento] As pastas são exibidas na janela de propriedades Enviar Ação.


1. Selecionar **Enviar ação** as **[!UICONTROL Enviar para o Armazenamento Azure Blob]**.
   ![GIF de Armazenamento Azure Blob](/help/forms/assets/azure-submit-video.gif)

1. Selecione o **[!UICONTROL Configuração de armazenamento]**, onde deseja salvar os dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Enviar.

Quando você envia o formulário, os dados são salvos na configuração especificada do contêiner de Armazenamento do Azure.
A estrutura de pastas para salvar dados é `/configuration_container/form_name/year/month/date/submission_id/data`.

Para definir valores de uma configuração, [Gerar configurações de OSGi usando o SDK AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)e [implantar a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) para a instância do Cloud Service.

## Usar envio síncrono ou assíncrono {#use-synchronous-or-asynchronous-submission}

Uma Ação de envio pode usar envio síncrono ou assíncrono.

**Envio síncrono**: Tradicionalmente, os formulários web são configurados para envio síncrono. Em um envio síncrono, quando os usuários enviam um formulário, ele é redirecionado para uma página de confirmação, uma página de agradecimento ou, se houver falha no envio, uma página de erro. Você pode selecionar a variável **[!UICONTROL Usar envio assíncrono]** opção para redirecionar os usuários para uma página da Web ou mostrar uma mensagem no envio.

![Configurar ação de envio](assets/thank-you-setting.png)

**Envio assíncrono**: Experiências modernas da Web, como aplicativos de página única, estão ganhando popularidade, onde a página da Web permanece estática, enquanto a interação cliente-servidor acontece em segundo plano. Agora você pode fornecer essa experiência com o Adaptive Forms [configuração do envio assíncrono](asynchronous-submissions-adaptive-forms.md).

## Revalidação do lado do servidor em forma adaptável {#server-side-revalidation-in-adaptive-form}

Normalmente, em qualquer sistema de captura de dados online, os desenvolvedores colocam algumas validações de JavaScript no lado do cliente para impor algumas regras de negócios. Mas nos navegadores modernos, os usuários finais têm como ignorar essas validações e fazer envios manualmente usando várias técnicas, como o Console DevTools do navegador Web. Essas técnicas também são válidas para o Adaptive Forms. Um desenvolvedor de formulários pode criar várias lógicas de validação, mas tecnicamente os usuários finais podem ignorar essas lógicas de validação e enviar dados inválidos para o servidor. Dados inválidos quebrariam as regras de negócios que um autor de formulários executou.

O recurso de revalidação do lado do servidor também permite executar as validações fornecidas por um autor do Adaptive Forms ao projetar um formulário adaptável no servidor. Impede qualquer possível comprometimento de envios de dados e violações de regras comerciais representadas em termos de validações de formulários.

### O que validar no Servidor? {#what-to-validate-on-server-br}

Todas as validações de campo prontas para uso (OOTB) de um Formulário adaptável que são executadas novamente no servidor são:

* Obrigatório
* Cláusula de Imagem de Validação
* Expressão de validação

### Habilitar validação do lado do servidor {#enabling-server-side-validation-br}

Use o **[!UICONTROL Revalidar no servidor]** em Contêiner de formulário adaptável na barra lateral para ativar ou desativar a validação do lado do servidor para o formulário atual.

![Ativação da validação no lado do servidor](assets/revalidate-on-server.png)

Ativação da validação no lado do servidor

Se o usuário final ignorar essas validações e enviar os formulários, o servidor executará novamente a validação. Se a validação falhar no final do servidor, a transação de envio será interrompida. O usuário final é apresentado ao formulário original novamente. Os dados capturados e enviados são apresentados ao usuário como um erro.

>[!NOTE]
>
>A validação do lado do servidor valida o modelo de formulário. É recomendável criar uma biblioteca cliente separada para validações e não misturá-la com outras coisas, como estilo de HTML e manipulação de DOM na mesma biblioteca do cliente.

### Suporte a funções personalizadas nas expressões de validação {#supporting-custom-functions-in-validation-expressions-br}

Às vezes, se houver **regras de validação complexas**, o script de validação exato reside em funções personalizadas e o autor chama essas funções personalizadas da expressão de validação de campo. Para tornar essa biblioteca de funções personalizada conhecida e disponível ao executar validações do lado do servidor, o autor do formulário pode configurar o nome AEM biblioteca do cliente no **[!UICONTROL Básico]** das propriedades do Contêiner de formulário adaptável, conforme mostrado abaixo.

![Suporte a funções personalizadas nas expressões de validação](assets/clientlib-cat.png)

Suporte a funções personalizadas nas expressões de validação

O autor pode configurar a biblioteca JavaScript personalizada por Formulário adaptável. Na biblioteca, mantenha somente as funções reutilizáveis, que têm dependência em bibliotecas de terceiros jquery e underscore.js.

## Tratamento de erros na ação Enviar {#error-handling-on-submit-action}

Como parte AEM diretrizes de segurança e proteção, configure páginas de erro personalizadas, como 400.jsp, 404.jsp e 500.jsp. Esses manipuladores são chamados quando um erro de formulário 400, 404 ou 500 é enviado. Os manipuladores também são chamados quando esses códigos de erro são acionados no nó Publicar . Você também pode criar páginas JSP para outros códigos de erro HTTP.

Ao preencher previamente um modelo de dados de formulário ou um formulário adaptável baseado em esquema com reclamação de dados XML ou JSON para um esquema que é dados não contém `<afData>`, `<afBoundData>`e `</afUnboundData>` , os dados dos campos não limitados do Formulário adaptável serão perdidos. O esquema pode ser um esquema XML, um esquema JSON ou um Modelo de dados de formulário. Campos não limitados são campos do Formulário adaptável sem a variável `bindref` propriedade.

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->
