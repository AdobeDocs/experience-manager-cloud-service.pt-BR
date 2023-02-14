---
title: jornada do desenvolvedor de CMS sem periféricos AEM
description: Saiba mais sobre o desenvolvimento sem periféricos usando o Adobe Experience Manager (AEM) como um CMS sem periféricos. Saiba como usar recursos como Modelos de conteúdo, Fragmentos de conteúdo e uma API do GraphQL para potencializar a entrega de conteúdo sem interface.
landing-page-description: Saiba mais sobre a entrega e implementação de conteúdo sem periféricos. Saiba mais sobre como desenvolver sua estratégia na sua empresa.
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
source-git-commit: 39a8b505ebf323ea18d014d9603356239dc39646
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 16%

---

# jornada do desenvolvedor de CMS sem periféricos AEM {#aem-headless-developer-journey}

Bem-vindo à documentação para desenvolvedores novos no Adobe Experience Manager CMS sem periféricos!

Saiba mais sobre os recursos avançados e flexíveis, seus recursos e como aproveitá-los em seu primeiro projeto de desenvolvimento sem periféricos. Esta jornada fornece todas as informações necessárias para desenvolver seu primeiro aplicativo sem periféricos.

>[!CONTEXTUALHELP]
>id="aemcloud_headless_developer_resources"
>title="Recursos do desenvolvedor sem cabeçalho AEM e documentação avançada"
>abstract="Tudo o que você precisa saber sobre AEM CMS sem periféricos e criar e enviar aplicativos melhores e experiências mais rápidas."
>additional-url="https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR" text="Recursos de desenvolvedor sem periféricos do AEM"

## Introdução {#introduction}

A implementação sem cabeçalho do AEM usa os Modelos de fragmentos de conteúdo e os Fragmentos de conteúdo para se concentrar na criação de fragmentos de conteúdo estruturados, neutros em canais e reutilizáveis, bem como no delivery entre canais. Para isso, ele perde o gerenciamento de páginas e componentes como é tradicional em soluções de pilha completa. É um padrão de desenvolvimento moderno e dinâmico para a implementação de experiências digitais.

Este guia aborda os tópicos de implementação sem cabeçalho no AEM para que, quando terminar, você:

* Ter uma compreensão completa do que é entrega de conteúdo sem periféricos e de seus benefícios.
* Entenda AEM recursos sem periféricos e como eles trabalham juntos para proporcionar uma experiência sem periféricos.
* Tenha a capacidade de realizar as primeiras etapas de implementação do seu primeiro projeto sem periféricos AEM.

