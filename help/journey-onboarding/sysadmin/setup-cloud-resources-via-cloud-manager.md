---
title: Configuração de recursos da nuvem pelo Cloud Manager
description: Saiba como usar o Cloud Manager para configurar e gerenciar seus próprios recursos de nuvem.
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 0db24518610fccf0d2ea5e0620a0c6a5f8009ea8
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 1%

---

# Configuração de recursos da nuvem pelo Cloud Manager {#setup-cloud-resources}

Saiba como usar o Cloud Manager para configurar e gerenciar seus próprios recursos de nuvem.

## Objetivo {#objective}

Este documento ajuda você a entender como os recursos da nuvem são criados e quem pode criá-los. Após ler esta seção, você deve entender:

* Um Administrador do sistema atribuído ao **Proprietário da empresa** deve ser a primeira função em sua organização a fazer logon e acessar o Cloud Manager.
* Como o programa em nuvem e os ambientes são criados.

## Introdução {#introduction}

A adição dos recursos de nuvem é feita pelo Cloud Manager pelo membro da equipe atribuído ao **Proprietário da empresa** perfil do produto. Normalmente, esse indivíduo é aquele que entende as necessidades dos negócios e que conclui a configuração inicial do Cloud Manager.

Siga as seções abaixo para saber como criar seu [programas do serviço em nuvem](#create-cloud-service-program) e [ambientes .](#create-cloud-environments)

### Pré-requisitos {#prerequisites}

* O Administrador do sistema atribuído ao **Proprietário da empresa** deve ter feito logon no Cloud Manager antes de qualquer outro usuário com a função **Proprietário da empresa** tentativa de acessar o Cloud Manager para executar e as etapas descritas neste documento.

   * Retorne ao [Atribuir membros da equipe aos perfis de produto do Cloud Manager](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) documento dessa jornada para obter mais informações.

* Você deve entender como [navegue e faça logon no Cloud Manager.](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* Você deve estar familiarizado com [Perfis de produto do Cloud Manager.](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* Você deve entender os conceitos do Cloud Manager [programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) e [ambientes .](/help/implementing/cloud-manager/manage-environments.md)

## Acesse o Cloud Manager como Administrador do sistema e Proprietário comercial {#access-sysadmin-bo}

Antes dos membros da equipe que você atribuiu à **Proprietário da empresa** pode acessar o cloud manager e começar a criar recursos na nuvem, o Administrador do Sistema deve receber a função **Proprietário da empresa** e faça logon no Cloud Manager.

1. Certifique-se de que você, como Administrador do sistema, tenha a **Proprietário da empresa** função atribuída.

   * Retorne à etapa anterior desta jornada, [Atribuir membros da equipe aos perfis de produto do Cloud Manager,](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) para obter mais informações sobre como atribuir a variável **Proprietário da empresa** para o Administrador do sistema, se você ainda não tiver feito isso.

1. Faça logon no Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e ser apresentada com a página de aterrissagem normal.

Ao fazer logon como Administrador do sistema com o **Proprietário da empresa** , você inicializa o Cloud Manager para uso pelos outros usuários com a função **Proprietário da empresa** função. Você não receberá uma confirmação desta ou de qualquer mensagem. Basta fazer logon.

Até você entrar no Cloud Manager como Administrador do sistema com a **Proprietário da empresa** , outros usuários com a função **Proprietário da empresa** A função não poderá criar programas no Cloud Manager mesmo se as funções corretas forem atribuídas a eles.

## Navegar para o Cloud Manager {#navigate-cloud-manager}

O usuário com a **Proprietário da empresa** A função receberá um email de boas-vindas com um link para começar. Siga as etapas abaixo para navegar até o Cloud Manager usando esse email de boas-vindas.

1. Em seu email de boas-vindas, clique em **Introdução**, conforme mostrado na figura abaixo.
   ![Exemplo de email](/help/journey-onboarding/assets/get-started-email.png)

1. Você navegará até o **Programas e produtos** página.

   >[!TIP]
   >
   >Você também pode navegar diretamente para a página de logon do Cloud Manager a partir de [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/). Marque esta página para referência futura.

1. Você será direcionado para a página de aterrissagem do Cloud Manager. Consulte [Visualização dos programas do Cloud Manager](#viewing-programs) para obter mais detalhes.

Também é possível navegar para o **Programas e produtos** da página inicial do Adobe Experience Cloud seguindo essas etapas

1. Navegue diretamente para [Adobe Experience Cloud](https://experience.adobe.com) e faça logon usando sua Adobe ID.

1. Na página inicial do Adobe Experience Cloud, selecione **Experience Manager**.

   ![Experience Cloud homepage](/help/journey-onboarding/assets/setup-resources2.png)

1. Isso o levará à página inicial da AEM. Aqui, clique em **Launch** no **Cloud Manager** mosaico.

   ![Página inicial do AEM](/help/journey-onboarding/assets/setup-resources3.png)

1. Após o logon bem-sucedido, você será direcionado para a página inicial do Cloud Manager. Consulte [Visualização dos programas do Cloud Manager](#viewing-programs) para obter mais detalhes.

A maneira como você acessa seus programas e produtos por meio do Cloud Manager é da sua responsabilidade e não afeta a forma como você usa o Cloud Manager ou como gerencia seus programas.

>[!NOTE]
>
>Dependendo das funções atribuídas em [!UICONTROL Cloud Manager] e o estado do aplicativo, você verá telas diferentes ao usar [!UICONTROL Cloud Manager] IU.

### Exibindo programas {#viewing-programs}

Depois de acessar o Cloud Manager com êxito, o que você vê dependerá do estado dos programas, conforme detalhado nas seções a seguir.

#### Quando Não Existem Programas {#no-programs}

Se não houver programas em sua organização, a landing page o direcionará para criar seu primeiro programa.

![Nenhum programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### Quando já existem programas {#programs-exist}

Se programas já existirem em sua organização, sua landing page exibirá seus programas existentes e também oferecerá um botão para adicionar outros programas.

![Existem programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### Quando um programa existe e você é um administrador do sistema {#programs-exist-sysadmin}

Se já houver programas em sua organização e você for o Administrador do sistema, sua landing page será exibida **Gerenciar acesso** botão junto com **Adicionar programa** opção.

![Exibição do administrador do sistema](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## Verificando suas funções de usuário {#verify-user-roles}

Depois de fazer logon no Cloud Manager com êxito, você pode verificar se recebeu a variável **Proprietário da empresa** perfil do produto.

1. Selecione o perfil na parte superior direita da janela.

   ![Perfil de usuário](/help/journey-onboarding/assets/setup-resources5.png)

1. Selecionar **Funções do usuário** para exibir as funções atribuídas ao usuário.

   ![Funções do usuário](/help/journey-onboarding/assets/setup-resources6.png)

1. Confirma que o usuário tem a variável **Proprietário da empresa** função.

   ![Lista de funções de usuário](/help/journey-onboarding/assets/setup-resources7.png)

Você fez logon no Cloud Manager as a Business Owner! Se você não receber a atribuição de **Proprietário da empresa** , entre em contato com o administrador do sistema.

## Criar um programa Cloud Service {#create-cloud-service-program}

Agora que você assegurou o acesso apropriado, é possível criar seu primeiro programa.

1. Navegue até a página de aterrissagem do Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e faça logon.

1. Na página de aterrissagem do Cloud Manager, clique em **Adicionar programa** para iniciar o assistente Adicionar programa .

   ![Página de aterrissagem](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >Para obter as instruções passo a passo sobre como usar o assistente Adicionar programa, consulte o documento [Criação de programas de produção](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) ou observe isso [vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) para saber como criar seu AEM as a Cloud program e saber mais sobre considerações importantes antes de criar seu programa.


1. Após a criação bem-sucedida do programa em nuvem, você pode navegar até o programa na página de aterrissagem do Cloud Manager para ver o **Visão geral** página do seu programa.

   ![Visão geral do programa](/help/journey-onboarding/assets/setup-resources8.png)

1. Os membros atribuídos ao perfil de produto do Desenvolvedor podem fazer logon no Cloud Manager e gerenciar repositórios de git do Cloud Manager.

   * Se você ainda não tiver feito isso, agora é um bom momento para atribuir membros ao **Desenvolvedor** na equipe do Cloud Manager. Retorne ao [Atribuir membros da equipe aos perfis de produto do Cloud Manager](/help/journey-onboarding/sysadmin/assign-team-members-cloud-manager.md) documento dessa jornada para obter mais informações.

Agora que seu programa foi criado com sucesso e seu repositório Git do Cloud Manager está disponível para que seus desenvolvedores acessem!

## Criar os ambientes do Cloud {#create-cloud-environments}

Depois de criar o programa de nuvem com sucesso, crie os ambientes de nuvem.

1. Navegue até a página de aterrissagem do Cloud Manager em [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selecione **Adicionar** no cartão de ambiente.

   ![Botão Adicionar ambiente](/help/journey-onboarding/assets/setup-resources9.png)

1. O assistente para adicionar ambiente inicia e orienta você durante a adição do ambiente. Adicione seu ambiente de desenvolvimento primeiro para se familiarizar com o assistente.

   >[!TIP]
   >
   >Consulte o documento [Adicionar um ambiente](/help/implementing/cloud-manager/manage-environments.md#adding-environments) para saber mais ou assistir [este tutorial em vídeo rápido](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) para saber mais sobre os ambientes do Cloud Manager e como adicioná-los ao seu programa.

1. Membros atribuídos ao **Desenvolvedor** o perfil de produto pode fazer logon no Cloud Manager e gerenciar repositórios git do Cloud Manager.

Agora que seu programa foi criado com sucesso e seu git do Cloud Manager está disponível para que seus desenvolvedores acessem!

## O que vem a seguir {#whats-next}

Agora que os recursos da nuvem foram criados e estão prontos para serem acessados pela sua equipe, o Administrador do sistema deve atribuir os membros da sua equipe a AEM perfis de produto as a Cloud Service da Adobe Admin Console para acessar esses recursos.

Você deve continuar sua jornada de integração ao revisar o documento [Atribuindo membros da equipe a AEM perfis de produto as a Cloud Service](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md) onde você aprenderá a conceder aos membros da equipe os direitos necessários para acessar seus novos ambientes.

## Recursos adicionais {#additional-resources}

Siga os recursos adicionais para saber mais sobre:

* [Tipos de programas e adição de um programa](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [Tipos de ambiente e adição de um ambiente](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [Gerenciamento do Git do Cloud Manager](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [Configuração do acesso a AEM as a Cloud Service do Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
