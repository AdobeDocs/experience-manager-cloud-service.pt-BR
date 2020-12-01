---
title: Modelo dinâmico para mapeamento de componentes para SPA
description: Este artigo descreve como o modelo dinâmico para mapeamento de componentes ocorre no Javascript SPA SDK para AEM.
translation-type: tm+mt
source-git-commit: cdd92032c627740c66de7b2f3836fa1dcd2ee2ca
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---


# Modelo dinâmico para mapeamento de componentes para SPA {#dynamic-model-to-component-mapping-for-spas}

Este documento descreve como o modelo dinâmico para mapeamento de componentes ocorre no Javascript SPA SDK para AEM.

## Módulo ComponentMapping {#componentmapping-module}

O módulo `ComponentMapping` é fornecido como um pacote NPM para o projeto front-end. Ele armazena componentes de front-end e fornece uma maneira para o aplicativo de página única mapear componentes de front-end para tipos de recursos AEM. Isso permite uma resolução dinâmica de componentes ao analisar o modelo JSON do aplicativo.

Cada item presente no modelo contém um campo `:type` que expõe um tipo de recurso AEM. Quando montado, o componente front-end pode se renderizar usando o fragmento do modelo recebido das bibliotecas subjacentes.

Consulte o documento [SPA Blueprint](blueprint.md) para obter mais informações sobre a análise do modelo e o acesso do componente de front-end ao modelo.

Consulte também o pacote npm: [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## Aplicativo de página única baseado em modelo {#model-driven-single-page-application}

Aplicativos de página única que usam o Javascript SPA SDK para AEM são orientados por modelo:

1. Os componentes de front-end se registram na [Repositório de Mapeamento de Componentes](#componentmapping-module).
1. Em seguida, o Container [](blueprint.md#container), uma vez fornecido com um modelo pelo [Fornecedor de Modelo](blueprint.md#the-model-provider), repete o conteúdo do modelo (`:items`).

1. No caso de uma página, seus filhos (`:children`) primeiro obtêm uma classe de componente do [Mapeamento de componentes](blueprint.md#componentmapping) e depois a instanciam.

## Inicialização do aplicativo {#app-initialization}

Cada componente é estendido com os recursos de [`ModelProvider`](blueprint.md#the-model-provider). Por conseguinte, a inicialização assume a seguinte forma geral:

1. Cada provedor de modelo se inicializa e escuta as alterações feitas no modelo que corresponde ao seu componente interno.
1. [`PageModelManager`](blueprint.md#pagemodelmanager) deve ser inicializado como representado pelo [fluxo de inicialização](blueprint.md).

1. Depois de armazenado, o gerenciador de modelo de página retorna o modelo completo do aplicativo.
1. Esse modelo é então passado para o componente raiz front-end [Container](blueprint.md#container) do aplicativo.
1. Partes do modelo são finalmente propagadas para cada componente filho individual.

![Inicialização do modelo de aplicativo](assets/app-model-initialization.png)
