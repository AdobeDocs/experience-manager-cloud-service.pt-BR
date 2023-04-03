---
title: Como configurar as fontes de dados?
description: A Integração de dados do Experience Manager Forms permite configurar e se conectar a fontes de dados diferentes. Saiba como configurar serviços Web RESTful, serviços Web baseados em SOAP e serviços OData como fontes de dados e usá-los para criar modelos de dados de formulário.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: 936aa33ca334523aa84300f540bde9543eb7ffb4
workflow-type: tm+mt
source-wordcount: '2135'
ht-degree: 0%

---

# Configurar fontes de dados {#configure-data-sources}

![Integração de dados](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] A Integração de dados permite configurar e conectar-se a fontes de dados diferentes. Os seguintes tipos são suportados imediatamente:

* Bancos de dados relacionais - MySQL, [!DNL Microsoft SQL Server], [!DNL IBM DB2]e [!DNL Oracle RDBMS]
* Serviços Web RESTful
* Serviços Web baseados em SOAP
* Serviços OData (Versão 4.0)
* Microsoft® Dynamics
* SalesForce
* Armazenamento de blobs do Microsoft® Azure

A integração de dados oferece suporte aos tipos de autenticação OAuth2.0, Basic Authentication e API Key prontos para uso e permite implementar autenticação personalizada para acessar serviços da Web. Enquanto os serviços RESTful, baseados em SOAP e OData são configurados em [!DNL Experience Manager] as a Cloud Service, JDBC para bancos de dados relacionais e conector para [!DNL Experience Manager] o perfil de usuário é configurado em [!DNL Experience Manager] console da Web.

## Configurar banco de dados relacional {#configure-relational-database}

### Pré-requisitos

Antes de configurar bancos de dados relacionais usando [!DNL Experience Manager] Configuração do Console da Web, é obrigatório:
* [Habilitar rede avançada por meio da API do cloud manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html), já que as portas estão desativadas por padrão.
* [Adicionar dependências de driver JDBC no Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies).


### Etapas para configurar o banco de dados relacional

Você pode configurar bancos de dados relacionais usando [!DNL Experience Manager] Configuração do Console da Web. Faça o seguinte:

1. Ir para [!DNL Experience Manager] console da Web em `https://server:host/system/console/configMgr`.
1. Localizar **[!UICONTROL Pools de Conexões JDBC do Day Commons]** configuração. Toque em para abrir a configuração no modo de edição.

   ![Pool de conectores JDBC](/help/forms/assets/jdbc_connector.png)

1. Na caixa de diálogo de configuração, especifique os detalhes do banco de dados que deseja configurar, como:

   * Nome da classe Java™ para o driver JDBC
   * URI de conexão JDBC
   * Nome de usuário e senha para estabelecer conexão com o driver JDBC
   * Especifique uma consulta SQL SELECT no **[!UICONTROL Consulta de validação]** para validar conexões do pool. A consulta deve retornar pelo menos uma linha. Com base no seu banco de dados, especifique um dos seguintes:
      * SELECT 1 (MySQL e MS SQL)
      * SELECIONE 1 de duplo (Oracle)
   * Nome da fonte de dados

   Strings de amostra para configurar o banco de dados relacional:

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > Consulte [Conexões SQL usando JDBC DataSourcePool](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html) para obter informações mais detalhadas.

1. Toque **[!UICONTROL Salvar]** para salvar a configuração.

Agora, você pode usar o banco de dados relacional configurado com seu Modelo de dados de formulário.

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

O serviço Web RESTful pode ser descrito usando [Especificações do Swagger](https://swagger.io/specification/v2/) no formato JSON ou YAML em um [!DNL Swagger] arquivo de definição. Para configurar o serviço Web RESTful no [!DNL Experience Manager] as a Cloud Service, certifique-se de ter a variável [!DNL Swagger] file ([Swagger versão 2.0](https://swagger.io/specification/v2/)) ou [!DNL Swagger] file ([Swagger versão 3.0](https://swagger.io/specification/v3/)) no sistema de arquivos ou no URL onde o arquivo está hospedado.

### Configurar serviços RESTful para Especificação de API aberta versão 2.0 {#configure-restful-services-open-api-2.0}

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta onde deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especificar um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço RESTful]** do **[!UICONTROL Tipo de serviço]** como opção, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço RESTful:

   * Selecione o URL ou o arquivo do [!UICONTROL Origem do Swagger] e especifique a variável [!DNL Swagger URL] para[!DNL  Swagger] arquivo de definição ou upload do [!DNL Swagger] do seu sistema de arquivos local.
   * Com base na[!DNL  Swagger] Entrada de origem., os seguintes campos são pré-preenchidos com valores:

      * Regime: Os protocolos de transferência usados pela REST API. O número de tipos de esquema exibidos na lista suspensa depende dos esquemas definidos na variável [!DNL Swagger] fonte.
      * Host: O nome de domínio ou endereço IP do host que serve a API REST. É um campo obrigatório.
      * Caminho básico: O prefixo do URL para todos os caminhos da API. É um campo opcional.\
         Se necessário, edite os valores pré-preenchidos para esses campos.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação Básica, Chave da API ou Autenticação Personalizada — para acessar o serviço RESTful e, de acordo, fornecer detalhes para autenticação.

   Se você selecionar **[!UICONTROL Chave da API]** como tipo de autenticação, especifique o valor da chave de API. A chave da API pode ser enviada como cabeçalho de solicitação ou como parâmetro de consulta. Selecione uma dessas opções no **[!UICONTROL Localização]** e especifique o nome do cabeçalho ou do parâmetro de consulta na **[!UICONTROL Nome do parâmetro]** correspondente.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço RESTful.

