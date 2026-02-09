---
title: Migração para Identidade Externa e Associação de Grupo Dinâmico
description: Guia técnico para migrar usuários e grupos locais para um modelo de identidade externo com associação de grupo dinâmica no AEM as a Cloud Service
solution: Experience Manager Sites
feature: Security
role: Developer, Admin
source-git-commit: bb4b60523f60b1285c5f2fd2e49f6cc8cff24324
workflow-type: tm+mt
source-wordcount: '2232'
ht-degree: 0%

---

# Migração para Identidade Externa e Associação de Grupo Dinâmico {#migrating-to-external-identity}

## Visão geral {#overview}

Quando a [Sincronização de Dados](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md#data-synchronization) está habilitada no AEM as a Cloud Service, o Manipulador de Autenticação SAML pode ser configurado para migrar automaticamente para identidades externas com associação de grupo dinâmico quando gerencia a criação de usuários e grupos. Se o projeto usar um código personalizado para criar usuários ou grupos, você deverá atualizá-lo para criar usuários e grupos externos, em vez de usuários e grupos locais.

### Por que usuários e grupos externos são necessários {#why-external-required}

A migração de usuários e grupos locais para identidades externas com associação de grupo dinâmica é essencial por vários motivos críticos:

**Otimização de desempenho:**

* **Gravações de Repositório Reduzidas**: a associação de grupo local tradicional requer a gravação de relações de associação no repositório em uma única propriedade de vários valores do nó do grupo. Com a associação de grupo dinâmica, os usuários têm uma única propriedade `rep:externalPrincipalNames` contendo todas as entidades de grupo, eliminando a necessidade de sincronizar o nó do grupo
* **Sincronização mais rápida**: ao sincronizar usuários entre nós do nível de publicação, os usuários externos com associação de grupo dinâmica requerem significativamente menos transferência de dados e menos operações de gravação em comparação aos usuários locais com associações de grupo tradicionais
* **Escalabilidade**: sistemas com um grande número de usuários e grupos se beneficiam drasticamente da redução da sobrecarga do repositório. A associação de grupo dinâmica é dimensionada com eficiência mesmo em grupos muito grandes.

Este documento fornece orientação técnica para:

* Compreensão do modelo de identidade externa
* Modificação do código personalizado para criar usuários e grupos externos
* Migração de usuários e grupos locais existentes para o modelo de identidade externa

## Noções básicas sobre identidade externa {#understanding-external-identity}

### Usuários externos {#external-users}

Os usuários externos são identificados pela propriedade `rep:externalId`, que vincula o usuário a um provedor de identidade externo. O formato é:

```
userId;idpName
```

Por exemplo: `john.doe;saml-idp`.

>[!NOTE]
>
> `idpName` refere-se ao nome do Provedor de Identidade Oak (Idp) conforme definido na configuração do Manipulador de Autenticação. Para integrações SAML, este é o valor definido para o atributo `idpIdentifier` no Manipulador de Autenticação SAML.

**Propriedades da Chave:**

* `rep:externalId`: propriedade obrigatória que marca um usuário como externo (por exemplo, `john.doe;saml-idp`)
* `rep:externalPrincipalNames`: propriedade com vários valores contendo entidades de grupo externas para associação dinâmica
* `rep:lastSynced`: carimbo de data/hora da última sincronização
* `rep:lastDynamicSync`: carimbo de data/hora da última sincronização de associação de grupo dinâmico

### Grupos Externos {#external-groups}

Os grupos externos também são identificados pela propriedade `rep:externalId` e usam um formato de nome principal:

```
groupId;idpName
```

Por exemplo: `content-authors;saml-idp`

### Associação de grupo dinâmico {#dynamic-group-membership}

Em vez de relações diretas entre usuário e grupo armazenadas no repositório, a associação dinâmica de grupo usa a propriedade `rep:externalPrincipalNames` no nó do usuário. Quando um usuário tem um nome principal externo que corresponde à ID de um grupo externo, ele se torna um membro desse grupo automaticamente. Para obter mais informações, consulte a [documentação do Apache Oak](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html).

**Vantagens:**

* Gravações de repositório reduzidas (nenhum nó de associação de grupo é modificado quando os usuários são adicionados/removidos dos grupos)
* Sincronização mais rápida entre nós do nível de publicação
* Gerenciamento escalonável de associação de grupo
* Compatível com os requisitos de sincronização de dados

## Configuração de usuário do serviço {#service-user-configuration}

Todas as operações que criam ou modificam usuários e grupos externos devem ser executadas usando um **usuário do serviço** configurado corretamente para ignorar a proteção padrão nas propriedades `rep:externalId` e `rep:externalPrincipalNames`.

### Por que é necessário um usuário de serviço? {#why-is-a-service-user-required}

Por padrão, a segurança do Oak impede que as sessões regulares modifiquem propriedades protegidas como:

* `rep:externalId` - Marca usuários/grupos como externos
* `rep:externalPrincipalNames` - Armazena entidades de associação de grupo dinâmico

Somente um usuário de serviço configurado corretamente pode modificar essas propriedades.

### Configuração e mapeamento de usuário de serviço {#service-user-configuration-mapping}

A configuração de um usuário de serviço para gerenciar identidades externas requer três configurações coordenadas:

1. Criar o usuário do serviço via `repoinit`
2. Configurar proteção do `ExternalPrincipal`
3. Mapeie o usuário do serviço para seu pacote de aplicativos.

Consulte abaixo para obter uma descrição abrangente dessas etapas.

#### Etapa 1: Criar o Usuário de Serviço via Repoinit {#create-the-serviice-user-via-repoinit}

Esta etapa detalha a criação do usuário do serviço com as permissões necessárias usando um script `repoinit`.

**Arquivo de Configuração:** `org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json`

**Local exemplar:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "scripts": [
    "create service user group-provisioner with path system/yourproject",
    "set ACL for group-provisioner\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/users\n  allow jcr:read,jcr:readAccessControl,jcr:modifyAccessControl,rep:userManagement,rep:write on /home/groups\nend"
  ]
}
```

**Visão geral das permissões**

* `jcr:read`: Ler usuários e grupos
* `jcr:readAccessControl`: Ler ACLs
* `jcr:modifyAccessControl`: Modificar ACLs (necessário para definir propriedades)
* `rep:userManagement`: Criar e gerenciar usuários/grupos
* `rep:write`: Gravar propriedades incluindo `rep:externalId` e `rep:externalPrincipalNames`

>[!NOTE]
>
>O usuário do serviço foi criado em `/home/users/system/yourproject` para mantê-lo organizado com outros usuários do sistema.

#### Etapa 2: Configurar a Proteção ExternalPrincipal {#configure-externalprincipal-protection}

Veja abaixo um exemplo de configuração para adicionar o usuário do serviço à lista de permissões, de modo que ele possa ignorar a proteção aplicada às propriedades de identidade externas.

**Nome do arquivo de configuração:** `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json`

**Exemplo de local:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "protectExternalIdentities": "Warn",
  "systemPrincipalNames": [
    "group-provisioner",
    "saml-migration-service"
  ]
}
```

