---
title: Acesso ao Admin Console
description: Depois de entender a preparação necessária para realizar a integração e as noções básicas da estrutura do AEMaaCS, você estará pronto para fazer logon no Admin Console pela primeira vez.
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 97%

---

# Acesso ao Admin Console {#accessing-admin-console}

Nesta parte da [jornada de integração,](overview.md) você aprenderá sobre a preparação necessária antes de fazer logon no sistema pela primeira vez.

## Objetivo {#objective}

Agora que você leu o artigo [Terminologia do AEM as a Cloud Service](terminology.md) e compreende a estrutura do AEMaaCS, você está pronto para fazer logon no Admin Console pela primeira vez!

Como administrador do sistema, você é responsável por gerenciar os usuários da sua organização. Você faz isso usando o Admin Console. Depois de ler esta seção, você deverá:

* Compreender o que é uma Adobe ID.
* Ser capaz de fazer logon no Admin Console.
* Entenda como revisar seus privilégios como administrador do sistema por meio do Admin Console.
* Saber como entrar em contato com o suporte da Adobe para obter ajuda.

## O Admin Console {#admin-console}

O Adobe Admin Console é um local central para administrar e gerenciar licenças e usuários da Adobe. Ele permite criar e gerenciar usuários em um só local, em vez de em várias soluções separadas.

## Adobe ID {#adobe-id}

Para entrar no Admin Console, você precisará de uma Adobe ID. A Adobe ID é uma conta vinculada a um endereço de email específico que é necessária para fazer logon e acessar o AEM as a Cloud Service ou qualquer solução da Adobe. Ao usar a Adobe ID, você mantém todos os seus planos e produtos da Adobe associados a uma só conta.

Quando você, como administrador do sistema, configura sua equipe no Admin Console, especifica o endereço de email que é usado como Adobe ID.

Há três tipos de Adobe IDs:

* **Personal ID**: esse é o tipo padrão de Adobe ID e é criado em adobe.com. Essa conta é controlada pela Adobe e qualquer pessoa pode criar uma.

* **Enterprise ID**: as organizações geralmente querem ter maior controle sobre as contas dos usuários. Somente administradores do sistema podem criar Enterprise IDs e a organização é proprietária dessas contas junto à Adobe, que atua somente como host.

* **Federated ID**: com as Federated IDs, a organização é proprietária e controla totalmente as contas. Para fazer isso, sua organização precisa integrar a Adobe Experience Cloud ao seu sistema de logon único (SSO) SAML2. Isso permite que os usuários se autentiquem em relação ao sistema SSO da organização em vez de uma conta hospedada pela Adobe.

Como administrador do sistema, você pode decidir integrar a si mesmo e a sua equipe ao AEM as a Cloud Service usando Personal IDs antes da configuração de Enterprise IDs ou Federated IDs. Depois da configuração de Enterprise IDs ou Federated IDs, os membros poderão ser migrados para o uso dessas IDs.

## Logon no Admin Console {#steps-admin-console}

Antes de usar o Admin Console para administrar os usuários da sua equipe, você precisa garantir que pode acessá-lo corretamente e tem as devidas permissões.

1. Como administrador do sistema, você receberá vários emails da Adobe como parte do processo de integração. Procure o email de boas-vindas que fornece informações sobre o nome da organização à qual você recebeu acesso.

