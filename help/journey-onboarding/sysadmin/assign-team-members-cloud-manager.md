---
title: 'Atribuindo membros da equipe a perfis de produto do Cloud Manager '
description: Siga esta página para saber como atribuir membros da equipe a perfis de produto do Cloud Manager
index: false
feature: Onboarding
role: Admin, User, Developer
source-git-commit: d72ecc81e3afd68dee64e7e4934703db84df25d6
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 0%

---


# Atribuir membros da equipe aos perfis de produto do Cloud Manager {#assign-team-members}

Depois de saber como fazer logon no [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en) e visualizar seus privilégios como um [Administrador do sistema](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=en), você estará pronto para atribuir membros da equipe aos perfis de produto do Cloud Manager.

## Objetivo {#objective}

Este documento resume como atribuir membros da equipe aos perfis de produto do Cloud Manager da Adobe Admin Console.

Após ler esta seção, você deve ser capaz de:

* Entenda por que e como você deve adicionar membros da equipe.
* Saiba mais sobre três perfis de produto diferentes do Cloud Manager, como Proprietário comercial, Gerenciador de implantação e Desenvolvedor.
* Atribua membros da equipe a perfis de produtos do Cloud Manager, como Proprietário comercial, Gerenciador de implantação e Desenvolvedor.

## Pré-requisitos {#prerequisites}

Os seguintes pré-requisitos devem ser considerados antes de iniciar esta seção. Você deve:

* Seja um Administrador do sistema e entenda [Perfis de produto do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).
* Entenda as noções básicas do [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en).
* Tenha detalhes sobre os membros da sua equipe. Um Administrador do sistema deve ter os nomes, endereços de email e as funções e responsabilidades dos membros da equipe que precisarão acessar o AEM como Cloud Service.

   >[!NOTE]
   >Para fins de integração, recomendamos que você adicione inicialmente usuários que participarão das tarefas imediatas, como administradores, desenvolvedores e autores de conteúdo. Você pode continuar o resto da integração sem adicionar todos os usuários. Depois de concluir a integração, você pode dimensionar para um número maior de usuários posteriormente.

## Revisar perfis de produto do Cloud Manager {#review-product-profiles}

Na Adobe Admin Console, é possível ver a lista de Perfis do Cloud Manager.

>[!NOTE]
>Antes de revisar os perfis de produto do Cloud Manager no Admin Console, é recomendável revisar os [Perfis de produto do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) disponíveis.

Siga as etapas abaixo para exibir a lista de Perfis do Cloud Manager:

1. Faça logon em [Adobe Admin Console](https://adminconsole.adobe.com/). Na página **Visão geral**, selecione **Adobe Experience Manager como um Cloud Service** no cartão **Produtos e serviços**.

   ![](/help/journey-onboarding/assets/assign-team1.png)

   >[!NOTE]
   >Consulte Fazer logon no Admin Console para saber como usar o Admin Console.


1. Navegue até a instância **Cloud Manager** a partir da lista de todas as instâncias.

   ![](/help/journey-onboarding/assets/assign-team2.png)

1. Você verá a lista de [perfis de produto do Cloud Manager pré-configurados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

   ![](/help/journey-onboarding/assets/assign-team3.png)


## Atribuir usuários ao perfil de produto do proprietário comercial {#assign-users-business-owner}

Agora você está pronto para adicionar usuários e atribuí-los ao perfil de produto Proprietário comercial do Cloud Manager.

>[!NOTE]
>Para fazer isso com êxito, no console de administração do Adobe, é necessário adicionar um usuário ao produto (AEM como Cloud Service neste caso) e [Perfil de produto Proprietário comercial do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

As etapas a seguir guiarão você por isso:

1. Identifique os usuários que gerenciarão os programas do Cloud Manager e adicione-os ao perfil de produto Proprietário comercial. O Administrador do sistema deve ser a primeira pessoa a acessar e fazer logon no Cloud Manager. Você deve adicionar a si mesmo (Administrador do sistema) ao perfil de produto Proprietário comercial primeiro.

1. Na página [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Visão geral**, selecione **Adobe Experience Manager como Cloud Service** produto da placa **Produtos e serviços** como mostrado abaixo.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione a guia **Users** no início da navegação e selecione **Adicionar usuário**.

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. Na caixa de diálogo **Adicionar usuários à sua equipe**, digite a ID do email do usuário que deseja adicionar. Para o Tipo de ID, selecione Adobe ID, se o Federated ID para os membros da equipe ainda não tiver sido configurado.

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. Na seleção Produto , selecione **Adobe Experience Manager como Cloud Service** e atribua o perfil de produto **Proprietário comercial** ao usuário, conforme mostrado abaixo.

   >[!NOTE]
   >Consulte [Cloud Manager product profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) para garantir que as funções certas sejam atribuídas aos usuários certos no Admin Console, conforme mostrado abaixo.

   ![](/help/journey-onboarding/assets/assign-team6.png)

   >[!NOTE]
   >Atribua o usuário a pelo menos um perfil de produto para que ele possa acessar o Cloud Manager. Lembre-se de atribuir a si mesmo (Administrador do sistema) ao Proprietário comercial.

1. Clique em **Salvar**. Um email de boas-vindas é enviado ao usuário adicionado. O usuário convidado pode acessar o Cloud Manager clicando no link do email de boas-vindas e fazendo logon usando a Adobe ID.

   Parabéns! Sua equipe recém-formada do Cloud Manager (incluindo você atribuído à função &quot;Proprietário comercial&quot;) foi configurada. Os membros receberão um email de boas-vindas convidando-os para fazer logon e acessar o Cloud Manager. Na função de Proprietário comercial, agora você está a apenas um passo de fazer logon no Cloud Manager e ativar a criação dos recursos de nuvem.

## Atribuir usuários ao perfil de produto do Gerenciador de implantação {#assign-users-deployment-manager}

1. Identifique os usuários que gerenciarão os programas do Cloud Manager e adicione-os ao perfil de produto do Deployment Manager. O Administrador do sistema deve ser a primeira pessoa a acessar e fazer logon no Cloud Manager. Primeiro, você deve adicionar a si mesmo (Administrador do sistema) ao perfil de produto Proprietário comercial (conforme descrito na seção anterior).

1. Na página [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Visão geral**, selecione **Adobe Experience Manager como Cloud Service** produto da placa **Produtos e serviços** como mostrado abaixo.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione a guia **Users** no início da navegação e selecione **Adicionar usuário**.

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. Na caixa de diálogo **Adicionar usuários à sua equipe**, digite a ID do email do usuário que deseja adicionar. Para o Tipo de ID, selecione Adobe ID, se o Federated ID para os membros da equipe ainda não tiver sido configurado.

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. Na seleção Produto , selecione **Adobe Experience Manager como Cloud Service** e atribua o perfil de produto **Gerenciador de implantação** ao usuário, conforme mostrado abaixo.

   >[!NOTE]
   >Consulte [Cloud Manager product profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) para garantir que as funções certas sejam atribuídas aos usuários certos no Admin Console, conforme mostrado abaixo.

   ![](/help/journey-onboarding/assets/assign-team6.png).

   >[!IMPORTANT]
   >O usuário pode ser adicionado ao perfil de produto do Gerenciador de implantação depois que os recursos do Cloud Manager forem criados.

## Atribuir usuários ao perfil de produto do desenvolvedor {#assign-users-developer}

1. Identifique os usuários que gerenciarão os programas do Cloud Manager e adicione-os ao perfil de produto do Desenvolvedor. O Administrador do sistema deve ser a primeira pessoa a acessar e fazer logon no Cloud Manager. Você deve adicionar a si mesmo (Administrador do sistema) ao perfil de produto Proprietário comercial primeiro.

1. Na página [Admin Console](https://adminconsole.adobe.com/enterprise/overview) **Visão geral**, selecione **Adobe Experience Manager como Cloud Service** produto da placa **Produtos e serviços** como mostrado abaixo.

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione a guia **Users** no início da navegação e selecione **Adicionar usuário**.

   ![](/help/journey-onboarding/assets/assign-team4.png)

1. Na caixa de diálogo **Adicionar usuários à sua equipe**, digite a ID do email do usuário que deseja adicionar. Para o Tipo de ID, selecione Adobe ID, se o Federated ID para os membros da equipe ainda não tiver sido configurado.

   >[!NOTE]
   >Para saber mais sobre tipos de identidade no Adobe Admin Console, consulte [Visão geral da identidade](https://helpx.adobe.com/enterprise/using/identity.html).

   ![](/help/journey-onboarding/assets/assign-team5.png)

1. Na seleção Produto , selecione **Adobe Experience Manager como Cloud Service** e atribua o perfil de produto **Desenvolvedor** ao usuário, conforme mostrado abaixo.

   >[!NOTE]
   >Consulte [Cloud Manager product profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles) para garantir que as funções certas sejam atribuídas aos usuários certos no Admin Console, conforme mostrado abaixo.

   ![](/help/journey-onboarding/assets/assign-team6.png).


   >[!IMPORTANT]
   >O usuário pode ser adicionado ao perfil de produto Desenvolvedor após a criação dos recursos do Cloud Manager.

## O que vem a seguir {#whats-next}

Você aprendeu sobre três perfis de produto diferentes do Cloud Manager, como Proprietário comercial, Gerenciador de implantação e Desenvolvedor. Em seguida, você atribuiu membros da equipe a perfis de produtos do Cloud Manager, como Proprietário comercial, Gerenciador de implantação e Desenvolvedor. Agora você está pronto para continuar sua jornada de integração ao revisar o documento [Configurar recursos da nuvem por meio do Cloud Manager](/help/journey-onboarding/sysadmin/setup-cloud-resources-via-cloud-manager.md), onde você aprenderá:

1. Como Administrador do sistema atribuído à função *Proprietário comercial*, você deve acessar e fazer logon no Cloud Manager.

1. Em seguida, um usuário do Cloud Manager na função *Proprietário comercial* pode fazer logon e configurar os recursos da nuvem, incluindo o Programa da nuvem e os Ambientes. Isso garantirá que sua equipe de especialistas possa começar a acessar o AEM como Cloud Service o mais rápido possível.

1. Depois que seu *Proprietário da empresa* configurar seus recursos de nuvem, os *Desenvolvedores* e os *Gerenciadores de implantação* que foram adicionados com êxito aos perfis de produto do Cloud Manager poderão acessar o Cloud Manager e se familiarizar como eles podem continuar em seu caminho de aprendizagem.

## Recursos adicionais {#additional-resources}

Siga os recursos adicionais para saber mais sobre:

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Perfis de produto do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Visão geral da identidade do Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
