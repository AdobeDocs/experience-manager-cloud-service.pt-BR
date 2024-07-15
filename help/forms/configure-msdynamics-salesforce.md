---
title: Como configurar modelos de dados de formulário prontos para uso do Microsoft Dynamics 365 e Salesforce para o Adaptive Forms?
description: Saiba como integrar o Microsoft Dynamics 365 e o Salesforce ao Adaptive Forms.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 2a43b2db-2dfb-4c79-88be-ea770b44dac1
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# Configurar o Microsoft® Dynamics 365 ou Salesforce para AEM Forms {#configure-azure-storage}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM as a Cloud Service | Este artigo |

A [[!DNL Experience Manager Forms] Integração de Dados](data-integration.md) fornece serviços de nuvem do [!DNL Microsoft® Dynamics 365] e do [!DNL Salesforce] para integrar formulários adaptáveis com o Modelo de Dados de Formulário (FDM) pronto para uso. O Forms adaptável pode interagir com os servidores [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] para habilitar fluxos de trabalho comerciais. Por exemplo:

* Gravar dados em [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] no envio do Formulário Adaptável.
* Grave dados em [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] por meio de entidades personalizadas definidas no Modelo de Dados de Formulário (FDM) e vice-versa.
* Consultar o servidor [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] para obter dados e popular previamente o Forms Adaptável.
* Ler dados do servidor [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce].

