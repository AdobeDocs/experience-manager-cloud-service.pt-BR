---
title: Criar componentes
description: AEM componentes são usados para manter, formatar e renderizar o conteúdo disponibilizado nas suas páginas da Web. Siga esta página para saber mais sobre criação de canais e renderização de componentes.
exl-id: a81e812e-29ed-45de-b2d0-1fb0a8c5ce1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 3%

---

# Criar componentes {#creating-components}

AEM componentes são usados para manter, formatar e renderizar o conteúdo disponibilizado nas suas páginas da Web.

## Canais de criação {#authoring-channels}

O canal é o objeto central do conteúdo fornecido para um conjunto de exibições. Portanto, um autor de conteúdo normalmente abriria um canal no editor para adicionar ou modificar o conteúdo. Como o canal é um ***cq:Page*** ele seguirá o mesmo padrão UX tradicional para adicionar e alterar componentes no canal.

No entanto, como os componentes em um canal normalmente são renderizados em tela cheia, a experiência de criação será afetada ao tentar editar componentes únicos ou compor novos pedidos. Portanto, o canal dependerá dos seletores para renderizar diferentes exibições dos componentes. O ambiente de criação aproveitará o seletor de edição para ativar a renderização de canal personalizado.

Por exemplo, `http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html](http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html`

O usuário não precisa adicionar o seletor ao URL durante a edição. Uma lógica do lado do cliente está ouvindo o evento de troca de camada e adiciona o seletor se um canal tiver o tipo de recurso dedicado *telas/núcleo/componentes/canal.*

## Componentes de renderização {#rendering-components}

Para ativar a criação adequada, os componentes precisam fornecer as duas renderizações a seguir:

| **Componente** | **Representações** |
|---|---|
| *my-component/my-component.html* | renderização de produção |
| *my-component/edit.html* | edição da renderização em uma exibição menor |

Os componentes incorporados aproveitam as seguintes categorias da biblioteca do cliente:

| **Componente** | **Biblioteca do cliente** |
|---|---|
| *cq.screens.components.edit* | CSS e JS que devem ser carregados durante a criação |
| *cq.screens.components.production* | CSS e JS que devem ser carregados quando o canal estiver em execução |
| *cq.screens.components* | CSS e JS compartilhados |

>[!NOTE]
>
>Para desenvolver componentes personalizados, use o ***[Modelo de componente de amostra do AEM Screens](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)***.
