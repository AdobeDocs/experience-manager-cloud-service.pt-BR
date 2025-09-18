---
title: Jornada de Desenvolvedor do AEM CMS Headless
description: Saiba mais sobre o desenvolvimento headless usando o Adobe Experience Manager (AEM) como um CMS Headless. Saiba como usar recursos como Modelos de conteúdo, Fragmentos de conteúdo e uma API GraphQL para potencializar a entrega de conteúdo headless.
landing-page-description: Saiba mais sobre a entrega e implementação de conteúdo headless. Saiba mais sobre como desenvolver sua estratégia dentro do seu negócio.
exl-id: d14a1e30-dd04-49a8-8cda-27c80a4bb0f5
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: f9634228fed8c194f1bdcdc9a368d4c0492b7fd5
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 94%

---

# Jornada de Desenvolvedor do AEM CMS Headless {#aem-headless-developer-journey}

Bem-vindo à documentação para desenvolvedores novos no Adobe Experience Manager CMS headless!

Saiba mais sobre os avançados e flexíveis recursos headless, suas funcionalidades e como aproveitá-los em seu primeiro projeto de desenvolvimento headless. Esta jornada fornece todas as informações necessárias para desenvolver seu primeiro aplicativo headless.

>[!CONTEXTUALHELP]
>id="aemcloud_headless_developer_resources"
>title="Recursos de desenvolvedor do AEM Headless e documentação avançada"
>abstract="Tudo o que você precisa aprender sobre o CMS headless do AEM, para criar e distribuir aplicativos melhores e fornecer experiências mais rápidas."
>additional-url="https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR" text="Recursos de desenvolvedor do AEM Headless"


## Introdução {#introduction}

A implementação Headless do AEM usa os Modelos de fragmentos de conteúdo e os Fragmentos de conteúdo para se concentrar na criação de fragmentos de conteúdo estruturados, neutros e reutilizáveis, bem como em sua entrega entre canais. Para isso, ele abre mão do gerenciamento de páginas e componentes, como é tradicional em soluções de pilha completa. É um padrão de desenvolvimento moderno e dinâmico para implementação de experiências digitais.

Este guia aborda os tópicos de implementação headless no AEM. Quando terminar, você poderá:

* Tenha uma compreensão completa do que é entrega de conteúdo headless e seus benefícios.
* Entenda os recursos headless do AEM e como eles trabalham juntos para proporcionar uma experiência headless.
* Dê os primeiros passos para implementar seu primeiro projeto headless no AEM.

