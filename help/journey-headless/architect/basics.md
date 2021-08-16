---
title: Conheça as noções básicas da modelagem de conteúdo
description: Saiba mais sobre a base de modelagem de conteúdo para seu CMS sem cabeçalho usando Fragmentos de conteúdo.
hide: true
hidefromtoc: true
source-git-commit: d0e870f5e49580bb95d347092a2ece4c2497a1c9
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 4%

---


# Saiba mais sobre a modelagem de conteúdo para headless com AEM {#content-modeling-headless-basics}

## A história até agora {#story-so-far}

No início da [AEM Jornada do arquiteto de conteúdo headless](overview.md) a [Introdução](introduction.md) cobria os conceitos básicos e a terminologia relevantes para a modelagem de conteúdo sem periféricos.

Este artigo se baseia neles para que você entenda como modelar o conteúdo para o seu projeto sem periféricos de AEM.

## Objetivo {#objective}

* **Público-alvo**: Iniciante
* **Objetivo**: Apresente os conceitos de modelagem de conteúdo para CMS sem interface.

## Modelagem de conteúdo com modelos de fragmento de conteúdo {#architect-content-fragment-models}

A modelagem de conteúdo (dados) é um conjunto de técnicas estabelecidas, geralmente usadas quando bancos de dados de relacionamento desenvolvidos, portanto, o que a modelagem de conteúdo significa para AEM headless?

### Por quê? {#why}

Para garantir que seu aplicativo possa solicitar e receber o conteúdo necessário de AEM de forma consistente e eficiente, esse conteúdo deve ser estruturado.

Isso significa que o aplicativo sabe antecipadamente a forma de resposta e, portanto, como processá-la. Isso é muito mais fácil do que receber conteúdo de forma livre, que deve ser analisado para determinar o que contém e, portanto, como ele pode ser usado.

### Introdução a Como? {#how}

O AEM usa Fragmentos de conteúdo para fornecer as estruturas necessárias para a entrega sem cabeçalho do conteúdo aos seus aplicativos.

A estrutura do modelo de conteúdo é:

* realizado pela definição do modelo de fragmento de conteúdo,
* usado como base dos Fragmentos de conteúdo usados para a geração de conteúdo.

>[!NOTE]
>
>Os Modelos do Fragmento de conteúdo também são usados como a base dos Esquemas GraphQL de AEM, usados para recuperar o conteúdo - mais sobre isso na Jornada do desenvolvedor.

As solicitações de conteúdo são feitas usando a API GraphQL AEM, uma implementação personalizada da API GraphQL padrão. A API GraphQL AEM permite que os aplicativos executem consultas (complexas) nos Fragmentos de conteúdo, sendo que cada consulta é feita de acordo com um tipo de modelo específico.

O conteúdo retornado pode ser usado pelos seus aplicativos.

## Criar a estrutura com modelos de fragmento de conteúdo {#create-structure-content-fragment-models}

Os Modelos de fragmentos do conteúdo fornecem vários mecanismos que permitem definir a estrutura do conteúdo.

Um Modelo de fragmento de conteúdo descreve uma entidade.

>[!NOTE]
>A funcionalidade Fragmento de conteúdo deve estar ativada no Navegador de configuração para que você possa criar novos modelos.

>[!TIP]
>
>O modelo deve ser nomeado para que o autor de conteúdo saiba qual modelo selecionar ao criar um Fragmento de conteúdo.

Dentro de um modelo:

1. **Os** Tipos de dados permitem definir os atributos individuais.
Por exemplo, defina o campo com o nome de um professor como **Text** e seus anos de serviço como **Number**.
1. Os tipos de dados **Referência de conteúdo** e **Referência de fragmento** permitem criar relacionamentos com outro conteúdo no AEM.
1. O tipo de dados **Referência do fragmento** permite que você atinja vários níveis de estrutura aninhando seus Fragmentos de conteúdo (de acordo com o tipo de modelo). Isso é essencial para a modelagem de conteúdo.

Por exemplo:

