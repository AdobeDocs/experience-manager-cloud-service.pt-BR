---
title: ContextHub
description: O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---


# ContextHub {#contexthub}

O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto. O principal recurso é oferecer a capacidade de [visualização dados de contexto ao simular e alternar entre várias personas.](/help/sites-cloud/authoring/personalization/contexthub.md)

O ContextHub permite:

* [Apresentar, visualização, alternar personas e simular a ](#presentation) experiência do usuário ao criar páginas usando dados de contexto.
* [Persiste os ](#persistence) dados de contexto no seu site como uma representação de camada de dados.
* [Gerenciar ](#segmentation) segmentos para o contexto selecionado.

A API Javascript do cliente permite acessar os dados para personalizar o conteúdo.

## Apresentação {#presentation}

A [barra de ferramentas do ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) permite que comerciantes e autores vejam e manipulem dados de armazenamento para simular a experiência do usuário ao criar páginas. A barra de ferramentas consiste em grupos de módulos de interface que fornecem acesso a [armazenamentos do ContextHub,](#persistence) que persistem nos dados do ContextHub no cliente.

Cada módulo de interface do usuário do ContextHub é uma instância de um tipo de módulo predefinido:

* O ContextHub fornece vários [tipos de módulo de amostra](sample-modules.md).
* Use AEM consoles para [adicionar módulos de interface de usuário](configuring-contexthub.md#adding-a-ui-module) e para [agrupá-los em modos de interface de usuário](configuring-contexthub.md#adding-a-ui-mode).
* Os desenvolvedores podem [criar tipos de módulo personalizados](extending-contexthub.md#creating-contexthub-ui-module-types).

Os desenvolvedores precisam [adicionar o componente ContextHub à página](configuring-contexthub.md).

## Persistência {#persistence}

O ContextHub armazena dados de contexto persistentes no cliente. A API Javascript do ContextHub permite acessar lojas para criar, atualizar e excluir dados, conforme necessário. Dessa forma, o ContextHub representa uma camada de dados em suas páginas.

Cada armazenamento ContextHub é uma instância de um tipo de armazenamento predefinido:

* O ContextHub fornece vários [tipos de armazenamento de amostra](sample-stores.md).
* Use AEM consoles para [criar armazenamentos](configuring-contexthub.md#creating-a-contexthub-store).
* Os desenvolvedores podem [criar tipos de armazenamento personalizados](extending-contexthub.md#creating-custom-store-candidates).
* Os desenvolvedores podem [acessar dados do armazenamento](adding-contexthub.md#interacting-with-contexthub-stores) por meio do Javascript.

## Segmentação {#segmentation}

O ContextHub inclui um mecanismo de segmentação que gerencia segmentos e determina quais segmentos são resolvidos para o contexto atual. Vários segmentos são definidos. Você pode usar a API Javascript para [determinar segmentos resolvidos](adding-contexthub.md#determining-resolved-contexthub-segments).
