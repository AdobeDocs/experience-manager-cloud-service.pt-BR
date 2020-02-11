---
title: Suporte IMS para o Adobe Experience Manager como um serviço em nuvem
description: 'Suporte IMS para o Adobe Experience Manager como um serviço em nuvem '
translation-type: tm+mt
source-git-commit: bef17376f0b7de79511f9ad6ceb00e9f084f45d2

---


# Suporte IMS para o Adobe Experience Manager como um serviço em nuvem {#ims-support-for-aem-as-a-cloud-service}

## Introdução {#introduction}

* O AEM como um serviço em nuvem inclui suporte do Admin Console para instâncias do AEM e autenticação baseada no Adobe Identity Management System (IMS para abreviação).
* O Admin Console permite que os administradores gerenciem centralmente todos os usuários da Experience Cloud.
* Usuários e grupos podem ser atribuídos a perfis de produtos associados ao AEM como instâncias do serviço em nuvem, permitindo que eles façam logon nessa instância.

## Destaques principais {#key-highlights}

O AEM como serviço em nuvem oferece suporte à autenticação IMS somente para usuários de Autor, Administrador e Desenvolvimento. Ele não oferece suporte para usuários finais externos de sites de clientes como visitantes do site.

* O Admin Console representará clientes como Organizações IMS, Instâncias de autor e publicação em um ambiente como Instâncias de contexto de produto. Isso permitirá que os administradores do Sistema e do Produto gerenciem o acesso às instâncias.
* Perfis de produto no Admin Console determinam quais instâncias um usuário pode acessar.
* Os clientes poderão usar seus próprios provedores de identidade compatíveis com SAML 2 (IDP para abreviação) para logon único.
* Somente Enterprise ID ou Federated IDs para o Single Sign On do cliente serão compatíveis, sem Adobe IDs pessoais.

## Arquitetura {#architecture}

A autenticação IMS funciona usando o protocolo OAuth entre o AEM e o terminal Adobe IMS. Depois que um usuário é adicionado ao IMS e tem uma Adobe Identity, ele pode fazer logon no serviço de autor do AEM usando credenciais IMS.

O fluxo de logon do usuário é mostrado abaixo, o usuário será redirecionado para o IMS e, opcionalmente, para o IDP do cliente para SSO e redirecionado para o AEM.

![Arquitetura IMS](/help/security/assets/ims1.png)

## Como configurar {#how-to-set-up}

### Organizações integradas ao Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

A integração do cliente ao Adobe Admin Console é um pré-requisito para o uso do Adobe IMS para autenticação AEM.

