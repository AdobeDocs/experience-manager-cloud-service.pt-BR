---
title: Como enviar dados para um armazenamento de Lista do SharePoint no envio de um Formulário adaptável?
Description: Learn how to send data from your Adaptive Form to a SharePoint storage like a SharePoint list when you submit the form.
keywords: Como conectar a lista do SharePoint para um formulário adaptável?, Enviar para o SharePoint, Criar uma configuração de lista do SharePoint, Usar a ação enviar Enviar para o SharePoint em um formulário adaptável, Conectar um formulário adaptável à lista do Microsoft&reg; SharePoint.
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
role: User, Developer
exl-id: 9ac3e7be-c6fa-4dbc-9aba-b81741ba6c55
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 1%

---

# Conectar um formulário adaptável à lista Microsoft® SharePoint {#connect-af-sharepoint-list}

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

<span> Este vídeo se aplica somente aos Componentes principais. Para Componentes UE/Foundation, consulte o artigo.</span>

Para usar a ação enviar [!UICONTROL Enviar para a Lista do SharePoint] em um formulário adaptável:

1. [Criar uma Configuração de Lista do SharePoint](#1-create-a-sharepoint-list-configuration): ela conecta o AEM Forms ao Armazenamento de Lista do Microsoft® Sharepoint.
1. [Usar o Enviar usando o Modelo de Dados de Formulário (FDM) em um Formulário Adaptável](#2-use-the-submit-using-form-data-model-fdm-in-an-adaptive-form-use-submit-using-fdm): ele conecta seu Formulário Adaptável ao Microsoft® SharePoint configurado.

## &#x200B;1. Criar uma configuração de lista do SharePoint

Para conectar o AEM Forms à sua lista do Microsoft® Sharepoint:

1. Vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Serviços na Nuvem]** > **[!UICONTROL Microsoft® SharePoint]**.
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


## &#x200B;2. Usar o Enviar usando o Modelo de dados de formulário (FDM) em um Formulário adaptável {#use-submit-using-fdm}

Você pode usar a configuração da Lista do SharePoint criada em um Formulário adaptável para salvar dados ou o Documento de registro gerado em uma Lista do SharePoint. Execute as seguintes etapas para usar uma Lista SharePoint em um Formulário adaptável como:

1. [Criar um modelo de dados de formulário (FDM) usando o Microsoft](/help/forms/create-form-data-models.md)
1. [Configurar o Modelo de dados de formulário (FDM) para recuperar e enviar dados](/help/forms/work-with-form-data-model.md#configure-services)
1. [Criação de um Formulário adaptável](/help/forms/creating-adaptive-form-core-components.md)
1. [Configurar a ação Enviar usando um Modelo de dados de formulário (FDM)](/help/forms/using-form-data-model.md)

Ao enviar o formulário, os dados são salvos no Armazenamento de Lista do Microsoft® Sharepoint especificado.

>[!NOTE]
>
> Na Lista do Microsoft® SharePoint, os seguintes tipos de coluna não são suportados:
>
> * coluna de imagem
> * coluna de metadados
> * coluna de pessoa
> * coluna de dados externos

## Artigos relacionados

{{af-submit-action}}
