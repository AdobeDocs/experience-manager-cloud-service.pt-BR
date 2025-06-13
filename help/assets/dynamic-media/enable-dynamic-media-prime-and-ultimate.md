---
title: Habilitar [!DNL Dynamic Media] Prime e Ultimate
description: Saiba como habilitar [!DNL Dynamic Media] ofertas do Prime e do Ultimate.
feature: Asset Management
role: User, Admin
exl-id: 0ee161f5-bf44-41f1-928e-c07574fd43cc
source-git-commit: 82a3016149645701abe829ad89c493f480956267
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 2%

---

# Habilitar o [!DNL Dynamic Media] Prime e o Ultimate {#enable-dynamic-media-prime-and-ultimate}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nova</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>integração do AEM Assets com o Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novo</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Extensibilidade da Interface do Usuário</b></a>
        </td>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Práticas recomendadas de pesquisa</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Práticas recomendadas para metadados</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de conteúdo</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media com recursos da OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentação do AEM Assets para desenvolvedores</b></a>
        </td>
    </tr>
</table>

O as a Cloud Service [!DNL Adobe Experience Manager] permite que você acesse as ofertas do Prime e do Ultimate [!DNL Dynamic Media] para simplificar seus fluxos de trabalho digitais e otimizar o gerenciamento de conteúdo. Consulte [Dynamic Media Prime e Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md) para entender seus benefícios e as principais diferenças entre eles.

Este artigo fornece o fluxo de trabalho completo para habilitar as ofertas do Prime e do Ultimate [!DNL Dynamic Media].

## Habilitar o [!DNL Dynamic Media] Ultimate {#enable-dynamic-media-ultimate}

Para habilitar o Ultimate [!DNL Dynamic Media]:

1. [Ativar [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi)
1. [Configurar [!DNL Dynamic Media] soluções](#configure-dynamic-media-solutions)
1. [Criar e listar [!DNL Dynamic Media] empresas](#create-and-list-dynamic-media-companies)
1. [Configurar domínio personalizado na camada de entrega](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the [!DNL AEM] [!DNL Dynamic Media] API card](#onboarding-api-keys)
-->

Se você precisar habilitar [!DNL Dynamic Media Prime], consulte os links rápidos fornecidos em [Habilitar [!DNL Dynamic Media Prime]](#enable-dynamic-media-prime).

### Ativar [!DNL Dynamic Media with OpenAPI] {#activate-dynamic-media-with-openapi}

O [!DNL Dynamic Media] com recursos OpenAPI coloca o DAM no centro de um ecossistema ágil e eficiente de cadeia de fornecimento de conteúdo para garantir a governança e a entrega de ativos.

A primeira etapa do processo de habilitação do Ultimate [!DNL Dynamic Media] é ativar o [[!DNL Dynamic Media] com OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) para o seu ambiente Cloud Service.

#### Prepare-se para começar {#prerequisites}

Certifique-se de atender aos seguintes requisitos antes de iniciar o processo de ativação:

1. [Acesso ao Cloud Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Seu programa inclui [!DNL Dynamic Media] soluções](#configure-dynamic-media-solutions).
1. Você tem [!DNL Dynamic Media] licença do Prime ou Ultimate.

#### Habilitar recursos do [!DNL Dynamic Media with OpenAPI] no seu ambiente do Cloud Service {#enable-dynamic-media-with-openapi-capabilites-in-your-CS-environment}

Execute estas etapas para habilitar o [!DNL Dynamic Media with OpenAPI] para o seu ambiente do Cloud Service:

1. [Navegue até a interface do Cloud Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).

1. [Crie um ambiente](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments), se você não tiver acesso a um ambiente existente.

1. Selecione **[!UICONTROL Clique para ativar]** na linha **[!UICONTROL Dynamic Media]** da seção **[!UICONTROL Informações do ambiente]**, na página Detalhes do ambiente.

   ![ativar mídia dinâmica com recursos OpenAPI](/help/assets/assets/activate-adv-capabiliites-of-dm-openAPI.png)

1. Clique em **[!UICONTROL Ativar]** na caixa de diálogo de confirmação para iniciar o processo de ativação [!DNL Dynamic Media with OpenAPI]. Após a ativação bem-sucedida, o Cloud Manager exibe as seguintes atualizações de status:
   1. **[!UICONTROL Estágio do ambiente]**: **[!UICONTROL Em execução]**
   1. ![DM ativado](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media ]**:**[!UICONTROL  Os recursos OpenAPI estão ativados ]**

      ![ativação bem-sucedida](/help/assets/assets/activation-successful.png){width="700" align="left"}

#### Tentar ativação novamente {#retry-activation}

Se a ativação falhar, o Cloud Manager exibirá as seguintes atualizações de status:

* **[!UICONTROL Estágio do ambiente]**: **[!UICONTROL Falha no DM com OpenAPI]**
* ![DM ativado](/help/assets/assets/Images_icon.svg)**[!UICONTROL Dynamic Media ]**:**[!UICONTROL  Falha ao ativar os recursos OpenAPI ]**

  ![repetir ativação](/help/assets/assets/retry-dm-openapi-failed-activation.png){width="700" align="left"}

Selecione **[!UICONTROL Clique para tentar novamente]** para reiniciar a ativação.

Como alternativa, execute estas etapas para reiniciar o processo de ativação:

1. Navegue até a página que lista todos os ambientes.

1. Clique em mais opções (![mais opções](/help/assets/assets/three-dots.svg)) no final da linha do ambiente.

1. Selecione **[!UICONTROL Repetir DM com OpenAPI Ativation]** para reiniciar a ativação.

   ![repetir ativação da página de detalhes do ambiente](/help/assets/assets/restart-activation-process-from-list-environment-page.png)

### Configurar soluções do [!DNL Dynamic Media] {#configure-dynamic-media-solutions}

Configure as soluções do [!UICONTROL Dynamic Media] para usar os recursos básicos e avançados do [Dynamic Media com OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) em ambientes existentes ou novos disponíveis no Cloud Manager.

#### Prepare-se para começar {#prerequisites-to-configure-dynamic-media-solutions}

Verifique se você tem o seguinte para configurar as soluções do [!UICONTROL Dynamic Media]:

1. [Acesso ao Cloud Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. Você tem [!DNL Dynamic Media] licença Ultimate.

#### Configurar soluções do [!DNL Dynamic Media] para entrega de ativos {#configure-dynamic-media-solutions-for-asset-delivery}

Execute as seguintes etapas:

1. [Crie um novo programa](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-program) ou navegue até um programa existente e clique em **[!UICONTROL Editar]**. A página **[!UICONTROL Configurar para produção]** exibe a guia **[!UICONTROL Soluções e complementos]**.

1. Selecione **[!UICONTROL Assets]**, **[!UICONTROL Assets Prime]**, **[!UICONTROL Assets Ultimate]** ou **[!UICONTROL Sites]** para adicionar a solução **[!UICONTROL Dynamic Media]** ao seu programa.

1. Selecione a solução **[!UICONTROL Dynamic Media]** e clique em **[!UICONTROL Continuar]** para adicionar a solução **[!UICONTROL Dynamic Media]** ao seu programa. Esta ação reinicia todos os ambientes existentes no programa e adiciona a solução [!DNL Dynamic Media] a eles. Além disso, qualquer ambiente novo que você criar em seu programa automaticamente obterá [!DNL Dynamic Media].

   ![configurar para produção](/help/assets/assets/set-up-for-prod.png){width="500" align="left"}

Consulte [Ativar [!DNL Dynamic Media with OpenAPI]](#activate-dynamic-media-with-openapi) para começar a usar os recursos do [!DNL Dynamic Media] com os recursos OpenAPI em seu ambiente.

### Criar e listar [!DNL Dynamic Media] empresas {#create-and-list-dynamic-media-companies}

Crie e liste empresas do [!DNL Dynamic Media] em seu ambiente do AEM Cloud Service para gerenciar configurações em seu ambiente do AEM.

#### Prepare-se para começar {#prerequisites-to-create-and-list-dynamic-media-companies}

Para ver as empresas (contas) existentes ou adicionar uma nova empresa (conta) do [!DNL Dynamic Media] na sua organização IMS, você deve ter:

1. [Acesso ao Cloud Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).

1. Você tem [!DNL Dynamic Media] licença Ultimate.

#### Criar e listar [!DNL Dynamic Media] empresas em sua organização IMS {#create-and-list-dynamic-media-companies-in-your-ims-organisation}

Execute estas etapas para criar e listar uma nova empresa (conta) do [!DNL Dynamic Media] que possa ser configurada em seu ambiente [!DNL AEM]:

1. Navegue até a [página de licença do Cloud Manager](https://experience-stage.adobe.com/#/@ssahnichstage/cloud-manager/license).

1. Clique em **[!UICONTROL Adicionar Empresa]**, a caixa de diálogo **[!UICONTROL Criar Empresa do Dynamic Media]** será exibida.

1. Especifique um nome de empresa [!DNL Dynamic Media] exclusivo, selecione uma região de empresa e adicione uma lista de IDs de email de administrador de empresa separadas por vírgulas.

   ![Criar empresa do Dynamic Media](/help/assets/assets/create-dynamic-media-company.png){width="500" align="left"}

1. Clique em **[!UICONTROL Criar]** para começar a criar sua empresa. Esta ação adiciona uma nova linha à seção **[!UICONTROL [!DNL Dynamic Media]empresas]** e exibe **[!UICONTROL Configurando]** como o **[!UICONTROL STATUS]** da empresa.

   ![criação da empresa Dynamic Media iniciada](/help/assets/assets/dm-company-creation-initiated.png)

1. **Opcional:** Clique em ![ícone de informações](/help/assets/assets/info-icon-solid-black.svg) para ver os detalhes da empresa. O **[!UICONTROL STATUS]** atualiza para **[!UICONTROL Pronto]**, quando a empresa é criada.

   ![Informações sobre a empresa Dynamic Media](/help/assets/assets/dm-company-information.png)

1. Como Administrador do Dynamic Media, verifique se há um email de boas-vindas na sua caixa de correio que inclua uma lista de etapas para a empresa [configurar [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#architecture-diagram-of-dynamic-media) no seu ambiente do Cloud Service [!DNL AEM] para começar.

   ![email de boas-vindas](/help/assets/assets/welcome-email.png)

#### Tentar novamente a criação da empresa {#retry-company-creation}

Se a criação da empresa [!DNL Dynamic Media] falhar, execute as seguintes etapas com base no status da falha:

1. Se o **[!UICONTROL Status]** estiver Pendente, levante o problema para a equipe de suporte ao cliente para resolução.


   ![status pendente](/help/assets/assets/company-creation-pending-status.png){width="350" align="center"}



1. Se o **[!UICONTROL Status]** falhar, tente novamente com base no motivo da falha.

   ![status de falha](/help/assets/assets/company-creation-failure-status.png){width="380" align="center"}

### Opcional: configurar o domínio personalizado no nível de entrega {#configure-custom-domain-in-delivery-tier}

Embora o AEM as a Cloud Service venha com um domínio padrão, você pode personalizá-lo de acordo com suas necessidades. Anexe um domínio personalizado à camada de entrega usando o Cloud Manager.

#### Prepare-se para começar {#prerequisites-to-configure-custom-domain-in-delivery-tier}

Certifique-se de atender aos seguintes requisitos antes de iniciar o processo de configuração:

1. [Acesso ao Cloud Manager](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Já ativado [!DNL Dynamic Media with OpenAPI] em seu ambiente](#activate-dynamic-media-with-openapi).
1. Habilitado [!DNL Dynamic Media with OpenAPI] no estado pronto.
1. Certificado do tipo EV ou OV para o domínio a ser usado para a camada de entrega. Consulte [Introdução a certificados SSL](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates) para obter mais detalhes.

#### Configurar domínio personalizado na camada de entrega usando o Cloud Manager {#configure-custom-domain-in-delivery-tier-using-cloud-manager}

Execute as seguintes etapas no Cloud Manager para configurar um domínio personalizado no nível de entrega:

1. [Adicione um certificado SSL gerenciado pelo cliente](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate#add-customer-managed-ssl-cert).

1. [Adicione um nome de domínio personalizado](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name#adding-cdn-settings).

1. Navegue até a página de detalhes do ambiente e [adicione uma configuração de CDN](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/domain-mappings/add-domain-mapping). Ao adicionar a configuração, selecione **[!UICONTROL Delivery]** no campo **[!UICONTROL Tier]** na caixa de diálogo **[!UICONTROL Configurar CDN]**.

   ![Configurar CDN](/help/assets/assets/select-delivery-tier-in-configure-cdn-form.png)

   Depois de adicionar as configurações, o **[!UICONTROL STATUS]** de **[!UICONTROL Configurações de CDN]** atualiza para **[!UICONTROL Aplicado]**.

   ![Configurar o status de implantação da CDN](/help/assets/assets/cdn-configuration-deployment-status.png)

1. Clique em mais opções (![mais opções](/help/assets/assets/three-dots.svg)) e selecione **[!UICONTROL Ativar preparação]** para exibir a caixa de diálogo **[!UICONTROL Ativar preparação]**.

   ![opção de preparação para ativação](/help/assets/assets/go-live-readiness-option.png)

1. Execute as etapas **[!UICONTROL Configurar CNAME]** para mapear `cdn.adobeaemcloud.com` (registro CNAME) no registro DNS do provedor de serviços DNS. Esse mapeamento garante que as solicitações recebidas no domínio personalizado sejam redirecionadas para o CDN da Adobe.

   ![caixa de diálogo de preparação para ativação](/help/assets/assets/go-live-readiness-dialogbox.png){width="500" align="left"}

1. Clique em **[!UICONTROL Ok]**, o **[!UICONTROL STATUS]** atualiza para **[!UICONTROL Verificado]**. O domínio personalizado está pronto para uso no URL de entrega.


   ![Configurar CDN](/help/assets/assets/cdn-configurations-varified.png)



<!--
### Onboard API keys {#onboarding-api-keys}

Create an API key to access [!DNL Dynamic Media] with OpenAPIs and the delivery tier backed Asset Selector.

#### Prepare yourself for API keys onboarding process {#prerequisites-for-onboarding-api-keys} 

To start the API keys onboarding process, ensure you have:

1. [Access to Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager).
1. [Activated [!DNL Dynamic Media with OpenAPI] in your environment](#activate-dynamic-media-with-openapi).
1. [Access to the Adobe Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis#create-adobe-developer-console-adc-project).

#### Onboard the API keys using [!DNL AEM Dynamic Media] API card {#onboarding-api-keys-using-aem-dynamic-media-api-card}

Use the [Adobe Developer Console](https://developer.adobe.com/developer-console/) to onboard the API keys to:

1. [Access Dynamic Media APIs](#access-dynamic-media-apis)
1. [Access Delivery tier backed Asset Selector](#access-delivery-tier-backed-asset-selector)

#### Create an API key to access [!DNL Dynamic Media] with OpenAPIs {#access-dynamic-media-apis}

Execute the following steps to create an API key to access [!DNL Dynamic Media] with OpenAPIs:

1. Navigate to the **[!UICONTROL Admin Console]**. The Admin Console displays the **[!UICONTROL author]**, **[!UICONTROL delivery]** and **[!UICONTROL publish]** instances.
![instances on admin console](/help/assets/assets/delivery-instance-admin-console.png)
1. Select the **[!UICONTROL delivery]** instance to display the product profile with **[!UICONTROL AEM Dynamic Media enable API Services]** enabled by default. The product profile looks like this: **[!UICONTROL AEM Assets DM OpenAPI Users - delivery  - Program [ID Number] - Environment [ID Number]]**. 

   ![product profile on admin console](/help/assets/assets/admin-console-product-profile.png)

   >[!NOTE]
   >
   >This delivery instance is common for [!DNL Content Hub] and [!DNL Dynamic Media] with OpenAPI capabilities.

1. Navigate to the [Adobe Developer console](https://developer.adobe.com/console) and [create a new project](https://developer.adobe.com/dep/guides/dev-console/create-project/). See [Invoke OpenAPI-based AEM APIs for server to server authentication](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/aem-apis/invoke-openapi-based-aem-apis) to learn about creating a new project.
1. Select **[!UICONTROL AEM Dynamic Media API]** to access to the [!DNL Dynamic Media with OpenAPI capabilities] and click **[!UICONTROL Next]**.
![adobe developer console](/help/assets/assets/adobe-developer-console.png)
1. Select **[!UICONTROL Server-to-Server Authentication]** and click **[!UICONTROL Next]**. See [Server to Server authentication](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) to learn more about this authentication type.
![server-to-server-authentication](/help/assets/assets/server-to-server-authentication.png)
1. Select **[!UICONTROL OAuth Server-to-Server]**, specify a unique **[!UICONTROL Credential name]** and click **[!UICONTROL Next]**.
![oauth server to server credential](/help/assets/assets/oauth-server-server-and-credential-name.png)
1. Select your product profile (mentioned in step 2) to access the APIs using the environment's delivery endpoint and click **[!UICONTROL Save configured API]**.
![select product profile](/help/assets/assets/select-product-profile.png)
1. Select **[!UICONTROL AEM Dynamic Media API]**. Use the **[!UICONTROL OAuth Server-to-Server]** to fetch the **X-API-key** and access the token for the **authorization** header. 
![oauth server to server](/help/assets/assets/oauth-server-to-server-credentials.png)
Execute the below steps to use [Dynamic Media with OpenAPIs](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/) using the **[!UICONTROL OAuth Server-to-Server]** credentials. 
    1. Copy the **[!UICONTROL API KEY (Client ID)]** and replace the `X-Api-Key` in the cURL.
    1. Click **[!UICONTROL Generate access token]** to generate an access token and replace `YOUR_JWT_HERE` with the token in the cURL.

The cURL looks like this:
```
headers: {
    'Content-Type': 'application/json',
      'X-Adobe-Accept-Experimental': '1',
      Authorization: 'Bearer <YOUR_JWT_HERE>',
      'X-Api-Key': 'YOUR_API_KEY_HERE'
    `},
```
See [Search Assets API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/search-assets-api#search-assets-api-header) for more information.

### Access Delivery tier backed Asset Selector {#access-delivery-tier-backed-asset-selector}

TBD: Wiki in progress..
-->

## Habilitar o [!DNL Dynamic Media] Prime {#enable-dynamic-media-prime}

Para habilitar o Prime [!DNL Dynamic Media]:

1. [Ativar Dynamic Media com OpenAPI](#activate-dynamic-media-with-openapi)
1. [Opcional: configurar o domínio personalizado na camada de entrega](#configure-custom-domain-in-delivery-tier)

<!--
1. [Onboard API keys using the AEM Dynamic Media API card](#onboarding-api-keys)
-->
