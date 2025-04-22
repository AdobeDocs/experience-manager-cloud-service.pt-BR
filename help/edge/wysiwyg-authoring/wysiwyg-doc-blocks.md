---
title: Blocos para WYSIWYG e Criação baseada em documento
description: Saiba como criar blocos que podem ser usados para criação no WYSIWYG e em criação baseada em documento.
feature: Edge Delivery Services
role: User
exl-id: f039c70a-e1a0-4fcc-8f42-dfa0f8bb3764
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Blocos para WYSIWYG e Criação baseada em documento {#wysiwyg-and-doc-blocks}

Saiba como criar blocos que podem ser usados para criação no WYSIWYG e em criação baseada em documento.

## Visão geral {#overview}

Em determinados projetos, talvez você queira oferecer suporte à criação do [WYSIWYG usando o Editor Universal](/help/edge/wysiwyg-authoring/authoring.md) e à [criação baseada em documento](/help/edge/docs/authoring.md). Para minimizar o tempo de desenvolvimento e garantir a mesma experiência do site, você pode criar um conjunto de blocos para dar suporte a ambos os casos de uso.

Para fazer isso, você deve usar a mesma abordagem de modelagem de conteúdo para a configuração de criação do WYSIWYG e para a configuração de criação baseada em documento.

## Abordagem {#approach}

Na criação do WYSIWYG no AEM, você [declara um modelo](/help/edge/wysiwyg-authoring/content-modeling.md) e fornece convenções de nomenclatura. Os dados são renderizados em estruturas de bloco semelhantes a tabelas usando o Edge Delivery da mesma forma que se a tabela tivesse sido criada manualmente usando a criação baseada em documento.

Para isso, determinadas suposições são feitas, como para um bloco simples, como um teaser de que todas as propriedades e grupos de propriedades são renderizados em 1.n linhas com uma única coluna cada. Para blocos que têm 1..Em itens (como carrossel e cartões), os itens são anexados após essas linhas, com uma linha cada e uma coluna para cada propriedade/grupo de propriedades.

Se você seguir a mesma abordagem para a criação baseada em documentos, será possível reutilizar os blocos do WYSIWYG.