**Propriedades de Configuração:**

* `protectExternalIdentities`: Controla o nível de proteção para propriedades de identidade externa:
   * `"Strict"`: somente entidades do sistema na lista de permissões podem modificar propriedades externas. Esse é o nível recomendado para produção.
   * `"Warn"`: registra avisos, mas permite modificações. Útil para desenvolvimento/teste.
   * `"None"`: Sem proteção. Não recomendado.
* `systemPrincipalNames`: Lista de nomes de usuários de serviço com permissão para modificar `rep:externalId` e `rep:externalPrincipalNames`. Inclua todos os usuários de serviço que precisam gerenciar identidades externas (por exemplo, `group-provisioner`, `saml-migration-service`).

>[!IMPORTANT]
>
>Os nomes de usuário do serviço em `systemPrincipalNames` devem corresponder exatamente às IDs de usuário do serviço criadas no script de repoinit.

#### Etapa 3: Mapeamento de usuários de serviço {#service-user-mapping}

Mapeie o usuário do serviço para seu pacote de aplicativos para que seu código possa usá-lo.

**Arquivo de Configuração:** `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json`

**Local:** `ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/config.publish/`

```json
{
  "user.mapping": [
    "yourproject.core:group-provisioner=[group-provisioner]"
  ]
}
```

**Formato de Mapeamento:**

