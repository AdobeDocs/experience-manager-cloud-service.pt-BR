---
title: Equipe e perfis de produto do AEM as a Cloud Service
description: Saiba como AEM equipe as a Cloud Service e os perfis de produto podem conceder e limitar o acesso às soluções de Adobe licenciadas.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 69ac8e444a0f22649b48ec25b549ad60858f8b1b
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 2%

---

# Equipe e perfis de produto do AEM as a Cloud Service {#product-profiles}

Saiba como AEM equipe as a Cloud Service e os perfis de produto podem conceder e limitar o acesso às soluções de Adobe licenciadas.

## Perfis de produto {#profiles}

Ao conceder acesso de usuário a uma solução Adobe específica, você não quer necessariamente conceder acesso total a ele. Os perfis de produto permitem que cada solução tenha seu próprio conjunto de permissões do usuário. Eles estão disponíveis e podem ser acessados por meio da variável [Admin Console.](/help/journey-onboarding/admin-console.md)

## AEM perfis de produto as a Cloud Service {#aem-product-profiles}

AEM as a Cloud Service é uma oferta totalmente nativa em nuvem que oferece AEM como um serviço. Ele fornece AEM de maneira nativa em nuvem, com novos atributos como sempre ativos, sempre atuais, sempre seguros e sempre em escala. Ao mesmo tempo, mantém a principal proposta de valor que o AEM oferece como uma plataforma personalizável para os clientes e permite que equipes de nível empresarial se integrem em seus procedimentos de desenvolvimento e entrega. Consulte [Introdução ao Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md) para saber mais sobre AEM as a Cloud Service.

Os membros AEM da equipe as a Cloud Service serão adicionados e atribuídos a um ou mais dos seguintes perfis de produto por meio do Admin Console durante a integração.

* **Administradores de AEM**: Normalmente, um administrador de AEM é atribuído aos desenvolvedores, em particular desenvolvedores que precisarão ter acesso, por exemplo, aos ambientes de desenvolvimento. O perfil de produto do administrador de AEM será usado para conceder privilégios de administrador na instância de AEM associada.

* **Usuários AEM**: AEM usuários são os usuários em sua organização que geralmente usam AEM as a Cloud Service para criar conteúdo. Esses usuários precisarão acessar AEM para realizar suas tarefas. O perfil de produto AEM usuários normalmente é atribuído a um autor de conteúdo AEM que cria e revisa o conteúdo. Esse conteúdo pode ser de vários tipos, como páginas, ativos, publicações, e assim por diante. O perfil de produto AEM usuários mostrado abaixo é atribuído a esses membros.

![Perfis de produto](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>Todos os usuários atribuídos a um perfil de produto AEM as a Cloud Service têm acesso somente leitura ao Cloud Manager por meio do **Usuário do Cloud Manager** função.
>
>Usuários com somente o **Usuário do Cloud Manager** A função pode fazer logon no Cloud Manager e navegar até os ambientes do autor do AEM (se existirem) usando o **Programas** opções de menu. O **Usuário do Cloud Manager** não é suficiente para acessar os detalhes do programa. Se esse acesso for necessário, os usuários devem receber funções adicionais pelo administrador do sistema.

>[!TIP]
>
>* Para saber mais sobre AEM perfis de produtos, consulte o documento [Atribuindo Perfis de Produto AEM.](/help/journey-onboarding/assign-profiles-aem.md)
>* Para obter mais informações sobre o processo de integração, consulte [jornada de integração.](/help/journey-onboarding/overview.md)


## Perfis de produto do Cloud Manager {#cloud-manager-product-profiles}

O Cloud Manager tem perfis de produto pré-configurados que podem ser considerados permissões com base em funções. O administrador do sistema é responsável pela configuração da equipe do Cloud Manager, atribuindo-a a esses perfis de produto.

>[!TIP]
>
>Consulte o documento [Permissões baseadas em funções no Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) para obter mais detalhes.

Cada um dos perfis de produto tem permissões específicas associadas a eles.

* **Proprietário da empresa** - Nesta função, você tem permissão para adicionar um novo programa ou editar um programa, adicionar ou atualizar um ambiente, implantar código em AEM ambiente ou executar verificações de qualidade de código.
* **Gerenciador de implantação** - Nesta função, você tem a permissão para adicionar ou atualizar um ambiente, executar qualquer pipeline e implantar código em AEM ambiente ou executar verificações de qualidade de código.
* **Desenvolvedor** - Nesta função, você tem permissão para gerar tokens de acesso pessoal para acessar o git.
* **Gerenciador de programas** - Nessa função, você tem permissão para programar pipelines, substituir as portas de qualidade de 3 níveis e fornecer aprovação de produção.

Um usuário pode ser atribuído a vários perfis de produto. Por exemplo, atribuir ambos **Proprietário da empresa** e **Gerenciamento de implantação** As funções r a um usuário fornecem a soma dessas permissões.

A equipe do Cloud Manager incluirá pelo menos:

* One **Proprietário da empresa**, que normalmente também é o administrador do sistema e deve ser a primeira pessoa a fazer logon e acessar o Cloud Manager
* One **Gerenciador de implantação**
* One **Desenvolvedor**

>[!NOTE]
>
>Para ter acesso a AEM as a Cloud Service, os usuários devem pertencer a um dos dois perfis de produto: `AEM Users` ou `AEM Administrators`. As permissões para administrar o Cloud Manager não serão suficientes.

>[!TIP]
>
>* Para saber mais sobre os perfis de produtos do Cloud Manager, consulte o documento [Atribuindo membros da equipe aos perfis de produto do Cloud Manager.](/help/journey-onboarding/assign-profiles-cloud-manager.md)
>* Para obter mais informações sobre o processo de integração, consulte [jornada de integração.](/help/journey-onboarding/overview.md)

