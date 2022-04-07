---
title: Como configurar as fontes de dados?
description: A Integração de dados do Experience Manager Forms permite configurar e se conectar a fontes de dados diferentes. Saiba como configurar serviços Web RESTful, serviços Web baseados em SOAP e serviços OData como fontes de dados e usá-los para criar modelos de dados de formulário.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: b6c654f5456e1a7778b453837f04cbed32a82a77
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 0%

---

# Configurar fontes de dados {#configure-data-sources}

![Integração de dados](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] A Integração de dados permite configurar e conectar-se a fontes de dados diferentes. Os seguintes tipos são suportados prontos para uso. No entanto, com pouca personalização, também é possível integrar outras fontes de dados.

<!-- * Relational databases - MySQL, [!DNL Microsoft SQL Server], [!DNL IBM DB2], and [!DNL Oracle RDBMS] 
* [!DNL Experience Manager] user profile  -->
* Serviços Web RESTful
* Serviços Web baseados em SOAP
* Serviços OData

A integração de dados oferece suporte aos tipos de autenticação OAuth2.0, Basic Authentication e API Key prontos para uso e permite implementar autenticação personalizada para acessar serviços da Web. Enquanto os serviços RESTful, baseados em SOAP e OData são configurados em [!DNL Experience Manager] as a Cloud Service <!--, JDBC for relational databases --> e conector para [!DNL Experience Manager] o perfil de usuário é configurado em [!DNL Experience Manager] console da Web.

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] não suporta banco de dados relacional.

<!-- ## Configure relational database {#configure-relational-database}

You can configure relational databases using [!DNL Experience Manager] Web Console Configuration. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://server:host/system/console/configMgr`.
1. Look for **[!UICONTROL Apache Sling Connection Pooled DataSource]** configuration. Tap to open the configuration in edit mode.
1. In the configuration dialog, specify the details for the database you want to configure, such as:

    * Name of the data source
    * Data source service property that stores the data source name
    * Java class name for the JDBC driver
    * JDBC connection URI
    * Username and password to establish connection with the JDBC driver

   >[!NOTE]
   >
   >Ensure that you encrypt sensitive information like passwords before configuring the data source. To encrypt:
   >
   >    
   >    
   >    1. Go to https://'[server]:[port]'/system/console/crypto.
   >    1. In the **[!UICONTROL Plain Text]** field, specify the password or any string to encrypt and tap **[!UICONTROL Protect]**.
   >    
   >    
   >    
   >The encrypted text appears in the Protected Text field that you can specify in the configuration.

1. Enable **[!UICONTROL Test on Borrow]** or **[!UICONTROL Test on Return]** to specify that the objects are validated before being borrowed or returned from and to the pool, respectively.
1. Specify a SQL SELECT query in the **[!UICONTROL Validation Query]** field to validate connections from the pool. The query must return at least one row. Based on your database, specify one of the following:

    * SELECT 1 (MySQL and MS SQL) 
    * SELECT 1 from dual (Oracle)

1. Tap **[!UICONTROL Save]** to save the configuration. -->

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties will be available for use in form data model. Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Tap **[!UICONTROL Save]** to save the configuration. -->

## Configurar pasta para configurações do serviço de nuvem {#cloud-folder}

A configuração da pasta de serviços em nuvem é necessária para configurar os serviços em nuvem para os serviços RESTful, SOAP e OData.

Todas as configurações do serviço em nuvem em [!DNL Experience Manager] são consolidadas no `/conf` pasta em [!DNL Experience Manager] repositório. Por padrão, a variável `conf` A pasta contém o `global` pasta onde você pode criar configurações do serviço de nuvem. No entanto, é necessário ativá-lo manualmente para configurações de nuvem. Você também pode criar pastas adicionais em `conf` para criar e organizar configurações do serviço de nuvem.

Para configurar a pasta das configurações do serviço de nuvem:

1. Ir para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**.
   * Consulte a [Navegador de configuração](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) documentação para obter mais informações.
