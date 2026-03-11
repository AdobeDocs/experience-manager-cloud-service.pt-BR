---
title: Como conectar o AEM Adaptive Forms ao Azure Blob Storage?
description: Saiba como criar uma configuração do Azure Blob Storage no AEM Forms e usá-la em seu Adaptive Forms para um armazenamento de dados eficiente.
keywords: Integração do Azure Blob Storage com o AEM Forms, envio de dados para o Azure Storage, criação da configuração do Azure Storage no AEM Forms, uso do Azure Blob Storage na ação enviar do Adaptive Forms
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
badgeSaas: label="AEM Forms" type="Positive" tooltip="Aplicável ao AEM Forms)."
exl-id: 0c9f8f85-c4e9-4c79-bd0b-abdcac99a2d4
role: User, Developer
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 1%

---

# Enviar um formulário adaptável para o Armazenamento de blobs do Azure

A ação enviar **[!UICONTROL Enviar para o Azure Blob Storage]** conecta um formulário adaptável a um portal Microsoft® Azure. É possível enviar os dados do formulário, arquivos, anexos ou Documento de registro para os contêineres conectados do Azure Storage.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/aem-forms-submit-action.md).

## Vantagens

Algumas das vantagens da integração do Azure Blob Storage com o AEM Forms são:

* Isso ajuda a simplificar o processo de envio de dados, arquivos, anexos e documentos de registro do formulário adaptável para os contêineres de armazenamento da Azure.
* Ele usa o Azure Blob Storage para o armazenamento centralizado e organizado de envios de formulários adaptáveis.

## Conecte o AEM Forms com o Microsoft® Azure Blob Storage

Para usar o Azure Blob Storage na ação enviar do Adaptive Forms:

1. [Criar um Contêiner de Armazenamento Azure Blob](#create-a-azure-blob-storage-container-create-azure-configuration): ele conecta o AEM Forms aos contêineres de Armazenamento Azure.
2. [Usar a Configuração de Armazenamento do Azure em um Formulário Adaptável](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): ela conecta o Formulário Adaptável aos contêineres configurados do Azure Storage.

### Criar um contêiner de armazenamento do Azure Blob {#create-azure-configuration}

Para conectar o AEM Forms aos seus contêineres de Armazenamento do Azure:

1. Vá para sua instância do **AEM Forms Author** > **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure Storage]**.
1. Após selecionar o **[!UICONTROL Azure Storage]**, você será redirecionado para o **[!UICONTROL Azure Storage Browser]**.
1. Selecione um **Contêiner de Configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]**. O assistente Criar configuração de armazenamento do Azure é exibido.

   ![Configuração de Armazenamento do Azure](/help/forms/assets/azure-storage-configuration.png)

1. Especifique o **[!UICONTROL Título]**, a **[!UICONTROL Conta de Armazenamento da Azure]** e a **[!UICONTROL Chave de Acesso da Azure]**.

   * Você pode recuperar o nome de `Azure Storage Account` e `Azure Access key` das Contas de Armazenamento no portal Microsoft® Azure.
<!--

    >[!NOTE]
    >
    > The URL for **[!UICONTROL Azure Blob Endpoint]** is automatically appended to the textbox when a value is entered for **[!UICONTROL Azure Storage Account]**. You can update the Azure Blob End Point URL with your custom domain. Steps to update URL for **[!UICONTROL Azure Blob End Point]**:
    > 1. [Enable the AEM Advance Networking VPN support](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=pt-BR)
    > 1. [Enable dedicated egress IP link](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html?lang=pt-BR)
    > 1. [Map custom domain to azure blob storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal)
-->

1. Clique em **[!UICONTROL Salvar]**.

Agora, você pode usar essa configuração do contêiner de Armazenamento do Azure para a ação de envio em um Formulário adaptável.

### Usar a configuração de armazenamento do Azure em um formulário adaptável {#use-azure-storage-configuartion-in-af}

