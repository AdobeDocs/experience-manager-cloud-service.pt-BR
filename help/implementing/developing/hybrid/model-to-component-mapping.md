---
title: Modelo dinâmico para mapeamento de componentes para SPA
description: Este artigo descreve como o modelo dinâmico para mapeamento de componentes ocorre no SDK SPA do JavaScript para AEM.
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Modelo dinâmico para mapeamento de componentes para SPA {#dynamic-model-to-component-mapping-for-spas}

Este documento descreve como o modelo dinâmico para mapeamento de componentes ocorre no SDK SPA JavaScript para AEM.

## Módulo ComponentMapping {#componentmapping-module}

A variável `ComponentMapping` O módulo é fornecido como um pacote NPM para o projeto de front-end. Ele armazena componentes de front-end e fornece uma maneira para o Aplicativo de página única mapear componentes de front-end para tipos de recursos de AEM. O módulo permite uma resolução dinâmica de componentes ao analisar o modelo JSON do aplicativo.

Cada item presente no modelo contém um `:type` campo que expõe um tipo de recurso AEM. Quando montado, o componente de front-end pode ser renderizado usando o fragmento de modelo que recebeu das bibliotecas subjacentes.

Consulte [Blueprint SPA](blueprint.md) documento para obter mais informações sobre a análise de modelos e o acesso do componente front-end ao modelo.

Consulte também o pacote npm: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicativo de página única orientado por modelo {#model-driven-single-page-application}

Aplicativos de página única que usam o SDK do SPA do JavaScript para AEM são orientados por modelo:

1. Os componentes de front-end se registram no [Loja de mapeamento de componentes](#componentmapping-module).
1. Em seguida, o [Container](blueprint.md#container), uma vez fornecido um modelo pelo [Provedor de modelo](blueprint.md#the-model-provider), repete o conteúdo do seu modelo (`:items`).

1. Se houver uma página, suas páginas secundárias (`:children`) primeiro obtenha uma classe de componente do [Mapeamento de componentes](blueprint.md#componentmapping) e, em seguida, instanciá-lo.

## Inicialização do aplicativo {#app-initialization}

Cada componente é estendido com os recursos do [`ModelProvider`](blueprint.md#the-model-provider). A inicialização assume a seguinte forma geral:

1. Cada provedor de modelo se inicializa e escuta as alterações feitas na parte do modelo que corresponde ao componente interno.
1. A variável [`PageModelManager`](blueprint.md#pagemodelmanager) deve ser inicializado conforme representado pela variável [fluxo de inicialização](blueprint.md).

1. Depois de armazenado, o gerenciador de modelo de página retorna o modelo completo do aplicativo.
1. Esse modelo é então passado para a raiz do front-end [Container](blueprint.md#container) componente do aplicativo.
1. Partes do modelo são finalmente propagadas para cada componente filho individual.

![Inicialização do modelo de aplicativo](assets/app-model-initialization.png)