### Configurar serviços RESTful para Especificação de API aberta versão 3.0 {#configure-restful-services-open-api-3.0}

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta onde deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especificar um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço RESTful]** do **[!UICONTROL Tipo de serviço]** como opção, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço RESTful:

   * Selecione o URL ou o arquivo do [!UICONTROL Origem do Swagger] e especifique a variável [!DNL Swagger 3.0 URL] para[!DNL  Swagger] arquivo de definição ou upload do [!DNL Swagger] do seu sistema de arquivos local.
   * Com base na[!DNL  Swagger] Entrada de origem, as informações de conexão com o servidor de destino são exibidas.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação Básica, Chave da API ou Autenticação Personalizada — para acessar o serviço RESTful e, de acordo, fornecer detalhes para autenticação.

   Se você selecionar **[!UICONTROL Chave da API]** como tipo de autenticação, especifique o valor da chave de API. A chave da API pode ser enviada como cabeçalho de solicitação ou como parâmetro de consulta. Selecione uma dessas opções no **[!UICONTROL Localização]** e especifique o nome do cabeçalho ou do parâmetro de consulta na **[!UICONTROL Nome do parâmetro]** correspondente.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço RESTful.

Algumas das operações não compatíveis com a versão 3.0 da especificação de API aberta dos serviços RESTful são:
* Retornos de chamada
* one/anyof
* Referência remota
* Links
* Diferentes organismos de solicitação para diferentes tipos MIME para uma única operação

Você pode se referir a [Especificação do OpenAPI 3.0](https://swagger.io/specification/v3/) para obter informações detalhadas.

### Modelo de dados de formulário Configuração do cliente HTTP para otimizar o desempenho {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] O modelo de dados de formulário ao integrar com os serviços Web RESTful como fonte de dados inclui configurações de cliente HTTP para otimização de desempenho.

Defina as seguintes propriedades da variável **[!UICONTROL Modelo de dados de formulário Configuração do cliente HTTP para fonte de dados REST]** configuração para especificar a expressão regular:

* Use o `http.connection.max.per.route` para definir o número máximo de conexões permitidas entre o modelo de dados de formulário e os serviços da Web RESTful. O valor padrão é 20 conexões.

* Use o `http.connection.max` para especificar o número máximo de conexões permitidas para cada rota. O valor padrão é 40 conexões.

* Use o `http.connection.keep.alive.duration` para especificar a duração, para a qual uma conexão HTTP persistente é mantida ativa. O valor padrão é de 15 segundos.

* Use o `http.connection.timeout` para especificar a duração, para a qual a variável [!DNL Experience Manager Forms] O servidor aguarda uma conexão ser estabelecida. O valor padrão é de 10 segundos.

* Use o `http.socket.timeout` para especificar o período máximo de tempo para inatividade entre dois pacotes de dados. O valor padrão é de 30 segundos.

O seguinte arquivo JSON exibe uma amostra:


```json
{   
   "http.connection.keep.alive.duration":"15",   
   "http.connection.max.per.route":"20",   
   "http.connection.timeout":"10",   
   "http.socket.timeout":"30",   
   "http.connection.idle.connection.timeout":"15",   
   "http.connection.max":"40" 
} 
```

1. Toque **[!UICONTROL Modelo de dados de formulário Configuração do cliente HTTP para fonte de dados REST]**.

1. No [!UICONTROL Modelo de dados de formulário Configuração do cliente HTTP para fonte de dados REST] caixa de diálogo:

   * Especifique o número máximo de conexões permitidas entre o modelo de dados de formulário e os serviços Web RESTful no **[!UICONTROL Limite de conexão no total]** campo. O valor padrão é 20 conexões.

   * Especifique o número máximo de conexões permitidas para cada rota no **[!UICONTROL Limite de conexão por rota]** campo. O valor padrão é duas conexões.

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
>Para obter o guia passo a passo da configuração do [!DNL Microsoft® Dynamics 365], em linha ou no local, consulte [[!DNL Microsoft® Dynamics] Configuração de OData](ms-dynamics-odata-configuration.md).

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta onde deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especificar um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço OData]** do **[!UICONTROL Tipo de serviço]** como opção, navegue e selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço OData:

   * URL raiz do serviço do serviço OData a ser configurado.
   * Selecione o tipo de autenticação — Nenhum, OAuth2.0, Autenticação Básica, Chave da API ou Autenticação Personalizada — para acessar o serviço OData e fornecer os detalhes para autenticação.

   Se você selecionar **[!UICONTROL Chave da API]** como tipo de autenticação, especifique o valor da chave de API. A chave da API pode ser enviada como cabeçalho de solicitação ou como parâmetro de consulta. Selecione uma dessas opções no **[!UICONTROL Localização]** e especifique o nome do cabeçalho ou do parâmetro de consulta na **[!UICONTROL Nome do parâmetro]** correspondente.

   >[!NOTE]
   Você deve selecionar o tipo de autenticação OAuth 2.0 com o qual se conectar [!DNL Microsoft® Dynamics] serviços que usam o ponto de extremidade OData como a raiz do serviço.

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço OData.

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model, both the data source and [!DNL Experience Manager] Server running Form Data Model authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and tap **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and tap **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, tap **[!UICONTROL Select Certificate File]**, upload the certificate, and tap **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Próximas etapas {#next-steps}

As fontes de dados foram configuradas. Em seguida, é possível criar um Modelo de dados de formulário ou, se já tiver criado um Modelo de dados de formulário sem uma fonte de dados, associá-lo às fontes de dados configuradas. Consulte [Criar modelo de dados de formulário](create-form-data-models.md) para obter detalhes.
