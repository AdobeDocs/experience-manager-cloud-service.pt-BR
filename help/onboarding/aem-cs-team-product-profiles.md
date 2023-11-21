---
title: Perfis de produto e de equipe do AEM as a Cloud Service
description: Descubra como os perfis de produto e de equipe do AEM as a Cloud Service podem conceder e limitar o acesso às suas soluções licenciadas da Adobe.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 81%

---


# Perfis de produto e de equipe do AEM as a Cloud Service {#product-profiles}

Descubra como os perfis de produto e de equipe do AEM as a Cloud Service podem conceder e limitar o acesso às suas soluções licenciadas da Adobe.

## Perfis de produto {#profiles}

Ao conceder ao usuário acesso a uma solução específica da Adobe, você pode não pretender conceder acesso total a ele. Os perfis de produto permitem que cada solução tenha seu próprio conjunto de permissões do usuário. Eles estão disponíveis e podem ser acessados por meio do [Admin Console](/help/journey-onboarding/admin-console.md).

## Perfis de produto e de equipe do AEM as a Cloud Service {#aem-product-profiles}

O AEM as a Cloud Service é uma oferta em nuvem totalmente nativa que fornece o AEM como serviço. Ele fornece o AEM de maneira nativa em nuvem, com novos atributos como sempre ativo, sempre atual, sempre seguro e sempre em escala. Ao mesmo tempo, mantém a principal proposta de valor do AEM na forma de uma plataforma personalizável para os clientes e permite que equipes de nível empresarial se integrem em seus procedimentos de desenvolvimento e entrega. Consulte [Introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md) para saber mais sobre o AEM as a Cloud Service.

Os membros da sua equipe do AEM as a Cloud Service são adicionados e atribuídos a um ou mais dos seguintes perfis de produto por meio do Admin Console durante a integração.

* **Administradores de AEM**: um administrador de AEM normalmente é atribuído aos desenvolvedores, especialmente a desenvolvedores que precisam de acesso, por exemplo, aos ambientes de desenvolvimento. O perfil de produto de admin do AEM será usado para conceder privilégios de administração na instância associada do AEM.

* **Usuários do AEM**: são os usuários em sua organização que geralmente usam o AEM as a Cloud Service para criar conteúdo. Esses usuários precisam acessar o AEM para realizar suas tarefas. O perfil de produto dos usuários do AEM normalmente é atribuído a um autor de conteúdo do AEM que cria e revisa conteúdo. Esse conteúdo pode ser de vários tipos, como páginas, ativos, publicações etc. O perfil de produto dos usuários do AEM mostrado abaixo é atribuído a esses membros.

![Perfis de produto](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>Todos os usuários atribuídos a um perfil de produto AEM as a Cloud Service têm acesso de somente leitura ao Cloud Manager por meio da função **Usuário do Cloud Manager**.
>
>Usuários com somente a função de **Usuário do Cloud Manager** pode fazer logon no Cloud Manager e navegar até os ambientes de autor do AEM (se existirem) usando as opções do menu **Programas**. A função de **Usuário do Cloud Manager** não é suficiente para acessar os detalhes do programa. Se tal acesso for necessário, os usuários devem receber funções adicionais pelo administrador do sistema.

>[!WARNING]
>
>O nome do perfil do produto **Administradores do AEM** não deve ser alterado. A alteração do perfil do produto **Administradores do AEM** removerá os direitos de administrador de todos os usuários atribuídos a esse perfil.

>[!TIP]
>
>* Para saber mais sobre perfis de produto AEM, consulte [Atribuição de perfis de produto do AEM](/help/journey-onboarding/assign-profiles-aem.md).
>* Para obter mais informações sobre o processo de integração, consulte a [jornada de integração](/help/journey-onboarding/overview.md).

## Perfis de produto do Cloud Manager {#cloud-manager-product-profiles}

O Cloud Manager tem perfis de produto pré-configurados que podem ser considerados permissões com base em função. O administrador do sistema é responsável pela configuração da sua equipe do Cloud Manager, atribuindo-a a esses perfis de produto.

>[!TIP]
>
>Consulte [Permissões com base em funções no Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) para obter mais detalhes.

Cada um dos perfis de produto tem permissões específicas associadas a eles.

* **Proprietário da empresa**
   * Nesta função, você tem permissão para adicionar um novo programa ou editar um programa, adicionar ou atualizar um ambiente, implantar código no ambiente AEM ou executar verificações de qualidade do código.
   * Esse usuário é responsável por definir KPIs, aprovar implantações de produção e neutralizar falhas de nível 3 importantes, quando necessário.
* **Gerenciador de implantação**
   * Nessa função, você tem permissão para adicionar ou atualizar um ambiente, executar pipelines e implantar código no ambiente AEM ou executar verificações de qualidade do código.
   * Esse usuário gerencia operações de implantação e usa o Cloud Manager para executar implantações de preparo/produção, editar os pipelines de CI/CD, aprovar falhas de nível 3 importantes quando necessário e acessar o repositório Git.
* **Desenvolvedor**
   * Nesta função, você tem permissão para gerar tokens de acesso pessoal para acessar o Git.
   * Esse usuário desenvolve e testa o código de aplicativo personalizado e usa principalmente o Cloud Manager para visualizar o status da implantação e acessar o repositório Git para confirmações de código.
* **Gerenciador de programas**
   * Nessa função, você tem permissão para agendar pipelines, substituir os quality gates (portais de qualidade) de três níveis e fornecer aprovação de produção.
   * Esse usuário usa o Cloud Manager para executar a configuração da equipe, revisar o status, visualizar KPIs e, quando necessário, pode aprovar falhas de nível 3 importantes.

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
>* Para saber mais sobre os perfis de produto do Cloud Manager, consulte [Atribuir membros da equipe aos perfis de produto do Cloud Manager](/help/journey-onboarding/assign-profiles-cloud-manager.md).
>* Para obter mais informações sobre o processo de integração, consulte a [jornada de integração](/help/journey-onboarding/overview.md).
