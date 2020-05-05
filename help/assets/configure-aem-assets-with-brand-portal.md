---
title: Configurar o serviço em nuvem do AEM Assets com o Brand Portal
description: Configurar o serviço em nuvem do AEM Assets com o Brand Portal
contentOwner: Vishabh Gupta
translation-type: ht
source-git-commit: bbb3327d4bc7cef8eede3169bc14a1d247ee2bdc

---


# Configurar o AEM Assets com o Brand Portal {#configure-aem-assets-with-brand-portal}

O Adobe Experience Manager (AEM) Assets é configurado com o Brand Portal por meio do Adobe I/O, que obtém um token IMS para autorização do locatário do Brand Portal.

## Pré-requisitos {#prerequisites}

Você precisa do seguinte para configurar o AEM Assets com o Brand Portal:

* Uma instância da nuvem ativa e em execução do AEM Assets.
* URL do locatário do Brand Portal.
* Um usuário com privilégios de administrador do sistema na organização IMS do locatário do Brand Portal.

**Entre em contato com o suporte** para obter mais consultas.

## Criar configuração {#create-new-configuration}

Crie a configuração no Adobe I/O para configurar sua instância da nuvem do AEM Assets com o Brand Portal.

Execute as seguintes etapas na sequência listada:
1. [Obter certificado público](#public-certificate)
1. [Criar integração do Adobe I/O](#createnewintegration)
1. [Criar configuração de conta IMS](#create-ims-account-configuration)
1. [Configurar o serviço em nuvem](#configure-the-cloud-service)
1. [Testar configuração](#test-configuration)

### Criar configuração IMS {#create-ims-configuration}

A configuração IMS autentica seu locatário do Brand Portal com a instância do autor do AEM Assets.

A configuração IMS inclui duas etapas:

* [Obter certificado público](#public-certificate)
* [Criar configuração de conta IMS](#create-ims-account-configuration)

### Obter certificado público {#public-certificate}

O certificado público permite autenticar seu perfil no Adobe I/O.

1. Faça logon na instância da nuvem do AEM Assets.

1. No painel **Ferramentas** da ![ferramenta](assets/tools.png), navegue até **[!UICONTROL Segurança]** >> **[!UICONTROL Configurações do Adobe IMS]**.

   ![Interface do usuário de configuração de conta do Adobe IMS](assets/ims-configuration1.png)

1. A página Configurações do Adobe IMS é aberta.

   Clique em **[!UICONTROL Criar]**.

   Isso o levará à página **[!UICONTROL Configuração técnica de conta do Adobe IMS]**.

1. Por padrão, a guia **Certificado** é aberta.

   Em **Solução da nuvem**, selecione **[!UICONTROL Adobe Brand Portal]**.

1. Marque a caixa de seleção **[!UICONTROL Criar novo certificado]** e especifique um **alias** para o certificado. O alias atua como nome da caixa de diálogo.

1. Clique em **[!UICONTROL Criar certificado]**. Uma caixa de diálogo é exibida. Clique em **[!UICONTROL OK]** para gerar o certificado público.

   ![Criar certificado](assets/ims-config2.png)

1. Clique em **[!UICONTROL Baixar chave pública]** e salve o arquivo de certificado *AEM-Adobe-IMS.crt* no computador. O arquivo de certificado é usado para [criar a integração do Adobe I/O](#createnewintegration).

   ![Baixar certificado](assets/ims-config3.png)

1. Clique em **[!UICONTROL Avançar]**.

   Na guia **Conta**, crie a conta do Adobe IMS, mas para isso você precisará dos detalhes de integração. Mantenha esta página aberta por enquanto.

   Abra uma nova guia e [crie a integração do Adobe I/O](#createnewintegration) para obter os detalhes de integração das configurações de conta do IMS.

### Criar integração do Adobe I/O {#createnewintegration}

A integração do Adobe I/O gera a chave da API, o segredo do cliente e a carga (JWT), que são necessários para configurar as configurações da conta do IMS.

1. Faça logon no Console do Adobe I/O com privilégios de administrador de sistema na organização IMS do locatário do Brand Portal.

   URL padrão: [https://console.adobe.io/](https://console.adobe.io/)

1. Clique em **[!UICONTROL Criar integração]**.

1. Selecione **[!UICONTROL Acessar uma API]** e clique em **[!UICONTROL Continuar]**.

   ![Criar nova integração](assets/create-new-integration1.png)

1. Uma nova página de integração é exibida.

   Selecione sua organização na lista suspensa.

   Em **[!UICONTROL Experience Cloud]**, selecione **[!UICONTROL AEM Brand Portal]** e clique em **[!UICONTROL Continuar]**.

   Se a opção Brand Portal estiver desativada para você, verifique se selecionou a organização correta na caixa suspensa acima da opção **[!UICONTROL Serviços da Adobe]**. Se não souber sua organização, entre em contato com o administrador.

   ![Criar integração](assets/create-new-integration2.png)

1. Especifique um nome e uma descrição para a integração. Clique em **[!UICONTROL Selecionar um arquivo do seu computador]** e faça upload do arquivo `AEM-Adobe-IMS.crt` baixado na seção [obter certificados públicos](#public-certificate).

1. Selecione o perfil da organização.

   Ou selecione o **[!UICONTROL Assets Brand Portal]** e clique em **[!UICONTROL Criar integração]**. A integração é criada.

1. Clique em **[!UICONTROL Continuar para obter detalhes de integração]** para visualizar as informações de integração.

   Copie a **[!UICONTROL chave da API]**

   Clique em **[!UICONTROL Recuperar segredo do cliente]** e copie a chave Segredo do cliente.

   ![Chave da API, segredo do cliente e informações de carga de uma integração](assets/create-new-integration3.png)

1. Navegue até a guia **[!UICONTROL JWT]** e copie a carga **[!UICONTROL JWT]**.

   As informações da chave da API, da chave Segredo do cliente e da carga JWT serão usadas para criar a configuração da conta do IMS.

### Criar configuração de conta IMS {#create-ims-account-configuration}

Verifique se você executou as seguintes etapas:

* [Obter certificado público](#public-certificate)
* [Criar integração do Adobe I/O](#createnewintegration)

**Etapas para criar a configuração da conta IMS:**

1. Abra a página Configuração IMS, guia **[!UICONTROL Contas]**. Você manteve a página aberta no final da seção, [Obter certificado público](#public-certificate).

1. Especifique um **[!UICONTROL Título]** para a conta IMS.

   No **[!UICONTROL Servidor de autorização]**, insira o URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Cole a chave da API, o segredo do cliente e a carga JWT copiados no final da integração [Criar Adobe I/O](#createnewintegration).

   Clique em **[!UICONTROL Criar]**.

   A integração é criada.

   ![Configurar a conta IMS](assets/create-new-integration6.png)


1. Selecione a configuração IMS e clique em **[!UICONTROL Verificar integridade]**. Uma caixa de diálogo é exibida.

   Clique em **[!UICONTROL Verificar]**. Ao se conectar com êxito, a mensagem *Token recuperado com êxito* é exibida.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Você deve ter apenas uma configuração IMS. Não crie várias configurações IMS.
>
>A configuração IMS deve ser aprovada na verificação de integridade. Se a configuração não for aprovada na verificação de integridade, ela será inválida. Você deve excluí-la e criar uma configuração nova e válida.



### Configurar o serviço em nuvem {#configure-the-cloud-service}

Execute as seguintes etapas para criar a configuração do serviço em nuvem do Brand Portal:

1. Faça logon na instância da nuvem do AEM Assets.

1. No painel **Ferramentas** da ![ferramenta](assets/tools.png), navegue até **[!UICONTROL ****Cloud Services > AEM Brand Portal]**.

   A página Configurações do Brand Portal é aberta.

1. Clique em **[!UICONTROL Criar]**.

1. Especifique um **[!UICONTROL Título]** para a configuração.

   Selecione a Configuração IMS criada na etapa e [crie a configuração da conta IMS](#create-ims-account-configuration).

   No **[!UICONTROL URL de serviço]**, insira o URL do locatário do Brand Portal.

   ![](assets/create-cloud-service.png)

1. Clique em **[!UICONTROL Salvar e fechar]**. A configuração da nuvem é criada. A instância da nuvem do AEM Assets agora está configurada com o locatário do Brand Portal.

### Testar configuração{#test-configuration}

1. Faça logon na instância da nuvem do AEM Assets.

1. No painel **Ferramentas** da ![ferramenta](assets/tools.png), navegue até **[!UICONTROL Implantação]** > **[!UICONTROL Distribuição]**.

   ![](assets/test-bpconfig1.png)

1. A página Distribuição é aberta.

   Um agente de distribuição do Brand Portal `bpdistributionagent0` é criado em **[!UICONTROL Publicar no Brand Portal]**.

   Clique em **[!UICONTROL Publicar no Brand Portal]**

   ![](assets/test-bpconfig2.png)

   >[!NOTE]
   >
   >Por padrão, um agente de distribuição é criado para um locatário do Brand Portal.

1. A página do agente de distribuição é aberta. Por padrão, a guia **[!UICONTROL Status]** é aberta e preenche as filas de distribuição.

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

Verifique os registros para obter informações detalhadas sobre as ações executadas no agente de distribuição.

Por exemplo, publicamos um ativo do AEM Assets no Brand Portal para verificar a configuração.

1. Siga as etapas (Etapa 1 - 4) conforme mostrado em **[!UICONTROL Testar conexão]** e navegue até a página do agente de distribuição.

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
