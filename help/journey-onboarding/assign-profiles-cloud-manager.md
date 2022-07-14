---
title: Atribuindo membros da equipe a perfis de produto do Cloud Manager
description: Siga esta página para saber como atribuir membros da equipe a perfis de produtos do Cloud Manager
feature: Onboarding
role: Admin, User, Developer
exl-id: 555688e5-f937-462c-9fcc-b90685f1882b
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 2%

---


# Atribuir membros da equipe aos perfis de produto do Cloud Manager {#assign-team-members}

Nesta parte do [jornada de integração,](overview.md) você aprenderá a atribuir membros da equipe aos perfis de produto do Cloud Manager.

## Objetivo {#objective}

Na etapa anterior desta jornada, [Acessar o Admin Console,](admin-console.md) agora você aprendeu a fazer logon no Admin Console e a verificar seus privilégios como administrador do sistema. Agora você está pronto para permitir que os membros da equipe acessem o Cloud Manager. Para fazer isso, atribua perfis de produto.

Ao conceder aos usuários acesso a uma solução Adobe, você não quer necessariamente conceder a eles acesso total. Os perfis de produto permitem que cada solução tenha seu próprio conjunto de permissões do usuário. Use o Admin Console para atribuir perfis de produto.

Seu primeiro passo é conceder aos usuários acesso ao Cloud Manager. O Cloud Manager oferece suporte a você com configurações de desenvolvimento corporativo e seus pipelines de CI/CD criados especificamente, que são equipados para garantir testes completos e a mais alta qualidade do código para fornecer experiências excepcionais.

Após ler este documento, você deve:

* Entenda quais perfis de produto são.
* Entenda o que é o Cloud Manager.
* Conheça os três perfis de produto importantes do Cloud Manager: **Proprietário da empresa**, **Gerenciador de implantação** e **Desenvolvedor**.
* Atribua membros da equipe a perfis de produto do Cloud Manager.

## Pré-requisitos {#prerequisites}

Para atribuir membros da equipe a perfis de produtos, você precisará ter detalhes sobre os membros da equipe, que precisarão acessar AEM as a Cloud Service, incluindo:

* Nomes
* Endereços de email
* Funções e responsabilidades

>[!TIP]
>
>Para fins de integração, o Adobe recomenda que você adicione inicialmente usuários que participarão das tarefas imediatas, como administradores, desenvolvedores e autores de conteúdo.
>
>Você pode continuar o processo de integração sem adicionar todos os usuários. Após concluir a integração, você pode adicionar outros usuários.

## Perfis de produto {#product-profiles}

Ao conceder aos usuários acesso a uma solução Adobe, você não quer necessariamente conceder a eles acesso total. Os perfis de produto permitem que cada solução tenha seu próprio conjunto de permissões de usuário definidas usando o Admin Console.

Por exemplo, posteriormente nesta jornada, você usará o Admin Console para conceder aos usuários acesso à solução de AEM, atribuindo perfis de produto a administradores de AEM e autores de AEM.

No entanto, a próxima etapa é conceder perfis de produtos para que os membros da sua equipe tenham acesso ao Cloud Manager.

## Cloud Manager {#cloud-manager}

Como administrador do sistema, você sabe que um projeto bem-sucedido AEM as a Cloud Service depende não apenas da criação de conteúdo surpreendente usando AEM, mas também do desenvolvimento e implantação de seu próprio código personalizado e aplicativos para fornecer seu conteúdo AEM.

O Cloud Manager é parte integral AEM as a Cloud Service e é usado para gerenciar seus pipelines de CI/CD para a implantação de código, gerenciar seus repositórios de código e gerenciar seus ambientes.

Antes que a equipe possa fazer qualquer outra coisa, ela deve ser integrada ao Cloud Manager, concedendo-lhe os perfis de produto necessários. As próximas etapas mostram onde encontrar o perfil de produto do Cloud Manager usando o Admin Console e como atribuí-lo aos membros da equipe.

## Revisar perfis de produto do Cloud Manager {#review-product-profiles}

