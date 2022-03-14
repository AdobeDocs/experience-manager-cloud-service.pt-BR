---
title: Limitações do editor
description: O editor na interface habilitada para toque usa as sobreposições para interagir com o conteúdo confinado em um iframe. Essa interação cria algumas limitações no uso do editor e também para desenvolvedores.
exl-id: 6a4f0e43-1076-4da9-95dc-9c5bf83e30d0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 10%

---

# Limitações do editor {#editor-limitations}

O editor na interface habilitada para toque usa as sobreposições para interagir com o conteúdo confinado em um iframe. Essa interação cria algumas limitações no uso do editor e também para desenvolvedores. Esta página resume essas limitações e fornece soluções ou soluções alternativas, sempre que possível.

## Limitações funcionais {#functional-limitations}

Um autor pode encontrar as seguintes limitações funcionais ao usar o editor para criar páginas.

### Links não ativos {#links-not-active}

When [edição de uma página](/help/sites-cloud/authoring/fundamentals/editing-content.md), os links não estão ativos.

* [Mudar para **Visualizar** modo](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) para navegar usando os links no seu conteúdo.

### Páginas da estrutura {#structure-pages}

Páginas não podem ser nomeadas `structure`. Páginas nomeadas `structure` não será editável no editor de páginas.

## Limitações de CSS {#css-limitations}

Um desenvolvedor pode encontrar as seguintes limitações com as interações do editor com o CSS.

### Elementos absolutamente posicionados {#absolutely-positioned-elements}

Elementos totalmente posicionados podem causar problemas na posição de sua sobreposição.

* Se isso acontecer, verifique se as dimensões do elemento absolutamente posicionado estão corretas, pois o editor criará uma sobreposição com as mesmas dimensões.

### unidades vh {#vh-units}

`vh` não há suporte para unidades porque a altura do iframe deve ser ajustada automaticamente pelo AEM.

### Imagens de plano de fundo fixas {#fixed-background-images}

Imagens de plano de fundo fixas podem não ser exibidas como fixas ao rolar devido ao fato de estarem incorporadas a um iframe.

* Selecionar **Exibir página como publicada** nas ações da barra de cabeçalho, a página é exibida corretamente.

### Altura de 100% {#height}

A altura de 100% não é suportada no elemento de corpo de uma página.

* Uma solução alternativa é possível para implementar um corpo em tela cheia &quot;esticando&quot; o elemento do corpo da seguinte maneira:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Redução da Margem {#margin-collapsing}

Problemas de colapso da margem podem ser vistos se o primeiro elemento filho do elemento do corpo tiver uma margem.

* A solução é adicionar uma correção clara no nível do elemento corporal, como a seguir:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
