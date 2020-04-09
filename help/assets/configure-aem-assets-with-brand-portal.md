---
title: Configurar o serviço em nuvem do AEM Assets com o Brand Portal
description: Configure o serviço em nuvem do AEM Assets com o Brand Portal.
contentOwner: Vishabh Gupta
translation-type: tm+mt
source-git-commit: 9d37fdae4445d0ccbdd6f800fc3ad4cbeec971fe

---


# Configurar ativos AEM com o Portal de marcas {#configure-aem-assets-with-brand-portal}

Os ativos Adobe Experience Manager (AEM) são configurados com o Brand Portal por meio da E/S da Adobe, que obtém um token IMS para autorização do locatário do Brand Portal.

## Pré-requisitos {#prerequisites}

Você precisa do seguinte para configurar os ativos AEM com o Portal de marcas:

* Uma instância da nuvem ativa e em execução do AEM Assets.
* URL do locatário do Portal de Marcas.
* Um usuário com privilégios de administrador do sistema na organização IMS do locatário do Brand Portal.

**Entre em contato com o suporte** para obter mais query.

## Create configuration {#create-new-configuration}

Você pode criar uma nova configuração em E/S da Adobe para configurar sua instância da nuvem do AEM Assets com o Brand Portal.

Execute as seguintes etapas na sequência listada:
1. [Obter certificado público](#public-certificate)
1. [Criar integração de E/S da Adobe](#createnewintegration)
1. [Criar configuração de conta IMS](#create-ims-account-configuration)
1. [Configurar serviço em nuvem](#configure-the-cloud-service)
1. [Testar configuração](#test-configuration)

### Criar configuração IMS {#create-ims-configuration}

A configuração do IMS autentica seu locatário do Brand Portal com a instância do autor AEM Assets.

A configuração de IMS inclui duas etapas:

* [Obter certificado público](#public-certificate)
* [Criar configuração de conta IMS](#create-ims-account-configuration)

### Obter certificado público {#public-certificate}

O certificado público permite autenticar seu perfil em E/S da Adobe.

1. Faça logon na instância da nuvem do AEM Assets

1. No painel **Ferramentas** ![Ferramentas](assets/tools.png) , navegue até **[!UICONTROL Segurança]** > Configurações **[!UICONTROL do]** Adobe IMS.

   ![Interface do usuário de configuração de conta do Adobe IMS](assets/ims-configuration1.png)

1. A página Configurações do Adobe IMS é aberta.

   Clique em **[!UICONTROL Criar]**.

   Isso o levará à página Configuração **[!UICONTROL técnica da conta]** Adobe IMS.

1. Por padrão, a guia **Certificado** é aberta.

   Na **Cloud Solution**, selecione **[!UICONTROL Adobe Brand Portal]**.

1. Marcar a caixa de seleção **[!UICONTROL Criar novo certificado]** e especificar um **alias** para o certificado. O alias serve como nome da caixa de diálogo.

1. Clique em **[!UICONTROL Criar certificado]**. Uma caixa de diálogo é exibida. Clique em **[!UICONTROL OK]** para gerar o certificado público.

   ![Criar certificado](assets/ims-config2.png)

1. Clique em **[!UICONTROL Baixar chave]** pública e salve o arquivo de certificado *AEM-Adobe-IMS.crt* em seu computador. O arquivo de certificado é usado para [criar a integração](#createnewintegration)de E/S da Adobe.

   ![Fazer download do certificado](assets/ims-config3.png)

1. Clique em **[!UICONTROL Avançar]**.

   Na guia **Conta** , você cria a conta Adobe IMS, mas para isso você precisará dos detalhes de integração. Mantenha esta página aberta por enquanto.

   Abra uma nova guia e [crie a integração](#createnewintegration) de E/S da Adobe para obter os detalhes de integração das configurações da conta IMS.

### Criar integração de E/S da Adobe {#createnewintegration}

A integração de E/S da Adobe gera a chave da API, o segredo do cliente e a carga (JWT), que são necessários para configurar as configurações da conta IMS.

1. Faça logon no Console de E/S da Adobe com privilégios de administrador de sistema na organização IMS do locatário do Portal de Marcas.

   URL padrão: [https://console.adobe.io/](https://console.adobe.io/)

1. Clique em **[!UICONTROL Criar integração]**.

1. Selecione **[!UICONTROL Acessar uma API]** e clique em **[!UICONTROL Continuar]**.

   ![Criar nova integração](assets/create-new-integration1.png)

1. Será aberta uma nova página de integração.

   Selecione sua organização na lista suspensa.

   Na **[!UICONTROL Experience Cloud]**, selecione **[!UICONTROL AEM Brand Portal]** e clique em **[!UICONTROL Continuar]**.

   Se a opção Brand Portal estiver desativada para você, verifique se você selecionou a organização correta na caixa suspensa acima da opção Serviços **[!UICONTROL da]** Adobe. Se você não souber sua organização, entre em contato com o administrador.

   ![Criar integração](assets/create-new-integration2.png)

1. Especifique um nome e uma descrição para a integração. Clique em **[!UICONTROL Selecionar um arquivo do seu computador]** e faça upload do `AEM-Adobe-IMS.crt` arquivo baixado na seção [obter certificados](#public-certificate) públicos.

1. Selecione o perfil de sua organização.

   Ou selecione o Portal **[!UICONTROL de marcas dos]** ativos de perfil padrão e clique em **[!UICONTROL Criar integração]**. A integração é criada.

1. Clique em **[!UICONTROL Continuar para obter detalhes]** de integração para visualização das informações de integração.

   Copiar a chave **[!UICONTROL da API]**

   Clique em **[!UICONTROL Recuperar segredo]** do cliente e copie a chave Segredo do cliente.

   ![Chave da API, segredo do cliente e informações de carga de uma integração](assets/create-new-integration3.png)

1. Navegue até a guia **[!UICONTROL JWT]** e copie a carga **[!UICONTROL JWT]**.

   As informações da chave da API, da chave Segredo do cliente e da carga JWT serão usadas para criar a configuração da conta IMS.

### Criar configuração de conta IMS {#create-ims-account-configuration}

Verifique se você executou as seguintes etapas:

* [Obter certificado público](#public-certificate)
* [Criar integração de E/S da Adobe](#createnewintegration)

**Etapas para criar a configuração da conta IMS:**

1. Abra a página Configuração IMS, guia **[!UICONTROL Contas]** . Você manteve a página aberta no final da seção, [Obter certificado](#public-certificate)público.

1. Especifique um **[!UICONTROL Título]** para a conta IMS.

   No Servidor **[!UICONTROL de Autorização]**, insira o URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Cole a chave da API, o segredo do cliente e a carga JWT que você copiou no final da integração [](#createnewintegration)Criar E/S da Adobe.

   Clique em **[!UICONTROL Criar]**.

   A integração é criada.

   ![Configuração da conta IMS](assets/create-new-integration6.png)


1. Selecione a configuração IMS e clique em **[!UICONTROL Verificar integridade]**. Uma caixa de diálogo é exibida.

   Clique em **[!UICONTROL Verificar]**. Na conexão bem-sucedida, a mensagem *Token recuperado com êxito* é exibida.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Crie apenas uma configuração IMS válida. Não crie várias configurações IMS.
>
> Certifique-se de que a configuração esteja saudável. Caso a configuração não esteja funcionando, exclua-a e crie uma configuração nova e saudável.


### Configurar serviço em nuvem {#configure-the-cloud-service}

Execute as seguintes etapas para criar a configuração do serviço em nuvem do Brand Portal:

1. Faça logon na instância da nuvem do AEM Assets

1. No painel **Ferramentas** ![Ferramentas](assets/tools.png) , navegue até Serviços **[!UICONTROL em nuvem > Portal]** da marca AEM.

   A página Configurações do Portal de Marcas é aberta.

1. Clique em **[!UICONTROL Criar]**.

1. Especifique um **[!UICONTROL Título]** para a configuração.

   Selecione a Configuração IMS que você criou na etapa e [crie a configuração](#create-ims-account-configuration)da conta IMS.

   No URL **[!UICONTROL do]** serviço, insira o URL do locatário do Brand Portal.

   ![](assets/create-cloud-service.png)

1. Click **[!UICONTROL Save and Close]**. A configuração da nuvem é criada. A instância da nuvem do AEM Assets agora está configurada com o locatário do Brand Portal.

### Test configuration {#test-configuration}

1. Faça logon na instância da nuvem do AEM Assets.

1. No painel **Ferramentas** ![Ferramentas](assets/tools.png) , navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Distribuição]**.

   ![](assets/test-bpconfig1.png)

1. A página Distribuição é aberta.

   Um agente de distribuição do Brand Portal `bpdistributionagent0` é criado em **[!UICONTROL Publicar no Brand Portal]**.

   Click **[!UICONTROL Publish to Brand Portal]**.

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >Por padrão, um agente de distribuição é criado para um locatário do Brand Portal.

1. A página do agente de distribuição é aberta. Por padrão, a guia **[!UICONTROL Status]** é aberta e preenche as filas de distribuição.

   Um agente de distribuição contém duas filas:
   * Uma fila de processamento para distribuição de ativos ao Brand Portal.
   * Uma fila de erros para os ativos em que a distribuição falhou.
   ![](assets/test-bpconfig3.png)

1. Para verificar a conexão entre os ativos AEM e o Portal de marcas, clique em **[!UICONTROL Testar conexão]**.

   ![](assets/test-bpconfig4.png)

   Uma mensagem é exibida na parte inferior da página informando que o pacote de teste foi entregue com êxito.

   >[!NOTE]
   >
   >Evite desativar o agente de distribuição, pois isso pode causar falha na distribuição dos ativos (em execução na fila).


Depois que o Brand Portal for configurado com êxito com sua instância de nuvem do AEM Assets, você poderá:

* [Publicar ativos do AEM Assets no Brand Portal](publish-to-brand-portal.md)
* [Publicar pastas do AEM Assets no Brand Portal](publish-to-brand-portal.md#publish-folders-to-brand-portal)
* [Publicar coleções dos ativos AEM no Portal de marcas](publish-to-brand-portal.md#publish-collections-to-brand-portal)

Além do acima, você também pode publicar schemas de metadados, predefinições de imagens, aspectos de pesquisa e tags de AEM Assets para o Brand Portal.

* [Publicar predefinições, schemas e aspectos no Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html)
* [Publicar marcações no Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html)


Consulte a documentação [do](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) Brand Portal para obter mais informações.


## Logs de distribuição {#distribution-logs}

Você pode verificar os registros para obter informações detalhadas sobre as ações executadas no agente de distribuição.

Por exemplo, publicamos um ativo do AEM Assets para o Brand Portal para verificar a configuração.

1. Siga as etapas (Etapa 1 a 4) conforme mostrado em **[!UICONTROL Testar conexão]** e navegue até a página do agente de distribuição.

1. Clique em **[!UICONTROL Logs]** para visualização nos registros de distribuição. Você pode ver o processamento e os registros de erros aqui.

   ![](assets/test-bpconfig5.png)

O agente de distribuição gera os seguintes registros:

* INFORMAÇÕES: Este é um log gerado pelo sistema acionado na configuração bem-sucedida que habilita o agente de distribuição.
* DSTRQ1 (Solicitação 1): Disparado na conexão de teste.

Ao publicar o ativo, os seguintes registros de solicitação e resposta são gerados:

**Solicitação** do agente de distribuição:
* DSTRQ2 (Solicitação 2): A solicitação de publicação de ativos é acionada.
* DSTRQ3 (Solicitação 3): O sistema aciona outra solicitação para publicar a pasta na qual o ativo existe e replicar a pasta no Brand Portal.

**Resposta** do agente de distribuição:
* queue-bpdistributionagent0 (DSTRQ2): O ativo é publicado no Brand Portal.
* queue-bpdistributionagent0 (DSTRQ3): O sistema replica a pasta que contém o ativo no Brand Portal.

No exemplo acima, uma solicitação e uma resposta adicionais são acionadas. O sistema não pôde localizar a pasta pai (ou seja, Adicionar caminho) no Brand Portal porque o ativo foi publicado pela primeira vez, portanto, aciona uma solicitação adicional para criar uma pasta pai com o mesmo nome no Brand Portal onde o ativo é publicado.

>[!NOTE]
>>Solicitação adicional é gerada caso a pasta pai não exista no Brand Portal (no exemplo acima) ou a pasta pai tenha sido modificada nos ativos AEM.
>

## Informações adicionais {#additional-information}

Vá para `/system/console/slingmetrics` para obter estatísticas relacionadas ao conteúdo distribuído:

1. **Métricas de contador**
   * sling: `mac_sync_request_failure`
   * sling: `mac_sync_request_received`
   * sling: `mac_sync_request_success`

1. **Métricas de tempo**
   * sling: `mac_sync_distribution_duration`
   * sling: `mac_sync_enqueue_package_duration`
   * sling: `mac_sync_setup_request_duration`



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
