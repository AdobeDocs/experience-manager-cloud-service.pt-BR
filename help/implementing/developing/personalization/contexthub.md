---
title: ContextHub
description: O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# ContextHub {#contexthub}

O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto. O principal recurso é oferecer a capacidade de [exibir dados de contexto ao simular e alternar entre várias personas.](/help/sites-cloud/authoring/personalization/contexthub.md)

O ContextHub permite:

* [Apresentar, exibir, alternar personas e simular a experiência do usuário](#presentation) ao criar páginas usando dados de contexto.
* [Manter dados de contexto](#persistence) no seu site como uma representação de camada de dados.
* [Gerenciar segmentos](#segmentation) para o contexto selecionado.

A API Javascript do lado do cliente permite acessar os dados para personalizar o conteúdo.

## Apresentação {#presentation}

O [Barra de ferramentas do ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) permite que profissionais de marketing e autores vejam e manipulem dados de armazenamento para simular a experiência do usuário ao criar páginas. A barra de ferramentas consiste em grupos de módulos de interface que fornecem acesso a [armazenamentos do ContextHub,](#persistence) que persistem dados do ContextHub no cliente.

Cada módulo do ContextHub UI é uma instância de um tipo de módulo predefinido:

* O ContextHub fornece vários [tipos de módulos de amostra](sample-modules.md).
* Use AEM consoles para [adicionar módulos de interface](configuring-contexthub.md#adding-a-ui-module)e para [agrupá-los em modos de interface do usuário](configuring-contexthub.md#adding-a-ui-mode).
* Os desenvolvedores podem [criar tipos de módulo personalizados](extending-contexthub.md#creating-contexthub-ui-module-types).

Os desenvolvedores precisam [adicionar o componente ContextHub à página](configuring-contexthub.md).

## Persistência {#persistence}

O ContextHub armazena dados de contexto persistentes no cliente. A API Javascript do ContextHub permite acessar armazenamentos para criar, atualizar e excluir dados, conforme necessário. Dessa forma, o ContextHub representa uma camada de dados nas páginas.

Cada armazenamento do ContextHub é uma instância de um tipo de armazenamento predefinido:

* O ContextHub fornece vários [tipos de armazenamento de exemplo](sample-stores.md).
* Use AEM consoles para [criar lojas](configuring-contexthub.md#creating-a-contexthub-store).
* Os desenvolvedores podem [criar tipos de loja personalizada](extending-contexthub.md#creating-custom-store-candidates).
* Os desenvolvedores podem [acessar dados do armazenamento](adding-contexthub.md#interacting-with-contexthub-stores) via Javascript.

## Segmentação {#segmentation}

O ContextHub inclui um mecanismo de segmentação que gerencia segmentos e determina quais segmentos são resolvidos para o contexto atual. Vários segmentos são definidos. Você pode usar a API do Javascript para [determinar segmentos resolvidos](adding-contexthub.md#determining-resolved-contexthub-segments).
