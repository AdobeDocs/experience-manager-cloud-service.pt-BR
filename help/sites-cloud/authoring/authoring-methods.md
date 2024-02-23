---
title: Métodos para criar conteúdo no AEM
description: Saiba mais sobre as diferentes maneiras de criar conteúdo no AEM e como elas são diferentes.
feature: Authoring
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# Métodos para criar conteúdo no AEM {#authoring-methods}

Saiba mais sobre as diferentes maneiras de criar conteúdo no AEM, como eles diferem e quando você pode usar um em vez do outro.

## Flexibilidade de criação no AEM {#authoring-flexibility}

O AEM as a Cloud Service oferece vários editores diferentes para editar diferentes tipos de conteúdo e oferecer suporte a diferentes casos de uso de criação.

* [Editor de página AEM](#page-editor) - Este é o editor clássico para a criação de conteúdo em AEM, testado e confiável para milhares e milhares de sites.
* [Editor de fragmento de conteúdo do AEM](#cf-editor) - Esse é o editor escolhido para criar conteúdo headless.
* [Editor universal](#universal-editor) - Essa interface moderna permite que você crie conteúdo de AEM de forma agnóstica em relação ao conteúdo e é a primeira escolha para projetos de AEM que utilizam Edge Delivery Services.
* [Criação baseada em documento](#document-based) - Se você usar os serviços de Entrega de borda, poderá optar por criar seu conteúdo como documentos convencionais, como o Microsoft Word ou Google Docs, totalmente fora dos consoles AEM.

Devido à natureza integrada e escalável do AEM, esses métodos podem ser usados exclusivamente ou em combinação entre si, dependendo das necessidades do seu projeto.

Consulte o administrador do sistema ou o gerente de projeto se não tiver certeza de quais opções de criação estão disponíveis ou se deseja explorar novas opções para a criação de conteúdo.

## Editor de página AEM {#page-editor}

Este é o editor clássico para a criação de conteúdo em AEM, testado e confiável para milhares e milhares de sites.

![O editor de páginas AEM](assets/authoring-methods-page-editor.png)

O editor de página de AEM apresenta um ambiente integrado para a criação de conteúdo usando uma interface &quot;o que você vê é o que você obtém&quot; (What-You-See-is-What-You-Get, ou WYSIWYG). Arraste e solte componentes predefinidos para criar sua página e editar o conteúdo no local.

Para saber mais sobre o editor de página AEM, consulte o documento [O Editor de páginas AEM.](/help/sites-cloud/authoring/page-editor/introduction.md)

## Editor de fragmento de conteúdo do AEM {#cf-editor}

O editor de fragmento de conteúdo do AEM é o editor preferido para a criação de conteúdo headless.

![O editor de fragmento de conteúdo do AEM](assets/authoring-methods-cf-editor.png)

O editor de fragmento de conteúdo do AEM apresenta uma interface clara para a criação e o gerenciamento de conteúdo estruturado, ideal para entrega headless.

Para saber mais sobre o editor de fragmento de conteúdo do AEM, consulte o documento [Gerenciamento de fragmentos de conteúdo.](/help/assets/content-fragments/content-fragments-managing.md)

## Editor universal {#universal-editor}

O Editor universal é uma interface do usuário moderna que permite criar conteúdo de AEM de maneira independente de conteúdo e é a primeira escolha para projetos de AEM aproveitando Edge Delivery Services.

![O Editor universal](assets/authoring-methods-ue.png)

O Editor universal é acessado por meio do console Sites no AEM, mas oferece a potência e a flexibilidade independente de conteúdo para criar não apenas seu conteúdo AEM, mas também conteúdo externo adequadamente instrumentado.

Para saber mais sobre o Universal Editor, consulte o documento [Criação de conteúdo com o Universal Editor.](/help/implementing/universal-editor/authoring.md)

## Criação baseada em documento {#document-based}

Se você usar os serviços de Entrega de borda, poderá optar por criar seu conteúdo como documentos convencionais, como o Microsoft Word ou Google Docs, totalmente fora do console do AEM.

![Edição de conteúdo baseado em documento](assets/authoring-methods-document.jpg)

Com a criação baseada em documentos, os autores podem usar as ferramentas que já conhecem e ainda se beneficiar da velocidade e do desempenho dos Edge Delivery Services AEM para publicar seu conteúdo. A criação baseada em documentos não requer o uso do console AEM.

Para saber mais sobre a criação baseada em documento, consulte o documento [Criação de conteúdo para Edge Delivery Services.](/help/edge/authoring.md)
