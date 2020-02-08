---
title: Como o gerenciamento multisite para conteúdo direcionado está estruturado
description: Um diagrama mostra como o suporte multisite para conteúdo direcionado está estruturado
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Como o gerenciamento multisite para conteúdo direcionado está estruturado {#how-multisite-management-for-targeted-content-is-structured}

O diagrama a seguir mostra como o suporte multisite para conteúdo direcionado está estruturado.

Areas appear underneath **/content/campaigns/&lt;brand>** and by default each brand has a master area, which is created automatically. Cada área contém seu próprio conjunto de atividades, experiências e ofertas.

![Estrutura de vários sites](/help/sites-cloud/authoring/assets/multisite-structure.png)

Para procurar conteúdo direcionado, páginas ou sites podem ser mapeados para uma área. Se não houver nenhuma área configurada, o AEM recuará para a área mestre dessa marca específica.

O diagrama a seguir é um exemplo de como a lógica funciona para três sites, chamados de site1, site2 e site3.

![Estrutura de vários sites](/help/sites-cloud/authoring/assets/multisite-structure-2.png)

* Site1 pesquisa myarea1 em busca de brand1 e otherarea2 em busca de brand2 com base no mapeamento de áreas.
* Site2 pesquisa myarea1 em busca de brand1 e a área mestra em busca de brand2, pois apenas o mapeamento de áreas para brand1 está definido.
* Site3 pesquisa a área mestra para brand1 e brand2, pois nenhum outro mapeamento de área é definido para esse site.
