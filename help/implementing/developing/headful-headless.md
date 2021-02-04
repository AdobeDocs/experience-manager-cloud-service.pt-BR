---
title: Cabeça e Sem Cabeça em AEM
description: AEM projetos podem ser implementados em um modelo sem cabeça, mas a escolha não é binária. AEM a flexibilidade para explorar as vantagens de ambos os modelos em um único projeto.
translation-type: tm+mt
source-git-commit: 772717b7ad3baa17a58e251c128663035eb89931
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---


# Cabeça e Sem Cabeça em AEM {#headful-headless}

Os projetos da Adobe Experience Manager podem ser implementados em modelos com e sem cabeça, mas a escolha não é binária. AEM a flexibilidade para explorar as vantagens de ambos os modelos em um único projeto. Este documento fornece uma visão geral dos diferentes modelos e descreve os níveis de integração SPA.

## Visão geral {#overview}

AEM ferramentas poderosas do oferta para gerenciar a criação de conteúdo e seu delivery em uma única plataforma. Este é um modelo tradicional de gestão de conteúdo &quot;cuidadosa&quot;, onde os autores e desenvolvedores de conteúdo trabalham na mesma plataforma para fornecer as experiências aos consumidores de conteúdo.

AEM também pode ser usado para gerenciar o conteúdo, permitindo que a apresentação e o delivery do conteúdo sejam gerenciados por outra plataforma. Este é o modelo &quot;sem cabeça&quot; de gestão de conteúdo, onde os autores e desenvolvedores de conteúdo trabalham em diferentes plataformas para fornecer experiência aos consumidores de conteúdo.

Mas isso não precisa ser uma escolha binária. AEM uma flexibilidade sem precedentes, permitindo que você explore as vantagens de ambos os modelos para o seu projeto.

![Modelos de implementação AEM](headless/assets/aem-implementation-models.png)

Em um modelo com pilha completa ou cheia, o conteúdo é gerenciado no repositório AEM e AEM componentes com base em Java, HTL etc. são usadas para renderizar o conteúdo da experiência do usuário. Neste modelo, criar o conteúdo, estilizá-lo, apresentá-lo e disponibilizá-lo tudo acontece em AEM.

Em um modelo sem cabeçalho, o conteúdo é gerenciado no repositório AEM, mas é fornecido por APIs como REST e GraphQL para outro sistema para renderizar o conteúdo da experiência do usuário. Neste modelo, o conteúdo é criado em AEM, mas estilizando-o, apresentando-o e distribuindo-o tudo acontece em outra plataforma.

Aplicativos de página única (SPA) são geralmente o destino para o conteúdo entregue impiedosamente por AEM. No entanto, estas SPA não precisam de ser completamente externas à AEM. AEM permite que você decida em que grau seus SPA estão integrados ao AEM. Vejamos um exemplo.

## Exemplo do Web Shop {#web-shop-example}

Digamos que você já tem uma loja de web para sua empresa como SPA. Nele você tem todos os detalhes e imagens do seu produto. Depois, você apresenta AEM para potencializar seus esforços de marketing, como sites promocionais, blogs e conteúdo de campanhas. Como o senhor integra os dois? AEM permite um espectro de opções:

* **Permita que os sistemas funcionem de forma independente.**
* **Forneça à web shop conteúdo limitado da AEM via GraphQL.** O conteúdo pode ser criado por autores em AEM, mas somente visto por meio da SPA da loja da Web.
* **Incorpore a loja da Web SPA em AEM.** O conteúdo pode ser criado pelos autores no AEM e exibido no AEM no contexto da loja da Web, mas não manipulado.
* **Incorpore o SPA da web shop em AEM e ative pontos editáveis.** O conteúdo pode ser criado por autores em AEM e exibido em AEM no contexto da loja da Web, e os autores têm capacidade limitada de manipular o conteúdo da loja da Web SPA dentro do AEM.
* **Incorpore o SPA da loja da Web em AEM e ative zonas inteiras para edição.** O conteúdo pode ser criado por autores em AEM e exibido em AEM no contexto da loja da Web, e os autores têm capacidade limitada de manipular o conteúdo da loja da Web SPA dentro do AEM.

