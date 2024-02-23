---
title: Limitações do editor
description: O editor na interface habilitada para toque usa sobreposições para interagir com o conteúdo confinado em um iframe. Essa interação cria algumas limitações no uso do editor e também para desenvolvedores.
exl-id: 6a4f0e43-1076-4da9-95dc-9c5bf83e30d0
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 6%

---

# Limitações do editor {#editor-limitations}

O editor na interface habilitada para toque usa sobreposições para interagir com o conteúdo confinado em um iframe. Essa interação cria algumas limitações no uso do editor e também para desenvolvedores. Esta página resume essas limitações e fornece soluções ou soluções alternativas, quando possível.

## Limitações funcionais {#functional-limitations}

Um autor pode encontrar as seguintes limitações funcionais ao usar o editor para criar páginas.

### Links não ativos {#links-not-active}

Quando [editar uma página](/help/sites-cloud/authoring/page-editor/edit-content.md), os links não estão ativos.

* [Alternar para **Visualizar** modo](/help/sites-cloud/authoring/page-editor/introduction.md#preview-mode) para navegar usando os links no seu conteúdo.

### Páginas de estrutura {#structure-pages}

Páginas não podem ser nomeadas `structure`. Páginas nomeadas `structure` não serão editáveis no editor de páginas.

## Limitações de CSS {#css-limitations}

Um desenvolvedor pode encontrar as seguintes limitações nas interações do editor com o CSS.

### Elementos posicionados de forma absoluta {#absolutely-positioned-elements}

Elementos posicionados de forma absoluta podem causar problemas na posição da sobreposição.

* Se isso acontecer, verifique se as dimensões do elemento absolutamente posicionado estão corretas, pois o editor criará uma sobreposição com exatamente as mesmas dimensões.

### Unidades de vh {#vh-units}

`vh` unidades não são suportadas porque a altura do iframe deve ser ajustada automaticamente pelo AEM.

### Imagens de fundo fixas {#fixed-background-images}

Imagens de fundo fixas podem não ser exibidas como fixas ao rolar a tela devido ao fato de que elas estão incorporadas em um iframe.

* Selecionar **Exibir página como publicada** nas ações da barra de cabeçalho, o exibe a página corretamente.

### Altura de 100% {#height}

Não há suporte para 100% de altura no elemento de corpo de uma página.

* Uma solução alternativa é possível implementar um corpo de tela cheia &quot;esticando&quot; o elemento do corpo da seguinte maneira:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Recolhimento de margem {#margin-collapsing}

Problemas de recolhimento de margem podem ser vistos se o primeiro elemento filho do elemento body tiver uma margem.

* A solução é adicionar uma correção clara no nível do elemento do corpo, como a seguir:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
