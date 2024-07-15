---
Title: How to submit data from an Adaptive Form to Microsoft® OneDrive?
Description: Explore the streamlined process of connecting AEM Forms with Microsoft® OneDrive using the Submit to OneDrive Submit Action. Learn the step-by-step guide to configure OneDrive and set up submission actions for efficient data storage and retrieval
keywords: Integração do AEM Forms OneDrive, Conectar-se ao Microsoft OneDrive, Configuração do OneDrive com formulários AEM
feature: Adaptive Forms, Core Components
exl-id: dbfa4094-1b92-4a7c-a799-f66973d27054
title: "Como configurar uma ação enviar para um formulário adaptável?"
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Enviar um formulário adaptável ao Microsoft® OneDrive

A Ação de Envio **[!UICONTROL Enviar para o OneDrive]** conecta um Formulário adaptável com um Microsoft® OneDrive. Você pode enviar dados de formulário, arquivos, anexos ou Documento de registro para o Microsoft® OneDrive Storage conectado.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md).

## Vantagens

Algumas das vantagens da integração perfeita entre o AEM Forms e o Microsoft® OneDrive são:

* A acessibilidade entre dispositivos do OneDrive garante que os dados de formulário armazenados estejam prontamente disponíveis em plataformas diferentes. Os usuários podem acessar os dados, anexos e documentos enviados a partir de desktops, laptops, tablets e dispositivos móveis, melhorando a acessibilidade e a flexibilidade.
* A integração do OneDrive com formulários AEM fornece uma solução confiável e escalável para um armazenamento de dados eficiente. Todos os envios de formulários adaptáveis, como arquivos, anexos e documentos de registro, podem ser convenientemente salvos no OneDrive, garantindo dados organizados e acessíveis.

## Conectar o OneDrive a um Formulário adaptável

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

Configurando o envio do OneDrive for AEM Forms, execute as seguintes etapas:

1. [Criar uma Configuração do OneDrive](#create-a-onedrive-configuration-create-onedrive-configuration): ela conecta o AEM Forms ao seu Microsoft® OneDrive Storage.
2. [Use a ação de envio Enviar para o OneDrive em um Formulário Adaptável](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): ele conecta seu Formulário Adaptável ao Microsoft® OneDrive configurado.

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

## Artigos relacionados

{{af-submit-action}}