Você pode usar a configuração criada do contêiner de Armazenamento do Azure em um Formulário adaptável para salvar dados ou o Documento de registro gerado no contêiner de Armazenamento do Azure.

>[!NOTE]
>
> * Selecione o mesmo [!UICONTROL Contêiner de Configuração] para um Formulário Adaptável, onde você criou seu armazenamento do OneDrive.
> * Se nenhum [!UICONTROL Contêiner de Configuração] for selecionado, as pastas de [!UICONTROL Configuração de Armazenamento] globais serão exibidas na janela de propriedades da Ação de Envio.

>[!BEGINTABS]

>[!TAB Componente de base]

Execute as seguintes etapas para usar a configuração do contêiner de Armazenamento do Azure em um Formulário adaptável com base nos Componentes de base como:

1. Abra o Formulário adaptável para edição e navegue até a seção **[!UICONTROL Envio]** das propriedades do Contêiner de formulário adaptável.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **[!UICONTROL Enviar para o Azure Blob Storage]**.

   ![Azure Blob Storage GIF](/help/forms/assets/submit-to-azure-blob-fc.png){width=50%,height=50%}

   Você também pode salvar o Documento de registro (DoR) no Armazenamento de blobs da Azure.

1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

Ao enviar o formulário, os dados são salvos na configuração especificada do container do Azure Storage.
A estrutura de pasta para salvar dados é `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!TAB Componente principal]

Execute as seguintes etapas para usar a configuração do contêiner de Armazenamento do Azure em um Formulário adaptável com base nos Componentes principais como:

1. Abra o navegador Conteúdo e selecione o componente **[!UICONTROL Contêiner do Guia]** do seu Formulário adaptável.
1. Clique no ícone de propriedades do Guia Contêiner ![Propriedades do Guia](/help/forms/assets/configure-icon.svg). A caixa de diálogo Contêiner de formulário adaptável é aberta.
1. Clique na guia **[!UICONTROL Envio]**.
1. Na lista suspensa **[!UICONTROL Enviar Ação]**, selecione **[!UICONTROL Enviar para o Azure Blob Storage]**.

   ![Azure Blob Storage GIF](/help/forms/assets/azure-submit-video.gif)

   Você também pode salvar o Documento de registro (DoR) no Armazenamento de blobs da Azure.

1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

Ao enviar o formulário, os dados são salvos na configuração especificada do container do Azure Storage.
A estrutura de pasta para salvar dados é `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!TAB Universal Editor]

Execute as seguintes etapas para usar a configuração do contêiner de Armazenamento do Azure em um Formulário adaptável criado no Universal Editor:

1. Abra o Formulário adaptável para edição.
1. Clique na extensão **Editar propriedades do formulário** no editor.
A caixa de diálogo **Propriedades do Formulário** é exibida.

   >[!NOTE]
   >
   > * Se você não vir o ícone **Editar Propriedades do Formulário** na interface do Universal Editor, habilite a extensão **Editar Propriedades do Formulário** na Extension Manager.
   > * Consulte o artigo [Destaques dos recursos do Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions) para saber como habilitar ou desabilitar extensões no Universal Editor.

1. Clique na guia **Envio** e selecione a ação de envio **[!UICONTROL Enviar para o Azure Blob Storage]**.
   ![Armazenamento de Blob da Azure](/help/forms/assets/azure-blob-storage-ue.png)

   Se você selecionar **Salvar anexos com nome original**, os anexos serão armazenados na pasta usando seus nomes de arquivo originais. Você também pode salvar o Documento de registro (DoR) no Armazenamento de blobs da Azure.

1. Selecione a **[!UICONTROL Configuração de Armazenamento]**, onde você deseja salvar seus dados.
1. Clique em **[!UICONTROL Salvar&amp;Fechar]** para salvar as configurações de Envio.

Ao enviar o formulário, os dados são salvos na configuração especificada do container do Azure Storage.
A estrutura de pasta para salvar dados é `/configuration_container/form_name/year/month/date/submission_id/data`.

>[!ENDTABS]

## Artigos relacionados

{{af-submit-action}}
