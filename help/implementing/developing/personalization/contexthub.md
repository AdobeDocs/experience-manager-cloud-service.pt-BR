---
title: ContextHub
description: O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
feature: Developing, Personalization
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# ContextHub {#contexthub}

O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto. Seu recurso principal é oferecer a capacidade de [exibir dados de contexto ao simular e alternar entre várias personalidades](/help/sites-cloud/authoring/personalization/contexthub.md).

O ContextHub permite:

* [Presente, exiba, alterne perfis e simule a experiência do usuário](#presentation) ao criar páginas usando dados de contexto.
* [Mantenha os dados de contexto](#persistence) em seu site como uma representação da camada de dados.
* [Gerenciar segmentos](#segmentation) para o contexto selecionado.

A API do JavaScript do lado do cliente permite acessar os dados para personalizar o conteúdo.

## Apresentação {#presentation}

A [Barra de ferramentas do ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) permite que profissionais de marketing e autores vejam e manipulem dados de armazenamento para simular a experiência do usuário ao criar páginas. A barra de ferramentas consiste em grupos de módulos de interface do usuário que fornecem acesso a [armazenamentos do ContextHub](#persistence), que mantêm os dados do ContextHub no cliente.

Cada módulo da interface do usuário do ContextHub é uma instância de um tipo de módulo predefinido:

* O ContextHub fornece vários [tipos de módulo de amostra](sample-modules.md).
* Use os consoles do AEM para [adicionar módulos de interface](configuring-contexthub.md#adding-a-ui-module) e para [agrupá-los nos modos de interface](configuring-contexthub.md#adding-a-ui-mode).
* Os desenvolvedores podem [criar tipos de módulo personalizados](extending-contexthub.md#creating-contexthub-ui-module-types).

Os desenvolvedores precisam [adicionar o componente ContextHub à página](configuring-contexthub.md).

## Persistência {#persistence}

O ContextHub armazena dados de contexto persistentes no cliente. A API do ContextHub JavaScript permite acessar armazenamentos para criar, atualizar e excluir dados conforme necessário. Dessa forma, o ContextHub representa uma camada de dados em suas páginas.

Cada armazenamento do ContextHub é uma instância de um tipo de armazenamento predefinido:

* O ContextHub fornece vários [tipos de armazenamento de amostra](sample-stores.md).
* Use os consoles do AEM para [criar lojas](configuring-contexthub.md#creating-a-contexthub-store).
* Os desenvolvedores podem [criar tipos de armazenamento personalizados](extending-contexthub.md#creating-custom-store-candidates).
* Os desenvolvedores podem [acessar os dados do armazenamento](adding-contexthub.md#interacting-with-contexthub-stores) por meio do JavaScript.

## Segmentação {#segmentation}

O ContextHub inclui um mecanismo de segmentação que gerencia segmentos e determina quais segmentos são resolvidos para o contexto atual. Vários segmentos estão definidos. Você pode usar a API do JavaScript para [determinar segmentos resolvidos](adding-contexthub.md#determining-resolved-contexthub-segments).