>[!TIP]
>
> Se preferir **aprenda fazendo** e já tiver conhecimento do AEM, visite os tutoriais do AEM Headless, que são organizados pela API e pela estrutura e estão disponíveis no [Seção Recursos adicionais](#additional-resources) no final deste documento.

## Público {#audience}

Essa jornada foi projetada para o persona do desenvolvedor, apresentando os requisitos, as etapas e a abordagem de um projeto sem cabeçalho AEM da perspectiva do desenvolvedor. A jornada define personas adicionais com as quais o desenvolvedor deve interagir para um projeto bem-sucedido, mas o ponto de vista da jornada é o do desenvolvedor.

A seguir estão os perfis que interagem nessa jornada.

| Perfil | Descrição | Função nesta Jornada |
|---|---|---|
| Desenvolvedor (público-alvo) | Tem experiência no desenvolvimento de aplicativos sem periféricos que consomem conteúdo de diferentes fontes | Público-alvo desta jornada |
| Autor de conteúdo | Cria e gerencia conteúdo entregue sem interface | Os autores de conteúdo criam conteúdo que o desenvolvedor oferece sem cabeçalho. |
| Administrador | Gerencia as definições básicas e a configuração do AEM | O desenvolvedor trabalha com o administrador para fazer as alterações de configuração necessárias para o desenvolvimento. |
| Arquiteto de conteúdo | Analisa os requisitos dos dados que devem ser entregues sem periféricos e define a estrutura desses dados | Os desenvolvedores trabalham com o arquiteto de conteúdo para entender a estrutura dos dados e os requisitos para fornecê-los sem interrupções. |

## A Jornada de desenvolvedores headless {#the-journey}

Abordaremos muitos tópicos nesta jornada, que lhe fornecerá o conhecimento fundamental de ser imprudente em AEM.

Embora seja possível ir diretamente para uma parte específica da jornada, muitos conceitos são criados com base em artigos anteriores. Recomendamos que você comece no início e avance sequencialmente.

| # | Artigo | Descrição |
|---|---|---|
| 0 | jornada do desenvolvedor sem periféricos do AEM | Este documento |
| 1 | [Saiba mais sobre o desenvolvimento headless CMS](learn-about.md) | Saiba mais sobre a tecnologia headless e quando usá-la. |
| 2 | [Introdução ao AEM Headless as a Cloud Service](getting-started.md) | Saiba mais sobre AEM pré-requisitos headless |
| 3 | [Caminho para sua primeira experiência usando o AEM Headless](path-to-first-experience.md) | Configure seu ambiente de desenvolvimento e saiba como integrar um aplicativo simples com AEM headless |
| 4 | [Como modelar seu conteúdo](model-your-content.md) | Saiba como modelar sua estrutura de conteúdo. |
| 5 | [Como acessar seu conteúdo por meio das APIs de entrega do AEM](access-your-content.md) | Saiba como usar consultas do GraphQL para acessar o conteúdo dos Fragmentos de conteúdo. |
| 6 | [Como atualizar seu conteúdo por meio de APIs do AEM Assets](update-your-content.md) | Saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo. |
| 7 | [Como unir tudo - seu aplicativo e seu conteúdo no AEM Headless](put-it-all-together.md) | Saiba como aceitar seu AEM Project e prepará-lo para entrar em vigor com o AEM Headless SDK. |
| 8 | [Como executar o aplicativo headless](go-live.md) | Saiba como implantar o aplicativo ao vivo e obter seu código local no Git e movê-lo para o pipeline de Git do Cloud Manager para CI/CD. |
| 9 | [Opcional - Como criar aplicativos de página única (SPA) com AEM](create-spa.md) | Explore como combinar a entrega sem interface e saiba como criar SPA editáveis usando AEM estrutura SPA Editor. |

{style=&quot;table-layout:auto&quot;}

## O que vem a seguir {#what-is-next}

Comece fazendo check-out do próximo artigo: [Saiba mais sobre o CMS Headless Development (Desenvolvimento sem periféricos CMS).](learn-about.md)

### Escolha Sua Própria Aventura {#choose-your-path}

Você prefere aprender a seu próprio ritmo? Confira estas opções:

* Se preferir continuar a **saiba mais sobre conceitos sem periféricos e AEM tecnologias sem periféricos**, você deve continuar sua jornada sem periféricos AEM conforme recomendado ao revisar o documento em seguida [Como modelar seu conteúdo como modelos de conteúdo AEM](model-your-content.md) onde você aprende a modelar sua estrutura de conteúdo no AEM.
* Se preferir **aprenda fazendo**, você pode pular para o [Introdução ao AEM tutorial prático](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=pt-BR) onde você vai participar diretamente AEM desenvolvimento sem cabeçalho implementando um projeto simples para expor AEM conteúdo sem cabeçalho.

## Recursos adicionais {#additional-resources}

As jornadas de documentação mostram como o AEM soluciona um problema comercial fornecendo uma narrativa que o orienta por processos e recursos relacionados. Uma jornada ilustra como vários recursos trabalham juntos para atender a uma única necessidade de negócios.

Confira estas jornadas adicionais para obter mais informações sobre como AEM recursos avançados trabalham juntos.

* [Tutoriais AEM headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR) - Se você preferir aprender fazendo e tendo conhecimento existente de AEM, utilize nossos tutoriais práticos organizados por API e framework, que exploram a criação e o uso de aplicativos criados AEM Headless.
* [jornada de tradução sem cabeçalho AEM](/help/journey-headless/translation/overview.md) - Essa jornada de documentação oferece uma ampla compreensão da tecnologia sem interface, como a AEM fornece conteúdo sem interface e como você pode traduzi-la.
* [Jornada de criação headless](/help/journey-headless/author/overview.md) - comece aqui para obter uma jornada guiada pelos recursos headless avançados e flexíveis do AEM, suas funcionalidades e aprenda a modelar o conteúdo em seu primeiro projeto headless.
* [Jornada do arquiteto headless](/help/journey-headless/architect/overview.md) - comece aqui para obter uma introdução aos recursos headless avançados e flexíveis do Adobe Experience Manager as a Cloud Service e aprender como modelar o conteúdo para seu projeto.
* [AEM documentação técnica as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=pt-BR) - Se você já tem uma compreensão firme das tecnologias AEM e sem interface, confira nossos documentos técnicos aprofundados.
