---
title: Suporte OAuth2 para o serviço de email
description: Suporte do Oauth2 para o serviço de email no Adobe Experience Manager as a Cloud Service
exl-id: 93e7db8b-a8bf-4cc7-b7f0-cda481916ae9
source-git-commit: cf2582965249187fae943ce5ef37821388116905
workflow-type: ht
source-wordcount: '674'
ht-degree: 100%

---

# Suporte OAuth2 para o serviço de email {#oauth2-support-for-the-mail-service}

O AEM as a Cloud Service oferece suporte do OAuth2 para seu serviço de email integrado, a fim de permitir que as organizações cumpram com os requisitos de segurança de emails.

Você pode configurar o OAuth para vários provedores de email. Abaixo estão as instruções passo a passo para configurar o Serviço de email do AEM para autenticar via OAuth2 com o Microsoft Office 365 Outlook. Outros fornecedores podem ser configurados de maneira semelhante.

Para obter mais informações sobre o Serviço de email do AEM as a Cloud Service, consulte [Envio de email](/help/implementing/developing/introduction/development-guidelines.md#sending-email).

## Microsoft Outlook {#microsoft-outlook}

1. Acesse [https://portal.azure.com/](https://portal.azure.com/) e faça logon.
1. Pesquise por **Azure Active Directory** na barra de pesquisa e clique no resultado. Como alternativa, você pode navegar diretamente para [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Clique em **Registro do aplicativo** - **Novo registro**

   ![](assets/oauth-outlook1.png)

1. Preencha as informações de acordo com suas necessidades e clique em **Registrar**
1. Acesse o aplicativo recém-criado e selecione **Permissões de API**
1. Vá em **Adicionar permissão** - **Permissão de gráfico** - **Permissões delegadas**
1. Selecione as permissões abaixo para seu aplicativo e clique em **Adicionar permissão**:
   * `https://graph.microsoft.com/SMTP.Send`
   * `https://graph.microsoft.com/Mail.Read`
   * `https://graph.microsoft.com/Mail.Send`
   * `https://graph.microsoft.com/User.Read`
   * `openid`
   * `offline_access`
   * `email`
   * `profile`
1. Vá em **Autenticação** - **Adicionar uma plataforma** - **Web** e na seção **Redirecionar URLs**, adicione os URLs abaixo - um com e um sem a barra:
   * `http://localhost/`
   * `http://localhost`
1. Pressione **Configurar** depois de adicionar cada URL e defina as configurações de acordo com seus requisitos
1. Em seguida, vá em **Certificados e segredos**, clique em **Novo segredo de cliente** e siga as etapas na tela para criar um segredo. Anote este segredo para uso posterior
1. Pressione **Visão geral** no painel esquerdo e copie os valores de **ID do aplicativo (cliente)** e **ID do diretório (locatário)** para uso posterior

Para recapitular, você precisará das seguintes informações para configurar o OAuth2 para o serviço de email no lado do AEM:

* O URL de autenticação, que será construído com a ID do locatário. Ele terá este formato: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* O URL do token, que será construído com a ID do locatário. Ele terá este formato: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* O URL de atualização, que será construído com a ID do locatário. Ele terá este formato: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* A ID do cliente
* O segredo do cliente

### Geração do token de atualização {#generating-the-refresh-token}

Em seguida, você precisa gerar o token de atualização, que fará parte da configuração OSGi em uma etapa subsequente.

Você pode fazer isso seguindo estas etapas:

1. Abra o seguinte URL no navegador após substituir `clientID` e `tenantID` com os valores específicos da sua conta: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize?client_id=<clientId>&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https://graph.microsoft.com/SMTP.Send https://graph.microsoft.com/Mail.Read https://graph.microsoft.com/Mail.Send https://graph.microsoft.com/User.Read email openid profile offline_access&state=12345`
1. Permitir quando solicitado
1. O URL será redirecionado para um novo local, construído neste formato: `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. Copie o valor de `<code>` no exemplo acima
1. Use o seguinte comando cURL para obter o refreshToken. É necessário substituir a tenantID, clientID e clientSecret pelos valores da sua conta, bem como o valor de `<code>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_5vR5dAQAAALDXP9gOAAAAwIpkkQEAAACT2T_YDgAAAA' \
   --data-urlencode 'client_id=<clientID>' \
   --data-urlencode 'scope=https://graph.microsoft.com/SMTP.Send https://graph.microsoft.com/Mail.Read https://graph.microsoft.com/Mail.Send https://graph.microsoft.com/User.Read email openid profile offline_access' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=authorization_code' \
   --data-urlencode 'client_secret=<clientSecret>' \
   --data-urlencode 'code=<code>'
   ```

1. Anote o refreshToken e o accessToken.

### Validação dos tokens {#validating-the-tokens}

Antes de continuar a configurar o OAuth no lado do AEM, valide o accessToken e o refreshToken com o procedimento abaixo:

1. Gere o accessToken usando o refreshToken produzido no procedimento anterior. Você pode fazer isso com o seguinte curl, substituindo os valores de `<client_id>`,`<client_secret>` e `<refreshToken>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenetId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_IezHLAQAAAPeNSdgOAAAA' \
   --data-urlencode 'client_id=<client_id>' \
   --data-urlencode 'scope=https://graph.microsoft.com/SMTP.Send https://graph.microsoft.com/Mail.Read https://graph.microsoft.com/Mail.Send https://graph.microsoft.com/User.Read email openid profile offline_access' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=refresh_token' \
   --data-urlencode 'client_secret=<client_secret>' \
   --data-urlencode 'refresh_token=<refreshToken>'
   ```

1. Envie um email usando o accessToken para ver se está funcionando corretamente.

>[!NOTE]
>
> Você pode obter a coleção da API Postman [deste local](https://docs.microsoft.com/pt-br/azure/active-directory/develop/v2-oauth2-auth-code-flow).

### Integração com o AEM as a Cloud Service {#integration-with-aem-as-a-cloud-service}

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
       authCodeRedirectUrl: "http://localhost",
       refreshUrl: "<Refresh token Url>",
       refreshToken: "$[secret:SECRET_SMTP_OAUTH_REFRESH_TOKEN]"
   }
   ```

1. Preencha o `authUrl`, `tokenUrl` e `refreshURL` construindo-os conforme descrito na seção anterior.
1. Adicione os seguintes escopos à configuração:
   * `https://graph.microsoft.com/SMTP.Send`
   * `https://graph.microsoft.com/Mail.Read`
   * `https://graph.microsoft.com/Mail.Send`
   * `https://graph.microsoft.com/User.Read`
   * `openid`
   * `offline_access`
   * `email`
   * `profile`
1. Crie um arquivo de propriedade OSGI chamado `called com.day.cq.mailer.DefaultMailService.cfg.json`
em 
`/apps/<my-project>/osgiconfig/config` com a seguinte sintaxe:

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

1. Para o Outlook, o valor de configuração do `smtp.host` é `smtp.office365.com`
1. No tempo de execução, forneça os segredos `refreshToken values` e `clientSecret` usando a API de variáveis do Cloud Manager, conforme descrito [aqui](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api). Os valores das variáveis `SECRET_SMTP_OAUTH_REFRESH_TOKEN` e `SECRET_SMTP_OAUTH_CLIENT_SECRET` devem ser definidos.

### Resolução de problemas {#troubleshooting}

Se o serviço de email não estiver funcionando corretamente, você precisará, na maioria dos casos, gerar novamente a variável `refreshToken` conforme descrito acima, fornecendo o novo valor pela API do Cloud Manager. Levará alguns minutos para o novo valor ser implantado.