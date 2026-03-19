---
title: Configuração do seletor de Assets para o editor universal
description: Entenda como configurar o seletor de ativos para uso com o Editor universal.
feature: Developing
role: Admin, Developer
source-git-commit: 0ed57393afaf9af3258dacdcb043487f4a098e03
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 1%

---


# Configuração do seletor de Assets para o editor universal {#configure-assets-selector}

Entenda como configurar o seletor de ativos para uso com o Editor universal.

## Visão geral {#overview}

O Editor Universal usa [o seletor de ativos](/help/assets/overview-asset-selector.md#using-asset-selector) para permitir que os autores naveguem e selecionem ativos para inserção em seu conteúdo.

O seletor de ativos pode ser configurado no Universal Editor com o uso de [&#x200B; filtros de componentes.](/help/implementing/universal-editor/filtering.md) Este documento descreve quais opções de configuração estão disponíveis.

>[!NOTE]
>
>Quando você inicia um projeto do Universal Editor, não há filtros em vigor para o seletor de ativos. Os autores terão acesso a todos os ativos normalmente permitidos pelas permissões do usuário.

## Definição de filtro {#filter-definition}

A definição de filtro do seletor de ativos tem uma estrutura simples.

```json
[
  {
    "id": "assets-filter",
    "assets": {...}
   }
]
```

## Opções de filtro {#filter-options}

O filtro `assets` pode ter as seguintes opções.

* `deliveryTier?`: - Define qual das seguintes camadas de entrega usar:
   * `dm`: Dynamic Media (preferencial) com fallback para `publish`, se necessário
   * `publish`: instância de publicação do AEM
* `repoNames?`: Cadeia de caracteres - Lista de repositórios do AEM que podem ser usados para selecionar imagens.
   * Padrão: todos os repositórios de entrega
* `selectionTier?`: Cadeia de caracteres - Camadas do AEM para selecionar ativos
   * Padrão: `["author", "delivery"]`
* `disableRemote?`: Booleano - Desabilitar suporte a repositório remoto
* `preselectedTypes?`: Cadeia de caracteres - Tipos de arquivo pré-selecionados a serem aplicados como filtro padrão no Seletor de ativos
* `minMaxDimensions?`: Objeto - Fornece dimensões mínimas e/ou máximas (em pixels) a serem aplicadas como filtro padrão no seletor de ativos
   * `widthMin?`: Número - Largura mínima
   * `widthMax?`: Número - Largura máxima
   * `heightMin?`: Número - Altura mínima
   * `heightMax?`: Número - Altura máxima
* `minMaxFileSize?`: Objeto - Forneça o tamanho mínimo e/ou máximo de arquivo (em bytes) a ser aplicado como filtro padrão no seletor de ativos
   * `min?`: Número - Tamanho mínimo do arquivo
   * `max?`: número - Tamanho máximo do arquivo
* `customFileTypeFilters?`: Objeto - Fornece filtros de tipo de arquivo personalizados a serem mostrados no seletor de ativos
   * `label`: Cadeia de caracteres - Rótulo a ser exibido na interface do usuário de seleção de ativos
   * `value`: Cadeia de caracteres - Valor do tipo de arquivo a ser filtrado
* `displayFilters?`: Booleano - Usado para desabilitar a interface do usuário de filtros no seletor de ativos; verdadeiro por padrão

## Exemplo {#example}

O exemplo a seguir contém a maioria das opções para fins de ilustração.

```json
[
  {
    "id": "assets-filter",
    "assets": {
      "deliveryTier": "dm",
      "repoNames": ["thisRepo", "thatRepo"],
      "selectionTier": ["author", "delivery"],
      "disableRemote": true,
      "preselectedTypes": ["png", "svg", "jpg", "gif"],
      "minMaxDimensions": {
        "widthMin": 640,
        "widthMax": 640,
        "heightMin": 480,
        "heightMax": 480
      },
      "minMaxFileSize": {
        "min": 1024,
        "max": 1024
      }
    }
   }
]
```

## Recursos adicionais {#additional-resources}

Para obter detalhes sobre o seletor de ativos, consulte o documento [Seletor de ativos de microfront-end](/help/assets/overview-asset-selector.md#using-asset-selector) na documentação de ativos.
