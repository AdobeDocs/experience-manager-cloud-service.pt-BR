---
title: Configuração de recursos da nuvem via Cloud Manager
description: Siga esta página para saber como configurar os Recursos da nuvem por meio do Cloud Manager
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 7fe39bbc8d5e965af7f339b2a524420c76360552
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---

# Configuração de recursos da nuvem via Cloud Manager {#setup-cloud-resources}

O Administrador do sistema atribuído à função Proprietário comercial deve acessar e fazer logon no Cloud Manager. Em seguida, um membro da equipe atribuído ao perfil de produto Proprietário comercial deve fazer logon no Cloud Manager e criar seu programa e ambientes de nuvem para que a equipe de especialistas possa começar.

## Objetivo {#objective}

Este documento ajuda você a entender como os recursos da nuvem são criados e quem pode fazê-lo.

Após ler esta seção, você deve entender:

* Um Administrador do sistema atribuído à função Proprietário comercial deve ser o primeiro a acessar e fazer logon no Cloud Manager.
* Como o programa em nuvem e os ambientes são criados.

## Introdução {#introduction}

A adição dos recursos da nuvem é feita pelo Cloud Manager pelo membro da equipe atribuído ao Perfil de produto do Proprietário comercial do Cloud Manager. Normalmente, esse indivíduo é aquele que entende as necessidades dos negócios e que conclui a configuração inicial do Cloud Manager.

