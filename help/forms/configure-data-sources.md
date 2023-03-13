---
title: Como configurar fontes de dados?
description: A Integração de dados do Experience Manager Forms permite configurar e conectar-se a diferentes fontes de dados. Saiba como configurar serviços Web RESTful, serviços Web baseados em SOAP e serviços OData como fontes de dados e usá-los para criar modelos de dados de formulário.
feature: Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: 6bca307dcf41b138b5b724a8eb198ac35e2d906e
workflow-type: tm+mt
source-wordcount: '2139'
ht-degree: 0%

---

# Configurar fontes de dados {#configure-data-sources}

![Integração de dados](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] A Integração de dados permite configurar e conectar-se a diferentes fontes de dados. Os seguintes tipos são prontos para uso:

* Bancos de dados relacionais - MySQL, [!DNL Microsoft SQL Server], [!DNL IBM DB2], e [!DNL Oracle RDBMS]
* Serviços Web RESTful
* Serviços da Web com base em SOAP
* Serviços OData (Versão 4.0)
* Microsoft® Dynamics
* Força de vendas
* Armazenamento Microsoft® Azure Blob

A integração de dados é compatível com os tipos de autenticação OAuth2.0, Autenticação básica e Chave de API prontos para uso e permite a implementação de autenticação personalizada para acessar serviços da Web. Enquanto os serviços RESTful, baseados em SOAP e OData são configurados em [!DNL Experience Manager] as a Cloud Service <!--, JDBC for relational databases --> e conector para [!DNL Experience Manager] O perfil do usuário está configurado em [!DNL Experience Manager] console da web.

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] não dá suporte a banco de dados relacional.

## Configurar banco de dados relacional {#configure-relational-database}

### Pré-requisitos

Antes de configurar bancos de dados relacionais usando [!DNL Experience Manager] Configuração do console da Web, é obrigatório:
* [Habilitar rede avançada por meio da API do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html), já que as portas são desativadas por padrão.
* [Adicionar dependências de driver JDBC no Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies).


### Etapas para configurar o banco de dados relacional

É possível configurar bancos de dados relacionais usando [!DNL Experience Manager] Configuração do console da Web. Faça o seguinte:

1. Ir para [!DNL Experience Manager] console da web em `https://server:host/system/console/configMgr`.
1. Localizar **[!UICONTROL Pools de Conexões JDBC do Day Commons]** configuração. Toque para abrir a configuração no modo de edição.

   ![Pool do Conector JDBC](/help/forms/assets/jdbc_connector.png)