* `yourproject.core`: O nome simbólico do pacote (encontrado em `pom.xml` `<Bundle-SymbolicName>`)
* `group-provisioner` (antes de `=`): o nome do subserviço que você usará no código
* `[group-provisioner]` (após `=`): a ID de usuário de serviço real criada em repoinit

### Usando o usuário do serviço no código {#using-the-service-user-in-code}

Ao abrir uma sessão para executar operações de migração ou criação de usuários/grupos, você deve usar o usuário do serviço:

```java
import org.apache.sling.jcr.api.SlingRepository;

@Reference
private SlingRepository repository;

// Login as the service user
Session serviceSession = repository.loginService("group-provisioner", null);

try {
    UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
    // Perform operations...
    serviceSession.save();
} finally {
    if (serviceSession != null && serviceSession.isLive()) {
        serviceSession.logout();
    }
}
```

>[!IMPORTANT]
>
>Sem a configuração adequada do usuário de serviço, as tentativas de definir `rep:externalId` ou `rep:externalPrincipalNames` falharão com erros de permissão. Verifique se o usuário do serviço está configurado corretamente na configuração `ExternalPrincipal` antes de tentar a migração.

## Exemplo de configuração completa {#complete-configuration-example}

Abaixo, você encontrará um exemplo completo de funcionamento mostrando todas as três configurações juntas:

### Estrutura do arquivo {#file-structure}

```
ui.config/src/main/content/jcr_root/apps/yourproject/osgiconfig/
└── config.publish/
    ├── org.apache.sling.jcr.repoinit.RepositoryInitializer~group-provisioner.cfg.json
    ├── org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration.cfg.json
    └── org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended~group-provisioner.cfg.json
```

### Modificação do código personalizado {#modifying-custom-code}

#### Criar usuários externos {#creating-external-users}

**Antes (Usuário Local):**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
User user = userManager.createUser(userId, password);
```

**Depois (Usuário Externo):**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create user with principal
Principal userPrincipal = new Principal() {
    @Override
    public String getName() {
        return userId;
    }
};

User user = userManager.createUser(userId, null, userPrincipal, null);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
String externalId = externalRef.getString(); // Format: userId;idpName
user.setProperty("rep:externalId", valueFactory.createValue(externalId));

// Set sync timestamps to far future (workaround for OAK-12079)
// Set to 10 years in the future to prevent premature cleanup of external group memberships
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));

session.save();
```

#### Criando Grupos Externos {#creating-external-groups}

**Antes (Grupo Local):**

```java
UserManager userManager = ((JackrabbitSession) session).getUserManager();
Group group = userManager.createGroup(groupId);
```

**Depois (Grupo Externo):**

```java
import org.apache.jackrabbit.oak.spi.security.authentication.external.ExternalIdentityRef;

UserManager userManager = ((JackrabbitSession) session).getUserManager();
ValueFactory valueFactory = session.getValueFactory();

// Create group with principal
Principal groupPrincipal = new Principal() {
    @Override
    public String getName() {
        return groupId;
    }
};

Group group = userManager.createGroup(groupPrincipal);

// Set rep:externalId
ExternalIdentityRef externalRef = new ExternalIdentityRef(groupId, idpName);
String externalId = externalRef.getString(); // Format: groupId;idpName
group.setProperty("rep:externalId", valueFactory.createValue(externalId));

session.save();
```

#### Atribuição de associação de grupo dinâmico {#assigning-dynamic-membership}

**Antes (Associação Direta):**

```java
Group group = (Group) userManager.getAuthorizable(groupId);
User user = (User) userManager.getAuthorizable(userId);
group.addMember(user);
```

**Depois (Associação Dinâmica):**

