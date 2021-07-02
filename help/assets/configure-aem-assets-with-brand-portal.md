---
title: Configurar o AEM Assets as a [!DNL Cloud Service] com o Brand Portal
description: Configurar o AEM Assets com o Brand Portal.
contentOwner: Vishabh Gupta
feature: Brand Portal,Distribuição de ativos,Configuração
role: Administrator
exl-id: 078e522f-bcd8-4734-95db-ddc8772de785
source-git-commit: 9d219b8de11fd977dab4f75468836892cb13364a
workflow-type: tm+mt
source-wordcount: '2409'
ht-degree: 12%

---

# Configurar o AEM Assets as a [!DNL Cloud Service] com o Brand Portal {#configure-aem-assets-with-brand-portal}

A configuração do Adobe Experience Manager Assets Brand Portal permite publicar ativos de marca aprovados do Adobe Experience Manager Assets como uma instância [!DNL Cloud Service] no Brand Portal e distribuí-los aos usuários do Brand Portal.

## Ativar o Brand Portal usando o Cloud Manager {#activate-brand-portal}

O usuário do Cloud Manager ativa o Brand Portal para uma instância do AEM Assets como [!DNL Cloud Service]. O fluxo de trabalho de ativação cria as configurações necessárias (token de autorização, configuração IMS e serviço de nuvem do Brand Portal) no back-end e reflete o status do locatário do Brand Portal no Cloud Manager. Ativar o Brand Portal permite que os usuários do AEM Assets publiquem ativos no Brand Portal e os distribuam para os usuários do Brand Portal.

**Pré-requisitos**

Você precisa do seguinte para ativar o Brand Portal em seu AEM Assets como uma instância [!DNL Cloud Service]:

* Uma instância ativa e em execução do AEM Assets como [!DNL Cloud Service].
* Um usuário com acesso ao Cloud Manager, atribuído aos Perfis do Cloud Manager Product. Consulte [acessar o Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#accessing-cloud-manager) para obter mais informações.

>[!NOTE]
>
>Uma instância do AEM Assets as a [!DNL Cloud Service] tem direito a se conectar a apenas um locatário do Brand Portal. Você pode ter vários ambientes (desenvolvimento, produção e estágio) para seu AEM Assets como uma instância [!DNL Cloud Service], onde o Brand Portal é ativado em um ambiente.

**Etapas para ativar o Brand Portal**

Você pode ativar o Brand Portal ao criar os ambientes para sua AEM Assets como uma instância [!DNL Cloud Service] ou separadamente. Vamos supor que os ambientes já foram criados e agora você precisa ativar o Brand Portal.

1. Faça logon no Adobe Cloud Manager e navegue até **[!UICONTROL Ambientes]**.

   A página **[!UICONTROL Ambientes]** exibe a lista de todos os ambientes existentes.

1. Selecione os ambientes (um por um) na lista para exibir os detalhes do ambiente.

   O Brand Portal tem direito a um dos ambientes disponíveis e é refletido no **[!UICONTROL Environment Information]**.

   Depois de encontrar o ambiente associado ao Brand Portal, clique no botão **[!UICONTROL Ativate Brand Portal]** para iniciar o workflow de ativação.

   ![Ativar o Brand Portal](assets/create-environment4.png)

1. São necessários alguns minutos para ativar o locatário do Brand Portal, pois o fluxo de trabalho de ativação cria as configurações necessárias no back-end. Quando o locatário do Brand Portal é ativado, o status é alterado para Ativado.

   ![Exibir status](assets/create-environment5.png)


>[!NOTE]
>
>O Brand Portal deve ser ativado na mesma organização IMS do AEM Assets como uma instância [!DNL Cloud Service].
>
>Se você tiver uma configuração de nuvem Brand Portal existente ([manualmente configurada usando o Adobe Developer Console](#manual-configuration)) para uma organização IMS (org1-existing) e seu AEM Assets como uma instância [!DNL Cloud Service] estiver configurado para outra organização IMS (org2-new), ativar o Brand Portal no Cloud Manager redefinirá a organização do Brand Portal IMS para `org2-new`. Embora a configuração de nuvem configurada manualmente em `org1-existing` esteja visível na instância do autor do AEM Assets, mas não estará mais em uso após ativar o Brand Portal no Cloud Manager.
>
>Se a configuração de nuvem existente do Brand Portal e a instância do AEM Assets as [!DNL Cloud Service] estiverem usando a mesma organização IMS (org1), será necessário ativar o Brand Portal somente no Cloud Manager.

**Consulte também**:
* [Adicionar usuários e funções no AEM Assets as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en)

* [Gerenciar ambientes no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#adding-environments)


**Faça logon no locatário** do Brand Portal:

Após a ativação do locatário do Brand Portal no Cloud Manager, é possível fazer logon no Brand Portal pelo Admin Console ou diretamente usando o URL do locatário.

O URL padrão do seu locatário do Brand Portal é: `https://<tenant-id>.brand-portal.adobe.com/`.

Onde, a ID do locatário é a organização IMS.

Execute as seguintes etapas se não tiver certeza do URL do Brand Portal:

1. Faça logon em [Admin Console](http://adminconsole.adobe.com/) e navegue até **[!UICONTROL Produtos]**.
1. No painel esquerdo, selecione **[!UICONTROL Adobe Experience Manager Brand Portal - Brand Portal]**.
1. Clique em **[!UICONTROL Vá para Brand Portal]** para abrir diretamente o Brand Portal no navegador.

   Ou copie o URL do locatário do Brand Portal do link **[!UICONTROL Ir para Brand Portal]** e cole-o em seu navegador para abrir a interface do Brand Portal.

   ![Acessar o Brand Portal](assets/access-bp-on-cloud.png)


**Testar conexão**

Execute as etapas a seguir para validar a conexão entre sua AEM Assets como uma instância [!DNL Cloud Service] e o locatário do Brand Portal:

1. Faça logon no AEM Assets.

1. No painel **Ferramentas**, navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Distribuição]**.

   ![](assets/test-bpconfig1.png)

   Um agente de distribuição Brand Portal (**[!UICONTROL bpdistributionagent0]**) é criado em **[!UICONTROL Publicar no Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Clique em **[!UICONTROL Publicar no Brand Portal]** para abrir o agente de distribuição.

   Você pode ver as filas de distribuição na guia **[!UICONTROL Status]**.

   Um agente de distribuição contém duas filas:
   * **fila de processamento**: para distribuição de ativos no Brand Portal.

   * **fila de erros**: para os ativos em que a distribuição falhou.
   >[!NOTE]
   >
   >É recomendável analisar as falhas e limpar a **fila de erros** periodicamente.

   ![](assets/test-bpconfig3.png)

1. Para verificar a conexão entre o AEM Assets as a [!DNL Cloud Service] e o Brand Portal, clique no ícone **[!UICONTROL Testar conexão]**.

   ![](assets/test-bpconfig4.png)

   Aparece uma mensagem de que seu *pacote de teste foi entregue com êxito*.

   >[!NOTE]
   >
   >Evite desativar o agente de distribuição, pois isso pode causar falha na distribuição dos ativos (em execução na fila).

Para verificar a conexão entre sua instância do AEM Assets as a [!DNL Cloud Service] e o locatário do Brand Portal, publique um ativo do AEM Assets para o Brand Portal. Se a conexão for bem-sucedida, o ativo publicado estará visível na interface do Brand Portal.


Agora você pode:

* [Publicar ativos do AEM Assets no Brand Portal](publish-to-brand-portal.md)
* [Publicar pastas do AEM Assets no Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicar coleções do AEM Assets no Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publicar ativos do Brand Portal no AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=en)  - Origem de ativos no Brand Portal
* [Publicar predefinições, esquemas e aspectos no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar marcações no Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

Consulte a [documentação do Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para obter mais informações.

**Registros de distribuição**

Você pode monitorar os registros do agente de distribuição para o fluxo de trabalho de publicação de ativos.

Agora, vamos publicar um ativo do AEM Assets para o Brand Portal e ver os logs.

1. Siga as etapas (de 1 a 4) conforme mostrado na seção **Testar conexão** e navegue até a página do agente de distribuição.
1. Clique em **[!UICONTROL Logs]** para visualizar o processamento e os logs de erro.

   ![](assets/test-bpconfig5.png)

O agente de distribuição gerou os seguintes logs:

* INFORMAÇÕES: É um registro gerado pelo sistema que dispara para uma configuração bem-sucedida do agente de distribuição.
* DSTRQ1 (Solicitação 1): acionado na conexão de teste.

Ao publicar o ativo, os seguintes registros de solicitação e resposta são gerados:

**Solicitação do agente de distribuição**:

* DSTRQ2 (Solicitação 2): a solicitação de publicação de ativo é acionada.
* DSTRQ3 (Solicitação 3): O sistema aciona outra solicitação para publicar a pasta do AEM Assets (na qual o ativo existe) e replicar a pasta no Brand Portal.

**Resposta do agente de distribuição**:

* queue-bpdistributionagent0 (DSTRQ2): o ativo é publicado no Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): O sistema replica a pasta AEM Assets (contendo o ativo) no Brand Portal.

No exemplo acima, uma solicitação e uma resposta adicionais são acionadas. O sistema não pôde localizar a pasta principal (Adicionar caminho) no Brand Portal porque o ativo foi publicado pela primeira vez, portanto, acionou uma solicitação adicional para criar uma pasta principal com o mesmo nome no Brand Portal, onde o ativo é publicado.

>[!NOTE]
>
>A solicitação adicional é gerada caso a pasta principal não exista no Brand Portal ou tenha sido modificada no AEM Assets.

Junto com o fluxo de trabalho de automação para ativar o Brand Portal no AEM Assets como um [!DNL Cloud Service], existe outro método para configurar manualmente o AEM Assets como um [!DNL Cloud Service] com o Brand Portal usando o Console do Desenvolvedor do Adobe, o que não é mais recomendado.

>[!NOTE]
>
>Entre em contato com o Suporte do Adobe se tiver algum problema ao ativar o locatário do Brand Portal.

## Configuração manual usando o Console do desenvolvedor do Adobe {#manual-configuration}

A seção a seguir descreve como configurar manualmente o AEM Assets as a [!DNL Cloud Service] com o Brand Portal usando o Console do Desenvolvedor do Adobe.

Anteriormente, o AEM Assets as a [!DNL Cloud Service] era configurado manualmente com o Brand Portal via Console do Desenvolvedor do Adobe, que obtém um token de conta do Adobe Identity Management Services (IMS) para autorização do locatário do Brand Portal. Ela requer configurações no AEM Assets e no Console do desenvolvedor do Adobe.

1. No AEM Assets, crie uma conta IMS e gere uma chave pública (certificado).
1. No Console do desenvolvedor do Adobe, crie um projeto para seu locatário do Brand Portal (organização).
1. No projeto, configure uma API usando a chave pública para criar uma conexão de conta de serviço.
1. Obtenha as credenciais da conta de serviço e as informações de carga JSON Web Token (JWT).
1. No AEM Assets, configure a conta IMS usando as credenciais da conta de serviço e a carga JWT.
1. No AEM Assets, configure o serviço de nuvem da Brand Portal usando a conta IMS e o terminal Brand Portal (URL da organização).
1. Teste sua configuração publicando um ativo do AEM Assets para o Brand Portal.

>[!NOTE]
>
>Uma instância do AEM Assets como [!DNL Cloud Service] só deve ser configurada com um locatário do Brand Portal.

**Pré-requisitos**

Você precisa do seguinte para configurar o AEM Assets com o Brand Portal:

* Criar e executar o AEM Assets como uma instância [!DNL Cloud Service]
* Um URL de locatário do Brand Portal
* Um usuário com privilégios de administrador do sistema na organização IMS do locatário do Brand Portal

## Criar configuração {#create-new-configuration}

Execute as etapas a seguir na sequência especificada para configurar o AEM Assets com o Brand Portal.

1. [Obter certificado público](#public-certificate)
1. [Criar conexão de conta de serviço (JWT)](#createnewintegration)
1. [Configurar conta IMS](#create-ims-account-configuration)
1. [Configurar o serviço em nuvem](#configure-the-cloud-service)

### Criar configuração IMS {#create-ims-configuration}

A configuração IMS autentica sua AEM Assets como uma instância [!DNL Cloud Service] com o locatário do Brand Portal.

A configuração IMS inclui duas etapas:

* [Obter certificado público](#public-certificate)
* [Configurar conta IMS](#create-ims-account-configuration)

### Obter certificado público {#public-certificate}

A chave pública (certificado) autentica seu perfil no Console do desenvolvedor do Adobe.

1. Faça logon no AEM Assets.
1. No painel **Ferramentas**, navegue até **[!UICONTROL Segurança]** > **[!UICONTROL Adobe IMS Configurations]**.
1. Na página Configurações do Adobe IMS , clique em **[!UICONTROL Criar]**. Ele redirecionará para a página **[!UICONTROL Adobe IMS Technical Account Configuration]** . Por padrão, a guia **Certificate** é aberta.
1. Selecione **[!UICONTROL Adobe Brand Portal]** na lista suspensa **[!UICONTROL Cloud Solution]**.
1. Marque a caixa de seleção **[!UICONTROL Create new certificate]** e especifique um **alias** para a chave pública. O alias serve como nome da chave pública.
1. Clique em **[!UICONTROL Criar certificado]**. Em seguida, clique em **[!UICONTROL OK]** para gerar a chave pública.

   ![Criar certificado](assets/ims-config2.png)

1. Clique no ícone **[!UICONTROL Baixar chave pública]** e salve o arquivo de chave pública (CRT) no computador.

   A chave pública é usada posteriormente para configurar a API do locatário do Brand Portal e gerar credenciais de conta de serviço no Console do desenvolvedor do Adobe.

   ![Baixar certificado](assets/ims-config3.png)

1. Clique em **[!UICONTROL Avançar]**.

   Na guia **Account**, é criada a conta Adobe IMS que requer as credenciais da conta de serviço geradas no Console do Desenvolvedor do Adobe. Mantenha esta página aberta por enquanto.

   Abra uma nova guia e [crie uma conexão de conta de serviço (JWT) no Console do Desenvolvedor do Adobe](#createnewintegration) para obter as credenciais e a carga JWT para configurar a conta IMS.

### Criar conexão de conta de serviço (JWT) {#createnewintegration}

No Console do desenvolvedor do Adobe, os projetos e as APIs são configurados no nível de locatário (organização) do Brand Portal. Configurar uma API cria uma conexão de conta de serviço (JWT). Há dois métodos para configurar a API, gerando um par de chaves (chaves privadas e públicas) ou carregando uma chave pública. Para configurar o AEM Assets com o Brand Portal, você deve gerar uma chave pública (certificado) no AEM Assets e criar credenciais no Console do desenvolvedor do Adobe fazendo upload da chave pública. Essas credenciais são necessárias para configurar a conta IMS no AEM Assets. Após configurar a conta IMS, é possível configurar o serviço de nuvem da Brand Portal no AEM Assets.

Execute as seguintes etapas para gerar as credenciais da conta de serviço e a carga JWT:

1. Faça logon no Console do desenvolvedor do Adobe com privilégios de administrador de sistema na organização IMS (locatário do Brand Portal). O URL padrão é [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Certifique-se de ter selecionado a organização IMS correta (locatário do Brand Portal) na lista suspensa (organização) localizada no canto superior direito.

1. Clique em **[!UICONTROL Criar novo projeto]**. Um projeto em branco com um nome gerado pelo sistema é criado para sua organização.

   Clique em **[!UICONTROL Editar projeto]** para atualizar o **[!UICONTROL Título do projeto]** e **[!UICONTROL Descrição]** e clique em **[!UICONTROL Salvar]**.

1. Na guia **[!UICONTROL Visão geral do projeto]**, clique em **[!UICONTROL Adicionar API]**.

1. Na janela **[!UICONTROL Adicionar uma API]**, selecione **[!UICONTROL AEM Brand Portal]** e clique em **[!UICONTROL Próximo]**.

   Certifique-se de ter acesso ao serviço AEM Brand Portal.

1. Na janela **[!UICONTROL Configure API]**, clique em **[!UICONTROL Upload your public key]**. Em seguida, clique em **[!UICONTROL Selecione um Arquivo]** e faça upload da chave pública (arquivo .crt) que você baixou na seção [obter certificado público](#public-certificate).

   Clique em **[!UICONTROL Avançar]**.

   ![Fazer upload da chave pública](assets/service-account3.png)

1. Verifique a chave pública e clique em **[!UICONTROL Next]**.

1. Selecione **[!UICONTROL Assets Brand Portal]** como o perfil de produto padrão e clique em **[!UICONTROL Salvar API configurada]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Selecionar Perfil de Produto](assets/service-account4.png)

1. Depois que a API for configurada, você será redirecionado para a página de visão geral da API. Na navegação à esquerda em **[!UICONTROL Credentials]**, clique na opção **[!UICONTROL Service Account (JWT)]**.

   >[!NOTE]
   >
   >Você pode exibir as credenciais e executar ações como gerar tokens JWT, copiar detalhes da credencial, recuperar o segredo do cliente e assim por diante.

1. Na guia **[!UICONTROL Credenciais do cliente]** , copie o **[!UICONTROL ID do cliente]**.

   Clique em **[!UICONTROL Recuperar Segredo do Cliente]** e copie o **[!UICONTROL segredo do cliente]**.

   ![Credenciais da Conta de Serviço](assets/service-account5.png)

1. Navegue até a guia **[!UICONTROL Generate JWT]** e copie as informações **[!UICONTROL JWT Payload]**.

Agora você pode usar a ID do cliente (chave de API), o segredo do cliente e a carga JWT para [configurar a conta IMS](#create-ims-account-configuration) no AEM Assets.

<!--
1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
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

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.

-->

### Configurar conta IMS {#create-ims-account-configuration}

Verifique se você executou as seguintes etapas:

* [Obter certificado público](#public-certificate)
* [Criar conexão de conta de serviço (JWT)](#createnewintegration)

Execute as etapas a seguir para configurar a conta IMS.

1. Abra a Configuração IMS e navegue até a guia **[!UICONTROL Account]**. Você manteve a página aberta enquanto [obtinha o certificado público](#public-certificate).

1. Especifique um **[!UICONTROL Título]** para a conta IMS.

   No campo **[!UICONTROL Servidor de autorização]**, especifique o URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Especifique a ID do cliente no campo **[!UICONTROL Chave da API]**, **[!UICONTROL Segredo do Cliente]** e **[!UICONTROL Carga]** (Carga JWT) que copiou enquanto [cria a conexão da conta de serviço (JWT)](#createnewintegration).

   Clique em **[!UICONTROL Criar]**.

   A conta IMS está configurada.

   ![Configurar a conta IMS](assets/create-new-integration6.png)


1. Selecione a configuração da conta IMS e clique em **[!UICONTROL Verificar integridade]**.

   Clique em **[!UICONTROL Marcar]** na caixa de diálogo. Na configuração bem-sucedida, uma mensagem é exibida informando que o token *foi recuperado com êxito*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Você deve ter apenas uma configuração IMS.
>
>A configuração IMS deve ser aprovada na verificação de integridade. Se a configuração não for aprovada na verificação de integridade, ela será inválida. Você deve excluí-la e criar uma configuração nova e válida.

### Configurar o serviço em nuvem {#configure-the-cloud-service}

Execute as seguintes etapas para configurar o serviço de nuvem do Brand Portal:

1. Faça logon no AEM Assets.

1. No painel **Ferramentas**, navegue até **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Na página Configurações do Brand Portal , clique em **[!UICONTROL Criar]**.

1. Especifique um **[!UICONTROL Título]** para a configuração.

   Selecione a configuração IMS que você criou ao [configurar a conta IMS](#create-ims-account-configuration).

   No campo **[!UICONTROL URL do serviço]**, especifique o URL do locatário (organização) do Brand Portal.

   ![](assets/create-cloud-service.png)

1. Clique em **[!UICONTROL Salvar e fechar]**. A configuração da nuvem é criada.

   Sua instância do AEM Assets as a [!DNL Cloud Service] agora está configurada com o locatário do Brand Portal.

Agora é possível testar a configuração, verificando o agente de distribuição e publicando ativos no Brand Portal.

<!--
### Test configuration {#test-configuration}

Perform the following steps to validate the configuration:

1. Log in to AEM Assets.

1. From the **Tools** panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

    ![](assets/test-bpconfig1.png)

   A Brand Portal distribution agent (**[!UICONTROL bpdistributionagent0]**) is created under **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)


1. Click **[!UICONTROL Publish to Brand Portal]** to open the distribution agent. 

   You can see the distribution queues under the **[!UICONTROL Status]** tab. 
   
   A distribution agent contains two queues: 
   * **processing-queue**: for the distribution of assets to Brand Portal. 

   * **error-queue**: for the assets where distribution has failed. 
   
   >[!NOTE]
   >
   >It is recommended to review the failures and  clear the **error-queue** periodically.  

   ![](assets/test-bpconfig3.png)

1. To verify the connection between AEM Assets as a [!DNL Cloud Service] and Brand Portal, click on the **[!UICONTROL Test Connection]** icon.

   ![](assets/test-bpconfig4.png)

   A message appears that your *test package is successfully delivered*.

   >[!NOTE]
   >
   >Avoid disabling the distribution agent, as it can cause the distribution of the assets (running-in-queue) to fail.

You can now:

* [Publish assets from AEM Assets to Brand Portal](publish-to-brand-portal.md)
* [Publish folders from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publish collections from AEM Assets to Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)
* [Publish assets from Brand Portal to AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=en) - Asset Sourcing in Brand Portal
* [Publish presets, schemas, and facets to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publish tags to Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)

See [Brand Portal documentation](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) for more information.

## Distribution logs {#distribution-logs}

You can monitor the distribution agent logs for the asset publishing workflow. 

For example, we have published an asset from AEM Assets to Brand Portal to validate the configuration. 

1. Follow the steps (from 1 to 4) as shown in the [Test Configuration](#test-configuration) section and navigate to the distribution agent page.
1. Click **[!UICONTROL Logs]** to view the processing and error logs.

   ![](assets/test-bpconfig5.png)

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
