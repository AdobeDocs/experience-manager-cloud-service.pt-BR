---
title: Suporte ao Open ID Connect para AEM as a Cloud Service no nível de publicação
description: Saiba como configurar o Open ID Connect (OIDC) para o AEM as a Cloud Service no nível de publicação
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: 70687e4f2ea0df923e44237bc20635745c46323a
workflow-type: tm+mt
source-wordcount: '2610'
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
    "baseUrl":"<https://login.microsoftonline.com/tenant-id/v2.0>",
    "clientId":"client-id-from-idp",
    "clientSecret":"xxxxxx"
   }
   ```

Em alguns ambientes, o provedor de identidade (IdP) pode não expor um ponto de extremidade `.well-known` válido.
Quando isso ocorre, os endpoints necessários podem ser definidos manualmente especificando as seguintes propriedades no arquivo de configuração.
Neste modo de configuração, a propriedade `baseUrl` não deve ser definida.

```
"authorizationEndpoint": "https://idp-url/oauth2/v1/authorize",
"tokenEndpoint": "https://idp-url/oauth2/v1/token",
"jwkSetURL":"https://idp-url/oauth2/v1/keys",
"issuer": "https://idp-url"
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
   * `callbackUri`: o caminho a ser protegido, adicionando o sufixo: `/j_security_check`. O mesmo callbackUri também deve ser configurado no IdP remoto como url de redirecionamento.
   * `defaultConnectionName`: configurar com o mesmo nome definido para a conexão OIDC na etapa anterior+
   * `pkceEnabled`: `true` Chave de Prova para Troca de Código (PKCE) no fluxo de código de Autorização
   * `idp`: o nome do [Provedor de Identidade Externo do OAK](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html). Observe que um OAK IDP diferente não pode compartilhar usuários ou grupos

### Configurar SlingUserInfoProcessor {#configure-slinguserinfoprocessor}

