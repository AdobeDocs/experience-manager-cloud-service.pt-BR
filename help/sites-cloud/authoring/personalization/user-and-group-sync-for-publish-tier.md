---
title: 'Registro, logon e perfil do usuário '
description: Saiba mais sobre Registro, Logon, Dados do usuário e Sincronização de grupo para AEM as a Cloud Service
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
source-git-commit: c49a70b4048acc4e925c69b7ebbedbf8779bbbc0
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 1%

---

# Registro, logon e perfil do usuário {#registration-login-and-userprofile}

## Introdução {#introduction}

As aplicações web geralmente fornecem recursos de gerenciamento de conta para os usuários finais se registrarem em um site, o que persiste nas informações dos dados do usuário, permitindo que eles façam logon no futuro e desfrutem de uma experiência consistente. Este artigo descreve os seguintes conceitos para AEM as a Cloud Service:

* Registro
* Logon
* Armazenamento de dados do perfil do usuário
* Associação de Grupo
* Sincronização de dados

>[!IMPORTANT]
>
>Para que a funcionalidade descrita neste artigo funcione, o recurso de Sincronização de dados do usuário deve ser ativado, o que, no momento, requer uma solicitação de suporte ao cliente indicando o programa e os ambientes apropriados. Se não estiver ativado, as informações do usuário serão mantidas por apenas um curto período (1 a 24 horas) antes de desaparecer.

## Registro {#registration}

Quando um usuário final se registra em uma conta em um aplicativo AEM, uma conta de usuário é criada no serviço de publicação do AEM, como refletido em um recurso de usuário em `/home/users` no repositório JCR.

Há duas abordagens para a implementação do registro, conforme descrito abaixo.

### AEM gerenciado {#aem-managed-registration}

O código de registro personalizado pode ser gravado com o mínimo de nome de usuário e senha do usuário final, e cria um registro de usuário no AEM que pode ser usado para autenticação durante o logon. As etapas a seguir são normalmente usadas para construir esse mecanismo de registro:

1. Exibir um componente de AEM personalizado que coleta informações de registro
1. Após o envio, um usuário de serviço devidamente provisionado é usado para
   1. Verifique se um usuário existente ainda não existe, usando uma das APIs do UserManager `findAuthorizables()` métodos
   1. Crie um registro de usuário usando uma das APIs do UserManager `createUser()` métodos
   1. Mantenha todos os dados de perfil capturados usando a interface Autorizável `setProperty()` métodos
1. Fluxos opcionais, como exigir que o usuário valide seu email.

### Externo {#external-managed-registration}

Em alguns casos, o registro ou a criação de usuários já aconteceu em uma infraestrutura fora do AEM. Nesse cenário, o registro do usuário é criado em AEM durante o logon.

## Logon {#login}

Depois que um usuário final é registrado no serviço de publicação do AEM, esses usuários podem fazer logon para ter acesso autenticado (usando mecanismos de autorização AEM) e dados persistentes e específicos do usuário, como dados do perfil.

## Implementação {#implementation}

O logon pode ser implementado com as duas abordagens a seguir:

### AEM gerenciado {#aem-managed-implementation}

Os clientes podem gravar seus próprios componentes personalizados. Para saber mais, considere se familiarizar com:

