---
title: Gerencie experiências de catálogo de produtos em estágios
description: Saiba como gerenciar experiências de catálogo de produtos por etapas.
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
feature: Commerce Integration Framework
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 10%

---

# Criação de experiências de catálogo de produtos em estágios {#building-experiences}

Saiba como gerenciar experiências de catálogo de produtos por etapas.

## A história até agora {#story-so-far}

No documento anterior do Conteúdo do AEM e jornada do Commerce, [Gerenciar páginas e modelos do catálogo de produtos](catalog-templates.md), você aprendeu a gerenciar e criar experiências de catálogo de produtos com base em modelos.

Este artigo se baseia nesses fundamentos.

## Objetivo {#objective}

Este documento ajuda você a entender como gerenciar a experiência do catálogo de produtos com base em dados de produtos preparados e inicializações de AEM. Muitas vezes, os autores precisam preparar em paralelo um lançamento de produto em breve (como uma nova coleção de roupas). Isso requer acesso a dados de produto preparados (ainda não ativados) e a capacidade de preparar o conteúdo. Esse novo conteúdo entrará no ar com o lançamento do produto.

    >[!NOTE]
    >
    >Esse recurso só está disponível com o Adobe Commerce ou Cloud Edition e conectores de terceiros que oferecem suporte à autenticação baseada em token. Consulte [Introdução](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html) para obter mais informações.

Primeiro, vamos ver como os autores podem acessar dados de produtos preparados com CIF.

## Trabalhar com dados de produto por etapas {#staged-product-data}

Uma maneira de acessar dados de produto preparados é usar o cockpit de produtos. Abra o catálogo de produtos clicando no ícone do Commerce no menu principal do AEM. Isso dará acesso aos dados dinâmicos do produto. Abra a guia de filtro à esquerda e expanda **CATÁLOGO PREPARADO**. Usando os dados de visualização, agora é possível acessar os dados de produto preparados para qualquer point-in-time. Os dados preparados incluem novas categorias, produtos ou campos atualizados, como preço.

![cockpit de preparo](assets/staged-cockpit.png)

É possível visualizar uma vitrine com dados preparados usando a visualização do Timewarp. Abra o editor e alterne o modo para timewarp. Selecione qualquer data futura. Observe as informações sobre o editor que você está visualizando a página para uma determinada data.

![estágio do timewarp](assets/staged-timewarp.png)

Agora você pode navegar pelo catálogo com os dados preparados. Se você abrir uma categoria ou página de produto preparada, o editor mostrará um indicador visual.

![plp de estágio](assets/staged-plp.png)

    >[!NOTE]
    >
    >O Omnisearch não tem um contexto e, portanto, retornará apenas dados do catálogo de produtos em tempo real

## Inicializações do AEM {#launches}

Inicializações do AEM permitem criar conteúdo para dados de produtos preparados. Se não estiver familiarizado com o Launches, siga o link da documentação sob o [Seção Recursos adicionais](#additional-resources). A Data de inicialização é usada para acessar dados de produtos preparados.

![inicialização de estágio](assets/staged-launch.png)

Observe que os seletores respeitam a data de lançamento com o indicador preparado no lado direito.

![seletor de estágio](assets/staged-picker.png)

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada, você deve:

* entender os conceitos de catálogo de produtos e conteúdo preparados com o Launches
* ser capaz de acessar dados preparados do catálogo de produtos por meio do cockpit e do editor de produtos

Agora você está pronto para gerenciar o [experiências do produto](product-experience-management.md). No entanto, o Conteúdo AEM e o Commerce têm muitas opções adicionais disponíveis. Confira alguns dos recursos adicionais disponíveis na [seção Recursos adicionais](#additional-resources) para saber mais sobre os recursos que você viu nesta jornada.

## Recursos adicionais {#additional-resources}

* [Cockpit do produto](/help/commerce-cloud/authoring/product-cockpit.md)
* [Introdução](/help/commerce-cloud/getting-started.md)
* [Lançamentos](/help/sites-cloud/authoring/launches/overview.md)
