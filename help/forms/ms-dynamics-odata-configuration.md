---
title: Como configurar o  [!DNL Microsoft Dynamics] OData para o AEM Forms?
description: Saiba como criar o Modelo de dados de formulário (FDM) com base nas entidades, atributos e serviços definidos no serviço  [!DNL Microsoft Dynamics] .
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb7b41f0-fd4f-4ba6-9f45-792a66ba6368
hide: true
hidefromtoc: true
source-git-commit: 3a12fff170f521f6051f0c24a4eb28a12439eec1
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# Configuração OData de [!DNL Microsoft Dynamics] {#microsoft-dynamics-odata-configuration}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/ms-dynamics-odata-configuration.html) |
| AEM as a Cloud Service | Este artigo |

![integração de dados](assets/data-integeration.png)

O [!DNL Microsoft Dynamics] é um software de CRM (relacionamento com o cliente) e ERP (planejamento de recursos corporativos) que fornece soluções corporativas para criar e gerenciar contas, contatos, clientes potenciais, oportunidades e casos de clientes. [[!DNL Experience Manager Forms] A Integração de Dados](data-integration.md) fornece uma configuração do serviço de nuvem OData para integrar o Forms ao servidor [!DNL Microsoft Dynamics] local e online. Ela permite criar o Modelo de Dados de Formulário (FDM) com base nas entidades, atributos e serviços definidos no serviço [!DNL Microsoft Dynamics]. O Modelo de Dados de Formulário (FDM) pode ser usado para criar o Forms Adaptável que interage com o servidor [!DNL Microsoft Dynamics] para habilitar fluxos de trabalho de negócios. Por exemplo:

* Consultar o servidor [!DNL Microsoft Dynamics] para obter dados e pré-popular o Adaptive Forms
* Gravar dados em [!DNL Microsoft Dynamics] no envio do Formulário Adaptável
* Gravar dados em [!DNL Microsoft Dynamics] por meio de entidades personalizadas definidas no Modelo de Dados de Formulário (FDM) e vice-versa

<!--[!DNL Experience Manager Forms] add-on package also includes reference OData configuration that you can use to quickly integrate [!DNL Microsoft Dynamics] with [!DNL Experience Manager Forms].-->

<!--When the package is installed, the following entities and services are available on your [!DNL Experience Manager Forms] instance:

* MS Dynamics OData Cloud Service (OData Service)-->
<!--* Form Data Model with preconfigured [!DNL Microsoft Dynamics] entities and services.-->