1. Crie o arquivo de configuração. Neste exemplo, usaremos `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json`. O sufixo `azure` deve ser um identificador exclusivo. Consulte um exemplo do arquivo de configuração abaixo:

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false,
      "idpNameInPrincipals": true
   }
   ```

1. Em seguida, configure suas propriedades da seguinte maneira:
   * `groupsInIdToken`: Definido como verdadeiro se os grupos forem enviados no Token de ID. Se o valor for falso, ou não for especificado, os grupos serão lidos do ponto de extremidade UserInfo.
   * `groupsClaimName`: O nome da declaração contém os grupos a serem sincronizados no AEM.
   * `connection`: configurar com o mesmo nome definido para a conexão OIDC na etapa anterior
   * `storeAccessToken`: verdadeiro se o token de acesso precisar ser armazenado no repositório. Por padrão, é falso. Defina como verdadeiro somente se o AEM precisar acessar recursos em nome do usuário armazenado em servidores externos protegidos pelo mesmo IdP.
   * `storeRefreshToken`: verdadeiro se o token de atualização deve ser armazenado no repositório. Por padrão, é falso. Defina-o como verdadeiro somente se o AEM precisar acessar recursos em nome do usuário armazenado em servidores externos protegidos pelo mesmo IdP e precisar atualizar o token do IdP.
   * `idpNameInPrincipals`: quando definido como verdadeiro, o nome do IdP é adicionado como sufixo às entidades de segurança de usuário e grupo separadas por um &#39;;&#39;. Por exemplo, se o nome do IdP for `azure-idp` e o nome de usuário for `john.doe`, a entidade de segurança armazenada no oak será `john.doe;azure-idp`. Isso é útil quando vários IdPs são configurados no oak para evitar conflitos entre usuários ou grupos com o mesmo nome vindo de IdPs diferentes. Isso também pode ser definido para evitar conflitos com usuários ou grupos criados por outros manipuladores de autenticação, como o Saml.
Observe que o token de acesso e o token de atualização são armazenados criptografados com a chave mestre do AEM.


### Configurar o Manipulador de sincronização {#configure-the-synchronization-handler}

Pelo menos um Manipulador de sincronização deve ser configurado para sincronizar os usuários autenticados no oak. Para obter mais detalhes, consulte [esta](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html) página.

Crie um arquivo chamado `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json`. O sufixo **azure** deve ser um identificador exclusivo. Para obter mais informações sobre como configurar suas propriedades, consulte a [documentação sobre Sincronização de Usuários e Grupos do Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html). Encontre um exemplo de configuração abaixo:

```
{
  "user.expirationTime":"1h",
  "user.membershipExpTime":"1h",
  "group.expirationTime": "1d"
  "user.propertyMapping":[
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "access_token=access_token",
    "refresh_token=refresh_token"
  ],
  "user.pathPrefix":"azure",
  "handler.name":"azure"
}
```

Durante o desenvolvimento, os tempos de expiração podem ser reduzidos a um valor mais baixo (por exemplo: 1s) para acelerar os testes de sincronização de usuários e grupos no oak.
Abaixo alguns dos atributos mais relevantes a serem configurados em DefaultSyncHandler. Observe que a Associação de grupo dinâmico deve estar sempre habilitada nos Serviços em nuvem.

| Nome da propriedade | Notas | Valor sugerido |
|---|---|---|
| `user.expirationTime` | Duração até que um usuário sincronizado expire. Os usuários são sincronizados somente após a expiração. | 1h |
| `user.membershipExpTime` | Duração até que uma associação de usuário sincronizada expire. As associações de usuário são sincronizadas somente após a hora de expiração. | 1h |
| `user.dynamicMembership` | Recomendamos ativar a associação dinâmica de grupo | verdadeiro |
| `user.enforceDynamicMembership` | Recomendamos ativar a imposição de associação de grupo dinâmico | verdadeiro |
| `group.dynamicGroups` | Recomendamos ativar grupos dinâmicos | verdadeiro |
| user.propertyMapping | A implementação fornecida de `UserInfoProcessor` sincroniza apenas algumas propriedades. Ele pode ser modificado e personalizado. | <code>&quot;profile/givenName=profile/given_name&quot;,</code><br><code>&quot;profile/familyName=profile/family_name&quot;,</code><br><code>&quot;rep:fullname=perfil/nome&quot;,</code><br><code>&quot;profile/email=profile/email&quot;,</code><br><code>&quot;access_token=access_token&quot;,</code><br><code>&quot;atualizar_token=atualizar_token&quot;</code> |
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

O usuário é autenticado por um token de ID e atributos adicionais são obtidos do ponto de extremidade `userInfo` definido para o IdP. O `UserInfoProcessor` é responsável por transformar os dados recebidos do provedor de identidade em credenciais e atributos que o AEM pode usar para a sincronização de usuários.

#### Quando criar um UserInfoProcessor personalizado {#when-to-create-custom-userinfoprocessor}

O [SlingUserInfoProcessorImpl](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java) padrão lida com declarações OIDC padrão e sincronização de grupos. Talvez seja necessária uma implementação personalizada se você precisar:

* Extrair e processar declarações personalizadas da resposta do token de ID ou UserInfo
* Transformar ou mapear declarações para nomes de atributo diferentes
* Implementar lógica personalizada para extração de grupos de declarações aninhadas
* Adicionar outros atributos do usuário que não fazem parte do perfil OIDC padrão
* Processar tokens de acesso ou atualizar tokens para casos de uso específicos
* Integrar a sistemas externos para enriquecer os dados do usuário durante a autenticação

#### Como entender a interface do UserInfoProcessor {#understanding-userinfoprocessor-interface}

A interface `UserInfoProcessor` do pacote `org.apache.sling.auth.oauth_client.spi` define dois métodos:

```java
public interface UserInfoProcessor {
    /**
     * Process the UserInfo and token response to create OIDC credentials
     *
     * @param userInfo - JSON response from the UserInfo endpoint (may be null)
     * @param tokenResponse - JSON response from the token endpoint
     * @param oidcSubject - The subject claim from the ID token
     * @param idp - The configured IDP name
     * @return OidcAuthCredentials containing user attributes and group memberships
     */
    @NotNull OidcAuthCredentials process(
        @Nullable String userInfo,
        @NotNull String tokenResponse,
        @NotNull String oidcSubject,
        @NotNull String idp
    );

    /**
     * @return The name of the OIDC connection this processor is associated with
     */
    @NotNull String connection();
}
```

O objeto `OidcAuthCredentials` retornado permite:
* Definir atributos de usuário via `setAttribute(key, value)` - eles são sincronizados com base nos mapeamentos de propriedade `DefaultSyncHandler`
* Adicionar associações de grupo via `addGroup(groupName)` - esses grupos são criados/sincronizados no AEM

#### Exemplo: implementação personalizada do UserInfoProcessor {#custom-userinfoprocessor-implementation}

Abaixo está um exemplo completo de como implementar um `UserInfoProcessor` personalizado:

```java
package com.mycompany.aem.auth;

