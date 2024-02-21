---
Title: How to submit data from an Adaptive Form to Microsoft® OneDrive?
Description: Explore the streamlined process of connecting AEM Forms with Microsoft® OneDrive using the Submit to OneDrive Submit Action. Learn the step-by-step guide to configure OneDrive and set up submission actions for efficient data storage and retrieval
keywords: Integração do AEM Forms OneDrive, Conectar-se ao Microsoft OneDrive, Configuração do OneDrive com formulários AEM
feature: Adaptive Forms, Core Components
source-git-commit: 20458e710502e445cf5c8f582a1d183bdac75c8d
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# Enviar um formulário adaptável ao Microsoft® OneDrive

A variável **[!UICONTROL Enviar para o OneDrive]** A ação enviar conecta um formulário adaptável a um Microsoft® OneDrive. Você pode enviar dados de formulário, arquivos, anexos ou Documento de registro para o Microsoft® OneDrive Storage conectado.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções na [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md)  artigo.

## Vantagens

Algumas das vantagens da integração perfeita entre o AEM Forms e o Microsoft® OneDrive são:

* A acessibilidade entre dispositivos do OneDrive garante que os dados de formulário armazenados estejam prontamente disponíveis em plataformas diferentes. Os usuários podem acessar os dados, anexos e documentos enviados a partir de desktops, laptops, tablets e dispositivos móveis, melhorando a acessibilidade e a flexibilidade.
* A integração do OneDrive com formulários AEM fornece uma solução confiável e escalável para um armazenamento de dados eficiente. Todos os envios de formulários adaptáveis, como arquivos, anexos e documentos de registro, podem ser convenientemente salvos no OneDrive, garantindo dados organizados e acessíveis.

## Conectar o OneDrive a um Formulário adaptável

>[!VIDEO](https://video.tv.adobe.com/v/3424864/connect-aem-adaptive-form-to-onedrive/?quality=12&learn=on)

Configurando o envio do OneDrive for AEM Forms, execute as seguintes etapas:

1. [Criar uma Configuração do OneDrive](#create-a-onedrive-configuration-create-onedrive-configuration): ele conecta o AEM Forms ao seu Microsoft® OneDrive Storage.
2. [Usar a ação de envio Enviar para o OneDrive em um Formulário adaptável](#use-onedrive-configuration-in-an-adaptive-form-use-onedrive-configuartion-in-af): ele conecta seu formulário adaptável ao Microsoft® OneDrive configurado.

### Criar uma Configuração do OneDrive {#create-onedrice-configuration}

Para conectar o AEM Forms ao seu Microsoft® OneDrive Storage:

1. Vá para o **Autor do AEM Forms** instância > **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® OneDrive]**.
1. Depois de selecionar a variável **[!UICONTROL Microsoft® OneDrive]**, você será redirecionado para **[!UICONTROL Navegador do OneDrive]**.
1. Selecione um **Contêiner de configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]**. O assistente de configuração do OneDrive é exibido.

   ![Tela de Configuração do OneDrive](/help/forms/assets/onedrive-configuration.png)

1. Especifique a **[!UICONTROL Título]**, **[!UICONTROL ID do cliente]**, **[!UICONTROL Segredo do cliente]** e **[!UICONTROL URL do OAuth]**. Para obter informações sobre como recuperar a ID do cliente, o Segredo do cliente e a ID do locatário para o URL do OAuth, consulte [Documentação Microsoft®](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
   * Você pode recuperar a variável `Client ID` e `Client Secret` do seu aplicativo no portal do Microsoft® Azure.
   * No portal do Microsoft® Azure, adicione o URI de redirecionamento como `https://[author-instance]/libs/cq/onedrive/content/configurations/wizard.html`. Substituir `[author-instance]` com o URL da sua instância do Author.
   * Adicionar as permissões da API `offline_access` e `Files.ReadWrite.All` para fornecer permissões de leitura/gravação.
   * Usar URL do OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Substituir `<tenant-id>` com o `tenant-id` do seu aplicativo no portal do Microsoft® Azure.

   >[!NOTE]
   >
   > A variável **segredo do cliente** é obrigatório ou opcional depende da configuração do aplicativo do Azure Ative Diretory. Se o aplicativo estiver configurado para usar um segredo do cliente, é obrigatório fornecer o segredo do cliente.

1. Clique em **[!UICONTROL Conectar]**. Em uma conexão bem-sucedida, a variável `Connection Successful` é exibida.

1. Agora, selecione **[!UICONTROL Container do OneDrive]** > **[Pasta do OneDrive]**  para salvar os dados.

   >[!NOTE]
   >
   >* Por padrão, `forms-ootb-storage-adaptive-forms-submission` está presente no OneDrive Container.
   > * Criar uma pasta como `forms-ootb-storage-adaptive-forms-submission`, se ainda não estiver presente clicando em **Criar pasta**.

Agora, você pode usar esta configuração de armazenamento do OneDrive para a ação de envio em um Formulário adaptável.

### Usar a configuração do OneDrive em um formulário adaptável {#use-onedrive-configuartion-in-af}

Você pode usar a configuração de armazenamento do OneDrive criada em um Formulário adaptável para salvar dados ou o Documento de Registro gerado em uma pasta do OneDrive. Execute as seguintes etapas para usar a configuração de armazenamento do OneDrive em um Formulário adaptável como:
1. Criar um [Formulário adaptável](/help/forms/creating-adaptive-form.md).

   >[!NOTE]
   >
   > * Selecionar o mesmo [!UICONTROL Contêiner de configuração] para um Formulário adaptável, em que você criou seu armazenamento do OneDrive.
   > * Se não [!UICONTROL Contêiner de configuração] for selecionada, a variável global [!UICONTROL Configuração de armazenamento] pastas são exibidas na janela de propriedades Submeter Ação.

1. Selecionar **Ação de envio** as **[!UICONTROL Enviar para o OneDrive]**.
   ![GIF do OneDrive](/help/forms/assets/onedrive-video.gif)
1. Selecione o **[!UICONTROL Configuração de armazenamento]**, onde deseja salvar os dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

Ao enviar o formulário, os dados são salvos no Armazenamento do Microsoft® OneDrive especificado.
A estrutura de pastas para salvar os dados é `/folder_name/form_name/year/month/date/submission_id/data`.

## Artigos relacionados

{{af-submit-action}}