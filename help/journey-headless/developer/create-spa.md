---
title: Opcional - Como criar aplicativos de página única (SPAs) com o Adobe Experience Manager (AEM)
description: Nesta seção opcional da jornada de desenvolvedor headless do AEM, você aprenderá como o AEM pode combinar a entrega headless com os recursos tradicionais de CMS de pilha completa e como criar SPAs editáveis usando a estrutura do editor de SPA do AEM.
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 100%

---

# Como criar aplicativos de página única (SPAs) com o AEM {#create-spa}

Nesta continuação opcional da [Jornada do desenvolvedor headless do AEM](overview.md), você aprenderá como o AEM pode combinar a entrega headless com os recursos tradicionais de CMS de pilha completa. Você também aprenderá a criar SPAs editáveis usando a estrutura do Editor de SPA do AEM e a integrar SPAs externos, habilitando os recursos de edição conforme necessário.

## A história até agora {#story-so-far}

A esta altura, você deve ter completado toda a [Jornada de desenvolvedor headless do AEM](overview.md) e compreendido as noções básicas de entrega headless no AEM, e deve entender sobre:

* A diferença entre a entrega de conteúdo headless e headful.
* Recursos headless do AEM.
* Como organizar um projeto do AEM Headless.
* Como criar conteúdo headless no AEM.
* Como recuperar e atualizar conteúdo headless no AEM.
* Como ativar um projeto do AEM Headless.

Até o momento, ou você já colocou em prática seu primeiro projeto AEM Headless ou tem o conhecimento necessário para fazê-lo. Parabéns.

