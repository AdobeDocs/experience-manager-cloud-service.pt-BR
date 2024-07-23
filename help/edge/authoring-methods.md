---
title: Escolhendo um Método de Criação
description: Saiba mais sobre considerações importantes ao decidir como você cria seu conteúdo no AEM para ajudá-lo a tomar a melhor decisão para os autores de conteúdo.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 15eef2d3790d1c0cf5414ca55b191de5b644fed0
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Escolhendo um Método de Criação {#authoring-methods}

Saiba mais sobre considerações importantes ao decidir como você cria seu conteúdo no AEM para ajudá-lo a tomar a melhor decisão para os autores de conteúdo.

## Visão geral das considerações {#overview}

A flexibilidade do AEM garante que suas necessidades de criação sejam cobertas, independentemente da escolha de criação baseada em documento ou WYSIWYG. Lembre-se dos fatos a seguir ao iniciar suas considerações.

* **Sempre envolva seus autores de conteúdo na decisão.** - Seus autores de conteúdo são seus especialistas e seu insight é vital.
* **Vários métodos de criação podem ser implementados.** - Embora a Adobe recomende começar de forma simples e escalonar a complexidade conforme a necessidade surgir, vários métodos de criação podem trabalhar juntos em um único projeto.
* **Você sempre pode alterar seu método de criação depois do fato.** - O que quer que você decida que não está preso. A mudança de um método para outro é direta com o auxílio de ferramentas de migração automatizadas Adobe.
* **Você não deve decidir antes da implementação, mas como parte da implementação.** - O AEM é um produto unificado, portanto, essa decisão importante não precisa fazer parte das negociações de contrato. Quando você compra AEM, você tem todos eles. Em vez disso, essa é uma decisão durante a implementação.

O Adobe pode ajudar você a determinar qual método (ou métodos) melhor se adapta aos seus requisitos como parte da implementação.

## Um único tamanho não serve para tudo {#one-size}

Cada implementação do AEM tem seus próprios fluxos de trabalho e metas. Um projeto pode envolver um modelo de criação simples, com autores de conteúdo responsáveis por suas próprias publicações. Já outro pode ter uma rede complexa de contribuidores e aprovações.

![Fluxos de trabalho de criação diferentes](assets/authoring-workflows.png)

Projetos diferentes podem ter casos de uso diferentes (e vários).

![Casos de uso](assets/use-cases.png)

O Adobe entende isso e, portanto, não oferece uma abordagem única para todos. O AEM é a sua solução única que oferece diferentes abordagens para a entrega de conteúdo, bem como para a criação de conteúdo que melhor se adapta às suas necessidades.

Para determinar a melhor abordagem, você precisa considerar quatro itens.

1. [Você tem preferência de entrega de conteúdo?](#content-delivery)
1. [Você tem alguma preferência de criação de conteúdo?](#content-authoring)
1. [Qual é o objetivo do seu projeto?](#project-goals)
1. [Quais desafios de criação você está enfrentando atualmente?](#authoring-challenges)

## Preferências de entrega de conteúdo {#content-delivery}

Sua primeira consideração deve ser como você deseja fornecer seu conteúdo. O Edge Delivery Services oferece sites com velocidade surpreendente, mas talvez seu foco seja a entrega headless. A árvore decisória a seguir pode ajudá-lo a considerar suas opções.

![Árvore de decisão de entrega de conteúdo](assets/content-delivery-decision-tree.png)

Isso pode ajudá-lo a decidir se precisa de:

* [AEM como um CMS headless](/help/headless/introduction.md) usando o Editor de fragmento de conteúdo e/ou o Editor universal.
* AEM Edge Delivery Services usando a [edição baseada em documento](/help/edge/docs/authoring.md) ou a [criação WYSIWYG com o Editor Universal.](/help/edge/wysiwyg-authoring/authoring.md)

## Preferências de criação de conteúdo {#content-authoring}

Sua próxima consideração deve ser como você deseja criar seu conteúdo. A árvore decisória a seguir pode ajudá-lo a considerar suas opções.

![Árvore de decisão de criação de conteúdo](assets/content-authoring-decision-tree.png)

Isso pode ajudá-lo a decidir se precisa de:

* AEM Edge Delivery Services usando a [edição baseada em documento.](/help/edge/docs/authoring.md)
* [Criação WYSIWYG com o Editor universal.](/help/edge/wysiwyg-authoring/authoring.md)

## Objetivos do Projeto {#project-goals}

Como você se parece com o sucesso da criação? Como você define o sucesso do seu projeto?

* Talvez você precise permitir que mais pessoas criem conteúdo, mas queira evitar o treinamento em um novo conjunto de ferramentas. (Pense em criação baseada em documento.)
* Talvez seja necessário aumentar a quantidade de conteúdo gerado. (Pense em criação baseada em documento.)
* Talvez você precise se concentrar no layout de conteúdo visual, mas minimizar a necessidade de codificar o conhecimento. (Considere a criação WYSIWYG.)

Metas de projeto claramente definidas no início da implementação ajudarão você a tomar uma decisão bem informada sobre o método de criação.

## Desafios de criação {#authoring-challenges}

Por fim, considere os desafios específicos que você enfrenta hoje em relação à criação de conteúdo.

* Talvez você enfrente a duplicação de trabalho com conteúdo criado fora do seu CMS, que precisa ser importado ou copiado e colado. (Pense em criação baseada em documento.)
* Talvez seja necessário reduzir o tempo necessário para treinar os autores sobre como usar um CMS. (Pense em criação baseada em documento.)
* Talvez seus autores precisem editar o layout visual do seu conteúdo com frequência, o que requer suporte constante do desenvolvedor. (Considere a criação WYSIWYG.)
