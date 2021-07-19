---
title: 'Atribuindo membros da equipe a perfis de produto do Cloud Manager '
description: Siga esta página para saber como atribuir membros da equipe a perfis de produto do Cloud Manager.
hide: true
hidefromtoc: true
index: false
source-git-commit: ede12ce0b62056f6e11ebd3d40d2c995f8d70d52
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 0%

---


# Atribuindo membros da equipe a perfis de produto do Cloud Manager {#assign-team-members}

Depois de saber como fazer logon no Admin Console e visualizar seus privilégios como Administrador do sistema, você estará pronto para atribuir membros da equipe aos perfis de produto do Cloud Manager.

## Objetivo {#objective}

Este documento resume como atribuir membros da equipe aos perfis de produto do Cloud Manager a partir do Admin Console.

Após ler esta seção, você deve ser capaz de:

* Entenda por que e como você deve adicionar membros da equipe.
* Saiba mais sobre três perfis de produto diferentes do Cloud Manager, como Proprietário comercial, Gerenciador de implantação e Desenvolvedor.
* Atribua membros da equipe aos perfis de produto do Cloud Manager (Proprietário comercial, Gerenciador de implantação e Desenvolvedor).

## Revisar perfis de produto do Cloud Manager {#review-product-profiles}

No Admin Console, é possível ver a lista de Perfis do Cloud Manager.

>[!NOTE]
>Antes de revisar os perfis de produto do Cloud Manager no Admin Console, é recomendável revisar os Perfis de produto do Cloud Manager disponíveis.

Siga as etapas abaixo para exibir a lista de Perfis do Cloud Manager:

1. Faça logon no Adobe Admin Console. Na página **Visão geral** , selecione Adobe Experience Manager as a Cloud Service no cartão Produtos e Serviços .

   >[!NOTE]
   >Consulte Fazer logon no Admin Console para saber como usar o Admin Console.


1. Navegue até a instância do cloud manager na tabela com a lista de todas as instâncias. Você verá a lista de perfis de produto pré-configurados do Cloud Manager.


## Atribuir usuários ao perfil de produto do proprietário comercial {#assign-users-business-owner}

Agora você está pronto para adicionar usuários e atribuí-los ao perfil de produto Proprietário comercial do Cloud Manager.

Para fazer isso com sucesso, no Admin Console do Adobe, é necessário adicionar um usuário ao produto (AEM como Cloud Service neste caso) e ao perfil de produto Proprietário comercial do Cloud Manager.

As etapas a seguir guiarão você por isso:

1. Identifique os usuários que gerenciarão os programas do Cloud Manager e adicione-os ao perfil de produto Proprietário comercial. O administrador do sistema deve ser a primeira pessoa a acessar e fazer logon no Cloud Manager. Você deve adicionar a si mesmo (administrador do sistema) ao perfil de produto Proprietário comercial primeiro.

1. Na página Visão geral do Admin Console , selecione Adobe Experience Manager como Cloud Service de produtos e cartão de serviços, conforme mostrado abaixo:

1. Selecione a guia Usuários na navegação superior e selecione Adicionar usuário.

1. Na caixa de diálogo adicionar usuário, digite a ID de email do usuário que deseja adicionar. Para o Tipo de ID, selecione Adobe ID se o Federated ID para os membros da equipe ainda não tiver sido configurado.

1. Na seleção Produto , selecione &quot;Adobe Experience Manager como Cloud Service&quot; e atribua o perfil de produto &quot;Proprietário comercial&quot; ao usuário, conforme mostrado abaixo. Consulte os perfis de produto do Cloud Manager para garantir que as funções certas sejam atribuídas aos usuários certos no Admin Console, como mostrado abaixo.

1. Atribua o usuário a pelo menos um perfil de produto para que ele possa acessar o Cloud Manager. Lembre-se de atribuir a si mesmo (administrador do sistema) ao &quot;Proprietário comercial&quot;.

1. Clique em Salvar. Um email de boas-vindas é enviado ao usuário adicionado. O usuário convidado pode acessar o Cloud Manager clicando no link do email de boas-vindas e fazendo logon usando a Adobe ID.