Os serviços de nuvem [!DNL Microsoft® Dynamics 365] e [!DNL Salesforce] e o Modelo de Dados de Formulário (FDM) estão disponíveis imediatamente no Servidor [!DNL AEM Forms] depois que você [configurar um projeto de desenvolvimento para o Forms com base no arquétipo de Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>O Microsoft® Dynamics 365 e o [!DNL Salesforce] Cloud Services e o Form Data Model (FDM) estarão disponíveis imediatamente se você configurar um [!DNL Experience Manager Forms] como um projeto [!DNL Cloud Service] com base no [Arquétipo AEM 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) ou posterior.

## Configurar o serviço de nuvem [!DNL Salesforce] {#configure-salesforce-cloud-service}

Antes de configurar os serviços de nuvem do [!DNL Salesforce], execute as seguintes tarefas:

* [Criar um  [!DNL Salesforce] aplicativo](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&amp;type=5) habilitado para OAuth conectado. Ao criar o aplicativo conectado [!DNL Salesforce], especifique a URL de retorno de chamada no seguinte formato:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Onde servidor e porta se referem ao nome do host e ao número da porta do [!DNL AEM Forms] Server.

* Ao criar o aplicativo [!DNL Salesforce] conectado, especifique `full` e `offline_access` como os valores para o escopo OAuth.

* Anote os valores da ID do cliente (chamada de Consumer Key) e do segredo do cliente (chamada de Consumer Secret) para o aplicativo conectado.

Execute as seguintes etapas para configurar o serviço de nuvem [!DNL Salesforce]:

1. Na instância do autor [!DNL AEM Forms], navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Fontes de Dados]**. A lista de pastas de wrapper disponíveis inclui uma pasta com o título especificado para `DappTitle` enquanto [gerando o projeto de arquétipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. Selecione o nome da pasta, selecione **[!UICONTROL Configuração de nuvem do Salesforce]** e selecione **[!UICONTROL Propriedades]**.
1. Na guia **[!UICONTROL Configurações de autenticação]**:
   1. Especifique a URL do Domínio [!DNL Salesforce] no campo **[!UICONTROL Host]**. Por exemplo, [Nome-domínio].my.salesforce.com.
   1. Especifique a ID do cliente (chamada de Chave do consumidor) e o segredo do cliente (chamada de Segredo do consumidor) para o aplicativo conectado.
   1. Especifique **full offline_access** (`full` e `offine_access` valores separados por um espaço) no campo **[!UICONTROL Escopo de Autorização]**.
   1. Selecione **[!UICONTROL Conectar ao OAuth]**. Você é redirecionado à página de logon [!DNL Microsoft® Dynamics].
   1. Faça logon com suas credenciais do [!DNL Salesforce] e aceite para permitir que a configuração do serviço de nuvem se conecte ao serviço [!DNL Salesforce]. Se a conexão for bem-sucedida, você será redirecionado para a página de configuração do serviço de nuvem [!DNL Salesforce], que exibe uma mensagem de sucesso.
1. Selecione **[!UICONTROL Salvar e fechar]** para concluir a configuração.

### Acessar o [!DNL Salesforce] Form Data Model (FDM) pronto para uso

Um [!DNL Salesforce] Modelo de Dados de Formulário (FDM) está disponível por padrão no [!DNL AEM Forms] Server após você [configurar um projeto de desenvolvimento para o Forms com base no arquétipo de Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

Para acessar o Modelo de Dados de Formulário (FDM), navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrações de Dados]**. A lista de pastas disponíveis inclui uma pasta com o título especificado para `DappTitle` enquanto [gerando o projeto do arquétipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment). Selecione o nome da pasta, o **[!UICONTROL Modelo de Dados do Salesforce]** e o ícone Editar ![Editar](assets/edit.png) para exibir o modelo de dados de formulário (FDM).

Após configurar o [[!DNL Salesforce] serviço de Configuração na Nuvem](#configure-salesforce-cloud-service), você pode integrar formulários adaptáveis com o Modelo de Dados [!DNL Salesforce] pronto para uso.

## Configurar o serviço de nuvem [!DNL Microsoft® Dynamics 365] {#configure-dynamics-cloud-service}

Antes de configurar o serviço de nuvem [!DNL Microsoft® Dynamics 365], execute as seguintes tarefas:

* [Registre um aplicativo para [!DNL Microsoft® Dynamics 365] com o Azure Ative Diretory](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/walkthrough-register-app-azure-active-directory). Ao criar o aplicativo [!DNL Microsoft® Dynamics 365] conectado, especifique as URLs de Resposta no seguinte formato:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Onde servidor e porta se referem ao nome do host e ao número da porta do [!DNL AEM Forms] Server.

* Anote os valores da ID do cliente (também chamada de ID do aplicativo) e o segredo do cliente para o aplicativo conectado.

Execute as seguintes etapas para configurar o serviço de nuvem [!DNL Microsoft® Dynamics 365]:

1. Na instância do autor [!DNL AEM Forms], navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Fontes de Dados]**. A lista de pastas de wrapper disponíveis inclui uma pasta com o título especificado para `DappTitle` enquanto [gerando o projeto de arquétipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment).
1. Selecione o nome da pasta, selecione **[!UICONTROL Configuração de nuvem do Microsoft® Dynamics 365]** e selecione **[!UICONTROL Propriedades]**.
1. Na guia **[!UICONTROL Configurações de autenticação]**:
   1. Insira o valor para o campo **[!UICONTROL Raiz de Serviço]**. Vá para a instância do Dynamics e navegue até [Recursos do Desenvolvedor](https://docs.microsoft.com/en-us/powerapps/developer/data-platform/view-download-developer-resources) para exibir o valor do campo Raiz do Serviço. Por exemplo, `https://<tenant-name>.dynamics.com/api/data/v9.1/`
   1. Especifique a ID do cliente (referida como ID do aplicativo) e o segredo do cliente para o aplicativo conectado.
   1. Substitua `{tenant}` por uma ID de locatário nos campos **[!UICONTROL URL do OAuth]**, **[!UICONTROL URL do Token de Atualização]** e **[!UICONTROL URL do Token de Acesso]**.
   1. Especifique a URL da instância do Dynamics no campo **[!UICONTROL Recurso]** para configurar o [!UICONTROL Microsoft® Dynamics] com um Modelo de Dados de Formulário (FDM). Use o URL raiz do serviço para derivar o URL da instância do Dynamics. Por exemplo, `https://<tenant-name>.dynamics.com`.

   1. Especifique `openid` no campo **[!UICONTROL Escopo de Autorização]** para o processo de autorização em [!DNL Microsoft® Dynamics 365].
   1. Faça logon com suas credenciais do [!DNL Microsoft® Dynamics 365] e aceite para permitir que a configuração do serviço de nuvem se conecte ao serviço [!DNL Microsoft® Dynamics 365]. Se a conexão for bem-sucedida, você será redirecionado para a página de configuração do serviço de nuvem [!DNL Microsoft® Dynamics 365], que exibe uma mensagem de sucesso.
1. Selecione **[!UICONTROL Salvar e fechar]** para concluir a configuração.

### Acessar o [!DNL Microsoft® Dynamics 365] Form Data Model (FDM) pronto para uso

Um [!DNL Microsoft® Dynamics 365] Modelo de Dados de Formulário (FDM) está disponível por padrão no [!DNL AEM Forms] Server após você [configurar um projeto de desenvolvimento para o Forms com base no arquétipo de Experience Manager](setup-local-development-environment.md##forms-cloud-service-local-development-environment).

Para acessar o Modelo de Dados de Formulário (FDM), navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrações de Dados]**. A lista de pastas disponíveis inclui uma pasta com o título especificado para `DappTitle` enquanto [gerando o projeto do arquétipo AEM](setup-local-development-environment.md#forms-cloud-service-local-development-environment). Selecione o nome da pasta, o **[!UICONTROL Modelo de Dados do Microsoft® Dynamics 365]** e o ícone Editar ![Editar](assets/edit.png) para exibir o modelo de dados de formulário (FDM).

Após configurar o [[!DNL Microsoft® Dynamics 365] serviço de Configuração na Nuvem](#configure-dynamics-cloud-service), você pode integrar formulários adaptáveis com o Modelo de Dados [!DNL Microsoft® Dynamics 365] pronto para uso.

>[!MORELIKETHIS]
>
>* [Configurar fontes de dados para o AEM Forms](/help/forms/configure-data-sources.md)
>* [Configurar o armazenamento do Azure para o AEM Forms](/help/forms/configure-azure-storage.md)
>  [Adicionar o Portal Forms a uma página do AEM Sites](/help/forms/configure-forms-portal.md)
