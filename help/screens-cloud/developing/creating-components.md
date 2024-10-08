---
title: Criar componentes
description: Os componentes do AEM são usados para reter, formatar e renderizar o conteúdo disponibilizado em suas páginas da Web. Siga esta página para saber mais sobre a criação de canais e a renderização de componentes.
exl-id: a81e812e-29ed-45de-b2d0-1fb0a8c5ce1a
feature: Developing Screens
role: Admin, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 3%

---

# Criar componentes {#creating-components}

Os componentes do AEM são usados para reter, formatar e renderizar o conteúdo disponibilizado em suas páginas da Web.

## Criação de canais {#authoring-channels}

O canal é o objeto central do conteúdo entregue a um conjunto de exibições. Portanto, um autor de conteúdo normalmente abriria um canal no editor para adicionar ou modificar conteúdo. Como o Canal é um ***cq:Page***, ele seguirá o mesmo padrão de UX tradicional para adicionar e alterar componentes no canal.

No entanto, como os componentes em um canal normalmente são renderizados em tela cheia, a experiência de criação sofrerá ao tentar editar componentes únicos ou compor novos pedidos. Portanto, o canal dependerá de seletores para renderizar diferentes visualizações dos componentes. O ambiente de criação usa o seletor de edição para ativar a renderização do canal personalizado.

Por exemplo, `http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html](http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html`

O usuário não precisa cuidar da adição do seletor ao URL durante a edição. Uma lógica do lado do cliente está escutando o evento de troca de camada e adiciona o seletor se o canal tiver o tipo de recurso dedicado *telas/núcleo/componentes/canal.*

## Componentes de renderização {#rendering-components}

Para ativar a criação adequada, os componentes precisam fornecer as duas renderizações a seguir:

| **Componente** | **Representações** |
|---|---|
| *my-component/my-component.html* | renderização de produção |
| *my-component/edit.html* | edição da renderização em uma exibição menor |

Os componentes integrados usam as seguintes categorias de bibliotecas de clientes:

| **Componente** | **Biblioteca do cliente** |
|---|---|
| *cq.screens.components.edit* | CSS e JS que devem ser carregados durante a criação |
| *cq.screens.components.production* | CSS e JS que devem ser carregados quando o canal estiver em execução |
| *cq.screens.components* | CSS e JS compartilhados |

>[!NOTE]
>
>Para desenvolver componentes personalizados, use o ***[modelo de componente de amostra do AEM Screens](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)***.
