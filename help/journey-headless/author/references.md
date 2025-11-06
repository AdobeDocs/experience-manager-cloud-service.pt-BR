---
title: Saiba mais sobre como usar referências em Fragmentos de conteúdo
description: Saiba mais sobre como usar referências em Fragmentos de conteúdo para conteúdo, outros fragmentos e outros ativos (mídia). Apresente a necessidade e a mecânica de fragmentos aninhados para a criação de CMS headless.
exl-id: a65e8a5a-954b-4307-8027-ca8bac5f4261
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 75%

---

# Saiba mais sobre como usar referências em Fragmentos de conteúdo {#author-headless-references}

## A história até agora {#story-so-far}

No início da [Jornada do autor de conteúdo headless do AEM](overview.md), a [Introdução](introduction.md) abordou os conceitos básicos e a terminologia relevante para a criação de conteúdo headless.

Você aprendeu os fundamentos da criação de CMS headless, com uma introdução à autoria com AEMaaCS e, em particular, à autoria de Fragmentos de conteúdo.

Este artigo se baseia nesses itens para que você entenda como usar referências para criar seu próprio conteúdo para seu projeto headless do AEM.

## Objetivo {#objective}

* **Público-alvo**: avançado
* **Objetivo**: introduzir o uso de referências para a Criação de CMS headless. Que tipos de referências estão disponíveis e quais são seus objetivos:

   * Referências do conteúdo
   * Referências de ativo/mídia
   * Referências de fragmento
   * Referências improvisadas em um bloco de texto

## O que são referências {#what-are-references}

As referências são simplesmente um mecanismo para conectar seus recursos, seja outro conteúdo, ativos (como em imagens) ou outros fragmentos. Embora muito parecidas, há algumas diferenças.

Algumas referências têm tipos de dados dedicados (por exemplo, Referências de conteúdo e Referências de fragmento), enquanto outras são simplesmente adicionadas como uma referência em um bloco de texto (referências de ativos e referências improvisadas).

![Fragmentos de conteúdo: referências](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-overview.png)

## Referências de conteúdo {#content-references}

As Referências de conteúdo fazem exatamente isso: permitem que você faça referência a qualquer outro conteúdo. Isso abre um navegador que permite selecionar o item de conteúdo.

Há dois tipos:

* **Referência de conteúdo**
   * especifica o caminho para o recurso referenciado
* **Referência de conteúdo (UUID)**
   * No editor, a referência especifica o caminho para o recurso referenciado; internamente, a referência é mantida como uma ID universalmente exclusiva (UUID) que faz referência ao recurso

## Referências de ativo/mídia {#assets-media-references}

Os ativos (por exemplo, imagens ou mídia) podem ser referenciados em um bloco de texto usando a opção **Inserir ativo**. Isso abre um navegador que permite selecionar o ativo.

![Fragmentos de conteúdo: inserir ativo](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## Referências de fragmento {#fragment-references}

Novamente, as Referências de fragmento fazem exatamente isso, permitem que você faça referência a outro fragmento. Por ser relevante, precisa de um pouco mais de explicação.

Por exemplo, você pode ter os seguintes modelos de fragmento de conteúdo definidos:

* Cidade
* Empresa
* Pessoa
* Prêmios

Parece muito simples, mas uma empresa tem um CEO e funcionários...e todos são definidos como uma Pessoa.

E uma pessoa pode ter um prêmio (ou talvez dois).

* Minha empresa - Empresa
   * CEO - Pessoa
   * Funcionário(s) - Pessoa
      * Prêmios pessoais - Prêmio

E isso é só para começar. Dependendo da complexidade, um prêmio pode ser específico da empresa ou uma empresa pode ter seu escritório principal em uma cidade específica.

A representação dessas inter-relações pode ser alcançada com as Referências de fragmento, já que são entendidas por você (o autor) e pelos aplicativos headless.

Como autor(a), você não é responsável por definir esses relacionamentos (isso é feito por arquitetos(as) de conteúdo ao criar o modelo de fragmento de conteúdo), mas é preciso saber como reconhecer e editar as referências.

Há duas classificações:

* **Referência do fragmento**
   * especifica o caminho para o recurso referenciado
* **Referência de fragmento (UUID)**
   * No editor, a referência especifica o caminho para o recurso referenciado; internamente, a referência é mantida como uma ID universalmente exclusiva (UUID) que faz referência ao recurso

### Como criar fragmentos aninhados {#author-nested-fragment}

A criação de referências de fragmento é bastante direta (embora o campo geralmente não seja rotulado como **Referência de fragmento**). Você pode digitar a referência diretamente ou (mais provavelmente) selecionar o ícone de pasta para abrir um navegador que permita navegar e selecionar o fragmento necessário.

![Fragmentos de conteúdo: referências](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

A definição do Modelo de fragmento de conteúdo controla:

* se você pode optar por adicionar várias referências
* os tipos de modelo de Fragmentos de conteúdo que você pode selecionar; o Modelo de fragmento de conteúdo define os modelos de fragmento permitidos para a referência, de modo que o AEM apresenta apenas fragmentos com base nesses modelos.

### Como navegar pelos fragmentos aninhados {#navigate-nested-fragment}

Com a utilização da guia **Árvore da estrutura** do Editor de fragmento de conteúdo, é possível navegar pelos fragmentos referenciados pelo fragmento e, em seguida, por meio de quaisquer referências que eles possam conter. Selecionar uma referência abre esse fragmento para edição.

![Árvore de estrutura do fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-structure-tree.png)

## Referências ad hoc {#adhoc-references}

Referências improvisadas podem ser adicionadas como um link simples em um bloco de texto:

![Fragmentos de conteúdo: referências ad hoc](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## O que vem a seguir {#whats-next}

Agora que você aprendeu sobre referências e estrutura nos Fragmentos de conteúdo, a próxima etapa é [Saber mais sobre metadados e marcação](metadata-tagging.md). Isso apresentará e discutirá como você pode definir metadados e tags para os Fragmentos de conteúdo.

## Recursos adicionais {#additional-resources}

* [Trabalho com Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)

   * [Gerenciamento dos Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md)

      * [Aplique a configuração à sua pasta de ativos](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder)

      * [Criação de um Fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment)

   * [Criação de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/authoring.md)

   * [Modelos de fragmentos do conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)

      * [Modelos de fragmento de conteúdo - Tipos de dados](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)

      * [Modelos de fragmento de conteúdo: propriedades](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties)

* Guias de introdução
   * [Criação de uma pasta de ativos - Configuração do headless](/help/headless/setup/create-assets-folder.md)

* Jornada do arquiteto de conteúdo do AEM Headless

* Jornada de tradução headless do AEM
