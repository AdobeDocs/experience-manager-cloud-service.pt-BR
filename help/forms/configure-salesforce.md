---
title: Como configurar modelos de dados de formulário prontos para uso do Salesforce para o Adaptive Forms?
description: Saiba como integrar o Salesforce ao Adaptive Forms.
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 184db05b-7237-4dce-8059-03c39b93d7d7
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Configurar o Salesforce para o AEM Forms {#configure-azure-storage}

A [[!DNL Experience Manager Forms] Integração de Dados](data-integration.md) fornece o [!DNL Salesforce] Cloud Services para integrar o Forms Adaptável com o Modelo de Dados de Formulário (FDM) OOTB. O Forms adaptável pode interagir com os servidores do [!DNL Salesforce] para habilitar fluxos de trabalho de negócios. Por exemplo:

* Gravar dados em [!DNL Salesforce] no envio do Formulário Adaptável.
* Grave dados em [!DNL Salesforce] por meio de entidades personalizadas definidas no Modelo de Dados de Formulário (FDM) e vice-versa.
* Consulte o servidor [!DNL Salesforce] para obter dados e popular previamente o Forms Adaptável.
* Ler dados do servidor [!DNL Salesforce].

Os [!DNL Salesforce] serviços em nuvem e o Form Data Model (FDM) estão disponíveis imediatamente no [!DNL AEM Forms] Server depois que você [configurou um projeto de desenvolvimento para o Forms com base no arquétipo Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

>[!NOTE]
>
>Os [!DNL Salesforce] serviços em nuvem e o Modelo de dados de formulário (FDM) estarão disponíveis imediatamente se você configurar um [!DNL Experience Manager Forms] como um projeto [!DNL Cloud Service] com base no [Arquétipo do AEM 30](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30) ou posterior.

## Configurar o serviço de nuvem [!DNL Salesforce] {#configure-salesforce-cloud-service}

Antes de configurar os serviços de nuvem do [!DNL Salesforce], execute as seguintes tarefas:

* [Criar um  [!DNL Salesforce] aplicativo](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&type=5) habilitado para OAuth conectado. Ao criar o aplicativo conectado [!DNL Salesforce], especifique a URL de retorno de chamada no seguinte formato:

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  Onde servidor e porta se referem ao nome do host e ao número da porta do [!DNL AEM Forms] Server.

* Ao criar o aplicativo [!DNL Salesforce] conectado, especifique `full` e `offline_access` como os valores para o escopo OAuth.

* Anote os valores da ID do cliente (chamada de Consumer Key) e do segredo do cliente (chamada de Consumer Secret) para o aplicativo conectado.

Execute as seguintes etapas para configurar o serviço de nuvem [!DNL Salesforce]:

1. Na instância do autor [!DNL AEM Forms], navegue até **[!UICONTROL Ferramentas]** ![martelo](assets/hammer.png) > **[!UICONTROL Serviços da nuvem]** > **[!UICONTROL Fontes de dados]**.
2. Selecione o nome da pasta, selecione **[!UICONTROL Salesforce Cloud Config]** e **[!UICONTROL Properties]**.
3. Na guia **[!UICONTROL Configurações de autenticação]**:
   1. Especifique a URL do Domínio [!DNL Salesforce] no campo **[!UICONTROL Host]**. Por exemplo, [Nome-domínio].my.salesforce.com.
   2. Especifique a ID do cliente (chamada de Chave do consumidor) e o segredo do cliente (chamada de Segredo do consumidor) para o aplicativo conectado.
   3. Especifique **full offline_access** (`full` e `offine_access` valores separados por um espaço) no campo **[!UICONTROL Escopo de Autorização]**.
   4. Selecione **[!UICONTROL Conectar ao OAuth]**. Você é redirecionado à página de logon [!DNL Salesforce].
   5. Faça logon com suas credenciais do [!DNL Salesforce] e aceite para permitir que a configuração do serviço de nuvem se conecte ao serviço [!DNL Salesforce]. Se a conexão for bem-sucedida, você será redirecionado para a página de configuração do serviço de nuvem [!DNL Salesforce], que exibe uma mensagem de sucesso.
4. Selecione **[!UICONTROL Salvar e fechar]** para concluir a configuração.

### Acessar o [!DNL Salesforce] Form Data Model (FDM) pronto para uso

Um FDM (Modelo de Dados de Formulário) do [!DNL Salesforce] está disponível por padrão no Servidor do [!DNL AEM Forms] depois que você [configurou um projeto de desenvolvimento para o Forms com base no arquétipo do Experience Manager](setup-local-development-environment.md#forms-cloud-service-local-development-environment).

Para acessar o Modelo de dados de formulário (FDM):

1. Navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Integrações de Dados]**.
1. Selecione o nome da pasta, o **[!UICONTROL Modelo de Dados do Salesforce]** e o ícone Editar ![Editar](assets/edit.png) para exibir o modelo de dados de formulário (FDM).

Após configurar o [[!DNL Salesforce] serviço de Configuração na Nuvem](#configure-salesforce-cloud-service), você pode integrar formulários adaptáveis com o Modelo de Dados [!DNL Salesforce] pronto para uso.

>[!MORELIKETHIS]
>
>* [Configurar fontes de dados para o AEM Forms](/help/forms/configure-data-sources.md)
>* [Configurar o armazenamento do Azure para o AEM Forms](/help/forms/configure-azure-storage.md)
>  [Adicionar o Portal Forms a uma página do AEM Sites](/help/forms/configure-forms-portal.md)
