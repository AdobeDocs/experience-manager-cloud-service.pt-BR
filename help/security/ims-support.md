---
title: Suporte IMS do Adobe Experience Manager as a Cloud Service
description: Suporte IMS do Adobe Experience Manager as a Cloud Service
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
source-git-commit: 1e3130578b7e36e5ffd5ad7b04cc7981a95bb291
workflow-type: tm+mt
source-wordcount: '2054'
ht-degree: 97%

---

# Suporte IMS do Adobe Experience Manager as a Cloud Service {#ims-support-for-aem-as-a-cloud-service}

## Introdução {#introduction}

* O AEM as a Cloud Service inclui suporte do Admin Console para instâncias do AEM e autenticação baseada no Adobe Identity Management System (IMS).
* O Admin Console permite que os administradores gerenciem todos os usuários da Experience Cloud de maneira centralizada.
* Usuários e grupos podem ser atribuídos a perfis de produtos associados às instâncias do AEM as a Cloud Service, permitindo que façam logon nessa instância.

>[!TIP]
>
>Veja nosso curso da Experience League, [Configurar acesso ao AEM para administradores](https://experienceleague.adobe.com/?recommended=ExperienceManager-A-1-2020.1.aem&amp;lang=pt-BR), para uma introdução sobre como os usuários se autenticam usando o Adobe IMS para o AEM as a Cloud Service. O curso também explica como os usuários, grupos de usuários e perfis de produtos do Adobe IMS são usados para controlar o acesso ao AEM e seus recursos e funcionalidades. Adobe ID necessário.

>[!NOTE]
>
>No momento, o AEM não oferece suporte à atribuição de grupos a perfis. Em vez disso, os usuários devem ser adicionados individualmente.

## Destaques principais {#key-highlights}

O AEM as a Cloud Service oferece suporte à autenticação do IMS somente para os usuários Autor, Administrador e Desenvolvimento. Ele não oferece suporte para usuários finais externos de sites do cliente como visitantes do site.

* O Admin Console representará clientes como Organizações de IMS, Instâncias de criação e publicação em um ambiente como Instâncias de contexto de produto. Isso permitirá que os administradores do Sistema e do Produto gerenciem o acesso às instâncias.
* Os perfis de produto no Admin Console determinam quais instâncias um usuário pode acessar.
* Os clientes poderão usar seus próprios Provedores de identidade compatíveis com SAML 2 (IDP) para Logon único.
* Somente IDs Enterprise ou Federated para Logon único do cliente serão compatíveis, sem Adobe IDs pessoais.

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
>Uma versão de pré-lançamento **2.4RC1** está disponível com suporte à criação de grupos dinâmicos e pode ser encontrada [aqui](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

Os principais recursos desta versão são a capacidade de mapear dinamicamente novos grupos LDAP para associação de usuários no Admin Console, bem como a criação dinâmica de grupos de usuários.

Mais informações sobre os novos recursos do grupo podem ser encontradas [neste local](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options).

**Documentação da sincronização de usuários**

Consulte a [documentação da UST](https://adobe-apiplatform.github.io/user-sync.py/bp/) para obter mais detalhes.

A Ferramenta de sincronização de usuários precisa se registrar como uma UMAPI do cliente de E/S da Adobe usando o procedimento [aqui](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

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

Quando o Administrador do produto fizer logon no Admin Console, ele verá várias instâncias do Contexto de produto do AEM as a Cloud Service, como mostrado abaixo. Por exemplo, selecione qualquer um dos produtos da página **Visão geral**:

![Logon de instâncias](/help/security/assets/ims6.png)

Você verá uma lista de instâncias existentes:

![Logon de instâncias 2](/help/security/assets/ims7.png)

Em cada instância de Contexto do Produto, haverá instâncias que abrangem os serviços de Autor ou Publicação em todos os ambientes de Produção, Preparo ou Desenvolvimento. Cada instância será associada às funções Perfis de produto ou Cloud Manager. Esses perfis de produto são usados para atribuir acesso a usuários e grupos com os privilégios necessário.

O **Administradores de AEM_xxx** O perfil será usado para conceder privilégios de Administrador na instância de AEM associada enquanto a função **AEM Users_xxx** perfil é usado para adicionar usuários regulares.

Os usuários e grupos adicionados nesse perfil de produto poderão fazer logon nessa instância específica, como mostra o exemplo abaixo:

![Perfil de produto](/help/security/assets/ims8.png)

>[!WARNING]
>
>O **Administradores de AEM** o nome do perfil de produto não deve ser alterado. Alteração do nome do **Administradores de AEM** o perfil de produto removerá os direitos de administrador de todos os usuários atribuídos a esse perfil.

### Fazendo logon no Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**Logon do administrador local**

O AEM pode continuar a oferecer suporte a logons locais para usuários Admin. A tela de logon tem uma opção para entrar localmente:

![Logon local](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**Logon baseado no IMS**

Para outros usuários, o logon baseado no IMS pode ser usado assim que o IMS for configurado na instância. Primeiro, o usuário clicará no botão Fazer logon na Adobe, conforme mostrado abaixo:

![Logon do IMS](/help/security/assets/ims10.png)


>[!NOTE]
>
>Qualquer usuário criado no IMS pode ser criado usando a Adobe ID ou a Federated ID. Se um usuário for configurado usando o Federated ID, ele será autenticado usando o Provedor de identidade da empresa para fazer logon.

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


### Acesso ao Cloud Manager {#accessing-cloud-manager}

Para acessar os ambientes do Cloud Manager ou do AEM as a Cloud Service, você deve ser atribuído aos Perfis do Cloud Manager Product.

Consulte Definições de função para saber mais sobre funções para usuários que controlam a disponibilidade de recursos específicos no Cloud Manager.

>[!NOTE]
>O Cloud Manager tem funções pré-configuradas com permissões apropriadas. Para saber mais sobre cada uma das funções com permissões específicas, tarefas pré-configuradas ou permissões associadas a cada função, consulte [Permissões baseadas em funções](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html?lang=pt-BR).

**Etapas para adicionar um usuário**

1. Adicione um usuário a um perfil específico na tela de um usuário existente ou na tela de um novo usuário.

1. Como alternativa, você também pode adicionar um usuário na tela **Visão geral**, como mostrado na figura abaixo.

   ![ACL3](/help/security/assets/ims23.png)

   >[!NOTE]
   >É possível atribuir mais de um perfil a um usuário, conforme mostrado na figura abaixo.

   ![ACL3](/help/security/assets/ims22.png)


1. Após ser adicionado ao perfil apropriado, você pode acessar os respectivos locatários no Cloud Manager por meio da [Adobe Experience Cloud](https://my.cloudmanager.adobe.com), usando o canto superior direito da interface do usuário.


### Acesso a uma instância no AEM as a Cloud Service {#accessing-instance-cloud-service}

>[!IMPORTANT]
>As etapas mencionadas na seção anterior já devem ter sido concluídas antes de você ter acesso a uma instância no AEM as a Cloud Service.

Para ter acesso a uma instância do AEM no **Admin Console**, você deve ver o Cloud Manager Program e os ambientes dentro do programa na lista de produtos no **Admin Console**.

Por exemplo, na captura de tela abaixo, você verá dois ambientes disponíveis, a saber, *autor de desenvolvimento* e uma *publicação*.

![ACL3](/help/security/assets/ims19.png)

Para obter acesso às instâncias do AEM, o usuário precisará ser adicionado a um grupo do Cloud Service Product apropriado.

Cada instância do autor terá um Perfil de administradores do AEM e usuários do AEM e cada instância de publicação terá um Perfil de usuários do AEM. É possível adicionar outros perfis, conforme necessário.

Para obter acesso de nível administrativo à instância do AEM, adicione o usuário ao Perfil de administradores do AEM para esse Produto específico.