```java
User user = (User) userManager.getAuthorizable(userId);
ValueFactory valueFactory = session.getValueFactory();

// Get existing external principal names
Value[] existingValues = user.getProperty("rep:externalPrincipalNames");
List<String> principalNames = new ArrayList<>();

if (existingValues != null) {
    for (Value value : existingValues) {
        principalNames.add(value.getString());
    }
}

// Add new principal name (format: groupId;idpName)
String dynamicGroupPrincipal = groupId + ";" + idpName;
if (!principalNames.contains(dynamicGroupPrincipal)) {
    principalNames.add(dynamicGroupPrincipal);
    
    // Create new Value array
    Value[] newValues = new Value[principalNames.size()];
    for (int i = 0; i < principalNames.size(); i++) {
        newValues[i] = valueFactory.createValue(principalNames.get(i));
    }
    
    // Set the property
    user.setProperty("rep:externalPrincipalNames", newValues);
    
    // Update sync timestamps to far future (workaround for OAK-12079)
    // Set to 10 years in the future to prevent premature cleanup of external group memberships
    // See: https://issues.apache.org/jira/browse/OAK-12079
    java.util.Calendar future = java.util.Calendar.getInstance();
    future.add(java.util.Calendar.YEAR, 10);
    user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
    user.setProperty("rep:lastSynced", valueFactory.createValue(future));
}

session.save();
```

## Processo de migração {#migration-process}

A migração de usuários e grupos locais existentes para a identidade externa não é necessária quando o código personalizado foi atualizado antes da habilitação dos Serviços de Sincronização de Dados.

Se os usuários e grupos locais já tiverem sido mantidos no repositório e o ambiente for usado ativamente, recomendamos que você execute uma migração em várias etapas, como a seguir, para evitar interrupções ou inconsistências.