import java.nio.charset.StandardCharsets;
import java.util.Base64;

import org.apache.sling.auth.oauth_client.spi.OidcAuthCredentials;
import org.apache.sling.auth.oauth_client.spi.UserInfoProcessor;
import org.jetbrains.annotations.NotNull;
import org.jetbrains.annotations.Nullable;
import org.osgi.service.component.annotations.Activate;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.metatype.annotations.AttributeDefinition;
import org.osgi.service.metatype.annotations.Designate;
import org.osgi.service.metatype.annotations.ObjectClassDefinition;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.google.gson.JsonObject;
import com.google.gson.JsonParser;

/**
 * Custom UserInfoProcessor that extracts additional claims from the ID token
 * and adds custom user attributes and group memberships.
 */
@Component(service = UserInfoProcessor.class, property = {"service.ranking:Integer=50"})
@Designate(ocd = CustomUserInfoProcessor.Config.class, factory = true)
public class CustomUserInfoProcessor implements UserInfoProcessor {

    private static final Logger logger = LoggerFactory.getLogger(CustomUserInfoProcessor.class);

    @ObjectClassDefinition(name = "Custom UserInfo Processor")
    @interface Config {
        @AttributeDefinition(name = "Connection Name", description = "OIDC Connection Name")
        String connection();
    }

    private final String connection;

    @Activate
    public CustomUserInfoProcessor(Config config) {
        this.connection = config.connection();
        logger.info("CustomUserInfoProcessor activated for connection: {}", connection);
    }

    @Override
    public @NotNull OidcAuthCredentials process(
            @Nullable String userInfo,
            @NotNull String tokenResponse,
            @NotNull String oidcSubject,
            @NotNull String idp) {

        // Parse the token response to extract tokens
        JsonObject tokenJson = JsonParser.parseString(tokenResponse).getAsJsonObject();
        String accessToken = tokenJson.has("access_token") ?
            tokenJson.get("access_token").getAsString() : null;
        String idToken = tokenJson.has("id_token") ?
            tokenJson.get("id_token").getAsString() : null;

        logger.debug("Processing authentication for subject: {}", oidcSubject);

        // Decode and extract claims from ID Token
        JsonObject claims = null;
        if (idToken != null) {
            claims = decodeJwtPayload(idToken);
            logger.debug("Extracted claims from ID token: {}", claims);
        }

        // Create credentials object
        OidcAuthCredentials credentials = new OidcAuthCredentials(oidcSubject, idp);
        credentials.setAttribute(".token", "");

        // Extract standard profile attributes
        if (claims != null) {
            // Standard OIDC claims
            setAttributeIfPresent(credentials, claims, "given_name", "profile/given_name");
            setAttributeIfPresent(credentials, claims, "family_name", "profile/family_name");
            setAttributeIfPresent(credentials, claims, "email", "profile/email");
            setAttributeIfPresent(credentials, claims, "name", "profile/name");

            // Custom claims from your IdP
            setAttributeIfPresent(credentials, claims, "department", "profile/department");
            setAttributeIfPresent(credentials, claims, "employee_id", "profile/employeeId");
            setAttributeIfPresent(credentials, claims, "job_title", "profile/jobTitle");
        }

        // Extract group memberships from claims
        if (claims != null && claims.has("groups")) {
            if (claims.get("groups").isJsonArray()) {
                claims.get("groups").getAsJsonArray().forEach(group -> {
                    credentials.addGroup(group.getAsString());
                });
            }
        }

        // Optionally store tokens if needed for later API calls
        // Note: Only store tokens if your application needs to call external APIs
        // on behalf of the user. Tokens are encrypted before storage.
        if (accessToken != null) {
            credentials.setAttribute("access_token", accessToken);
        }

        return credentials;
    }

    @Override
    public @NotNull String connection() {
        return connection;
    }