Usando o Admin Console, você pode ver a lista de perfis do Cloud Manager.

1. Faça logon no Adobe Admin Console em [adminconsole.adobe.com](https://adminconsole.adobe.com/) e da **Visão geral** página, selecione **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

   ![AEM como produto](/help/journey-onboarding/assets/assign-team1.png)

1. Navegue até o **Cloud Manager** da lista de todas as instâncias.

   ![Cloud Manager](/help/journey-onboarding/assets/assign-team2.png)

1. Você verá a lista de perfis de produto pré-configurados do Cloud Manager.

   ![Perfis de produto](/help/journey-onboarding/assets/assign-team3.png)

Os perfis mais importantes a serem atribuídos como parte do processo inicial de integração são:

* **Proprietário da empresa** - Esses usuários gerenciam programas diferentes.
* **Gerenciador de implantação** - Esses usuários implantam o código de seus repositórios para executar AEM ambientes.
* **Desenvolvedor** - Esses usuários desenvolvem seus aplicativos de AEM personalizados e cometem código aos repositórios.

Sabendo quais são essas funções e o que elas fazem, revise sua lista de membros da equipe para determinar quem precisa de qual perfil. Lembre-se de que os usuários podem ter e geralmente têm várias funções em sua equipe e, portanto, também precisam de vários perfis.

## Atribuir o perfil de produto do proprietário comercial {#assign-business-owner}

Agora você está pronto para adicionar usuários e atribuí-los à variável **Proprietário da empresa** perfil do produto.

1. Identifique os usuários que precisam gerenciar os programas do Cloud Manager. Esses serão seus **Proprietários de negócios**.

1. Faça logon no Admin Console em `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` e no **Visão geral** página, selecione **Adobe Experience Manager as a Cloud Service** produto de **Produtos e serviços** cartão.

   ![Produtos e serviços](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione o **Usuários** na navegação superior, em seguida, selecione **Adicionar usuário**.

   ![Adicionar usuário](/help/journey-onboarding/assets/assign-team4.png)

1. No **Adicionar usuários à equipe** , insira a ID de email do usuário que deseja adicionar.

   * Se a ID federada dos membros da equipe ainda não tiver sido configurada, selecione **Adobe ID** para **Tipo de ID**.

   ![Adicionar detalhes do usuário](/help/journey-onboarding/assets/assign-team5.png)

1. Clique no botão de mais sob a **Selecionar produtos ou grupos de usuários** para iniciar a seleção do produto e selecione **Adobe Experience Manager as a Cloud Service** e atribuir **Proprietário da empresa** perfil de produto para o usuário.

   * Atribua cada usuário a pelo menos um perfil de produto para que ele possa acessar o Cloud Manager.
   * Lembre-se de atribuir a si mesmo como administrador do sistema ao **Proprietário da empresa** função.

   ![Atribuição de usuários](/help/journey-onboarding/assets/assign-team6.png)

1. Clique em **Salvar** e um email de boas-vindas é enviado ao usuário adicionado. O usuário convidado pode acessar o Cloud Manager clicando no link do email de boas-vindas e fazendo logon usando a Adobe ID.

1. Repita essas etapas para os usuários em sua equipe.

Seu **Proprietário da empresa** Eles foram atribuídos e agora podem acessar o Cloud Manager. Não se esqueça de também se atribuir como administrador de sistema ao **Proprietário da empresa** perfil.

## Atribuir o Perfil de Produto do Gerenciador de Implantação {#assign-deployment-manager}

1. Identifique os usuários que precisam implantar o código.

1. Faça logon no Admin Console em `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` e no **Visão geral** seleção de página **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

   ![Produtos e serviços](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione o **Usuários** no início da navegação e selecione **Adicionar usuário**.

   ![Adicionar usuário](/help/journey-onboarding/assets/assign-team4.png)

1. No **Adicionar usuários à equipe** , insira a ID de email do usuário que deseja adicionar.

   * Se a ID federada dos membros da equipe ainda não tiver sido configurada, selecione **Adobe ID** para **Tipo de ID**.

   ![Inserir ID](/help/journey-onboarding/assets/assign-team5.png)

1. Clique no botão de mais sob a **Selecionar produtos ou grupos de usuários** para iniciar a seleção do produto e selecione **Adobe Experience Manager as a Cloud Service** e atribuir **Gerenciador de implantação** perfil de produto para o usuário.

   ![Atribuir perfil](/help/journey-onboarding/assets/assign-team6.png)

Seu **Gerenciador de implantação** Eles foram atribuídos e agora podem acessar o Cloud Manager. Dependendo de suas responsabilidades futuras, você pode ou não precisar se atribuir como administrador do sistema ao **Gerenciador de implantação** perfil.

## Atribua o perfil de produto do desenvolvedor {#assign-developer}

1. Identifique os usuários que precisam desenvolver aplicativos AEM e gerenciar código.

1. Faça logon no Admin Console em `[adminconsole.adobe.com](https://adminconsole.adobe.com/enterprise/overview)` e no **Visão geral** seleção de página **Adobe Experience Manager as a Cloud Service** do **Produtos e serviços** cartão.

   ![Produtos e serviços](/help/journey-onboarding/assets/assign-team1.png)

1. Selecione o **Usuários** no início da navegação e selecione **Adicionar usuário**.

   ![Adicionar usuário](/help/journey-onboarding/assets/assign-team4.png)

1. Em **Adicionar usuários à equipe** , insira a ID de email do usuário que deseja adicionar.

   * Se a ID federada dos membros da equipe ainda não tiver sido configurada, selecione **Adobe ID** para **Tipo de ID**.

   ![Adicionar ID de usuário](/help/journey-onboarding/assets/assign-team5.png)

1. Clique no botão de mais sob a **Selecionar produtos ou grupos de usuários** para iniciar a seleção do produto e selecione **Adobe Experience Manager as a Cloud Service** e atribuir **Desenvolvedor** perfil de produto para o usuário.

   ![Atribuir perfil](/help/journey-onboarding/assets/assign-team6.png).

Seu **Desenvolvedor** Eles foram atribuídos e agora podem acessar o Cloud Manager. Dependendo de suas responsabilidades futuras, você pode ou não precisar se atribuir como administrador do sistema ao **Desenvolvedor** perfil.

## O que vem a seguir {#whats-next}

Parabéns. Sua equipe recém-formada do Cloud Manager (incluindo você atribuído ao **Proprietário da empresa** ) foi configurado. No papel de **Proprietário da empresa**, agora você está a apenas um passo de fazer logon no Cloud Manager e ativar a criação dos recursos da nuvem.

Nesta parte da jornada de integração você aprendeu a atribuir membros da equipe a perfis no Admin Console. Agora você deve:

* Entenda quais perfis de produto são.
* Entenda o que é o Cloud Manager.
* Conheça os três perfis de produto importantes do Cloud Manager: **Proprietário da empresa**, **Gerenciador de implantação** e **Desenvolvedor**.
* Atribua membros da equipe a perfis de produto do Cloud Manager.

Agora você está pronto para continuar sua jornada de integração ao revisar o documento [Access Cloud Manager,](cloud-manager.md) onde você aprenderá a acessar o Cloud Manager e criar os recursos do projeto.

## Recursos adicionais {#additional-resources}

É recomendável continuar na jornada de integração conforme descrito anteriormente. Esses são alguns recursos adicionais se você quiser fazer um mergulho profundo em um tópico específico desta jornada.

* [Introdução ao Cloud Manager](/help/onboarding/cloud-manager-introduction.md) - Saiba mais sobre o Cloud Manager, programas e ambientes do Cloud Manager.
* [Perfis de produto do Cloud Manager](/help/onboarding/aem-cs-team-product-profiles.md) - Saiba mais sobre AEM equipe as a Cloud Service e perfis de produto.
* [Tipos de identidade no Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html) - O sistema de gerenciamento de identidade do Adobe ajuda os administradores a criar e gerenciar o acesso do usuário a aplicativos e serviços. O Adobe oferece esses tipos de identidades ou contas para autenticar e autorizar usuários.