>[!IMPORTANT]
>
>Todas as etapas de migração devem ser executadas usando um usuário de serviço configurado corretamente (por exemplo, `group-provisioner`) que tenha permissões para ignorar a proteção nas propriedades `rep:externalId` e `rep:externalPrincipalNames`. Consulte [Configuração de Usuário de Serviço](#service-user-configuration) para obter mais detalhes.

### Etapa 1: Criar Estrutura de Grupo Externo {#step-1-create-external-group-structure}

Para cada grupo local que precisa ser migrado:

1. Crie um grupo externo correspondente com o nome principal: `<localGroupId>;<idpName>`. Usar uma convenção de nomenclatura que ajude a vincular grupos externos a grupos locais
1. Defina a propriedade `rep:externalId` no grupo externo com valores: `<localGroupId>;<idpName>`
1. Adicione o grupo externo como membro do grupo local original.

**Validação**

* Você pode validar os resultados verificando se cada grupo local tem um grupo externo correspondente. Além disso, cada grupo externo é membro do grupo local correspondente.

**Exemplo de Ponto de Extremidade de Servlet:**

```java
@SlingServletPaths("/bin/migration/step1")
public class MigrationStep1Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String groupPath = request.getParameter("groupPath");
        String idpName = request.getParameter("idpName");

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Get local group
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        String localGroupId = localGroup.getID();
        
        // Create external group
        String externalGroupPrincipalName = localGroupId + ";" + idpName;
        // The function createExternalGroup performs the following steps:
        // 1. Creates a new external group with the given principal name (format: "<localGroupId>;<idpName>").
        // 2. Sets the 'rep:externalId' property on the group to mark it as an external group (value: "<localGroupId>;<idpName>").
        // 3. Sets the 'rep:principalName' property for the group if required.
        // 4. Assigns any other required group metadata, such as a title or description, if needed.
        // 5. Persists the new group node in the repository at the appropriate path under /home/groups.
        // 6. Returns the created Group object so it can be used for further operations, such as membership assignment.
        Group externalGroup = createExternalGroup(externalGroupPrincipalName, localGroupId, idpName);
        
        // Add external group to local group
        localGroup.addMember(externalGroup);
        
        session.save();
    }
}
```

**Uso:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/c/content-authors&idpName=saml-idp"
```

### Etapa 2: Converter usuários e atribuir associação dinâmica {#step-2-convert-users-and-assign-dynamic-membership}

Para cada usuário membro de um grupo local:

1. Verifique se ele tem o conjunto `rep:externalId`definido (converta para usuário externo, se necessário).
1. Para cada associação de grupo, adicione a entidade de grupo externa correspondente a `rep:externalPrincipalNames`
1. Atualizar carimbos de data e hora de sincronização.

>[!IMPORTANT]
>
>Ignorar grupos do sistema como &quot;todos&quot; durante esse processo.

**Exemplo de Ponto de Extremidade de Servlet:**

```java
@SlingServletPaths("/bin/migration/step2")
public class MigrationStep2Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {
        String userId = request.getParameter("userId");
        String idpName = request.getParameter("idpName");
        
        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        // Login as the service user
        Session serviceSession = repository.loginService("group-provisioner", null);

        try {
            UserManager userManager = ((JackrabbitSession) serviceSession).getUserManager();
            User user = (User) userManager.getAuthorizable(userId);
            
            // Ensure user has rep:externalId
            Value[] externalIdValues = user.getProperty("rep:externalId");
            if (externalIdValues == null || externalIdValues.length == 0) {
                ExternalIdentityRef externalRef = new ExternalIdentityRef(userId, idpName);
                user.setProperty("rep:externalId", 
                            valueFactory.createValue(externalRef.getString()));
            }
            
            // Get all group memberships
            Iterator<Group> groupIterator = user.declaredMemberOf();
            List<String> principalNames = new ArrayList<>();
            
            while (groupIterator.hasNext()) {
                Group group = groupIterator.next();
                String groupId = group.getID();
                
                // Skip system groups
                if ("everyone".equals(groupId)) {
                    continue;
                }
                
                // Add dynamic group principal
                String dynamicGroupPrincipal = groupId + ";" + idpName;
                principalNames.add(dynamicGroupPrincipal);
            }
            
            // Set rep:externalPrincipalNames
            if (!principalNames.isEmpty()) {
                Value[] newValues = new Value[principalNames.size()];
                for (int i = 0; i < principalNames.size(); i++) {
                    newValues[i] = valueFactory.createValue(principalNames.get(i));
                }
                user.setProperty("rep:externalPrincipalNames", newValues);
            }
            
            // Update timestamps to far future (workaround for OAK-12079)
            // Set to 10 years in the future to prevent premature cleanup of external group memberships
            // See: https://issues.apache.org/jira/browse/OAK-12079
            java.util.Calendar future = java.util.Calendar.getInstance();
            future.add(java.util.Calendar.YEAR, 10);
            user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
            user.setProperty("rep:lastSynced", valueFactory.createValue(future));
        
        // Perform operations...
        serviceSession.save();
    } finally {
        if (serviceSession != null && serviceSession.isLive()) {
            serviceSession.logout();
        }
}    }
}
```

**Uso:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step2?userId=john.doe&idpName=saml-idp"
```

**Validação**

Você pode validar isso verificando se cada usuário tem os atributos `rep:externalId` e `rep:externalPrincipalName` com o `principalName` de cada grupo externo. Os usuários são membros dos grupos locais *e* dos grupos externos.

### Etapa 3: Remover Associações Diretas de Usuário {#step-3-remove-direct-user-memberships}

Depois que os usuários tiverem uma associação de grupo dinâmica configurada:

1. Remover associações diretas de usuários de grupos locais
1. Manter associações de grupo para grupo (incluindo a associação de grupo externo)

**Exemplo de Ponto de Extremidade de Servlet:**

```java
@SlingServletPaths("/bin/migration/step3")
public class MigrationStep3Servlet extends SlingAllMethodsServlet {
    
    @Override
    protected void doPost(SlingHttpServletRequest request, 
                          SlingHttpServletResponse response) {

        // Check if the caller is authorized to run the servlet
        isAuthorizedCaller(request, response);

        String groupPath = request.getParameter("groupPath");
        
        Authorizable localGroupAuth = userManager.getAuthorizableByPath(groupPath);
        Group localGroup = (Group) localGroupAuth;
        
        // Process each member
        Iterator<Authorizable> members = localGroup.getDeclaredMembers();
        
        while (members.hasNext()) {
            Authorizable member = members.next();
            
            // Remove only user members, keep group members
            if (!member.isGroup()) {
                localGroup.removeMember(member);
            }
        }
        
        session.save();
    }
}
```