    /**
     * Helper method to set attribute if present in claims
     */
    private void setAttributeIfPresent(OidcAuthCredentials credentials,
                                      JsonObject claims,
                                      String claimName,
                                      String attributeName) {
        if (claims.has(claimName) && !claims.get(claimName).isJsonNull()) {
            String value = claims.get(claimName).getAsString();
            if (value != null && !value.isEmpty()) {
                credentials.setAttribute(attributeName, value);
            }
        }
    }

    /**
     * Decode JWT payload (middle part) to extract claims
     */
    private JsonObject decodeJwtPayload(String jwt) {
        try {
            String[] parts = jwt.split("\\.");
            if (parts.length != 3) {
                logger.warn("Invalid JWT format");
                return null;
            }

            // Decode the payload (second part)
            String payload = parts[1];
            // Add padding if needed
            payload = payload + "====".substring(0, (4 - payload.length() % 4) % 4);
            // Replace URL-safe characters
            payload = payload.replace('-', '+').replace('_', '/');

            byte[] decoded = Base64.getDecoder().decode(payload);
            String json = new String(decoded, StandardCharsets.UTF_8);
            return JsonParser.parseString(json).getAsJsonObject();
        } catch (Exception e) {
            logger.error("Failed to decode JWT payload", e);
            return null;
        }
    }
}
```

#### Configuração {#custom-userinfoprocessor-configuration}

Crie um arquivo de configuração para seu `UserInfoProcessor` personalizado em seu projeto do AEM em `ui.config/src/main/content/jcr_root/apps/myapp/osgiconfig/config.publish/`:

**com.mycompany.aem.auth.CustomUserInfoProcessor~azure.cfg.json**

```json
{
  "connection": "azure"
}
```

A configuração deve corresponder ao nome da conexão definido na sua configuração `OidcConnectionImpl`. A propriedade `service.ranking` na anotação `@Component` (definida como `50` no exemplo) determina a prioridade se vários processadores estiverem registrados para a mesma conexão. Classificações mais altas têm precedência sobre o padrão `SlingUserInfoProcessorImpl` (que tem uma classificação de `0`).

#### Dependências {#custom-userinfoprocessor-dependencies}

Adicione as seguintes dependências ao `pom.xml` do módulo principal:

```xml
<dependency>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.auth.oauth-client</artifactId>
    <version>0.1.7</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.8.9</version>
    <scope>provided</scope>
