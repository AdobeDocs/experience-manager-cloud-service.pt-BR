---
title: Como configurar o Microsoft Dynamics 365 e o Salesforce para modelos de dados de formulário prontos para uso para formulários adaptáveis?
description: Saiba como integrar o Microsoft Dynamics 365 e o Salesforce a formulários adaptáveis.
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---

# Configurar [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] serviços em nuvem {#configure-azure-storage}

[[!DNL Experience Manager Forms] Integração de dados](data-integration.md) forneça [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] serviços em nuvem para integrar formulários adaptáveis aos Modelos de dados de formulário prontos para uso. O Adaptive Forms pode então interagir com [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] servidores para ativar workflows de negócios. Por exemplo:

* Gravar dados em [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] no envio do formulário adaptável.
* Gravar dados em [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] por meio de entidades personalizadas definidas no Modelo de dados de formulário e vice-versa.
* Query [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] para dados e pré-preencher o Adaptive Forms.
* Ler dados de [!DNL Microsoft Dynamics 365] e [!DNL Salesforce] servidor.

[!DNL Microsoft Dynamics 365] e [!DNL Salesforce] os serviços em nuvem e os Modelos de dados de formulário estão disponíveis prontamente no [!DNL AEM Forms] servidor após [configurar um projeto de desenvolvimento para o Forms com base no arquétipo do Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Microsoft Dynamics 365 e [!DNL Salesforce] os serviços em nuvem e os Modelos de dados de formulário estão disponíveis para uso imediato somente se você configurar um [!DNL Experience Manager Forms] como [!DNL Cloud Service] projeto baseado em [Arquétipo de AEM 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) ou posterior.

## Configurar [!DNL Salesforce] serviço na nuvem {#configure-salesforce-cloud-service}

Antes de configurar o [!DNL Salesforce] serviços em nuvem, certifique-se de executar as seguintes tarefas:

* [Criar um OAuth conectado habilitado [!DNL Salesforce] aplicativo](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5). Ao criar o [!DNL Salesforce] , especifique o URL de retorno de chamada no seguinte formato:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Onde o servidor e a porta se referem ao nome do host e ao número da porta para o [!DNL AEM Forms] servidor.

* Ao criar o [!DNL Salesforce] aplicativo, especifique `full` e `offline_access` como os valores para o escopo OAuth.

* Anote os valores para a ID do cliente (chamada de Chave do consumidor) e o segredo do cliente (referido como Segredo do consumidor) para o aplicativo conectado.

Execute as etapas a seguir para configurar o [!DNL Salesforce] serviço em nuvem:

1. Ligado [!DNL AEM Forms] instância do autor, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fontes de dados]**. A lista de pastas disponíveis do wrapper inclui uma pasta com o título especificado para `DappTitle`  while [geração do projeto de arquétipo de AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Toque no nome da pasta e selecione **[!UICONTROL Configuração da nuvem do Salesforce]** e toque em **[!UICONTROL Propriedades]**.
1. No **[!UICONTROL Configurações de autenticação]** guia :
   1. Especifique a [!DNL Salesforce] URL de domínio na **[!UICONTROL Host]** campo. Por exemplo, [Nome do domínio].my.salesforce.com.
   1. Especifique a ID do cliente (referida como Chave do consumidor) e o segredo do cliente (referido como Segredo do consumidor) para o aplicativo conectado.
   1. Especificar **acesso offline total** (`full` e `offine_access` valores separados por um espaço) na variável **[!UICONTROL Escopo da Autorização]** campo.
   1. Toque **[!UICONTROL Conectar-se ao OAuth]**. Você é redirecionado para [!DNL Microsoft Dynamics] página de logon.
   1. Faça logon com seu [!DNL Salesforce] credenciais e aceitar permitir que a configuração do serviço de nuvem se conecte [!DNL Salesforce] serviço. Se a conexão for bem-sucedida, você será redirecionado para a função [!DNL Salesforce] página de configuração do serviço em nuvem, que exibe uma mensagem de sucesso.
1. Toque **[!UICONTROL Salvar e fechar]** para concluir a configuração.

### Acesso pronto para uso [!DNL Salesforce] Modelo de dados do formulário

A [!DNL Salesforce] O Modelo de dados de formulário está disponível imediatamente no [!DNL AEM Forms] servidor após [configurar um projeto de desenvolvimento para o Forms com base no arquétipo do Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Para acessar o Modelo de dados do formulário, navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrações de dados]**. A lista de pastas disponíveis inclui uma pasta com o título especificado para `DappTitle`  while [geração do projeto de arquétipo de AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Toque no nome da pasta e selecione o **[!UICONTROL Modelo de dados do Salesforce]** e toque em Editar ![Editar](assets/edit.png) ícone para exibir o modelo de dados do formulário.

Após configurar o [[!DNL Salesforce] Serviço de configuração na nuvem](#configure-salesforce-cloud-service), é possível integrar formulários adaptáveis imediatamente [!DNL Salesforce] Modelo de dados.

## Configurar [!DNL Microsoft Dynamics 365] serviço na nuvem {#configure-dynamics-cloud-service}

Antes de configurar o [!DNL Microsoft Dynamics 365] serviço em nuvem, certifique-se de executar as seguintes tarefas:

* [Registre um aplicativo para [!DNL Microsoft Dynamics 365] com o Azure Ative Diretory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). Ao criar o [!DNL Microsoft Dynamics 365] , especifique os URLs de resposta no seguinte formato:

   ```
   https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
   ```

   Onde o servidor e a porta se referem ao nome do host e ao número da porta para o [!DNL AEM Forms] servidor.

* Anote os valores para a ID do cliente (também chamada de ID do aplicativo) e o segredo do cliente para o aplicativo conectado.

Execute as etapas a seguir para configurar o [!DNL Microsoft Dynamics 365] serviço em nuvem:

1. Ligado [!DNL AEM Forms] instância do autor, navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Fontes de dados]**. A lista de pastas disponíveis do wrapper inclui uma pasta com o título especificado para `DappTitle`  while [geração do projeto de arquétipo de AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment).
1. Toque no nome da pasta e selecione **[!UICONTROL Configuração da nuvem do Microsoft Dynamics 365]** e toque em **[!UICONTROL Propriedades]**.
1. No **[!UICONTROL Configurações de autenticação]** guia :
   1. Insira o valor da variável **[!UICONTROL Raiz do serviço]** campo. Vá para a instância do Dynamics e navegue até [Recursos do desenvolvedor](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) para exibir o valor do campo Service Root . Por exemplo, `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. Especifique a ID do cliente (referida como ID do aplicativo) e o segredo do cliente para o aplicativo conectado.
   1. Substituir `{tenant}` com uma ID de locatário no **[!UICONTROL URL de OAuth]**, **[!UICONTROL Atualizar URL do token]** e **[!UICONTROL URL do token de acesso]** campos.
   1. Especifique o URL da instância dinâmica no **[!UICONTROL Recurso]** campo para configurar [!UICONTROL Microsoft Dynamics] com um Modelo de dados de formulário. Use o URL raiz do serviço para derivar o URL da instância do Dynamics. Por exemplo, `https://<tenant-name>.dynamics.com`.

   1. Especificar `openid` no **[!UICONTROL Escopo da Autorização]** campo para o processo de autorização em [!DNL Microsoft Dynamics 365].
   1. Faça logon com seu [!DNL Microsoft Dynamics 365] credenciais e aceitar permitir que a configuração do serviço de nuvem se conecte [!DNL Microsoft Dynamics 365] serviço. Se a conexão for bem-sucedida, você será redirecionado para a função [!DNL Microsoft Dynamics 365] página de configuração do serviço em nuvem, que exibe uma mensagem de sucesso.
1. Toque **[!UICONTROL Salvar e fechar]** para concluir a configuração.

### Acesso pronto para uso [!DNL Microsoft Dynamics 365] Modelo de dados do formulário

A [!DNL Microsoft Dynamics 365] O Modelo de dados de formulário está disponível imediatamente no [!DNL AEM Forms] servidor após [configurar um projeto de desenvolvimento para o Forms com base no arquétipo do Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Para acessar o Modelo de dados do formulário, navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrações de dados]**. A lista de pastas disponíveis inclui uma pasta com o título especificado para `DappTitle`  while [geração do projeto de arquétipo de AEM](setup-local-development-environment.md##forms-cloud-service-local-development-environment). Toque no nome da pasta e selecione o **[!UICONTROL Modelo de dados do Microsoft Dynamics 365]** e toque em Editar ![Editar](assets/edit.png) ícone para exibir o modelo de dados do formulário.

Após configurar o [[!DNL Microsoft Dynamics 365] Serviço de configuração na nuvem](#configure-dynamics-cloud-service), é possível integrar formulários adaptáveis imediatamente [!DNL Microsoft Dynamics 365] Modelo de dados.