A próxima seção explora esses níveis de integração com mais detalhes.

>[!NOTE]
>
>É claro que você também poderia reimplementar o SPA da web shop como um AEM de funcionamento completo [usando a estrutura AEM SPA Editor.](/help/implementing/developing/hybrid/introduction.md) Se você já tiver AEM e desejar criar uma nova web shop ou outra SPA, este é o método recomendado, mas não está no escopo deste documento.

## Níveis de integração SPA {#integration-levels}

SPA integração se enquadra em um espectro de quatro níveis em AEM.

* **Nível 0: Sem integração**
   * As SPA e AEM existem separadamente e não trocam informações.
   * O conteúdo é criado, gerenciado e entregue de forma independente em dois sistemas separados.
* **Nível 1: Integração do fragmento de conteúdo**
   * [Os ](/help/assets/content-fragments/content-fragments.md) Fragmentos de conteúdo são usados em AEM para criar e gerenciar conteúdo limitado para o SPA.
   * O SPA recupera este conteúdo por meio AEM [API do GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Alguns conteúdos são gerenciados em AEM e outros em um sistema externo.
   * O conteúdo só pode ser exibido no SPA.
* **Nível 2: Incorporar o SPA no AEM**
   * [Os ](/help/assets/content-fragments/content-fragments.md) Fragmentos de conteúdo são usados em AEM para criar e gerenciar conteúdo para o SPA.
   * O SPA recupera este conteúdo por meio AEM [API do GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * Alguns conteúdos são gerenciados em AEM e outros em um sistema externo.
   * O conteúdo pode ser visualizado em contexto dentro do AEM.
   * O conteúdo limitado pode ser editado no AEM.
* **Nível 3: Incorporar e habilitar totalmente SPA em AEM**
   * [Os ](/help/assets/content-fragments/content-fragments.md) Fragmentos de conteúdo são usados em AEM para criar e gerenciar conteúdo para o SPA.
   * O SPA recupera este conteúdo por meio AEM [API do GraphQL.](/help/assets/content-fragments/graphql-api-content-fragments.md)
   * O conteúdo pode ser visualizado em contexto dentro do AEM.
   * A maioria do conteúdo pode ser editada dentro do AEM.

O Nível 1 é um exemplo de uma implementação sem cabeçalho típica. No entanto, os autores de conteúdo só podem visualização seu conteúdo no contexto no SPA. AEM é apenas uma ferramenta de criação.

A vantagem e a flexibilidade da AEM tornam-se evidentes com os níveis 2 e 3, mantendo as vantagens da SPA. Os autores de conteúdo podem criar seu conteúdo em AEM, mas também visualizá-lo em contexto dentro de AEM. O SPA ganha a capacidade de ser criado em AEM, mas ainda pode ser entregue como um SPA.

## Implementação dos níveis de integração {#implementing}

Há diferentes ferramentas AEM disponíveis, dependendo do nível de integração escolhido. Cada nível baseia-se nas ferramentas usadas no anterior. A lista a seguir está vinculada aos recursos relevantes.

* **Nível 1:Fragmentos** de conteúdo e a  [AEM ](/help/implementing/developing/headless/introduction.md) estrutura sem cabeçalho podem ser usados para fornecer conteúdo AEM ao SPA.
* **Nível 2:** Além do nível 1:
   * [O ](/help/implementing/developing/hybrid/remote-page.md) componente RemotePage pode ser usado para incorporar o SPA externo ao AEM, onde AEM conteúdo pode ser exibido no contexto.
   * Alguns pontos no SPA também podem ser habilitados para [permitir a edição limitada em AEM.](/help/implementing/developing/hybrid/editing-external-spa.md)
* **Nível 3:** Além do nível 2:
   * Zonas inteiras do SPA podem ser habilitadas para permitir uma edição abrangente no AEM.
