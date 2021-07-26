---
title: Configuração de recursos da nuvem via Cloud Manager
description: Siga esta página para saber como configurar os Recursos da nuvem por meio do Cloud Manager
hide: true
hidefromtoc: true
index: false
source-git-commit: 5a909976909eb7ce2c008d2eac9ffb60e906023e
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 0%

---

# Configuração de recursos da nuvem via Cloud Manager {#setup-cloud-resources}

O Administrador do sistema atribuído à função *Proprietário comercial* deve acessar e fazer logon no Cloud Manager. Em seguida, um membro da equipe atribuído ao perfil de produto *Proprietário comercial* deve fazer logon no Cloud Manager e criar o programa e os ambientes de nuvem para que a equipe de especialistas possa começar.

## Objetivo {#objective}

Este documento ajuda você a entender como os recursos da nuvem são criados e quem pode fazê-lo.

Após ler esta seção, você deve entender:

* Um Administrador do sistema atribuído à função *Proprietário comercial* deve ser o primeiro a acessar e fazer logon no Cloud Manager.
* Como o programa em nuvem e os ambientes são criados.

## Introdução {#introduction}

A adição dos recursos da nuvem é feita pelo Cloud Manager pelo membro da equipe atribuído ao Perfil de produto do Proprietário comercial do Cloud Manager. Normalmente, esse indivíduo é aquele que entende as necessidades dos negócios e que conclui a configuração inicial do Cloud Manager.

Siga as seções abaixo para saber como criar seus [programas de serviço em nuvem](#create-cloud-service-program) e [ambientes](#create-cloud-environments).

### Pré-requisitos {#prerequisites}

* O Administrador do sistema atribuído à função *Proprietário comercial* deve acessar e fazer logon no Cloud Manager.

* Entenda como [navegar e fazer logon no Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en).

* Familiarize-se com os [perfis de produto do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

* Entenda as considerações para criar seu programa. Assista a este vídeo para saber mais.

* Entenda os conceitos do Cloud Manager [programas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html?lang=en) e [ambientes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en)

## Navegar para o Cloud Manager {#navigate-cloud-manager}

1. O usuário *Proprietário comercial* receberá um email de boas-vindas de onde pode começar, ou se não conseguir encontrá-lo, vá diretamente para [Adobe Experience Cloud](https://experience.adobe.com/#/@ccs/home) e faça logon usando sua Adobe ID.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources1.png)

1. Na página inicial do Adobe Experience Cloud, selecione **Experience Manager**.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources2.png)

1. Isso o levará à página inicial da AEM. A partir daqui, inicie o **Cloud Manager** .

   ![](/help/onboarding/onboarding-journey/assets/setup-resources3.png)

1. A página de aterrissagem do Cloud Manager é exibida, como mostrado na figura abaixo.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources4.png)

1. Verifique se você recebeu o Perfil de Produto do Proprietário Comercial. Para fazer isso, selecione o perfil na parte superior direita, conforme mostrado abaixo.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources5.png)

1. Selecione **Funções de Usuário** e verifique se você está atribuído ao Proprietário da Empresa.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources6.png)

1. Isso confirma sua função de usuário como um Proprietário comercial.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources7.png)

   Excelente trabalho! Você fez logon no Cloud Manager as a Business Owner!

## Criar programa Cloud Service {#create-cloud-service-program}

Siga as etapas abaixo para criar seu programa de serviços em nuvem pelo Cloud Manager:

1. Navegue até a página de aterrissagem do Cloud Manager, conforme mostrado abaixo.

   >[!NOTE]
   >Você deve ser um membro da equipe atribuído ao perfil de produto Proprietário comercial do Cloud Manager para concluir com êxito esta etapa.

   A partir daqui, clique em **Adicionar Programa** para iniciar o assistente Adicionar Programa.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources4.png)

   >[!NOTE]
   >Assista ao [vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en) para saber como criar seu AEM as a Cloud e saber mais sobre considerações importantes antes de criar seu programa.

   >[!IMPORTANT]
   >Para obter instruções passo a passo sobre como usar o assistente Adicionar programa, acesse [aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=en).
   >
   >* Lembre-se de que o nome do programa não pode ser alterado após a criação. Recomendamos que você tenha certeza sobre qual nome deseja dar ao seu programa.
   >* Caso seja necessário alterar o nome do seu programa, isso envolverá a abertura de um caso com o Suporte do Adobe ou, alternativamente, o contato com seu representante do Adobe. Eles ajudarão a excluir o programa com eficácia. Terá de começar tudo de novo com a potencial perda de trabalho que a equipe fez.


