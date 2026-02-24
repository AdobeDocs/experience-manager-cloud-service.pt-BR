---
title: Análise de fragmentos de conteúdo
description: Entender a estrutura dos fragmentos de conteúdo. Isso fornece informações relevantes para entrega headless e criação de página.
feature: Content Fragments
role: User, Developer
badgeSaas: label="AEM Sites" type="Positive" tooltip="Aplicável ao AEM Sites)."
exl-id: d9268c1a-bfe6-4df7-bad9-6007dd79e0aa
solution: Experience Manager Sites
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 5%

---

# Análise da estrutura do fragmento de conteúdo {#analyzing-content-fragments-structure}

Os Fragmentos de conteúdo foram criados para [entrega headless usando o GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md). Isso significa que eles podem ter uma estrutura de várias camadas.

O Experience Manager (AEM) fornece vários métodos de visualização e análise da estrutura dos fragmentos.

## Referências {#references}

A estrutura de várias camadas é criada usando Referências:

* [Os tipos de dados para Referências são definidos no Modelo de fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* Ao criar, é possível:
   * [Gerenciar essas referências](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [Localizar referências principais do fragmento](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## Árvore de estrutura {#structure-tree}

Abra a guia **Árvore de estrutura** na barra de ferramentas do editor para mostrar a estrutura hierárquica do fragmento de conteúdo e suas referências. Use o ícone de link para abrir referências.

Por exemplo:

![Editor de fragmento de conteúdo - Árvore de estrutura](assets/cf-authoring-structure-tree.png)
