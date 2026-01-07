---
title: Como configurar fontes de dados?
description: Saiba como configurar serviços Web RESTful, serviços Web baseados em SOAP e serviços OData como fontes de dados para um modelo de dados de formulário (FDM).
feature: Adaptive Forms, Form Data Model
role: User, Developer
level: Beginner
exl-id: cb77a840-d705-4406-a94d-c85a6efc8f5d
source-git-commit: f913871da16b44d7a465e0fa00608835524ba7e3
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 1%

---


# Configurar fontes de dados {#configure-data-sources}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/configure-data-sources.html) |
| AEM as a Cloud Service | Este artigo |

![Integração de dados](do-not-localize/data-integeration.png)

A Integração de Dados do [!DNL Experience Manager Forms] permite que você configure e se conecte a fontes de dados diferentes. Os seguintes tipos são prontos para uso:

* Bancos de dados relacionais - MySQL, [!DNL Microsoft® SQL Server], [!DNL IBM® DB2®], postgreSQL, Azure SQL e [!DNL Oracle RDBMS]
* Serviços Web RESTful
* Serviços da Web com base no SOAP
* Serviços OData (Versão 4.0)
* Microsoft® Dynamics
* Salesforce
* Armazenamento Microsoft® Azure Blob

A integração de dados oferece suporte aos tipos de autenticação OAuth2.0([Código de Autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais de Cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticação Básica e Chave de API prontos para uso, e permite a implementação de autenticação personalizada para acessar serviços Web. Enquanto os serviços RESTful, baseados em SOAP e OData estão configurados no as a Cloud Service [!DNL Experience Manager], o JDBC para bancos de dados relacionais e o conector para o perfil de usuário [!DNL Experience Manager] estão configurados no console Web [!DNL Experience Manager].

## Configurar banco de dados relacional {#configure-relational-database}

### Pré-requisitos

Antes de configurar bancos de dados relacionais usando a Configuração do Console da Web [!DNL Experience Manager], é obrigatório:

* [Habilite a rede avançada por meio da API do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/advanced-networking.html), já que as portas são desabilitadas por padrão.
* [Adicionar dependências de driver JDBC no Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html?lang=en#mysql-driver-dependencies).


### Etapas para configurar um banco de dados relacional

Você pode configurar bancos de dados relacionais usando a Configuração do Console da Web [!DNL Experience Manager]. Faça o seguinte:

**Etapa1: clonar repositório Git do AEM as a Cloud Service**

1. Abra a linha de comando e escolha um diretório para armazenar seu repositório do AEM as a Cloud Service, como `/cloud-service-repository/`.

2. Execute o comando abaixo para clonar o repositório:

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **Onde encontrar essas informações?**

   Para obter as instruções passo a passo sobre como localizar esses detalhes, consulte o artigo &quot;[Acessando o Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git)&quot; da Adobe Experience League.

   Quando o comando for concluído com sucesso, você verá uma nova pasta criada no diretório local. Esta pasta é nomeada em homenagem ao seu aplicativo.

**Etapa 2: Navegar até a Pasta de Configuração**

1. Abra a pasta do repositório em um editor.

1. Navegue até o seguinte diretório em seu `<application folder>`, onde a configuração OSGi do pool JDBC deve ser colocada:

   ```bash
   cd ui.config/src/jcr_root/apps/<application folder>/osgiconfig/config/
   ```

**Etapa 3: Criar o Arquivo de Configuração de Conexão MySQL**

1. Crie o arquivo:

   ```bash
   com.day.commons.datasource.jdbcpool.JdbcPoolService~<application folder>-mysql.cfg.json
   ```

1. Adicione as linhas de código abaixo:

```json
{
  "jdbc.driver.class": "com.mysql.cj.jdbc.Driver",
  "jdbc.connection.uri": "jdbc:mysql://<hostname>:<port>/<database>?useSSL=false",
  "jdbc.username": "<your-db-username>",
  "jdbc.password": "<your-db-password>",
  "datasource.name": "<application folder>-mysql",
  "datasource.svc.prop.name": "<application folder>-mysql"
}
```

> 
>
> Substitua espaços reservados como `<application folder>`, `<hostname>`, `<database>`, `<your-db-username>` e `<your-db-password>` por valores reais.

**Etapa 4: confirmar e enviar as alterações**

Abra o terminal e execute os comandos abaixo:

```bash
git add .
git commit -m "<commit message>"
git push 
```

**Etapa 5: implantar as alterações por meio do pipeline de Cloud Manager**

1. Faça logon no **AEM Cloud Manager**.
1. Navegue até o projeto e execute o pipeline para implantar as alterações.

>[!NOTE]
>
> Consulte [Conexões SQL usando o JDBC DataSourcePool](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/networking/examples/sql-datasourcepool.html) para obter informações mais detalhadas.

<!--
1. Go to [!DNL Experience Manager] web console at `https://server:host/system/console/configMgr`.
2. Locate **[!UICONTROL Day Commons JDBC Connections Pools]** configuration. Select to open the configuration in edit mode.

   ![JDBC Connector Pool](/help/forms/assets/jdbc_connector.png)

3. In the configuration dialog, specify the details for the database you want to configure, such as:

    * Java&trade; class name for the JDBC driver
    * JDBC connection URI
    * Username and password to establish connection with the JDBC driver
    * Specify a SQL SELECT query in the **[!UICONTROL Validation Query]** field to validate connections from the pool. The query must return at least one row. Based on your database, specify one of the following:
      * SELECT 1 (MySQL and MS&reg; SQL) 
      * SELECT 1 from dual (Oracle)
    * Name of the data source

   Sample strings for configuring a relational database:

   ```text
      "datasource.name": "sqldatasourcename-mysql",
      "jdbc.driver.class": "com.mysql.jdbc.Driver",
      "jdbc.connection.uri": "jdbc:mysql://$[env:AEM_PROXY_HOST;default=proxy.tunnel]:30001/sqldatasourcename"
   ```


    
4. Select **[!UICONTROL Save]** to save the configuration.

Now, you can use the configured relational database with your Form Data Model (FDM). 

<!-- ## Configure [!DNL Experience Manager] user profile {#configure-aem-user-profile}

You can configure [!DNL Experience Manager] user profile using User Profile Connector configuration in [!DNL Experience Manager] Web Console. Do the following:

1. Go to [!DNL Experience Manager] web console at `https://[server]:[port]/system/console/configMgr`.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and select to open the configuration in edit mode.
1. In the User Profile Connector Configuration dialog, you can add, remove, or update user profile properties. The specified properties are available for use in form data model (FDM). Use the following format to specify user profile properties:

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Examples:

    * `name=profile/phoneNumber,type=string`
    * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The **&#42;** in the above example denotes all nodes under the `profile/empLocation/` node in [!DNL Experience Manager] user profile in CRXDE structure. It means that the Form Data Model (FDM) can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. However, the nodes that contain the specified property must follow a consistent structure.

1. Select **[!UICONTROL Save]** to save the configuration. -->

## Configurar pasta para configurações do serviço em nuvem {#cloud-folder}

A configuração da pasta de serviços em nuvem é necessária para configurar serviços em nuvem para serviços RESTful, SOAP e OData.

Todas as configurações do serviço de nuvem em [!DNL Experience Manager] são consolidadas na pasta `/conf` no repositório [!DNL Experience Manager]. Por padrão, a pasta `conf` contém a pasta `global`, na qual você pode criar configurações do serviço de nuvem. No entanto, você deve habilitá-lo manualmente para configurações de nuvem. Você também pode criar pastas adicionais no `conf` para criar e organizar as configurações do serviço de nuvem.

Para definir a pasta de configurações do serviço de nuvem:

1. Vá para **[!UICONTROL Ferramentas > Geral > Navegador de Configuração]**.
   * Consulte a documentação do [Navegador de Configuração](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/configurations.html) para obter mais informações.
1. Faça o seguinte para habilitar a pasta global para configurações de nuvem ou ignore esta etapa para criar e configurar outra pasta para configurações de serviço de nuvem.

   1. No **[!UICONTROL Navegador de Configuração]**, selecione a pasta `global` e selecione **[!UICONTROL Propriedades]**.

   1. Na caixa de diálogo **[!UICONTROL Propriedades da Configuração]**, habilite as **[!UICONTROL Configurações de Nuvem]**.

   1. Selecione **[!UICONTROL Salvar e fechar]** para salvar a configuração e sair da caixa de diálogo.

1. No **[!UICONTROL Navegador de Configuração]**, selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo **[!UICONTROL Criar Configuração]**, especifique um título para a pasta e habilite as **[!UICONTROL Configurações de Nuvem]**.
1. Selecione **[!UICONTROL Criar]** para criar a pasta habilitada para configurações do serviço de nuvem.

## Configurar serviços Web RESTful {#configure-restful-web-services}

Os serviços Web RESTful podem ser descritos usando [especificações do Swagger](https://swagger.io/specification/v2/) no formato JSON ou YAML em um arquivo de definição [!DNL Swagger] ou um Ponto de Extremidade de Serviço.

>[!NOTE]
> Para configurar o serviço Web RESTful no as a Cloud Service [!DNL Experience Manager], verifique se você tem o arquivo [!DNL Swagger] ([Swagger Versão 2.0](https://swagger.io/specification/v2/)) ou o arquivo [!DNL Swagger] ([Swagger Versão 3.0](https://swagger.io/specification/v3/)) no seu sistema de arquivos ou na URL onde o arquivo está hospedado.

### Configurar serviços RESTful para a especificação de API aberta versão 2.0 {#configure-restful-services-open-api-2.0}

1. Acesse **[!UICONTROL Ferramentas > Serviços da nuvem > Fontes de dados]**. Selecione para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do serviço de nuvem.

1. Selecione **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente de Criação de Configuração de Source de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço RESTful]** no menu suspenso **[!UICONTROL Tipo de serviço]**, opcionalmente, procure e selecione uma imagem em miniatura para a configuração e selecione **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço RESTful:

   * Selecione uma URL ou um Arquivo no menu suspenso [!UICONTROL Swagger Source] e especifique o [!DNL Swagger URL] para o arquivo de definição [!DNL &#x200B; Swagger] ou carregue o arquivo [!DNL Swagger] do seu sistema de arquivos local.
   * Com base na entrada do Source [!DNL &#x200B; Swagger]., os seguintes campos são pré-preenchidos com valores:

      * Esquema: os protocolos de transferência usados pela API REST. O número de tipos de esquema exibidos na lista suspensa depende dos esquemas definidos na origem [!DNL Swagger].
      * Host: o nome do domínio ou endereço IP do host que serve a API REST. É um campo obrigatório.
      * Caminho base: o prefixo do URL para todos os caminhos da API. É um campo opcional.\
        Se necessário, edite os valores pré-preenchidos nesses campos.

   * Selecione o tipo de autenticação — None, OAuth2.0([Código de Autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais do Cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticação Básica, Chave de API ou Autenticação Personalizada — para acessar o serviço RESTful e fornecer os detalhes correspondentes para autenticação.

   Se você selecionar **[!UICONTROL Chave de API]** como o tipo de autenticação, especifique o valor da chave de API. A chave de API pode ser enviada como um cabeçalho de solicitação ou como um parâmetro de consulta. Selecione uma dessas opções na lista suspensa **[!UICONTROL Local]** e especifique o nome do cabeçalho ou do parâmetro de consulta no campo **[!UICONTROL Nome do Parâmetro]**.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Selecione **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço RESTful.

### Configurar serviços RESTful para a especificação de API aberta versão 3.0 {#configure-restful-services-open-api-3.0}

1. Acesse **[!UICONTROL Ferramentas > Serviços da nuvem > Fontes de dados]**. Selecione para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do serviço de nuvem.

1. Selecione **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente de Criação de Configuração de Source de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço RESTful]** no menu suspenso **[!UICONTROL Tipo de serviço]**, opcionalmente, procure e selecione uma imagem em miniatura para a configuração e selecione **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço RESTful:

   * Selecione uma URL ou um Arquivo no menu suspenso [!UICONTROL Swagger Source] e especifique o [!DNL Swagger 3.0 URL] para o arquivo de definição [!DNL &#x200B; Swagger] ou carregue o arquivo [!DNL Swagger] do seu sistema de arquivos local.
   * Com base na entrada do Source [!DNL &#x200B; Swagger], as informações de conexão com o servidor de destino são exibidas.
   * Selecione o tipo de autenticação — None, OAuth2.0([Código de Autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais do Cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticação Básica, Chave de API ou Autenticação Personalizada — para acessar o serviço RESTful e fornecer os detalhes correspondentes para autenticação.

   Se você selecionar **[!UICONTROL Chave de API]** como o tipo de autenticação, especifique o valor da chave de API. A chave de API pode ser enviada como um cabeçalho de solicitação ou como um parâmetro de consulta. Selecione uma dessas opções na lista suspensa **[!UICONTROL Local]** e especifique o nome do cabeçalho ou do parâmetro de consulta no campo **[!UICONTROL Nome do Parâmetro]**.

   <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Selecione **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço RESTful.

Algumas das operações não suportadas pela Especificação da API aberta dos serviços RESTful versão 3.0 são:

* Retornos de chamada
* um/qualquer um
* Referência remota
* Links
* Diferentes corpos de solicitação para diferentes tipos MIME para uma única operação

Consulte a [Especificação da OpenAPI 3.0](https://swagger.io/specification/v3/) para obter informações detalhadas.

### Configurar serviços RESTful usando Ponto de Extremidade de Serviço {#configure-restful-services-service-endpoint}

<span class="preview"> O recurso de Ponto de Extremidade de Serviço está no Programa de Primeiros Adotores e se aplica somente aos Componentes Principais. Você pode escrever para aem-forms-ea@adobe.com a partir da sua ID de email oficial para ingressar no programa de adoção antecipada e solicitar acesso ao recurso. </span>

1. Acesse **[!UICONTROL Ferramentas > Serviços da nuvem > Fontes de dados]**. Selecione para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do serviço de nuvem.

1. Selecione **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente de Criação de Configuração de Source de Dados]**.

1. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço RESTful]** no menu suspenso **[!UICONTROL Tipo de serviço]**, opcionalmente, procure e selecione uma imagem em miniatura para a configuração e selecione **[!UICONTROL Próximo]**.

1. Na próxima página, selecione **[!UICONTROL Ponto de Extremidade de Serviço]** na lista suspensa **[!UICONTROL Serviço RESTful]**.

   ![Ponto de Extremidade de Serviço](/help/forms/assets/select-service-endpoint.png)

1. Especifique a **[!UICONTROL URL do Ponto de Extremidade de Serviço]**.

   >[!NOTE]
   > Por padrão, o Tipo de método é POST.
1. Selecione um dos Tipos de conteúdo que você deseja escolher na lista suspensa. Os tipos de conteúdo são Dados de formulário de várias partes, JSON e Codificado por URL (Par de valores chave).
1. Agora você pode selecionar qualquer um dos Tipos de autenticação, como OAuth 2.0, Autenticação básica, Chave de API, Autenticação personalizada, na lista suspensa.
   ![Tipo de autenticação de Ponto de Extremidade de Serviço](/help/forms/assets/service-endpoint-authtype.png)
1. Clique em Criar.

### Configuração do cliente HTTP do Form Data Model (FDM) para otimizar o desempenho {#fdm-http-client-configuration}

O [!DNL Experience Manager Forms] forma um modelo de dados ao integrar com serviços Web RESTful como fonte de dados inclui configurações de cliente HTTP para otimização de desempenho.

Defina as seguintes propriedades da configuração do **[!UICONTROL Configuração do Cliente HTTP do Modelo de Dados de Formulário para a fonte de dados REST]** para especificar a expressão regular:

* Use a propriedade `http.connection.max.per.route` para definir o número máximo de conexões permitidas entre o modelo de dados de formulário (FDM) e os serviços Web RESTful. O valor padrão é de 20 conexões.

* Use a propriedade `http.connection.max` para especificar o número máximo de conexões permitidas para cada rota. O valor padrão é 40 conexões.

* Use a propriedade `http.connection.keep.alive.duration` para especificar a duração, para a qual uma conexão HTTP persistente é mantida ativa. O valor padrão é de 15 segundos.

* Use a propriedade `http.connection.timeout` para especificar a duração pela qual o servidor [!DNL Experience Manager Forms] aguarda o estabelecimento de uma conexão. O valor padrão é de 10 segundos.

* Use a propriedade `http.socket.timeout` para especificar o período máximo de inatividade entre dois pacotes de dados. O valor padrão é de 30 segundos.

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

1. Selecione **[!UICONTROL Configuração do Cliente HTTP do Modelo de Dados de Formulário para a fonte de dados REST]**.

1. Na caixa de diálogo [!UICONTROL Configuração do Cliente HTTP do Modelo de Dados de Formulário para a fonte de dados REST]:

   * Especifique o número máximo de conexões permitidas entre o FDM (modelo de dados de formulário) e os serviços Web RESTful no campo **[!UICONTROL Limite de conexão no total]**. O valor padrão é de 20 conexões.

   * Especifique o número máximo de conexões permitidas para cada rota no campo **[!UICONTROL Limite de conexão por rota]**. O valor padrão é duas conexões.

   * Especifique a duração, para a qual uma conexão HTTP persistente é mantida ativa, no campo **[!UICONTROL Keep alive]**. O valor padrão é de 15 segundos.

   * No campo [!DNL Experience Manager Forms]Tempo limite de conexão **[!UICONTROL , especifique a duração pela qual o servidor]** aguarda o estabelecimento de uma conexão. O valor padrão é de 10 segundos.

   * Especifique o período máximo de inatividade entre dois pacotes de dados no campo **[!UICONTROL Tempo limite do soquete]**. O valor padrão é de 30 segundos.

## Configurar os serviços Web do SOAP {#configure-soap-web-services}

Os serviços Web baseados em SOAP são descritos usando as [especificações WSDL (Web Services Description Language)](https://www.w3.org/TR/wsdl). [!DNL Experience Manager Forms] não dá suporte ao modelo WSDL de estilo RPC.

Para configurar o serviço da Web com base em SOAP no as a Cloud Service [!DNL Experience Manager], verifique se você tem a URL WSDL para o serviço da Web e faça o seguinte:

1. Acesse **[!UICONTROL Ferramentas > Serviços da nuvem > Fontes de dados]**. Selecione para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](configure-data-sources.md#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do serviço de nuvem.

1. Selecione **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente de Criação de Configuração de Source de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL SOAP Web Service]** no menu suspenso **[!UICONTROL Tipo de Serviço]**, opcionalmente, procure e selecione uma imagem em miniatura para a configuração e selecione **[!UICONTROL Próximo]**.
1. Especifique o seguinte para o serviço Web SOAP:

   * URL WSDL do serviço Web.
   * Ponto de Extremidade de Serviço. Especifique um valor neste campo para substituir o ponto final de serviço mencionado no WSDL.
   * Selecione o tipo de autenticação — None, OAuth2.0([Código de Autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais do Cliente](https://oauth.net/2/grant-types/client-credentials/)), Autenticação Básica ou Autenticação Personalizada — para acessar o serviço SOAP e fornecer os detalhes de autenticação de acordo.

     <!--If you select **[!UICONTROL X509 Token]** as the Authentication type, configure the X509 certificate. For more information, see [Set up certificates](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).-->
     <!--Specify the KeyStore alias for the X509 certificate in the **[!UICONTROL Key Alias]** field. Specify the time, in seconds, until the authentication request remains valid, in the **[!UICONTROL Time To Live]** field. Optionally, select to sign the message body or timestamp header or both.-->

     <!--If you select **[!UICONTROL Mutual Authentication]** as the authentication type, see [Certificate-based mutual authentication for RESTful and SOAP web services](#mutual-authentication).-->

1. Selecione **[!UICONTROL Criar]** para criar a configuração de nuvem do serviço Web SOAP.

### Ativar o uso de instruções de importação no WSDL de serviços Web do SOAP {#enable-import-statements}

Você pode especificar uma expressão regular que serve como filtro para URLs absolutos que são permitidos como instruções de importação no WSDL dos serviços Web do SOAP. Por padrão, não há nenhum valor nesse campo. Como resultado, [!DNL Experience Manager] bloqueia todas as instruções de importação disponíveis no WSDL. Se você especificar `.*` como o valor neste campo, [!DNL Experience Manager] permitirá todas as instruções de importação.

Defina a propriedade `importAllowlistPattern` da configuração **[!UICONTROL Incluo na lista de permissões de Importação de Serviços Web da SOAP do Modelo de Dados de Formulário]** para especificar a expressão regular. O seguinte arquivo JSON exibe uma amostra:

```json
{
  "importAllowlistPattern": ".*"
}
```

Para definir valores de uma configuração, [Gere Configurações OSGi usando o AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [implante a configuração](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) na sua instância do Cloud Service.

## Configurar serviços OData {#config-odata}

Um serviço OData é identificado por sua URL raiz de serviço. Para configurar um serviço OData no as a Cloud Service [!DNL Experience Manager], certifique-se de que possui uma URL raiz de serviço para o serviço e faça o seguinte:

>[!NOTE]
>
> O FDM (Modelo de Dados de Formulário) dá suporte à [OData versão 4](https://www.odata.org/documentation/).
>Para obter um guia passo a passo para configurar o [!DNL Microsoft®® Dynamics 365], online ou no local, consulte [[!DNL Microsoft® Dynamics] Configuração OData](ms-dynamics-odata-configuration.md).

1. Acesse **[!UICONTROL Ferramentas > Serviços da nuvem > Fontes de dados]**. Selecione para selecionar a pasta na qual deseja criar uma configuração de nuvem.

   Consulte [Configurar pasta para configurações do serviço de nuvem](#cloud-folder) para obter informações sobre como criar e configurar uma pasta para configurações do serviço de nuvem.

1. Selecione **[!UICONTROL Criar]** para abrir o **[!UICONTROL Assistente de Criação de Configuração de Source de Dados]**. Especifique um nome e, opcionalmente, um título para a configuração, selecione **[!UICONTROL Serviço OData]** na lista suspensa **[!UICONTROL Tipo de Serviço]**, opcionalmente, procure e selecione uma imagem em miniatura para a configuração e selecione **[!UICONTROL Próximo]**.
1. Especifique os seguintes detalhes para o serviço OData:

   * URL da Raiz de Serviço do serviço OData a ser configurado.
   * Selecione o tipo de autenticação — None, OAuth2.0([Código de Autorização](https://oauth.net/2/grant-types/authorization-code/), [Credenciais do Cliente](https://oauth.net/2/grant-types/client-credentials/)), Basic Authentication, API Key ou Custom Authentication — para acessar o serviço OData e fornecer os detalhes de autenticação de acordo.

   Se você selecionar **[!UICONTROL Chave de API]** como o tipo de autenticação, especifique o valor da chave de API. A chave de API pode ser enviada como um cabeçalho de solicitação ou como um parâmetro de consulta. Selecione uma dessas opções na lista suspensa **[!UICONTROL Local]** e especifique o nome do cabeçalho ou do parâmetro de consulta no campo **[!UICONTROL Nome do Parâmetro]**.

   >[!NOTE]
   >
   >Selecione o tipo de autenticação OAuth 2.0 para se conectar com os serviços do [!DNL Microsoft®® Dynamics] usando o ponto de extremidade OData como raiz de serviço.

1. Selecione **[!UICONTROL Criar]** para criar a configuração de nuvem para o serviço OData.

<!--
## Configure Microsoft&reg; SharePoint List {#config-sharepoint-list}

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

To save data in a tabular form use, Microsoft&reg; SharePoint List. To configure a Microsoft SharePoint List in [!DNL Experience Manager] as a Cloud Service, do the following:

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft&reg; SharePoint]**.   
1. Select a **Configuration Container**. The configuration is stored in the selected Configuration Container. 
1. Click **[!UICONTROL Create]** > **[!UICONTROL SharePoint List]** from the drop-down list. The SharePoint configuration wizard appears.  
1. Specify the **[!UICONTROL Title]**, **[!UICONTROL Client ID]**, **[!UICONTROL Client Secret]** and **[!UICONTROL OAuth URL]**. For information on how to retrieve Client ID, Client Secret, Tenant ID for OAuth URL, see [Microsoft&reg; Documentation](https://learn.microsoft.com/en-us/graph/auth-register-app-v2).
    * You can retrieve the `Client ID` and `Client Secret` of your app from the Microsoft&reg; Azure portal.
    * In the Microsoft&reg; Azure portal, add the Redirect URI as `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`. Replace `[author-instance]` with the URL of your Author instance.
    * Add the API permissions `offline_access` and `Sites.Manage.All` in the **Microsoft&reg; Graph** tab to provide read/write permissions. Add `AllSites.Manage` permission in the **Sharepoint** tab to interact remotely with SharePoint data.
    * Use OAuth URL: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Replace `<tenant-id>` with the `tenant-id` of your app from the Microsoft&reg; Azure portal.

      >[!NOTE]
      >
      > The **client secret** field is mandatory or optional depends upon your Azure Active Directory application configuration. If your application is configured to use a client secret, it is mandatory to provide the client secret.

1. Click **[!UICONTROL Connect]**. On a successful connection, the `Connection Successful` message appears.
1. Select **[!UICONTROL SharePoint Site]** and **[!UICONTROL SharePoint List]** from the drop-down list.
1. Select **[!UICONTROL Create]** to create the cloud configuration for the Microsoft&reg; SharePointList.

-->

<!--## Certificate-based mutual authentication for RESTful and SOAP web services {#mutual-authentication}

When you enable mutual authentication for form data model (FDM), both the data source and [!DNL Experience Manager] Server running Form Data Model (FDM) authenticate each other's identity before sharing any data. You can use mutual authentication for REST and SOAP-based connections (data sources). To configure mutual authentication for a Form Data Model (FDM) on your [!DNL Experience Manager Forms] environment:

1. Upload the private key (certificate) to [!DNL Experience Manager Forms] server. To upload the private key:
   1. Log in to your [!DNL Experience Manager Forms] server as an administrator.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Select the `fd-cloudservice` user and select **[!UICONTROL Properties]**.
   1. Open the **[!UICONTROL Keystore]** tab, expand the **[!UICONTROL Add Private Key from KeyStore file]** option, upload the KeyStore File, specify the aliases, passwords, and select **[!UICONTROL Submit]**. The Certificate is uploaded.  The private key alias is mentioned in the certificate and set while creating the certificate.
1. Upload trust certificate to Global Trust Store. To upload the certificate:
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Trust Store]**.
   1. Expand the **[!UICONTROL Add Certificate from CER file]** option, select **[!UICONTROL Select Certificate File]**, upload the certificate, and select **[!UICONTROL Submit]**.
1. Configure [SOAP](#configure-soap-web-services) or [RESTful](#configure-restful-web-services) web services as the data source and select **[!UICONTROL Mutual authentication]** as the authentication type. If you configure multiple self-signed certificates for `fd-cloudservice` user, specify the Key Alias name for the certificate.-->

## Próximas etapas {#next-steps}

Você configurou as fontes de dados. Em seguida, você poderá criar um Modelo de dados de formulário (FDM) ou, se já tiver criado um Modelo de dados de formulário (FDM) sem uma fonte de dados, poderá associá-lo às fontes de dados configuradas. Consulte [Criar modelo de dados de formulário](create-form-data-models.md) para obter detalhes.

<!--

>[!MORELIKETHIS]
>
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)
>*  [Add Forms Portal to an AEM Sites page](/help/forms/configure-forms-portal.md)

-->