1. Faça o seguinte para habilitar a pasta global para configurações de nuvem ou ignore esta etapa para criar e configurar outra pasta para configurações do serviço de nuvem.

   1. No **[!UICONTROL Navegador de configuração]**, selecione o `global` pasta e toque **[!UICONTROL Propriedades]**.

   1. No **[!UICONTROL Propriedades da configuração]** caixa de diálogo, habilitar **[!UICONTROL Configurações da nuvem]**.

   1. Toque **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.

1. No **[!UICONTROL Navegador de configuração]**, toque em **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um título para a pasta e habilite **[!UICONTROL Configurações da nuvem]**.
1. Toque **[!UICONTROL Criar]** para criar a pasta habilitada para as configurações do serviço de nuvem.

## Configurar serviços Web RESTful {#configure-restful-web-services}

O serviço Web RESTful pode ser descrito usando [Especificações do Swagger](https://swagger.io/specification/) no formato JSON ou YAML em um [!DNL Swagger] arquivo de definição. Para configurar o serviço Web RESTful no [!DNL Experience Manager] as a Cloud Service, certifique-se de ter a variável [!DNL Swagger] no seu sistema de arquivos ou no URL onde o arquivo está hospedado.

Faça o seguinte para configurar os serviços RESTful:

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta onde deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especificar um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço RESTful]** do **[!UICONTROL Tipo de serviço]** como opção, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço RESTful:

   * Selecione o URL ou o arquivo do [!UICONTROL Origem do Swagger] e especifique a variável [!DNL Swagger URL] para[!DNL  Swagger] arquivo de definição ou upload do [!DNL Swagger] do seu sistema de arquivos local.
   * Com base na[!DNL  Swagger] Entrada de origem, os seguintes campos são pré-preenchidos com valores:

      * Regime: Os protocolos de transferência usados pela REST API. O número de tipos de esquema exibidos na lista suspensa depende dos esquemas definidos na variável [!DNL Swagger] fonte.
      * Host: O nome de domínio ou endereço IP do host que serve a API REST. É um campo obrigatório.
      * Caminho básico: O prefixo do URL para todos os caminhos da API. É um campo opcional.\
         Se necessário, edite os valores pré-preenchidos para esses campos.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação Básica, Chave da API ou Autenticação Personalizada — para acessar o serviço RESTful e, de acordo, fornecer detalhes para autenticação.

   Se você selecionar **[!UICONTROL Chave da API]** como tipo de autenticação, especifique o valor da chave de API. A chave da API pode ser enviada como cabeçalho de solicitação ou como parâmetro de consulta. Selecione uma dessas opções no **[!UICONTROL Localização]** e especifique o nome do cabeçalho ou do parâmetro de consulta na **[!UICONTROL Nome do parâmetro]** correspondente.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço RESTful.

### Modelo de dados de formulário Configuração do cliente HTTP para otimizar o desempenho {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] O modelo de dados de formulário ao integrar com os serviços Web RESTful como fonte de dados inclui configurações de cliente HTTP para otimização de desempenho.
Execute as seguintes etapas para configurar o cliente HTTP do modelo de dados de formulário:

