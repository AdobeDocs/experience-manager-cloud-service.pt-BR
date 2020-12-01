---
title: 'Registro, login e Perfil do usuário '
description: Saiba mais sobre Registro, Logon e Perfil de usuário na Camada de publicação
translation-type: tm+mt
source-git-commit: 2c00c3723c3c84365044b5cd2fe6779de0360736
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---


# Registro, login e Perfil do usuário {#registration-login-and-userprofile}

## Introdução {#introduction}

Muitas vezes, o Aplicação web fornece recursos de gerenciamento de conta para que os usuários finais se registrem em um site, o que persiste em suas informações de perfil do usuário, permitindo que eles façam logon no futuro e desfrutem de uma experiência consistente. Este artigo descreve:

* Registro
* Logon
* Armazenamento de dados de perfil do usuário
* Associação de grupo
* Sincronização de dados

>[!IMPORTANT]
>
>Para que a funcionalidade descrita neste artigo funcione, o recurso Sincronização de dados do usuário deve estar ativado, o que, no momento, requer uma solicitação ao suporte ao cliente indicando o programa e os ambientes apropriados. Se não estiver ativado, as informações do usuário serão mantidas por apenas um curto período (de 1 a 24 horas) antes de desaparecer.

## Registro {#registration}

Quando um usuário final se registra para uma conta em um aplicativo AEM, uma conta de usuário é criada no serviço de publicação de AEM, como refletido em um recurso de usuário em `/home/users` no repositório JCR.

Há duas abordagens para a implementação do registro, como descrito abaixo.

### AEM gerenciado {#aem-managed-registration}

O código de registro personalizado pode ser gravado com o mínimo de nome de usuário e senha do usuário final e cria um registro de usuário no AEM que pode ser usado para autenticação durante o logon. Normalmente, as etapas a seguir são usadas para construir esse mecanismo de registro:

1. Exibir um componente AEM personalizado que coleta informações de registro
1. Após o envio, um usuário de serviço devidamente provisionado é usado para
   1. Verifique se um usuário existente ainda não existe, usando um dos métodos `findAuthorizables()` da API do UserManager
   1. Crie um registro de usuário usando um dos métodos `createUser()` da API do UserManager
   1. Persistir em qualquer dado de perfil capturado usando os métodos `setProperty()` da interface Autorizável
1. Fluxos opcionais, como exigir que o usuário valide seus emails.

### Externo {#external-managed-registration}

Em alguns casos, o registro ou a criação de usuários já aconteceram em infraestrutura fora da AEM. Nesse cenário, o registro do usuário é criado em AEM durante o logon.

## Logon {#login}

Depois que um usuário final é registrado no serviço de publicação de AEM, esses usuários podem fazer logon para ter acesso autenticado (usando mecanismos de autorização AEM) e dados persistentes e específicos do usuário, como dados do perfil.

## Implementação {#implementation}

O logon pode ser implementado com as duas abordagens a seguir:

### AEM gerenciado {#aem-managed-implementation}

Os clientes podem escrever seus próprios componentes personalizados. Para saber mais, considere se familiarizar com:

* A [Estrutura de Autenticação Sling](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* E considere [perguntar à sessão AEM Community Experts](http://bit.ly/ATACEFeb15) sobre o logon.

### Integração com um provedor de identidade {#integration-with-an-idp}

Os clientes podem se integrar a um IdP (provedor de identidade), que autentica o usuário. As tecnologias de integração incluem SAML e OAuth/SSO, conforme descrito abaixo.

**COM BASE EM SAML**

Os clientes podem usar a autenticação baseada em SAML por meio de seu IdP SAML preferencial. Ao usar um IdP com AEM, o IdP é responsável por autenticar as credenciais do usuário final e intermediar a autenticação do usuário com AEM, criar o registro do usuário em AEM conforme necessário e gerenciar a associação do usuário ao grupo em AEM, conforme descrito pela asserção SAML.

>[!NOTE]
>
>Somente a autenticação inicial das credenciais do usuário é autenticada pelo IdP, e as solicitações subsequentes para AEM são executadas usando um cookie de token de login AEM, desde que o cookie esteja disponível.

Consulte a documentação para obter mais informações sobre o [SAML 2.0 Authentication Handler](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=en#saml-authentication-handler).

**OAuth/SSO**

Consulte a documentação [Logon único (SSO)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html) para obter informações sobre como usar o Serviço de Manipulador de Autenticação SSO AEM.

A interface `com.adobe.granite.auth.oauth.provider` pode ser implementada com o provedor OAuth de sua escolha.

### Sessões adesivas e Tokens Encapsulados {#sticky-sessions-and-encapsulated-tokens}

AEM como um Cloud Service tem sessões adesivas baseadas em cookies ativadas, o que garante que um usuário final seja roteado para o mesmo nó de publicação em cada solicitação. Para aumentar o desempenho, o recurso de token encapsulado é ativado por padrão, de modo que o registro do usuário no repositório não precisa ser referenciado em cada solicitação. Se o nó de publicação no qual um usuário final tem uma afinidade for substituído, seu registro de ID de usuário estará disponível no novo nó de publicação, conforme descrito na seção de sincronização de dados abaixo.

## Perfil de usuário {#user-profile}

Existem várias abordagens para dados persistentes, dependendo da natureza desses dados.

### Repositório AEM {#aem-repository}

As informações de perfil do usuário podem ser gravadas e lidas de duas formas:

* Uso pelo lado do servidor com a interface UserPropertiesManager da interface `com.adobe.granite.security.user`, que colocará os dados sob o nó do usuário em `/home/users`. Verifique se as páginas exclusivas por usuário não estão em cache.
* Do lado do cliente usando o ContextHub, conforme descrito por [a documentação](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization).

### Armazenamentos de dados de terceiros {#third-party-data-stores}

Os dados do usuário final podem ser enviados a fornecedores terceirizados, como CRMs, e recuperados por meio de APIs após o logon do usuário para AEM e persistirem (ou atualizem) no nó do perfil do usuário AEM, e usados por AEM conforme necessário.

O acesso em tempo real a serviços de terceiros para recuperar atributos de perfil é possível, no entanto, é importante garantir que isso não afete materialmente o processamento de solicitações em AEM.

## Permissões (Grupos de usuários fechados) {#permissions-closed-user-groups}

As políticas de acesso da camada de publicação, também chamadas de Grupos de usuários fechados (CUGs), são definidas no autor do AEM como [descrito aqui](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages). Para restringir determinadas seções ou páginas de um site de alguns usuários, aplique os CUGs conforme necessário usando o autor do AEM, conforme descrito aqui, e replique-os na camada de publicação.

* Se os usuários fizerem logon autenticando com um provedor de identidade (IdP) usando SAML, o manipulador de autenticação identificará as associações de grupo do usuário (que devem corresponder aos CUGs na camada de publicação) e persistirá a associação entre o usuário e o grupo por meio de um registro de repositório
* Se o logon for realizado sem a integração do IdP, o código personalizado poderá aplicar os mesmos relacionamentos de estrutura de repositório.

Independentemente do logon, o código personalizado também pode persistir e gerenciar as associações de grupo de um usuário, conforme exigido pelos requisitos exclusivos de uma organização.

## Sincronização de dados {#data-synchronization}

Os usuários finais do site têm uma expectativa de uma experiência consistente em cada solicitação de página da Web ou mesmo quando fazem logon usando um navegador diferente, mesmo que desconhecidos para eles, eles são direcionados para diferentes nós de servidor da infraestrutura da camada de publicação. AEM como um Cloud Service consegue isso sincronizando rapidamente a hierarquia de pastas `/home` (informações do perfil do usuário, associação de grupo etc.) em todos os nós da camada de publicação.

Ao contrário de outras soluções AEM, a sincronização de associação de usuários e grupos em AEM como Cloud Service não usa uma abordagem de mensagens ponto a ponto, em vez de implementar uma abordagem de assinatura de publicação que não requer configuração do cliente.

>[!NOTE]
>
>Por padrão, o perfil do usuário e a sincronização de associação de grupo não estão ativados e, portanto, os dados não serão sincronizados nem persistidos permanentemente na camada de publicação. Para ativar o recurso, envie uma solicitação ao Suporte ao cliente indicando o programa e os ambientes apropriados.

## Considerações sobre cache {#cache-considerations}

As solicitações HTTP autenticadas podem ser difíceis de armazenar em cache tanto no CDN quanto no Dispatcher, já que elas têm a possibilidade de o estado específico do usuário ser transferido como parte da resposta da solicitação. O armazenamento inadvertidamente em cache de solicitações autenticadas e sua disponibilização para outros navegadores solicitantes pode resultar em experiências incorretas ou mesmo vazar dados protegidos ou do usuário.

As abordagens para manter a alta capacidade de cache das solicitações e, ao mesmo tempo, suportar respostas específicas do usuário incluem:

* AEM Dispatcher Permissões para armazenamento em cache sensível
* Inclusão dinâmica do Sling
* AEM ContextHub