---
Title: How to send data to a SharePoint storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list or Document library when you submit the form.
keywords: Como conectar a lista do SharePoint para um formulário adaptável?, Como conectar a biblioteca de documentos do SharePoint para um formulário adaptável, Enviar para o SharePoint, Criar uma configuração da biblioteca de documentos do SharePoint, Usar a ação enviar Enviar para o SharePoint em um formulário adaptável, Conectar um formulário adaptável à lista do Microsoft&reg; SharePoint.
feature: Adaptive Forms, Core Components
exl-id: e925a750-5fb5-4950-afd3-78551eec985d
title: "Como configurar uma ação enviar para um formulário adaptável?"
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# Conectar um formulário adaptável ao Microsoft® SharePoint

A variável **[!UICONTROL Enviar para o SharePoint]** A ação enviar permite conectar facilmente o Formulário adaptável com um armazenamento Microsoft® SharePoint. Ele envia os dados do formulário para o armazenamento SharePoint de sua escolha depois que você envia o formulário.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções na [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md)  artigo.

## Vantagens

Algumas das vantagens de enviar dados de um Formulário adaptável para o armazenamento do SharePoint são:

* Ele facilita o envio direto de dados de formulário para o SharePoint, fornecendo um local centralizado para armazenar e gerenciar informações.
* Ao aplicar os recursos de controle de acesso e permissões do SharePoint, ele garante que somente indivíduos autorizados possam visualizar ou modificar os dados enviados.

Usar **[!UICONTROL Enviar para o SharePoint]**, você pode:

