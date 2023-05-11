---
title: Introdução à jornada de integração do AEM as a Cloud Service
description: Comece aqui para obter uma visão geral da jornada guiada por meio do processo de integração para o AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 5c5db0d133adfbbb678930ef27d8ade10fd0c3be
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 95%

---


# Jornada de integração {#onboarding-journey}

Parabéns por escolher o AEM as a Cloud Service! Este documento é o seu ponto de partida para uma jornada guiada pelo processo de integração. Se você estiver implantando um novo aplicativo ou migrando um existente, essa jornada de integração garante que suas equipes estejam configuradas e tenham acesso ao AEM as a Cloud Service.

## Introdução {#introduction}

A integração é o processo durante o qual um administrador de sistema designado configura o AEM as a Cloud Service para sua organização. O processo inclui o provisionamento inicial de recursos de nuvem e a atribuição de usuários a funções com base em suas responsabilidades de trabalho. Como resultado, cada membro pode fazer logon e acessar os recursos do AEM as a Cloud Service.

![A jornada de integração](/help/journey-onboarding/assets/onboarding-journey.png)

Este guia aborda os tópicos mais importantes da integração. No final, você terá:

* Uma compreensão completa dos diferentes termos, serviços e usuários envolvidos no processo de integração.
* Uma equipe habilitada para dar os primeiros passos e aprender como criar e desenvolver conteúdo para o seu aplicativo AEM as a Cloud Service.

Como resultado:

* Sua equipe está configurada e terá acesso aos recursos de nuvem.
* Os autores do AEM terão acesso ao AEM as a Cloud Service e poderão começar a criar conteúdo.
* Os desenvolvedores e gerentes de implantação do AEM terão acesso ao AEM as a Cloud Service e poderão começar a criar e implantar aplicativos personalizados.

## Conceitos e objetivo {#concepts}

Embora pareça haver muito a aprender quando se começa a usar o AEM as a Cloud Service, conceitualmente, existem apenas algumas partes óbvias.

* **O contrato** - Você precisa se familiarizar com o seu contrato com a Adobe, pois ele define os aspectos do processo de integração.
* **Admin Console** - É aqui que os usuários são gerenciados e as funções são atribuídas.
* **Cloud Manager** - Essa é a ferramenta usada para configurar recursos como programas e ambientes. Também é onde você acessa o Git e cria pipelines para gerenciar e implantar código personalizado.

Esses conceitos serão abordados em detalhes nesta jornada de integração. O objetivo é que, ao final da jornada, você:

* Conceda aos usuários necessários acesso ao AEMaaCS
* Configure os primeiros recursos de nuvem para o seu projeto
* Saiba como implantar seu primeiro código e criar seu primeiro conteúdo.

Basicamente, você vai começar com o pé direito seu novo projeto do AEM as a Cloud Service!

## Público {#audience}

A jornada de integração é escrita especificamente para o **administrador do sistema** de clientes novos no AEM as a Cloud Service e no AEM em geral. O administrador do sistema é o indivíduo com quem a Adobe entra em contato inicialmente após a assinatura do contrato do AEM as a Cloud Service e normalmente é a primeira pessoa a acessar e configurar os recursos do AEM as a Cloud Service. Se estiver lendo isso, provavelmente você é o administrador do sistema.

O administrador do sistema gerencia todos os aspectos dos usuários do AEMaaCS da organização, desde o acesso até as permissões. No entanto, o administrador do sistema deve interagir com outras pessoas ao longo do caminho.

| Perfil | Descrição | Função na jornada |
|---|---|---|
| Administrador do sistema | Trata-se do público-alvo desta jornada; realiza o provisionamento inicial dos recursos de nuvem e atribui os usuários às funções apropriadas com base em suas responsabilidades de trabalho | Gerencia todos os aspectos dos usuários, desde o acesso até as permissões |
| Autor de conteúdo | Cria e revisa conteúdo no AEM | Uma vez concedidas as permissões pelo administrador do sistema, os autores podem iniciar suas próprias jornadas criando conteúdo |
| Desenvolvedor | Desenvolve aplicativos do AEM que consomem conteúdo de diferentes fontes | Uma vez concedidas as permissões pelo administrador do sistema, os desenvolvedores podem iniciar suas próprias jornadas desenvolvendo soluções |
| Gerente de implantação | Adiciona ou atualiza um ambiente, executa pipelines e implanta código no ambiente do AEM ou qualidade de código. | Uma vez concedidas as permissões pelo administrador do sistema, os gerentes de implantação podem iniciar suas próprias jornadas gerenciando implantações |

