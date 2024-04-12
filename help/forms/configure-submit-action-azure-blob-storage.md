---
Title: How to connect AEM Adaptive Forms with Azure Blob Storage?
Description: Learn how to create an Azure Blob Storage Configuration in AEM Forms and use it within your Adaptive Forms for efficient data storage.
keywords: Integração do Armazenamento Azure Blob com o AEM Forms, Envio de dados para o Armazenamento Azure, Criação da configuração de armazenamento do Azure no AEM Forms, Uso do Armazenamento Azure Blob na Ação de envio adaptável do Forms
feature: Adaptive Forms, Core Components
source-git-commit: a22ecddf7c97c5894cb03eb44296e0562ac46ddb
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---


# Enviar um formulário adaptável para o Armazenamento de blobs do Azure

A variável **[!UICONTROL Enviar para o Armazenamento Azure Blob]**  A ação enviar conecta um formulário adaptável a um portal do Microsoft® Azure. Você pode enviar os dados do formulário, arquivos, anexos ou Documento de registro para os contêineres conectados do Armazenamento do Azure.

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções na [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md) artigo.

## Vantagens

Algumas das vantagens da integração do Armazenamento Azure Blob com o AEM Forms são:

* Isso ajuda a simplificar o processo de envio de dados, arquivos, anexos e documentos de registro do Formulário adaptável para contêineres de Armazenamento do Azure.
* Ele usa o Armazenamento Azure Blob para o armazenamento centralizado e organizado de envios de formulários adaptáveis.

## Conectar o AEM Forms com o Microsoft® Azure Blob Storage

Para usar o Armazenamento Azure Blob na ação enviar do Adaptive Forms:

1. [Criar um contêiner de armazenamento do Azure Blob](#create-a-azure-blob-storage-container-create-azure-configuration): conecta o AEM Forms aos contêineres de Armazenamento do Azure.
2. [Usar a configuração de armazenamento do Azure em um formulário adaptável](#use-azure-storage-configuration-in-an-adaptive-form-use-azure-storage-configuartion-in-af): ele conecta seu Formulário adaptável aos contêineres configurados do Armazenamento do Azure.

### Criar um contêiner de armazenamento do Azure Blob {#create-azure-configuration}

Para conectar o AEM Forms aos seus contêineres de Armazenamento do Azure:
1. Vá para o **Autor do AEM Forms** instância > **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Armazenamento do Azure]**.
1. Depois de selecionar a variável **[!UICONTROL Armazenamento do Azure]**, você será redirecionado para **[!UICONTROL Navegador de armazenamento do Azure]**.
1. Selecione um **Contêiner de configuração**. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]**. O assistente Criar configuração de armazenamento do Azure é exibido.

   ![Configuração de armazenamento do Azure](/help/forms/assets/azure-storage-configuration.png)

1. Especifique a **[!UICONTROL Título]**, **[!UICONTROL Conta de armazenamento do Azure]** e **[!UICONTROL Chave de acesso do Azure]**.

   * Você pode recuperar `Azure Storage Account` nome e `Azure Access key` a partir das Contas de armazenamento no portal Microsoft® Azure.
<!--

    >[!NOTE]
    >
    > The URL for **[!UICONTROL Azure Blob Endpoint]** is automatically appended to the textbox when a value is entered for **[!UICONTROL Azure Storage Account]**. You can update the Azure Blob End Point URL with your custom domain. Steps to update URL for **[!UICONTROL Azure Blob End Point]**:
    > 1. [Enable the AEM Advance Networking VPN support](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)
    > 1. [Enable dedicated egress IP link](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html)
    > 1. [Map custom domain to azure blob storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal)
-->

1. Clique em **[!UICONTROL Salvar]**.

Agora, você pode usar essa configuração do contêiner de Armazenamento do Azure para a ação de envio em um Formulário adaptável.

### Usar a configuração de armazenamento do Azure em um formulário adaptável {#use-azure-storage-configuartion-in-af}

Você pode usar a configuração do contêiner de Armazenamento do Azure criada em um Formulário adaptável, para salvar dados ou o Documento de registro gerado no contêiner de Armazenamento do Azure. Execute as seguintes etapas para usar a configuração do contêiner de Armazenamento do Azure em um Formulário adaptável como:
1. Criar um [Formulário adaptável](/help/forms/creating-adaptive-form-core-components.md).

   >[!NOTE]
   >
   > * Selecionar o mesmo [!UICONTROL Contêiner de configuração] para um Formulário adaptável, em que você criou seu armazenamento do OneDrive.
   > * Se não [!UICONTROL Contêiner de configuração] for selecionada, a variável global [!UICONTROL Configuração de armazenamento] pastas são exibidas na janela de propriedades Submeter Ação.

1. Selecionar **Ação de envio** as **[!UICONTROL Enviar para o Armazenamento Azure Blob]**.
   ![GIF de armazenamento do Azure Blob](/help/forms/assets/azure-submit-video.gif)

1. Selecione o **[!UICONTROL Configuração de armazenamento]**, onde deseja salvar os dados.
1. Clique em **[!UICONTROL Salvar]** para salvar as configurações de Envio.

Ao enviar o formulário, os dados são salvos na configuração especificada do contêiner de Armazenamento do Azure.
A estrutura de pastas para salvar os dados é `/configuration_container/form_name/year/month/date/submission_id/data`.

## Artigos relacionados

{{af-submit-action}}