Como primeira etapa, os clientes precisam ter uma organização provisionada no Adobe IMS. Os clientes do Adobe Enterprise são representados como Organizações IMS no [Adobe Admin Console](https://helpx.adobe.com/enterprise/using/admin-console.html) . Este é o portal usado pelos clientes da Adobe para gerenciar seus direitos de produto para seus usuários e grupos.

Os clientes do AEM já devem ter uma organização provisionada e, como parte do provisionamento do IMS, as instâncias do cliente serão disponibilizadas no Admin Console para gerenciar direitos e acesso do usuário.

Assim que um cliente existir como uma organização IMS, ele terá que configurar seu sistema como resumido abaixo:

![Inicialização IMS](/help/security/assets/ims2.png)

1. O administrador do sistema designado recebe um convite para fazer logon no Cloud Manager. Depois de fazer logon no gerenciador da Cloud, os administradores de sistema podem optar por provisionar programas e ambientes AEM ou navegar até o Admin Console para tarefas administrativas.
1. O Administrador do Sistema alega que um domínio confirma a propriedade do respectivo domínio (por exemplo, acme.com)
1. O Administrador do Sistema configura os Diretórios de Usuário
1. O administrador do sistema faz a configuração do IDP no Admin Console para configurar o logon único.
1. O administrador do AEM gerencia os grupos locais, permissões e privilégios, como de costume.

As noções básicas do Adobe Identity Management, incluindo a configuração do IDP, são abordadas [aqui](https://helpx.adobe.com/enterprise/using/set-up-identity.html).

O uso do Enterprise Administration e do Admin Console é abordado [aqui](https://helpx.adobe.com/enterprise/managing/user-guide.html).

### Usuários integrados no Admin Console {#onboarding-users-in-admin-console}

Existem três maneiras de os usuários integrados dependerem do tamanho do cliente e de suas preferências: crie usuários manualmente no Admin Console, carregue um arquivo .csv ou sincronize usuários do Enterprise Ative Diretory do cliente.

**Adição manual por meio da interface do usuário do Admin Console**

Usuários e grupos podem ser criados manualmente na interface do usuário do Admin Console. Este método pode ser usado se você não tiver um grande número de usuários para gerenciar. Por exemplo, menos de 50 usuários do AEM ou se você já estiver usando esse método para administrar outros produtos da Adobe, como aplicativos do Analytics, Target ou Creative Cloud.

![Integração de usuários](/help/security/assets/ims3.png)

**Upload de arquivo na interface do usuário do Admin Console**

Para facilitar a manipulação da criação do usuário, um `.csv` arquivo pode ser carregado para adicionar usuários em massa.

![Upload de arquivo](/help/security/assets/ims4.png)

**Ferramenta de sincronização do usuário**

A User Sync Tool (UST) permite que nossos clientes corporativos criem e gerenciem usuários da Adobe que utilizam o Ative Diretory. Isso também funciona para outros serviços de diretório OpenLDAP testados. Os usuários de destino são Administradores de identidade de TI (Enterprise Diretory ou Administradores de sistema) que poderão instalar e configurar a ferramenta. A ferramenta open source é personalizável para que os clientes possam modificá-la de acordo com seus próprios requisitos específicos.

Quando a Sincronização de usuários é executada, ela obtém uma lista de usuários do Ative Diretory da organização e a compara com a lista de usuários no Admin Console.  Em seguida, chama a API de gerenciamento de usuários da Adobe para que o Admin Console seja sincronizado com o diretório da organização. O fluxo de mudanças é totalmente unidirecional. Quaisquer edições feitas no Admin Console não são enviadas para o diretório.

A ferramenta permite que o administrador do sistema mapeie grupos de usuários no diretório do cliente com a configuração do produto e grupos de usuários no Admin Console.

Para configurar a Sincronização de usuários, a organização precisa criar um conjunto de credenciais da mesma forma que usaria a API [de Gerenciamento de](https://www.adobe.io/apis/experienceplatform/umapi-new.html)usuários.

![Ferramenta de sincronização do usuário](/help/security/assets/ims5.png)

A Ferramenta de sincronização do usuário é distribuída pelo repositório do Adobe Github [neste local](https://github.com/adobe-apiplatform/user-sync.py/releases/latest).

>[!NOTE]
>
> Uma versão de pré-lançamento **2.4RC1** está disponível com suporte à criação de grupos dinâmicos e pode ser encontrada [aqui](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1).

Os principais recursos desta versão são a capacidade de mapear dinamicamente novos grupos LDAP para associação de usuários no Admin Console, bem como a criação dinâmica de grupos de usuários.

Mais informações sobre os novos recursos do grupo podem ser encontradas [neste local](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options).

**Documentação de sincronização do usuário**

Consulte a documentação [](https://adobe-apiplatform.github.io/user-sync.py/en/) UST para obter mais detalhes.

A Ferramenta de sincronização do usuário precisa se registrar como uma UMAPI do cliente de E/S da Adobe usando o procedimento [aqui](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).

A Documentação do console de E/S da Adobe pode ser encontrada [aqui](https://www.adobe.io/apis/cloudplatform/console.html).

A API de gerenciamento de usuários usada pela Ferramenta de sincronização de usuário é abordada [aqui](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

## Configuração do Adobe Experience como um serviço em nuvem {#aem-configuration}

> [!NOTE]
>
>A configuração AEM IMS necessária será configurada automaticamente quando os ambientes e as instâncias do AEM forem provisionados. No entanto, o administrador pode modificá-la de acordo com seus requisitos, usando o método descrito [aqui](/help/implementing/deploying/overview.md).

A configuração IMS do AEM necessária será configurada automaticamente quando os ambientes e as instâncias do AEM forem provisionados.  Os administradores de clientes podem modificar parte da configuração de acordo com seus requisitos

A abordagem geral é configurar o Adobe IMS como um provedor OAuth. O **Apache Jackrabbit Oak Default Sync Handler** pode ser modificado da mesma forma que para a sincronização LDAP.

Abaixo estão as principais configurações OSGI que precisam ser modificadas para alterar propriedades como Associação automática do usuário ou Mapeamentos de grupos.

<!-- Arun to provide list of osgi configs -->

## Como usar {#how-to-use}

### Gerenciamento de produtos e acesso do usuário no Admin Console {#managing-products-and-user-access-in-admin-console}

Quando o administrador do produto fizer logon no Admin Console, verá várias instâncias do Contexto de produto dos serviços gerenciados do AEM, como mostrado abaixo:

![Logon de instâncias](/help/security/assets/ims6.png)

Neste exemplo, a organização **AEM-MS-Onboard** tem 32 instâncias abrangendo topologias e ambientes diferentes, como Stage ou Prod.

![Logon de instâncias2](/help/security/assets/ims7.png)

Em cada instância do Contexto do produto, haverá Perfis do produto associados. Esses perfis de produto são usados para atribuir acesso a usuários e grupos com o privilégio necessário.

O perfil **Administrator_xxx** será usado para conceder privilégios de Administrador na instância AEM associada, enquanto o perfil **User_xxx** for usado para adicionar usuários regulares.

Todos os usuários e grupos adicionados sob este perfil de produto poderão fazer logon nessa instância específica, como mostra o exemplo abaixo:

![Perfil do produto](/help/security/assets/ims8.png)

### Fazer logon no Adobe Experience Manager como um serviço da nuvem (#logon-in-to-aem)

**Logon do administrador local**

O AEM pode continuar a suportar logons locais para usuários administradores. A tela de logon tem uma opção para fazer logon localmente:

![Logon local](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**Logon baseado em IMS**

Para outros usuários, o logon com base em IMS pode ser usado assim que o IMS for configurado na instância. O usuário primeiro clicará no botão Fazer logon com a Adobe, conforme mostrado abaixo:

![Logon do IMS](/help/security/assets/ims10.png)

Eles serão então redirecionados para a tela de login do IMS e precisarão digitar suas credenciais:

![Logon IMS2](/help/security/assets/ims11.png)

![Logon IMS3](/help/security/assets/ims12.png)

Se um IDP federado for configurado durante a configuração inicial do Admin Console, o usuário será redirecionado ao IDP do cliente para SSO:

![Logon IMS4](/help/security/assets/ims13.png)

Após a conclusão da autenticação, o usuário será redirecionado de volta para o AEM e conectado:

![Logon IMS5](/help/security/assets/ims14.png)

### Gerenciando permissões e ACLs no Adobe Experience Manager como um serviço em nuvem {#managing-permissions-in-aem}

As ACLs e permissões continuarão a ser gerenciadas no AEM. Os Grupos de usuários sincronizados do IMS podem ser atribuídos a grupos locais onde ACLs e privilégios são definidos.

No exemplo abaixo, adicionamos grupos sincronizados ao grupo local **Dam_Users** como exemplo.

O usuário faz parte dos seguintes Grupos no IMS:

![ACL1](/help/security/assets/ims15.png)

Quando o usuário faz logon, suas Associações de grupo são sincronizadas, como mostrado abaixo:

![ACL2](/help/security/assets/ims16.png)

No AEM, os Grupos de usuários sincronizados do IMS podem ser adicionados como membros a grupos locais existentes, como Usuários **do** DAM.

![ACL3](/help/security/assets/ims17.png)

Como mostrado abaixo, o grupo **AEM-GRP_008** herda as permissões e os privilégios dos usuários **do** DAM, essa é uma maneira eficaz de gerenciar permissões para grupos sincronizados e também é comumente usada no método de autenticação baseado em LDAP.

![ACL3](/help/security/assets/ims18.png)