Siga as seções abaixo para saber como criar seu [programas do serviço em nuvem](#create-cloud-service-program) e [ambientes .](#create-cloud-environments)

### Pré-requisitos {#prerequisites}

* O Administrador do sistema atribuído à função Proprietário comercial deve acessar e fazer logon no Cloud Manager.

* Entenda como [navegue e faça logon no Cloud Manager.](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* Familiarize-se com [Perfis de produto do Cloud Manager.](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* Entender os conceitos do Cloud Manager [programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/understand-program-types.md) e [ambientes .](/help/implementing/cloud-manager/manage-environments.md)

## Navegar para o Cloud Manager {#navigate-cloud-manager}

O usuário Proprietário comercial receberá um email de boas-vindas com um link para começar ou, se não conseguir encontrá-lo, acessar [Cloud Manager](https://my.cloudmanager.adobe.com/) fazendo logon diretamente usando sua Adobe ID.

Siga as etapas abaixo para navegar até o Cloud Manager:

1. Em seu email de boas-vindas, clique em **Introdução**, conforme mostrado na figura abaixo.
   ![](/help/journey-onboarding/assets/get-started-email.png)

1. Você navegará até o **Programas e produtos** página.

   >[!IMPORTANT]
   >
   >Como alternativa, você também pode navegar diretamente para a página de logon do Cloud Manager a partir de [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). Marque esta página como referência futura e para ajudá-lo a navegar diretamente para a página de aterrissagem do Cloud Manager.

1. Você será direcionado para a página de aterrissagem do Cloud Manager. Consulte [Visualização dos programas do Cloud Manager](#viewing-programs) para obter mais detalhes.

Além disso, você pode navegar até o **Programas e produtos** página inicial do Adobe Experience Cloud. Siga as etapas abaixo:

1. Navegue diretamente para [Adobe Experience Cloud](https://experience.adobe.com) e faça logon usando sua Adobe ID.

1. Na página inicial do Adobe Experience Cloud, selecione **Experience Manager**.

   ![](/help/journey-onboarding/assets/setup-resources2.png)

1. Isso o levará à página inicial da AEM. A partir daqui, inicie **Cloud Manager** .

   ![](/help/journey-onboarding/assets/setup-resources3.png)

1. Após o logon bem-sucedido, você será direcionado para a página inicial do Cloud Manager. Consulte [Visualização dos programas do Cloud Manager](#viewing-programs) para obter mais detalhes.

   >[!NOTE]
   >
   >Dependendo das funções atribuídas em [!UICONTROL Cloud Manager] e o estado do aplicativo, você verá telas diferentes ao usar [!UICONTROL Cloud Manager] IU.

### Visualização de programas na página de aterrissagem do Cloud Manager {#viewing-programs}

Após o logon bem-sucedido, você será direcionado para a página inicial do Cloud Manager. Você verá uma das três opções, descritas abaixo:

#### Quando nenhum programa existe no Cloud Manager {#no-programs}

Se não houver programas em sua organização, a landing page direcionará você para criar seu primeiro programa, como mostrado na figura abaixo.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### Quando programas já existem no Cloud Manager {#programs-exist}

Se o(s) programa(s) já existir(em) em sua Organização, a landing page o direcionará para adicionar outro programa e exibirá todos os programas existentes também, como mostrado na figura abaixo.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### Quando um programa existe e o usuário é o Administrador do sistema {#programs-exist-sysadmin}

Se o(s) programa(s) já existir(em) em sua organização e você for um Administrador do sistema, sua landing page será exibida **Gerenciar acesso** botão junto com **Adicionar programa** , conforme mostrado na figura abaixo.

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## Verificando suas funções de usuário {#verify-user-roles}

Depois de fazer logon no Cloud Manager com êxito, siga as etapas abaixo para verificar se o Perfil de produto do proprietário de negócios foi atribuído a você:

1. Selecione o perfil no canto superior direito, como mostrado abaixo.

   ![](/help/journey-onboarding/assets/setup-resources5.png)

1. Selecionar **Funções do usuário** e certifique-se de que você esteja atribuído ao Proprietário comercial.

   ![](/help/journey-onboarding/assets/setup-resources6.png)

1. Isso confirma sua função de usuário como um Proprietário comercial.

   ![](/help/journey-onboarding/assets/setup-resources7.png)

   Excelente trabalho! Você fez logon no Cloud Manager as a Business Owner!

## Criar programa Cloud Service {#create-cloud-service-program}

Siga as etapas abaixo para criar seu programa de serviços em nuvem pelo Cloud Manager:

1. Navegue até a página de aterrissagem do Cloud Manager, conforme mostrado abaixo.

   >[!NOTE]
   >
   >Você deve ser um membro da equipe atribuído ao perfil de produto Proprietário comercial do Cloud Manager para concluir com êxito esta etapa.

   Clique aqui em **Adicionar programa** para iniciar o assistente Adicionar programa .

   ![](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >Observe a [vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) para saber como criar seu AEM as a Cloud program e saber mais sobre considerações importantes antes de criar seu programa.

   >[!TIP]
   >
   >Para obter instruções passo a passo sobre como usar o assistente Adicionar programa, acesse [here](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-program.md).

1. Após a criação bem-sucedida do seu programa em nuvem, você pode navegar até o programa para ver o **Visão geral** do seu programa, conforme mostrado abaixo.

   ![](/help/journey-onboarding/assets/setup-resources8.png)

   >[!NOTE]
   >
   >Se você ainda não tiver feito isso, agora é um bom momento para adicionar seus membros do Desenvolvedor à sua equipe do Cloud Manager. Consulte Adicionar usuários ao perfil de produto do desenvolvedor e siga as etapas descritas.

1. Os membros atribuídos ao perfil de produto do Desenvolvedor podem fazer logon no Cloud Manager e [Gerenciar Git Do Cloud Manager](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

   Excelente trabalho! Agora que seu programa foi criado com sucesso, seu Git do Cloud Manager está disponível para que seus desenvolvedores acessem!


## Criar os ambientes do Cloud {#create-cloud-environments}

Depois de criar o programa de nuvem com sucesso, crie os ambientes de nuvem.

Siga as etapas abaixo para criar seus ambientes de nuvem a partir do Cloud Manager:

1. Navegue até o **Visão geral** e selecione **Adicionar** no cartão de ambiente.

   ![](/help/journey-onboarding/assets/setup-resources9.png)

   >[!IMPORTANT]
   >
   >Um usuário do Cloud Manager na função Proprietário da empresa ou Gerenciador de implantação deve estar conectado para concluir esta etapa com êxito.

   Além disso, assista o rápido [vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) para saber mais sobre os ambientes do Cloud Manager e como adicioná-los ao seu programa.

1. Isso iniciará o assistente para adicionar ambiente que o guiará pela adição do ambiente. Adicione seu ambiente de desenvolvimento primeiro para se familiarizar com o assistente. Consulte [Adicionar um ambiente](/help/implementing/cloud-manager/manage-environments.md#adding-environments) para saber mais.

   >[!NOTE]
   >
   >Se você ainda não tiver feito isso, agora é um bom momento para adicionar seus membros do Desenvolvedor à sua equipe do Cloud Manager. Consulte Adicionar usuários ao perfil de produto do desenvolvedor e siga as etapas descritas.

1. Os membros atribuídos ao perfil de produto do Desenvolvedor podem fazer logon no Cloud Manager e [Gerenciar Git Do Cloud Manager.](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

   Excelente trabalho! Agora que seu programa foi criado com sucesso e seu Git do Cloud Manager está disponível para que seus desenvolvedores acessem!

   Parabéns! Agora, seus ambientes do programa em nuvem foram criados e seus Desenvolvedores foram adicionados à equipe!

## O que vem a seguir {#whats-next}

Os membros da equipe devem receber permissões para a instância, pois as permissões para administrar o Cloud Manager não serão suficientes. Agora que os recursos da nuvem foram criados e estão prontos para serem acessados pela sua equipe, o Administrador do sistema deve atribuir os membros da sua equipe a AEM perfis de produto as a Cloud Service da Adobe Admin Console.

>[!NOTE]
>
>Para ter acesso AEM usuários as a Cloud Service deve pertencer a um dos dois perfis de produto `AEM Users` ou `AEM Administrators`. Consulte [Gerenciamento de produtos e acesso do usuário no Admin Console](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) para saber mais.

Você deve continuar sua jornada de integração ao revisar o documento [Atribuindo membros da equipe a AEM perfis de produto as a Cloud Service.](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md)


## Recursos adicionais {#additional-resources}

Siga os recursos adicionais para saber mais sobre:

* [Tipos de programas e adição de um programa](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [Tipos de ambiente e adição de um ambiente](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [Gerenciamento do Git do Cloud Manager](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [Configuração do acesso a AEM as a Cloud Service do Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
