---
title: Como o gerenciamento multisite para conteúdo direcionado está estruturado
description: Um diagrama mostra como o suporte multisite para conteúdo direcionado está estruturado
exl-id: c6b05c2a-0897-4514-8937-e23bfcf757d5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 86%

---

# Como o gerenciamento multisite para conteúdo direcionado está estruturado {#how-multisite-management-for-targeted-content-is-structured}

O diagrama a seguir mostra como o suporte multisite para conteúdo direcionado está estruturado.

Áreas aparecem embaixo **/content/campanhas/&lt;brand>** por padrão, cada marca tem uma área principal, que é criada automaticamente. Cada área contém seu próprio conjunto de atividades, experiências e ofertas.

![Estrutura multisite](/help/sites-cloud/authoring/assets/multisite-structure.png)

Para procurar conteúdo direcionado, páginas ou sites podem ser mapeados para uma área. Se não houver nenhuma área configurada, o AEM recuará para a área mestre dessa marca específica.

O diagrama a seguir é um exemplo de como a lógica funciona para três sites, chamados de site1, site2 e site3.

![Estrutura multisite em sites](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* Site1 pesquisa myarea1 em busca de brand1 e otherarea2 em busca de brand2 com base no mapeamento de áreas.
* Site2 pesquisa myarea1 em busca de brand1 e a área mestra em busca de brand2, pois apenas o mapeamento de áreas para brand1 está definido.
* Site3 pesquisa a área mestra para brand1 e brand2, pois nenhum outro mapeamento de área é definido para esse site.
