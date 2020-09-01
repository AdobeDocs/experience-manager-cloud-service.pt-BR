---
title: Limitações do editor
description: O editor na interface habilitada para toque usa sobreposições para interagir com conteúdo confinado em um iframe. Essa interação cria algumas limitações no uso do editor e também para desenvolvedores.
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---


# Limitações do editor {#editor-limitations}

O editor na interface habilitada para toque usa sobreposições para interagir com conteúdo confinado em um iframe. Essa interação cria algumas limitações no uso do editor e também para desenvolvedores. Esta página resume essas limitações e fornece soluções ou soluções alternativas, sempre que possível.

## Limitações funcionais {#functional-limitations}

Um autor pode encontrar as seguintes limitações funcionais ao usar o editor para criar páginas.

### Links não ativos {#links-not-active}

Ao [editar uma página](/help/sites-cloud/authoring/fundamentals/editing-content.md), os links não ficam ativos.

* [Alterne para o modo **de** Pré-visualização](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) para navegar usando os links no seu conteúdo.

### Páginas de estrutura {#structure-pages}

As páginas não podem ser nomeadas `structure`. As páginas nomeadas não `structure` poderão ser editadas no editor de páginas.

## Limitações de CSS {#css-limitations}

Um desenvolvedor pode encontrar as seguintes limitações com as interações do editor com o CSS.

### Elementos totalmente posicionados {#absolutely-positioned-elements}

Elementos com posição absoluta podem causar problemas na posição de sua sobreposição.

* Se isso acontecer, verifique se as dimensões do elemento absolutamente posicionado estão corretas, pois o editor criará uma sobreposição com as mesmas dimensões.

### unidades vh {#vh-units}

`vh` não há suporte para unidades, pois a altura do iframe deve ser automaticamente ajustada por AEM.

### Imagens de plano de fundo fixas {#fixed-background-images}

Imagens de plano de fundo fixas podem não ser exibidas como fixas na rolagem devido ao fato de estarem incorporadas em um iframe.

* Selecionar Página de **Visualização como Publicada** nas ações da barra de cabeçalho exibe a página corretamente.

### 100% Height {#height}

A altura de 100% não é suportada no elemento de corpo de uma página.

* Uma solução alternativa é possível para implementar um corpo em tela cheia &quot;alongando&quot; o elemento body da seguinte forma:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Redução da margem {#margin-collapsing}

Problemas de redução da margem podem ser vistos se o primeiro elemento filho do elemento body tiver uma margem.

* A solução é adicionar uma correção no nível do elemento do corpo, como a seguir:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
