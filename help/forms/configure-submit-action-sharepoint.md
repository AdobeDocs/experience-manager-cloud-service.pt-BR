---
Title: How to send data to a SharePoint storage on submission of an Adaptive Form?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list or Document library when you submit the form.
keywords: Como conectar a lista do SharePoint para um formulário adaptável?, Como conectar a biblioteca de documentos do SharePoint para um formulário adaptável, Enviar para o SharePoint, Criar uma configuração da biblioteca de documentos do SharePoint, Usar a ação enviar Enviar para o SharePoint em um formulário adaptável, Conectar um formulário adaptável à lista do Microsoft&reg; SharePoint.
feature: Adaptive Forms, Core Components
exl-id: e925a750-5fb5-4950-afd3-78551eec985d
title: "Como configurar uma ação enviar para um formulário adaptável?"
role: User, Developer
source-git-commit: 5e1d08e82cafc3a8a715653727f42ce0048f2b1f
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---

# Conectar um formulário adaptável ao Microsoft® SharePoint

A ação de envio **[!UICONTROL Enviar para o SharePoint]** permite que você conecte facilmente seu Formulário adaptável a um armazenamento do Microsoft® SharePoint. Ele envia os dados do formulário para o armazenamento SharePoint de sua escolha depois que você envia o formulário.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md).

## Vantagens

Algumas das vantagens de enviar dados de um Formulário adaptável para o armazenamento do SharePoint são:

* Ele facilita o envio direto de dados de formulário para o SharePoint, fornecendo um local centralizado para armazenar e gerenciar informações.
* Ao aplicar os recursos de controle de acesso e permissões do SharePoint, ele garante que somente indivíduos autorizados possam visualizar ou modificar os dados enviados.

Usando o **[!UICONTROL Enviar para o SharePoint]**, você pode:

* [Conectar um formulário adaptável à biblioteca de documentos do SharePoint](#connect-af-sharepoint-doc-library)
* [Conectar um formulário adaptável à lista do SharePoint](#connect-af-sharepoint-list)

## Conectar um formulário adaptável à biblioteca de documentos do SharePoint {#connect-af-sharepoint-doc-library}

Para usar a Ação Enviar **[!UICONTROL Enviar para a Biblioteca de Documentos do SharePoint]** em um Formulário adaptável:

1. [Criar uma Configuração da Biblioteca de Documentos da SharePoint](#create-a-sharepoint-configuration-create-sharepoint-configuration): ela conecta o AEM Forms ao Armazenamento do Microsoft® Sharepoint.
2. [Use a ação enviar para o SharePoint em um Formulário adaptável](#use-sharepoint-configuartion-in-af): ele conecta seu Formulário adaptável ao Microsoft® SharePoint configurado.

### Criar uma configuração da Biblioteca de documentos da SharePoint {#create-sharepoint-configuration}

Para conectar o AEM Forms ao seu armazenamento da Biblioteca de Documentos do Microsoft® Sharepoint:

1. Vá para sua instância do **AEM Forms Author** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft® SharePoint]**.
1. Após selecionar o **[!UICONTROL Microsoft® SharePoint]**, você será redirecionado para o **[!UICONTROL Navegador SharePoint]**.
1. Selecione um **Contêiner de Configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]** > **[!UICONTROL Biblioteca de Documentos da SharePoint]** na lista suspensa. O assistente de configuração do SharePoint é exibido.

   ![Configuração do SharePoint](/help/forms/assets/sharepoint_configuration.png)
1. Especifique o **[!UICONTROL Título]**, **[!UICONTROL ID do Cliente]**, **[!UICONTROL Segredo do Cliente]** e **[!UICONTROL URL do OAuth]**. Para obter informações sobre como recuperar a ID do cliente, o Segredo do cliente e a ID do locatário para a URL do OAuth, consulte a [Documentação da Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Você pode recuperar os `Client ID` e `Client Secret` de seu aplicativo do portal do Microsoft® Azure.
   * No portal do Microsoft® Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Substitua `[author-instance]` pela URL da sua instância de Autor.
   * Adicione as permissões de API `offline_access` e `Sites.Manage.All` para fornecer permissões de leitura/gravação. O `Sites.Manage.All` é um escopo de permissão na API Graph do Microsoft que concede a um aplicativo a capacidade de gerenciar todos os aspectos dos Sites do SharePoint, como excluir ou modificar Sites.

     >[!NOTE]
     >
     > Você também pode [configurar os Sites do SharePoint com acesso limitado](/help/forms/configure-sharepoint-site-limited-access.md) usando o escopo de permissão `Sites.Selected` na API gráfica do Microsoft. O `Sites.Selected` é um escopo de permissão na API gráfica do Microsoft que permite acesso mais granular e restrito aos sites do SharePoint.

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

### Usar a configuração da biblioteca de documentos SharePoint em um formulário adaptável {#use-sharepoint-configuartion-in-af}

Você pode usar a configuração criada da Biblioteca de documentos da SharePoint em um Formulário adaptável para salvar dados ou o Documento de registro gerado em uma pasta do SharePoint. Execute as seguintes etapas para usar uma configuração de armazenamento da Biblioteca de documentos da SharePoint em um Formulário adaptável como:

1. Crie um [Formulário adaptável](/help/forms/creating-adaptive-form-core-components.md).

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

## Conectar um formulário adaptável à lista Microsoft® SharePoint {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

Para usar a ação enviar [!UICONTROL Enviar para a Lista do SharePoint] em um formulário adaptável:

1. [Criar uma Configuração de Lista do SharePoint](#create-sharepoint-list-configuration): ela conecta o AEM Forms ao Armazenamento de Lista do Microsoft® Sharepoint.
1. [Usar o Enviar usando o Modelo de Dados de Formulário (FDM) em um Formulário Adaptável](#use-submit-using-fdm): ele conecta seu Formulário Adaptável ao Microsoft® SharePoint configurado.

### Criar uma configuração de lista do SharePoint {#create-sharepoint-list-configuration}

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
