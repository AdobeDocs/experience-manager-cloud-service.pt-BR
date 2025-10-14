---
title: Suporte IMS do Adobe Experience Manager as a Cloud Service
description: Suporte do Sistema de gerenciamento de imagens para o Adobe Experience Manager as a Cloud Service.
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
feature: Security
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 85%

---

# Suporte IMS do Adobe Experience Manager as a Cloud Service {#ims-support-for-aem-as-a-cloud-service}

## Introdução {#introduction}

* O AEM as a Cloud Service inclui suporte do Admin Console para instâncias do AEM e autenticação baseada no Adobe Identity Management System (IMS).
* O Admin Console permite que os administradores gerenciem todos os usuários da Experience Cloud de maneira centralizada.
* Usuários e grupos podem ser atribuídos a perfis de produtos associados a uma instância do AEM as a Cloud Service, permitindo que façam logon nessa instância.

>[!TIP]
>
>Consulte [Configuração do acesso ao AEM para administradores](https://experienceleague.adobe.com/?lang=pt-br&recommended=ExperienceManager-A-1-2020.1.aem&lang=pt-BR) para obter uma introdução sobre como os usuários se autenticam usando o Adobe IMS para o AEM as a Cloud Service. Saiba também como usuários do Adobe IMS, grupos de usuários e perfis de produtos são usados para controlar o acesso ao AEM e seus recursos e funcionalidades. Adobe ID necessário.

## Destaques principais {#key-highlights}

O AEM as a Cloud Service oferece suporte à autenticação IMS somente para os usuários Autor, Administrador e Desenvolvedor. Ele não oferece suporte para usuários finais externos de sites do cliente como visitantes do site.

* O Admin Console representará clientes como Organizações IMS, Autores e Instâncias de publicação em um ambiente como Instâncias de contexto de produto. Essa representação permitirá que os administradores de sistema e de produto gerenciem o acesso às instâncias.
* Os perfis de produto no Admin Console determinam quais instâncias um usuário pode acessar.
* Os clientes poderão usar seus próprios Provedores de identidade (IDP, na sigla em inglês) compatíveis com SAML 2 para Logon único.
* Somente IDs empresariais ou federadas para Logon único do cliente serão compatíveis, sem Adobe IDs pessoais.

## Arquitetura {#architecture}

A autenticação do IMS funciona usando o protocolo OAuth entre o AEM e o terminal Adobe IMS. Depois que um usuário é adicionado ao IMS e tem uma Adobe Identity, ele pode fazer logon no serviço de criação do AEM usando as credenciais do IMS.

O fluxo de logon do usuário é mostrado abaixo. O usuário será redirecionado para o IMS e, como opção, para o IDP do cliente para o SSO e redirecionado de volta para o AEM.

![Arquitetura IMS](/help/security/assets/ims1.png)

## Como configurar {#how-to-set-up}

### Integração de organizações ao Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

A integração do cliente ao Adobe Admin Console é um pré-requisito para o uso do Adobe IMS para autenticação do AEM.

Como primeira etapa, os clientes devem ter uma Organização que seja provisionada no Adobe IMS. Os clientes do Adobe Enterprise são representados como Organizações IMS no [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html). Essa área é o portal usado pelos clientes da Adobe para gerenciar os direitos de seus produtos para usuários e grupos.

Os clientes do AEM já devem ter uma Organização provisionada e, como parte do provisionamento do IMS, as instâncias do cliente são disponibilizadas no Admin Console para gerenciar os direitos e o acesso do usuário.

Depois que um cliente passa a existir como uma Organização IMS, será necessário configurar o sistema conforme resumido a seguir:

![Integração do IMS](/help/security/assets/ims2.png)

1. O administrador do sistema designado recebe um convite para fazer logon no Cloud Manager. Depois de fazer logon no Cloud Manager, os administradores do sistema podem optar por provisionar programas e ambientes AEM ou navegar até o Admin Console para tarefas Administrativas.
1. O Administrador do sistema alega que um domínio confirma a propriedade do respectivo domínio (por exemplo, acme.com)
1. O Administrador do sistema configura os Diretórios de usuário.
1. O Administrador do sistema faz a configuração do IDP no Admin Console para configurar o Logon único.
1. O Administrador do AEM gerencia os grupos locais, permissões e privilégios, como de costume.

As noções básicas do Adobe Identity Management, incluindo a configuração do IDP, são abordadas em [Configurar identidade e logon único](https://helpx.adobe.com/br/enterprise/using/set-up-identity.html).

A Administração e o uso do Admin Console de empresas são abordados em [Bem-vindo ao guia de administração de empresas e equipes](https://helpx.adobe.com/br/enterprise/admin-guide.html).

### Integração de usuários ao Admin Console {#onboarding-users-in-admin-console}

Há três maneiras de integrar usuários. Cada método depende do tamanho do cliente e de sua preferência. É possível criar usuários manualmente no Admin Console, fazer upload de um arquivo .csv ou sincronizar usuários do diretório principal corporativo do cliente.

**Adição manual por meio da interface do usuário do Admin Console**

Usuários e grupos podem ser criados manualmente na interface do usuário do Admin Console. Esse método pode ser usado se não houverem muitos usuários para gerenciar. Por exemplo, menos de 50 usuários do AEM ou se você já estiver usando esse método para administrar outros produtos da Adobe, como aplicativos do Analytics, do Target ou da Creative Cloud.

![Integração de usuários](/help/security/assets/ims3.png)

**Upload de arquivo na interface do usuário do Admin Console**

Para facilitar a criação de usuários, um arquivo `.csv` pode ser carregado para adicionar usuários em massa.

![Upload de arquivo](/help/security/assets/ims4.png)

**Ferramenta de sincronização de usuários**

A Ferramenta de Sincronização de Usuários (UST, sigla em inglês) permite que nossos clientes corporativos criem e gerenciem usuários da Adobe usando o diretório principal. Isso também funciona para outros serviços de diretório OpenLDAP testados. Os usuários de destino são administradores de identidade de TI (diretório corporativo ou administradores do sistema) que poderão instalar e configurar a ferramenta. A ferramenta de código aberto pode ser personalizada para que os clientes possam modificá-la de acordo com seus próprios requisitos específicos.

Quando a Sincronização de usuários é executada, ela obtém uma lista de usuários do Diretório principal da organização e a compara com a lista de usuários no Admin Console. Em seguida, chama a API User Management da Adobe para que o Admin Console seja sincronizado com o diretório da organização. O fluxo de mudanças é totalmente unidirecional. As edições realizadas no Admin Console não são enviadas para o diretório.

A ferramenta permite que o administrador do sistema mapeie grupos de usuários no diretório do cliente com a configuração do produto e grupos de usuários no Admin Console.

Para configurar a Sincronização de usuários, a organização precisa criar um conjunto de credenciais da mesma forma que usaria a [API User Management](https://developer.adobe.com/umapi/).

![Ferramenta de sincronização de usuários](/help/security/assets/ims5.png)

A Ferramenta de sincronização de usuários é distribuída pelo repositório do Github da Adobe [neste local](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.9.0rc2).

>[!NOTE]
>
>Uma versão de pré-lançamento **2.4RC1** está disponível com suporte à criação de grupos dinâmicos em [Ferramenta de Sincronização de Usuários v2.4rc1 no GitHub](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

Os principais recursos desta versão são a capacidade de mapear dinamicamente novos grupos LDAP para associações de usuários no Admin Console, bem como a criação dinâmica de grupos de usuários.

Mais informações sobre os novos recursos de grupo podem ser encontradas em [Ferramenta de Sincronização de Usuário do Adobe - Opções de Grupo Adicionais](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options).

**Documentação da sincronização de usuários**

Consulte:

* [Documentação da UST](https://adobe-apiplatform.github.io/user-sync.py/bp/)

* a Ferramenta de Sincronização de Usuários deve se registrar como uma UMAPI de cliente Adobe Developer usando o procedimento de [Autenticação para Acesso à API](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)

* a [Documentação do Adobe Developer Console](https://developer.adobe.com/developer-console/)

* a [API de Gerenciamento de Usuário usada pela Ferramenta de Sincronização de Usuário](https://adobe-apiplatform.github.io/user-sync.py/en/)

## Configuração do Adobe Experience as a Cloud Service {#aem-configuration}

>[!NOTE]
>
>A configuração IMS do AEM necessária será configurada automaticamente quando os ambientes e as instâncias do AEM forem provisionados. No entanto, o administrador pode modificá-la de acordo com seus requisitos, consulte [Implantação no AEM as a Cloud Service](/help/implementing/deploying/overview.md).

A configuração IMS do AEM necessária será configurada automaticamente quando os ambientes e as instâncias do AEM forem provisionados. Os administradores do cliente podem modificar parte da configuração de acordo com seus requisitos

A abordagem geral é configurar o Adobe IMS como provedor OAuth. O **Apache Jackrabbit Oak Default Sync Handler** pode ser modificado da mesma forma que na sincronização de LDAP.

Abaixo estão as principais configurações de OSGI que devem ser modificadas para alterar propriedades como associação automática de usuários ou mapeamentos de grupos.

<!-- Arun to provide list of osgi configs -->

## Como usar {#how-to-use}

### Gerenciamento de produtos e acesso do usuário no Admin Console {#managing-products-and-user-access-in-admin-console}

Quando o administrador do produto fizer logon no Admin Console, ele verá várias instâncias do Contexto de produto do AEM as a Cloud Service, como mostrado abaixo. Por exemplo, selecione qualquer um dos produtos da página **Visão geral**:

![Logon de instâncias](/help/security/assets/ims6.png)

Você verá uma lista de instâncias já existentes:

![Logon de instâncias 2](/help/security/assets/ims7.png)

Em cada instância de Contexto de produto, haverá instâncias que abrangem os serviços de autor ou publicação nos ambientes de produção, preparo ou desenvolvimento. Cada instância está associada a funções de perfis de produto ou do Cloud Manager. Esses perfis de produto são usados para atribuir acesso a usuários e grupos com os privilégios necessários.

O perfil **Administradores_xxx do AEM** será usado para conceder privilégios de Administrador na instância do AEM associada, enquanto o perfil **Usuários_xxx do AEM** é usado para adicionar usuários normais.

Todos os usuários e grupos adicionados a esse perfil de produto podem fazer logon nessa instância, conforme mostrado no exemplo abaixo:

![Perfil de produto](/help/security/assets/ims8.png)

>[!WARNING]
>
>Não altere o nome do perfil de produto dos **Administradores do AEM**. A alteração do nome do perfil de produto dos **Administradores do AEM** removerá os direitos de administrador de todos os usuários atribuídos a esse perfil.

### Fazendo logon no Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**Logon do administrador local**

O AEM pode continuar a oferecer suporte a logons locais para usuários Admin. A tela de logon permite fazer logon localmente:

![Logon local](/help/security/assets/ims9.png)

<!-- the above image must be updated for skyline -->

**Logon baseado em IMS**

Para outros usuários, o logon baseado em IMS é usado após a configuração do IMS na instância. O usuário clica no botão Fazer logon com a Adobe, conforme mostrado abaixo:

![Logon do IMS](/help/security/assets/ims10.png)


>[!NOTE]
>
>Qualquer usuário criado no IMS pode ser criado usando a Adobe ID ou a Federated ID. Se um usuário for configurado usando o Federated ID, ele será autenticado usando o Provedor de identidade da empresa para fazer logon.

Eles são redirecionados para a tela de logon do IMS e devem inserir suas credenciais:

![Logon do IMS 2](/help/security/assets/ims11.png)

![Logon do IMS 3](/help/security/assets/ims12.png)

Se um IDP federado for configurado durante a configuração inicial do Admin Console, o usuário será redirecionado para o IDP do cliente para o SSO:

![Logon do IMS 4](/help/security/assets/ims13.png)

Após a conclusão da autenticação, o usuário será redirecionado de volta para o AEM e conectado:

![Logon do IMS 5](/help/security/assets/ims14.png)

### Gerenciando permissões e ACLs no Adobe Experience Manager as a Cloud Service {#managing-permissions-in-aem}

ACLs e permissões continuam a ser gerenciadas no AEM. Os grupos de usuários sincronizados do IMS podem ser atribuídos a grupos locais onde ACLs e privilégios são definidos.

No exemplo abaixo, adicionamos grupos sincronizados ao grupo local **Dam_Users**, como exemplo.

O usuário faz parte dos seguintes Grupos no IMS:

![ACL1](/help/security/assets/ims15.png)

Quando o usuário faz logon, as Associações de grupo são sincronizadas, como mostrado abaixo:

![ACL2](/help/security/assets/ims16.png)

No AEM, os Grupos de usuários sincronizados do IMS podem ser adicionados como membros a grupos locais existentes, como **Usuários do DAM**.

![ACL3](/help/security/assets/ims17.png)

Como mostrado abaixo, o grupo **AEM-GRP_008** herda as permissões e os privilégios de **Usuários DAM**. Essa herança é uma maneira eficaz de gerenciar permissões para grupos sincronizados e geralmente é usada no método de autenticação baseado em LDAP.

![ACL3](/help/security/assets/ims18.png)


### Acesso ao Cloud Manager {#accessing-cloud-manager}

Para acessar o Cloud Manager ou os ambientes do AEM as a Cloud Service, é necessário estar atribuído aos Perfis do produto do Cloud Manager.

Consulte Definições de função se quiser saber mais sobre funções para usuários que controlam a disponibilidade de recursos específicos no Cloud Manager.

>[!NOTE]
>O Cloud Manager tem funções pré-configuradas com permissões apropriadas. Para saber mais sobre cada uma das funções com permissões específicas, tarefas pré-configuradas ou permissões associadas a cada função, consulte [Permissões baseadas em funções](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions).

**Etapas para adicionar um usuário**

1. Adicione um usuário a um perfil específico na tela de um usuário existente ou na tela de um novo usuário.

1. Como alternativa, você também pode adicionar um usuário na tela **Visão geral**, como mostrado na figura abaixo.

   ![ACL3](/help/security/assets/ims23.png)

   >[!NOTE]
   >É possível atribuir mais de um perfil a um usuário, conforme mostrado na figura abaixo.

   ![ACL3](/help/security/assets/ims22.png)


1. Após ter sido adicionado ao perfil apropriado, será possível acessar os respectivos locatários no Cloud Manager por meio da [Adobe Experience Cloud](https://my.cloudmanager.adobe.com), usando o canto superior direito da interface.


### Acesso a uma instância no AEM as a Cloud Service {#accessing-instance-cloud-service}

>[!IMPORTANT]
>As etapas mencionadas na seção anterior já devem ter sido concluídas antes de você ter acesso a uma instância no AEM as a Cloud Service.

Para ter acesso a uma instância do AEM no **Admin Console**, você deve ver o programa do Cloud Manager e os ambientes dentro do programa na lista de produtos no **Admin Console**.

Por exemplo, na captura de tela abaixo, você verá dois ambientes disponíveis, o *autor de desenvolvimento* e uma *publicação*.

![ACL3](/help/security/assets/ims19.png)

Para obter acesso às instâncias do AEM, o usuário deve ser adicionado a um grupo do produto Cloud Service apropriado.

Cada instância do autor tem um Perfil de administradores do AEM e usuários do AEM e cada instância de publicação tem um Perfil de usuários do AEM. É possível adicionar outros perfis, conforme necessário.

Para obter acesso de nível administrativo à instância do AEM, adicione o usuário ao Perfil de administradores do AEM para esse Produto específico.