Então, por que você está lendo esta continuação adicional e opcional da jornada? Provavelmente você se lembra que na [Introdução](getting-started.md#integration-levels) foi discutido como o AEM não só oferece suporte à entrega headless e aos modelos tradicionais de pilha completa, mas também a modelos híbridos que combinam as vantagens de ambos. Embora não sejam o modelo tradicional headless, esses modelos híbridos podem oferecer uma flexibilidade sem precedentes a certos projetos.

Este artigo amplia seu conhecimento sobre o AEM Headless, explorando em detalhes como criar seus próprios aplicativos de página única (SPAs) editáveis no AEM. Dessa forma, é possível criar conteúdo e enviá-lo através do método headless para um SPA, enquanto esse SPA permanece editável no AEM.

## Objetivo {#objective}

Este documento ajuda você a entender como aplicativos de página única são desenvolvidos usando a estrutura do editor de SPA do AEM. Depois de ler este documento, você deverá:

* Entender a função básica do editor de SPA.
* Saber quais são os requisitos para criar uma SPA totalmente editável para o AEM.
* Entender como SPAs externos podem ser integrados ao AEM.
* Entender como a renderização do lado do servidor pode ou não ser implementada.

## Requisitos e pré-requisitos {#requirements-prerequisites}

Há uma série de requisitos antes de começar a trabalhar com SPAs no AEM.

### Conhecimento {#knowledge}

* Experiência de desenvolvimento na criação de SPAs com estruturas React ou Angular
* Habilidades básicas do AEM para criar fragmentos de conteúdo e usar o editor
* Certifique-se de revisar o documento [Headful e headless no AEM](/help/implementing/developing/headful-headless.md) para compreender os vários níveis de integração de SPA possíveis.

### Ferramentas {#tools}

* Acesso à sandbox para testar a implantação do seu projeto
* Instância de desenvolvimento local para modelagem e teste de dados
* SPAs externos existentes (opcional, dependendo do modelo de integração escolhido)
* Arquétipo de projeto do AEM

## O que é um SPA? {#what-is-a-spa}

Um aplicativo de página única (SPA) é diferente de uma página convencional, no sentido de que ele é renderizado no lado do cliente e orientado principalmente por Javascript, dependendo das chamadas Ajax para carregar dados e atualizar dinamicamente a página. A maior parte, ou todo o conteúdo, é recuperado de uma vez em um único carregamento de página, com recursos adicionais carregados de forma assíncrona, conforme necessário, com base na interação do usuário com a página.

Isso reduz a necessidade de atualizações de página e apresenta uma experiência ao usuário que é contínua, rápida e se parece mais com uma experiência de aplicativo nativo.

O editor de SPA do AEM permite que desenvolvedores de front-end criem SPAs que possam ser integrados a um site do AEM, possibilitando que os autores de conteúdo editem o conteúdo do SPA tão facilmente quanto qualquer outro conteúdo do AEM.

## Por que um SPA? {#why-spa}

Por ser mais rápido, fluido e mais parecido com um aplicativo nativo, o SPA se torna uma experiência atraente. Isso é bom não apenas para o visitante da página da Web, mas também para os profissionais de marketing e desenvolvedores, devido à natureza do funcionamento dos SPAs.

Para obter uma descrição completa dos SPAs e por que usá-los, consulte a seção de [recursos adicionais](#additional-resources) que contém links para uma documentação mais detalhada.

## Como o AEM lida com SPAs

O desenvolvimento de aplicativos de página única no AEM parte do princípio de que o desenvolvedor de front-end segue as práticas recomendadas padronizadas ao criar um SPA. Como desenvolvedor de front-end, se seguir essas práticas gerais recomendadas e alguns princípios específicos do AEM, seu SPA se tornará funcional com o AEM e seus recursos de criação de conteúdo.

* **Portabilidade** - Assim como com qualquer componente, os componentes do SPA devem ser desenvolvidos para serem tão portáteis quanto possível. O SPA deve ser desenvolvido com componentes portáteis e reutilizáveis.
* **AEM controla a estrutura do site** - O desenvolvedor de front-end cria componentes e tem a propriedade de sua estrutura interna, mas depende do AEM para definir a estrutura de conteúdo do site.
* **Renderização dinâmica** - Todas as renderizações devem ser dinâmicas.
* **Roteamento dinâmico** - O SPA é responsável pelo roteamento e o AEM o escuta e realiza buscas com base nele. Qualquer roteamento também deve ser dinâmico.

Para obter uma descrição completa de como o AEM lida com SPAs, consulte a seção de [recursos adicionais](#additional-resources) que fornece links para uma documentação mais detalhada.

## O editor de SPA do AEM {#aem-spa-editor}

Sites criados usando estruturas comuns de SPA, como o React e o Angular, carregam seu conteúdo por meio de JSON dinâmico. Eles não fornecem a estrutura de HTML necessária para que o Editor de páginas do AEM possa colocar controles de edição.

Para habilitar a edição de SPAs no AEM, é necessário um mapeamento entre a saída JSON do SPA e o modelo de conteúdo no repositório do AEM para salvar as alterações no conteúdo.

O suporte ao SPA no AEM introduz uma camada fina de JavaScript que interage com o código JavaScript do SPA quando carregado no Editor de páginas com o qual os eventos podem ser enviados. O local dos controles de edição pode ser ativado para permitir a edição no contexto. Esse recurso se baseia no conceito de ponto de acesso da API de serviços de conteúdo, pois o conteúdo do SPA deve ser carregado por meio dos serviços de conteúdo.

Para obter uma descrição completa do editor de SPA do AEM, consulte a seção de [recursos adicionais](#additional-resources) que fornece links para uma documentação mais detalhada.

## Acomodando SPAs existentes {#existing-spas}

Se você tiver um SPA já existente, o AEM é compatível com sua integração para que ele fique visível para seus autores de conteúdo no Editor do AEM. Esse recurso pode ser útil para visualizar o conteúdo que eles estão criando por meio de fragmentos de conteúdo no contexto do aplicativo final em que ele é consumido.

Além disso, com apenas algumas pequenas alterações, é possível habilitar determinados recursos de edição para o SPA externo no Editor do AEM.

O componente RemotePage permite a renderização de um SPA externo no AEM.

Para obter uma descrição completa de como tornar um SPA externo editável no AEM, consulte a seção de [recursos adicionais](#additional-resources) que fornece links para uma documentação mais detalhada.

## O que vem a seguir {#what-is-next}

Para começar a desenvolver seus próprios SPAs para o AEM, revise os seguintes documentos:

* [Tutorial WKND do SPA](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [Introdução à utilização do React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Introdução à utilização do Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Se precisar adaptar um SPA já existente para usá-lo no AEM, revise os seguintes documentos:

* [O componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)
* [Edição de um SPA externo no AEM](/help/implementing/developing/hybrid/editing-external-spa.md)

Veja abaixo os [recursos adicionais](#additional-resources) que abordam tópicos relacionados a SPA no AEM com mais detalhes.

## Recursos adicionais {#additional-resources}

Veja a seguir alguns recursos adicionais que explicam melhor alguns conceitos mencionados neste documento.

* [Headful e headless no AEM](/help/implementing/developing/headful-headless.md): uma descrição dos diferentes modelos de entrega disponíveis no AEM
* [Introdução e passo a passo do SPA](/help/implementing/developing/hybrid/introduction.md) - Uma boa introdução aos SPAs no AEM.
* [Desenvolvimento de SPAs para o AEM](/help/implementing/developing/hybrid/developing.md): diretrizes sobre como desenvolver SPAs para o AEM
* [Visão geral do editor de SPA](/help/implementing/developing/hybrid/editor-overview.md): detalhes de como o editor de SPA funciona
* [Documentos de referência de SPA](/help/implementing/developing/hybrid/reference-materials.md): referências da API JavaScript e links para projetos de código aberto do GitHub para SPAs do AEM
* [Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments): como criar fragmentos de conteúdo
* [Arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR): modelo do Maven que cria um projeto simples do Adobe Experience Manager (AEM) com base em práticas recomendadas para ser usado como o ponto de partida do seu site
