---
title: Perfis de produto e de equipe do AEM as a Cloud Service
description: Descubra como os perfis de produto e de equipe do AEM as a Cloud Service podem conceder e limitar o acesso às suas soluções licenciadas da Adobe.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 1e3130578b7e36e5ffd5ad7b04cc7981a95bb291
workflow-type: ht
source-wordcount: '778'
ht-degree: 100%

---

# Perfis de produto e de equipe do AEM as a Cloud Service {#product-profiles}

Descubra como os perfis de produto e de equipe do AEM as a Cloud Service podem conceder e limitar o acesso às suas soluções licenciadas da Adobe.

## Perfis de produto {#profiles}

Ao conceder ao usuário acesso a uma solução específica da Adobe, você pode não pretender conceder acesso total a ele. Os perfis de produto permitem que cada solução tenha seu próprio conjunto de permissões do usuário. Eles estão disponíveis e podem ser acessados por meio do [Admin Console.](/help/journey-onboarding/admin-console.md)

## Perfis de produto e de equipe do AEM as a Cloud Service {#aem-product-profiles}

O AEM as a Cloud Service é uma oferta em nuvem totalmente nativa que fornece o AEM como serviço. Ele fornece o AEM de maneira nativa em nuvem, com novos atributos como sempre ativo, sempre atual, sempre seguro e sempre em escala. Ao mesmo tempo, mantém a principal proposta de valor do AEM na forma de uma plataforma personalizável para os clientes e permite que equipes de nível empresarial se integrem em seus procedimentos de desenvolvimento e entrega. Consulte [Introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md) para saber mais sobre o AEM as a Cloud Service.

Os membros da sua equipe do AEM as a Cloud Service serão adicionados e atribuídos a um ou mais dos perfis de produto descritos a seguir por meio do Admin Console durante a integração.

* **Administradores do AEM**: normalmente, um administrador do AEM é atribuído aos desenvolvedores, especialmente a desenvolvedores que precisarão ter acesso, por exemplo, aos ambientes de desenvolvimento. O perfil de produto do administrador do AEM será usado para conceder privilégios de administrador na instância associada do AEM.

* **Usuários do AEM**: são os usuários em sua organização que geralmente usam o AEM as a Cloud Service para criar conteúdo. Esses usuários precisarão acessar o AEM para realizar suas tarefas. O perfil de produto dos usuários do AEM normalmente é atribuído a um autor de conteúdo do AEM que cria e revisa conteúdo. Esse conteúdo pode ser de vários tipos, como páginas, ativos, publicações etc. O perfil de produto dos usuários do AEM mostrado abaixo é atribuído a esses membros.

![Perfis de produto](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>Todos os usuários atribuídos a um perfil de produto AEM as a Cloud Service têm acesso de somente leitura ao Cloud Manager por meio da função **Usuário do Cloud Manager**.
>
>Usuários com somente a função de **Usuário do Cloud Manager** pode fazer logon no Cloud Manager e navegar até os ambientes de autor do AEM (se existirem) usando as opções do menu **Programas**. A função de **Usuário do Cloud Manager** não é suficiente para acessar os detalhes do programa. Se tal acesso for necessário, os usuários devem receber funções adicionais pelo administrador do sistema.

>[!WARNING]
>
>O nome do perfil do produto **Administradores do AEM** não deve ser alterado. A alteração do nome do perfil do produto **Administradores do AEM** removerá os direitos de administrador de todos os usuários atribuídos a esse perfil.

>[!TIP]
>
>* Para saber mais sobre perfis de produtos do AEM, consulte o documento [Atribuição de perfis de produto AEM](/help/journey-onboarding/assign-profiles-aem.md).
>* Para obter mais informações sobre o processo de integração, consulte a [jornada de integração.](/help/journey-onboarding/overview.md)


## Perfis de produto do Cloud Manager {#cloud-manager-product-profiles}

O Cloud Manager tem perfis de produto pré-configurados que podem ser considerados permissões com base em função. O administrador do sistema é responsável pela configuração da sua equipe do Cloud Manager, atribuindo-a a esses perfis de produto.

>[!TIP]
>
>Consulte o documento [Permissões com base em função no Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) para obter mais detalhes.

Cada um dos perfis de produto tem permissões específicas associadas a eles.

* **Proprietário da empresa** - Nesta função, você tem permissão para adicionar um novo programa ou editar um programa existente, adicionar ou atualizar um ambiente, implantar código no ambiente do AEM ou executar verificações de qualidade do código.
* **Gerente de implantação** - Nessa função, você tem permissão para adicionar ou atualizar um ambiente, executar pipelines e implantar código no ambiente do AEM ou executar verificações de qualidade do código.
* **Desenvolvedor** - Nesta função, você tem permissão para gerar tokens de acesso pessoal para acessar o Git.
* **Gerente de programas** - Nessa função, você tem permissão para programar pipelines, substituir os quality gates (portais de qualidade) de três níveis e fornecer aprovação de produção.

Um usuário pode ser atribuído a vários perfis de produto. Por exemplo, atribuir as funções **Proprietário da empresa** e **Gerente de implantação** a um usuário fornecerá a ele a soma dessas permissões.

A equipe do Cloud Manager incluirá pelo menos:

* Um **Proprietário da empresa**, que normalmente também é o administrador do sistema e deve ser a primeira pessoa a fazer logon e acessar o Cloud Manager
* Um **Gerente de implantação**
* Um **Desenvolvedor**

>[!NOTE]
>
>Para ter acesso ao AEM as a Cloud Service, os usuários devem pertencer a um de dois perfis de produto: `AEM Users` ou `AEM Administrators`. Não é suficiente ter permissões para administrar o Cloud Manager.

>[!TIP]
>
>* Para saber mais sobre os perfis de produtos do Cloud Manager, consulte o documento [Atribuição de membros de equipe aos perfis de produto do Cloud Manager.](/help/journey-onboarding/assign-profiles-cloud-manager.md)
>* Para obter mais informações sobre o processo de integração, consulte a [jornada de integração.](/help/journey-onboarding/overview.md)

