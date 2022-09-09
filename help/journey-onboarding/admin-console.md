---
title: Acesso ao Admin Console
description: Assim que entender a preparação necessária para integração e as noções básicas da estrutura do AEMaaCS, você estará pronto para fazer logon no Admin Console pela primeira vez.
exl-id: 0ccce328-a356-4ba9-b7fe-f67abc25b924
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 2%

---

# Acesso ao Admin Console {#accessing-admin-console}

Nesta parte do [jornada de integração,](overview.md) você aprenderá sobre a preparação necessária antes de fazer logon no sistema pela primeira vez.

## Objetivo {#objective}

Agora que leu o artigo [AEM Terminologia as a Cloud Service](terminology.md) e entenda as noções básicas da estrutura do AEMaaCS, você está pronto para fazer logon no Admin Console pela primeira vez!

Como administrador do sistema, você é responsável por gerenciar usuários em sua organização. Você faz isso usando o Admin Console. Após ler esta seção, você deve:

* Entenda o que é uma Adobe ID.
* Faça logon no Admin Console.
* Entenda como revisar seus privilégios como administrador de sistema via Admin Console.
* Saiba como entrar em contato com o suporte do Adobe para obter ajuda.

## O Admin Console {#admin-console}

O Adobe Admin Console é um local central para administrar e gerenciar licenças e usuários de Adobe. O Admin Console permite criar e gerenciar usuários em um único local, em vez de em suas várias soluções individuais.

## Adobe ID {#adobe-id}

Para entrar no Admin Console, você precisará de uma Adobe ID. E o Adobe ID é uma conta vinculada a um endereço de email específico que é necessário para fazer logon e acessar AEM as a Cloud Service ou qualquer solução do Adobe. Ao usar a Adobe ID, você mantém todos os seus planos e produtos de Adobe associados a uma única conta.

Quando você, como administrador do sistema, configurar sua equipe no Admin Console, especifique o endereço de email que será usado como Adobe ID.

Há três tipos de IDs de Adobe:

* **ID pessoal**: Esse é o tipo padrão de Adobe ID e é criado em adobe.com. Esta conta é gerida pelo Adobe e qualquer pessoa pode criar uma conta deste tipo.

* **Enterprise ID**: As organizações geralmente querem aumentar o controle das contas de usuários. Somente administradores de sistema podem criar Enterprise IDs e a organização é proprietária dessas contas com o Adobe servindo somente como host.

* **Federated ID**: Com as Federated IDs, a organização é proprietária e controla totalmente as contas. Para fazer isso, sua organização precisa integrar a Adobe Experience Cloud ao seu sistema de logon único (SSO) SAML2. Isso permite que os usuários se autentiquem em relação ao sistema SSO de sua organização em vez de uma conta hospedada pelo Adobe.

Como administrador do sistema, você pode decidir integrar-se a si mesmo e à sua equipe em AEM as a Cloud Service usando IDs pessoais antes da configuração das Enterprise IDs ou Federated IDs. Depois que as Enterprise IDs ou Federated IDs forem configuradas, os membros poderão ser migrados para o uso dessas IDs.

## Logon no Admin Console {#steps-admin-console}

Antes de usar o Admin Console para administrar usuários em sua equipe, você precisa garantir que possa acessá-lo corretamente e ter as permissões apropriadas.

1. Como administrador do sistema, você receberá vários emails do Adobe como parte do processo de integração. Procure o email de boas-vindas que fornece as informações sobre o nome da organização ao qual você recebeu acesso.

1. Clique no botão **Introdução** link no email de boas-vindas para navegar até o Admin Console. Se não conseguir encontrar o email, abra um navegador diretamente no Admin Console em [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com).

   ![Email de boas-vindas](/help/journey-onboarding/assets/get-started-email.png)

1. Faça logon usando sua Adobe ID. Após o logon bem-sucedido, você verá a variável **Visão geral** da Adobe Admin Console.

   ![O Admin Console](/help/journey-onboarding/assets/get-started1.png)

