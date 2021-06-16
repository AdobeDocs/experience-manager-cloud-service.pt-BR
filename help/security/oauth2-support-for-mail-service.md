---
title: Suporte OAuth2 para o serviço de email
description: Suporte Oauth2 para o serviço de email no Adobe Experience Manager as a Cloud Service
source-git-commit: 67c4aabea838c1430e43f5ebaa8a52ec55362936
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---


# Suporte OAuth2 para o serviço de email {#oauth2-support-for-the-mail-service}

O AEM as a Cloud Service oferece suporte ao OAuth2 para seu serviço de email integrado, a fim de permitir que as organizações adiram para proteger os requisitos de email.

Você pode configurar o OAuth para vários provedores de email. Abaixo estão as instruções passo a passo para configurar o Serviço de Correio do AEM para autenticar via OAuth2 com o Microsoft Office 365 Outlook. Outros fornecedores podem ser configurados de maneira semelhante.

Para obter mais informações sobre o AEM como um Cloud Service Mail Service, consulte [Enviar Email](/help/implementing/developing/introduction/development-guidelines.md#sending-email).

## Microsoft Outlook {#microsoft-outlook}

1. Vá para [https://portal.azure.com/](https://portal.azure.com/) e faça logon.
1. Procure por **Azure Ative Diretory** na barra de pesquisa e clique no resultado. Como alternativa, você pode navegar diretamente para [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Clique em **Registro do Aplicativo** - **Novo Registro**

   ![](assets/oauth-outlook1.png)

1. Preencha as informações de acordo com seus requisitos e clique em **Register**
1. Vá para o aplicativo recém-criado e selecione **Permissões da API**
1. Vá para **Adicionar permissão** - **Permissão de gráfico** - **Permissões delegadas**
1. Selecione as permissões abaixo para seu aplicativo e clique em **Adicionar permissão**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Vá para **Authentication** - **Add a platform** - **Web** e, na seção **Redirect Urls**, adicione os URLs abaixo - um com e um sem uma barra:
   * `http://localhost/`
   * `http://localhost`
1. Pressione **Configurar** depois de adicionar cada URL e definir suas configurações de acordo com seus requisitos
1. Em seguida, vá para **Certificados e Segredos**, clique em **Novo segredo de cliente** e siga as etapas na tela para criar um segredo. Anote este segredo para uso posterior
1. Pressione **Visão geral** no painel esquerdo e copie os valores para **ID de aplicativo (cliente)** e **ID de diretório (locatário)** para uso posterior

Para recapitular, você precisará das seguintes informações para configurar o OAuth2 para o serviço de Email no lado do AEM:

* O URL de autenticação, que será construído com a ID do locatário. Ele terá este formulário: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* O URL do token, que será construído com a ID do locatário. Ele terá este formulário: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* O URL de atualização, que será construído com a ID do locatário. Ele terá este formulário: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* A ID do cliente
* O Segredo Do Cliente

### Gerar o token de atualização {#generating-the-refresh-token}

Em seguida, você precisa gerar o token de atualização, que fará parte da configuração do OSGi em uma etapa subsequente.

Você pode fazer isso seguindo estas etapas:

1. Abra o seguinte URL no navegador depois de substituir `clientID` e `tenantID` pelos valores específicos da sua conta: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize?client_id=<clientId>&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20EWS.AccessAsUser.All%20https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office365.com%2FMail.Read%20https%3A%2F%2Foutlook.office365.com%2FMail.Send%20openid%20offline_access&state=12345`
1. Permitir permissão quando solicitado
1. O URL será redirecionado para um novo local, construído neste formato: `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. Copie o valor de `<code>` no exemplo acima
1. Use o seguinte comando cURL para obter o refreshToken. É necessário substituir o tenantID, clientID e clientSecret pelos valores de sua conta, bem como o valor de `<code>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_5vR5dAQAAALDXP9gOAAAAwIpkkQEAAACT2T_YDgAAAA' \
   --data-urlencode 'client_id=<clientID>' \
   --data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=authorization_code' \
   --data-urlencode 'client_secret=<clientSecret>' \
   --data-urlencode 'code=<code>'
   ```

1. Anote o refreshToken e o accessToken.

### Validando os tokens {#validating-the-tokens}

Antes de continuar a configurar o OAuth no lado do AEM, valide o accessToken e o refreshToken com o procedimento abaixo:

1. Gere o accessToken usando o refreshToken produzido no procedimento anterior. Você pode fazer isso com o seguinte curl, substituindo os valores para `<client_id>`,`<client_secret>` e `<refreshToken>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenetId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_IezHLAQAAAPeNSdgOAAAA' \
   --data-urlencode 'client_id=<client_id>' \
   --data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=refresh_token' \
   --data-urlencode 'client_secret=<client_secret>' \
   --data-urlencode 'refresh_token=<refreshToken>'
   ```

1. Envie um email usando o accessToken para ver se o está funcionando corretamente.

>[!NOTE]
>
> Você pode obter a coleção da API Postman de [this location](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow).

### Integração com AEM como Cloud Service {#integration-with-aem-as-a-cloud-service}

1. Crie um arquivo de propriedade OSGI chamado `com.day.cq.mailer.oauth.impl.OAuthConfigurationProviderImpl.cfg.json` em `/apps/<my-project>/osgiconfig/config` com a seguinte sintaxe:

   ```
   {
       authUrl: "<Authorization Url>",
       tokenUrl: "<Token Url>",
       clientId: "<clientID>",
       clientSecret: "$[secret:SECRET_SMTP_OAUTH_CLIENT_SECRET]",
       scopes: [
          "scope1",
          "scope2"
       ],
       refreshUrl: "<Refresh token Url>",
       refreshToken: "$[secret:SECRET_SMTP_OAUTH_REFRESH_TOKEN]"
   }
   ```

1. Preencha os campos `authUrl`, `tokenUrl` e `refreshURL` construindo-os conforme descrito na seção anterior.
1. Adicione os seguintes escopos à configuração:
   * `openid`
   * `offline_access`
   * `https://outlook.office365.com/Mail.Send`
   * `https://outlook.office365.com/Mail.Read`
   * `https://outlook.office365.com/SMTP.Send`
1. Criar um arquivo de propriedade OSGI `called com.day.cq.mailer.impl.DefaultMailService.cfg.json`
under 
`/apps/<my-project>/osgiconfig/config`  com a seguinte sintaxe:

   ```
   {
    "smtp.host": "<smtp hostname>"
    "smtp.user": "<user account that logged into get the oauth tokens>",
    "smtp.password": "value not used",
    "smtp.port": 587,
    "from.address": "<from address used for sending>"
    "smtp.ssl": false,
    "smtp.starttls": true,
    "smtp.requiretls": true,
    "debug.email": false,
    "oauth.flow": true
   }
   ```

1. Para o outlook, o valor de configuração `smtp.host` é `smtp.office365.com`
1. No tempo de execução, transmita os segredos `refreshToken values` e `clientSecret` usando a API de variáveis do Cloud Manager, conforme descrito [aqui](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api). Os valores para as variáveis `SECRET_SMTP_OAUTH_REFRESH_TOKEN` e `SECRET_SMTP_OAUTH_CLIENT_SECRET` devem ser definidos.

### Resolução de problemas {#troubleshooting}

Se o serviço de email não estiver funcionando corretamente, você precisará, na maioria dos casos, gerar novamente o `refreshToken` conforme descrito acima, enviando o novo valor pela API do Cloud Manager. Levará alguns minutos para o novo valor ser implantado.
