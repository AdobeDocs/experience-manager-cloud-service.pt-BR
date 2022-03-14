---
title: Modelo dinâmico para mapeamento de componentes para SPA
description: Este artigo descreve como o modelo dinâmico para mapeamento de componentes ocorre no Javascript SPA SDK for AEM.
exl-id: 3a7b3f26-4a09-40c1-af03-bb8408a68e57
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Modelo dinâmico para mapeamento de componentes para SPA {#dynamic-model-to-component-mapping-for-spas}

Este documento descreve como o modelo dinâmico para mapeamento de componentes ocorre no Javascript SPA SDK for AEM.

## Módulo ComponentMapping {#componentmapping-module}

O `ComponentMapping` é fornecido como um pacote NPM para o projeto front-end. Ele armazena componentes de front-end e fornece uma maneira de o Aplicativo de página única mapear componentes de front-end para AEM tipos de recursos. Isso permite uma resolução dinâmica de componentes ao analisar o modelo JSON do aplicativo.

Cada item presente no modelo contém um `:type` que expõe um tipo de recurso AEM. Quando montado, o componente de front-end pode se renderizar usando o fragmento de modelo recebido das bibliotecas subjacentes.

Consulte a [SPA Blueprint](blueprint.md) documento para obter mais informações sobre a análise do modelo e o acesso do componente de front-end ao modelo.

Consulte também o pacote npm: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicativo de página única orientado por modelo {#model-driven-single-page-application}

Aplicativos de página única que usam o Javascript SPA SDK para AEM são orientados por modelo:

1. Os componentes de front-end se registram no [Armazenamento de mapeamento de componentes](#componentmapping-module).
1. Em seguida, [Contêiner](blueprint.md#container), uma vez fornecido com um modelo pela [Provedor de Modelo](blueprint.md#the-model-provider), repete o conteúdo do modelo (`:items`).

1. No caso de uma página, seus filhos (`:children`) primeiro obtenha uma classe de componente do [Mapeamento de componentes](blueprint.md#componentmapping) e depois instancie-o.

## Inicialização do aplicativo {#app-initialization}

Cada componente é estendido com os recursos do [`ModelProvider`](blueprint.md#the-model-provider). Por conseguinte, a inicialização assume a seguinte forma geral:

1. Cada provedor de modelo inicializa-se e escuta alterações feitas no modelo que corresponde ao seu componente interno.
1. O [`PageModelManager`](blueprint.md#pagemodelmanager) deve ser inicializado, representado pelo [fluxo de inicialização](blueprint.md).

1. Depois de armazenado, o gerenciador de modelo de página retorna o modelo completo do aplicativo.
1. Esse modelo é então passado para a raiz de front-end [Contêiner](blueprint.md#container) componente do aplicativo.
1. Partes do modelo são finalmente propagadas para cada componente filho individual.

![Inicialização do modelo de aplicativo](assets/app-model-initialization.png)
