---
title: 'Atribuir membros da equipe ao AEM como perfis de produto do Cloud Service '
description: Siga esta página para saber como atribuir membros da equipe ao AEM como perfis de produto do Cloud Service
hide: true
index: false
source-git-commit: 4a6408c498b093fc8b3baf4bdf1798b4281c90c2
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 2%

---


# Atribuir membros da equipe ao AEM como perfis de produto do Cloud Service {#assign-team-members-cloud-service}

## Objetivo {#objective}

Este documento ajuda você a entender as etapas que o Administrador do sistema deve tomar para atribuir os membros da equipe ao AEM como perfis de produto do Cloud Service e por que é crucial permitir que os autores do AEM iniciem sua jornada com o AEM.

Após ler esta seção, você deve entender:

* Por que e como os membros da equipe são atribuídos ao AEM como perfis de produto do Cloud Service.
* Como adicionar membros da equipe AEM perfil de produto do usuário.
* Como adicionar membros da equipe ao perfil de produto Administradores AEM.


## Introdução {#introduction}

Para receber acesso ao AEM como Cloud Service, os usuários devem pertencer a um dos dois perfis de produto:  `AEM Users` ou `AEM Administrators`. Os membros da equipe devem receber permissões para a instância do AEM, pois as permissões para administrar o Cloud Manager não serão suficientes.

>[!NOTE]
>Todos os usuários atribuídos a AEM perfil de produto do Usuário pelo administrador do sistema terão (somente leitura) acesso ao Cloud Manager.

## Pré-requisitos {#prerequisites}

Antes de começar a ler esta seção, você deve considerar seguir estes pré-requisitos:

* Entenda [AEM como um Cloud Service product profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)
* Familiarize-se com [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)
* Os perfis de produto do Cloud Manager foram atribuídos aos membros de sua equipe, conforme apropriado, e os recursos de nuvem foram configurados
* Detalhes sobre o membro da equipe: O Administrador do sistema deve ter os nomes e endereços de email e as funções e responsabilidades dos membros da equipe que precisarão acessar o AEM como Cloud Service.

   >[!NOTE]
   >Para fins de integração, recomendamos que você adicione inicialmente usuários que participarão das tarefas imediatas, como administradores, desenvolvedores e autores de conteúdo. Você pode continuar o resto da integração sem adicionar todos os usuários. Depois de concluir a integração, você pode dimensionar para um número maior de usuários posteriormente.


   >[!IMPORTANT]
   >Antes de começar a revisar as etapas para atribuir membros da equipe ao AEM como Perfis de produto do Cloud Service, siga estas duas etapas:
   >
   >1. Faça logon em [Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en). Consulte Fazer logon no Admin Console para obter mais detalhes.
      >
      >
   1. Revise [AEM como um Cloud Service Product Profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).


Siga as etapas abaixo para ver a lista de Perfis do Cloud Manager da Adobe Admin Console:

1. Faça logon em [Adobe Admin Console](https://adminconsole.adobe.com/). Na página **Visão geral**, selecione **Adobe Experience Manager como um Cloud Service** no cartão **Produtos e serviços**.

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. Navegue e selecione a instância (Instância do autor do ambiente de desenvolvimento), conforme mostrado na figura abaixo.

   ![](/help/onboarding/onboarding-journey/assets/cloud-profiles-1.png)


1. Você verá a lista de AEM como perfis de produto do Cloud Service que serão necessários para atribuir a um usuário com base em sua função.

   >[!NOTE]
   >Para saber mais sobre isso, consulte [AEM como um Cloud Service Product Profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/onboarding/onboarding-journey/assets/cloud-profiles-2.png)


## Adicionar membros da equipe ao perfil de produto AEM usuário ou administrador AEM {#add-team-members}

Para receber acesso ao AEM como uma instância do Cloud Service, os usuários devem pertencer a um dos dois perfis de produto `AEM Users` ou `AEM Administrators`.

>[!NOTE]
>Você deve receber permissões para a instância. As permissões para administrar o Cloud Manager não serão suficientes. Saiba mais.

As etapas abaixo devem ser seguidas por um Administrador de sistema que também esteja na função de Proprietário comercial.

1. Navegue até o seu programa pelo Cloud Manager e selecione o botão **Gerenciar Acesso** no contexto do ambiente de interesse, conforme mostrado abaixo.

   ![](/help/onboarding/onboarding-journey/assets/add-team1.png)

1. Uma nova guia navega até o Adobe Admin Console de onde você tem acesso à instância do autor do ambiente. Selecione **AEM Administradores** ou **AEM Usuários** com base nas permissões que esse indivíduo precisa conceder. Saiba mais sobre [AEM como um Cloud Service product profiles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles).

   ![](/help/onboarding/onboarding-journey/assets/add-team2.png)

1. Selecione `AEM Administrator` ou `AEM User` e clique em **Adicionar Usuário** como mostrado abaixo e envie os detalhes necessários para concluir a adição do membro da equipe.

   ![](/help/onboarding/onboarding-journey/assets/add-team3.png)

   O usuário adicionado agora terá acesso ao AEM como um Cloud Service Author services!

   >[!NOTE]
   >Você desejará repetir essas etapas para todos os ambientes, incluindo Desenvolvimento, Estágio e Produção, se tiver as informações dos membros da equipe que precisam de acesso disponíveis.


## O que vem a seguir {#whats-next}

Os usuários designados ao AEM como perfis de produto do Cloud Service agora estão prontos para acessar o Author e se familiarizar com a criação de páginas no AEM as a Cloud Service. Você deve seguir o caminho, revisando o documento Caminho de aprendizagem para [Usuários AEM](/help/onboarding/onboarding-journey/learning-path-aem-users.md) ou para [Desenvolvedores e Gerentes de implantação](/help/onboarding/onboarding-journey/learning-path-developers-deploymentmanagers.md).

## Recursos adicionais {#additional-resources}

* [Gerenciamento de produtos e acesso do usuário no Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console)
* [Configuração do acesso ao AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)
* [Guia de início rápido para a criação de páginas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=en)