---
title: Introdução à Jornada de integração AEM as a Cloud Service
description: Comece aqui para obter uma visão geral da jornada guiada por meio do processo de integração para o AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 75c0e8cbaa409fa48750e794c27ace98eda107d0
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 17%

---


# Jornada de integração {#onboarding-journey}

Parabéns por escolher AEM as a Cloud Service! Este documento é o seu ponto de partida para uma jornada guiada pelo processo de integração. Se você estiver implantando um novo aplicativo ou migrando um existente, essa jornada de integração garante que suas equipes estejam configuradas e tenham acesso a AEM as a Cloud Service.

## Introdução {#introduction}

A integração é o processo durante o qual um administrador de sistema designado se configura AEM as a Cloud Service para sua organização. Isso inclui o provisionamento inicial de recursos de nuvem e a atribuição de usuários a funções com base em suas responsabilidades de trabalho. Como resultado, cada membro pode fazer logon e acessar seus recursos as a Cloud Service AEM.

![A jornada de integração](/help/journey-onboarding/assets/onboarding-journey.png)

Este guia aborda os tópicos de integração mais importantes, para que, na conclusão, você tenha:

* Compreensão completa dos diferentes termos, serviços e usuários envolvidos no processo de integração.
* Uma equipe habilitada para dar os primeiros passos e aprender como criar e desenvolver conteúdo para o seu aplicativo AEM as a Cloud Service.

Como resultado:

* Sua equipe será configurada e terá acesso aos recursos da nuvem.
* AEM autores terão acesso AEM as a Cloud Service e poderão começar a criar conteúdo.
* AEM desenvolvedores e gerentes de implantação terão acesso a AEM as a Cloud Service e poderão começar a criar e implantar aplicativos personalizados.

## Conceitos e meta {#concepts}

Embora pareça haver muito para aprender quando se começa com AEM as a Cloud Service, conceitualmente existem apenas algumas peças lógicas.

* **O contrato** - Você precisa conhecer seu contrato de Adobe, pois ele define os aspectos do processo de integração.
* **Admin Console** - É aqui que os usuários são gerenciados e as funções são atribuídas.
* **Cloud Manager** - Essa é a ferramenta para configurar recursos como programas e ambientes. Também é onde você acessa o git e cria pipelines para gerenciar e implantar seu código personalizado.

Esses conceitos serão detalhados nesta jornada de integração. O objetivo é que, ao final da jornada, você:

* Concederam aos usuários necessários acesso ao AEMaaCS
* Configure os primeiros recursos da nuvem para o seu projeto
* Saiba como implantar seu primeiro código e criar seu primeiro conteúdo.

Basicamente, você vai chegar ao fim com seu novo projeto as a Cloud Service AEM!

## Público {#audience}

A jornada de integração é escrita especificamente para a **administrador do sistema** do cliente novo para AEM as a Cloud Service e AEM em geral. O administrador do sistema é o indivíduo que é contatado pela primeira vez pelo Adobe depois que seu contrato as a Cloud Service AEM é assinado e normalmente é a primeira pessoa a acessar e configurar seus recursos as a Cloud Service AEM. Se estiver lendo isso, você provavelmente será o administrador do sistema.

O administrador do sistema gerencia todos os aspectos dos usuários do AEMaaCS de sua organização, do acesso às permissões. No entanto, o administrador do sistema deve interagir com outras pessoas ao longo do caminho.

| Perfil | Descrição | Função na jornada |
|---|---|---|
| Administrador do sistema | O Target dessa jornada fornece provisionamento inicial de recursos de nuvem e atribuição de usuários a funções apropriadas com base em suas responsabilidades de trabalho | Gerencia todos os aspectos dos usuários do acesso às permissões |
| Autor do conteúdo | Cria e revisa o conteúdo no AEM | Depois de concedidas permissões pelo administrador do sistema, os autores podem iniciar sua própria jornada criando conteúdo |
| Desenvolvedor | Desenvolve aplicativos do AEM que consomem conteúdo de diferentes fontes | Depois de obter as permissões do administrador do sistema, os desenvolvedores podem iniciar suas próprias soluções de desenvolvimento do jornada |
| Gerenciador de implantação | Adiciona ou atualiza um ambiente, executa pipelines e implanta código para AEM ambiente ou qualidade de código. | Depois de conceder permissões pelo administrador do sistema, os gerentes de implantação podem iniciar suas próprias implantações de gerenciamento de jornadas |

