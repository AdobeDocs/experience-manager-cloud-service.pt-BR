---
title: Configurar o AEM Assets as a [!DNL Cloud Service] with Brand Portal
description: Saiba como configurar o AEM Assets com o Brand Portal. A configuração permite publicar ativos de marca aprovados de uma instância do AEM na Brand Portal e distribuí-los aos usuários da Brand Portal.
contentOwner: AK
feature: Brand Portal, Asset Distribution, Configuration
role: Admin
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '1784'
ht-degree: 10%

---

# Configurar o Experience Manager Assets com o Brand Portal {#configure-aem-assets-with-brand-portal}

| [Pesquisar Práticas Recomendadas](/help/assets/search-best-practices.md) | [Práticas recomendadas de metadados](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | [Dynamic Media com recursos OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [documentação para desenvolvedores do AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/brandportal/configure-aem-assets-with-brand-portal.html?lang=pt-BR) |
| AEM as a Cloud Service | Este artigo |

A configuração do Adobe Experience Manager Assets Brand Portal permite publicar ativos de marca aprovados da Adobe Experience Manager Assets como uma instância [!DNL Cloud Service] no Brand Portal e distribuí-los aos usuários da Brand Portal.

## Ativar o Brand Portal usando o Cloud Manager {#activate-brand-portal}

O usuário do Cloud Manager ativa o Brand Portal para uma instância do Experience Manager Assets as a [!DNL Cloud Service]. O fluxo de trabalho de ativação cria as configurações necessárias (token de autorização, configuração do IMS e Brand Portal Cloud Service) no back-end e reflete o status do locatário do Brand Portal no Cloud Manager. A ativação do Brand Portal permite que os usuários do Experience Manager Assets publiquem ativos no Brand Portal e os distribuam aos usuários do Brand Portal.

**Pré-requisitos**

Você precisa do seguinte para ativar o Brand Portal no seu Experience Manager Assets como uma instância [!DNL Cloud Service]:

* Uma instância ativa e em execução do Experience Manager Assets as a [!DNL Cloud Service].
* Um usuário com acesso ao Cloud Manager, atribuído aos Perfis do produto Cloud Manager. Consulte [acessando o Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#accessing-cloud-manager) para obter mais informações.

>[!NOTE]
>
>Um ambiente de produção configurado é necessário para uma instância do Experience Manager Assets as a [!DNL Cloud Service] se conectar com o locatário do Brand Portal.

**Etapas para ativar o Brand Portal**

Você pode ativar o Brand Portal ao criar os ambientes de produção para o Experience Manager Assets como uma instância [!DNL Cloud Service] ou separadamente. Vamos supor que o ambiente já tenha sido criado e que agora você seja solicitado a ativar o Brand Portal.

1. Faça logon no Adobe Cloud Manager e navegue até **[!UICONTROL Ambientes]**.

   A página **[!UICONTROL Ambientes]** exibe a lista de todos os ambientes existentes.

1. Selecione os ambientes (um por um) na lista para exibir os detalhes do ambiente.

   O Brand Portal tem direito a um dos ambientes disponíveis e é refletido nas **[!UICONTROL Informações do ambiente]**.

   Depois de encontrar o ambiente associado ao Brand Portal, clique no botão **[!UICONTROL Ativar Brand Portal]** para iniciar o fluxo de trabalho de ativação.

   ![Ativar Brand Portal](assets/create-environment4.png)

1. Leva alguns minutos para ativar o locatário do Brand Portal, pois o fluxo de trabalho de ativação cria as configurações necessárias no back-end. Depois que o locatário do Brand Portal é ativado, o status muda para Ativated.

   ![Exibir Status](assets/create-environment5.png)


>[!NOTE]
>
>O Brand Portal deve ser ativado na mesma organização IMS da Experience Manager Assets como uma instância [!DNL Cloud Service].
>
>Se você tiver uma configuração de nuvem existente do Brand Portal ([configurada manualmente usando o Adobe Developer Console](#manual-configuration)) para uma organização IMS (org1-existing) e sua Experience Manager Assets como uma instância [!DNL Cloud Service] estiver configurada para outra organização IMS (org2-new), ativar o Brand Portal a partir da Cloud Manager redefinirá a organização IMS do Brand Portal para `org2-new`. Embora a configuração de nuvem definida manualmente em `org1-existing` esteja visível na instância do autor do Experience Manager Assets, mas não estará mais em uso após ativar o Brand Portal na Cloud Manager.
>
>Se a configuração de nuvem existente do Brand Portal e a instância do Experience Manager Assets as a [!DNL Cloud Service] estiverem usando a mesma organização IMS (org1), você só precisará ativar o Brand Portal na Cloud Manager.
>
>Não modifique nenhuma configuração gerada automaticamente.

**Consulte também**:

* [Adicionar usuários e funções no Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)

* [Gerenciar ambientes no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)


**Faça logon no seu locatário do Brand Portal**:

Após a ativação do locatário do Brand Portal no Cloud Manager, faça logon no Brand Portal pelo Admin Console ou usando diretamente o URL do locatário.

A URL padrão do seu locatário do Brand Portal é: `https://<tenant-id>.brand-portal.adobe.com/`.

Onde, a ID do locatário é a Organização IMS.


Execute as seguintes etapas se não tiver certeza do URL do Brand Portal:

1. Faça logon em [Admin Console](https://adminconsole.adobe.com/) e navegue até **[!UICONTROL Produtos]**.
1. No painel esquerdo, selecione **[!UICONTROL Adobe Experience Manager Brand Portal - Brand Portal]**.
1. Clique em **[!UICONTROL Ir para Brand Portal]** para abrir o Brand Portal diretamente no navegador.

   Ou copie a URL do locatário do Brand Portal do link **[!UICONTROL Ir para o Brand Portal]** e cole-a no navegador para abrir a interface do Brand Portal.

   ![Acessar o Brand Portal](assets/access-bp-on-cloud.png)


**Testar conexão**

Execute as seguintes etapas para validar a conexão entre sua instância do Experience Manager Assets as a [!DNL Cloud Service] e o locatário do Brand Portal:

1. Faça logon no Experience Manager Assets.

1. No painel **Ferramentas**, navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Distribuição]**.

   ![Navegue até a opção de distribuição](assets/test-bpconfig1.png)

   Um agente de distribuição do Brand Portal (**[!UICONTROL bpdistributionagent0]**) foi criado em **[!UICONTROL Publish para Brand Portal]**.

   ![Criar agente de distribuição](assets/test-bpconfig2.png)

1. Clique em **[!UICONTROL Publish to Brand Portal]** para abrir o agente de distribuição.

   Você pode ver as filas de distribuição na guia **[!UICONTROL Status]**.

   Um agente de distribuição contém duas filas:
   * **fila de processamento**: para distribuição de ativos no Brand Portal.

   * **fila de erros**: para os ativos em que a distribuição falhou.

   >[!NOTE]
   >
   >É recomendável analisar as falhas e limpar a **fila de erros** periodicamente.

   ![Fila de processamento para a distribuição de ativos](assets/test-bpconfig3.png)

1. Para verificar a conexão entre o Experience Manager Assets as a [!DNL Cloud Service] e o Brand Portal, clique no ícone **[!UICONTROL Testar Conexão]**.

   ![Verificar conexão entre AEM e Brand Portal](assets/test-bpconfig4.png)

   Aparece uma mensagem informando que o *pacote de teste foi entregue com êxito*.

   >[!NOTE]
   >
   >Evite desativar o agente de distribuição, pois isso pode causar falha na distribuição dos ativos (em execução na fila).

Para verificar a conexão entre sua instância do Experience Manager Assets as a [!DNL Cloud Service] e o locatário do Brand Portal, publique um ativo do Experience Manager Assets no Brand Portal. Se a conexão for bem-sucedida, o ativo publicado ficará visível na interface do Brand Portal.


Agora você pode:

* [Ativos Publish do Experience Manager Assets para o Brand Portal](publish-to-brand-portal.md)
* [Pastas Publish do Experience Manager Assets para o Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Coleções Publish do Experience Manager Assets para o Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Ativos do Publish do Brand Portal para o Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=pt-BR) - Origem de ativos no Brand Portal
* [Publicar predefinições, esquemas e aspectos no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar marcações no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Consulte a [documentação do Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para obter mais informações.

**Logs de distribuição**

É possível monitorar os logs do agente de distribuição para o fluxo de trabalho de publicação de ativos.

Vamos publicar um ativo do Experience Manager Assets no Brand Portal e ver os logs.

1. Siga as etapas (de 1 a 4) conforme mostrado na seção **Testar conexão** e navegue até a página do agente de distribuição.
1. Clique em **[!UICONTROL Logs]** para exibir os logs de processamento e de erros.

   ![Logs de processamento e erro](assets/test-bpconfig5.png)

O agente de distribuição gerou os seguintes registros:

* INFO: é um registro gerado pelo sistema que é acionado na configuração bem-sucedida do agente de distribuição.
* DSTRQ1 (Solicitação 1): acionado na conexão de teste.

Ao publicar o ativo, os seguintes registros de solicitação e resposta são gerados:

**Solicitação do agente de distribuição**:

* DSTRQ2 (Solicitação 2): a solicitação de publicação de ativo é acionada.
* DSTRQ3 (Solicitação 3): o sistema aciona outra solicitação para publicar a pasta do Experience Manager Assets (na qual o ativo existe) e replicar a pasta no Brand Portal.

**Resposta do agente de distribuição**:

* queue-bpdistributionagent0 (DSTRQ2): o ativo é publicado no Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): o sistema replica a pasta do Experience Manager Assets (que contém o ativo) no Brand Portal.

No exemplo acima, uma solicitação e uma resposta adicionais são acionadas. O sistema não pôde localizar a pasta principal (Adicionar caminho) no Brand Portal porque o ativo foi publicado pela primeira vez. Portanto, acionou uma solicitação adicional para criar uma pasta principal com o mesmo nome no Brand Portal onde o ativo é publicado.

>[!NOTE]
>
>A solicitação adicional é gerada caso a pasta principal não exista no Brand Portal ou tenha sido modificada no Experience Manager Assets.

Juntamente com o fluxo de trabalho de automação para ativar o Brand Portal no Experience Manager Assets como um [!DNL Cloud Service], existe outro método para configurar manualmente o Experience Manager Assets como um [!DNL Cloud Service] com o Brand Portal usando o Adobe Developer Console que não é mais recomendado.

>[!NOTE]
>
>Entre em contato com o Suporte ao cliente se estiver enfrentando algum problema ao ativar seu locatário do Brand Portal.

## Configuração manual usando o Adobe Developer Console {#manual-configuration}

>[!NOTE]
>
> Não é possível criar novas credenciais JWT a partir de junho de 2024. De agora em diante, somente as credenciais do OAuth são criadas.
> Veja mais [criando uma configuração OAuth](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration:~:text=For%20example%3A-,Creating%20an%20OAuth%20configuration,-To%20create%20a).

A seção a seguir descreve como configurar manualmente o Experience Manager Assets as a [!DNL Cloud Service] com o Brand Portal usando o Adobe Developer Console.

Anteriormente, o Experience Manager Assets as a [!DNL Cloud Service] era configurado manualmente com o Brand Portal via Adobe Developer Console, que obtém um token de conta do Adobe Identity Management Services (IMS) para autorização do locatário do Brand Portal. Ele requer configurações no Experience Manager Assets e no Adobe Developer Console.

<!--1. In Experience Manager Assets, create an IMS account and generate a public key (certificate).-->
<!--1. Under the project, configure an API using the public key to create a service account connection.
1. Get the service account credentials and JSON Web Token (JWT) payload information.
1. In Experience Manager Assets, configure the IMS account using the service account credentials and JWT payload.-->
1. No Adobe Developer Console, crie um projeto para seu locatário do Brand Portal (organização).
1. No Experience Manager Assets, configure o serviço em nuvem da Brand Portal usando a conta IMS e o terminal Brand Portal (URL da organização).
1. Teste sua configuração publicando um ativo do Experience Manager Assets no Brand Portal.

>[!NOTE]
>
>Uma instância do Experience Manager Assets as a [!DNL Cloud Service] só deve ser configurada com um locatário do Brand Portal.

**Pré-requisitos**

Você precisa do seguinte para configurar o Experience Manager Assets com o Brand Portal:

* Uma instância ativa e em execução do Experience Manager Assets as a [!DNL Cloud Service]
* Um URL de locatário do Brand Portal
* Um usuário com privilégios de administrador do sistema na organização IMS do locatário do Brand Portal

## Criar configuração {#create-new-configuration}

Execute as seguintes etapas na sequência especificada para configurar o Experience Manager Assets com o Brand Portal.

1. [Configurar as credenciais do OAuth no Adobe Developer Console](#config-oauth)
1. [Criar uma nova integração do Adobe IMS usando o OAuth](#create-ims-account-configuration)
1. [Configurar o serviço em nuvem](#configure-cloud-service)
   <!--1. [Obtain public certificate](#public-certificate)-->
<!--1. [Create service account (JWT) connection](#createnewintegration) 
1. [Configure IMS account](#create-ims-account-configuration)-->

<!--
### Create IMS configuration {#create-ims-configuration}

The IMS configuration authenticates your Experience Manager Assets as a [!DNL Cloud Service] instance with the Brand Portal tenant. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)
-->
<!--

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your profile on Adobe Developer Console.

1. Login to Experience Manager Assets.
1. From the **Tools** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.
1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. It will redirect to the **[!UICONTROL Adobe IMS Technical Account Configuration]** page. By default, the **Certificate** tab opens.
1. Select **[!UICONTROL Adobe Brand Portal]** in the **[!UICONTROL Cloud Solution]** drop-down list.  
1. Select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 
1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

   ![Create Certificate](assets/ims-config2.png)

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (CRT) file on your machine.

   The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.  

   ![Download Certificate](assets/ims-config3.png)

1. Click **[!UICONTROL Next]**.

    In the **Account** tab, Adobe IMS account is created which requires the service account credentials that are generated in Adobe Developer Console. Keep this page open for now.

    Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration) to get the credentials and JWT payload for configuring the IMS account. 
-->
<!--

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at Brand Portal tenant (organization) level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. To configure Experience Manager Assets with Brand Portal, you must generate a public key (certificate) in Experience Manager Assets and create credentials in Adobe Developer Console by uploading the public key. These credentials are required to configure the IMS account in Experience Manager Assets. Once the IMS account is configured, you can configure the Brand Portal cloud service in Experience Manager Assets.

Perform the following steps to generate the service account credentials and JWT payload:

1. Login to Adobe Developer Console with system administrator privileges on the IMS organization (Brand Portal tenant). The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Ensure that you have selected the correct IMS organization (Brand Portal tenant) from the drop-down (organization) list located at the upper-right corner.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]** to update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Next]**. 

   Ensure that you have access to the Experience Manager Brand Portal service.

1. In the **[!UICONTROL Configure API]** window, click **[!UICONTROL Upload your public key]**. Then, click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. 

   Click **[!UICONTROL Next]**.

   ![Upload Public Key](assets/service-account3.png)

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select **[!UICONTROL Assets Brand Portal]** as the default product profile and click **[!UICONTROL Save configured API]**. 

   ![Select Product Profile](assets/service-account4.png)

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option.

   >[!NOTE] 
   >
   >* You can view the credentials and perform actions such as generate JWT tokens, copy credential details, retrieve client secret, and so on.
   >* Currently, only the Adobe's Developer Console Service Account (JWT) credential type is supported. Do not use the `OAuth Server-to-Server` credential type until it is supported in mid-April. Read more at [JWT Credentials Deprecation in Adobe Developer Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html).

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Service Account Credentials](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in Experience Manager Assets.
-->
<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create an integration page. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information is used to create IMS account configuration.

-->

### Configurar as credenciais do OAuth no Adobe Developer Console {#config-oauth}

[Configure as credenciais do OAuth no Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#credentials-in-the-developer-console) e selecione a API do Brand Portal.

### Criar nova integração do Adobe IMS usando o OAuth {#create-ims-account-configuration}

[Crie uma nova Integração do Adobe IMS usando o OAuth](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service#creating-oauth-configuration) e selecione Brand Portal no menu suspenso em Solução da nuvem.

<!--
Ensure that you have performed the following steps:

* [Obtain public certificate](#public-certificate)
* [Create service account (JWT) connection](#createnewintegration)
-->

<!--1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. Keep the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, specify the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)  
-->
<!--
1. Complete the configuration based on details from the [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/). Click **[!UICONTROL Create]**.
-->
<!--Specify client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

   The IMS account is configured. 

   ![IMS Account configuration](assets/create-new-integration6.png)

 <!--  
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![Adobe IMS Configurations Check Health.](assets/create-new-integration5.png)
-->
<!--
>[!CAUTION]
>
>You must have only one IMS configuration.
>
>Ensure that the IMS configuration passes the health check. If the configuration does not pass the health check, it is invalid. You must delete it and create another valid configuration.
-->

### Configurar o serviço em nuvem {#configure-cloud-service}

Execute as seguintes etapas para configurar o Brand Portal Cloud Service:

1. Faça logon no Experience Manager Assets.

1. No painel **Ferramentas**, navegue até **[!UICONTROL Cloud Service]** > **[!UICONTROL AEM Brand Portal]**.

1. Na página Configurações do Brand Portal, clique em **[!UICONTROL Criar]**.

1. Especifique um **[!UICONTROL Título]** para a configuração.

   Selecione a configuração IMS criada ao [configurar a conta IMS](#create-ims-account-configuration).

   No campo **[!UICONTROL URL do Serviço]**, especifique a URL do locatário (organização) da Brand Portal.

   ![Caixa de diálogo Configuração do Brand Portal.](assets/create-cloud-service.png)

1. Clique em **[!UICONTROL Salvar e fechar]**. A configuração da nuvem é criada.

   Sua instância do Experience Manager Assets as a [!DNL Cloud Service] agora está configurada com o locatário do Brand Portal.

Agora você pode testar a configuração verificando o agente de distribuição e publicando ativos no Brand Portal.

**Incluir na lista de permissões IPs de saída no SPS se a visualização segura estiver habilitada**
Se estiver usando o Dynamic Media-Scene7 com a [visualização segura](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en) habilitada para uma empresa, recomenda-se que o administrador da empresa Scene7 [inclua na lista de permissões os IPs de saída públicos](#https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en#testing-the-secure-testing-service) para as respectivas regiões usando a interface flash do SPS (Scene7 Publishing System).
Os IPs de saída são os seguintes:

| **Região** | **IP de saída** |
|--- |--- |
| ND | 130 248 160 68 20 94 203 130 |
| EMEA | 51.132.146.75, 130.248.244.202, 130.248.244.203, 130.248.244.204, 130.248.244.210, 130.248.244.211, 130.248.244.212 |
| APAC | 63.140.44.54 |

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Login to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![test-bpconfig1](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![test-bpconfig2](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![test-bpconfig3](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click the **[!UICONTROL Test Connection]** icon.

   ![test-bpconfig4](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![ctest-bpconfig4](assets/ctest-bpconfig4.png)

The distribution agent has generated the following logs:

* INFO: This is a system-generated log that triggers on successful configuration of the distribution agent. 
* DSTRQ1 (Request 1): Triggers on test connection.

On publishing the asset, the following request and response logs are generated:

**Distribution agent request**:

* DSTRQ2 (Request 2): The asset publishing request is triggered.
* DSTRQ3 (Request 3): The system triggers another request to publish the AEM Assets folder (in which the asset exists) and replicates the folder in Brand Portal.

**Distribution agent response**:

* queue-bpdistributionagent0 (DSTRQ2): The asset is published to Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): The system replicates the AEM Assets folder (containing the asset) in Brand Portal.

In the above example, an additional request and response is triggered. The system could not find the parent folder (Add Path) in Brand Portal because the asset was published for the first time, therefore, it triggered an additional request to create a parent folder with the same name in Brand Portal where the asset is published.  

>[!NOTE]
>
>Additional request is generated in case the parent folder does not exist in Brand Portal or has been modified in AEM Assets. 
-->

<!--

## Additional information {#additional-information}

Go to `/system/console/slingmetrics` for statistics related to the distributed content:

1. **Counter metrics**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Time metrics**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`

-->

<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
-->

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publish Assets para AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
