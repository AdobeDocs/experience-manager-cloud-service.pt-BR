---
title: Introdução à jornada de integração do AEM as a Cloud Service
description: Comece aqui para obter uma visão geral da jornada guiada por meio do processo de integração para o AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 58%

---


# Jornada de integração {#onboarding-journey}

Parabéns por escolher o AEM as a Cloud Service! Este documento é o seu ponto de partida para uma jornada guiada pelo processo de integração. Se você estiver implantando um novo aplicativo ou migrando um já existente, essa jornada de integração garante que suas equipes estejam configuradas e tenham acesso ao AEM as a Cloud Service.

## Introdução {#introduction}

A integração é o processo durante o qual um administrador de sistema designado configura o AEM as a Cloud Service para sua organização. Esse processo inclui o provisionamento inicial de recursos de nuvem e a atribuição de usuários a funções com base em suas responsabilidades de trabalho. Como resultado, cada membro é capaz de fazer logon e acessar seu recurso no AEM as a Cloud Service.

![A jornada de integração](/help/journey-onboarding/assets/onboarding-journey.png)

Este guia aborda os tópicos mais importantes da integração. No final, você terá o seguinte:

* Uma compreensão completa dos diferentes termos, serviços e usuários envolvidos no processo de integração.
* Uma equipe habilitada para dar os primeiros passos e aprender como criar e desenvolver conteúdo para o seu aplicativo AEM as a Cloud Service.

Como resultado:

* Sua equipe está configurada e tem acesso aos recursos de nuvem.
* Autores de AEM têm acesso ao AEM as a Cloud Service e podem começar a criar conteúdo.
* Desenvolvedores e gerentes de implantação do AEM têm acesso ao AEM as a Cloud Service e podem começar a criar e implantar aplicativos personalizados.

## Conceitos e objetivo {#concepts}

Embora pareça haver muito a aprender quando se começa a usar o AEM as a Cloud Service, conceitualmente, existem apenas algumas partes óbvias.

* **O Contrato** - Você deve conhecer seu contrato de Adobe, pois ele define os aspectos do processo de integração.
* **Admin Console** - Onde os usuários são gerenciados e as funções são atribuídas.
* **Cloud Manager** - A ferramenta para configurar recursos como programas e ambientes. Também é onde você acessa o Git e cria pipelines para gerenciar e implantar código personalizado.

Esses conceitos são apresentados em detalhes nesta jornada de integração. O objetivo é que, ao final da jornada, você:

* Conceda ao usuário necessário acesso ao AEM as a Cloud Service.
* Configure os primeiros recursos de nuvem para o seu projeto.
* Saiba como implantar seu primeiro código e criar seu primeiro conteúdo.

Basicamente, você chega ao fim com seu novo projeto as a Cloud Service de AEM!

## Público {#audience}

A jornada de integração é escrita especificamente para o **administrador do sistema** de clientes novos no AEM as a Cloud Service e no AEM em geral. O administrador do sistema é o indivíduo com quem o Adobe entra em contato pela primeira vez depois que seu contrato com o AEM as a Cloud Service é assinado. Normalmente, eles são a primeira pessoa a acessar e configurar seus recursos no AEM as a Cloud Service. Se você estiver lendo este tópico, é provável que seja o administrador do sistema.

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
>Se você é novo no AEM e está as a Cloud Service com o AEM e está migrando do Adobe Managed Services ou do local, não deixe de conferir [Jornada de migração as a Cloud Service para AEM](/help/journey-migration/getting-started.md).

## Visão geral da jornada de integração {#overview}

Os artigos a seguir descrevem em detalhes os principais conceitos de integração e fornecem conhecimento fundamental sobre o AEM as a Cloud Service. Embora seja possível ir diretamente para uma parte específica da jornada, muitos conceitos baseiam-se em artigos anteriores. Portanto, se você for novo na integração, o Adobe recomenda começar do início e avançar sequencialmente.

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
| 8 | [Atribuição de perfis de produto do AEM](assign-profiles-aem.md) | Saiba como o Administrador do sistema atribui membros da equipe a perfis de produtos no AEM as a Cloud Service. | Administrador do sistema |
| 9 | [Tarefas do desenvolvedor e do gerente de implantação](developers.md) | Opcional - Como desenvolvedor, saiba como acessar e gerenciar o Git do Cloud Manager e como você pode configurar pipelines e implantar código no Cloud Manager. | Desenvolvedores e gerentes de implantação |
| 10 | [Tarefas do usuário do AEM](aem-users.md) | Opcional - Como autor de AEM, saiba como você pode acessar a instância as a Cloud Service AEM do AEM e se familiarizar com o conteúdo de criação para o as a Cloud Service. | Usuários do AEM |

## O que vem a seguir {#what-is-next}

Agora você está pronto para iniciar sua jornada de integração do AEM as a Cloud Service. É recomendável continuar com a próxima parte da jornada e ler o artigo [Preparação para a integração](preparation.md)

## Jornadas de documentação do AEM {#documentation-journeys}

[Uma Jornada de documentação](/help/journey-documentation/documentation-journeys.md) O une vários tópicos e recursos diferentes e complicados. Ele fornece uma narrativa que ajuda um leitor novo no AEM a entender e resolver um problema empresarial do começo ao fim, assumindo o mínimo de conhecimento prévio sobre o tópico ou AEM.

As Jornadas de documentação foram projetadas com princípios de práticas recomendadas, informadas pela última pesquisa da Adobe, experiência comprovada de implementação dos consultores da Adobe e feedback de projetos de clientes.

Se você quiser saber o que a Adobe recomenda sobre como integrar sua equipe ao seu novo aplicativo AEM as a Cloud Service, comece por aqui!

<!-- ERROR: Not Found (HTTP error 404)
## Additional Resources {#additional-resources}

The following are additional, optional resources if you would like to go beyond the content of the onboarding journey.

* [AEM Champion Tips and Tricks - Cloud Manager Onboarding Playbook](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/onboarding-playbook.md) - Watch this video to learn Cloud Manager onboarding tips and trick from an AEM champion. -->