Este guia de integração ilustra todo o processo de integração como administrador do sistema. As funções de usuários, desenvolvedores e gerentes de implantação AEM são brevemente exploradas como partes adicionais e opcionais da jornada.

>[!TIP]
>
>Se você é novo em AEM as a Cloud Service, mas já está familiarizado com AEM e está migrando do Adobe Managed Services ou no local, certifique-se de verificar o [AEM Jornada de migração as a Cloud Service.](/help/journey-migration/getting-started.md)

## Visão geral da integração da Jornada {#overview}

Os artigos a seguir descrevem em detalhes os principais conceitos de integração e fornecem conhecimento fundamental AEM as a Cloud Service. Embora seja possível ir diretamente para uma parte específica da jornada, muitos conceitos baseiam-se em artigos anteriores. Portanto, se você não estiver familiarizado com integração, recomendamos que você comece no início e avance sequencialmente.

| # | Artigo | Descrição | Público |
|---|---|---|---|
| 0 | Jornada de integração | Este documento | Administrador do sistema |
| 1 | [Preparação de integração](preparation.md) | Antes do início do processo de integração, há várias etapas preparatórias que o administrador do sistema deve entender antes de fazer logon no sistema. | Administrador do sistema |
| 2 | [AEM Terminologia as a Cloud Service](terminology.md) | Antes de fazer logon no AEMaaCS pela primeira vez, é útil entender a terminologia do sistema e sua estrutura básica. | Administrador do sistema |
| 3 | [O Admin Console](admin-console.md) | Saiba o que é o Admin Console, como fazer logon e como verificar seu perfil como administrador de sistema. | Administrador do sistema |
| 4 | [Atribuir perfis de produto do Cloud Manager](assign-profiles-cloud-manager.md) | Revise os Perfis de produto do Cloud Manager e saiba como atribuir membros da equipe aos perfis de produto do Cloud Manager. | Administrador do sistema |
| 5 | [Acessar o Cloud Manager](cloud-manager.md) | Saiba como acessar o Cloud Manager para poder configurar os recursos do projeto. | Administrador do sistema |
| 6 | [Criar um programa](create-program.md) | Saiba como criar um programa usando o Cloud Manager. | Administrador do sistema |
| 7 | [Criar ambientes](create-environments.md) | Saiba como criar um ambiente usando o Cloud Manager. | Administrador do sistema |
| 8 | [Atribuir perfis de produto AEM](assign-profiles-aem.md) | Saiba como o Administrador do sistema atribui membros da sua equipe a AEM perfis de produto as a Cloud Service. | Administrador do sistema |
| 9 | [Tarefas do desenvolvedor e do gerenciador de implantação](developers.md) | Opcional - saiba como, como desenvolvedor, você pode acessar e gerenciar o Git do Cloud Manager e como, como Gerenciador de implantação, você pode configurar pipelines e implantar código no Cloud Manager. | Desenvolvedores e gerenciadores de implantação |
| 10 | [Tarefas do usuário AEM](aem-users.md) | Opcional - saiba como um autor de AEM você pode acessar AEM instância as a Cloud Service e se familiarizar com o conteúdo de criação para AEM as a Cloud Service. | Usuários AEM |

## O que vem a seguir {#what-is-next}

Agora você está pronto para iniciar sua jornada de integração as a Cloud Service AEM. Recomendamos que você continue para a próxima parte da jornada e leia o artigo [Preparação de integração](preparation.md)

## Jornadas de documentação do AEM {#documentation-journeys}

[Uma Jornada de documentação](/help/journey-documentation/documentation-journeys.md) une vários tópicos e recursos diferentes e talvez complicados, fornecendo uma narrativa que ajuda o leitor, que pode ser novo no AEM, a entender e resolver um problema da empresa do começo ao fim, assumindo o mínimo de conhecimento prévio do tópico ou do AEM.

As Jornadas de documentação foram projetadas com princípios de práticas recomendadas, informadas pela última pesquisa da Adobe, experiência comprovada de implementação dos consultores da Adobe e feedback de projetos de clientes.

Se você quiser saber como o Adobe recomenda como integrar sua equipe ao novo aplicativo as a Cloud Service AEM, este é o ponto de partida!
