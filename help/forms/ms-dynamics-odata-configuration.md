---
title: Como configurar [!DNL Microsoft Dynamics] OData?
description: Saiba como criar o Modelo de dados de formulário com base nas entidades, atributos e serviços definidos em [!DNL Microsoft Dynamics] service. The Form Data Model can be used to create Adaptive Forms that interact with [!DNL Microsoft Dynamics] para ativar workflows de negócios.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb7b41f0-fd4f-4ba6-9f45-792a66ba6368
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 1%

---

# [!DNL Microsoft Dynamics] Configuração de OData {#microsoft-dynamics-odata-configuration}

![integração de dados](assets/data-integeration.png)

[!DNL Microsoft Dynamics] é um software de CRM (relacionamento com o cliente) e ERP (Enterprise Resource Planning, planejamento de recursos empresariais) que fornece soluções corporativas para criar e gerenciar contas, contatos, clientes potenciais, oportunidades e casos de clientes. [[!DNL Experience Manager Forms] Integração de dados](data-integration.md) fornece uma configuração de serviço em nuvem OData para integrar o Forms com soluções online e locais [!DNL Microsoft Dynamics] servidor. Ela permite criar o Modelo de dados de formulário com base nas entidades, atributos e serviços definidos em [!DNL Microsoft Dynamics] serviço. O Modelo de dados de formulário pode ser usado para criar um Forms adaptável que interage com o [!DNL Microsoft Dynamics] para ativar workflows de negócios. Por exemplo:

