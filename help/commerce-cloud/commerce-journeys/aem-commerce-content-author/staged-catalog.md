---
title: Gerenciar experiências de catálogo de produtos preparados
description: Saiba como gerenciar experiências de catálogo de produtos preparados.
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 2%

---

# Criação de experiências de catálogo de produtos em estágios {#building-experiences}

Saiba como gerenciar experiências de catálogo de produtos preparados.

## A História Até Agora {#story-so-far}

No documento anterior da jornada Conteúdo e Comércio da AEM, [Gerenciar páginas e modelos do catálogo de produtos](catalog-templates.md), você aprendeu a gerenciar e criar experiências de catálogo de produtos com base em modelos.

Este artigo tem por base esses fundamentos.

## Objetivo {#objective}

Este documento ajuda você a entender como gerenciar a experiência de catálogo de produtos com base em dados de produto preparados e AEM inicializações. Muitas vezes, os autores têm de preparar em paralelo um lançamento de produto futuro (como uma nova coleção de vestuário). Isso requer acesso aos dados do produto preparados (ainda não ativos) e a capacidade de preparar o conteúdo. Este novo conteúdo será atualizado com o lançamento do produto.

    >[!OBSERVAÇÃO]
    >
    >Este recurso só está disponível com conectores Adobe Commerce ou Cloud Edition e de terceiros que oferecem suporte para autenticação baseada em token. Consulte [Introdução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html) para obter mais informações.

Primeiro, vamos ver como os autores podem acessar dados de produtos preparados com a CIF.

## Trabalhar com dados de produto preparados {#staged-product-data}

Uma maneira de acessar os dados de produtos preparados é usando o cockpit de produtos. Abra o catálogo de produtos clicando no ícone Comércio no menu AEM principal. Isso dará acesso aos dados do produto ao vivo. Abra a guia de filtro à esquerda e expanda **CATÁLOGO PREPARADO**. Com os dados de visualização, agora é possível acessar os dados do produto preparados para qualquer momento. Os dados preparados incluem novas categorias, produtos ou campos atualizados, como preço.

![cockpit de palco](assets/staged-cockpit.png)

Visualizar uma loja com dados preparados é possível usando a visualização de distorção de tempo. Abra o editor e alterne o modo para timewarp. Selecione qualquer data futura. Observe as informações na parte superior do editor de que você está visualizando a página por uma determinada data.

![distorção de tempo do estágio](assets/staged-timewarp.png)

Agora você pode navegar pelo catálogo com os dados preparados. Se você abrir uma página de categoria ou produto preparada, o editor mostrará um indicador visual.

![palco](assets/staged-plp.png)

    >[!OBSERVAÇÃO]
    >
    >O Omnisearch não tem um contexto e, portanto, retornará apenas dados de catálogo de produtos em tempo real

## AEM inicializações {#launches}

AEM Lançamentos permite criar conteúdo para dados de produtos preparados. Se você não estiver familiarizado com Lançamentos, siga o link da documentação sob a [Seção Recursos adicionais](#additional-resources). A Data de lançamento é usada para acessar os dados de produtos preparados.

![lançamento da etapa](assets/staged-launch.png)

Observe que os seletores respeitam a data de lançamento com o indicador de preparo no lado direito.

![seletor de palco](assets/staged-picker.png)

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada, deve:

* entender os conceitos do catálogo de produtos e conteúdo preparados com inicializações
* poder acessar dados do catálogo de produtos preparados por meio do cockpit e do editor de produtos

Agora você está pronto para gerenciar [experiências do produto](product-experience-management.md). No entanto, AEM conteúdo e comércio têm muitas opções adicionais disponíveis. Confira alguns dos recursos adicionais disponíveis no [Seção Recursos adicionais](#additional-resources) para saber mais sobre os recursos que você viu nesta jornada.

## Recursos adicionais {#additional-resources}

* [Cockpit do produto](/help/commerce-cloud/authoring/product-cockpit.md)
* [Introdução](/help/commerce-cloud/getting-started.md)
* [Lançamentos](/help/sites-cloud/authoring/launches/overview.md)