* [Conectar um formulário adaptável à biblioteca de documentos do SharePoint](#connect-af-sharepoint-doc-library)
* [Conectar um formulário adaptável à lista do SharePoint](#connect-af-sharepoint-list)

## Conectar um formulário adaptável à biblioteca de documentos do SharePoint {#connect-af-sharepoint-doc-library}

Para usar o **[!UICONTROL Enviar para a Biblioteca de documentos da SharePoint]** Enviar ação em um formulário adaptável:

1. [Criar uma configuração da biblioteca de documentos da SharePoint](#create-a-sharepoint-configuration-create-sharepoint-configuration): ele conecta o AEM Forms ao seu Microsoft® Sharepoint Storage.
2. [Usar a ação enviar Enviar para o SharePoint em um Formulário adaptável](#use-sharepoint-configuartion-in-af): ele conecta seu formulário adaptável ao Microsoft® SharePoint configurado.

### Criar uma configuração da Biblioteca de documentos da SharePoint {#create-sharepoint-configuration}

Para conectar o AEM Forms ao seu armazenamento da Biblioteca de Documentos do Microsoft® Sharepoint:

1. Vá para o **Autor do AEM Forms** instância > **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. Depois de selecionar a variável **[!UICONTROL Microsoft® SharePoint]**, você será redirecionado para **[!UICONTROL Navegador SharePoint]**.
1. Selecione um **Contêiner de configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]** > **[!UICONTROL Biblioteca de documentos da SharePoint]** na lista suspensa. O assistente de configuração do SharePoint é exibido.

   ![Configuração do Sharepoint](/help/forms/assets/sharepoint_configuration.png)
1. Especifique a **[!UICONTROL Título]**, **[!UICONTROL ID do cliente]**, **[!UICONTROL Segredo do cliente]** e **[!UICONTROL URL do OAuth]**. Para obter informações sobre como recuperar a ID do cliente, o Segredo do cliente e a ID do locatário para o URL do OAuth, consulte [Documentação Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Você pode recuperar a variável `Client ID` e `Client Secret` do seu aplicativo no portal do Microsoft® Azure.
   * No portal do Microsoft® Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Substituir `[author-instance]` com o URL da sua instância do Author.
   * Adicionar as permissões da API `offline_access` e `Sites.Manage.All` para fornecer permissões de leitura/gravação.
   * Usar URL do OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substituir `<tenant-id>` com o `tenant-id` do seu aplicativo no portal do Microsoft® Azure.

   >[!NOTE]
   >
   > A variável **segredo do cliente** é obrigatório ou opcional depende da configuração do aplicativo do Azure Ative Diretory. Se o aplicativo estiver configurado para usar um segredo do cliente, é obrigatório fornecer o segredo do cliente.

1. Clique em **[!UICONTROL Conectar]**. Em uma conexão bem-sucedida, a variável `Connection Successful` é exibida.

1. Agora, selecione **Site do SharePoint** > **Biblioteca de documentos** > **Pasta do SharePoint**, para salvar os dados.

   >[!NOTE]
   >
   >* Por padrão, `forms-ootb-storage-adaptive-forms-submission` está presente no site do SharePoint selecionado.
   >* Criar uma pasta como `forms-ootb-storage-adaptive-forms-submission`, se ainda não estiver presente no `Documents` do site do SharePoint selecionado clicando em **Criar pasta**.

Agora, você pode usar essa configuração do SharePoint Sites para a ação enviar em um Formulário adaptável.

### Usar a configuração da biblioteca de documentos SharePoint em um formulário adaptável {#use-sharepoint-configuartion-in-af}

Você pode usar a configuração criada da Biblioteca de documentos da SharePoint em um Formulário adaptável para salvar dados ou o Documento de registro gerado em uma pasta do SharePoint. Execute as seguintes etapas para usar uma configuração de armazenamento da Biblioteca de documentos da SharePoint em um Formulário adaptável como:

1. Criar um [Formulário adaptável](/help/forms/creating-adaptive-form-core-components.md).

   >[!NOTE]
   >
   > * Selecionar o mesmo [!UICONTROL Contêiner de configuração] para um Formulário adaptável, em que você criou o armazenamento da Biblioteca de documentos da SharePoint.
   > * Se não [!UICONTROL Contêiner de configuração] for selecionada, a variável global [!UICONTROL Configuração de armazenamento] pastas são exibidas na janela de propriedades Submeter Ação.

1. Selecionar **Ação de envio** as **[!UICONTROL Enviar para o SharePoint]**.
   ![GIF do Sharepoint](/help/forms/assets/sharedrive-video.gif)
1. Selecione o **[!UICONTROL Configuração de armazenamento]**, onde deseja salvar os dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

Ao enviar o formulário, os dados são salvos no Armazenamento da Biblioteca de Documentos do Microsoft® Sharepoint especificado.
A estrutura de pastas para salvar os dados é `/folder_name/form_name/year/month/date/submission_id/data`.

## Conectar um formulário adaptável à lista Microsoft® SharePoint {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

Para usar o [!UICONTROL Enviar para a lista do SharePoint] Enviar ação em um formulário adaptável:

1. [Criar uma configuração de lista do SharePoint](#create-sharepoint-list-configuration): ele conecta o AEM Forms ao seu Armazenamento de lista do Microsoft® Sharepoint.
1. [Usar o Enviar usando o Modelo de dados de formulário (FDM) em um formulário adaptável](#use-submit-using-fdm): ele conecta seu formulário adaptável ao Microsoft® SharePoint configurado.

### Criar uma configuração de lista do SharePoint {#create-sharepoint-list-configuration}

Para conectar o AEM Forms à sua lista do Microsoft® Sharepoint:

1. Ir para **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. Selecione um **Contêiner de configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]** > **[!UICONTROL Lista do SharePoint]** na lista suspensa. O assistente de configuração do SharePoint é exibido.
1. Especifique a **[!UICONTROL Título]**, **[!UICONTROL ID do cliente]**, **[!UICONTROL Segredo do cliente]** e **[!UICONTROL URL do OAuth]**. Para obter informações sobre como recuperar a ID do cliente, o Segredo do cliente e a ID do locatário para o URL do OAuth, consulte [Documentação Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Você pode recuperar a variável `Client ID` e `Client Secret` do seu aplicativo no portal do Microsoft® Azure.
   * No portal do Microsoft® Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Substituir `[author-instance]` com o URL da sua instância do Author.
   * Adicionar as permissões da API `offline_access` e `Sites.Manage.All` no **Gráfico Microsoft®** para fornecer permissões de leitura/gravação. Adicionar `AllSites.Manage` permissão na **Sharepoint** para interagir remotamente com os dados do SharePoint.
   * Usar URL do OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substituir `<tenant-id>` com o `tenant-id` do seu aplicativo no portal do Microsoft® Azure.

     >[!NOTE]
     >
     > A variável **segredo do cliente** é obrigatório ou opcional depende da configuração do aplicativo do Azure Ative Diretory. Se o aplicativo estiver configurado para usar um segredo do cliente, é obrigatório fornecer o segredo do cliente.

1. Clique em **[!UICONTROL Conectar]**. Em uma conexão bem-sucedida, a variável `Connection Successful` é exibida.
1. Selecionar **[!UICONTROL Site do SharePoint]** e **[!UICONTROL Lista do SharePoint]** na lista suspensa.
1. Selecionar **[!UICONTROL Criar]** para criar a configuração de nuvem do Microsoft® SharePointList.


### Usar o Enviar usando o Modelo de dados de formulário (FDM) em um formulário adaptável {#use-submit-using-fdm}

Você pode usar a configuração da Lista do SharePoint criada em um Formulário adaptável para salvar dados ou o Documento de registro gerado em uma Lista do SharePoint. Execute as seguintes etapas para usar uma Lista SharePoint em um Formulário adaptável como:

1. [Criar um modelo de dados de formulário (FDM) usando o Microsoft](/help/forms/create-form-data-models.md)
1. [Configurar o Modelo de dados de formulário (FDM) para recuperar e enviar dados](/help/forms/work-with-form-data-model.md#configure-services)
1. [Criação de um Formulário adaptável](/help/forms/creating-adaptive-form-core-components.md)
1. [Configurar a ação Enviar usando um Modelo de dados de formulário (FDM)](/help/forms/using-form-data-model.md)

Ao enviar o formulário, os dados são salvos no Armazenamento de Lista do Microsoft® Sharepoint especificado.

>[!NOTE]
>
> Na Lista do Microsoft® SharePoint, os seguintes tipos de coluna não são suportados:
> * coluna de imagem
> * coluna de metadados
> * coluna de pessoa
> * coluna de dados externos

## Artigos relacionados

{{af-submit-action}}
