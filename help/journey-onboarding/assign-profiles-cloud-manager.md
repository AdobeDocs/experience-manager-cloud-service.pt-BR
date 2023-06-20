---
title: Atribuir membros da equipe aos perfis de produto do Cloud Manager
description: Siga esta página para saber como atribuir membros da equipe a perfis de produtos do Cloud Manager
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 95%

---


# Atribuir membros da equipe aos perfis de produto do Cloud Manager {#assign-team-members}

Nesta parte da [jornada de integração,](overview.md) você aprenderá a atribuir membros da equipe aos perfis de produto do Cloud Manager.

## Objetivo {#objective}

Na etapa anterior desta jornada, [Acessar o Admin Console,](admin-console.md) você aprendeu a fazer logon no Admin Console e a verificar seus privilégios como administrador do sistema. Agora você está pronto para permitir que os membros da equipe acessem o Cloud Manager. Para fazer isso, atribua perfis de produto.

Ao conceder aos usuários acesso a uma solução da Adobe, você pode não pretender conceder acesso total a eles. Os perfis de produto permitem que cada solução tenha seu próprio conjunto de permissões do usuário. Use o Admin Console para atribuir perfis de produto.

Seu primeiro passo é conceder aos usuários acesso ao Cloud Manager. O Cloud Manager apoia você com configurações de desenvolvimento corporativo e pipelines de CI/CD criados com propósitos específicos, que estão equipados de forma a garantir testes completos e código da mais alta qualidade para fornecer experiências excepcionais.

Depois de ler este documento, você deverá:

* Entender o que são perfis de produtos.
* Entender o que é o Cloud Manager.
* Conhecer os três importantes perfis de produto do Cloud Manager: **Proprietário da empresa**, **Gerente de implantação** e **Desenvolvedor**.
* Poder atribuir membros da equipe aos perfis de produto do Cloud Manager.

## Pré-requisitos {#prerequisites}

Para atribuir membros da equipe a perfis de produto, você precisará ter detalhes sobre os membros da equipe que precisarão acessar o AEM as a Cloud Service, incluindo:

* Nomes
* Endereços de email
* Funções e responsabilidades

>[!TIP]
>
>Para fins de integração, a Adobe recomenda que você adicione inicialmente os usuários que participarão das tarefas imediatas, como administradores, desenvolvedores e autores de conteúdo.
>
>Você pode continuar o processo de integração sem adicionar todos os usuários. Depois de concluir a integração, você poderá adicionar outros usuários.

## Perfis de produto {#product-profiles}

Ao conceder aos usuários acesso a uma solução da Adobe, você pode não pretender conceder acesso total a eles. Os perfis de produto permitem que cada solução tenha seu próprio conjunto de permissões do usuário definidas usando o Admin Console.

Por exemplo, posteriormente nesta jornada, você usará o Admin Console para conceder aos usuários acesso à solução do AEM, atribuindo perfis de produto a administradores e autores do AEM.

No entanto, a próxima etapa é conceder perfis de produto para que os membros da sua equipe tenham acesso ao Cloud Manager.

## Cloud Manager {#cloud-manager}

Como administrador do sistema, você sabe que, para um projeto do AEM as a Cloud Service ser bem-sucedido, é preciso de uma excelente criação de conteúdo usando o AEM, bem como o desenvolvimento e a implantação de seu próprio código personalizado e aplicativos para fornecer esse conteúdo do AEM.

O Cloud Manager é parte integral do AEM as a Cloud Service e é usado para gerenciar seus pipelines de CI/CD para implantação de código, gerenciamento de repositórios de código e gerenciamento de ambientes.

Antes de tudo, a equipe deve ser integrada ao Cloud Manager, concedendo-lhe os perfis de produto necessários. As próximas etapas mostram onde encontrar o perfil de produto do Cloud Manager usando o Admin Console e como atribuí-lo aos membros da equipe.

## Revisar perfis de produto do Cloud Manager {#review-product-profiles}

Usando o Admin Console, você pode ver a lista de perfis do Cloud Manager.

