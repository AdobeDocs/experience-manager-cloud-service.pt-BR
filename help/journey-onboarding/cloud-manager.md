---
title: Acessar o Cloud Manager
description: Saiba como acessar o Cloud Manager para poder configurar os recursos do projeto.
role: Admin, User, Developer
exl-id: c9476ac9-8318-493e-a48d-94ff5a6433a7
feature: Onboarding
source-git-commit: 0db48ef4c15b6ca530b2626f7078c7172c872fff
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 57%

---

# Acessar o Cloud Manager {#cloud-resources}

Nesta parte da [jornada de integração](overview.md), você aprenderá a acessar o Cloud Manager para poder configurar os recursos do projeto.

## Objetivo {#objective}

No artigo anterior desta jornada de integração, [Atribuição dos membros da equipe aos perfis de produto do Cloud Manager](assign-profiles-cloud-manager.md), você concedeu as funções apropriadas à sua equipe do AEMaaCS. Agora saiba como acessar o Cloud Manager para poder configurar os recursos do projeto que a equipe pretende usar.

Como você concluiu a etapa anterior desta jornada, sua equipe pode acessar o Cloud Manager. O Cloud Manager é usado para criar e gerenciar os recursos do projeto, como programas e ambientes.

Depois de ler este documento, é preciso entender o seguinte:

* Que um administrador do sistema atribuído à função **Proprietário da empresa** deve ser o primeiro em sua organização a fazer logon e acessar o Cloud Manager.
* Como fazer logon no Cloud Manager.

## Cloud Manager {#cloud-manager}

O Cloud Manager é um componente essencial do AEM as a Cloud Service e serve como ponto de entrada único para a equipe. Ele apoia os clientes com configurações de desenvolvimento corporativo e pipelines de CI/CD criados com propósitos específicos, que estão equipados de forma a garantir testes completos e código da mais alta qualidade para fornecer experiências excepcionais. O Cloud Manager fornece tudo o que é necessário para começar a usar o autoatendimento, incluindo a capacidade de criar recursos e ambientes de nuvem.

Normalmente, um membro da equipe com o perfil de produto **Proprietário da empresa** é responsável por adicionar os recursos de nuvem, como programas e ambientes. Essa pessoa entende as necessidades comerciais e conclui a configuração inicial do Cloud Manager.

Para os fins desta jornada de integração, você, como administrador do sistema, já atribuiu a si mesmo o perfil de produto **Proprietário da empresa** e pode configurar os recursos da nuvem. Dependendo dos requisitos reais do projeto, os proprietários da empresa podem ou não ser os mesmos indivíduos que os administradores do sistema.

## Acessar o Cloud Manager como um Administrador do sistema e Proprietário da empresa {#access-sysadmin-bo}

Para que os membros da equipe com função de **Proprietário da empresa** possam acessar o Cloud Manager e começar a criar recursos de nuvem, o administrador do sistema deve receber a função de **Proprietário da empresa**. Eles também devem fazer logon no Cloud Manager como você fez na etapa anterior desta jornada de integração.

1. Certifique-se de que você, como administrador do sistema, receba a função **Proprietário da empresa**.

   Retorne à etapa anterior, [Atribuir Membros da Equipe a Perfis de Produto do Cloud Manager](assign-profiles-cloud-manager.md), para obter detalhes sobre como atribuir a função de **Proprietário da Empresa** ao administrador do sistema.