</dependency>
```

#### Sincronizando atributos com DefaultSyncHandler {#synchronizing-custom-attributes}

Para garantir que seus atributos personalizados sejam mantidos para nós de usuário no JCR, atualize sua configuração do `DefaultSyncHandler` para incluir mapeamentos de propriedade:

**org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json**

```json
{
  "user.expirationTime": "1h",
  "user.membershipExpTime": "1h",
  "user.propertyMapping": [
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "profile/department=profile/department",
    "profile/employeeId=profile/employeeId",
    "profile/jobTitle=profile/jobTitle",
    "access_token=access_token"
  ],
  "user.pathPrefix": "azure",
  "handler.name": "azure"
}
```

O formato é `jcrPropertyPath=credentialAttributeName`. O lado esquerdo é onde a propriedade é armazenada no nó do usuário em `/home/users`, e o lado direito corresponde ao nome do atributo definido em `UserInfoProcessor` usando `credentials.setAttribute()`.

#### Implantação e teste {#custom-userinfoprocessor-deployment}

1. **Crie e implante** seu projeto do AEM contendo o `UserInfoProcessor` personalizado:

   ```bash
   mvn clean install -PautoInstallPackage
   ```

2. **Verificar registro** no console OSGi em `/system/console/components`:
   * Procure pelo seu nome de classe de processador personalizado
   * Verifique se o componente está ativo e se a configuração de conexão está correta

3. **Testar fluxo de autenticação**:
   * Acessar um caminho protegido configurado no `OidcAuthenticationHandler`
   * Após a autenticação bem-sucedida, verifique o nó do usuário no CRXDE em `/home/users/<prefix>/<username>`
   * Verificar se os atributos personalizados estão sincronizados
   * Verificar associações de grupo em `/home/groups`

4. **Habilite o log de depuração** para solucionar problemas:

   ```
   Logger: com.mycompany.aem.auth
   Log Level: DEBUG
   ```

#### Práticas recomendadas {#custom-userinfoprocessor-best-practices}

* **Minimizar armazenamento de token**: armazene tokens de acesso ou atualize tokens somente se o aplicativo precisar fazer chamadas de API para serviços externos em nome dos usuários. Os tokens são criptografados, mas ainda adicionam sobrecarga.
* **Validar declarações**: sempre verifique se as declarações existem e não são nulas antes de processá-las.
* **Tratamento de erros**: registre os erros adequadamente, mas verifique se o fluxo de autenticação pode ser concluído mesmo se as declarações opcionais estiverem ausentes.
* **Desempenho**: mantenha a lógica de processamento leve, pois ela é executada em cada autenticação.
* **Segurança**: nunca registre informações confidenciais, como tokens completos ou senhas de usuário. Use `substring()` se estiver registrando tokens para depuração.
* **Testes**: teste com vários perfis de usuário de seu IdP para garantir que todas as variações de declaração sejam tratadas corretamente.

### Configurar ACL para grupos externos {#configure-acl-for-external-groups}

Quando os usuários são autenticados por meio do OIDC, suas associações de grupo normalmente são sincronizadas do provedor de identidade externo.
Esses grupos externos são criados dinamicamente no repositório do AEM, mas não são associados automaticamente a nenhuma entrada de controle de acesso.
Para garantir que os usuários tenham as permissões apropriadas, as listas de controle de acesso (ACLs) devem ser explicitamente definidas para esses grupos.

Duas abordagens principais estão disponíveis.

### Opção 1 — Grupos locais

O grupo externo pode ser adicionado como membro de um grupo local que já tem as ACLs necessárias.

* O grupo externo deve existir no repositório, que ocorre automaticamente quando um usuário pertencente a esse grupo faz logon pela primeira vez.
* Essa opção geralmente é preferida quando Grupos de usuários fechados (CUGs) estão em uso, pois o grupo local existe em ambos os ambientes, autor e publicação.

### Opção 2 — ACLs diretas em grupos externos via RepoInit

As ACLs podem ser aplicadas diretamente a grupos externos usando scripts RepoInit.

* Essa abordagem é mais eficiente e é preferível quando os CUGs não são usados.
* O exemplo a seguir mostra uma configuração RepoInit que atribui permissões de leitura a um grupo externo. A opção `ignoreMissingPrincipal` permite a criação da ACL mesmo se o grupo ainda não existir no repositório:

  ```
  {
    "scripts":[
      "set ACL for \"my-group;my-idp\"  (ACLOptions=ignoreMissingPrincipal)\r\n  allow jcr:read on /content/wknd/us/en/magazine\r\nend"
    ]
  }    
  ```

>[!NOTE]
>A interface de permissões do AEM pode ser usada para inspecionar as ACLs atribuídas a entidades de grupo

## Exemplo: configurar a autenticação OIDC com o Azure Ative Diretory

### Configurar um novo Aplicativo no Azure Ative Diretory {#configure-a-new-application-in-azure-ad}

1. Crie um novo aplicativo no Azure Ative Diretory seguindo a [documentação do Azure Ative Diretory](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure).  Veja abaixo a aparência da tela que detalha a visão geral do aplicativo:

   ![Visão geral do aplicativo](/help/security/assets/odic-application-overview.png)

1. Se forem necessários Grupos ou funções de aplicativo, siga a [documentação](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers) para habilitá-los para o aplicativo e envie-os no Token de ID. Abaixo, um exemplo de grupos configurados:

![ID do Token de Declaração OIDC](/help/security/assets/oidc-claim-id-token.png)

1. Siga as etapas documentadas anteriormente para criar os arquivos de configuração necessários. Abaixo um exemplo específico do Azure AD, onde:
   * Definimos o nome da conexão OIDC, Manipulador de autenticação e DefaultSyncHandler como: `azure`
   * A URL do site é: `www.mywebsite.com`
   * Protegemos o caminho `/content/wknd/us/en/adventures` que é acessível apenas a usuários autenticados membros do grupo `adventures`
   * O inquilino é: `tennat-id`,
   * ID do cliente: `client-id`,
   * O segredo é: `secret`,
   * Os grupos são enviados no Token de ID em uma declaração chamada: `groups`

### org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json

```
{
  "name":"azure",
  "scopes":[
    openid", "User.Read", "profile", "email"
  ],
  "baseUrl":"https://login.microsoftonline.com/tenant-id/v2.0",
  "clientId":"client-id",
  "clientSecret":"secret"
}
```

### org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json

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

### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json

```
{
  "sync.handlerName":"azure",
  "idp.name":"azure"
}
```

### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json

```
{
  "user.expirationTime":"1h",
  "user.membershipExpTime":"1h",
  "group.expirationTime": "1d"
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

### org.apache.sling.jcr.repoinit.RepositoryInitializer~azure.cfg.json

```
{
  "scripts":[
    "set ACL for \"adventures;azure\"  (ACLOptions=ignoreMissingPrincipal)\r\n  allow jcr:read on /content/wknd/us/en/adventures\r\nend"
  ]
}
```

### org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json

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

Para configurar um grupo para o aplicativo empresarial no Microsoft Azure Portal, você precisa pesquisar o aplicativo em: **Aplicativos empresariais** e adicionar os grupos: <!-- Alexandru: this bit cound be clearer-->

![Adição de grupo OIDC](/help/security/assets/oidc-ad-additional-info.png)

Para habilitar a declaração de grupo no Token de Id, adicione a declaração na seção **Configuração de Token** do Portal Azure do Microsoft: <!-- Alexandru: this bit cound be clearer as well-->

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

## Personalizar redirecionamento após autenticação {#custom-redirect-after-authentication}

Por padrão, após a autenticação OIDC bem-sucedida, os usuários são redirecionados de volta para o URL solicitado originalmente. No entanto, você pode personalizar esse comportamento usando o parâmetro de consulta `redirect`.

### Uso do parâmetro de redirecionamento

Ao iniciar a autenticação, você pode especificar uma URL de redirecionamento personalizada adicionando o parâmetro `redirect` à sua solicitação de autenticação:

```
/content/wknd/us/en/adventures?redirect=/content/wknd/us/en/welcome
```

Neste exemplo, após a autenticação bem-sucedida, o usuário será redirecionado para `/content/wknd/us/en/welcome` em vez da página solicitada originalmente.

### Restrições de segurança

Por motivos de segurança, o parâmetro `redirect` tem as seguintes restrições:

* **Deve ser um caminho relativo**: a URL de redirecionamento deve começar com `/` (por exemplo, `/content/mysite/dashboard`)
* **Nenhum redirecionamento entre sites**: URLs absolutas (por exemplo, `https://external-site.com`) não são permitidas
* **Nenhuma URL relativa a protocolo**: URLs iniciadas com `//` são rejeitadas para impedir redirecionamentos relativos a protocolo

Se um URL de redirecionamento inválido for fornecido, a autenticação falhará com um erro.

### Exemplo de casos de uso

1. **Página de boas-vindas após o logon**: redirecionar usuários para uma página de boas-vindas personalizada após o primeiro logon

   ```
   /content/mysite/secure-area?redirect=/content/mysite/welcome
   ```

2. **Redirecionamento do painel**: direciona os usuários para um painel específico após a autenticação

   ```
   /content/mysite/login?redirect=/content/mysite/user/dashboard
   ```

3. **Deep linking**: permitir que os usuários autentiquem e acessem um recurso específico

   ```
   /content/mysite/protected?redirect=/content/mysite/protected/specific-document
   ```

## Como migrar do Manipulador de autenticação Saml para o Manipulador de autenticação Oidc

Quando o AEM já estiver configurado com um Manipulador de Autenticação SAML e os usuários estiverem presentes no repositório com a [sincronização de dados](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier#data-synchronization) habilitada, poderão ocorrer conflitos entre os usuários SAML originais e os novos usuários OIDC.

1. Configure o [OidcAuthenticationHandler](#configure-oidc-authentication-handler) e habilite `idpNameInPrincipals` na configuração [SlingUserInfoProcessor](#configure-slinguserinfoprocessor)
1. Configuração [ACL para grupos externos](#configure-acl-for-external-groups).
1. Após o logon dos usuários, os usuários antigos criados pelo manipulador de autenticação saml podem ser excluídos.

>[!NOTE]
>Quando o Manipulador de Autenticação SAML estiver desabilitado e o Manipulador de Autenticação OIDC estiver habilitado, se a [sincronização de dados](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/personalization/user-and-group-sync-for-publish-tier#data-synchronization) não estiver habilitada, as sessões existentes se tornarão inválidas. Os usuários precisarão se autenticar novamente, o que resulta na criação de novos nós de usuário OIDC no repositório.

