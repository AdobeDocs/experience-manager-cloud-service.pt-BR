---
title: Opcional - Como criar aplicativos de página única (SPA) com AEM
description: Nesta continuação opcional da Jornada de desenvolvedor sem cabeçalho AEM, você aprenderá como AEM pode combinar a entrega sem cabeçalho com os recursos tradicionais de CMS de pilha completa e como criar SPA editáveis usando AEM estrutura SPA Editor.
hide: true
hidefromtoc: true
index: false
translation-type: tm+mt
source-git-commit: 1b6dbf401ff921964537f6c79d12544789e93c92
workflow-type: tm+mt
source-wordcount: '1301'
ht-degree: 0%

---


# Como criar aplicativos de página única (SPA) com AEM {#create-spa}

>[!CAUTION]
>
>TRABALHO EM ANDAMENTO - A criação deste documento está em curso e não deve ser entendida como completa ou definitiva, nem deve ser usada para fins de produção.

Nesta continuação opcional da [AEM Jornada do desenvolvedor sem cabeçalho,](overview.md) você aprenderá como AEM pode combinar a entrega sem periféricos com os recursos tradicionais de CMS de pilha completa e como você pode criar SPA editáveis usando SPA estrutura do editor, bem como integrar SPA externos, habilitando os recursos de edição conforme necessário.

## A história até agora {#story-so-far}

Neste ponto, você deve ter concluído toda a [AEM Jornada de desenvolvedor sem periféricos](overview.md) e entender as noções básicas da entrega sem periféricos no AEM incluindo uma compreensão de:

* A diferença entre a entrega de conteúdo sem periféricos e com periféricos.
* AEM recursos sem periféricos.
* Como organizar e AEM um projeto autônomo.
* Como criar conteúdo sem periféricos no AEM.
* Como recuperar e atualizar o conteúdo sem periféricos no AEM.
* Como participar de um projeto sem cabeçalho AEM.

Então agora você já foi ao vivo com seu primeiro projeto sem Cabeça de AEM ou tem todo o conhecimento que é necessário para isso. Parabéns!

