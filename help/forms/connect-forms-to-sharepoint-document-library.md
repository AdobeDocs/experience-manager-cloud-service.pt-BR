---
Title: How to integrate Adaptive Form to a SharePoint Document Library?
Description: This article explains how to send data from your Adaptive Form to a SharePoint  Document library when you submit the form.
keywords: Como conectar a biblioteca de documentos do SharePoint para um formulário adaptável, Enviar para o SharePoint, Criar uma configuração da biblioteca de documentos do SharePoint, Usar a ação de envio Enviar para o SharePoint em um formulário adaptável, Biblioteca de documentos do SharePoint do modelo de dados do AEM Forms, Biblioteca de documentos do SharePoint do modelo de dados do Forms, Integrar o modelo de dados do Forms à biblioteca de documentos do SharePoint
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
role: User, Developer
exl-id: a00b4a93-2324-4c2a-824f-49146dc057b0
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---

# Conecte um formulário adaptável à Biblioteca de documentos Microsoft® SharePoint {#connect-af-sharepoint-doc-library}

>[!VIDEO](https://video.tv.adobe.com/v/3444368/formautomation-productivitytools-adaptiveforms--sharepointintegration-documentlibrary/?quality=12&learn=on)

Para usar a Ação Enviar **[!UICONTROL Enviar para a Biblioteca de Documentos do SharePoint]** em um Formulário adaptável:

1. [Criar uma Configuração da Biblioteca de Documentos da SharePoint](#1-create-a-sharepoint-document-library-configuration): ela conecta o AEM Forms ao Armazenamento do Microsoft® Sharepoint.
2. [Use a ação enviar para o SharePoint em um Formulário adaptável](#2-use-sharepoint-document-library-configuration-in-an-adaptive-form): ele conecta seu Formulário adaptável ao Microsoft® SharePoint configurado.

## &#x200B;1. Criar uma configuração da Biblioteca de documentos da SharePoint

Para conectar o AEM Forms ao seu armazenamento da Biblioteca de Documentos do Microsoft® Sharepoint:

1. Vá para sua instância do **AEM Forms Author** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® SharePoint]**.
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

1. O escopo de permissão `offline_access Sites.Selected` na API gráfica do Microsoft, que permite acesso mais granular e restrito aos sites do SharePoint. O escopo de permissão `offline_access Sites.Manage.All` na API gráfica do Microsoft que permite acesso total aos sites do SharePoint.
1. Clique em **[!UICONTROL Conectar]**. Em uma conexão bem-sucedida, a mensagem `Connection Successful` é exibida.

1. Agora, selecione **Site do SharePoint** > **Biblioteca de Documentos** > **Pasta do SharePoint** para salvar os dados.

   >[!NOTE]
   >
   >* Por padrão, `forms-ootb-storage-adaptive-forms-submission` está presente no site do SharePoint selecionado.
   >* Crie uma pasta como `forms-ootb-storage-adaptive-forms-submission`, se ainda não estiver presente na biblioteca `Documents` do Site do SharePoint selecionado clicando em **Criar Pasta**.

Agora, você pode usar essa configuração do SharePoint Sites para a ação enviar em um Formulário adaptável.

### &#x200B;2. Usar a configuração da Biblioteca de documentos da SharePoint em um formulário adaptável

Você pode usar a configuração criada da Biblioteca de documentos da SharePoint em um Formulário adaptável para salvar dados ou o Documento de registro gerado em uma pasta do SharePoint.

>[!NOTE]
>
> * Selecione o mesmo [!UICONTROL Contêiner de configuração] para um Formulário adaptável, onde você criou seu armazenamento da Biblioteca de documentos da SharePoint.
> * Se nenhum [!UICONTROL Contêiner de Configuração] for selecionado, as pastas de [!UICONTROL Configuração de Armazenamento] globais serão exibidas na janela de propriedades da Ação de Envio.

>[!BEGINTABS]

>[!TAB Componente de base]

Execute as seguintes etapas para usar uma configuração de armazenamento da Biblioteca de documentos da SharePoint em um formulário adaptável com base no componente de base como:

1. Abra o Formulário adaptável para edição e navegue até a seção **[!UICONTROL Envio]** das propriedades do Contêiner de formulário adaptável.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **Enviar Ação** como **[!UICONTROL Enviar para o SharePoint]**.
   ![Sharepoint GIF](/help/forms/assets/submit-to-sharepoint-fc.png){width=50%}
1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

>[!NOTE]
>
> * Ao enviar o formulário, os dados são salvos no Armazenamento da Biblioteca de Documentos do Microsoft® Sharepoint especificado. A estrutura de pasta para salvar dados é `/folder_name/form_name/year/month/date/submission_id/data`.
> * Os anexos também são armazenados no diretório `/folder_name/form_name/year/month/date/submission_id/data`. No entanto, se você selecionar **Salvar anexos com nome original**, os anexos serão armazenados na pasta usando seus nomes de arquivo originais.

>[!TAB Componente principal]

Execute as seguintes etapas para usar uma configuração de armazenamento da Biblioteca de documentos da SharePoint em um formulário adaptável com base no Componente principal como:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique na guia **[!UICONTROL Envio]**.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **Enviar Ação** como **[!UICONTROL Enviar para o SharePoint]**.
   ![Sharepoint GIF](/help/forms/assets/sharedrive-video.gif)
1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

>[!NOTE]
>
> * Ao enviar o formulário, os dados são salvos no Armazenamento da Biblioteca de Documentos do Microsoft® Sharepoint especificado. A estrutura de pasta para salvar dados é `/folder_name/form_name/year/month/date/submission_id/data`.
> * Os anexos também são armazenados no diretório `/folder_name/form_name/year/month/date/submission_id/data`. No entanto, se você selecionar **Salvar anexos com nome original**, os anexos serão armazenados na pasta usando seus nomes de arquivo originais.

>[!TAB Editor Universal]

Execute as seguintes etapas para usar uma configuração de armazenamento da Biblioteca de documentos da SharePoint em um formulário adaptável criado no Editor universal como:

1. Abra o Formulário adaptável para edição.
1. Clique na extensão **Editar propriedades do formulário** no editor.
A caixa de diálogo **Propriedades do Formulário** é exibida.

   >[!NOTE]
   >
   > * Se você não vir o ícone **Editar Propriedades do Formulário** na interface do Universal Editor, habilite a extensão **Editar Propriedades do Formulário** na Extension Manager.
   > * Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar ou desabilitar extensões no Universal Editor.

1. Clique na guia **Envio** e selecione a ação de envio **[!UICONTROL Enviar para o SharePoint]**.
   ![Sharepoint GIF](/help/forms/assets/submit-to-sharepoint-ue.png)
1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar&amp;Fechar]** para salvar as configurações de Envio.

>[!NOTE]
>
> * Ao enviar o formulário, os dados são salvos no Armazenamento da Biblioteca de Documentos do Microsoft® Sharepoint especificado. A estrutura de pasta para salvar dados é `/folder_name/form_name/year/month/date/submission_id/data`.
> * Os anexos também são armazenados no diretório `/folder_name/form_name/year/month/date/submission_id/data`. No entanto, se você selecionar **Salvar anexos com nome original**, os anexos serão armazenados na pasta usando seus nomes de arquivo originais.

>[!ENDTABS]

## Artigos relacionados

{{af-submit-action}}
