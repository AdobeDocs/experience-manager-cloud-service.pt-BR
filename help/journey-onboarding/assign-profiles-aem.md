---
title: Atribuir perfis de produto AEM
description: Após configurar os recursos da nuvem, é necessário conceder à equipe acesso ao AEM usando AEM perfis de produto.
feature: Onboarding
role: Admin, User, Developer
exl-id: c00f5d28-85af-4bd3-a50c-913d1342241c
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---

# Atribuir perfis de produto AEM {#assign-profiles-aem}

Nesta parte do [jornada de integração,](overview.md) você aprenderá a conceder acesso de equipe ao AEM usando AEM perfis de produto.

## Objetivo {#objective}

Depois de ler o documento anterior nesta jornada de integração, [Criar ambientes,](create-environments.md) e tiver os recursos de nuvem configurados, será necessário conceder à equipe acesso ao AEM usando AEM perfis de produto. Como administrador do sistema, faça isso atribuindo AEM perfis de produto.

Depois de ler este documento, você deve entender:

* O que são AEM perfis de produto.
* Como adicionar membros da equipe AEM perfil de produto do usuário.
* Como adicionar membros da equipe ao perfil de produto Administradores AEM.

## Perfis de produto AEM {#aem-product-profiles}

Para usar AEM, os membros da equipe devem ser atribuídos a pelo menos um perfil de produto AEM. As permissões para acessar o Cloud Manager não serão suficientes. Os usuários devem pertencer a um dos dois perfis de produto:

* `AEM Users` - Esse grupo inclui usuários normais que realizam tarefas diárias de criação de conteúdo.
* `AEM Administrators` - Esse grupo inclui usuários responsáveis por recursos ou AEM avançados.

Todos os usuários atribuídos a um perfil de produto AEM também terão acesso somente leitura ao Cloud Manager. O acesso de gravação ao Cloud Manager pode ser concedido por meio de outros perfis de produto.

## Pré-requisitos {#prerequisites}

Antes de começar a ler esta seção, você deve ter as seguintes informações disponíveis sobre sua equipe que usará o AEM.

* Nomes
* Endereços de email
* Funções e responsabilidades

>[!TIP]
>
>Para fins de integração, recomendamos que você adicione inicialmente usuários que participarão das tarefas imediatas, como administradores, desenvolvedores e autores de conteúdo. Você pode continuar o resto da integração sem adicionar todos os usuários. Depois de concluir a integração, você pode dimensionar para um número maior de usuários posteriormente.

## Exibir AEM perfis de produto {#view-profiles}

Siga estas etapas para ver os perfis de produto AEM do Admin Console.

1. Faça logon no Admin Console at [`https://adminconsole.adobe.com`.](https://adminconsole.adobe.com)

1. No **Visão geral** página, selecione **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

   ![Cartão de produtos e serviços](/help/journey-onboarding/assets/assign-team1.png)

1. Navegue e selecione a instância.

   ![Selecionar instância](/help/journey-onboarding/assets/cloud-profiles-1.png)

1. Você verá a lista de AEM perfis de produto as a Cloud Service que podem ser atribuídos a um usuário com base em suas funções.

   ![Perfis de produto](/help/journey-onboarding/assets/cloud-profiles-2.png)

## Adicionar membros da equipe aos perfis de produto {#add-team-members}

Agora que você está familiarizado com os perfis disponíveis, é possível atribuí-los conforme necessário aos membros da equipe.

Essas tarefas exigem que você seja um administrador do sistema com a função **Proprietário da empresa** Perfil de produto do Cloud Manager.

1. Navegue até o seu programa pelo Cloud Manager e selecione o **Gerenciar acesso** no contexto do ambiente de interesse.

   ![Gerenciar acesso](/help/journey-onboarding/assets/add-team1.png)

1. Uma nova guia navega até a Admin Console, de onde você tem acesso à instância do autor do ambiente. Selecionar **Administradores de AEM** ou **Usuários AEM** com base nas permissões que esse indivíduo precisa receber.

   ![Atribuir acesso](/help/journey-onboarding/assets/add-team2.png)

1. Selecionar `AEM Administrator` ou `AEM User` e clique em **Adicionar usuário** como mostrado abaixo e envie os detalhes necessários para concluir a adição do membro da equipe.

   ![Adicionar membro da equipe](/help/journey-onboarding/assets/add-team3.png)

1. Repita essas etapas para todos os ambientes, incluindo desenvolvimento, armazenamento temporário e produção, se você tiver as informações dos membros da equipe que precisam de acesso disponíveis.

O usuário que você adicionou agora terá acesso aos AEM serviços de Autor as a Cloud Service!

## Fim da jornada? {#the-end}

Parabéns. Os usuários atribuídos a AEM perfis de produto as a Cloud Service agora estão prontos para acessar o ambiente de criação de AEM e começar a criar conteúdo com AEM as a Cloud Service. Da mesma forma, os desenvolvedores agora podem acessar o Cloud Manager para usar o git para armazenar o código de aplicativo personalizado e implantá-lo. Nesse sentido, a jornada de integração está concluída e os usuários agora podem usar o AEMaaCS.

No entanto, se você quiser entender melhor como os autores e desenvolvedores usam o sistema, continue com duas partes opcionais dessa jornada de integração:

* [Tarefas do desenvolvedor e do gerenciador de implantação](developers.md) - Onde você aprenderá como os desenvolvedores acessam o git para armazenar seu código personalizado e implantá-lo usando os pipelines do Cloud Manager.
* [Tarefas do usuário AEM](aem-users.md) - Onde você aprenderá a acessar o ambiente de AEM, onde poderá começar a criar conteúdo.

## Recursos adicionais {#additional-resources}

* [Gerenciamento de produtos e acesso do usuário no Admin Console](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) - Saiba como usar o Admin Console para gerenciar o acesso de uso.
* [Configuração do acesso ao AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en) - Confira esta apresentação resumida para saber mais sobre como configurar usuários do Adobe IMS, grupos de usuários e perfis de produtos no Admin Console.

