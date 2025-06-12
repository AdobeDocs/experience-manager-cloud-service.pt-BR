---
title: Métodos para criar conteúdo no AEM
description: Saiba mais sobre as diferentes maneiras de criar conteúdo no AEM e como elas são diferentes.
feature: Authoring
exl-id: ef482843-451b-474e-a8d0-d0bfcc17221b
solution: Experience Manager Sites
role: User
source-git-commit: 9a700e9eb3116252f42bb08db9dadc0e8a6adbf7
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Métodos para criar conteúdo no AEM {#authoring-methods}

Saiba mais sobre as diferentes maneiras de criar conteúdo no AEM, como elas são diferentes e quando você pode usar uma em vez da outra.

## Flexibilidade de criação da AEM {#authoring-flexibility}

O AEM as a Cloud Service oferece vários editores diferentes para editar diferentes tipos de conteúdo e oferecer suporte a diferentes casos de uso de criação.

* [Criação no WYSIWYG usando o Editor Universal](#universal-editor) - O Editor Universal é uma interface moderna que permite a criação de conteúdo no AEM de forma independente de conteúdo e está disponível para projetos do AEM que usam o Edge Delivery Services.
* [Criação no WYSIWYG usando o Editor de páginas](#page-editor) - O Editor de páginas é o editor clássico de criação de conteúdo no AEM, testado e confiável para milhares e milhares de sites.
* [Criação baseada em documentos](#document-based) - Se você usa os serviços do Edge Delivery, pode optar por criar seu conteúdo como documentos convencionais, como o Microsoft Word ou o Google Docs, totalmente fora dos consoles do AEM.
* [Editor de Fragmento de Conteúdo do AEM](#cf-editor) - Este é o editor preferido para a criação de conteúdo headless.

Devido à natureza integrada e escalável do AEM, esses métodos podem ser usados exclusivamente ou em combinação entre si, dependendo das necessidades do seu projeto.

Consulte o administrador do sistema ou o gerente de projeto se não tiver certeza de quais opções de criação estão disponíveis ou se deseja explorar novas opções para a criação de conteúdo.

## Criação no WYSIWYG usando o editor universal {#universal-editor}

O Editor universal é uma interface moderna que permite criar conteúdo do AEM de forma independente de conteúdo e é a primeira opção para projetos do AEM que usam o Edge Delivery Services.

![O Editor universal](assets/authoring-methods-ue.png)

O Editor universal é acessado por meio do console Sites no AEM, mas oferece a potência e a flexibilidade independente de conteúdo para criar não apenas o conteúdo do AEM, mas também conteúdo externo instrumentado corretamente.

Para saber mais sobre o Universal Editor, consulte o documento [Criação de Conteúdo com o Universal Editor](/help/sites-cloud/authoring/universal-editor/authoring.md).

## Criação no WYSIWYG usando o Editor de páginas {#page-editor}

Este é o editor clássico para a criação de conteúdo em projetos tradicionais do AEM, testado e confiável para milhares e milhares de sites.

![O editor de páginas do AEM](assets/authoring-methods-page-editor.png)

O editor de páginas do AEM apresenta um ambiente integrado para a criação de conteúdo usando uma interface &quot;o que você vê é o que você obtém&quot; (WYSIWYG). Arraste e solte componentes predefinidos para criar sua página e editar o conteúdo no local.

Para saber mais sobre o editor de páginas do AEM, consulte o documento [Editor de páginas do AEM](/help/sites-cloud/authoring/page-editor/introduction.md).

## Criação baseada em documento  {#document-based}

Se você usa os serviços do Edge Delivery, pode optar por criar seu conteúdo como documentos convencionais, como o Microsoft Word ou o Google Docs, totalmente fora do console do [AEM **Sites**](/help/sites-cloud/authoring/sites-console/introduction.md).

![Editando conteúdo baseado em documento](assets/authoring-methods-document.jpg)

Com a criação baseada em documentos, os autores podem usar as ferramentas que já conhecem e ainda se beneficiar da velocidade e do desempenho do Edge Delivery Services do AEM para publicar seu conteúdo. A criação baseada em documentos não requer o uso do console AEM.

Para saber mais sobre a criação baseada em documentos, consulte [Criação e publicação de conteúdo](/help/edge/docs/authoring.md).

## Editor de fragmento de conteúdo do AEM {#cf-editor}

O editor de fragmento de conteúdo do AEM é o editor preferido para a criação de conteúdo headless.

![O Editor de Fragmento de Conteúdo do AEM](assets/authoring-methods-cf-editor.png)

O editor de fragmento de conteúdo do AEM apresenta uma interface clara para a criação e o gerenciamento de conteúdo estruturado, ideal para entrega headless.

Para saber mais sobre o editor de fragmento de conteúdo do AEM, consulte os documentos [Gerenciamento de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md) e [Criação de fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md).

>[!NOTE]
>
>O editor *novo* destacado nesta seção não está disponível ao desenvolver localmente para o AEM as a Cloud Service.
>
>O [*original* editor de Fragmento de Conteúdo](/help/assets/content-fragments/content-fragments-variations.md) também está disponível.
