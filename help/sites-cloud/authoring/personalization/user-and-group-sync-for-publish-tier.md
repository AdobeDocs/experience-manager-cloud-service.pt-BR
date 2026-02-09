---
title: Registro, logon e perfil do usuário
description: Saiba mais sobre registro, logon, dados do usuário e sincronização de grupos no AEM as a Cloud Service
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: 3cc787fe9a0be9a687f7c20744d93f1df4b76f87
workflow-type: tm+mt
source-wordcount: '1487'
ht-degree: 58%

---

# Registro, logon e perfil do usuário {#registration-login-and-userprofile}

## Introdução {#introduction}

Os aplicativos web geralmente fornecem recursos de gerenciamento de conta para os usuários finais se registrarem em um site, o que armazena as informações dos dados do usuário, permitindo que eles façam logon no futuro e desfrutem de uma experiência consistente. Este artigo descreve os seguintes conceitos do AEM as a Cloud Service:

* Registro
* Logon
* Armazenamento de dados do perfil do usuário
* Associação de grupo
* Sincronização de dados

## Registro {#registration}

Quando um usuário final registra uma conta em um aplicativo do AEM, uma conta de usuário é criada no serviço de publicação do AEM, conforme refletido em um recurso de usuário em `/home/users`, no repositório JCR.

Há duas abordagens para a implementação do registro, conforme descrito abaixo.

### AEM Managed {#aem-managed-registration}

Pode-se escrever um código de registro personalizado que contenha, no mínimo, o nome de usuário e a senha do usuário. Isso criará um registro de usuário no AEM, que pode ser usado para autenticação durante o logon. As etapas a seguir são normalmente usadas para criar esse mecanismo de registro:

1. Exibir um componente personalizado do AEM que coleta informações de registro
1. Após o envio, um usuário de serviço devidamente provisionado é usado para:
   1. Verificar se um usuário já não existe, usando um dos métodos `findAuthorizables()` da API do UserManager
   1. Criar um registro de usuário usando um dos métodos `createUser()` da API do UserManager
   1. Armazenar todos os dados de perfil capturados usando os métodos `setProperty()` da interface do Authorizable
1. Fluxos opcionais, como exigir que o usuário valide seu email.

**Pré-requisito:**

