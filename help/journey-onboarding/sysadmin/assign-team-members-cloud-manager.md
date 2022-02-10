---
title: Atribuindo membros da equipe a perfis de produto do Cloud Manager
description: Siga esta página para saber como atribuir membros da equipe a perfis de produto do Cloud Manager
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 1%

---

# Atribuir membros da equipe aos perfis de produto do Cloud Manager {#assign-team-members}

Na etapa anterior desta jornada, [Introdução ao processo de integração](/help/journey-onboarding/sysadmin/get-started-onboarding-journey.md), agora você aprendeu a fazer logon no Admin Console e visualizou seus privilégios como Administrador do sistema. Agora você está pronto para atribuir membros da equipe aos perfis de produto do Cloud Manager.

## Objetivo {#objective}

Este documento resume como atribuir membros da equipe aos perfis de produto do Cloud Manager da Adobe Admin Console. Depois de atribuídos, esses membros podem criar recursos da nuvem de acesso, conforme descrito na próxima etapa desta jornada.

Após ler esta seção, você deve ser capaz de:

* Entenda por que e como você deve adicionar membros da equipe.
* Saiba mais sobre três perfis de produto importantes do Cloud Manager: **Proprietário da empresa**, **Gerenciador de implantação** e **Desenvolvedor**.
* Atribua membros da equipe aos perfis de produto do Cloud Manager.

>[!TIP]
>
>Para fins de integração, o Adobe recomenda adicionar usuários inicialmente que participarão das tarefas imediatas, como administradores, desenvolvedores e autores de conteúdo. Você pode continuar o processo de integração sem adicionar todos os usuários. Após concluir a integração, você pode adicionar outros usuários.

## Pré-requisitos {#prerequisites}

Os seguintes pré-requisitos devem ser atendidos antes de iniciar esta seção. Você deve:

* Seja um administrador do sistema e entenda os perfis de produto do Cloud Manager.
   * Retorne ao [Visão geral da Jornada de integração](onboarding-journey-overview.md) se você não estiver familiarizado com esses conceitos.
* Entenda as noções básicas do Adobe Admin Console.
   * Retorne ao [Visão geral da Jornada de integração](onboarding-journey-overview.md) se você não estiver familiarizado com esses conceitos.
* Tenha detalhes sobre os membros da sua equipe, que precisarão acessar AEM as a Cloud Service, incluindo
   * Nomes
   * Endereços de email
   * Funções e responsabilidades

## Revisar perfis de produto do Cloud Manager {#review-product-profiles}

No Adobe Admin Console, é possível ver a lista de perfis do Cloud Manager.

