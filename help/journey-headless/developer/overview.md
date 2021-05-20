---
title: jornada do desenvolvedor sem periféricos do AEM
description: Comece aqui para obter uma jornada guiada com os recursos avançados e flexíveis do AEM, seus recursos e como aproveitá-los em seu primeiro projeto de desenvolvimento.
source-git-commit: 1ac93a066f808e7dd2ed7e34aa7635e9914a4ea9
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 2%

---


# jornada do desenvolvedor sem cabeçalho AEM {#aem-headless-developer-journey}

Comece aqui para obter uma jornada guiada por meio dos recursos avançados e flexíveis sem interface de AEM, seus recursos e como aproveitá-los em seu primeiro projeto de desenvolvimento sem periféricos.

## Introdução {#introduction}

A implementação sem periféricos está se tornando cada vez mais importante para fornecer experiências ao seu público-alvo, onde quer que estejam e independentemente do canal.

A implementação sem cabeçalho perde o gerenciamento de página e componente, como é tradicional em soluções de pilha completa, e se concentra na criação de fragmentos de conteúdo reutilizáveis e neutros em canais e em sua entrega entre canais. É um padrão de desenvolvimento moderno e dinâmico para implementar experiências da Web.

Este guia aborda os tópicos mais importantes para que você, ao concluir:

* Ter uma compreensão completa do que é entrega de conteúdo sem periféricos e de seus benefícios.
* Entenda AEM recursos sem periféricos e como eles trabalham juntos para proporcionar uma experiência sem periféricos.
* Tenha a capacidade de realizar as primeiras etapas de implementação do seu primeiro projeto sem periféricos AEM.

## Público {#audience}

Essa jornada foi projetada para o persona do desenvolvedor, apresentando os requisitos, as etapas e a abordagem de um projeto sem cabeçalho AEM da perspectiva do desenvolvedor. A jornada definirá personas adicionais com as quais o desenvolvedor deve interagir para um projeto bem-sucedido, mas o ponto de vista da jornada é o do desenvolvedor.

As informações nesta jornada podem, é claro, ser úteis para outras pessoas, mas algumas informações serão supérfluas para certas funções. Fique atento às próximas jornadas que abordam outras funções.

## A Jornada do desenvolvedor sem cabeçalho {#the-journey}

Você explorará muitos tópicos nesta jornada. Os artigos a seguir fornecem um conhecimento fundamental da AEM sem cabeça e vinculam-se à documentação técnica detalhada.

Embora seja possível ir diretamente para uma parte específica da jornada, muitos conceitos baseiam-se em artigos anteriores. Portanto, se você é novo em AEM sem periféricos, recomendamos que você comece no início e avance sequencialmente.

| # | Artigo | Descrição |
|---|---|---|
| 0 | jornada do desenvolvedor sem periféricos do AEM | Este documento |
| 1 | [Saiba mais sobre o desenvolvimento sem cabeçalho CMS](learn-about.md) | Saiba mais sobre a tecnologia headless e quando usá-la. |
| 2 | [Introdução ao AEM Headless como um Cloud Service](getting-started.md) | Saiba mais sobre AEM pré-requisitos headless |
| 3 | [Caminho para sua primeira experiência usando AEM headless](path-to-first-experience.md) | Configure seu ambiente de desenvolvimento e saiba como integrar um aplicativo simples com AEM headless |
| 4 | [Como modelar seu conteúdo](model-your-content.md) | Saiba como modelar sua estrutura de conteúdo. Em seguida, perceba essa estrutura do Adobe Experience Manager (AEM) usando Modelos de fragmentos de conteúdo e Fragmentos de conteúdo, para reutilização em canais. |
| 5 | [Como acessar seu conteúdo por meio AEM APIs de entrega](access-your-content.md) | Saiba como usar consultas GraphQL para acessar o conteúdo dos Fragmentos de conteúdo. |
| 6 | [Como atualizar seu conteúdo por meio das APIs do AEM Assets](update-your-content.md) | Saiba como usar a REST API para acessar e atualizar o conteúdo dos Fragmentos de conteúdo. |
| 7 | [Como unir tudo - seu aplicativo e seu conteúdo no AEM Headless](put-it-all-together.md) | Saiba como aceitar seu AEM Project e prepará-lo para entrar em vigor com o AEM Headless SDK. |
| 8 | [Como executar o aplicativo sem periféricos](go-live.md) | Saiba como implantar o aplicativo ao vivo, obter seu código local no Git e movê-lo para o pipeline de Git do Cloud Manager para CI/CD. |
| 9 | [Opcional - Como criar aplicativos de página única (SPA) com AEM](create-spa.md) | Assim que você entender AEM recursos headless, explore como combinar delivery headful e headless e saiba como criar SPA editáveis usando AEM estrutura SPA Editor. |

## O que vem a seguir {#what-is-next}

Agora você está pronto para começar a usar sua jornada sem cabeça do Adobe. Recomendamos que você continue para a próxima parte da jornada e leia o artigo [Saiba mais sobre o desenvolvimento sem cabeçalho do CMS.](learn-about.md)

### Escolha seu próprio empreendimento {#choose-your-path}

No entanto, o Adobe quer que você tenha sucesso à medida que inicia seu projeto sem cabeçalho AEM, independentemente do seu estilo de aprendizagem. Por isso, por favor, considere estas duas opções.

* Se preferir continuar a **aprender sobre conceitos sem interface e AEM tecnologias sem periféricos**, continue sua jornada sem periféricos AEM conforme recomendado ao revisar o documento [Como modelar seu conteúdo como AEM Modelos de conteúdo](model-your-content.md), onde você aprenderá a modelar sua estrutura de conteúdo em AEM.
* Se preferir **aprender ao fazer**, você pode ir para o [Tutorial Introdução AEM mãos sem cabeçalho](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html), onde você irá ir diretamente para AEM desenvolvimento sem cabeçalho implementando um projeto simples para expor AEM conteúdo sem interface.