1. Faça logon em [!DNL Experience Manager Forms] Instância do autor como administrador e acesse [!DNL Experience Manager] pacotes do console da web. O URL padrão é [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Toque **[!UICONTROL Modelo de dados de formulário Configuração do cliente HTTP para fonte de dados REST]**.

1. No [!UICONTROL Modelo de dados de formulário Configuração do cliente HTTP para fonte de dados REST] caixa de diálogo:

   * Especifique o número máximo de conexões permitidas entre o modelo de dados de formulário e os serviços Web RESTful no **[!UICONTROL Limite de conexão no total]** campo. O valor padrão é 20 conexões.

   * Especifique o número máximo de conexões permitidas para cada rota no **[!UICONTROL Limite de conexão por rota]** campo. O valor padrão é 2 conexões.

   * Especifique a duração, para a qual uma conexão HTTP persistente é mantida viva, no **[!UICONTROL Manter vivo]** campo. O valor padrão é de 15 segundos.

   * Especifique a duração, para a qual a variável [!DNL Experience Manager Forms] O servidor aguarda que uma conexão seja estabelecida no **[!UICONTROL Tempo limite da conexão]** campo. O valor padrão é de 10 segundos.

   * Especifique o período máximo de tempo para a inatividade entre dois pacotes de dados no **[!UICONTROL Tempo limite do soquete]** campo. O valor padrão é de 30 segundos.


## Configurar serviços Web SOAP {#configure-soap-web-services}

Os serviços da Web baseados em SOAP são descritos usando [Especificações de WSDL (Web Services Description Language)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] não suporta o modelo WSDL de estilo RPC.

Para configurar o serviço da Web baseado em SOAP em [!DNL Experience Manager] as a Cloud Service, certifique-se de ter o URL WSDL para o serviço da Web e faça o seguinte:

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta onde deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especificar um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço Web SOAP]** do **[!UICONTROL Tipo de serviço]** como opção, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique o seguinte para o serviço Web SOAP:

   * URL WSDL do serviço da Web.
   * Terminal de serviço. Especifique um valor nesse campo para substituir o ponto de extremidade de serviço mencionado no WSDL.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação Básica ou Autenticação Personalizada — para acessar o serviço SOAP e fornecer os detalhes para autenticação.

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço da Web SOAP.

### Ativar o uso de instruções de importação no WSDL de serviços Web SOAP {#enable-import-statements}

Você pode especificar uma expressão regular que serve como filtro para URLs absolutos permitidos como declarações de importação no WSDL de serviços da Web SOAP. Por padrão, não há valor neste campo. Como resultado, [!DNL Experience Manager] bloqueia todas as instruções de importação disponíveis no WSDL. Se você especificar `.*` como o valor neste campo, [!DNL Experience Manager] permite todas as declarações de importação.

Defina as `importAllowlistPattern` da **[!UICONTROL de Importação de Serviços Web SOAP do Modelo de Dados de Formulário]** configuração para especificar a expressão regular. O seguinte arquivo JSON exibe uma amostra:

```json
{
  "importAllowlistPattern": ".*"
}
```

Para definir valores de uma configuração, [Gerar configurações de OSGi usando o SDK AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)e [implantar a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) para a instância do Cloud Service.

## Configurar serviços OData {#config-odata}

Um serviço OData é identificado por seu URL raiz do serviço. Para configurar um serviço OData em [!DNL Experience Manager] as a Cloud Service, certifique-se de ter o URL raiz do serviço e faça o seguinte:

>[!NOTE]
>
> Suporte ao modelo de dados de formulário [OData versão 4](https://www.odata.org/documentation/).
>Para obter o guia passo a passo da configuração do [!DNL Microsoft Dynamics 365], em linha ou no local, consulte [[!DNL Microsoft Dynamics] Configuração de OData](ms-dynamics-odata-configuration.md).

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta onde deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especificar um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço OData]** do **[!UICONTROL Tipo de serviço]** como opção, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço OData:

   * URL raiz do serviço do serviço OData a ser configurado.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação Básica, Chave da API ou Autenticação Personalizada — para acessar o serviço OData e fornecer os detalhes para autenticação.

   Se você selecionar **[!UICONTROL Chave da API]** como tipo de autenticação, especifique o valor da chave de API. A chave da API pode ser enviada como cabeçalho de solicitação ou como parâmetro de consulta. Selecione uma dessas opções no **[!UICONTROL Localização]** e especifique o nome do cabeçalho ou do parâmetro de consulta na **[!UICONTROL Nome do parâmetro]** correspondente.

   >[!NOTE]
   >
   >Você deve selecionar o tipo de autenticação OAuth 2.0 com o qual se conectar [!DNL Microsoft Dynamics] serviços que usam o ponto de extremidade OData como a raiz do serviço.

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço OData.

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other’s identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Próximas etapas {#next-steps}

As fontes de dados foram configuradas. Em seguida, é possível criar um Modelo de dados de formulário ou, se já tiver criado um Modelo de dados de formulário sem uma fonte de dados, associá-lo às fontes de dados recém-configuradas. Consulte [Criar modelo de dados de formulário](create-form-data-models.md) para obter detalhes.
