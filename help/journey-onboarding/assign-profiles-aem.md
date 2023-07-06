---
title: Atribuição de perfis de produto do AEM
description: Após configurar os recursos de nuvem, é necessário conceder à equipe acesso ao AEM usando perfis de produto do AEM.
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 94%

---

# Atribuição de perfis de produto do AEM {#assign-profiles-aem}

>[!CONTEXTUALHELP]
>id="assets_user_entitlements"
>title="Atribuir perfis de produto do AEM"
>abstract="Você não tem autorização para usar o Experience Manager Assets. Entre em contato com a administração."

Nesta parte da [jornada de integração,](overview.md) você aprenderá a conceder à sua equipe acesso ao AEM usando perfis de produto do AEM.

## Objetivo {#objective}

Depois de ler o documento anterior nesta jornada de integração, [Criar ambientes,](create-environments.md) e configurar os recursos de nuvem, será necessário conceder à sua equipe acesso ao AEM usando perfis de produto do AEM. Como administrador do sistema, faça isso atribuindo perfis de produto do AEM.

Depois de ler este documento, você deverá entender:

* O que são perfis de produto do AEM.
* Como adicionar membros da equipe ao perfil de produto Usuário do AEM.
* Como adicionar membros da equipe ao perfil de produto Administradores do AEM.

## Perfis de produto do AEM {#aem-product-profiles}

Para usar o AEM, os membros da equipe devem ser atribuídos a pelo menos um perfil de produto do AEM. As permissões para acessar o Cloud Manager não serão suficientes. Os usuários devem pertencer a um dos dois perfis de produto:

* `AEM Users` - Esse grupo inclui usuários normais que realizam tarefas diárias de criação de conteúdo.
* `AEM Administrators` - Esse grupo inclui usuários responsáveis por recursos avançados ou pelo AEM.

>[!NOTE]
>
>Todos os usuários atribuídos a um perfil de produto AEM as a Cloud Service têm acesso de somente leitura ao Cloud Manager por meio da função **Usuário do Cloud Manager**.
>
>Usuários com o **Cloud Manager** Somente a função de usuário pode fazer logon no Cloud Manager e navegar até os ambientes do autor do AEM (se existirem) usando as opções do menu Programas. A função de **Usuário do Cloud Manager** não é suficiente para acessar os detalhes do programa. Se tal acesso for necessário, os usuários devem receber funções adicionais pelo administrador do sistema.
>Consulte a [Seção Recursos adicionais abaixo](#additional-resources) para obter mais informações sobre as funções de usuário do Cloud Manager.

>[!CAUTION]
>
>Não edite nem exclua os perfis de produto com os nomes Administradores do AEM ou Usuários do AEM. A edição dos nomes desses perfis pode interromper o logon na instância de nuvem do AEM.

## Pré-requisitos {#prerequisites}

Antes de começar a ler esta seção, você deve ter as informações a seguir sobre a equipe que usará o AEM.

* Nomes
* Endereços de email
* Funções e responsabilidades

>[!TIP]
>
>Para fins de integração, recomendamos que você adicione inicialmente os usuários que participarão das tarefas imediatas, como administradores, desenvolvedores e autores de conteúdo. Você pode continuar o resto da integração sem adicionar todos os usuários. Depois de concluir a integração, você pode dimensionar para um número maior de usuários posteriormente.

## Exibir perfis de produto do AEM {#view-profiles}

Siga estas etapas para ver os perfis de produto do AEM no Admin Console.

1. Faça logon no Admin Console em [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. Na página **Visão geral**, selecione **Adobe Experience Manager as a Cloud Service** no cartão **Produtos e serviços**.

   ![Cartão Produtos e serviços](/help/journey-onboarding/assets/assign-team1.png)

1. Navegue e selecione a instância.

   ![Selecionar instância](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. Você verá a lista de perfis de produto do AEM as a Cloud Service que podem ser atribuídos a um usuário com base em suas funções.

   ![Perfis de produto](/help/journey-onboarding/assets/cloud-profiles-2.png)

## Adicionar membros da equipe a perfis de produto {#add-team-members}

Agora que você está familiarizado com os perfis disponíveis, pode atribuí-los conforme necessário aos membros da equipe.

Essas tarefas exigem que você seja um administrador do sistema com o perfil de produto **Proprietário da empresa** no Cloud Manager.

1. Navegue até o seu programa pelo Cloud Manager e clique no botão **Gerenciar acesso** no contexto do ambiente de interesse.

   ![Gerenciar acesso](/help/journey-onboarding/assets/add-team1.png)

1. Uma nova guia direciona você para o Admin Console para acessar a instância do autor do ambiente. Selecione **Administradores do AEM** ou **Usuários do AEM** com base nas permissões que esse indivíduo precisa receber.

   ![Atribuir acesso](/help/journey-onboarding/assets/add-team2.png)

1. Selecione `AEM Administrator` ou `AEM User` e clique em **Adicionar usuário** como mostrado abaixo e envie os detalhes necessários para concluir a adição do membro da equipe.

   ![Adicionar membro da equipe](/help/journey-onboarding/assets/add-team3.png)

1. Repita essas etapas para todos os ambientes, incluindo os de desenvolvimento, preparo e produção, se você tiver as informações dos membros da equipe que precisam de acesso.

O usuário que você adicionou terá acesso aos serviços de autoria do AEM as a Cloud Service!

## Fim da jornada? {#the-end}

Parabéns! Os usuários atribuídos a perfis de produto do AEM as a Cloud Service agora estão prontos para acessar o ambiente de autoria do AEM e começar a criar conteúdo usando o AEM as a Cloud Service. Da mesma forma, os desenvolvedores agora podem acessar o Cloud Manager para usar o Git para armazenar o código de aplicativo personalizado e implantá-lo. Nesse sentido, a jornada de integração está concluída e os usuários agora podem usar o AEMaaCS.

No entanto, se você quiser entender melhor como os autores e desenvolvedores usam o sistema, continue com as duas partes opcionais desta jornada de integração:

* [Tarefas do desenvolvedor e do gerente de implantação](developers.md) - Onde você aprenderá como os desenvolvedores acessam o Git para armazenar o código personalizado e implantá-lo usando os pipelines do Cloud Manager.
* [Tarefas do usuário do AEM](aem-users.md) - Onde você aprenderá a acessar o ambiente do AEM para começar a criar conteúdo.

## Recursos adicionais {#additional-resources}

A seguir estão recursos adicionais e opcionais se quiser ir além do conteúdo da jornada de integração.

* [Perfis de produto e de equipe do AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) - Saiba como os perfis de produto e de equipe do AEM as a Cloud Service podem conceder e limitar o acesso às soluções licenciadas da Adobe.
* [Gerenciamento de produtos e acesso do usuário no Admin Console](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) - Saiba como usar o Admin Console para gerenciar o acesso dos usuários.
* [Apresentação sobre como configurar o acesso ao AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html) - Confira esta apresentação resumida para saber mais sobre como configurar usuários, grupos de usuários e perfis de produto do Adobe IMS no Admin Console.