1. Após a criação bem-sucedida do programa em nuvem, você pode navegar até o programa para visualizar a página **Visão geral** do programa, conforme mostrado abaixo.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources8.png)

   >[!NOTE]
   >Se você ainda não tiver feito isso, agora é um bom momento para adicionar seus membros do Desenvolvedor à sua equipe do Cloud Manager. Consulte Adicionar usuários ao perfil de produto do desenvolvedor e siga as etapas descritas.

1. Os membros atribuídos ao perfil de produto do Desenvolvedor podem fazer logon no Cloud Manager e no [Gerenciar Git do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en).

   Excelente trabalho! Agora que seu programa foi criado com sucesso, seu Git do Cloud Manager está disponível para que seus desenvolvedores acessem!


## Criar os ambientes do Cloud {#create-cloud-environments}

Depois de criar o programa de nuvem com sucesso, crie os ambientes de nuvem.

Siga as etapas abaixo para criar seus ambientes de nuvem a partir do Cloud Manager:

1. Navegue até a página **Visão geral** do Cloud Manager e selecione **Adicionar** no cartão de ambiente.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources9.png)

   >[!IMPORTANT]
   >Um usuário do Cloud Manager na função Proprietário da empresa ou Gerenciador de implantação deve estar conectado para concluir esta etapa com êxito.

   Além disso, assista ao tutorial rápido de [vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en) para saber mais sobre os ambientes do Cloud Manager e como adicioná-los ao seu programa.

1. Isso iniciará o assistente para adicionar ambiente que guiará a adição do ambiente. Adicione seu ambiente de desenvolvimento primeiro para se familiarizar. Consulte [Adicionar um ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#adding-environments) para saber mais.

   >[!NOTE]
   >Se você ainda não tiver feito isso, agora é um bom momento para adicionar seus membros do Desenvolvedor à sua equipe do Cloud Manager. Consulte Adicionar usuários ao perfil de produto do desenvolvedor e siga as etapas descritas.

1. Os membros atribuídos ao perfil de produto do Desenvolvedor podem fazer logon no Cloud Manager e no [Gerenciar Git do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en).

   Excelente trabalho! Agora que seu programa foi criado com sucesso, seu Git do Cloud Manager está disponível para que seus desenvolvedores acessem!

   Parabéns! Agora, seus ambientes do programa em nuvem foram criados e seus Desenvolvedores foram adicionados à equipe!

## O que vem a seguir {#whats-next}

Os membros da equipe devem receber permissões para a instância, pois as permissões para administrar o Cloud Manager não serão suficientes. Agora que os recursos da nuvem foram criados e estão prontos para serem acessados pela sua equipe, o Administrador do sistema deve atribuir os membros da sua equipe ao AEM como perfis de produto do Cloud Service da Adobe Admin Console.

>[!NOTE]
>Para receber acesso ao AEM como Cloud Service, os usuários devem pertencer a um dos dois perfis de produto `AEM Users` ou `AEM Administrators`. Consulte [Gerenciamento de produtos e acesso do usuário no Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console) para saber mais.

Você deve continuar sua jornada de integração revisando o documento Atribuindo membros da equipe ao AEM como perfis de produto do Cloud Service.


## Recursos adicionais {#additional-resources}

Siga os recursos adicionais para saber mais sobre:

* [Tipos de programas e adição de um programa](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)
* [Tipos de ambiente e adição de um ambiente](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en)
* [Gerenciamento do Git do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)
* [Configuração do acesso ao AEM como um Cloud Service do Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#adobe-ims-users)
