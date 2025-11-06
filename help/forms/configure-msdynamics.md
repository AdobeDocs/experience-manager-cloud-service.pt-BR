---
title: Como configurar modelos de dados de formulário prontos para uso do Microsoft Dynamics 365 para o Adaptive Forms?
description: Saiba como integrar o Microsoft Dynamics 365 com o Adaptive Forms.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 29ee324c-cd4c-403b-bb3d-b1eda8e8ad88
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 0%

---


# Configurar o Microsoft® Dynamics 365 para AEM Forms

A Integração de dados do Adobe Experience Manager Forms fornece uma configuração de serviço na nuvem para integrar formulários ao servidor do Microsoft Dynamics. Ela permite criar o Modelo de dados de formulário (FDM) com base nas entidades, atributos e serviços definidos no serviço do Microsoft Dynamics. O modelo de dados de formulário (FDM) pode ser usado para criar o Adaptive Forms que interage com o servidor do Microsoft Dynamics para habilitar workflows de negócios. Por exemplo:

* Consulte o servidor Microsoft Dynamics para obter dados e preencha previamente o Adaptive Forms.
* Grave dados no Microsoft Dynamics no envio do Formulário adaptável.
* Grave dados no Microsoft Dynamics por meio de entidades personalizadas definidas no Modelo de dados de formulário (FDM).

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md).

<!-- 
[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Microsoft&reg; Dynamics 365] Cloud Services to integrate Adaptive Forms with out of the box Form Data Model (FDM). The Adaptive Forms can then interact with [!DNL Microsoft&reg; Dynamics 365] servers to enable business workflows. For example:

* Write data into [!DNL Microsoft&reg; Dynamics 365] on Adaptive Form submission.
* Write data in [!DNL Microsoft&reg; Dynamics 365] through custom entities defined in Form Data Model (FDM) and conversely.
* Query [!DNL Microsoft&reg; Dynamics 365]server for data and prepopulate Adaptive Forms.
* Read data from [!DNL Microsoft&reg; Dynamics 365] server.