Então por que você está lendo essa continuação adicional e opcional da jornada? Provavelmente, lembre-se de que na [Introdução](getting-started.md#integration-levels) discutimos brevemente como o AEM não só suporta delivery sem interface e modelos de pilha completa tradicionais, como também pode suportar modelos híbridos que combinam as vantagens de ambos. Embora não o modelo tradicional sem cabeça, esses modelos híbridos podem oferecer uma flexibilidade sem precedentes a certos projetos.

Este artigo baseia-se no seu conhecimento do AEM Headless , explorando detalhadamente como você pode criar seus próprios aplicativos de página única (SPA) que são editáveis na AEM. Dessa forma, você pode criar conteúdo e enviá-lo sem interrupções para um SPA, mas esse SPA permanece editável no AEM.

## Objetivo {#objective}

Este documento ajuda você a entender como Aplicativos de página única são desenvolvidos usando a estrutura Editor de SPA AEM. Após ler este documento, você deve:

* Entenda a função básica do Editor de SPA.
* Saiba quais são os requisitos para criar uma SPA totalmente editável para AEM.
* Entenda como o SPA externo pode ser integrado ao AEM.
* Entenda como a renderização do lado do servidor deve ou não ser implementada.

## Requisitos e pré-requisitos {#requirements-prerequisites}

Há vários requisitos antes de começar a trabalhar com SPA no AEM.

### Conhecimento {#knowledge}

* Experiência de desenvolvimento criando SPA com estruturas React ou Angular
* Habilidades básicas de AEM como criar Fragmentos de conteúdo e usar o editor
* Certifique-se de revisar o documento [Headless e Headless em AEM](/help/implementing/developing/headful-headless.md) para entender os vários níveis de integração SPA possível.

### Ferramentas {#tools}

* Acesso ao Sandbox para testar a implantação do seu projeto
* Instância de desenvolvimento local para modelagem e teste de dados
* SPA externos existentes (opcional, dependendo do modelo de integração escolhido)
* Arquétipo de projeto do AEM

## O que é um SPA? {#what-is-a-spa}

Um aplicativo de página única (SPA) é diferente de uma página convencional, na medida em que é renderizado no cliente e é principalmente orientado por Javascript, dependendo das chamadas do Ajax para carregar dados e atualizar dinamicamente a página. A maioria ou todo o conteúdo é recuperado uma vez em um único carregamento de página com recursos adicionais carregados de forma assíncrona, conforme necessário, com base na interação do usuário com a página.

Isso reduz a necessidade de atualizações de página e apresenta uma experiência ao usuário que é contínua, rápida e se parece mais com uma experiência de aplicativo nativo.

O Editor de SPA de AEM permite que desenvolvedores de front-end criem SPA que possam ser integradas a um site de AEM, permitindo que os autores de conteúdo editem o conteúdo de SPA da mesma forma que qualquer outro conteúdo AEM.

## Por que um SPA? {#why-spa}

Ao ser mais rápido, fluido e mais parecido com um aplicativo nativo, um SPA torna-se uma experiência muito atraente não apenas para o visitante da página da Web, mas também para profissionais de marketing e desenvolvedores, devido à natureza de como o SPA funciona.

Para obter uma descrição completa dos SPA e por que usá-los, consulte a seção [recursos adicionais](#additional-resources) para obter links para uma documentação mais detalhada.

## Como o AEM lida com SPA

O desenvolvimento de aplicativos de página única no AEM parte do princípio de que o desenvolvedor front-end cumpre as práticas recomendadas padrão ao criar um SPA. Se, como desenvolvedor front-end, você seguir essas práticas recomendadas gerais, bem como alguns princípios específicos de AEM, seu SPA funcionará com AEM e seus recursos de criação de conteúdo.

* **Portabilidade**  - Assim como com qualquer componente, os componentes do SPA devem ser construídos para serem tão portáteis quanto possível. A SPA deve ser criada com componentes portáveis e reutilizáveis.
* **AEM orienta a estrutura do site**  - o desenvolvedor front-end cria componentes e é proprietário de sua estrutura interna, mas depende do AEM para definir a estrutura de conteúdo do site.
* **Renderização dinâmica**  - Todas as renderizações devem ser dinâmicas.
* **Roteamento dinâmico**  - O SPA é responsável pelo roteamento e AEM o escuta e busca com base nele. Qualquer roteamento também deve ser dinâmico.

Para obter uma descrição completa de como o AEM lida com SPA, consulte a seção [recursos adicionais](#additional-resources) para obter links para uma documentação mais detalhada.

## O Editor de SPA de AEM {#aem-spa-editor}

Os sites criados usando estruturas SPA comuns, como o React e o Angular, carregam seu conteúdo por meio do JSON dinâmico e não fornecem a estrutura HTML necessária para o Editor de página AEM poder colocar controles de edição.

Para habilitar a edição de SPA no AEM, é necessário um mapeamento entre a saída JSON do SPA e o modelo de conteúdo no repositório AEM para salvar as alterações no conteúdo.

SPA suporte no AEM introduz uma fina camada JS que interage com o código JS SPA quando carregado no Editor de páginas com o qual os eventos podem ser enviados e o local dos controles de edição pode ser ativado para permitir a edição no contexto. Esse recurso tem como base o conceito de Ponto de extremidade da API dos serviços de conteúdo , pois o conteúdo do SPA precisa ser carregado por meio dos Serviços de conteúdo.

Para obter uma descrição completa do Editor de SPA de AEM, consulte a seção [recursos adicionais](#additional-resources) para obter links para mais documentação detalhada.

## Acomodando SPA existentes {#existing-spas}

Se você tiver um SPA existente, o AEM suporta a incorporação no AEM para que fique visível para os autores de conteúdo no editor de AEM. Isso pode ser muito útil para visualizar o conteúdo que eles estão criando por meio dos Fragmentos de conteúdo no contexto do aplicativo final, onde ele será consumido.

Além disso, com apenas pequenas alterações, é possível habilitar determinada capacidade de edição para o SPA externo no editor de AEM.

O componente RemotePage permite a renderização de um SPA externo no AEM.

Para obter uma descrição completa de como tornar um SPA externo editável no AEM, consulte a seção [additional resources](#additional-resources) para obter links para uma documentação mais detalhada.

## O que vem a seguir {#what-is-next}

Para começar a desenvolver seu próprio SPA para AEM, reveja os seguintes documentos:

* [Tutorial WKND do SPA](/help/implementing/developing/hybrid/wknd-tutorial.md)
* [Introdução ao React](/help/implementing/developing/hybrid/getting-started-react.md)
* [Introdução ao uso do Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Se precisar adaptar um SPA existente para usá-lo no AEM, revise os seguintes documentos:

* [O componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)
* [Edição de um SPA externo no AEM](/help/implementing/developing/hybrid/editing-external-spa.md)

Veja abaixo os [recursos adicionais](#additional-resources) que podem levá-lo mais a SPA tópicos em AEM.

## Recursos adicionais {#additional-resources}

Veja a seguir alguns recursos adicionais que aprofundam alguns conceitos mencionados neste documento.

* [Headful e Headless no AEM](/help/implementing/developing/headful-headless.md)  - Uma descrição dos diferentes modelos de delivery disponíveis no AEM
* [SPA Introdução e Apresentação.](/help/implementing/developing/hybrid/introduction.md) - Uma boa introdução à SPA em AEM
* [Desenvolvimento de SPA para AEM](/help/implementing/developing/hybrid/developing.md)  - Diretrizes sobre como desenvolver SPA para AEM
* [Visão geral do editor de SPA](/help/implementing/developing/hybrid/editor-overview.md)  - Detalhes de como o editor de SPA funciona
* [Renderização do lado do servidor](/help/implementing/developing/hybrid/ssr.md)  - Como configurar o SSR para AEM SPA
* [SPA Documentos de referência](/help/implementing/developing/hybrid/reference-materials.md)  - Referências da API JavaScript e links para projetos de código aberto AEM SPA GitHub
* [Fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)  - Como criar Fragmentos de conteúdo
* [Arquétipo de projeto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)  - modelo Maven que cria um projeto Adobe Experience Manager (AEM) mínimo, baseado em práticas recomendadas, como ponto de partida para seu site
