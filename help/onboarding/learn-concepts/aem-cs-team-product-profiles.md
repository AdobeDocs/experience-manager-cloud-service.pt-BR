---
title: AEM equipe as a Cloud Service e perfis de produto
description: Siga esta página para saber mais sobre AEM equipe as a Cloud Service e perfis de produto.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 56ca8e80081e62ceb3f5fc2bf9c32aa3bcee12c6
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# AEM equipe as a Cloud Service e perfis de produto {#product-profiles}

## Perfis de produto {#profiles}

Ao conceder acesso de usuário a uma solução Adobe específica, você não quer necessariamente conceder acesso total a ele. Os Perfis de produto permitem que cada solução tenha seu próprio conjunto de permissões do usuário. Eles estão disponíveis e podem ser acessados por meio da variável [Adobe Admin Console](/help/onboarding/learn-concepts/admin-console.md).

Leia mais sobre [AEM perfis de produto as a Cloud Service](#aem-product-profiles) e [Perfis de produto do Cloud Manager](#cloud-manager-product-profiles) para entender como eles funcionam em conjunto enquanto a equipe está configurada.

## AEM perfis de produto as a Cloud Service {#aem-product-profiles}

AEM as a Cloud Service é a oferta totalmente nativa em nuvem que oferece AEM como um serviço. Ele fornece AEM de maneira nativa em nuvem, com novos atributos como sempre ativos, sempre atuais, sempre seguros e sempre em escala. Ao mesmo tempo, mantém a principal proposta de valor que o AEM oferece como uma plataforma personalizável para os clientes e permite que equipes de nível empresarial se integrem em seus procedimentos de desenvolvimento e entrega. Consulte [Introdução ao Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en) para saber mais sobre AEM as a Cloud Service.

Os membros AEM da equipe as a Cloud Service serão adicionados e atribuídos a um ou mais dos seguintes perfis de produto por meio do Admin Console durante a integração.

* **Administradores de AEM**: Normalmente, um Administrador de AEM é atribuído a desenvolvedores, em particular desenvolvedores que precisarão ter acesso, por exemplo, aos ambientes de desenvolvimento. O perfil de produto Administradores de AEM será usado para conceder privilégios de administrador na instância de AEM associada.

* **Usuários AEM**: AEM Usuários são os usuários em sua organização que usam AEM as a Cloud Service como parte do contrato com o Adobe. Esses membros precisarão acessar AEM para realizar suas tarefas. O perfil de produto Usuários do AEM é tipicamente atribuído a um autor de conteúdo AEM que cria e revisa o conteúdo (pode ser de vários tipos; por exemplo, páginas, ativos, publicações e assim por diante) antes de ser publicado no site. O perfil de produto Usuários AEM mostrado abaixo é atribuído a esses membros.

   ![](/help/onboarding/learn-concepts/assets/admin-console-profiles.png)

   >[!NOTE]
   >Todos os usuários atribuídos a um perfil de produto AEM as a Cloud Service têm (somente leitura) acesso ao Cloud Manager.

## Perfis de produto do Cloud Manager {#cloud-manager-product-profiles}

O Cloud Manager tem perfis de produto pré-configurados ou, mais simplesmente, permissões baseadas em funções. O administrador do sistema será responsável pela configuração da equipe do Cloud Manager, atribuindo o a esses perfis de produtos e deverá se familiarizar com esses perfis de produtos e qual membro da equipe será atribuído a eles.
>[!NOTE]
>Consulte [Permissões baseadas em funções no Cloud Manager](/help/onboarding/learn-concepts/cloud-manager-introduction.md##role-based-permissions) para obter mais detalhes.

Cada um dos perfis de produto tem permissões específicas associadas a ele. Por exemplo, se você estiver na função de um:

* **Proprietário da empresa**, você tem a permissão de adicionar um novo programa ou editar um programa, adicionar ou atualizar um ambiente, adicionar/editar/excluir o pipeline e executar qualquer pipeline, além de implantar o código AEM ambiente ou qualidade de código.

* **Gerenciador de implantação**, você tem a permissão para adicionar ou atualizar um ambiente, executar qualquer pipeline e implantar o código AEM ambiente ou qualidade de código.

* **Desenvolvedor**, você tem permissão para gerar o Token de acesso pessoal para acessar o Git.

* **Gerenciador de programas**, você tem permissão para programar pipelines, substituir portas de qualidade de 3 camadas e fornecer aprovação de produção.

Um usuário pode ser atribuído a vários perfis de produto. Por exemplo, a atribuição de funções de Proprietário comercial e Gerente de implantação a um usuário fornece a combinação ou a soma dessas permissões.

A equipe do Cloud Manager incluirá pelo menos:

* Um proprietário comercial, que normalmente também é o Administrador do sistema, e deve ser a primeira pessoa a fazer logon e acessar o Cloud Manager
* Um gerenciador de implantação
* Um desenvolvedor

   >[!NOTE]
   >Para ter acesso a AEM as a Cloud Service, os usuários devem pertencer a um dos dois perfis de produto: `AEM Users` ou `AEM Administrators`. Você deve receber permissões para a instância. As permissões para administrar o Cloud Manager associado não serão suficientes.
