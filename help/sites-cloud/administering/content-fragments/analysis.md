---
title: Análise de fragmentos de conteúdo
description: Entenda a estrutura e a entrega de conteúdo dos Fragmentos de conteúdo. Isso fornece informações sobre entrega headless e criação de página.
feature: Content Fragments
role: User, Developer, Architect
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 2%

---


# Análise da estrutura do fragmento de conteúdo {#analyzing-content-fragments-structure}

Os fragmentos de conteúdo foram criados para [Entrega headless usando o GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md). Isso significa que eles podem ter uma estrutura de várias camadas.

O Experience Manager (AEM) fornece vários métodos de visualização e análise da estrutura dos fragmentos.

## Referências {#references}

A estrutura é criada usando Referências:

* [Os tipos de dados para Referências são definidos no Modelo de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* Ao criar, é possível:
   * [Gerenciar essas referências](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [Localizar referências principais do fragmento](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## Árvore de estrutura {#structure-tree}

Abra o **Árvore de estrutura** na barra de ferramentas do editor para mostrar a estrutura hierárquica do fragmento de conteúdo e suas referências. Use o ícone de link para abrir referências.

Por exemplo:

![Editor de fragmento de conteúdo — Árvore de estrutura](assets/cf-authoring-structure-tree.png)