---
title: Suporte IMS do Adobe Experience Manager as a Cloud Service
description: Suporte IMS do Adobe Experience Manager as a Cloud Service
translation-type: tm+mt
source-git-commit: d51d0e8c57a4c3d3af3083c58a4c1510869c5604

---


# Suporte IMS do Adobe Experience Manager as a Cloud Service {#ims-support-for-aem-as-a-cloud-service}

## Introdução {#introduction}

* O AEM as a Cloud Service inclui suporte do Admin Console para instâncias do AEM e autenticação baseada no Adobe Identity Management System (IMS).
* O Admin Console permite que os administradores gerenciem todos os usuários da Experience Cloud de maneira centralizada.
* Usuários e grupos podem ser atribuídos a perfis de produtos associados às instâncias do AEM as a Cloud Service, permitindo que façam logon nessa instância.

## Destaques principais {#key-highlights}

O AEM as a Cloud Service oferece suporte à autenticação do IMS somente para os usuários Autor, Administrador e Desenvolvimento. Ele não oferece suporte para usuários finais externos de sites do cliente como visitantes do site.

* O Admin Console representará clientes como Organizações de IMS, Instâncias de criação e publicação em um ambiente como Instâncias de contexto de produto. Isso permitirá que os administradores do Sistema e do Produto gerenciem o acesso às instâncias.
* Os perfis de produto no Admin Console determinam quais instâncias um usuário pode acessar.
* Os clientes poderão usar seus próprios Provedores de identidade compatíveis com SAML 2 (IDP) para Logon único.
* Somente IDs empresariais ou federadas para Logon único do cliente serão compatíveis, sem Adobe IDs pessoais.

## Arquitetura {#architecture}

A autenticação do IMS funciona usando o protocolo OAuth entre o AEM e o terminal Adobe IMS. Depois que um usuário é adicionado ao IMS e tem uma Adobe Identity, ele pode fazer logon no serviço de criação do AEM usando as credenciais do IMS.

O fluxo de logon do usuário é mostrado abaixo. O usuário será redirecionado para o IMS e, como opção, para o IDP do cliente para SSO e redirecionado para o AEM.

![Arquitetura do IMS](/help/security/assets/ims1.png)

## Como configurar {#how-to-set-up}

### Integração de organizações ao Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

A integração do cliente ao Adobe Admin Console é um pré-requisito para o uso do Adobe IMS para autenticação do AEM.

Como primeira etapa, os clientes precisam ter uma Organização provisionada no Adobe IMS. Os clientes do Adobe Enterprise são representados como Organizações do IMS no [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html). Este é o portal usado pelos clientes da Adobe para gerenciar os direitos de produto para usuários e grupos.

Os clientes do AEM já devem ter uma Organização provisionada e, como parte do provisionamento do IMS, as instâncias do cliente serão disponibilizadas no Admin Console para gerenciar os direitos e o acesso do usuário.

Depois que um cliente existir como uma Organização do IMS, ele precisará configurar o sistema conforme resumido abaixo:

![Integração do IMS](/help/security/assets/ims2.png)

1. O Administrador do sistema designado recebe um convite para fazer logon no Cloud Manager. Depois de fazer logon no Cloud Manager, os administradores do sistema podem optar por provisionar programas e ambientes do AEM ou navegar até o Admin Console para tarefas Administrativas.
1. O Administrador do sistema alega que um domínio confirma a propriedade do respectivo domínio (por exemplo, acme.com)
1. O Administrador do sistema configura os Diretórios de usuário
1. O Administrador do sistema faz a configuração do IDP no Admin Console para definir o Logon único.
1. O Administrador do AEM gerencia os grupos locais, permissões e privilégios, como de costume.