* O [Estrutura de Autenticação Sling](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* E considere [Solicitando a sessão AEM de peritos da Comunidade](http://bit.ly/ATACEFeb15) sobre logon.

### Integração com um provedor de identidade {#integration-with-an-idp}

Os clientes podem se integrar a um IdP (provedor de identidade), que autentica o usuário. As tecnologias de integração incluem SAML e OAuth/SSO, conforme descrito abaixo.

**SAML BASEADO**

Os clientes podem usar a autenticação baseada em SAML por meio de seu SAML IdP preferencial. Ao usar um IdP com AEM, o IdP é responsável por autenticar as credenciais do usuário final e intermediar a autenticação do usuário com o AEM, criar o registro do usuário no AEM conforme necessário e gerenciar a associação do grupo do usuário no AEM, conforme descrito pela asserção SAML.

>[!NOTE]
>
>Somente a autenticação inicial das credenciais do usuário é autenticada pelo IdP e as solicitações subsequentes de AEM são executadas usando um cookie de token de login AEM, desde que o cookie esteja disponível.

Consulte a documentação para obter mais informações sobre o [Manipulador de autenticação SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html).

**OAuth/SSO**

Consulte a [Documentação de Logon único (SSO)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html) para obter informações sobre o uso do Serviço de Manipulador de Autenticação SSO AEM.

O `com.adobe.granite.auth.oauth.provider` A interface pode ser implementada com o provedor OAuth de sua escolha.

### Sessões adesivas e tokens encapsulados {#sticky-sessions-and-encapsulated-tokens}

AEM as a Cloud Service tem sessões adesivas baseadas em cookies ativadas, o que garante que um usuário final seja roteado para o mesmo nó de publicação em cada solicitação. Para aumentar o desempenho, o recurso de token encapsulado é ativado por padrão, de modo que o registro do usuário no repositório não precise ser referenciado em cada solicitação. Se o nó de publicação no qual um usuário final tem uma afinidade for substituído, o registro da ID do usuário estará disponível no novo nó de publicação, conforme descrito na seção de sincronização de dados abaixo.

## Perfil de usuário {#user-profile}

Existem várias abordagens para dados persistentes, dependendo da natureza desses dados.

### Repositório AEM {#aem-repository}

As informações do perfil do usuário podem ser escritas e lidas de duas maneiras:

* Uso do lado do servidor com o `com.adobe.granite.security.user` Interface UserPropertiesManager, que colocará os dados sob o nó do usuário em `/home/users`. Certifique-se de que as páginas exclusivas por usuário não sejam armazenadas em cache.
* Lado do cliente usando o ContextHub, conforme descrito por [a documentação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization).

### Armazenamento de dados de terceiros {#third-party-data-stores}

Os dados do usuário final podem ser enviados a fornecedores terceirizados, como CRMs, e recuperados por meio de APIs, após o logon do usuário para AEM e mantidos (ou atualizados) no nó de perfil do usuário AEM, e usados pelo AEM, conforme necessário.

O acesso em tempo real a serviços de terceiros para recuperar atributos de perfil é possível. No entanto, é importante garantir que isso não afete materialmente o processamento de solicitações no AEM.

## Permissões (grupos de usuários fechados) {#permissions-closed-user-groups}

As políticas de acesso da camada de publicação, também chamadas de Grupos de usuários fechados (CUGs), são definidas no autor do AEM como [descrito aqui](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages). Para restringir determinadas seções ou páginas de um site de alguns usuários, aplique os CUGs conforme necessário usando o autor do AEM, conforme descrito aqui, e replique-os no nível de publicação.

* Se os usuários fizerem logon autenticando com um provedor de identidade (IdP) usando SAML, o manipulador de autenticação identificará as associações de grupo do usuário (que devem corresponder aos CUGs no nível de publicação) e manterá a associação entre o usuário e o grupo por meio de um registro de repositório
* Se o logon for realizado sem a integração do IdP, o código personalizado poderá aplicar os mesmos relacionamentos de estrutura de repositório.

Independentemente do logon, o código personalizado também pode persistir e gerenciar as associações de grupo de um usuário, conforme exigido pelos requisitos exclusivos de uma organização.

## Sincronização de dados {#data-synchronization}

Os usuários finais do site têm uma expectativa de uma experiência consistente em cada solicitação de página da Web ou mesmo quando fazem logon usando um navegador diferente, mesmo que desconhecidos para eles, eles são trazidos para diferentes nós de servidor da infraestrutura do nível de publicação. AEM as a Cloud Service consegue isso sincronizando rapidamente o `/home` hierarquia de pastas (informações de perfil do usuário, associação de grupo etc.) em todos os nós do nível de publicação.

Ao contrário de outras soluções de AEM, a sincronização de associação de usuários e grupos em AEM as a Cloud Service não usa uma abordagem de mensagens ponto a ponto, em vez de implementar uma abordagem de assinatura de publicação que não requer configuração de cliente.

>[!NOTE]
>
>Por padrão, a sincronização de associação de perfil de usuário e grupo não está habilitada e, portanto, os dados não serão sincronizados com ou até mesmo persistirão permanentemente no nível de publicação. Para ativar o recurso, envie uma solicitação ao Suporte ao cliente indicando o programa e os ambientes apropriados.

## Considerações sobre cache {#cache-considerations}

As solicitações HTTP autenticadas podem ser difíceis de armazenar em cache no CDN e no Dispatcher, pois elas têm a possibilidade de um estado específico do usuário ser transferido como parte da resposta da solicitação. O armazenamento em cache inadvertidamente de solicitações autenticadas e sua veiculação em outros navegadores solicitantes pode resultar em experiências incorretas ou até mesmo vazar dados protegidos ou do usuário.

As abordagens para manter a alta capacidade de cache das solicitações e, ao mesmo tempo, oferecer suporte a respostas específicas do usuário incluem:

* AEM Armazenamento em cache sensível a permissões do Dispatcher
* Sling Dynamic Include
* AEM ContextHub