1. Faça logon no Adobe Admin Console em [adminconsole.adobe.com](https://adminconsole.adobe.com/) e na página **Visão geral**, selecione **Adobe Experience Manager as a Cloud Service** no cartão **Produtos e serviços**.

   ![AEM como um produto](/help/journey-onboarding/assets/assign-team1.png)

1. Navegue até a instância do **Cloud Manager** a partir da lista de todas as instâncias.

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. Você verá a lista de perfis de produto pré-configurados do Cloud Manager.

   ![Perfis de produto](/help/journey-onboarding/assets/assign-team3.png)

Os perfis mais importantes a serem atribuídos como parte do processo inicial de integração são:

* **Proprietário da empresa** - Esses usuários gerenciam diferentes programas.
* **Gerente de implantação** - Esses usuários implantam o código dos repositórios nos ambientes em execução do AEM.
* **Desenvolvedor** - Esses usuários desenvolvem aplicativos personalizados do AEM e enviam código aos repositórios.

Sabendo quais são essas funções e o que elas fazem, revise sua lista de membros da equipe para determinar quem precisa de qual perfil. Lembre-se de que os usuários podem ter, e geralmente têm, várias funções em sua equipe e, portanto, também precisam de vários perfis.

## Atribuir o perfil de produto Proprietário da empresa {#assign-business-owner}

Agora você está pronto para adicionar usuários e atribuir a eles o perfil de produto **Proprietário da empresa**.

1. Identifique os usuários que precisam gerenciar os programas do Cloud Manager. Estes são os seus **Proprietários da empresa**.

1. Faça logon no Admin Console em `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` e no **Visão geral** selecione **Adobe Experience Manager as a Cloud Service** produto de **Produtos e serviços** cartão.

   ![Produtos e serviços](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione a guia **Usuários** na navegação superior e clique em **Adicionar usuário**.

   ![Adicionar usuário](/help/journey-onboarding/assets/assign-team4.png)

1. Na caixa de diálogo **Adicionar usuários à equipe**, digite a ID de email do usuário que deseja adicionar.

   * Se a Federated ID dos membros da equipe ainda não tiver sido configurada, selecione **Adobe ID** para o **Tipo de ID**.

   ![Adicionar detalhes do usuário](/help/journey-onboarding/assets/assign-team5.png)

1. Clique no botão de mais sob o cabeçalho **Selecionar grupos de produtos ou usuários** para iniciar a seleção do produto e selecione **Adobe Experience Manager as a Cloud Service** e atribua o perfil de produto **Proprietário da empresa** ao usuário.

   * Atribua cada usuário a pelo menos um perfil de produto para que ele possa acessar o Cloud Manager.
   * Lembre-se de atribuir a si mesmo, como administrador do sistema, a função **Proprietário da empresa**.

   ![Atribuição de usuários](/help/journey-onboarding/assets/assign-team6.png)

1. Clique em **Salvar** e um email de boas-vindas será enviado ao usuário adicionado. O usuário convidado pode acessar o Cloud Manager clicando no link do email de boas-vindas e fazendo logon com sua Adobe ID.

1. Repita essas etapas para os usuários da sua equipe.

Seus **Proprietários da empresa** foram atribuídos e agora podem acessar o Cloud Manager. Lembre-se de também atribuir a si mesmo, como administrador do sistema, o perfil **Proprietário da empresa**.

## Atribuir o perfil de produto Gerente de implantação {#assign-deployment-manager}

1. Identifique os usuários que precisam implantar código.

1. Faça logon no Admin Console em `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` e na página **Visão geral**, selecione o produto **Adobe Experience Manager as a Cloud Service** no cartão **Produtos e serviços**.

   ![Produtos e serviços](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione a guia **Usuários** na navegação principal e clique em **Adicionar usuário**.

   ![Adicionar usuário](/help/journey-onboarding/assets/assign-team4.png)

1. Na caixa de diálogo **Adicionar usuários à equipe**, digite a ID de email do usuário que deseja adicionar.

   * Se a Federated ID dos membros da equipe ainda não tiver sido configurada, selecione **Adobe ID** para o **Tipo de ID**.

   ![Inserir ID](/help/journey-onboarding/assets/assign-team5.png)

1. Clique no botão de mais sob o cabeçalho **Selecionar grupos de produtos ou usuários** para iniciar a seleção do produto e selecione **Adobe Experience Manager as a Cloud Service** e atribua o perfil de produto **Gerente de implantação** ao usuário.

   ![Atribuir perfil](/help/journey-onboarding/assets/assign-team6.png)

Seus **Gerentes de implantação** foram atribuídos e agora podem acessar o Cloud Manager. Dependendo de suas responsabilidades futuras, você pode ou não precisar atribuir a si mesmo, como administrador do sistema, o perfil **Gerente de implantação**.

## Atribuir o perfil de produto Desenvolvedor {#assign-developer}

1. Identifique os usuários que precisam desenvolver aplicativos do AEM e gerenciar código.

1. Faça logon no Admin Console em `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` e na página **Visão geral**, selecione o produto **Adobe Experience Manager as a Cloud Service** no cartão **Produtos e serviços**.

   ![Produtos e serviços](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione a guia **Usuários** na navegação principal e clique em **Adicionar usuário**.

   ![Adicionar usuário](/help/journey-onboarding/assets/assign-team4.png)

1. Na caixa de diálogo **Adicionar usuários à equipe**, digite a ID de email do usuário que deseja adicionar.

   * Se a Federated ID dos membros da equipe ainda não tiver sido configurada, selecione **Adobe ID** para o **Tipo de ID**.

   ![Adicionar ID do usuário](/help/journey-onboarding/assets/assign-team5.png)

1. Clique no botão de mais sob o cabeçalho **Selecionar grupos de produtos ou usuários** para iniciar a seleção do produto e selecione **Adobe Experience Manager as a Cloud Service** e atribua o perfil de produto **Desenvolvedor** ao usuário.

   ![Atribuir perfil](/help/journey-onboarding/assets/assign-team6.png).

Seus **Desenvolvedores** foram atribuídos e agora podem acessar o Cloud Manager. Dependendo de suas responsabilidades futuras, você pode ou não precisar atribuir a si mesmo, como administrador do sistema, o perfil **Desenvolvedor**.

## O que vem a seguir {#whats-next}

Parabéns! Sua equipe recém-formada do Cloud Manager (incluindo você atribuído ao perfil **Proprietário da empresa**) foi configurada. Com a função de **Proprietário da empresa**, agora você está a apenas um passo de fazer logon no Cloud Manager e ativar a criação dos recursos de nuvem.

Nesta parte da jornada de integração você aprendeu a atribuir perfis aos membros da equipe no Admin Console. Agora você deve:

* Entender o que são perfis de produtos.
* Entender o que é o Cloud Manager.
* Conhecer os três importantes perfis de produto do Cloud Manager: **Proprietário da empresa**, **Gerente de implantação** e **Desenvolvedor**.
* Poder atribuir membros da equipe aos perfis de produto do Cloud Manager.

Agora você está pronto para continuar sua jornada de integração revisando em seguida o documento [Acessar o Cloud Manager,](cloud-manager.md) no qual você aprenderá a acessar o Cloud Manager e criar os recursos do projeto.

## Recursos adicionais {#additional-resources}

É recomendável continuar na jornada de integração conforme descrito anteriormente. Estes são alguns recursos adicionais se você quiser se aprofundar em um tópico específico desta jornada.

* [Introdução ao Cloud Manager](/help/onboarding/cloud-manager-introduction.md) - Saiba mais sobre o Cloud Manager e seus programas e ambientes.
* [Perfis de produto do Cloud Manager](/help/onboarding/aem-cs-team-product-profiles.md) - Saiba mais sobre os perfis de produto e equipe do AEM as a Cloud Service.
* [Tipos de identidade no Adobe Admin Console](https://helpx.adobe.com/br/enterprise/admin-guide.html/enterprise/using/identity.ug.html) - O sistema de gerenciamento de identidade do Adobe ajuda os administradores a criar e gerenciar o acesso do usuário a aplicativos e serviços. A Adobe oferece esses tipos de identidades ou contas para autenticar e autorizar os usuários.

