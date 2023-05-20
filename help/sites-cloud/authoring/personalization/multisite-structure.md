---
title: Como o gerenciamento multisite para conteúdo direcionado está estruturado
description: Um diagrama mostra como o suporte a vários sites para conteúdo direcionado está estruturado
exl-id: c6b05c2a-0897-4514-8937-e23bfcf757d5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 39%

---

# Como o gerenciamento multisite para conteúdo direcionado está estruturado {#how-multisite-management-for-targeted-content-is-structured}

O diagrama a seguir mostra como o suporte multisite para conteúdo direcionado está estruturado.

As áreas aparecem dentro de **/conteúdo/campanhas/&lt;marca>** e, por padrão, cada marca tem uma área principal, que é criada automaticamente. Cada área contém seu próprio conjunto de atividades, experiências e ofertas.

![Estrutura multisite](/help/sites-cloud/authoring/assets/multisite-structure.png)

Para pesquisar conteúdo direcionado, as páginas ou os sites podem mapear para uma área. Se não houver uma área configurada, o AEM voltará para a área principal dessa marca específica.

O diagrama a seguir é um exemplo de como a lógica funciona para três sites, chamados de site1, site2 e site3.

![Estrutura multisite entre sites](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* site1 procura myarea1 para brand1 e otherarea2 para brand2 com base no area mapping.
* site2 procura myarea1 para brand1 e área principal para brand2 pois somente o mapeamento de área para brand1 é definido.
* site3 procura a área principal para marca1 e marca2 já que nenhum outro mapeamento de área foi definido para este site.
