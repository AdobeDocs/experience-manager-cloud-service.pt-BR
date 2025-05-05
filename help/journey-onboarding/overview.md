---
title: Introdução à jornada de integração do AEM as a Cloud Service
description: Comece aqui para obter uma visão geral da jornada guiada por meio do processo de integração para o AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
recommendations: noDisplay
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 68%

---


# Jornada de integração {#onboarding-journey}

Parabéns por escolher o AEM as a Cloud Service! Este documento é o seu ponto de partida para uma jornada guiada pelo processo de integração. Se você estiver implantando uma nova aplicação ou migrando uma existente, esta jornada de integração configurará suas equipes. Isso garante que eles tenham acesso ao AEM as a Cloud Service.

## Introdução {#introduction}

O Adobe Experience Manager é um conjunto eficiente de serviços de conteúdo de composição que fornecem rapidamente experiências personalizadas e altamente impactantes em qualquer canal, desbloqueando conteúdo para todos. **Edge Delivery Services** é a mais recente inovação do Adobe Experience Manager, que permite uma velocidade de conteúdo extrema e oferece experiências excepcionais. Saiba como começar a usar os Edge Delivery Services, consultando a [Visão geral dos Edge Delivery Services](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/edge-delivery/overview). Para entender como usar o Edge Delivery Services, consulte a página [Tutorial do desenvolvedor](https://www.aem.live/developer/tutorial).

A integração é o processo durante o qual um administrador de sistema designado configura o AEM as a Cloud Service para sua organização. O processo inclui o provisionamento inicial de recursos da nuvem e a atribuição de usuários a funções com base em suas responsabilidades de trabalho. Como resultado, cada membro pode fazer logon e acessar os recursos do AEM as a Cloud Service.

![A jornada de integração](/help/journey-onboarding/assets/onboarding-journey.png).

Este guia aborda os tópicos mais importantes da integração. No final, você terá:

* Uma compreensão completa dos diferentes termos, serviços e usuários envolvidos no processo de integração.
* Uma equipe habilitada para dar os primeiros passos e aprender como criar e desenvolver conteúdo para o seu aplicativo AEM as a Cloud Service.

Como resultado:

* Sua equipe está configurada e tem acesso aos recursos da nuvem.
* Os autores do AEM terão acesso ao AEM as a Cloud Service e poderão começar a criar conteúdo.
* Os desenvolvedores e gerentes de implantação do AEM têm acesso ao AEM as a Cloud Service e poderão começar a criar e implantar aplicativos personalizados.

## Conceitos e objetivo {#concepts}

Embora pareça haver muito a aprender quando se começa a usar o AEM as a Cloud Service, conceitualmente, existem apenas algumas partes óbvias.

* **O Contrato**: é necessário se familiarizar com o contrato da Adobe, pois ele define os aspectos do processo de integração.
* **Admin Console**: É aqui que os usuários são gerenciados e as funções são atribuídas.
* **Cloud Manager**: essa é a ferramenta usada para configurar recursos como programas e ambientes. Também é onde você acessa o Git e cria pipelines para gerenciar e implantar código personalizado.

Esses conceitos serão abordados em detalhes nesta jornada de integração. O objetivo é que, ao final da jornada, você possa fazer o seguinte:

* Conceda ao usuário necessário acesso ao AEM as a Cloud Service.
* Configure os primeiros recursos de nuvem para o seu projeto.
* Sabe como implantar seu primeiro código e criar seu primeiro conteúdo.

Basicamente, começará com o pé direito seu novo projeto do AEM as a Cloud Service!

## Público {#audience}

A jornada de integração foi escrita especificamente para o **administrador do sistema** de clientes novos no AEM as a Cloud Service e no AEM em geral. O administrador do sistema é o indivíduo que entra em contato com o Adobe primeiro após a assinatura do contrato do AEM as a Cloud Service. Normalmente, é a primeira pessoa a acessar e configurar os recursos no AEM as a Cloud Service. Se estiver lendo este tópico, é provável que seja o administrador do sistema.

O administrador do sistema gerencia todos os aspectos dos usuários do AEMaaCS da organização, desde o acesso até as permissões. No entanto, o administrador do sistema deve interagir com outras pessoas ao longo do caminho.

| Perfil | Descrição | Função na jornada |
|---|---|---|
| Administrador do sistema | O público-alvo desta jornada fornece provisionamento inicial de recursos de nuvem e atribuição de usuários a funções apropriadas com base em suas responsabilidades de trabalho | Gerencia todos os aspectos dos usuários, desde o acesso até as permissões |
| Autor de conteúdo | Cria e revisa conteúdo no AEM | Uma vez concedidas as permissões pelo administrador do sistema, os autores podem iniciar sua própria jornada na criação de conteúdo |
| Desenvolvedor | Desenvolve aplicativos de AEM que consomem conteúdo de diferentes fontes | Uma vez concedidas as permissões pelo administrador do sistema, os desenvolvedores podem iniciar suas próprias jornadas no desenvolvimento de soluções |
| Gerente de implantação | Adiciona ou atualiza um ambiente, executa pipelines e implanta código no ambiente do AEM ou qualidade de código. | Uma vez concedidas as permissões pelo administrador do sistema, os gerentes de implantação podem iniciar suas próprias jornadas gerenciando implantações |

Este guia de integração ilustra todo o processo de integração como administrador do sistema. As funções de usuários, desenvolvedores e gerentes de implantação do AEM são brevemente exploradas como partes adicionais e opcionais da jornada.

>[!TIP]
>
>Se você é novo no AEM as a Cloud Service e está familiarizado com o AEM e está migrando do Managed Services local ou do Adobe, confira a [Jornada de migração do AEM as a Cloud Service](/help/journey-migration/getting-started.md).

## Visão geral da jornada de integração {#overview}

Os artigos a seguir descrevem em detalhes os principais conceitos de integração e fornecem conhecimento fundamental sobre o AEM as a Cloud Service. Embora seja possível ir diretamente para uma parte específica da jornada, muitos conceitos baseiam-se em artigos anteriores. Portanto, se for novo na integração, a Adobe recomenda começar no início e avançar sequencialmente.

| | Artigo | Descrição | Público |
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
| 9 | [Tarefas do desenvolvedor e do gerente de implantação](developers.md) | Opcional: saiba como um desenvolvedor consegue acessar e gerenciar o Git do Cloud Manager e como um gerente de implantação consegue configurar pipelines e implantar código no Cloud Manager. | Desenvolvedores e gerentes de implantação |
| 10 | [Tarefas do usuário do AEM](aem-users.md) | Opcional: saiba como um autor do AEM consegue acessar a instância do AEM as a Cloud Service e se familiarizar com a criação de conteúdo. | Usuários do AEM |

## O que vem a seguir {#what-is-next}

Agora você está pronto para iniciar sua jornada de integração do AEM as a Cloud Service. Recomendamos continuar na próxima parte da jornada e ler o artigo [Preparação para a integração](preparation.md)

## jornadas de documentação do AEM {#documentation-journeys}

[Uma jornada de documentação](/help/journey-documentation/documentation-journeys.md) une vários tópicos e recursos diferentes e complicados. Ela fornece uma narrativa que ajuda um leitor novo no AEM a entender e resolver um problema empresarial do começo ao fim, enquanto assume o mínimo de conhecimento prévio sobre o tópico ou o AEM.

As Jornadas de documentação foram criadas com base nos princípios das práticas recomendadas. Eles são informados usando a pesquisa mais recente do Adobe, a experiência comprovada de implementação dos consultores do Adobe e o feedback dos projetos de clientes.

Se quiser saber o que a Adobe recomenda sobre como integrar sua equipe ao novo aplicativo AEM as a Cloud Service, comece por aqui.

## Recursos adicionais {#additional-resources}

A seguir estão recursos adicionais e opcionais se quiser ir além do conteúdo da jornada de integração.

* [Integração com o AEM as a Cloud Service](https://experienceleague.adobe.com/pt-br/docs/experience-manager-learn/cloud-service/migration/moving-to-aem-as-a-cloud-service/onboarding) - Este breve vídeo fornece uma visão geral do processo de integração do Cloud Service para o AEM.