1. Faça logon no Adobe Admin Console em [adminconsole.adobe.com](https://adminconsole.adobe.com/) e da **Visão geral** página, selecione **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

   ![AEM como produto](/help/journey-onboarding/assets/assign-team1.png)

1. Navegue até o **Cloud Manager** da lista de todas as instâncias.

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. Você verá a lista de perfis de produto pré-configurados do Cloud Manager.

   ![Perfis de produto](/help/journey-onboarding/assets/assign-team3.png)

## Atribuir usuários ao perfil de produto do proprietário comercial {#assign-users-business-owner}

Agora você está pronto para adicionar usuários e atribuí-los à variável **Proprietário da empresa** perfil do produto.

1. Identifique os usuários que gerenciarão os programas do Cloud Manager e adicione-os ao perfil de produto Proprietário comercial.

1. Faça logon no Admin Console em [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) e no **Visão geral** página, selecione **Adobe Experience Manager as a Cloud Service** produto de **Produtos e serviços** cartão.

   ![Produtos e serviços](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione o **Usuários** na navegação superior, em seguida, selecione **Adicionar usuário**.

   ![Adicionar usuário](/help/journey-onboarding/assets/assign-team4.png)

1. No **Adicionar usuários à equipe** , insira a ID de email do usuário que deseja adicionar.

   * Se a ID federada dos membros da equipe ainda não tiver sido configurada, selecione **Adobe ID** para **Tipo de ID**.

   ![Adicionar detalhes do usuário](/help/journey-onboarding/assets/assign-team5.png)

1. Clique no botão de mais sob a **Selecionar produtos ou grupos de usuários** para iniciar a seleção do produto e selecione **Adobe Experience Manager as a Cloud Service** e atribuir **Proprietário da empresa** perfil de produto para o usuário.

   * Atribua cada usuário a pelo menos um perfil de produto para que ele possa acessar o Cloud Manager.
   * Lembre-se de atribuir a si mesmo como Administrador do sistema ao **Proprietário da empresa** função.

   ![Atribuição de usuários](/help/journey-onboarding/assets/assign-team6.png)

1. Clique em **Salvar** e um email de boas-vindas é enviado ao usuário adicionado. O usuário convidado pode acessar o Cloud Manager clicando no link do email de boas-vindas e fazendo logon usando a Adobe ID.

1. Repita essas etapas para os usuários em sua equipe.

Sua equipe recém-formada do Cloud Manager (incluindo você atribuído ao **Proprietário da empresa** foi configurada. No papel de **Proprietário da empresa**, agora você está a apenas um passo de fazer logon no Cloud Manager e ativar a criação dos recursos da nuvem.

## Atribuir usuários ao perfil de produto do Gerenciador de implantação {#assign-users-deployment-manager}

1. Identifique os usuários que gerenciarão os programas do Cloud Manager e adicione-os ao perfil de produto do Deployment Manager.

1. Faça logon no Admin Console em [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) e no **Visão geral** seleção de página **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

   ![Produtos e serviços](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione o **Usuários** no início da navegação e selecione **Adicionar usuário**.

   ![Adicionar usuário](/help/journey-onboarding/assets/assign-team4.png)

1. No **Adicionar usuários à equipe** , insira a ID de email do usuário que deseja adicionar.

   * Se a ID federada dos membros da equipe ainda não tiver sido configurada, selecione **Adobe ID** para **Tipo de ID**.

   ![Inserir ID](/help/journey-onboarding/assets/assign-team5.png)

1. Clique no botão de mais sob a **Selecionar produtos ou grupos de usuários** para iniciar a seleção do produto e selecione **Adobe Experience Manager as a Cloud Service** e atribuir **Gerenciador de implantação** perfil de produto para o usuário.

   ![Atribuir perfil](/help/journey-onboarding/assets/assign-team6.png).

## Atribuir usuários ao perfil de produto do desenvolvedor {#assign-users-developer}

1. Identifique os usuários que gerenciarão os programas do Cloud Manager.

1. Faça logon no Admin Console em [adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview) e no **Visão geral** seleção de página **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

   ![Produtos e serviços](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione o **Usuários** no início da navegação e selecione **Adicionar usuário**.

   ![Adicionar usuário](/help/journey-onboarding/assets/assign-team4.png)

1. Em **Adicionar usuários à equipe** , insira a ID de email do usuário que deseja adicionar.

   * Se a ID federada dos membros da equipe ainda não tiver sido configurada, selecione **Adobe ID** para **Tipo de ID**.

   ![Adicionar ID de usuário](/help/journey-onboarding/assets/assign-team5.png)

1. Clique no botão de mais sob a **Selecionar produtos ou grupos de usuários** para iniciar a seleção do produto e selecione **Adobe Experience Manager as a Cloud Service** e atribuir **Desenvolvedor** perfil de produto para o usuário.

   ![Atribuir perfil](/help/journey-onboarding/assets/assign-team6.png).

## O que vem a seguir {#whats-next}

Nesta parte da jornada de integração, você aprendeu tudo sobre como atribuir membros da equipe a funções no Admin Console. Agora você deve:

* Entenda por que e como você deve adicionar membros da equipe.
* Entenda três perfis de produto importantes do Cloud Manager: **Proprietário da empresa**, **Gerenciador de implantação** e **Desenvolvedor**.
* Atribua membros da equipe a perfis de produto do Cloud Manager.

Agora você está pronto para continuar sua jornada de integração ao revisar o documento [Configuração de recursos da nuvem via Cloud Manager](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md), onde você aprenderá:

1. Para que outros proprietários de negócios criem programas, você, como Administrador do Sistema, é atribuído ao **Proprietário da empresa** , deve primeiro acessar e fazer logon no Cloud Manager.
1. Como um usuário com a **Proprietário da empresa** pode fazer logon e configurar os recursos da nuvem, incluindo o Programa da nuvem e os Ambientes.
1. Como os usuários com a **Desenvolvedor** e **Gerenciador de implantação** As funções podem acessar o Cloud Manager.

## Recursos adicionais {#additional-resources}

É recomendável continuar na jornada de integração conforme descrito anteriormente. Esses são alguns recursos adicionais se você quiser fazer um mergulho profundo em um tópico específico desta jornada.

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Perfis de produto do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Visão geral da identidade do Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