1. Na caixa de diálogo de configuração, especifique os detalhes do banco de dados que você deseja configurar, como:

   * Nome da classe Java™ para o driver JDBC
   * URI da conexão JDBC
   * Nome de usuário e senha para estabelecer conexão com o driver JDBC
   * Especifique uma consulta SQL SELECT no **[!UICONTROL Consulta de validação]** para validar as conexões do pool. A consulta deve retornar pelo menos uma linha. Com base no seu banco de dados, especifique uma das seguintes opções:
      * SELECT 1 (MySQL e MS SQL)
      * SELECIONE 1 no duplo (Oracle)
   * Nome da fonte de dados

   Exemplos de cadeias de caracteres para configurar o banco de dados relacional:

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```

   >[!NOTE]
   >
   > Consultar [Conexões SQL usando DataSourcePool do JDBC](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html) para obter informações mais detalhadas.

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

## Configurar pasta para configurações do serviço em nuvem {#cloud-folder}

A configuração da pasta de serviços em nuvem é necessária para configurar serviços em nuvem para serviços RESTful, SOAP e OData.

Todas as configurações do serviço em nuvem no [!DNL Experience Manager] são consolidados na `/conf` pasta em [!DNL Experience Manager] repositório. Por padrão, a variável `conf` a pasta contém o `global` pasta onde você pode criar configurações do cloud service. No entanto, você deve habilitá-lo manualmente para configurações de nuvem. Você também pode criar pastas adicionais no `conf` para criar e organizar configurações do cloud service.

Para definir a pasta de configurações do serviço de nuvem:

1. Ir para **[!UICONTROL Ferramentas > Geral > Navegador de configuração]**.
   * Consulte a [Navegador de configuração](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) para obter mais informações.
1. Faça o seguinte para habilitar a pasta global para configurações de nuvem ou ignore esta etapa para criar e configurar outra pasta para configurações de serviço de nuvem.

   1. No **[!UICONTROL Navegador de configuração]**, selecione o `global` pasta e toque em **[!UICONTROL Propriedades]**.

   1. No **[!UICONTROL Propriedades de configuração]** caixa de diálogo, ativar **[!UICONTROL Configurações da nuvem]**.

   1. Toque **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair do diálogo.

1. No **[!UICONTROL Navegador de configuração]**, toque em **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração]** , especifique um título para a pasta e habilite **[!UICONTROL Configurações da nuvem]**.
1. Toque **[!UICONTROL Criar]** para criar a pasta habilitada para configurações do cloud service.

## Configurar serviços Web RESTful {#configure-restful-web-services}

O serviço Web RESTful pode ser descrito usando [Especificações do Swagger](https://swagger.io/specification/v2/) no formato JSON ou YAML em um [!DNL Swagger] arquivo de definição. Para configurar o serviço Web RESTful no [!DNL Experience Manager] as a Cloud Service, certifique-se de ter o [!DNL Swagger] arquivo ([Versão 2.0 do Swagger](https://swagger.io/specification/v2/)ou [!DNL Swagger] arquivo ([Versão 3.0 do Swagger](https://swagger.io/specification/v3/)) no sistema de arquivos ou no URL em que o arquivo está hospedado.

### Configurar serviços RESTful para a especificação de API aberta versão 2.0 {#configure-restful-services-open-api-2.0}

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço em nuvem](configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço RESTful]** do **[!UICONTROL Tipo de serviço]** selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próxima]**.
1. Especifique os seguintes detalhes para o serviço RESTful:

   * Selecione o URL ou o arquivo na [!UICONTROL Origem do Swagger] e especificar de acordo as [!DNL Swagger URL] para o[!DNL  Swagger] arquivo de definição ou carregue o [!DNL Swagger] do seu sistema de arquivos local.
   * Com base no[!DNL  Swagger] Entrada de origem. Os seguintes campos são pré-preenchidos com valores:

      * Esquema: os protocolos de transferência usados pela API REST. O número de tipos de esquema exibidos na lista suspensa depende dos esquemas definidos na variável [!DNL Swagger] origem.
      * Host: o nome do domínio ou endereço IP do host que serve a API REST. É um campo obrigatório.
      * Caminho base: o prefixo do URL para todos os caminhos da API. É um campo opcional.\
         Se necessário, edite os valores pré-preenchidos nesses campos.
   * Selecione o tipo de autenticação — None, OAuth2.0, Basic Authentication, API Key ou Custom Authentication — para acessar o serviço RESTful e fornecer os detalhes da autenticação de acordo.

   Se você selecionar **[!UICONTROL Chave de API]** como o tipo de autenticação, especifique o valor da chave de API. A chave de API pode ser enviada como um cabeçalho de solicitação ou como um parâmetro de consulta. Selecione uma dessas opções na **[!UICONTROL Localização]** e especifique o nome do cabeçalho ou do parâmetro de consulta na lista suspensa **[!UICONTROL Nome do parâmetro]** em conformidade.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço RESTful.

### Configurar serviços RESTful para a especificação de API aberta versão 3.0 {#configure-restful-services-open-api-3.0}

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço em nuvem](configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço RESTful]** do **[!UICONTROL Tipo de serviço]** selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próxima]**.
1. Especifique os seguintes detalhes para o serviço RESTful:

   * Selecione o URL ou o arquivo na [!UICONTROL Origem do Swagger] e especificar de acordo as [!DNL Swagger 3.0 URL] para o[!DNL  Swagger] arquivo de definição ou carregue o [!DNL Swagger] do seu sistema de arquivos local.
   * Com base no[!DNL  Swagger] Entrada de origem, as informações de conexão com o servidor de destino são exibidas.
   * Selecione o tipo de autenticação — None, OAuth2.0, Basic Authentication, API Key ou Custom Authentication — para acessar o serviço RESTful e fornecer os detalhes da autenticação de acordo.

   Se você selecionar **[!UICONTROL Chave de API]** como o tipo de autenticação, especifique o valor da chave de API. A chave de API pode ser enviada como um cabeçalho de solicitação ou como um parâmetro de consulta. Selecione uma dessas opções na **[!UICONTROL Localização]** e especifique o nome do cabeçalho ou do parâmetro de consulta na lista suspensa **[!UICONTROL Nome do parâmetro]** em conformidade.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço RESTful.

Algumas das operações não suportadas pela Especificação da API aberta dos serviços RESTful versão 3.0 são:
* Retornos de chamada
* um/qualquer um
* Referência remota
* Links
* Diferentes corpos de solicitação para diferentes tipos MIME para uma única operação

Você pode consultar [Especificação do OpenAPI 3.0](https://swagger.io/specification/v3/) para obter informações detalhadas.

### Configuração do cliente HTTP do modelo de dados de formulário para otimizar o desempenho {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] o modelo de dados de formulário ao integrar com os serviços Web RESTful como fonte de dados inclui configurações de cliente HTTP para otimização de desempenho.

Defina as seguintes propriedades da variável **[!UICONTROL Configuração do cliente HTTP do modelo de dados de formulário para fonte de dados REST]** configuração para especificar a expressão regular:

* Use o `http.connection.max.per.route` propriedade para definir o número máximo de conexões permitidas entre o modelo de dados de formulário e os serviços Web RESTful. O valor padrão é de 20 conexões.

* Use o `http.connection.max` para especificar o número máximo de conexões permitidas para cada rota. O valor padrão é 40 conexões.

* Use o `http.connection.keep.alive.duration` para especificar a duração, para a qual uma conexão HTTP persistente é mantida ativa. O valor padrão é de 15 segundos.

* Use o `http.connection.timeout` propriedade para especificar a duração, para a qual a variável [!DNL Experience Manager Forms] o servidor aguarda uma conexão ser estabelecida. O valor padrão é de 10 segundos.

* Use o `http.socket.timeout` para especificar o período máximo de inatividade entre dois pacotes de dados. O valor padrão é de 30 segundos.

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

1. Toque **[!UICONTROL Configuração do cliente HTTP do modelo de dados de formulário para fonte de dados REST]**.

1. No [!UICONTROL Configuração do cliente HTTP do modelo de dados de formulário para fonte de dados REST] diálogo:

   * Especifique o número máximo de conexões permitidas entre o modelo de dados de formulário e os serviços Web RESTful no **[!UICONTROL Limite de conexão total]** campo. O valor padrão é de 20 conexões.

   * Especifique o número máximo de conexões permitidas para cada rota na **[!UICONTROL Limite de conexão por rota]** campo. O valor padrão é duas conexões.

   * Especifique a duração, para a qual uma conexão HTTP persistente é mantida ativa, em **[!UICONTROL Manter vivo]** campo. O valor padrão é de 15 segundos.

   * Especificar a duração, para a qual o [!DNL Experience Manager Forms] o servidor aguarda uma conexão ser estabelecida, no campo **[!UICONTROL Tempo limite da conexão]** campo. O valor padrão é de 10 segundos.

   * Especifique o período máximo de inatividade entre dois pacotes de dados no **[!UICONTROL Tempo limite do soquete]** campo. O valor padrão é de 30 segundos.

## Configurar serviços da Web SOAP {#configure-soap-web-services}

Os serviços da Web baseados em SOAP são descritos usando [Especificações da Web Services Description Language (WSDL)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] não dá suporte ao modelo WSDL do estilo RPC.

Para configurar o serviço da Web com base em SOAP no [!DNL Experience Manager] as a Cloud Service, verifique se você tem o URL WSDL para o serviço Web e faça o seguinte:

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço em nuvem](configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço da Web SOAP]** do **[!UICONTROL Tipo de serviço]** selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próxima]**.
1. Especifique o seguinte para o serviço Web SOAP:

   * URL WSDL do serviço Web.
   * Terminal de serviço. Especifique um valor neste campo para substituir o ponto final de serviço mencionado no WSDL.
   * Selecione o tipo de autenticação — None, OAuth2.0, Basic Authentication ou Custom Authentication — para acessar o serviço SOAP e fornecer os detalhes de autenticação de acordo.

      <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
      <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

      <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Toque **[!UICONTROL Criar]** para criar a configuração de nuvem do serviço da Web SOAP.

### Habilitar o uso de instruções de importação em WSDL de serviços Web SOAP {#enable-import-statements}

Você pode especificar uma expressão regular que serve como filtro para URLs absolutos que são permitidos como instruções de importação em WSDL de serviços Web SOAP. Por padrão, não há nenhum valor nesse campo. Como resultado, [!DNL Experience Manager] bloqueia todas as instruções de importação disponíveis no WSDL. Se você especificar `.*` como o valor neste campo, [!DNL Experience Manager] permite todas as instruções de importação.

Defina o `importAllowlistPattern` propriedade do **[!UICONTROL Importação e Inclui na lista de permissões de serviços da Web SOAP do modelo de dados de formulário]** configuração para especificar a expressão regular. O seguinte arquivo JSON exibe uma amostra:


```json
{
  "importAllowlistPattern": ".*"
}
```


Para definir valores de uma configuração, [Gerar configurações de OSGi usando o SDK do AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart), e [implantar a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) para a instância do Cloud Service.

## Configurar serviços OData {#config-odata}

Um serviço OData é identificado por sua URL raiz de serviço. Para configurar um serviço OData no [!DNL Experience Manager] as a Cloud Service, verifique se você tem um URL raiz de serviço para o serviço e faça o seguinte:

>[!NOTE]
>
> Suporte ao modelo de dados de formulário [OData versão 4](https://www.odata.org/documentation/).
>Para obter um guia passo a passo para configurar o [!DNL Microsoft® Dynamics 365]on-line ou no local, consulte [[!DNL Microsoft® Dynamics] Configuração OData](ms-dynamics-odata-configuration.md).

1. Ir para **[!UICONTROL Ferramentas > Cloud Services > Fontes de dados]**. Toque para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço em nuvem](#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do cloud service.

1. Toque **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente para Criar Configuração da Fonte de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço OData]** do **[!UICONTROL Tipo de serviço]** selecione uma imagem em miniatura para a configuração e toque em **[!UICONTROL Próxima]**.
1. Especifique os seguintes detalhes para o serviço OData:

   * URL da Raiz de Serviço do serviço OData a ser configurado.
   * Selecione o tipo de autenticação — None, OAuth2.0, Basic Authentication, API Key ou Custom Authentication — para acessar o serviço OData e fornecer os detalhes de autenticação de acordo.

   Se você selecionar **[!UICONTROL Chave de API]** como o tipo de autenticação, especifique o valor da chave de API. A chave de API pode ser enviada como um cabeçalho de solicitação ou como um parâmetro de consulta. Selecione uma dessas opções na **[!UICONTROL Localização]** e especifique o nome do cabeçalho ou do parâmetro de consulta na lista suspensa **[!UICONTROL Nome do parâmetro]** em conformidade.

   >[!NOTE]
   Você deve selecionar o tipo de autenticação do OAuth 2.0 para se conectar [!DNL Microsoft® Dynamics] serviços usando o ponto de extremidade OData como a raiz do serviço.

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

Você configurou as fontes de dados. Em seguida, você pode criar um modelo de dados de formulário ou, se já tiver criado um modelo de dados de formulário sem uma fonte de dados, poderá associá-lo às fontes de dados configuradas. Consulte [Criar modelo de dados de formulário](create-form-data-models.md) para obter detalhes.
