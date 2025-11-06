---
title: Como enviar dados de um formulário adaptável para o Microsoft&reg; OneDrive?
description: Explore o processo simplificado de conexão do AEM Forms com o Microsoft&reg; OneDrive usando a Ação de envio Enviar para o OneDrive. Saiba mais sobre o guia passo a passo para configurar o OneDrive e definir ações de envio para obter armazenamento e recuperação de dados eficientes
keywords: Integração do AEM Forms OneDrive, Conectar-se ao Microsoft OneDrive, Configuração do OneDrive com formulários do AEM
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
exl-id: dbfa4094-1b92-4a7c-a799-f66973d27054
role: User, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 1%

---

# Enviar um formulário adaptável ao Microsoft® OneDrive

A Ação de Envio **[!UICONTROL Enviar para o OneDrive]** conecta um Formulário adaptável com um Microsoft® OneDrive. Você pode enviar dados de formulário, arquivos, anexos ou Documento de registro para o Microsoft® OneDrive Storage conectado.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/aem-forms-submit-action.md).

## Vantagens

Algumas das vantagens da integração perfeita entre o AEM Forms e o Microsoft® OneDrive são:

* A acessibilidade entre dispositivos do OneDrive garante que os dados de formulário armazenados estejam prontamente disponíveis em plataformas diferentes. Os usuários podem acessar os dados, anexos e documentos enviados a partir de desktops, laptops, tablets e dispositivos móveis, melhorando a acessibilidade e a flexibilidade.
* A integração do OneDrive com o AEM Forms fornece uma solução confiável e escalável para um armazenamento de dados eficiente. Todos os envios de formulários adaptáveis, como arquivos, anexos e documentos de registro, podem ser convenientemente salvos no OneDrive, garantindo dados organizados e acessíveis.

## Conectar o OneDrive a um Formulário adaptável

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

<span> Este vídeo se aplica somente aos Componentes principais. Para Componentes UE/Foundation, consulte o artigo.</span>

Configurando o envio do OneDrive for AEM Forms, execute as seguintes etapas:

1. [Criar uma Configuração do OneDrive](#create-a-onedrive-configuration-create-onedrive-configuration): ela conecta o AEM Forms ao seu Microsoft® OneDrive Storage.
2. [Use a ação de envio Enviar para o OneDrive em um Formulário Adaptável](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): ele conecta seu Formulário Adaptável ao Microsoft® OneDrive configurado.

### Criar uma Configuração do OneDrive {#create-onedrice-configuration}

Para conectar o AEM Forms ao seu Microsoft® OneDrive Storage:

1. Vá para sua **instância do AEM Forms Author** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® OneDrive]**.
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
   >* Crie uma pasta como `forms-ootb-storage-adaptive-forms-submission`, se ainda não estiver presente, clicando em **Criar Pasta**.

Agora, você pode usar esta configuração de armazenamento do OneDrive para a ação de envio em um Formulário adaptável.

### Usar a configuração do OneDrive em um formulário adaptável {#use-onedrive-configuartion-in-af}

Você pode usar a configuração de armazenamento do OneDrive criada em um Formulário adaptável para salvar dados ou o Documento de Registro gerado em uma pasta do OneDrive.

>[!NOTE]
>
> * Selecione o mesmo [!UICONTROL Contêiner de Configuração] para um Formulário Adaptável, onde você criou seu armazenamento do OneDrive.
> * Se nenhum [!UICONTROL Contêiner de Configuração] for selecionado, as pastas de [!UICONTROL Configuração de Armazenamento] globais serão exibidas na janela de propriedades da Ação de Envio.

>[!BEGINTABS]

>[!TAB Componente de base]

Execute as seguintes etapas para usar a configuração de armazenamento do OneDrive em um Formulário adaptável com base no Componente de base como:

1. Abra o Formulário adaptável para edição e navegue até a seção **[!UICONTROL Envio]** das propriedades do Contêiner de formulário adaptável.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **[!UICONTROL Enviar para o OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/wubmit-to-onedrive-fc.png){width=50%,height=50%}
Você também pode salvar o Documento de registro (DoR) no OneDrive.
1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

Ao enviar o formulário, os dados são salvos no Armazenamento do Microsoft® OneDrive especificado.
A estrutura de pasta para salvar dados é `/folder_name/form_name/year/month/date/submission_id/data`.

>[!TAB Componente principal]

Execute as seguintes etapas para usar a configuração de armazenamento do OneDrive em um Formulário adaptável com base no Componente principal como:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique na guia **[!UICONTROL Envio]**.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **[!UICONTROL Enviar para o OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/onedrive-video.gif)
Você também pode salvar o Documento de registro (DoR) no OneDrive.
1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

>[!TAB Universal Editor]

Execute as seguintes etapas para usar a configuração de armazenamento do OneDrive em um Formulário adaptável criado no Universal Editor:

1. Abra o Formulário adaptável para edição.
1. Clique na extensão **Editar propriedades do formulário** no editor.
A caixa de diálogo **Propriedades do Formulário** é exibida.

   >[!NOTE]
   >
   > * Se você não vir o ícone **Editar Propriedades do Formulário** na interface do Universal Editor, habilite a extensão **Editar Propriedades do Formulário** na Extension Manager.
   > * Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar ou desabilitar extensões no Universal Editor.
1. Clique na guia **Envio** e selecione **[!UICONTROL Enviar para o OneDrive]**.
   ![OneDrive GIF](/help/forms/assets/submit-to-onedrive-ue.png)
Se você selecionar **Salvar anexos com nome original**, os anexos serão armazenados na pasta usando seus nomes de arquivo originais. Você também pode salvar o Documento de registro (DoR) no Armazenamento de blobs do Azure.
1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar&amp;Fechar]**

>[!ENDTABS]

## Artigos relacionados

{{af-submit-action}}