Parabéns! Agora, sua equipe recém-formada do Cloud Manager, incluindo o usuário atribuído à função &quot;Proprietário comercial&quot;, foi configurada. Os membros receberão um email de boas-vindas convidando-os para fazer logon e acessar o Cloud Manager. Na função de Proprietário comercial, agora você está a apenas um passo de fazer logon no Cloud Manager e ativar a criação dos recursos de nuvem.

## Atribuir usuários ao perfil de produto do Gerenciador de implantação {#assign-users-deployment-manager}

1. Identifique os usuários que gerenciarão os programas do Cloud Manager e adicione-os ao perfil de produto Proprietário comercial. O administrador do sistema deve ser a primeira pessoa a acessar e fazer logon no Cloud Manager. Você deve adicionar a si mesmo (administrador do sistema) ao perfil de produto Proprietário comercial primeiro.

1. Na página Visão geral do Admin Console , selecione Adobe Experience Manager como Cloud Service de produtos e cartão de serviços, conforme mostrado abaixo:

1. Selecione a guia Usuários na navegação superior e selecione Adicionar usuário.

1. Na caixa de diálogo adicionar usuário, digite a ID de email do usuário que deseja adicionar. Para o Tipo de ID, selecione Adobe ID se o Federated ID para os membros da equipe ainda não tiver sido configurado.

1. Na seleção Produto , selecione &quot;Adobe Experience Manager como Cloud Service&quot; e atribua o perfil de produto &quot;Deployment Manager&quot; ao usuário, como mostrado abaixo. Consulte os perfis de produto do Cloud Manager para garantir que as funções certas sejam atribuídas aos usuários certos no Admin Console, como mostrado abaixo.

   >[!NOTE]
   >O usuário pode ser adicionado ao perfil de produto do Gerenciador de implantação depois que os recursos do Cloud Manager forem criados.

## Atribuir usuários ao perfil de produto do desenvolvedor {#assign-users-developer}

1. Identifique os usuários que gerenciarão os programas do Cloud Manager e adicione-os ao perfil de produto Proprietário comercial. O administrador do sistema deve ser a primeira pessoa a acessar e fazer logon no Cloud Manager. Você deve adicionar a si mesmo (administrador do sistema) ao perfil de produto Proprietário comercial primeiro.

1. Na página Visão geral do Admin Console , selecione Adobe Experience Manager como Cloud Service de produtos e cartão de serviços, conforme mostrado abaixo:

1. Selecione a guia Usuários na navegação superior e selecione Adicionar usuário.

1. Na caixa de diálogo adicionar usuário, digite a ID de email do usuário que deseja adicionar. Para o Tipo de ID, selecione Adobe ID se o Federated ID para os membros da equipe ainda não tiver sido configurado.

1. Na seleção Produto , selecione &quot;Adobe Experience Manager como Cloud Service&quot; e atribua o perfil de produto &quot;Desenvolvedor&quot; ao usuário, conforme mostrado abaixo. Consulte os perfis de produto do Cloud Manager para garantir que as funções certas sejam atribuídas aos usuários certos no Admin Console, como mostrado abaixo.

   >[!NOTE]
   >O usuário pode ser adicionado ao perfil de produto Desenvolvedor após a criação dos recursos do Cloud Manager.

## O que vem a seguir {#whats-next}

Como Administrador do sistema atribuído à função *Proprietário comercial*, você deve acessar e fazer logon no Cloud Manager.
>[!NOTE]
>Consulte Navegar até o Cloud Manager para saber como fazer logon e acessar o Cloud Manager.

Um usuário do Cloud Manager na função de Proprietário comercial pode fazer logon e configurar os recursos da nuvem, incluindo seus Programas e Ambientes. Isso garantirá que sua equipe de especialistas possa começar a acessar o AEM como Cloud Service o mais rápido possível.
Depois que o proprietário da empresa configurar os recursos de nuvem, os desenvolvedores e os gerentes de implantação que foram adicionados com sucesso aos perfis de produto do Cloud Manager poderão acessar o Cloud Manager e se familiarizar com a forma como eles podem continuar no caminho de aprendizagem.

## Recursos adicionais {#additional-resources}

Siga os recursos adicionais para saber mais sobre:

* Cloud Manager
* Perfis de produto do Cloud Manager
* Visão geral da identidade do Admin Console