1. Se você tiver acesso a várias organizações, verifique se fez logon na organização correta. Para alterar sua organização, clique no nome da organização no canto superior direito e escolha a organização necessária à qual você precisa acessar.

   ![Alterar organização](/help/journey-onboarding/assets/admin-console-orgswitch.png)

1. Selecionar **Administradores** do **Usuários** para verificar se você é um administrador do sistema.

   ![Administradores de revisão](/help/journey-onboarding/assets/get-started2.png)

1. Depois de clicar em **Administradores** do **Usuários** , você pode pesquisar inserindo seu email do Adobe ID, nome de usuário, nome ou sobrenome.

   ![Pesquisar usuários](/help/journey-onboarding/assets/get-started3.png)

1. Se tudo estiver funcionando corretamente, a pesquisa retornará seu registro. Se o valor na variável **FUNÇÃO DE ADMINISTRADOR** a coluna mostra **Sistema**, você sabe que você (ou o usuário exibido) é um administrador do sistema.

   ![Status do sistema](/help/journey-onboarding/assets/get-started4.png)

Parabéns, administrador do sistema!

## Identity Management System da Adobe {#ims}

AEM as a Cloud Service vem pré-configurado com o Adobe Identity Management System (também conhecido como IMS) para autenticação. Você não precisa fazer nada como administrador do sistema para habilitar isso.

Ao usar o IMS, AEM o as a Cloud Service consolida a experiência de logon entre o AEM e o restante da Adobe Experience Cloud. Organizações com vários produtos do Adobe se beneficiam especialmente ao criar grupos com base em funções no Admin Console e atribuir acesso a vários produtos, incluindo AEM as a Cloud Service via IMS.

Você aprenderá mais sobre perfis de produtos e atribuirá usuários na próxima parte desta jornada de integração.

## Entrar em contato com o suporte ao Adobe {#support}

Em caso de problemas, o suporte ao Adobe pode ser acessado através do Admin Console. O **Suporte** A guia permite acessar várias funções de suporte do Adobe por meio de uma interface simples e fácil de usar.

![Guia Suporte](/help/journey-onboarding/assets/support-menu.png)

A guia permite criar e gerenciar casos, conversar diretamente com representantes do suporte ao cliente do Adobe e agendar sessões com especialistas. Os administradores de sistema e administradores de suporte devem fazer logon para acessar os casos de suporte e as opções de sessão de especialistas.

## O que vem a seguir {#whats-next}

Agora que leu este documento, você deve:

* Entenda o que é e o Adobe ID.
* Faça logon no Admin Console.
* Entenda como revisar seus privilégios como administrador de sistema via Admin Console.
* Saiba como entrar em contato com o suporte do Adobe para obter ajuda.

Você está pronto para continuar sua jornada de integração, aprendendo como [atribuir membros da equipe aos Perfis de produto do Cloud Manager](assign-profiles-cloud-manager.md) para que você também possa acessar o AEMaaCS.

## Recursos adicionais {#additional-resources}

* [Visão geral do Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) - Uma visão geral abrangente do Admin Console
* [Criar ou atualizar seu Adobe ID](https://helpx.adobe.com/ca/manage-account/using/create-update-adobe-id.html#HowtocreateorupdateyourAdobeID) - Saiba como criar uma Adobe ID, alterá-la e gerenciar várias IDs de Adobe.
* [Manipulador de autenticação SAML 2.0](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/saml-2-0-authenticationhandler.html) - AEM navios com um manipulador de autenticação SAML. Este manipulador fornece suporte para o protocolo SAML 2.0 Authentication Request Protocol (perfil Web-SSO) usando a vinculação HTTP POST.
* [Funções administrativas](https://helpx.adobe.com/enterprise/using/admin-roles.ug.html) - Usando a Adobe Admin Console, as organizações podem definir uma hierarquia administrativa flexível que permita o gerenciamento refinado do acesso e uso do produto Adobe.
* [Sessões de suporte e especialistas](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) - Saiba como acessar as opções de suporte no Admin Console, gerenciar os casos de suporte, agendar uma sessão de especialistas e muito mais.