![Modelagem de conteúdo com ](assets/headless-modeling-01.png "fragmentos de conteúdoModelagem de conteúdo com fragmentos de conteúdo")

## Tipos de dados {#data-types}

AEM fornece os seguintes tipos de dados para você modelar o conteúdo:

* Texto em linha única
* Texto multilinha
* Número
* Booleano
* Data e hora
* Enumeração
* Tags
* Referência de conteúdo
* Referência do fragmento
* Objeto JSON

>[!NOTE]
>
>Mais detalhes estão disponíveis em Modelos de fragmento de conteúdo - Tipos de dados.

## Referências e conteúdo aninhado {#references-nested-content}

Dois tipos de dados fornecem referências ao conteúdo fora de um fragmento específico:

* ****
Referência de conteúdoFornece uma referência simples a outro conteúdo de qualquer tipo.
Por exemplo, você pode fazer referência a uma imagem em um local especificado.

* **Referência**
de fragmentoFornece referências a outros Fragmentos de conteúdo.
Esse tipo de referência é usado para criar conteúdo aninhado, introduzindo as relações necessárias para modelar seu conteúdo.
O tipo de dados pode ser configurado para permitir que os autores de fragmento:
   * Edite o fragmento referenciado diretamente.
   * Crie um novo fragmento de conteúdo, com base no modelo apropriado

>[!NOTE]
>
>Você também pode criar referências ad hoc usando links dentro de blocos de texto.

## Níveis de estrutura (Fragmentos aninhados) {#levels-of-structure-nested-fragments}

Para modelagem de conteúdo, o tipo de dados **Referência de fragmento** permite criar vários níveis de estrutura e relacionamentos.

Com essa referência, você pode *conectar* vários Modelos de Fragmento de Conteúdo para representar as interrelações. Isso permite que o aplicativo sem periféricos siga as conexões e acesse o conteúdo conforme necessário.

>[!NOTE]
>
>Isso deve ser usado com cautela e a prática recomendada pode ser definida como *aninhar o mais necessário, mas o menos possível*.

As Referências de fragmento fazem exatamente isso - permitem que você faça referência a outro fragmento.

Por exemplo, você pode ter os seguintes Modelos de fragmento de conteúdo definidos:

* Cidade
* Empresa
* Person
* Prêmios

Parece muito simples, mas é claro que uma empresa tem um CEO e funcionários....E estas são todas pessoas, cada uma definida como uma Pessoa.

E uma Pessoa pode ter um Prêmio (ou talvez dois).

* Minha empresa - Empresa
   * CEO - Pessoa
   * Empregado(s) - Pessoa
      * Prêmio(s) Pessoal - Prêmio

E isso é só para começar. Dependendo da complexidade, um prêmio pode ser específico da empresa ou uma empresa pode ter seu escritório principal em uma cidade específica.

A representação dessas interrelações pode ser alcançada com as Referências de fragmento, já que elas são entendidas por você (o arquiteto), pelo autor de conteúdo e pelos aplicativos sem periféricos.

## O que vem a seguir {#whats-next}

Agora que você aprendeu as noções básicas, a próxima etapa é [Saiba mais sobre como Criar modelos de fragmentos de conteúdo em AEM](model-structure.md). Isso introduzirá e discutirá as várias referências disponíveis e como criar níveis de estrutura com as Referências de fragmento - uma parte chave da modelagem para sem periféricos.

## Recursos adicionais {#additional-resources}

* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)

   * [Modelos de fragmentos do conteúdo - Tipos de dados](/help/assets/content-fragments/content-fragments-models.md#data-types)

* [Conceitos de criação](/help/sites-cloud/authoring/getting-started/concepts.md)

* [Manuseio básico](/help/sites-cloud/authoring/getting-started/basic-handling.md)  - esta página é baseada principalmente no console  **** Sites, mas muitos/a maioria dos recursos também são relevantes para a criação de  **Fragmentos** de conteúdo no console  **** Ativos.

* [Trabalho com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md)