As noções básicas do Adobe Identity Management, incluindo a configuração do IDP, são contempladas [aqui](https://helpx.adobe.com/br/enterprise/using/set-up-identity.html).

O uso do Enterprise Administration e do Admin Console é contemplado [aqui](https://helpx.adobe.com/br/enterprise/managing/user-guide.html).

### Integração de usuários ao Admin Console {#onboarding-users-in-admin-console}

Existem três maneiras de integrar os usuários dependendo do porte do cliente e de suas preferências: criar usuários manualmente no Admin Console, carregar um arquivo .csv ou sincronizar usuários do Diretório ativo corporativo do cliente.

**Adição manual por meio da interface do usuário do Admin Console**

Usuários e grupos podem ser criados manualmente na interface do usuário do Admin Console. Este método pode ser usado se você não tiver um grande número de usuários para gerenciar. Por exemplo, menos de 50 usuários do AEM ou se você já estiver usando esse método para administrar outros produtos da Adobe, como aplicativos do Analytics, Target ou Creative Cloud.

![Integração de usuários](/help/security/assets/ims3.png)

**Upload de arquivo na interface do usuário do Admin Console**

Para facilitar a criação de usuários, um arquivo `.csv` pode ser carregado para adicionar usuários em massa.

![Upload de arquivo](/help/security/assets/ims4.png)

**Ferramenta de sincronização de usuários**

A Ferramenta de sincronização de usuários (UST, User Sync Tool) permite que nossos clientes corporativos criem e gerenciem usuários da Adobe que utilizam o Diretório ativo. Também funciona para outros serviços de diretório OpenLDAP testados. Os usuários de destino são Administradores de identidade de TI (Diretório corporativo ou Administradores do sistema) que poderão instalar e configurar a ferramenta. A ferramenta de código aberto pode ser personalizada para que os clientes possam modificá-la de acordo com seus próprios requisitos específicos.

Quando a Sincronização de usuários é executada, ela obtém uma lista de usuários do Diretório ativo da organização e a compara com a lista de usuários no Admin Console.  Em seguida, chama a API de gerenciamento de usuários da Adobe para que o Admin Console seja sincronizado com o diretório da organização. O fluxo de mudanças é totalmente unidirecional. As edições realizadas no Admin Console não são enviadas para o diretório.

A ferramenta permite que o administrador do sistema mapeie grupos de usuários no diretório do cliente com a configuração do produto e grupos de usuários no Admin Console.

Para configurar a Sincronização de usuários, a organização precisa criar um conjunto de credenciais da mesma forma que usaria a [API de gerenciamento de usuários](https://www.adobe.io/apis/experienceplatform/umapi-new.html).

![Ferramenta de sincronização de usuários](/help/security/assets/ims5.png)

A Ferramenta de sincronização de usuários é distribuída pelo repositório do Adobe Github [neste local](https://github.com/adobe-apiplatform/user-sync.py/releases/latest).

>[!NOTE]
>
> Uma versão de pré-lançamento **2.4RC1** está disponível com suporte à criação de grupos dinâmicos e pode ser encontrada [aqui](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

Os principais recursos desta versão são a capacidade de mapear dinamicamente novos grupos LDAP para associação de usuários no Admin Console, bem como a criação dinâmica de grupos de usuários.

Mais informações sobre os novos recursos do grupo podem ser encontradas [neste local](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/br/user-manual/advanced_configuration.md#additional-group-options).

**Documentação da sincronização de usuários**

Consulte a [documentação da UST](https://adobe-apiplatform.github.io/user-sync.py/br/) para obter mais detalhes.

A Ferramenta de sincronização de usuários precisa se registrar como uma UMAPI do cliente de E/S da Adobe usando o procedimento [aqui](https://adobe-apiplatform.github.io/umapi-documentation/br/UM_Authentication.html).

A Documentação do console de E/S da Adobe pode ser encontrada [aqui](https://www.adobe.io/apis/cloudplatform/console.html).

A API de gerenciamento de usuários usada pela Ferramenta de sincronização de usuários é contemplada [aqui](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

## Configuração do Adobe Experience as a Cloud Service {#aem-configuration}

>[!NOTE]
>
>A configuração do AEM IMS necessária será configurada automaticamente quando os ambientes e as instâncias do AEM forem provisionados. No entanto, o administrador pode modificá-la de acordo com seus requisitos, usando o método descrito [aqui](/help/implementing/deploying/overview.md).

A configuração do AEM IMS necessária será configurada automaticamente quando os ambientes e as instâncias do AEM forem provisionados.  Os administradores do cliente podem modificar parte da configuração de acordo com seus requisitos

A abordagem geral é configurar o Adobe IMS como provedor OAuth. O **Apache Jackrabbit Oak Default Sync Handler** pode ser modificado da mesma forma que na sincronização de LDAP.

Estas são as principais configurações de OSGI que precisam ser modificadas para alterar propriedades como Associação automática do usuário ou Mapeamentos de grupos.

<!-- Arun to provide list of osgi configs -->

## Como usar {#how-to-use}

### Gerenciamento de produtos e acesso do usuário no Admin Console {#managing-products-and-user-access-in-admin-console}

Quando o Administrador do produto fizer logon no Admin Console, verá várias instâncias do Contexto de produto do AEM Managed Services, como mostrado abaixo:

![Logon de instâncias](/help/security/assets/ims6.png)

Neste exemplo, a organização **AEM-MS-Onboard** tem 32 instâncias que abrangem topologias e ambientes diferentes, como Preparo ou Produção.

![Logon de instâncias 2](/help/security/assets/ims7.png)

Em cada instância do Contexto do produto, haverá Perfis de produto associados. Esses perfis de produto são usados para atribuir acesso a usuários e grupos com o privilégio necessário.

O perfil **Administrator_xxx** será usado para conceder privilégios de Administrador na instância do AEM associada, enquanto o perfil **User_xxx** é usado para adicionar usuários regulares.

Os usuários e grupos adicionados nesse perfil de produto poderão fazer logon nessa instância específica, como mostra o exemplo abaixo:

![Perfil de produto](/help/security/assets/ims8.png)

### Logging into Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**Logon do administrador local**

O AEM pode continuar a oferecer suporte a logons locais para usuários Admin. A tela de logon tem uma opção para entrar localmente:

![Logon local](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**Logon baseado no IMS**

Para outros usuários, o logon baseado no IMS pode ser usado assim que o IMS for configurado na instância. Primeiro, o usuário clicará no botão Fazer logon na Adobe, conforme mostrado abaixo:

![Logon do IMS](/help/security/assets/ims10.png)


>[!NOTE]
> Qualquer usuário criado no IMS pode ser criado usando a Adobe ID ou a Federated ID. Se um usuário estiver configurado usando a Adobe ID, ele será autenticado usando seu Provedor de identidade do Empresa para fazer logon.

Eles serão redirecionados para a tela de logon do IMS e precisarão digitar as credenciais:

![Logon do IMS 2](/help/security/assets/ims11.png)

![Logon do IMS 3](/help/security/assets/ims12.png)

Se um IDP federado for configurado durante a instalação inicial do Admin Console, o usuário será redirecionado ao IDP do cliente para SSO:

![Logon do IMS 4](/help/security/assets/ims13.png)

Após a conclusão da autenticação, o usuário será redirecionado de volta para o AEM e conectado:

![Logon do IMS 5](/help/security/assets/ims14.png)

### Gerenciando permissões e ACLs no Adobe Experience Manager as a Cloud Service {#managing-permissions-in-aem}

As ACLs e permissões continuarão a ser gerenciadas no AEM. Os Grupos de usuários sincronizados do IMS podem ser atribuídos a grupos locais onde as ACLs e os privilégios são definidos.

No exemplo abaixo, adicionamos grupos sincronizados ao grupo local **Dam_Users**, como exemplo.

O usuário faz parte dos seguintes Grupos no IMS:

![ACL1](/help/security/assets/ims15.png)

Quando o usuário faz logon, as Associações de grupo são sincronizadas, como mostrado abaixo:

![ACL2](/help/security/assets/ims16.png)

No AEM, os Grupos de usuários sincronizados do IMS podem ser adicionados como membros a grupos locais existentes, como **Usuários do DAM**.

![ACL3](/help/security/assets/ims17.png)

Como mostrado abaixo, o grupo **AEM-GRP_008** herda as permissões e os privilégios dos **Usuários do DAM**, essa é uma maneira eficaz de gerenciar permissões para grupos sincronizados e também é usada normalmente no método de autenticação baseado em LDAP.

![ACL3](/help/security/assets/ims18.png)


### Acessar o Cloud Manager {#accessing-cloud-manager}

Para poder acessar o Cloud Manager ou o AEM como ambientes de serviço na nuvem, você deve ser atribuído aos Perfis do Produto Cloud Manager.

O Produto Cloud Manager tem os seguintes perfis:

* Proprietário da empresa
* Gerenciador de implantação
* Gerenciador de Programas
* Desenvolvedor
* Integrações

>[!NOTE]
>O Cloud Manager tem funções pré-configuradas com permissões apropriadas. Para saber mais sobre cada uma das funções com permissões específicas, tarefas pré-configuradas ou permissões associadas a cada função, consulte Permissões [com base em](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html)funções.

**Etapas para adicionar um usuário**

1. Adicione um usuário a um perfil específico na tela de um usuário existente ou em uma nova tela de usuário.

1. Como alternativa, você também pode adicionar um usuário na tela **Visão geral** , como mostrado na figura abaixo.

   ![ACL3](/help/security/assets/ims23.png)

   >[!NOTE]
   >Você pode atribuir mais de um perfil a um usuário, conforme mostrado na figura abaixo.

   ![ACL3](/help/security/assets/ims22.png)


1. Depois que você tiver sido adicionado ao perfil apropriado, poderá acessar os respectivos locatários no Cloud Manager por meio da [Adobe Experience Cloud](http://my.cloudmanager.adobe.com) , usando o canto superior direito da interface do usuário.


### Acessar uma instância no AEM como um serviço em nuvem {#accessing-instance-cloud-service}

>[!IMPORTANT]
>As etapas mencionadas na seção anterior já devem ter sido concluídas antes de você receber acesso a uma instância no AEM como um serviço de nuvem.

Para ter acesso a uma instância do AEM no **Admin Console**, você deve ver o Programa do Gerenciador de nuvem e os ambientes dentro do programa na lista do produto no Console **de** administração.

Por exemplo, na captura de tela abaixo, você verá dois ambientes disponíveis, a saber, autor ** dev e uma *publicação*.

![ACL3](/help/security/assets/ims19.png)

Para obter acesso às instâncias do AEM, o usuário precisará ser adicionado a um grupo do Produto de serviço em nuvem apropriado.

Cada instância do autor terá um Perfil de administradores de AEM e usuários de AEM e cada instância de publicação terá um Perfil de usuários de AEM. Você pode adicionar outros perfis, conforme necessário.

Para obter acesso de nível administrativo à instância do AEM, adicione o usuário ao Perfil Administradores do AEM para esse Produto específico.

