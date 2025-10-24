---
title: Acessar o Admin Console
description: Depois de entender a preparação necessária para realizar a integração e as noções básicas da estrutura do AEM as a Cloud Service, você estará pronto para fazer logon na Admin Console pela primeira vez.
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 8ed13eb6f476bab07da07549a83ab9ac16bdea72
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 43%

---

# Acessar o Admin Console {#accessing-admin-console}

Nesta parte da [jornada de integração](overview.md), você aprenderá sobre a preparação necessária antes de fazer logon no sistema pela primeira vez.

## Objetivo {#objective}

Agora que você leu o artigo [Terminologia do AEM as a Cloud Service](terminology.md) e compreende a estrutura do AEMaaCS, você está pronto para fazer logon no Admin Console pela primeira vez!

Como administrador do sistema, você é responsável por gerenciar os usuários em sua organização usando o Admin Console. Depois de ler esta seção, você poderá fazer o seguinte:

* Compreender o que é uma Adobe ID.
* Ser capaz de fazer logon na Admin Console.
* Entenda como revisar seus privilégios como administrador do sistema por meio do Admin Console.
* Saber como entrar em contato com o suporte da Adobe para obter ajuda.

## Sobre a Admin Console {#admin-console}

O Adobe Admin Console é um local central para administrar e gerenciar licenças e usuários da Adobe. O Admin Console permite criar e gerenciar usuários em um único local, em vez de em várias soluções individuais.

### Adobe ID {#adobe-id}

Para entrar na Admin Console, você precisa de uma Adobe ID. Uma Adobe ID é uma conta vinculada a um endereço de email específico que é necessária para fazer logon e acessar a AEM as a Cloud Service ou qualquer solução da Adobe. Ao usar sua Adobe ID, você mantém todos os seus planos e produtos da Adobe associados a uma única conta.

Ao configurar uma equipe no Admin Console, admins devem especificar o endereço de email que será usado como a Adobe ID.

Há três tipos de Adobe IDs:

* **Personal ID**: o tipo padrão de Adobe ID e é criado em adobe.com. Administrado pela Adobe, qualquer pessoa pode criar uma conta desse tipo.

* **Enterprise ID**: as organizações geralmente querem ter maior controle sobre as contas dos usuários. Somente administradores do sistema podem criar Enterprise IDs e a organização é proprietária dessas contas junto à Adobe, que atua somente como host.

* **Federated ID**: com IDs federadas, a organização é proprietária e controla totalmente as contas. Sua organização deve integrar a Adobe Experience Cloud ao seu sistema de logon único (SSO) SAML2. Isso permite que os usuários se autentiquem em relação ao sistema SSO da organização em vez de uma conta hospedada pela Adobe.

Como administrador do sistema, você pode integrar a si mesmo e a sua equipe ao AEM as a Cloud Service com IDs pessoais. Execute esta tarefa antes que as Enterprise IDs ou Federated IDs estejam em vigor. Depois da configuração de Enterprise IDs ou Federated IDs, os membros poderão ser migrados para o uso dessas IDs.

### Fazer logon diretamente no Admin Console {#steps-admin-console}

Antes de usar o Admin Console para administrar os usuários da sua equipe, você precisa garantir que pode acessá-lo corretamente e tem as devidas permissões.

1. Como administrador do sistema, você recebe vários emails do Adobe como parte do processo de integração. Procure o email de boas-vindas que fornece informações sobre o nome da organização à qual você recebeu acesso.