1. Clique no link **Introdução** no email de boas-vindas para acessar o Admin Console. Se não conseguir encontrar o email, abra um navegador diretamente no Admin Console em [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

   ![Email de boas-vindas](/help/journey-onboarding/assets/get-started-email.png)

1. Faça logon usando sua Adobe ID. Depois de fazer logon, você verá a página **Visão geral** do Adobe Admin Console.

   ![O Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. Se você tiver acesso a várias organizações, verifique se fez logon na organização correta. Para alterar a organização, clique no nome dela no canto superior direito e escolha a organização correta que você precisa acessar.

   ![Alterar organização](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. Selecione **Administradores** no cartão **Usuários** para verificar se você é um administrador do sistema.

   ![Revisar administradores](/help/journey-onboarding/assets/get-started2.png)

1. Depois de clicar em **Administradores** no cartão **Usuários**, você poderá pesquisar inserindo seu email (Adobe ID), nome de usuário, nome ou sobrenome.

   ![Pesquisar usuários](/help/journey-onboarding/assets/get-started3.png)

1. Se tudo estiver funcionando corretamente, a pesquisa retornará seu registro. Se o valor na coluna **FUNÇÃO DE ADMINISTRADOR** mostrar **Sistema**, isso quer dizer que você (ou o usuário mostrado) é um administrador do sistema.

   ![Status do sistema](/help/journey-onboarding/assets/get-started4.png)

Parabéns, administrador do sistema!

## Adobe Identity Management System {#ims}

O AEM as a Cloud Service vem pré-configurado com o Adobe Identity Management System (também conhecido como IMS) para autenticação. Você não precisa fazer nada como administrador do sistema para habilitar esse recurso.

Ao usar o IMS, o AEM as a Cloud Service consolida a experiência de logon entre o AEM e o restante da Adobe Experience Cloud. Organizações com vários produtos da Adobe se beneficiam ainda mais ao criar grupos com base em funções no Admin Console e atribuir acesso a vários produtos, incluindo o AEM as a Cloud Service por meio de IMS.

Você saberá mais sobre perfis de produto e atribuirá usuários na próxima parte desta jornada de integração.

## Contato com o suporte da Adobe {#support}

Em caso de problemas, o suporte da Adobe pode ser acessado por meio do Admin Console. A guia **Suporte** permite acessar várias funções de suporte da Adobe por meio de uma interface simples e fácil de usar.

![Guia Suporte](/help/journey-onboarding/assets/support-menu.png)

A guia permite criar e gerenciar casos, conversar diretamente com os representantes do suporte ao cliente da Adobe e agendar sessões com especialistas. Os administradores do sistema e de suporte devem fazer logon para acessar os casos de suporte e as opções de sessão com especialistas.

## O que vem a seguir {#whats-next}

Agora que você leu este documento, deve:

* Compreender o que é uma Adobe ID.
* Ser capaz de fazer logon no Admin Console.
* Entenda como revisar seus privilégios como administrador do sistema por meio do Admin Console.
* Saber como entrar em contato com o suporte da Adobe para obter ajuda.

Você está pronto para continuar sua jornada de integração, aprendendo como [atribuir membros da equipe aos Perfis de produto do Cloud Manager](assign-profiles-cloud-manager.md) para que você também possa acessar o AEMaaCS.

## Recursos adicionais {#additional-resources}

A seguir estão recursos adicionais e opcionais se quiser ir além do conteúdo da jornada de integração.

* [Visão geral do Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) - Uma visão geral abrangente do Admin Console
* [Criar ou atualizar seu Adobe ID](https://helpx.adobe.com/br/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - Saiba como criar um Adobe ID, alterá-lo e gerenciar vários Adobe IDs.
* [Manipulador de autenticação SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html?lang=pt-BR) - O AEM vem com um manipulador de autenticação SAML. Esse manipulador oferece suporte ao Protocolo de solicitação de autenticação SAML 2.0 (perfil Web-SSO) usando a associação POST HTTP.
* [Funções administrativas](https://helpx.adobe.com/br/enterprise/using/admin-roles.ug.html) - Usando o Adobe Admin Console, as organizações podem definir uma hierarquia administrativa flexível que permita o gerenciamento refinado do acesso e uso dos produtos da Adobe.
* [Suporte e sessões com especialistas](https://helpx.adobe.com/br/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) - Saiba como acessar as opções de suporte no Admin Console, gerenciar os casos de suporte, agendar uma sessão com um especialista e muito mais.