<!-- Preconfigured [!DNL Microsoft Dynamics] entities and services in a Form Data Model are available on your [!DNL Experience Manager Forms] instance only if the run mode for the [!DNL Experience Manager] instance is set as `samplecontent` (default). -->  O MS Dynamics OData Cloud Service (Serviço OData) está disponível com todos os modos de execução. Para obter mais informações sobre como configurar os modos de execução para uma instância [!DNL Experience Manager], consulte [Modos de Execução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=pt-BR#runmodes).

O AEM as a Cloud Service oferece várias ações de envio prontas para uso para manipular envios de formulários. Você pode saber mais sobre essas opções no artigo [Ação de envio do formulário adaptável](/help/forms/configure-submit-actions-core-components.md).


## Pré-requisitos {#prerequisites}

Antes de começar a instalar e configurar o [!DNL Microsoft Dynamics], verifique se você tem:

<!--* Installed the [[!DNL Experience Manager Forms] add-on package](installing-configuring-aem-forms-osgi.md) -->
* [!DNL Microsoft Dynamics] 365 online configurado ou instalado uma instância de uma das [!DNL Microsoft Dynamics] versões a seguir:

   * [!DNL Microsoft Dynamics] 365 no local
   * [!DNL Microsoft Dynamics] 2016 no local

* [Registrou o aplicativo para o [!DNL Microsoft Dynamics] serviço online [!DNL Microsoft Azure] Ative Diretory](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Anote os valores da ID do cliente (também chamada de ID do aplicativo) e o segredo do cliente para o serviço registrado. Estes valores são usados ao [configurar o serviço de nuvem para o seu [!DNL Microsoft Dynamics] serviço](#configure-cloud-service-for-your-microsoft-dynamics-service).

## Definir URL de Resposta para o aplicativo [!DNL Microsoft Dynamics] registrado {#set-reply-url-for-registered-microsoft-dynamics-application}

Faça o seguinte para definir a URL de resposta para o aplicativo [!DNL Microsoft Dynamics] registrado:

>[!NOTE]
>
>Use este procedimento somente durante a integração do [!DNL Experience Manager Forms] com o servidor [!DNL Microsoft Dynamics] online.

1. Vá para a conta do Ative Diretory [!DNL Microsoft Azure] e adicione a seguinte URL de configuração do serviço de nuvem nas configurações de **[!UICONTROL URLs de resposta]** para o aplicativo registrado:

   `https://[server]:[port]/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Diretório do Azure](assets/azure_directory_new.png)

1. Salve a configuração.

## Configurar [!DNL Microsoft Dynamics] para IFD {#configure-microsoft-dynamics-for-ifd}

[!DNL Microsoft Dynamics] usa autenticação baseada em declarações para fornecer acesso aos dados no servidor do CRM [!DNL Microsoft Dynamics] para usuários externos. Para habilitar isso, faça o seguinte para configurar o [!DNL Microsoft Dynamics] para IFD e definir as configurações de declaração.

>[!NOTE]
>
> Use este procedimento somente durante a integração do [!DNL Experience Manager Forms] com o servidor [!DNL Microsoft Dynamics] local.

1. Configure a instância local [!DNL Microsoft Dynamics] para o IFD conforme descrito em [Configurar o IFD para [!DNL Microsoft Dynamics]](https://technet.microsoft.com/en-us/library/dn609803.aspx).
1. Execute os seguintes comandos usando o Windows PowerShell para definir as configurações de declaração no [!DNL Microsoft Dynamics] habilitado para IFD:

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
>Use este procedimento somente durante a integração do [!DNL Experience Manager Forms] com o servidor [!DNL Microsoft Dynamics] local.

1. Execute o seguinte comando:

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Em que:

   * `Client-ID` é uma ID de cliente que você pode gerar usando qualquer gerador de GUID.
   * `redirect-uri` é a URL para o serviço de nuvem OData [!DNL Microsoft Dynamics] em [!DNL Experience Manager Forms]. O serviço de nuvem padrão instalado com o [!DNL Experience Manager Forms] é implantado na seguinte URL:
     `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Execute o seguinte comando para conceder acesso à máquina do AD FS:

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   Em que:

   * `resource` é a URL da organização [!DNL Microsoft Dynamics].

1. [!DNL Microsoft Dynamics] usa o protocolo HTTPS. Para invocar pontos de extremidade do AD FS do servidor [!DNL Forms], instale o certificado do site [!DNL Microsoft Dynamics] no armazenamento de certificados Java usando o comando `keytool` no computador que executa o [!DNL Experience Manager Forms].

## Configurar o serviço de nuvem para o serviço [!DNL Microsoft Dynamics] {#configure-cloud-service-for-your-microsoft-dynamics-service}

Um serviço OData é identificado por sua URL raiz de serviço. Para configurar um serviço OData no as a Cloud Service [!DNL Experience Manager], certifique-se de que possui uma URL raiz de serviço para o serviço e faça o seguinte:

<!--The **MS Dynamics OData Cloud Service (OData Service)** configuration comes with default OData configuration. To configure it to connect with your [!DNL Microsoft Dynamics] service, do the following.-->

>[!NOTE]
>
>Para obter o guia passo a passo para configurar o [!DNL Microsoft Dynamics 365], online ou no local, consulte [[!DNL Microsoft Dynamics] Configuração OData](ms-dynamics-odata-configuration.md).

1. Acesse **[!UICONTROL Ferramentas > Serviços da nuvem > Fontes de dados]**. Selecione para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do serviço de nuvem.

1. Selecione **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente de Criação de Configuração de Source de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço OData]** na lista suspensa **[!UICONTROL Tipo de Serviço]**, opcionalmente, procure e selecione uma imagem em miniatura para a configuração e selecione **[!UICONTROL Próximo]**.
Na guia **[!UICONTROL Configurações de autenticação]**:

   1. Insira o valor para o campo **[!UICONTROL Raiz de Serviço]**. Vá para a instância do Dynamics e navegue até **[!UICONTROL Recursos do Desenvolvedor]** para exibir o valor do campo Raiz do Serviço. Por exemplo, https://&lt;tenant-name>/api/data/v9.1/

   1. Selecione **[!UICONTROL OAuth 2.0]** como o tipo de autenticação.

   1. Substitua os valores padrão nos campos **[!UICONTROL ID do Cliente]** (também conhecido como **ID do Aplicativo**), **[!UICONTROL Segredo do Cliente]**, **[!UICONTROL URL do OAuth]**, **[!UICONTROL URL do Token de Atualização]**, **[!UICONTROL URL do Token de Acesso]** e **[!UICONTROL URL]** por valores da configuração do serviço [!DNL Microsoft Dynamics]. É obrigatório especificar a URL da instância do Dynamics no campo **[!UICONTROL Recurso]** para configurar [!DNL Microsoft Dynamics] com um modelo de dados de formulário (FDM). Use o URL raiz do serviço para derivar o URL da instância dinâmica. Por exemplo, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Especifique **[!UICONTROL openid]** no campo **[!UICONTROL Escopo de Autorização]** para o processo de autorização em [!DNL Microsoft Dynamics].

      ![Configurações de autenticação](assets/dynamics_authentication_settings_new.png)
Modelo de dados de formulário (FDM)
1. Clique em **[!UICONTROL Conectar ao OAuth]**. Você é redirecionado à página de logon [!DNL Microsoft Dynamics].
1. Faça logon com suas credenciais do [!DNL Microsoft Dynamics] e aceite para permitir que a configuração do serviço de nuvem se conecte ao serviço [!DNL Microsoft Dynamics]. É uma tarefa única estabelecer o Modelo de dados de formulário (FDM) entre o serviço em nuvem e o serviço.

   Você é a página Modelo de dados de formulário Configuração do serviço de nuvem, que exibe uma mensagem de que a configuração OData foi salva com êxito.

O serviço de nuvem MS Dynamics OData Cloud Service (OData Service) está configurado e conectado ao serviço Dynamics. Modelo de dados de formulário (FDM)

## Criar modelo de dados de formulário (FDM) {#create-form-data-model}

<!--When you install the [!DNL Experience Manager Forms] package, a form data model, **[!DNL Microsoft Dynamics] FDM**, is deployed on your [!DNL Experience Manager] instance. By default, the Form Data Model uses [!DNL Microsoft Dynamics] service configured in the MS Dynamics OData Cloud Service (OData Service) as its data source.

On opening the Form Data Model for the first time, it connects to the configured [!DNL Microsoft Dynamics] service and fetches entities from your [!DNL Microsoft Dynamics] instance. The "contact" and "lead" entities from [!DNL Microsoft Dynamics] are already added in the form data model.

To review the form data model, go to **[!UICONTROL Form Data Model egrations]**. Select **[!DNL Microsoft Dynamics] FDM** and click **[!UICONTROL Edit]** to open the Form Data Model in edit mode. Alternatively, you can open the Form Data Model directly from the following URL:

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`
 Form Data Model 
![default-fdm-1](assets/default-fdm-1.png)-->

Após configurar o serviço de nuvem MS Dynamics OData, você pode usá-lo ao criar o modelo de dados de formulário (FDM). Para obter mais informações, consulte [Criar modelo de dados de formulário (FDM)](create-form-data-models.md).

Em seguida, você pode criar um Modelo de dados de formulário (FDM) baseado no Formulário adaptável e usá-lo em vários casos de uso do Formulário adaptável, como:

* Preencha previamente o formulário adaptável consultando informações de [!DNL Microsoft Dynamics] entidades e serviços
* Invocar operações do servidor [!DNL Microsoft Dynamics] definidas em um Modelo de Dados de Formulário (FDM) usando regras de Formulário Adaptável
* Gravar dados de formulário enviados em [!DNL Microsoft Dynamics] entidades

<!--It is recommended to create a copy of the Form Data Model provided with the [!DNL Experience Manager Forms] package and configure data models and services to suit your requirements. It will ensure that any future updates to the package do not override your form data model.-->

Você pode [configurar a Ação de Envio do Modelo de Dados de Formulário](/help/forms/using-form-data-model.md) para um Formulário Adaptável para enviar dados para o Microsoft Dynamics OData.

Para obter mais informações sobre como criar e usar o Form Data Model (FDM) nos fluxos de trabalho de negócios, consulte [Integração de Dados](data-integration.md).

## Artigos relacionados

{{af-submit-action}}