[!DNL Microsoft&reg; Dynamics 365] cloud services and Form Data Model (FDM) are available out of the box on the [!DNL AEM Forms] Server after you [set up a development project for Forms based on Experience Manager archetype](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft&reg; Dynamics 365 cloud services and Form Data Model (FDM) are available out of the box only if you set up an [!DNL Experience Manager Forms] as a [!DNL Cloud Service] project based on [AEM Archetype 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) or later.-->

## Pré-requisitos

Antes de integrar o [!DNL Microsoft® Dynamics 365] ao AEM Forms as a Cloud Service, verifique se você executou as seguintes etapas:


1. **Configurar a conta no Microsoft Dynamics 365**

   Siga as etapas explicadas no vídeo para configurar uma conta do Microsoft Dynamics 365. Neste vídeo, uma conta de avaliação é criada para fins de demonstração.

   >[!VIDEO](https://video.tv.adobe.com/v/3444389/)

1. **Criar uma conta no Centro de Administração da Plataforma de Energia**

   Crie uma conta no **Centro de Administração do Power Platform** para:

   * Adicionar Dataverse
   * Habilitar aplicativos do Microsoft Dynamics 365

   Siga as etapas no vídeo para criar uma conta no Centro de administração da plataforma de energia. Neste vídeo, uma conta de avaliação foi criada para fins de demonstração.

   >[!VIDEO](https://video.tv.adobe.com/v/3444388)

1. **Registrar um aplicativo para [!DNL Microsoft® Dynamics 365] no Azure Ative Diretory**

   Siga as etapas no vídeo para registrar um aplicativo para [!DNL Microsoft® Dynamics 365] no Azure Ative Diretory.

   >[!VIDEO](https://video.tv.adobe.com/v/3444369/dynamics365integration-microsoftdynamics-apiaccess-azuread-appregistration)

   >[!NOTE]
   >
   >* Para criar o aplicativo [!DNL Microsoft® Dynamics 365] conectado, selecione **Web** como plataforma e especifique o **URI de Redirecionamento** no seguinte formato: `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/fdm.html`.
   >* Salve a ID do cliente (também conhecida como ID do aplicativo) e o segredo do cliente para referência futura.

## Conexão do Forms ao Microsoft® Dynamics 365

Após configurar os pré-requisitos acima, você pode prosseguir com a integração do Adaptive Forms com o Microsoft® Dynamics 365. Para enviar dados ao Microsoft® Dynamics 365 no envio de formulários, siga as etapas abaixo:

[&#x200B;1. Definir a configuração do serviço em nuvem para o Microsoft Dynamics](#1-configure-cloud-service-configuration-for-microsoft-dynamics)

[&#x200B;2. Criar Modelo de dados de formulário (FDM)](#2-create-form-data-model-fdm)

### &#x200B;1. Definir a configuração do serviço em nuvem para o Microsoft Dynamics

>[!VIDEO](https://video.tv.adobe.com/v/3444370/cloudconfiguration-dataintegration-adobeexperiencemanager-aemforms-microsoftdynamics)

Execute as seguintes etapas para definir a configuração do serviço de nuvem [!DNL Microsoft® Dynamics 365]:

1. Navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fontes de Dados]** na instância de autor [!DNL AEM Forms],.

   ![Selecionar Source de Dados na Nuvem](/help/forms/assets/dynamics-data-source.png)
1. Selecione um Contêiner de configuração. A configuração é armazenada no Contêiner de configuração selecionado.
1. Clique em **[!UICONTROL Criar]**.

   ![Criar configuração de nuvem](/help/forms/assets/dynamics-select-configuration.png)

   O assistente de configuração **Criar configuração de Source de Dados** é exibido.

   ![Assistente para Criar Configuração de Source de Dados](/help/forms/assets/dynamics-create-data-configuration.png)

1. Especifique o **[!UICONTROL Título]**, **[!UICONTROL Nome]** e selecione **[!UICONTROL Tipo de Serviço]** como **Serviço OData**.
1. Clique em **[!UICONTROL Avançar]**. A guia **Autenticação** é exibida.

   ![Guia Autenticação](/help/forms/assets/dynamics-authentication-tab.png)

1. Especifique o valor para o campo **[!UICONTROL Raiz de Serviço]**.

   Vá para a instância do Dynamics no **Centro de Administração do Power Platform** e navegue até [Recursos do Desenvolvedor](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) para exibir o valor da **Raiz de Serviço**. O **ponto de extremidade da API da Web** representa o valor **Raiz de Serviço** da instância do Dynamics que você deseja integrar ao Adaptive Forms. A URL da **Raiz de Serviço** está no seguinte formato: `https://<tenant-name>.dynamics.com/api/data/v9.1/`

   ![Campo Raiz do Serviço](/help/forms/assets/dynamics-service-root.png)

1. Selecione o **[!UICONTROL Tipo de autenticação]** como **OAuth2.0**.
1. Especifique a **ID do Cliente** (referida como ID do Aplicativo) e o **Segredo do Cliente** para o aplicativo conectado.
Você pode recuperar a **ID do Cliente** e o **Segredo do Cliente** do Aplicativo do Azure Ative Diretory.

   ![ID do Cliente e Segredo do Cliente](/help/forms/assets/dynamics-azure-app-resgistration.png)

1. Especifique o seguinte nos campos **[!UICONTROL URL do OAuth]**, **[!UICONTROL URL do Token de Atualização]** e **[!UICONTROL URL do Token de Acesso]**.
Você pode recuperar a **[!UICONTROL URL do OAuth]**, a **[!UICONTROL URL do Token de Atualização]** e a **[!UICONTROL URL do Token de Acesso]** da seção **Pontos de Extremidade** do Aplicativo do Azure Ative Diretory.

   ![Pontos de Extremidade do Aplicativo Azure](/help/forms/assets/dynamics-azure-app-endpoints.png)

1. Especifique `openid` no campo **[!UICONTROL Escopo de Autorização]** para o processo de autorização em [!DNL Microsoft® Dynamics 365].
1. Especifique a URL da instância dinâmica no campo **[!UICONTROL Recurso]** para configurar [!DNL Microsoft® Dynamics 365] com um Modelo de Dados de Formulário (FDM).
Você pode copiar a **URL do Ambiente** do **Centro de Administração do Power Platform** ou derivar a URL da instância do Dynamics usando a **Raiz de Serviço** URL. A URL do recurso está no seguinte formato: `https://<tenant-name>.dynamics.com`.

   ![Campo de Recursos do Aplicativo de Energia](/help/forms/assets/dynamics-resource-field.png)

1. Faça logon com suas credenciais do [!DNL Microsoft® Dynamics 365] e aceite para permitir que a configuração do serviço de nuvem se conecte ao serviço [!DNL Microsoft® Dynamics 365]. Se a conexão for bem-sucedida, você será redirecionado para a página de configuração do serviço de nuvem [!DNL Microsoft® Dynamics 365], que exibe uma mensagem de sucesso.
1. Selecione **[!UICONTROL Criar]** para salvar a configuração.

### &#x200B;2. Criar Modelo de dados de formulário (FDM)

>[!VIDEO](https://video.tv.adobe.com/v/3444367/aemforms-adobeexperiencemanager-formdatamodel--dataintegration-digitalforms)

Você pode usar a criação do Modelo de Dados de Formulário (FDM) usando a configuração de nuvem [!DNL Microsoft® Dynamics 365] criada. Execute as seguintes etapas para criar o Modelo de dados de formulário:

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrações de Dados]**.
   ![Criar modelo de dados de formulário](/help/forms/assets/dynamics-create-fdm.png)

1. Clique em **[!UICONTROL Criar]** e selecione **[!UICONTROL Modelo de dados de formulário]**.
   ![Selecionar modelo de dados do formulário](/help/forms/assets/dynamics-select-fdm.png)

   O assistente **Criar modelo de dados de formulário** é exibido.
1. Clique em **[!UICONTROL Avançar]**.
1. Selecione a configuração de nuvem criada na guia **Selecionar fonte de dados**.
   ![Selecionar configuração de nuvem](/help/forms/assets/dynamics-select-cloud-config.png)

1. Clique no ícone Editar ![Editar](assets/edit.png) para exibir e configurar o Modelo de Dados de Formulário (FDM).

Em seguida, você pode [configurar o Modelo de Dados de Formulário (FDM)](/help/forms/work-with-form-data-model.md#configure-services) e usá-lo em vários casos de uso do Formulário Adaptável, como:

* Preencha previamente o formulário adaptável consultando informações de [!DNL Microsoft Dynamics] entidades e serviços
* Invocar operações do servidor [!DNL Microsoft Dynamics] definidas em um Modelo de Dados de Formulário (FDM) usando regras de Formulário Adaptável
* Gravar dados de formulário enviados em [!DNL Microsoft Dynamics] entidades
* Você pode configurar a Ação de Envio do Modelo de Dados de Formulário para um Formulário adaptável para enviar dados para [!DNL Microsoft Dynamics].

Você pode usar a opção [Enviar usando o Modelo de Dados de Formulário (FDM)](/help/forms/using-form-data-model.md) em um **Formulário adaptável** para transferir dados do seu formulário para o [!DNL Microsoft® Dynamics 365] configurado.


>[!MORELIKETHIS]
>
>* [Configurar fontes de dados para o AEM Forms](/help/forms/configure-data-sources.md)
>* [Configurar o armazenamento do Azure para o AEM Forms](/help/forms/configure-azure-storage.md)
>  [Adicionar o Portal Forms a uma página do AEM Sites](/help/forms/configure-forms-portal.md)