Este guia de integração ilustra todo o processo de integração como administrador do sistema. As funções de usuários, desenvolvedores e gerentes de implantação do AEM são brevemente exploradas como partes adicionais e opcionais da jornada.

>[!TIP]
>
>Se você é novo no AEM as a Cloud Service, mas já está familiarizado com o AEM e está migrando do Adobe Managed Services ou do local, não deixe de conferir a [Jornada de migração do AEM as a Cloud Service.](/help/journey-migration/getting-started.md)

## Visão geral da jornada de integração {#overview}

Os artigos a seguir descrevem em detalhes os principais conceitos de integração e fornecem conhecimento fundamental sobre o AEM as a Cloud Service. Embora seja possível ir diretamente para uma parte específica da jornada, muitos conceitos baseiam-se em artigos anteriores. Portanto, se você for novo na integração, recomendamos começar do início e avançar sequencialmente.

| # | Artigo | Descrição | Público |
|---|---|---|---|
| 0 | Jornada de integração | Este documento | Administrador do sistema |
| 1 | [Preparação para a integração](preparation.md) | Antes de começar o processo de integração, há várias etapas preparatórias que o administrador do sistema deve entender para fazer logon no sistema. | Administrador do sistema |
| 2 | [Terminologia do AEM as a Cloud Service](terminology.md) | Antes de fazer logon no AEMaaCS pela primeira vez, é útil compreender a terminologia do sistema e sua estrutura básica. | Administrador do sistema |
| 3 | [O Admin Console](admin-console.md) | Saiba o que é o Admin Console, como fazer logon nele e como verificar seu perfil como administrador do sistema. | Administrador do sistema |
| 4 | [Atribuição de perfis de produto do Cloud Manager](assign-profiles-cloud-manager.md) | Revise os perfis de produto do Cloud Manager e saiba como atribuir membros da equipe aos perfis de produto do Cloud Manager. | Administrador do sistema |
| 5 | [Acessar o Cloud Manager](cloud-manager.md) | Saiba como acessar o Cloud Manager para poder configurar os recursos do projeto. | Administrador do sistema |
| 6 | [Criar um programa](create-program.md) | Saiba como criar um programa usando o Cloud Manager. | Administrador do sistema |
| 7 | [Criar ambientes](create-environments.md) | Saiba como criar um ambiente usando o Cloud Manager. | Administrador do sistema |
| 8 | [Atribuição de perfis de produto do AEM](assign-profiles-aem.md) | Saiba como o administrador do sistema atribui membros da equipe aos perfis de produto do AEM as a Cloud Service. | Administrador do sistema |
| 9 | [Tarefas do desenvolvedor e do gerente de implantação](developers.md) | Opcional - Saiba como você, na qualidade de desenvolvedor, pode acessar e gerenciar o Git do Cloud Manager e como você, na qualidade de gerente de implantação, pode configurar pipelines e implantar código no Cloud Manager. | Desenvolvedores e gerentes de implantação |
| 10 | [Tarefas do usuário do AEM](aem-users.md) | Opcional - Saiba como você, na qualidade de autor do AEM, pode acessar a instância do AEM as a Cloud Service e se familiarizar com o conteúdo de autoria. | Usuários do AEM |

## O que vem a seguir {#what-is-next}

Agora você está pronto para iniciar sua jornada de integração do AEM as a Cloud Service. Recomendamos que você continue com a próxima parte da jornada e leia o artigo [Preparação para a integração](preparation.md)

## Jornadas de documentação do AEM {#documentation-journeys}

[Uma Jornada de documentação](/help/journey-documentation/documentation-journeys.md) une vários tópicos e recursos diferentes e talvez complicados, fornecendo uma narrativa que ajuda o leitor, que pode ser novo no AEM, a entender e resolver um problema da empresa do começo ao fim, assumindo o mínimo de conhecimento prévio do tópico ou do AEM.

As Jornadas de documentação foram projetadas com princípios de práticas recomendadas, informadas pela última pesquisa da Adobe, experiência comprovada de implementação dos consultores da Adobe e feedback de projetos de clientes.

Se você quiser saber como a Adobe recomenda que você integre sua equipe no aplicativo AEM as a Cloud Service, este é o ponto de partida.

## Recursos adicionais {#additional-resources}

Veja a seguir recursos adicionais e opcionais, caso deseje ir além do conteúdo da jornada de integração.

* [Dicas e truques de campeão do AEM - Playbook integrado do Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/onboarding-playbook.md) - Assista a este vídeo para saber mais sobre dicas de integração do Cloud Manager e truques de um campeão de AEM.