**Uso:**

```bash
curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/c/content-authors"
```

**Validação**

* Você pode validar isso verificando se cada grupo local tem somente o grupo externo correspondente, ou outros grupos, como membro.


## Fluxo de trabalho de migração {#migration-workflow}

### Lista de verificação de pré-migração {#pre-migration-checklist}

* [ ] **Configurar Usuário de Serviço**: criar e configurar o usuário de serviço (por exemplo, `group-provisioner`) com as permissões adequadas
* [ ] **Verificar Configuração de ExternalPrincipal**: verifique se o usuário do serviço está configurado para ignorar a proteção em `rep:externalId` e `rep:externalPrincipalNames`
* [ ] **Testar Permissões de Usuário de Serviço**: verifique se o usuário do serviço pode definir propriedades de identidade externas em desenvolvimento
* [ ] Identifique todo o código personalizado que cria usuários ou grupos
* [ ] Revise e atualize o código personalizado para usar o modelo de identidade externo
* [ ] Teste de código atualizado no ambiente de desenvolvimento
* [ ] Faça um inventário de todos os usuários e grupos locais existentes para migrar
* [ ] Testar processo de migração em ambientes inferiores

### Etapas de execução {#execution-steps}

1. **Implantar Código Atualizado**: implante alterações de código personalizado para criar usuários/grupos externos

1. **Criar Grupos Externos** (para cada grupo local):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step1?groupPath=/home/groups/g/my-group&idpName=saml-idp"
   ```

1. **Migrar Usuários** (para cada usuário):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step2?userId=username&idpName=saml-idp"
   ```

1. **Limpeza** (para cada grupo migrado):

   ```bash
   curl -X POST "http://localhost:4503/bin/migration/step3?groupPath=/home/groups/g/my-group"
   ```

1. **Verificar**: verificar associações de grupo de usuários e testar permissões de acesso

1. **Habilitar Sincronização de Dados**: Contate o Suporte ao Cliente para habilitar o recurso

### Validação pós-migração {#post-migration-validation}

Verifique a migração:

1. **Verificar Propriedades do Usuário**:

   Em nós de usuário, verifique a presença de:

   * `rep:externalId`: O formato deve ser `userId;idpName`
   * `rep:externalPrincipalNames`: Matriz de entidades de grupo no formato `groupId;idpName`
   * `rep:lastSynced`: carimbo de data e hora definido como futuro distante (aproximadamente 10 anos a partir da data de migração)
   * `rep:lastDynamicSync`: carimbo de data e hora definido como futuro distante (aproximadamente 10 anos a partir da data de migração)

   **Observação**: os carimbos de data/hora são intencionalmente definidos como uma data futura distante como uma solução alternativa para o OAK-12079. Esse é o comportamento esperado.

1. **Verificar Propriedades do Grupo**:

   Em nós de grupos locais, verifique a presença de:

   * Membro do grupo externo com o formato `groupId;idpName`
   * Nenhum membro de usuário direto (somente após a Etapa 3)

1. **Testar Logon de Usuário**: verifique se os usuários podem fazer logon e se têm as permissões corretas

1. **Testar Controle de Acesso**: verificar se os usuários podem acessar conteúdo protegido por CUGs/ACLs

## Resolução de problemas {#troubleshooting}

### Problemas comuns {#common-issues}

**Problema: Erros de permissão ao configurar `rep:externalId` ou`rep:externalPrincipalNames`**

**Mensagens de Erro:**

* `javax.jcr.AccessDeniedException: Access denied`
* `OakAccess0000: Access denied`
* `Cannot set property 'rep:externalId'`

**Solução**: a sessão deve ser aberta usando um usuário de serviço configurado corretamente que tenha permissões para ignorar a proteção em propriedades de identidade externa.

**Etapas para resolver:**