1. Entre no Cloud Manager em [experience.adobe.com](https://experience.adobe.com).
1. No agrupamento Acesso rápido, clique em **Experience Manager**.
1. No painel lateral esquerdo, clique em **Cloud Manager**.

   ![Cloud Manager no console](/help/journey-onboarding/assets/consol-cloud-manager.png)

Ao entrar como administrador do sistema com a função **Proprietário da empresa**, você usa o Cloud Manager para ser usado pelos outros usuários com a função **Proprietário da empresa**. Você não recebe uma confirmação ou qualquer mensagem. Apenas fazer logon é suficiente.

Até você entrar no Cloud Manager como administrador do sistema com a função **Proprietário da empresa**, outros usuários com a função **Proprietário da empresa** não poderão criar programas no Cloud Manager. Essa regra é verdadeira mesmo se eles forem atribuídos às funções corretas.

## Acessar o Cloud Manager {#navigate-cloud-manager}

Usuários com a função **Proprietário da empresa** receberão um email de boas-vindas com um link para começar. Siga as etapas abaixo para acessar o Cloud Manager usando esse email de boas-vindas.

1. No email de boas-vindas, clique em **Começar**, conforme mostrado na figura abaixo.
   ![Exemplo de email](/help/journey-onboarding/assets/get-started-email.png)

1. Navegue até a página **Programas e produtos** do Cloud Manager.

   >[!TIP]
   >
   >Você também pode navegar diretamente para a página de logon do Cloud Manager em `[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)`. Marque esta página para referência futura.

1. Você será direcionado para a página de destino do Cloud Manager.

<!-- OLD
Alternatively, you can navigate to Cloud Manager's **Programs and Products** page from the Adobe Experience Cloud home page using these steps.

1. Navigate directly to [Adobe Experience Cloud](https://experience.adobe.com) and login using your Adobe ID.

1. From the Adobe Experience Cloud home page, select **Experience Manager** to open the AEM home page.

   ![Experience Cloud homepage](/help/journey-onboarding/assets/setup-resources2.png)

1. On the **Cloud Manager** tile, select **Launch**.

   ![AEM home page](/help/journey-onboarding/assets/setup-resources3.png)

1. After successfully logging on, you are directed to the Cloud Manager landing page. See [Viewing Cloud Manager's Programs](#viewing-programs) for more details.

How you access your programs and products via Cloud Manager is up to you and has no effect on how you use Cloud Manager or how you manage your programs.

>[!NOTE]
>
>Depending on the roles assigned in Cloud Manager and the state of the application, you see different screens while using the Cloud Manager user interface. -->

## Exibir programas {#viewing-programs}

Ao acessar o Cloud Manager, o conteúdo exibido dependerá do estado dos seus programas, conforme detalhado nas seções a seguir.

### Quando não existem programas {#no-programs}

Se não existirem programas em sua organização, a página de aterrissagem o direcionará para criar seu primeiro programa.

![Nenhum programa](/help/journey-onboarding/assets/cloud-manager-programs-do-not-exist.png)

### Quando os programas já existem {#programs-exist}

Se programas já existirem em sua organização, a página de destino exibirá os programas existentes e também oferecerá um botão para adicionar mais programas.

![Existem programas](/help/journey-onboarding/assets/cloud-manager-programs-exist.png)

### Quando existe um programa e você é um Administrador do sistema {#programs-exist-sysadmin}

Se houver programas em sua organização e você for um administrador do sistema, a página de aterrissagem exibirá o botão **Gerenciar Acesso** junto com a opção **Adicionar Programa**.

![Exibição do administrador do sistema](/help/journey-onboarding/assets/cloud-manager-programs-as-sysadmin.png)

## Verificar suas funções de usuário {#verify-user-roles}

Depois de fazer logon no Cloud Manager, você poderá verificar se recebeu o perfil de produto **Proprietário da empresa**.

1. Ao lado do canto superior direito da página, clique no ícone **Conta**.

1. Clique em **Funções de usuário**.

   ![Funções do usuário](/help/journey-onboarding/assets/cloud-manager-user-roles.png)

1. Na caixa de diálogo **Funções do Usuário**, confirme se o usuário tem a função **Proprietário da Empresa**.

   ![Lista de funções de usuário](/help/journey-onboarding/assets/cloud-manager-user-roles-business-owner.png)

Você fez logon no Cloud Manager como Proprietário da empresa. Se você não recebeu a função **Proprietário da empresa**, entre em contato com o administrador do sistema.

## O que vem a seguir {#whats-next}

Agora que você pode acessar o Cloud Manager como administrador do sistema, você está pronto para criar seu primeiro programa.

Continue a jornada de integração revisando o documento [Criar um programa](create-program.md), no qual você aprenderá a fazer isso.

## Recursos adicionais {#additional-resources}

A seguir estão recursos adicionais e opcionais se quiser ir além do conteúdo da jornada de integração.

* [Introdução ao Cloud Manager](/help/onboarding/cloud-manager-introduction.md) -
Saiba mais sobre o Cloud Manager e seus programas e ambientes.
* [Perfis de produto e de equipe do AEM as a Cloud Service](/help/onboarding/aem-cs-team-product-profiles.md) - Saiba como os perfis de produto e de equipe do AEM as a Cloud Service podem conceder e limitar o acesso às soluções licenciadas da Adobe.
<!-- ERROR: Not Found (HTTP error 404) * [AEM Champion Tips and Tricks - Cloud Manager UI](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/cloud-manager-ui.md) - Watch this video for an overview of Cloud Manager's UI from an AEM champion. -->
