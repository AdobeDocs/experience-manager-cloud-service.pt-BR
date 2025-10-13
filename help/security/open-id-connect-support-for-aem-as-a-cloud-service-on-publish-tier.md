---
title: Suporte ao Open ID Connect para AEM as a Cloud Service no nível de publicação
description: Saiba como configurar o Open ID Connect (OIDC) para o AEM as a Cloud Service no nível de publicação
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: eb03c8941f848ff10c38a4880c8fe85387cc441f
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 0%

---

# Suporte ao Open ID Connect para AEM as a Cloud Service no nível de publicação {#open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier}

## Introdução {#introduction}

À medida que as organizações modernizam suas experiências digitais, o gerenciamento de identidades seguro e escalável se torna um requisito fundamental. O Adobe Experience Manager (AEM) Cloud Service agora é compatível com o OpenID Connect (OIDC) no nível de publicação, permitindo integração contínua e baseada em padrões com os principais Provedores de identidade (IdPs), como Entra ID (Azure AD), Google, Okta, Auth0, Identidade de ping, ForgeRock e IDC compatíveis com os IDPs.

O OIDC é uma camada de identidade sobre o protocolo OAuth 2.0 que permite uma autenticação de usuário robusta, mantendo a simplicidade para os desenvolvedores. Ele é amplamente adotado para cenários B2C (B2C), intranet e portais de parceiros, em que são necessários logon seguro de usuários e federações de identidade.

Até agora, os clientes do AEM eram responsáveis por implementar sua própria lógica de logon personalizada no nível de publicação, o que aumentou o tempo de desenvolvimento e introduziu desafios de manutenção e segurança de longo prazo. Com suporte nativo para o OIDC, o AEM Cloud Service remove essa carga fornecendo um mecanismo de autenticação seguro, extensível e com suporte da Adobe para usuários finais que acessam ambientes de publicação.

Esteja você fornecendo um site personalizado do consumidor ou um portal interno autenticado, o OIDC on Publish simplifica a federação de identidades e reduz os riscos por meio de um controle de identidades centralizado. Também ajuda as organizações a atender aos padrões modernos de conformidade e segurança sem sacrificar a agilidade.

## Configurar o AEM para autenticação OIDC {#configure-aem-oidc-authentication}

### Pré-requisitos {#prerequisits}

Presumimos que as seguintes informações estão disponíveis ou definidas:

1. Os caminhos do conteúdo a ser protegido no repositório do AEM
1. Um identificador para o IdP a ser configurado. Pode ser qualquer cadeia de caracteres

Informações da configuração do IdP:

1. A ID do cliente configurada no IdP
1. O segredo do cliente configurado no Idp. Se PKCE foi configurado no Idp, o segredo do cliente não está disponível. Não armazene o valor de texto simples no arquivo de configuração. Usar um segredo CM e referenciá-lo
1. Os escopos configurados no Idp. Pelo menos o escopo `openid` deve ser fornecido
1. Se o PKCE está habilitado no IdP
1. O `callbackUrl` é definido usando um dos caminhos configurados definidos no ponto 1 e adicionando o sufixo: `/j_security_check`
1. O `baseUrl` para acessar o arquivo `.well-known` padrão. Por exemplo, se a URL conhecida for: `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0/.well-known/openid-configuration` a `baseUrl` for: `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891`

### Visão geral dos arquivos de configuração {#overview-of-the-configuration-files}

Encontre abaixo uma lista de arquivos que precisam ser configurados:

1. **Conexão OIDC**: será usada pelo `OidcAuthenticationHandler` para autenticar os usuários ou por outros componentes para [autorizar o acesso a recursos protegidos pelo IdP usando OAuth](https://github.com/apache/sling-org-apache-sling-auth-oauth-client)
1. **Manipulador de autenticação OIDC**: esse é o manipulador de autenticação usado para autenticar usuários que acessam os caminhos configurados
1. **UserInfoProcessor**: esse componente processa as informações recebidas pelo IdP. Ele pode ser estendido pelos clientes para implementar uma lógica personalizada
1. [**Manipulador de Sincronização Padrão**](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html): este componente cria o usuário no repositório
1. [**ExternalLoginModule**](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html): este componente autentica o usuário no repositório local do oak.

O diagrama a seguir mostra como os elementos de configuração mencionados são vinculados. Observe que, como esses são `ServiceFactory` componentes, `~uniqueid` pode ser qualquer sequência de caracteres exclusiva e aleatória:

![Diagrama de configuração do OIDC](/help/security/assets/oidc-diagram.png)

### Configurar a conexão OIDC {#configure-the-oidc-connection}

Primeiro, precisamos configurar a conexão OIDC. É possível configurar várias conexões OIDC, e cada uma precisa ter um nome diferente.

1. Crie um novo arquivo `.cfg.json` que hospedará a configuração. Por exemplo, você pode usar `org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json` - o sufixo **azure** deve ser um identificador exclusivo para a conexão
1. Siga o formato de configuração no exemplo abaixo:

   ```
   {
    "name":"azure",
    "scopes":[
      "openid"
    ],
    "baseUrl":"<https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0>",
    "clientId":"5199fc45-8000-473e-ac63-989f1a78759f",
    "clientSecret":"xxxxxx"
   }
   ```

1. Configure as propriedades da seguinte maneira:
   * O **&quot;nome&quot;** pode ser definido pelo usuário
   * `baseUrl`, `clientid` e `clientSecret` são valores de configuração que vêm do IdP.
   * Os escopos devem conter pelo menos o valor `openid`.

### Configurar o manipulador de autenticação OIDC {#configure-oidc-authentication-handler}

Agora, configure o manipulador de autenticação OIDC. Várias conexões OIDC podem ser configuradas. Cada um tem de ter um nome diferente. Se eles compartilharem o mesmo [Provedor de Identidade Externo do OAK](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html), eles poderão compartilhar usuários.

1. Crie o arquivo de configuração. Neste exemplo, usaremos `org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json`. O sufixo `azure` deve ser um identificador exclusivo. Consulte um exemplo do arquivo de configuração abaixo:

   ```
   {
     "path":"/content/tests/us/en/test-7",
     "callbackUri":"http://localhost:14503/content/tests/us/en/test-7/j_security_check",
     "pkceEnabled":false,
     "defaultConnectionName":"azure"
     "idp": "azure-idp"
   }
   ```

1. Em seguida, configure suas propriedades da seguinte maneira:
   * `path`: o caminho a ser protegido
   * `callbackUri`: ao caminho a ser protegido, adicionando o sufixo: `/j_security_check`
   * `defaultConnectionName`: configurar com o mesmo nome definido para a conexão OIDC na etapa anterior+
   * `pkceEnabled`: `true` Chave de Prova para Troca de Código (PKCE) no fluxo de código de Autorização
   * `idp`: o nome do [Provedor de Identidade Externo do OAK](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html). Observe que um OAK IDP diferente não pode compartilhar usuários ou grupos

### Configurar SlingUserInfoProcessor

1. Crie o arquivo de configuração. Neste exemplo, usaremos `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessor~azure.cfg.json`. O sufixo `azure` deve ser um identificador exclusivo. Consulte um exemplo do arquivo de configuração abaixo:

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false
   }
   ```

1. Em seguida, configure suas propriedades da seguinte maneira:
   * `groupsInIdToken`: Definido como verdadeiro se os grupos forem enviados no Token de ID. Se o valor for falso, ou não for especificado, os grupos serão lidos do ponto de extremidade UserInfo.
   * `groupsClaimName`: O nome da declaração contém os grupos a serem sincronizados no AEM.
   * `connection`: configurar com o mesmo nome definido para a conexão OIDC na etapa anterior
   * `storeAccessToken`: verdadeiro se o token de acesso precisar ser armazenado no repositório. Por padrão, é falso. Defina como verdadeiro somente se o AEM precisar acessar recursos em nome do usuário armazenado em servidores externos protegidos pelo mesmo IdP.
   * `storeRefreshToken`: verdadeiro se o token de atualização deve ser armazenado no repositório. Por padrão, é falso. Defina-o como verdadeiro somente se o AEM precisar acessar recursos em nome do usuário armazenado em servidores externos protegidos pelo mesmo IdP e precisar atualizar o token do IdP.
Observe que o token de acesso e o token de atualização são armazenados criptografados com a chave mestre do AEM.


### Configurar o Manipulador de sincronização {#configure-the-synchronization-handler}

Pelo menos um Manipulador de sincronização deve ser configurado para sincronizar os usuários autenticados no oak. Para obter mais detalhes, consulte [esta](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html) página.

Crie um arquivo chamado `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json`. O sufixo **azure** deve ser um identificador exclusivo. Para obter mais informações sobre como configurar suas propriedades, consulte a [documentação sobre Sincronização de Usuários e Grupos do Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html). Encontre um exemplo de configuração abaixo:

```
{
  "user.expirationTime":"300s",
  "user.membershipExpTime":"300s",
  "user.propertyMapping":[
    "profile/familyName=profile/familyName",
    "profile/givenName=profile/givenName",
    "rep:fullname=cn",
    "profile/email=profile/email",
    "oauth-tokens"
  ],
  "user.pathPrefix":"azure",
  "handler.name":"azure"
}
```

Abaixo alguns dos atributos mais relevantes a serem configurados em DefaultSyncHandler. Observe que a Associação de grupo dinâmico deve estar sempre habilitada nos Serviços em nuvem.

| Nome da propriedade | Notas | Valor sugerido |
|---|---|---|
| `user.expirationTime` | Duração até que um usuário sincronizado expire. Os usuários são sincronizados somente após a expiração. | 1h |
| `user.membershipExpTime` | Duração até que uma associação de usuário sincronizada expire. As associações de usuário são sincronizadas somente após a hora de expiração. | 1h |
| `user.dynamicMembership` | Recomendamos ativar a associação dinâmica de grupo | verdadeiro |
| `user.enforceDynamicMembership` | Recomendamos ativar a imposição de associação de grupo dinâmico | verdadeiro |
| `group.dynamicGroups` | Recomendamos ativar grupos dinâmicos | verdadeiro |
| user.propertyMapping | A implementação fornecida de `UserInfoProcessor` sincroniza apenas algumas propriedades. Ele pode ser modificado e personalizado. | <code>&quot;profile/givenName=profile/given_name&quot;,</code><br><code>&quot;profile/familyName=profile/family_name&quot;,</code><br><code>&quot;rep:fullname=perfil/nome&quot;,</code><br><code>&quot;profile/email=profile/email&quot;,</code><br><code>&quot;access_token=access_token&quot;,</code><br><code>&quot;atualizar_token=atualizar_token&quot;</code> |  |
| `user.membershipNestingDepth` | Retorna a profundidade máxima do aninhamento de grupos quando as relações de associação são sincronizadas. Um valor 0 desativa efetivamente a pesquisa de associação de grupo. Um valor igual a 1 adiciona apenas os grupos diretos de um usuário. Este valor não tem efeito ao sincronizar grupos individuais somente ao sincronizar uma ancestralidade de associação de usuários. | 1 |

### Configurar o módulo de logon externo {#configure-the-external-login-module}

Por fim, é necessário configurar o Módulo de logon externo.

1. Crie um arquivo chamado `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json`. Consulte um exemplo de configuração abaixo:

   ```
   {
    "sync.handlerName":"azure",
    "idp.name":"azure-idp"
   }
   ```

1. Configure suas propriedades da seguinte maneira:

   * `sync.handlerName`: nome do Manipulador de Sincronização definido anteriormente
   * `idp.name`: Provedor de Identidade OAK definido no Manipulador de Autenticação OIDC

### Opcional: Implementar um UserInfoProcessor personalizado {#implement-a-custom-userinfoprocessor}

O usuário é autenticado por um Token de ID e atributos adicionais são buscados no ponto de extremidade `userInfo` definido para o IdP. Se operações não padrão adicionais tiverem que ser executadas, uma implementação personalizada do [UserInfoProcessor](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java) será a implementação padrão do Sling.

## Exemplo: configurar a autenticação OIDC com o Azure Ative Diretory

### Configurar um novo Aplicativo no Azure Ative Diretory {#configure-a-new-application-in-azure-ad}

1. Crie um novo aplicativo no Azure Ative Diretory seguindo a [documentação do Azure Ative Diretory](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure).  Veja abaixo a aparência da tela que detalha a visão geral do aplicativo:

   ![Visão geral do aplicativo](/help/security/assets/odic-application-overview.png)

1. Se forem necessários Grupos ou funções de aplicativo, siga a [documentação](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers) para habilitá-los para o aplicativo e envie-os no Token de ID. Abaixo, um exemplo de grupos configurados:

![ID do Token de Declaração OIDC](/help/security/assets/oidc-claim-id-token.png)

1. Siga as etapas documentadas anteriormente para criar os arquivos de configuração necessários. Abaixo um exemplo específico do Azure AD, onde:
   * Definimos o nome da conexão OIDC, Manipulador de autenticação e DefaultSyncHandler como: `azure`
   * A URL do site é: `www.mywebsite.com`
   * Protegemos o caminho `/content/wknd/us/en/adventures`
   * O inquilino é: `tennat-id`,
   * ID do cliente: `client-id`,
   * O segredo é: `secret`,
   * Os grupos são enviados no Token de ID em uma declaração chamada: `groups`

#### org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json

```
{
  "name":"azure",
  "scopes":[
    openid", "User.Read", "profile", "email
  ],
  "baseUrl":"https://login.microsoftonline.com/tenant-id/v2.0",
  "clientId":"client-id",
  "clientSecret":"secret"
}
```

#### org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json

```
{
  "callbackUri":"https://www.mywebsite.com/content/wknd/us/en/adventures/j_security_check",
  "path":[
    "/content/wknd/us/en/adventures"
  ],
  "idp":"azure",
  "defaultConnectionName":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json

```
{
  "sync.handlerName":"azure",
  "idp.name":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json

```
{
  "user.expirationTime":"1s",
  "user.membershipExpTime":"1s",
  "user.propertyMapping":[
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "access_token=access_token",
    "refresh_token=refresh_token"
  ],
  "user.pathPrefix":"azure",
  "group.pathPrefix": "oidc",
  "user.membershipNestingDepth": "1",
  "handler.name":"azure"
}
```

#### org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json

```
{
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false",
  "connection": "azure",
  "groupsClaimName": "groups"
}
```

### Informações adicionais sobre grupos do Azure AD {#additional-information-about-azure-ad-groups}

Para configurar um grupo para o aplicativo corporativo no Portal do Microsoft Azure, você precisa pesquisar o aplicativo em: **Aplicativos Corporativos** e adicionar os grupos: <!-- Alexandru: this bit cound be clearer-->

![Adição de grupo OIDC](/help/security/assets/oidc-ad-additional-info.png)

Para habilitar a declaração de grupo no Token de Id, adicione a declaração na seção **Configuração de Token** do Portal do Microsoft Azure: <!-- Alexandru: this bit cound be clearer as well-->

![ID do Token de Declaração OIDC](/help/security/assets/oidc-claim-id-token.png)

A configuração de `SlingUserInfoProcessor` deve ser modificada como no exemplo abaixo.

O nome de arquivo que precisa ser modificado é `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl.cfg.json`. O conteúdo deve ser configurado da seguinte maneira:

```
{
  "connection": "azure",
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false"
}
```