* Query [!DNL Microsoft Dynamics] servidor para dados e pré-preencher o Adaptive Forms
* Gravar dados em [!DNL Microsoft Dynamics] no envio do formulário adaptável
* Gravar dados em [!DNL Microsoft Dynamics] por meio de entidades personalizadas definidas no Modelo de dados de formulário e vice-versa

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  MS Dynamics OData Cloud Service (OData Service) is available with all run modes. For more information on configuring run modes for an [!DNL Experience Manager] instance, see [Run Modes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#runmodes).

## Pré-requisitos {#prerequisites}

Antes de começar a configurar e configurar [!DNL Microsoft Dynamics], verifique se você tem:

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* Configurado [!DNL Microsoft Dynamics] 365 online ou instalado uma instância de uma das seguintes opções [!DNL Microsoft Dynamics] versões:

   * [!DNL Microsoft Dynamics] 365 no local
   * [!DNL Microsoft Dynamics] 2016 no local

* [Registrado o pedido de [!DNL Microsoft Dynamics] online service with [!DNL Microsoft Azure] Ative Diretory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Anote os valores para a ID do cliente (também chamada de ID do aplicativo) e o segredo do cliente para o serviço registrado. Esses valores são usados enquanto [configuração do serviço em nuvem para seu [!DNL Microsoft Dynamics] service](#configure-cloud-service-for-your-microsoft-dynamics-service).

## Definir URL de resposta para registrado [!DNL Microsoft Dynamics] aplicativo {#set-reply-url-for-registered-microsoft-dynamics-application}

Faça o seguinte para definir o URL de resposta para registrado [!DNL Microsoft Dynamics] aplicativo:

>[!NOTE]
>
>Use este procedimento somente durante a integração [!DNL Experience Manager Forms] on-line [!DNL Microsoft Dynamics] servidor.

1. Ir para [!DNL Microsoft Azure] Conta do Ative Diretory e adicione o seguinte URL de configuração de serviço em nuvem em **[!UICONTROL URLs de resposta]** configurações para seu aplicativo registrado:

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Diretório do Azure](assets/azure_directory_new.png)

1. Salve a configuração.

## Configurar [!DNL Microsoft Dynamics] para IFD {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics] O usa a autenticação baseada em declarações para fornecer acesso aos dados no [!DNL Microsoft Dynamics] Servidor CRM para usuários externos. Para habilitar isso, faça o seguinte para configurar [!DNL Microsoft Dynamics] para implantação com acesso à Internet (IFD) e defina as configurações de solicitação.

>[!NOTE]
>
>Use este procedimento somente durante a integração [!DNL Experience Manager Forms] com instalações [!DNL Microsoft Dynamics] servidor.

1. Configurar [!DNL Microsoft Dynamics] instância no local para o IFD, conforme descrito em [Configurar IFD para [!DNL Microsoft Dynamics]](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Execute os seguintes comandos usando o Windows PowerShell para definir as configurações de afirmação em IFD-enabled [!DNL Microsoft Dynamics]:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Consulte [Registro do aplicativo para CRM no local (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) para obter detalhes.

## Configurar o cliente OAuth no computador AD FS {#configure-oauth-client-on-ad-fs-machine}

Faça o seguinte para registrar um cliente OAuth na máquina do Ative Diretory Federation Services (AD FS) e conceder acesso à máquina do AD FS:

>[!NOTE]
>
>Use este procedimento somente durante a integração [!DNL Experience Manager Forms] com instalações [!DNL Microsoft Dynamics] servidor.

1. Execute o seguinte comando:

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Em que:

   * `Client-ID` é uma ID de cliente que você pode gerar usando qualquer gerador de GUID.
   * `redirect-uri` é o URL para o [!DNL Microsoft Dynamics] Serviço em nuvem OData em [!DNL Experience Manager Forms]. O serviço em nuvem padrão instalado com o [!DNL Experience Manager Forms] é implantada no seguinte URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Execute o seguinte comando para conceder acesso na máquina AD FS:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   Em que:

   * `resource` é [!DNL Microsoft Dynamics] URL da organização.

1. [!DNL Microsoft Dynamics] O usa o protocolo HTTPS. Para chamar pontos de extremidade do AD FS de [!DNL Forms] server, install [!DNL Microsoft Dynamics] certificado do site para o armazenamento de certificados Java usando o `keytool` no computador em execução [!DNL Experience Manager Forms].

## Configurar o serviço em nuvem para seu [!DNL Microsoft Dynamics] service {#configure-cloud-service-for-your-microsoft-dynamics-service}

Um serviço OData é identificado por seu URL raiz do serviço. Para configurar um serviço OData em [!DNL Experience Manager] as a Cloud Service, certifique-se de ter o URL raiz do serviço e faça o seguinte:

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>Para obter o guia passo a passo da configuração do [!DNL Microsoft Dynamics 365], em linha ou no local, consulte [[!DNL Microsoft Dynamics] Configuração de OData](ms-dynamics-odata-configuration.md).

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta onde deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especificar um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço OData]** do **[!UICONTROL Tipo de serviço]** como opção, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
No **[!UICONTROL Configurações de autenticação]** guia :

   1. Insira o valor da variável **[!UICONTROL Raiz do serviço]** campo. Vá para a instância do Dynamics e navegue até **[!UICONTROL Recursos do desenvolvedor]** para exibir o valor do campo Service Root . Por exemplo, https://&lt;tenant-name>/api/data/v9.1/

   1. Selecionar **[!UICONTROL OAuth 2.0]** como o tipo de autenticação.

   1. Substitua os valores padrão no **[!UICONTROL ID do cliente]** (também designado por **ID do aplicativo**), **[!UICONTROL Segredo do cliente]**, **[!UICONTROL URL de OAuth]**, **[!UICONTROL Atualizar URL do token]**, **[!UICONTROL URL do token de acesso]** e **[!UICONTROL Recurso]** campos com valores da [!DNL Microsoft Dynamics] configuração de serviço. É obrigatório especificar o URL da instância do dynamics no **[!UICONTROL Recurso]** campo para configurar [!DNL Microsoft Dynamics] com um modelo de dados de formulário. Use o URL raiz do serviço para derivar o URL da instância dinâmica. Por exemplo, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Especificar **[!UICONTROL openid]** no **[!UICONTROL Escopo da Autorização]** campo para o processo de autorização em [!DNL Microsoft Dynamics].

      ![Configurações de autenticação](assets/dynamics_authentication_settings_new.png)
Modelo de dados do formulário
1. Clique em **[!UICONTROL Conectar-se ao OAuth]**. Você é redirecionado para [!DNL Microsoft Dynamics] página de logon.
1. Faça logon com seu [!DNL Microsoft Dynamics] credenciais e aceitar permitir que a configuração do serviço de nuvem se conecte [!DNL Microsoft Dynamics] serviço. É uma tarefa única estabelecer o Form Data Model entre o serviço de nuvem e o serviço.

   Você é o Modelo de dados de formulário na página de configuração do serviço de nuvem, que exibe uma mensagem de que a configuração OData foi salva com êxito.

O serviço em nuvem do MS Dynamics OData Cloud Service (Serviço OData) é configurado e conectado ao serviço de Dynamics. Modelo de dados de formulário Modelo de dados

## Criar modelo de dados do formulário {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

Após configurar o serviço em nuvem do MS Dynamics OData Cloud Ser Form Data Model ce), você pode usar o serviço ao criar modelos de dados de formulário. Para obter mais informações, consulte [Criar modelo de dados de formulário](create-form-data-models.md).

Em seguida, é possível criar um formulário adaptável com base no modelo de Modelo de dados de formulário e usá-lo em vários casos de uso do Formulário adaptável, como:

* Preencha previamente o formulário adaptável consultando informações de [!DNL Microsoft Dynamics] entidades e serviços
* Invocar [!DNL Microsoft Dynamics] operações do servidor definidas em um Modelo de dados de formulário usando regras de formulário adaptável
* Gravar dados de formulário enviados em [!DNL Microsoft Dynamics] entities

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

Para obter mais informações sobre como criar e usar o Modelo de dados de formulário em fluxos de trabalho, consulte [Integração de dados](data-integration.md).