Para que a lógica descrita acima funcione corretamente, habilite a [sincronização de dados](#data-synchronization-data-synchronization) enviando
uma solicitação ao Suporte ao cliente indicando o programa e os ambientes apropriados.

### Externo {#external-managed-registration}

Em alguns casos, o registro ou a criação de usuários já aconteceu em uma infraestrutura fora do AEM. Nesse cenário, o registro do usuário é criado no AEM durante o logon.

## Logon {#login}

Depois que um usuário final é registrado no serviço de publicação do AEM, esses usuários podem fazer logon para obter acesso autenticado (usando mecanismos de autorização do AEM) e dados persistentes e específicos do usuário, como dados de perfil.

## Implementação {#implementation}

O logon pode ser implementado com as duas abordagens a seguir:

### AEM Managed {#aem-managed-implementation}

Os clientes podem gravar seus próprios componentes personalizados. Para saber mais, familiarize-se com:

* A [estrutura de autenticação do Sling](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* E considere [fazer perguntas na sessão dos especialistas da comunidade do AEM](https://bit.ly/ATACEFeb15) sobre logon.

**Pré-requisito:**

Para que a lógica descrita acima funcione corretamente, habilite a [sincronização de dados](#data-synchronization-data-synchronization) enviando
uma solicitação ao Suporte ao cliente indicando o programa e os ambientes apropriados.

### Integração com um provedor de identidade {#integration-with-an-idp}

Os clientes podem se integrar a um IdP (provedor de identidade), que autentica o usuário. As tecnologias de integração incluem SAML e OAuth/SSO, conforme descrito abaixo.

**BASEADA EM SAML**

Os clientes podem usar a autenticação baseada em SAML por meio de seu IdP de SAML preferencial. Ao usar um IdP com o AEM, ele é responsável por autenticar as credenciais do usuário e intermediar a autenticação do usuário com o AEM, criar o registro do usuário no AEM conforme necessário e gerenciar a associação de grupo do usuário no AEM, conforme descrito pela asserção do SAML.

>[!NOTE]
>
>Somente a autenticação inicial das credenciais do usuário é realizada pelo IdP. As solicitações subsequentes ao AEM são executadas usando um cookie de token de logon do AEM, desde que o cookie esteja disponível.

Consulte a documentação para obter mais informações sobre o [Manipulador de autenticação SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html?lang=pt-BR).

**OAuth/SSO**

Consulte a [Documentação de Logon único (SSO)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html?lang=pt-BR) para obter informações sobre o uso do Manipulador de autenticação SSO do AEM.

A interface `com.adobe.granite.auth.oauth.provider` pode ser implementada com o provedor OAuth de sua escolha.

**Pré-requisito:**

Como prática recomendada, sempre confie no idP (Identity Provider, Provedor de identidade) como um único ponto de verdade ao armazenar dados específicos do usuário. Se as informações adicionais do usuário forem armazenadas no repositório local, que não faz parte do idP, habilite a [sincronização de dados](#data-synchronization-data-synchronization) enviando uma solicitação ao Suporte ao Cliente indicando o programa e os ambientes apropriados. Além da [sincronização de dados](#data-synchronization-data-synchronization), no caso do provedor de autenticação SAML, verifique se a [associação de grupo dinâmico](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0) está habilitada.

### Sessões adesivas e tokens encapsulados {#sticky-sessions-and-encapsulated-tokens}

O AEM as a Cloud Service habilita sessões adesivas baseadas em cookies, garantindo que um usuário final seja roteado para o mesmo nó de publicação em cada solicitação. Em casos específicos, como picos de tráfego do usuário, o recurso de token encapsulado pode aumentar o desempenho, de modo que o registro do usuário no repositório não precise ser referenciado em cada solicitação. Se o nó de publicação com o qual um usuário final tem afinidade for substituído, o registro da ID do usuário estará disponível no novo nó de publicação, conforme descrito na seção [sincronização de dados](#data-synchronization-data-synchronization) abaixo.

Para aproveitar o recurso de token encapsulado, envie uma solicitação ao Suporte ao cliente indicando o programa e os ambientes apropriados. Mais importante ainda, o token encapsulado não pode ser habilitado sem a [sincronização de dados](#data-synchronization-data-synchronization) e deve ser habilitado em conjunto. Portanto, analise cuidadosamente o caso de uso antes de ativar e verifique se o recurso é essencial.

## Perfil de usuário {#user-profile}

Existem várias abordagens para dados persistentes, dependendo da natureza desses dados.

### Repositório do AEM {#aem-repository}

As informações do perfil do usuário podem ser escritas e lidas de duas maneiras:

* Pelo uso do servidor com a interface `com.adobe.granite.security.user` do UserPropertiesManager, que colocará os dados sob o nó do usuário em `/home/users`. Certifique-se de que as páginas exclusivas por usuário não sejam armazenadas em cache.
* Pelo lado do cliente usando o ContextHub, conforme descrito na [documentação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html#personalization).

**Pré-requisito:**

Para que a lógica de persistência de perfil de usuário do lado do servidor funcione corretamente, habilite a [sincronização de dados](#data-synchronization-data-synchronization) enviando
uma solicitação ao Suporte ao cliente indicando o programa e os ambientes apropriados.

### Armazenamento de dados de terceiros {#third-party-data-stores}

Os dados do usuário final podem ser enviados a fornecedores terceirizados, como CRMs, recuperados por meio de APIs após o logon do usuário no AEM, armazenados (ou atualizados) no nó de perfil do usuário e usados pelo AEM conforme necessário.

É possível obter acesso em tempo real a serviços de terceiros para recuperar atributos de perfil. No entanto, é importante garantir que isso não afete diretamente o processamento de solicitações no AEM.

**Pré-requisito:**

Para que a lógica descrita acima funcione corretamente, habilite a [sincronização de dados](#data-synchronization-data-synchronization) enviando
uma solicitação ao Suporte ao cliente indicando o programa e os ambientes apropriados.

## Permissões (grupos de usuários fechados) {#permissions-closed-user-groups}

As políticas de acesso do nível de publicação, também chamadas de Grupos de Usuários Fechados (CUGs), são definidas no autor do AEM, consulte [Criação de um Grupo de Usuários Fechado](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html#applying-your-closed-user-group-to-content-pages). Para restringir determinadas seções ou páginas de um site para alguns usuários, aplique os CUGs conforme necessário usando o autor do AEM, conforme descrito aqui, e replique-os no nível de publicação.

* Se os usuários fizerem logon com autenticação através de um provedor de identidade (IdP) usando SAML, o manipulador de autenticação identificará as associações de grupo do usuário (que devem corresponder aos CUGs no nível de publicação) e manterá a associação entre o usuário e o grupo por meio de um registro de repositório
* Se o logon for realizado sem a integração de um IdP, um código personalizado poderá aplicar os mesmos relacionamentos de estrutura do repositório.

Independentemente do logon, um código personalizado também pode manter e gerenciar as associações de grupo de um usuário, conforme exigido pelos requisitos exclusivos de uma organização.

## Sincronização de dados {#data-synchronization}

Os usuários finais do site têm uma expectativa de experiência consistente em cada solicitação de página da Web ou mesmo ao fazerem logon usando um navegador diferente; mesmo sem o conhecimento deles, eles são trazidos para diferentes nós de servidor da infraestrutura do nível de publicação. O AEM as a Cloud Service consegue isso sincronizando rapidamente a hierarquia de pastas `/home` (informações de perfil do usuário, associação de grupo etc.) em todos os nós do nível de publicação.

Ao contrário de outras soluções do AEM, a sincronização de usuários e associações de grupos no AEM as a Cloud Service não usa uma abordagem de mensagens ponto a ponto. Em vez disso, ela implementa uma abordagem de assinatura de publicação que não requer configuração de clientes.

>[!NOTE]
>
>Por padrão, a sincronização de perfis de usuário e associações de grupos não está habilitada e, portanto, os dados não serão sincronizados ou mantidos permanentemente no nível de publicação. Para habilitar o recurso, envie uma solicitação ao Suporte ao cliente indicando o programa e os ambientes apropriados.

>[!IMPORTANT]
>
>Teste a implementação em escala antes de habilitar a sincronização de dados no ambiente de produção. Dependendo do caso de uso e dos dados persistentes, podem ocorrer alguns problemas de consistência e latência.

### Requisitos de código personalizado e migração {#custom-code-and-migration-requirements}

Os requisitos a seguir se aplicam apenas nos casos em que o código personalizado é usado para criar usuários locais ou grupos locais. Quando a Sincronização de dados está ativada, esse código personalizado deve ser atualizado para criar usuários externos e grupos externos com associação de grupo dinâmico.

**Etapas Necessárias:**

* **Modificações no código personalizado**: qualquer lógica personalizada responsável por criar usuários ou grupos deve ser atualizada para:

   * Criar usuários externos definindo a propriedade `rep:externalId`
   * Criar grupos externos definindo a propriedade `rep:externalId`
   * Implementar a associação de grupo dinâmica usando a propriedade `rep:externalPrincipalNames`, em vez de usar relações diretas entre usuário e grupo

* **Migração de dados pré-existentes**: todos os usuários e grupos locais existentes precisam ser migrados para o modelo de identidade externo para que a Sincronização de Dados seja habilitada em ambientes de produção.

Para obter orientação técnica detalhada sobre como atualizar implementações personalizadas e migrar usuários e grupos existentes, consulte [Migrando para Identidade Externa e Associação de Grupo Dinâmico](/help/security/migrating-to-external-identity.md).

## Considerações sobre cache {#cache-considerations}

As solicitações HTTP autenticadas podem ser difíceis de armazenar em cache no CDN e no Dispatcher, pois elas apresentam a possibilidade de um estado específico do usuário ser transferido como parte da resposta da solicitação. O armazenamento inadvertido de solicitações autenticadas em cache e sua veiculação em outros navegadores solicitantes pode resultar em experiências incorretas ou até mesmo no vazamento de dados do usuário ou protegidos.

As abordagens para manter uma alta capacidade de cache das solicitações e, ao mesmo tempo, permitir respostas específicas do usuário incluem:

* Armazenamento em cache sensível a permissões do AEM Dispatcher
* Sling Dynamic Include
* AEM ContextHub