1. **Verificar se o usuário do serviço existe**: verifique se o usuário do serviço (por exemplo, `group-provisioner`) foi criado via repoinit
1. **Verificar mapeamento de usuário do serviço**: verifique se o servlet ou o serviço está usando `repository.loginService("group-provisioner", null)`
1. **Verificar configuração de ExternalPrincipal**: verifique se `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.principal.ExternalPrincipalConfiguration` está configurado corretamente
1. **Verificar permissões do usuário do serviço**: o usuário do serviço precisa de `rep:write` e `rep:userManagement` permissões em `/home/users` e `/home/groups`

Consulte [Configuração de Usuário de Serviço](#service-user-configuration) para obter instruções de instalação completas.

**Problema:`OakConstraint0072: Property 'rep:externalPrincipalNames' requires 'rep:externalId' to be present`**

**Solução**: os usuários devem ter `rep:externalId` definido antes da configuração `rep:externalPrincipalNames`. Primeiro, certifique-se de que a Etapa 2 converta usuários em usuários externos.

**Problema: os usuários perdem associações de grupo após a migração**

**Solução**: verifique se:

* O grupo externo foi criado com o formato de nome de entidade correto (`groupId;idpName`)
* Grupo externo adicionado como membro do grupo local (Etapa 1)
* O usuário tem nomes principais externos corretos em `rep:externalPrincipalNames` (Etapa 2)
* A limpeza da etapa 3 foi executada somente após a conclusão das Etapas 1 e 2

**Problema: as associações a grupos externos são removidas inesperadamente após o logon do usuário (OAK-12079)**

**Problema**: devido ao bug do Oak [OAK-12079](https://issues.apache.org/jira/browse/OAK-12079), o mecanismo de sincronização do Oak pode limpar prematuramente as associações a grupos externos com base nos carimbos de data/hora `rep:lastSynced` e `rep:lastDynamicSync`.

**Solução**: Defina os carimbos de data/hora `rep:lastSynced` e `rep:lastDynamicSync` para uma data futura distante (daqui a 10 anos) em vez da hora atual. Isso impede que o processo de limpeza da sincronização remova as associações de grupo externo.

**Implementação:**

```java
// Workaround for OAK-12079
// Set to 10 years in the future to prevent premature cleanup
// See: https://issues.apache.org/jira/browse/OAK-12079
java.util.Calendar future = java.util.Calendar.getInstance();
future.add(java.util.Calendar.YEAR, 10);
user.setProperty("rep:lastSynced", valueFactory.createValue(future));
user.setProperty("rep:lastDynamicSync", valueFactory.createValue(future));
```

**Por que isso funciona**: ao definir os carimbos de data/hora para uma data futura, a lógica de sincronização do Oak trata esses usuários como &quot;sincronizados recentemente&quot; e não aciona o processo de limpeza que removeria os nomes principais externos e as associações de grupo.

**Observação**: esta é uma solução temporária até que OAK-12079 seja resolvida em uma versão futura do Oak. Todos os exemplos de código neste documento já incluem essa solução alternativa.

**Problema: o grupo do sistema &quot;todos&quot; causa erros**

**Solução**: sempre ignorar o grupo do sistema &quot;todos&quot; durante a migração do usuário (Etapa 2). Este grupo é gerenciado automaticamente pela AEM.

### Procedimento de reversão {#rollback-procedure}

Se a migração encontrar problemas:

1. Interromper processo de migração
1. Restaurar a partir do backup se dados críticos forem afetados
1. Reverter as alterações no código para criar usuários externos e grupos com associação dinâmica a grupos
1. Revise e corrija os problemas antes de tentar a migração novamente.

## Práticas recomendadas {#best-practices}

* **Testar minuciosamente**: sempre teste a migração em ambientes de desenvolvimento e de preparo antes da produção
* **Processamento em lote**: para grandes bases de usuários, processe migrações em lotes para evitar problemas de tempo limite
* **Monitorar Desempenho**: Observe o desempenho do repositório durante a migração
* **Manter Trilha de Auditoria**: registra em log todas as operações de migração para solucionar problemas
* **Permissões de usuário de serviço**: certifique-se de que os servlets de migração usem os usuários de serviço apropriados com as permissões necessárias. O usuário do serviço deve ser configurado na configuração ExternalPrincipal para ignorar a proteção nas propriedades `rep:externalId` e `rep:externalPrincipalNames`
* **Operações idempotentes**: crie um código de migração para poder ser executado novamente com segurança
* **Validar em cada etapa**: verifique os resultados após cada etapa de migração antes de continuar

## Protegendo Servlets de Migração {#securing-migration-servlets}

Os servlets de migração têm privilégios elevados para criar e modificar usuários e grupos. É essencial restringir o acesso a esses endpoints para impedir o acesso não autorizado.

### Abordagem recomendada: Autenticação de conta técnica IMS {#recommended-approach-ims-technical-account}

A abordagem recomendada é proteger esses servlets usando a integração do Adobe IMS, permitindo que somente uma conta técnica autorizada acesse-os.

#### Etapa 1: criar uma conta técnica no AEM Developer Console {#create-a-technical-account-in-aem-developer-console}

1. Navegue até [Experience Manager](https://experience.adobe.com/) e depois **Cloud Manager**
1. Selecione seu programa e clique no ambiente em que deseja criar a conta técnica
1. Clique em **Developer Console** no menu de reticências do ambiente
1. No AEM Developer Console, acesse a guia **Integrações**
1. Clique em **Criar nova conta técnica**
1. Forneça um nome para a integração (por exemplo, &quot;Conta do serviço de migração&quot;)
1. Clique em **Criar**
1. Observe os seguintes valores da integração criada:
   * **ID do cliente**
   * **Segredo do cliente**
   * **ID da Conta Técnica** (esta será a ID do usuário acessando seus servlets - formato: `XXXXXXXXXXXXXXXXXXXXXXXX@techacct.adobe.com`)

Para obter instruções detalhadas, consulte [Gerando tokens de acesso para a documentação de APIs do lado do servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md).

Exemplo de código para verificar se o chamador está autorizado:

```
    private boolean isAuthorizedCaller(SlingHttpServletRequest request, 
                                       SlingHttpServletResponse response) {

        Session session = request.getResourceResolver().adaptTo(Session.class);
        String callerId = session != null ? session.getUserID() : null;
               
        if (!ALLOWED_TECHNICAL_ACCOUNT.equals(callerId)) {
            LOG.warn("Unauthorized access attempt by user: '{}' (expected: '{}')", callerId,   ALLOWED_TECHNICAL_ACCOUNT);
            response.setStatus(SlingHttpServletResponse.SC_FORBIDDEN);
            return false;
        }
        
        return true;
    }
```

### Defesa em profundidade: restrições baseadas em IP {#defense-in-depth-ip-based-restrictions}

Como uma camada adicional de segurança, você pode configurar regras de CDN para restringir o acesso a pontos de extremidade de migração por endereço IP. Isso é útil quando as migrações são executadas a partir de uma infraestrutura conhecida.

>[!NOTE]
>
>Restrições de IP por si só não são suficientes. Sempre combine com verificações de autenticação conforme descrito acima.

### Lista de verificação de segurança {#security-checklist}

Antes de implantar servlets de migração para produção:

* [ ] Criar integração IMS no AEM Developer Console
* [ ] Configurar servlets para validar a ID da conta técnica
* [ ] Testar o fluxo de autenticação em ambientes de desenvolvimento/preparo
* [ ] Considere restrições adicionais baseadas em IP no nível de CDN
* [ ] Planeje desabilitar ou remover servlets de migração após a conclusão da migração
* [ ] Auditoria e log de todo o acesso aos pontos de extremidade de migração

>[!IMPORTANT]
>
>Após a conclusão da migração, considere desativar ou remover os servlets de migração da implantação para eliminar qualquer risco potencial à segurança.

## Recursos adicionais {#additional-resources}

* [Sincronização de usuários e grupos para a camada de publicação](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md)
* [Manipulador de Autenticação SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html?lang=pt-BR)
* [Provedor de Identidade Externo](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)
* [Associação de Grupo Dinâmico](https://jackrabbit.apache.org/oak/docs/security/authentication/external/dynamic.html)
