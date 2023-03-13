---
title: Como configurar modelos de dados de formulário prontos para uso do Microsoft Dynamics 365 e Salesforce para formulários adaptáveis?
description: Saiba como integrar o Microsoft Dynamics 365 e Salesforce a formulários adaptáveis.
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# Configurar os serviços em nuvem do [!DNL Microsoft Dynamics 365] e do [!DNL Salesforce] {#configure-azure-storage}

[[!DNL Experience Manager Forms] Integração de dados](data-integration.md) fornece [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] serviços em nuvem para integrar formulários adaptáveis com Modelos de dados de formulário prontos para uso. O Forms adaptável pode interagir com o [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] habilitar fluxos de trabalho de negócios. Por exemplo:

* Gravar dados em [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] no envio do Formulário adaptável.
* Gravar dados em [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] por meio de entidades personalizadas definidas no Modelo de dados de formulário e vice-versa.
* Query [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] servidor para dados e pré-popular o Adaptive Forms.
* Ler dados de [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] servidor.

[!DNL Microsoft Dynamics 365] e [!DNL Salesforce] serviços em nuvem e modelos de dados de formulário estão disponíveis imediatamente no [!DNL AEM Forms] depois que você [configurar um projeto de desenvolvimento para o Forms com base no arquétipo Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft Dynamics 365 e [!DNL Salesforce] Os serviços em nuvem e os Modelos de dados de formulário estarão disponíveis imediatamente se você configurar um [!DNL Experience Manager Forms] as a [!DNL Cloud Service] projeto baseado em [Arquétipo AEM 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) ou posteriormente.

## Configurar [!DNL Salesforce] serviços na nuvem {#configure-salesforce-cloud-service}

Antes de configurar o [!DNL Salesforce] serviços em nuvem, execute as seguintes tarefas:

* [Criar um OAuth habilitado conectado [!DNL Salesforce] aplicativo](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). Ao criar a variável conectada [!DNL Salesforce] especifique o URL de retorno de chamada no seguinte formato:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Onde servidor e porta referem-se ao nome do host e ao número da porta para o [!DNL AEM Forms] servidor.

* Ao criar a conexão [!DNL Salesforce] aplicativo, especificar `full` e `offline_access` como os valores do escopo OAuth.

* Anote os valores da ID do cliente (chamada de Consumer Key) e do segredo do cliente (chamada de Consumer Secret) para o aplicativo conectado.

Execute as seguintes etapas para configurar o [!DNL Salesforce] serviços na nuvem:

1. Ligado [!DNL AEM Forms] instância do autor, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fontes de dados]**. A lista de pastas de wrapper disponíveis inclui uma pasta com o título especificado para `DappTitle`  enquanto [geração do projeto do arquétipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Toque no nome da pasta e selecione **[!UICONTROL Configuração de nuvem do Salesforce]** e toque em **[!UICONTROL Propriedades]**.
1. No **[!UICONTROL Configurações de autenticação]** guia:
   1. Especifique a [!DNL Salesforce] URL do domínio no **[!UICONTROL Host]** campo. Por exemplo, [Nome do domínio].my.salesforce.com.
   1. Especifique a ID do cliente (chamada de Chave do consumidor) e o segredo do cliente (chamada de Segredo do consumidor) para o aplicativo conectado.
   1. Especificar **full offline_access** (`full` e `offine_access` valores separados por um espaço) na variável **[!UICONTROL Escopo da autorização]** campo.
   1. Toque **[!UICONTROL Conectar-se ao OAuth]**. Você será redirecionado para [!DNL Microsoft Dynamics] página de logon.
   1. Faça logon com o [!DNL Salesforce] e aceite para permitir que a configuração do serviço de nuvem se conecte a [!DNL Salesforce] serviço. Se a conexão for bem-sucedida, você será redirecionado para a [!DNL Salesforce] página de configuração do cloud service, que exibe uma mensagem de sucesso.
1. Toque **[!UICONTROL Salvar e fechar]** para concluir a configuração.

### Acesso pronto para uso [!DNL Salesforce] Modelo de dados do formulário

A [!DNL Salesforce] O modelo de dados de formulário está disponível imediatamente na [!DNL AEM Forms] depois que você [configurar um projeto de desenvolvimento para o Forms com base no arquétipo Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Para acessar o modelo de dados do formulário, navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrações de dados]**. A lista de pastas disponíveis inclui uma pasta com o título especificado para `DappTitle`  enquanto [geração do projeto do arquétipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Toque no nome da pasta e selecione o **[!UICONTROL Modelo de dados do Salesforce]** e toque no botão Editar ![Editar](assets/edit.png) ícone para exibir o modelo de dados do formulário.

Após configurar o [[!DNL Salesforce] Serviço de configuração na nuvem](#configure-salesforce-cloud-service), é possível integrar formulários adaptáveis com o pronto para uso [!DNL Salesforce] Modelo de dados.

## Configurar [!DNL Microsoft Dynamics 365] serviços na nuvem {#configure-dynamics-cloud-service}

Antes de configurar o [!DNL Microsoft Dynamics 365] serviços em nuvem, certifique-se de executar as seguintes tarefas:

* [Registrar um aplicativo para [!DNL Microsoft Dynamics 365] com o Azure Ative Diretory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). Ao criar a variável conectada [!DNL Microsoft Dynamics 365] especifique os URLs de resposta no seguinte formato:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Onde servidor e porta referem-se ao nome do host e ao número da porta para o [!DNL AEM Forms] servidor.

* Anote os valores da ID do cliente (também chamada de ID do aplicativo) e o segredo do cliente para o aplicativo conectado.

Execute as seguintes etapas para configurar o [!DNL Microsoft Dynamics 365] serviços na nuvem:

1. Ligado [!DNL AEM Forms] instância do autor, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fontes de dados]**. A lista de pastas de wrapper disponíveis inclui uma pasta com o título especificado para `DappTitle`  enquanto [geração do projeto do arquétipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Toque no nome da pasta e selecione **[!UICONTROL Configuração de nuvem do Microsoft Dynamics 365]** e toque em **[!UICONTROL Propriedades]**.
1. No **[!UICONTROL Configurações de autenticação]** guia:
   1. Insira o valor para o **[!UICONTROL Raiz do serviço]** campo. Acesse a instância do Dynamics e navegue até [Recursos do desenvolvedor](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) para exibir o valor do campo Raiz do Serviço. Por exemplo, `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. Especifique a ID do cliente (referida como ID do aplicativo) e o segredo do cliente para o aplicativo conectado.
   1. Substituir `{tenant}` com uma ID de locatário na **[!UICONTROL URL do OAuth]**, **[!UICONTROL URL do token de atualização]**, e **[!UICONTROL URL do token de acesso]** campos.
   1. Especifique o URL da instância do Dynamics na **[!UICONTROL Recurso]** campo a ser configurado [!UICONTROL Microsoft Dynamics] com um modelo de dados de formulário. Use o URL raiz do serviço para derivar o URL da instância do Dynamics. Por exemplo, `https://<tenant-name>.dynamics.com`.

   1. Especificar `openid` no **[!UICONTROL Escopo da autorização]** campo para processo de autorização em [!DNL Microsoft Dynamics 365].
   1. Faça logon com o [!DNL Microsoft Dynamics 365] e aceite para permitir que a configuração do serviço de nuvem se conecte a [!DNL Microsoft Dynamics 365] serviço. Se a conexão for bem-sucedida, você será redirecionado para a [!DNL Microsoft Dynamics 365] página de configuração do cloud service, que exibe uma mensagem de sucesso.
1. Toque **[!UICONTROL Salvar e fechar]** para concluir a configuração.

### Acesso pronto para uso [!DNL Microsoft Dynamics 365] Modelo de dados do formulário

A [!DNL Microsoft Dynamics 365] O modelo de dados de formulário está disponível imediatamente na [!DNL AEM Forms] depois que você [configurar um projeto de desenvolvimento para o Forms com base no arquétipo Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Para acessar o modelo de dados do formulário, navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrações de dados]**. A lista de pastas disponíveis inclui uma pasta com o título especificado para `DappTitle`  enquanto [geração do projeto do arquétipo AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Toque no nome da pasta e selecione o **[!UICONTROL Modelo de dados do Microsoft Dynamics 365]** e toque no botão Editar ![Editar](assets/edit.png) ícone para exibir o modelo de dados do formulário.

Após configurar o [[!DNL Microsoft Dynamics 365] Serviço de configuração na nuvem](#configure-dynamics-cloud-service), é possível integrar formulários adaptáveis com o pronto para uso [!DNL Microsoft Dynamics 365] Modelo de dados.