>[!TIP]
>
> Se preferir **aprender na prática** e já tiver conhecimento do AEM, visite os tutoriais do AEM Headless, que são organizados pela API e pela estrutura e estão disponíveis na [Seção Recursos adicionais](#additional-resources) no final deste documento.

## Público-alvo {#audience}

Essa jornada foi projetada para o perfil do desenvolvedor, apresentando os requisitos, as etapas e a abordagem de um projeto AEM Headless da perspectiva do desenvolvedor. A jornada define perfis adicionais com as quais o desenvolvedor deve interagir para um projeto bem-sucedido, mas o ponto de vista da jornada é o do desenvolvedor.

A seguir estão os perfis que interagem nessa jornada.

| Perfil | Descrição | Função nesta jornada |
|---|---|---|
| Desenvolvedor (público-alvo) | Tem experiência no desenvolvimento de aplicativos headless que consomem conteúdo de diferentes fontes | Público-alvo desta jornada |
| Autor de conteúdo | Cria e gerencia conteúdo que é entregue de forma headless | Os Autores de conteúdo criam conteúdo que o desenvolvedor entrega de forma headless. |
| Administrador | Gerencia as definições básicas e a configuração do AEM | O desenvolvedor trabalha com o administrador para fazer as alterações de configuração necessárias para o desenvolvimento. |
| Arquiteto de conteúdo | Analisa os requisitos dos dados que devem ser entregues pelo método headless e define a estrutura desses dados | Os desenvolvedores trabalham com o arquiteto de conteúdo para entender a estrutura dos dados e os requisitos para fornecê-los de forma headless. |

## A jornada de desenvolvedores headless {#the-journey}

Abordaremos muitos tópicos nesta jornada, que lhe fornecerá o conhecimento fundamental de headless no AEM.

Embora você possa ir diretamente para uma parte específica da jornada, muitos conceitos são construídos sobre os citados nos artigos anteriores. A Adobe recomenda que você comece do início e avance sequencialmente.

| # | Artigo | Descrição |
|---|---|---|
| 0 | Jornada do desenvolvedor AEM headless | Este documento |
| 1 | [Saiba mais sobre o desenvolvimento headless CMS](learn-about.md) | Saiba mais sobre a Tecnologia headless e quando usá-la. |
| 2 | [Introdução ao AEM Headless as a Cloud Service](getting-started.md) | Saiba mais sobre os pré-requisitos AEM Headless |
| 3 | [Caminho para sua primeira experiência usando o AEM Headless](path-to-first-experience.md) | Configure seu ambiente de desenvolvimento e saiba como integrar um aplicativo simples com AEM Headless |
| 4 | [Como modelar seu conteúdo](model-your-content.md) | Saiba como modelar sua estrutura de conteúdo. |
| 5 | [Como acessar seu conteúdo por meio das APIs de entrega do AEM](access-your-content.md) | Saiba como usar consultas do GraphQL para acessar o Conteúdo dos fragmentos de conteúdo. |
| 6 | [Como atualizar seu conteúdo por meio de APIs do AEM Assets](update-your-content.md) | Saiba como usar a REST API para acessar e atualizar o Conteúdo dos fragmentos de conteúdo. |
| 7 | [Como unir tudo - seu aplicativo e seu conteúdo no AEM Headless](put-it-all-together.md) | Saiba como aceitar seu projeto AEM e prepará-lo para entrar em vigor com o SDK do AEM headless. |
| 8 | [Como executar o aplicativo headless](go-live.md) | Saiba como implantar o aplicativo, obter seu código local no Git e movê-lo do Cloud Manager Git para a pipeline CI/CD. |
| 9 | [Opcional - Como criar aplicativos de página única (SPAs) com o AEM](create-spa.md) | Explore como combinar a entrega headless e headful e saiba como criar SPAs editáveis usando a estrutura de Editor SPA do AEM. |

{style="table-layout:auto"}

## O que vem a seguir {#what-is-next}

Comece conferindo o próximo artigo: [Saiba mais sobre o desenvolvimento headless do CMS](learn-about.md),

### Escolha sua própria aventura {#choose-your-path}

Você prefere aprender em seu próprio ritmo? Confira estas opções:

* Se quiser **saber mais sobre conceitos headless e as tecnologias AEM headless**, continue sua jornada AEM headless, ao revisar, em seguida, o documento [Como modelar seu conteúdo como modelos de conteúdo AEM](model-your-content.md), por meio do qual você aprende a modelar sua estrutura de conteúdo no AEM.
* Se quiser **aprender na prática**, pule para o [Tutorial prático Introdução ao AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=pt-BR), que o levará diretamente ao desenvolvimento AEM Headless, implementando um projeto simples para expor o conteúdo AEM headless.

## Recursos adicionais {#additional-resources}

As jornadas de documentação mostram como o AEM soluciona um problema empresarial fornecendo uma narrativa que o orienta por processos e recursos relacionados. Uma jornada ilustra como vários recursos trabalham juntos para atender a uma única necessidade empresarial.

Confira essas jornadas adicionais para obter mais informações sobre como os eficientes recursos do AEM funcionam juntos.

* O [Portal do Desenvolvedor do AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=pt-BR)
* [Tutoriais do AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=pt-BR) - Se quiser aprender na prática e já tiver conhecimento sobre o AEM, acompanhe nossos tutoriais práticos organizados por API e estrutura, que exploram a criação e o uso de aplicativos do AEM Headless.
* [Jornada de tradução do AEM headless](/help/journey-headless/translation/overview.md) - essa jornada de documentação oferece uma ampla compreensão sobre a tecnologia headless, como o AEM fornece conteúdo headless e como você pode traduzi-lo.
* [Jornada de criação headless](/help/journey-headless/author/overview.md) - comece aqui para obter uma jornada guiada pelos recursos headless avançados e flexíveis do AEM, suas funcionalidades e aprenda a modelar o conteúdo em seu primeiro projeto headless.
* [Jornada do arquiteto headless](/help/journey-headless/architect/overview.md) - comece aqui para obter uma introdução aos recursos headless avançados e flexíveis do Adobe Experience Manager as a Cloud Service e aprender como modelar o conteúdo para seu projeto.
* [Documentação técnica do AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=pt-BR) - Se já possui um conhecimento sólido do AEM e das tecnologias headless, confira nossos documentos técnicos detalhados.
   * [Introdução ao AEM as a Headless CMS](/help/headless/introduction.md)
