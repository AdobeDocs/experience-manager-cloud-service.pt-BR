---
title: Como configurar [!DNL Microsoft Dynamics] OData?
description: Saiba como criar o Modelo de dados de formulário com base nas entidades, atributos e serviços definidos em [!DNL Microsoft Dynamics] serviço.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb7b41f0-fd4f-4ba6-9f45-792a66ba6368
source-git-commit: 92f89243b79c6c2377db3ca2b8ea244957416626
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 3%

---

# [!DNL Microsoft Dynamics] Configuração OData {#microsoft-dynamics-odata-configuration}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/ms-dynamics-odata-configuration.html) |
| AEM as a Cloud Service | Este artigo |

![integração de dados](assets/data-integeration.png)

[!DNL Microsoft Dynamics] O é um software de CRM (Customer Relationship Management, gerenciamento de relacionamento com o cliente) e ERP (Enterprise Resource Planning, planejamento de recursos corporativos) que fornece soluções corporativas para criar e gerenciar contas, contatos, clientes potenciais, oportunidades e casos de clientes. [[!DNL Experience Manager Forms] Integração de dados](data-integration.md) O fornece uma configuração do serviço de nuvem OData para integrar o Forms com o local e online [!DNL Microsoft Dynamics] servidor. Ela permite criar o Modelo de dados de formulário com base nas entidades, atributos e serviços definidos no [!DNL Microsoft Dynamics] serviço. O modelo de dados de formulário pode ser usado para criar o Forms adaptável que interage com o [!DNL Microsoft Dynamics] servidor para habilitar workflows de negócios. Por exemplo:

* Query [!DNL Microsoft Dynamics] servidor para dados e pré-popular o Adaptive Forms
* Gravar dados em [!DNL Microsoft Dynamics] no envio do Formulário adaptável
* Gravar dados em [!DNL Microsoft Dynamics] por meio de entidades personalizadas definidas no Modelo de dados de formulário e vice-versa

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  O Cloud Service OData (serviço OData) do MS Dynamics está disponível com todos os modos de execução. Para obter mais informações sobre a configuração dos modos de execução para um [!DNL Experience Manager] instância, consulte [Modos de execução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=pt-BR#runmodes).

## Pré-requisitos {#prerequisites}

Antes de começar a instalar e configurar [!DNL Microsoft Dynamics], verifique se você tem:

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* Configurado [!DNL Microsoft Dynamics] 365 on-line ou instalou uma instância de um dos seguintes [!DNL Microsoft Dynamics] versões:

   * [!DNL Microsoft Dynamics] 365 no local
   * [!DNL Microsoft Dynamics] 2016 no local

* [Registrou o aplicativo para [!DNL Microsoft Dynamics] serviço online com [!DNL Microsoft Azure] Ative Diretory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Anote os valores da ID do cliente (também chamada de ID do aplicativo) e o segredo do cliente para o serviço registrado. Esses valores são usados enquanto [configuração do cloud service para o [!DNL Microsoft Dynamics] serviço](#configure-cloud-service-for-your-microsoft-dynamics-service).

## Definir URL de resposta para registrado [!DNL Microsoft Dynamics] aplicativo {#set-reply-url-for-registered-microsoft-dynamics-application}

Faça o seguinte para definir o URL de resposta para registrado [!DNL Microsoft Dynamics] aplicativo:

>[!NOTE]
>
>Use este procedimento somente durante a integração [!DNL Experience Manager Forms] com on-line [!DNL Microsoft Dynamics] servidor.

1. Ir para [!DNL Microsoft Azure] Conta do Ative Diretory e adicione a seguinte URL de configuração do serviço de nuvem em **[!UICONTROL URLs de resposta]** configurações para seu aplicativo registrado:

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Diretório do Azure](assets/azure_directory_new.png)

1. Salve a configuração.

## Configurar [!DNL Microsoft Dynamics] para IFD {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics] O usa autenticação baseada em declarações para fornecer acesso a dados em [!DNL Microsoft Dynamics] Servidor do CRM para usuários externos. Para habilitar isso, faça o seguinte para configurar [!DNL Microsoft Dynamics] para implantação na Internet (IFD) e definir configurações de declaração.

>[!NOTE]
>
>Use este procedimento somente durante a integração [!DNL Experience Manager Forms] com local [!DNL Microsoft Dynamics] servidor.

1. Configurar [!DNL Microsoft Dynamics] local para o IFD, tal como descrito no anexo I, parte A, do Regulamento (CE) [Configurar IFD para [!DNL Microsoft Dynamics]](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Execute os seguintes comandos usando o Windows PowerShell para definir as configurações de declaração no IFD habilitado [!DNL Microsoft Dynamics]:

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Consulte [Registro de aplicativo para CRM local (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd) para obter detalhes.

## Configurar o cliente OAuth no computador do AD FS {#configure-oauth-client-on-ad-fs-machine}

Faça o seguinte para registrar um cliente OAuth em um computador do Ative Diretory Federation Services (AD FS) e conceder acesso a esse computador:

>[!NOTE]
>
>Use este procedimento somente durante a integração [!DNL Experience Manager Forms] com local [!DNL Microsoft Dynamics] servidor.

1. Execute o seguinte comando:

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Em que:

   * `Client-ID` é uma ID de cliente que você pode gerar usando qualquer gerador de GUID.
   * `redirect-uri` é o URL para o [!DNL Microsoft Dynamics] Serviço de nuvem OData ativado [!DNL Experience Manager Forms]. O serviço de nuvem padrão instalado com o [!DNL Experience Manager Forms] é implantado no seguinte URL:
     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Execute o seguinte comando para conceder acesso à máquina do AD FS:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   Em que:

   * `resource` é o [!DNL Microsoft Dynamics] URL da organização.

1. [!DNL Microsoft Dynamics] usa o protocolo HTTPS. Para chamar pontos de extremidade do AD FS de [!DNL Forms] servidor, instalar [!DNL Microsoft Dynamics] certificado do site para o armazenamento de certificados Java usando o `keytool` no computador que está executando [!DNL Experience Manager Forms].

## Configurar o serviço em nuvem para o seu [!DNL Microsoft Dynamics] serviço {#configure-cloud-service-for-your-microsoft-dynamics-service}

Um serviço OData é identificado por sua URL raiz de serviço. Para configurar um serviço OData no [!DNL Experience Manager] as a Cloud Service, verifique se você tem um URL raiz de serviço para o serviço e faça o seguinte:

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>Para obter um guia passo a passo para configurar o [!DNL Microsoft Dynamics 365]on-line ou no local, consulte [[!DNL Microsoft Dynamics] Configuração OData](ms-dynamics-odata-configuration.md).

1. Ir para **[!UICONTROL Ferramentas > Cloud Service > Fontes de dados]**. Toque para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço em nuvem](#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço OData]** do **[!UICONTROL Tipo de serviço]** selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próxima]**.
No **[!UICONTROL Configurações de autenticação]** guia:

   1. Insira o valor para o **[!UICONTROL Raiz do serviço]** campo. Acesse a instância do Dynamics e navegue até **[!UICONTROL Recursos do desenvolvedor]** para exibir o valor do campo Raiz do Serviço. Por exemplo, https://&lt;tenant-name>/api/data/v9.1/

   1. Selecionar **[!UICONTROL OAuth 2.0]** como o tipo de autenticação.

   1. Substitua os valores padrão no **[!UICONTROL ID do cliente]** (também referido como **ID do aplicativo**), **[!UICONTROL Segredo do cliente]**, **[!UICONTROL URL do OAuth]**, **[!UICONTROL URL do token de atualização]**, **[!UICONTROL URL do token de acesso]**, e **[!UICONTROL Recurso]** campos com valores do seu [!DNL Microsoft Dynamics] configuração do serviço. É obrigatório especificar o URL da instância do dynamics na variável **[!UICONTROL Recurso]** campo a ser configurado [!DNL Microsoft Dynamics] com um modelo de dados de formulário. Use o URL raiz do serviço para derivar o URL da instância dinâmica. Por exemplo, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Especificar **[!UICONTROL openid]** no **[!UICONTROL Escopo da autorização]** campo para processo de autorização em [!DNL Microsoft Dynamics].

      ![Configurações de autenticação](assets/dynamics_authentication_settings_new.png)
Modelo de dados do formulário
1. Clique em **[!UICONTROL Conectar-se ao OAuth]**. Você será redirecionado para [!DNL Microsoft Dynamics] página de logon.
1. Faça logon com o [!DNL Microsoft Dynamics] e aceite para permitir que a configuração do serviço de nuvem se conecte a [!DNL Microsoft Dynamics] serviço. É uma tarefa única estabelecer o Modelo de dados de formulário entre o serviço em nuvem e o serviço.

   Você é a página Modelo de dados de formulário Configuração do serviço de nuvem, que exibe uma mensagem de que a configuração OData foi salva com êxito.

O serviço de nuvem OData Cloud Service (OData Service) do MS Dynamics está configurado e conectado com seu serviço Dynamics. Modelo de dados do formulário Modelo de dados do formulário

## Criar modelo de dados do formulário {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

Depois de configurar o serviço de nuvem do MS Dynamics OData Cloud Ser Form Data Model (ce), você pode usar o serviço ao criar modelos de dados de formulário. Para obter mais informações, consulte [Criar modelo de dados de formulário](create-form-data-models.md).

Em seguida, você pode criar um Formulário adaptável com base no modelo de Modelo de dados de formulário e usá-lo em vários casos de uso do Formulário adaptável, como:

* Preencha previamente o formulário adaptável consultando informações do [!DNL Microsoft Dynamics] entidades e serviços
* Chamar [!DNL Microsoft Dynamics] operações do servidor definidas em um Modelo de dados de formulário usando regras de Formulário adaptável
* Gravar dados do formulário enviado em [!DNL Microsoft Dynamics] entidades

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

Para obter mais informações sobre como criar e usar o Modelo de dados de formulário em fluxos de trabalho de negócios, consulte [Integração de dados](data-integration.md).