1. Clique no link **Introdução** no email de boas-vindas para navegar até a Admin Console. Se não conseguir localizar o email, abra um navegador diretamente no Admin Console em [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

   ![Email de boas-vindas](/help/journey-onboarding/assets/get-started-email.png)

1. Faça logon usando sua Adobe ID. Depois de fazer logon, você verá a página **Visão geral** da Adobe Admin Console.

   ![O Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. Se você tiver acesso a várias organizações, verifique se fez logon na organização correta. Para alterar sua organização, clique no nome da organização no canto superior direito e escolha a organização que precisa acessar.

   ![Alterar organização](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. Selecione **Administradores** no cartão **Usuários** para verificar se você é um administrador do sistema.

   ![Revisar administradores](/help/journey-onboarding/assets/get-started2.png)

1. Depois de clicar em **Administradores** no cartão **Usuários**, você poderá pesquisar inserindo seu email (Adobe ID), nome de usuário, nome ou sobrenome.

   ![Pesquisar usuários](/help/journey-onboarding/assets/get-started3.png)

1. Se tudo funcionar corretamente, a pesquisa retornará seu registro. Se o valor na coluna **FUNÇÃO DE ADMINISTRADOR** mostrar **Sistema**, isso quer dizer que você (ou o usuário mostrado) é um administrador do sistema.

   ![Status do sistema](/help/journey-onboarding/assets/get-started4.png)

Parabéns, administrador do sistema!

## Acessar a Admin Console pelo Experience Hub  {#access-admin-console-via-experience-hub}

O [Experience Hub](/help/experience-hub.md) é a página inicial unificada e personalizada do AEM. Ele reúne as Ferramentas do AEM e a Admin Console em um só lugar.

![Opção do Admin Console como aparece na página inicial do Experience Hub](/help/journey-onboarding/assets/experiencehub-adminconsole1.png)

**Para acessar o Admin Console por meio do Experience Hub:**

1. Clique em [Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home) para abrir a home page do Experience Hub.

1. No agrupamento **Acesso rápido**, clique em [**Admin Console**](https://experience.adobe.com).

## Adobe Identity Management System {#ims}

O AEM as a Cloud Service vem pré-configurado com o Adobe Identity Management System (também conhecido como IMS) para autenticação. Você não precisa fazer nada como administrador do sistema para habilitar essa funcionalidade.

Ao usar o IMS, o AEM as a Cloud Service consolida a experiência de logon entre o AEM e o restante da Adobe Experience Cloud. Organizações com muitos produtos da Adobe são as que mais ganham. Crie grupos com base em funções no Admin Console e conceda acesso ao produto por meio do IMS, como o AEM as a Cloud Service.

Você aprenderá mais sobre perfis de produto e atribuirá usuários na próxima parte desta jornada de integração.

## Entre em contato com o Suporte da Adobe {#support}

Em caso de problemas, o suporte da Adobe pode ser acessado por meio do Admin Console. A guia **Suporte** permite acessar várias funções de suporte da Adobe por meio de uma interface simples e fácil de usar.

![Guia Suporte](/help/journey-onboarding/assets/support-menu.png)

A guia permite criar e gerenciar casos, conversar diretamente com os representantes do suporte ao cliente da Adobe e agendar sessões com especialistas. Os administradores do sistema e de suporte devem fazer logon para acessar os casos de suporte e as opções de sessão com especialistas.

## O que vem a seguir {#whats-next}

Agora que você leu este documento, deve:

* Compreender o que é uma Adobe ID.
* Ser capaz de fazer logon na Admin Console.
* Entenda como revisar seus privilégios como administrador do sistema usando o Admin Console.
* Saber como entrar em contato com o suporte da Adobe para obter ajuda.

Você está pronto para continuar sua jornada de integração, aprendendo como [atribuir membros da equipe aos Perfis de produto do Cloud Manager](assign-profiles-cloud-manager.md) para que seus colegas também possam acessar o AEMaaCS.

## Recursos adicionais {#additional-resources}

A seguir estão recursos adicionais e opcionais se quiser ir além do conteúdo da jornada de integração.

* [Visão geral do Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) - Uma visão geral abrangente do Admin Console
* [Criar ou atualizar seu Adobe ID](https://helpx.adobe.com/br/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - Saiba como criar um Adobe ID, alterá-lo e gerenciar vários Adobe IDs.
* [Manipulador de autenticação SAML 2.0](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/security/saml-2-0-authenticationhandler#) - O AEM vem com um manipulador de autenticação SAML. Esse manipulador oferece suporte ao Protocolo de solicitação de autenticação SAML 2.0 (perfil Web-SSO) usando a associação POST HTTP.
* [Funções administrativas](https://helpx.adobe.com/br/enterprise/using/admin-roles.html) - Usando o Adobe Admin Console, as organizações podem definir uma hierarquia administrativa flexível que permita o gerenciamento refinado do acesso e uso dos produtos da Adobe.
* [Suporte e sessões com especialistas](https://helpx.adobe.com/br/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.html) - Saiba como acessar as opções de suporte na Admin Console, gerenciar os casos de suporte, agendar uma sessão com um especialista e muito mais.
