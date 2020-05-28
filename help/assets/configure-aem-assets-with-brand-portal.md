---
title: Configurar o serviço em nuvem do AEM Assets com o Brand Portal
description: Configurar o serviço em nuvem do AEM Assets com o Brand Portal
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 3cb9ea561dbe55ac7ed43ff47e5b57563eaa3f67
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 37%

---


# Configurar o AEM Assets com o Brand Portal {#configure-aem-assets-with-brand-portal}

Os ativos Adobe Experience Manager (AEM) são configurados com o Brand Portal por meio do Adobe Developer Console, que obtém um token IMS para autorização do locatário do Brand Portal.

**Como a configuração funciona?**

A configuração da instância da nuvem do AEM Assets com um locatário do Brand Portal (organização) requer configurações tanto na instância da nuvem do AEM Assets quanto no Adobe Developer Console.

1. Na instância da nuvem do AEM Assets, crie uma conta IMS e gere um certificado público (chave pública).
1. No Adobe Developer Console, crie um projeto para seu locatário do Brand Portal (organização).
1. No projeto, configure uma API usando a chave pública para criar uma conexão de conta de serviço (JWT).
1. Obtenha as credenciais da conta de serviço e as informações de carga JWT.
1. Na instância da nuvem do AEM Assets, configure a conta IMS usando as credenciais da conta de serviço e a carga JWT.
1. Na instância da nuvem do AEM Assets, configure o serviço em nuvem do Brand Portal usando a conta IMS e o terminal do Brand Portal (URL da organização).
1. Teste a configuração publicando um ativo da instância de nuvem do AEM Assets no Brand Portal.

>[!NOTE]
>
>Um locatário do Brand Portal só deve ser configurado com uma instância da nuvem do AEM Assets.
>
>Não configure um locatário do Brand Portal com várias instâncias da nuvem do AEM Assets.


## Pré-requisitos {#prerequisites}

Você precisa do seguinte para configurar o AEM Assets com o Brand Portal:

* Uma instância da nuvem ativa e em execução do AEM Assets.
* URL do locatário do Brand Portal.
* Um usuário com privilégios de administrador do sistema na organização IMS do locatário do Brand Portal.

**Entre em contato com o Atendimento** ao cliente para obter mais query.

## Criar configuração {#create-new-configuration}

Execute as seguintes etapas na sequência especificada para configurar a instância da nuvem do AEM Assets com o Brand Portal.

1. [Obter certificado público](#public-certificate)
1. [Criar conexão de conta de serviço (JWT)](#createnewintegration)
1. [Configurar conta IMS](#create-ims-account-configuration)
1. [Configurar o serviço em nuvem](#configure-the-cloud-service)
1. [Testar configuração](#test-configuration)

### Criar configuração IMS {#create-ims-configuration}

A configuração IMS autentica seu locatário do Brand Portal com a instância do autor do AEM Assets.

A configuração IMS inclui duas etapas:

* [Obter certificado público](#public-certificate)
* [Configurar conta IMS](#create-ims-account-configuration)

### Obter certificado público {#public-certificate}

O certificado público permite autenticar seu perfil no Adobe Developer Console.

1. Faça logon na instância da nuvem do AEM Assets.

1. From the **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

   ![Interface do usuário de configuração de conta do Adobe IMS](assets/ims-configuration1.png)

1. Na página Configurações do Adobe IMS, clique em **[!UICONTROL Criar]**.

1. Você é redirecionado para a página Configuração **[!UICONTROL técnica da conta do]** Adobe IMS. By default, the **Certificate** tab opens.

   Selecione a solução em nuvem Portal **[!UICONTROL da marca da]** Adobe.

1. Marque a caixa de seleção **[!UICONTROL Criar novo certificado]** e especifique um **alias** para o certificado. O alias atua como nome da caixa de diálogo.

1. Clique em **[!UICONTROL Criar certificado]**. Em seguida, clique em **[!UICONTROL OK]** na caixa de diálogo para gerar o certificado público.

   ![Criar certificado](assets/ims-config2.png)

1. Click **[!UICONTROL Download Public Key]** and save the certificate (.crt) file on your machine.

   O arquivo de certificado será usado em outras etapas para configurar a API para o locatário do Brand Portal e gerar credenciais de conta de serviço no Adobe Developer Console.

   ![Baixar certificado](assets/ims-config3.png)

1. Clique em **[!UICONTROL Avançar]**.

   Na guia **Conta** , crie a conta Adobe IMS, mas para isso você precisará das credenciais da conta de serviço geradas no Adobe Developer Console. Mantenha esta página aberta por enquanto.

   Abra uma nova guia e [crie uma conexão de conta de serviço (JWT) no Adobe Developer Console](#createnewintegration) para obter as credenciais e a carga JWT para configurar a conta IMS.

### Criar conexão de conta de serviço (JWT) {#createnewintegration}

No Adobe Developer Console, os projetos e as APIs são configurados no nível da organização (locatário do Brand Portal). Configurar uma API cria uma conexão de conta de serviço (JWT) no Adobe Developer Console. Há dois métodos para configurar a API, gerando um par de chaves (chaves privadas e públicas) ou carregando uma chave pública. Para configurar a instância da nuvem do AEM Assets com o Brand Portal, você deve gerar um certificado público (chave pública) na instância da nuvem do AEM Assets e criar credenciais no Adobe Developer Console fazendo upload da chave pública. Essa chave pública é usada para configurar a API para a organização selecionada do Brand Portal e gera as credenciais e a carga JWT para a conta de serviço. Essas credenciais são usadas ainda mais para configurar a conta IMS na instância da nuvem do AEM Assets. Depois que a conta IMS for configurada, você poderá configurar o serviço em nuvem do Brand Portal na instância em nuvem do AEM Assets.

Execute as seguintes etapas para gerar as credenciais da conta de serviço e a carga JWT:

1. Faça logon no Adobe Developer Console com privilégios de administrador do sistema na organização IMS (locatário do Brand Portal). O URL padrão é

   [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui)


   >[!NOTE]
   >
   >Verifique se você selecionou a organização IMS correta (locatário do Brand Portal) na lista suspensa (lista da organização) localizada no canto superior direito.

1. Click **[!UICONTROL Create new project]**. Um projeto em branco é criado para sua organização.

   Clique em **[!UICONTROL Editar projeto]** para atualizar o Título **[!UICONTROL e a]** Descrição **[!UICONTROL do]** projeto e clique em **[!UICONTROL Salvar]**.

   ![Criar projeto](assets/service-account1.png)

1. Na guia Visão geral do projeto, clique em **[!UICONTROL Adicionar API]**.

   ![Adicionar API](assets/service-account2.png)

1. Na janela Adicionar uma API, selecione **[!UICONTROL AEM Brand Portal]** e clique em **[!UICONTROL Avançar]**.

   Certifique-se de ter acesso ao serviço AEM Brand Portal.

1. Na janela Configurar API, clique em **[!UICONTROL Carregar sua chave]** pública. Em seguida, clique em **[!UICONTROL Selecionar um arquivo]** e faça upload do certificado público (arquivo .crt) que você baixou na seção [obter certificado](#public-certificate) público.

   Clique em **[!UICONTROL Avançar]**.

   ![Carregar chave pública](assets/service-account3.png)

1. Verifique o certificado público e clique em **[!UICONTROL Avançar]**.

1. Selecione o perfil de produto padrão Portal **[!UICONTROL de marcas de]** Ativos de marca e clique em **[!UICONTROL Salvar configuração]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Selecionar Perfil do produto](assets/service-account4.png)

1. Com a API configurada, você é redirecionado para a visão geral da API. Na navegação à esquerda em **[!UICONTROL Credenciais]**, clique em **[!UICONTROL Service Account (JWT)]**.

   >[!NOTE]
   >
   >Você pode visualização as credenciais e executar outras ações (gerar tokens JWT, copiar detalhes das credenciais, recuperar o segredo do cliente e assim por diante) conforme necessário.

1. Na guia Credenciais **[!UICONTROL do]** cliente, copie a ID **[!UICONTROL do]** cliente.

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![Credenciais da Conta de Serviço](assets/service-account5.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]**.

Agora você pode usar a ID do cliente (chave da API), o segredo do cliente e a carga JWT para [configurar a conta](#create-ims-account-configuration) IMS na instância da nuvem do AEM Assets.

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

Execute as seguintes etapas para configurar a conta IMS que você criou na [obtenção de um certificado](#public-certificate)público.

1. Abra a Configuração IMS e navegue até a guia **[!UICONTROL Contas]** . Você manteve a página aberta enquanto [obtinha o certificado](#public-certificate)público.

1. Especifique um **[!UICONTROL Título]** para a conta IMS.

   No **[!UICONTROL Servidor de autorização]**, insira o URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Cole a ID do cliente na chave da API, o segredo do cliente e a carga JWT que você copiou ao [criar a conexão](#createnewintegration)da conta de serviço (JWT).

   Clique em **[!UICONTROL Criar]**.

   A conta IMS está configurada.

   ![Configurar a conta IMS](assets/create-new-integration6.png)


1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Clique em **[!UICONTROL Verificar]** na caixa de diálogo. Na configuração bem-sucedida, será exibida uma mensagem informando que o *Token foi recuperado com êxito*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Você deve ter apenas uma configuração IMS. Não crie várias configurações IMS.
>
>A configuração IMS deve ser aprovada na verificação de integridade. Se a configuração não for aprovada na verificação de integridade, ela será inválida. Você deve excluí-la e criar uma configuração nova e válida.



### Configurar o serviço em nuvem {#configure-the-cloud-service}

Execute as seguintes etapas para configurar o serviço em nuvem do Brand Portal:

1. Faça logon na instância da nuvem do AEM Assets.

1. From the **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Na página Configurações do Brand Portal, clique em **[!UICONTROL Criar]**.

1. Especifique um **[!UICONTROL Título]** para a configuração.

   Selecione a configuração IMS que você criou ao [configurar a conta](#create-ims-account-configuration)IMS.

   In the **[!UICONTROL Service URL]**, enter your Brand Portal tenant (organization URL).

   ![](assets/create-cloud-service.png)

1. Clique em **[!UICONTROL Salvar e fechar]**. A configuração da nuvem é criada. A instância da nuvem do AEM Assets agora está configurada com o locatário do Brand Portal.

### Testar configuração{#test-configuration}

Execute as seguintes etapas para validar a configuração:

1. Faça logon na instância da nuvem do AEM Assets.

1. From the **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Distribution]**.

   ![](assets/test-bpconfig1.png)

1. Na página Distribuição, você pode ver que um agente de distribuição do Brand Portal `bpdistributionagent0` é criado para **[!UICONTROL Publicar no Brand Portal]**.

   Clique em **[!UICONTROL Publicar no Brand Portal]**

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >Por padrão, um agente de distribuição é criado para um locatário do Brand Portal.

1. Na página do agente de distribuição, você pode ver as filas de distribuição na guia **[!UICONTROL Status]** .

   Um agente de distribuição contém duas filas:
   * **fila de processamento**: para distribuição de ativos no Brand Portal.

   * **fila de erros**: para os ativos em que a distribuição falhou.
   >[!NOTE]
   >
   >É recomendável analisar as falhas e limpar a **fila de erros** periodicamente.

   ![](assets/test-bpconfig3.png)

1. Para verificar a conexão entre o AEM Assets e o Brand Portal, clique em **[!UICONTROL Testar conexão]**.

   ![](assets/test-bpconfig4.png)

   Uma mensagem é exibida na parte inferior da página informando que o pacote de teste foi entregue com êxito.

   >[!NOTE]
   >
   >Evite desativar o agente de distribuição, pois isso pode causar falha na distribuição dos ativos (em execução na fila).


A instância da nuvem do AEM Assets foi configurada com êxito com o Brand Portal, agora é possível:

* [Publicar ativos do AEM Assets no Brand Portal](publish-to-brand-portal.md)
* [Publicar pastas do AEM Assets no Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicar coleções do AEM Assets no Brand Portal](publish-to-brand-portal.md#publish-collections-to-brand-portal)

Além do que foi descrito acima, você também pode publicar esquemas de metadados, predefinições de imagens, aspectos de pesquisa e tags do AEM Assets para o Brand Portal.

* [Publicar predefinições, esquemas e aspectos no Brand Portal](https://docs.adobe.com/content/help/br/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar marcações no Brand Portal](https://docs.adobe.com/content/help/br/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


Consulte a [documentação do Brand Portal](https://docs.adobe.com/content/help/br/experience-manager-brand-portal/using/home.html) para obter mais informações.


## Registros de distribuição {#distribution-logs}

Você pode verificar os registros para obter informações detalhadas sobre as ações executadas pelo agente de distribuição.

Por exemplo, publicamos um ativo do AEM Assets para o Brand Portal para validar a configuração.

1. Follow the steps (from 1 to 4) as shown in the [test connection](#test-configuration) section and navigate to the distribution agent page.

1. Clique em **[!UICONTROL Registros]** para exibir os registros de distribuição. Você pode ver o processamento e os registros de erros aqui.

   ![](assets/test-bpconfig5.png)

O agente de distribuição gera os seguintes registros:

* INFO: esse é um registro gerado pelo sistema acionado na configuração bem-sucedida que habilita o agente de distribuição.
* DSTRQ1 (Solicitação 1): acionado na conexão de teste.

Ao publicar o ativo, os seguintes registros de solicitação e resposta são gerados:

**Solicitação do agente de distribuição**:
* DSTRQ2 (Solicitação 2): a solicitação de publicação de ativo é acionada.
* DSTRQ3 (Solicitação 3): o sistema aciona outra solicitação para publicar a pasta na qual o ativo existe e replicar a pasta no Brand Portal.

**Resposta do agente de distribuição**:
* queue-bpdistributionagent0 (DSTRQ2): o ativo é publicado no Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): o sistema replica a pasta que contém o ativo no Brand Portal.

No exemplo acima, uma solicitação e uma resposta adicionais são acionadas. O sistema não pôde localizar a pasta principal (ou seja, Adicionar caminho) no Brand Portal porque o ativo foi publicado pela primeira vez. Portanto, aciona uma solicitação adicional para criar uma pasta principal com o mesmo nome no Brand Portal onde o ativo é publicado.

>[!NOTE]
>
>A solicitação adicional é gerada caso a pasta principal não exista no Brand Portal (no exemplo acima) ou a pasta principal tenha sido modificada no AEM Assets.



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
