---
title: Saiba mais sobre o conteúdo sem periféricos e como localizar no AEM
description: Aprenda conceitos sem interface, como eles mapeiam para AEM e a teoria AEM localização.
source-git-commit: 22ca7c01bfddb407c119de7d9a4d105941772664
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Saiba mais sobre o conteúdo sem periféricos e como localizar no AEM {#learn-about}

Aprenda conceitos sem interface, como eles mapeiam para AEM e a teoria AEM localização.

## Objetivo {#objective}

Este documento ajuda você a entender a entrega de conteúdo sem periféricos, como o AEM é compatível e como esse conteúdo pode ser localizado. Depois de ler, você deve:

* Entenda os conceitos básicos de entrega de conteúdo sem periféricos.
* Familiarize-se com o suporte AEM sem periféricos e localização.

## Entrega de conteúdo em pilha completa {#full-stack}

Desde o aumento dos sistemas de gerenciamento de conteúdo (CMSs) fáceis de usar e em larga escala, as organizações os aproveitaram como um local central para gerenciar mensagens, identidade visual e comunicações. Usar o CMS como ponto central para administrar experiências melhorou a eficiência, eliminando a necessidade de duplicar tarefas em sistemas diferentes.

![O CMS clássico de pilha completa](/help/journey-headless/developer/assets/full-stack.png)

Em um CMS de pilha completa, toda a funcionalidade de manipulação de conteúdo está no CMS. Os recursos do sistema constituem componentes diferentes da pilha do CMS. A solução de pilha completa tem muitas vantagens.

* Há um sistema para manter.
* O conteúdo é gerenciado centralmente.
* Todos os serviços do sistema estão integrados.
* A criação de conteúdo é contínua.

Portanto, se um novo canal precisar ser adicionado ou se o suporte para novos tipos de experiências for necessário, um (ou mais) novo componente poderá ser inserido na pilha e só há um lugar para fazer alterações.

![Adicionar um novo canal à pilha](/help/journey-headless/developer/assets/adding-channel.png)

A complexidade das dependências na pilha rapidamente se torna aparente, pois outros itens na pilha precisam ser ajustados para acomodar as alterações.

## A Cabeça em Sem Cabeça {#the-head}

O cabeçalho de qualquer sistema é geralmente o renderizador de saída desse sistema, normalmente na forma de uma GUI ou outro resultado gráfico.

Quando falamos de um CMS sem interface, o CMS gerencia o conteúdo e continua a entregá-lo aos consumidores. No entanto, ao fornecer apenas o **content** de forma padronizada, um CMS sem periféricos omita a renderização de saída final, deixando o **presentation** do conteúdo para o serviço de consumo.

![CMS sem periféricos](/help/journey-headless/developer/assets/headless-cms.png)

Os serviços que consomem, sejam experiências de AR, um webshop, experiências móveis, aplicativos web progressivos (PWA), etc., absorvem conteúdo do CMS sem cabeçalho e fornecem sua própria renderização. Eles cuidam de fornecer suas próprias cabeças para o seu conteúdo.

Omitir a cabeça simplifica o CMS ao remover a complexidade. Isso também altera a responsabilidade de renderizar o conteúdo para os serviços que realmente precisam do conteúdo e que geralmente são mais adequados para essa renderização.

## Localização de conteúdo sem cabeçalho no AEM {#localizing-in-aem}

Além de oferecer ferramentas robustas para criar, gerenciar e fornecer páginas da Web tradicionais em pilha completa, o AEM também oferece a capacidade de criar seleções independentes de conteúdo e disponibilizá-las sem interrupções.

O poder do AEM permite que ele forneça conteúdo sem interface, em pilha completa ou em ambos os modelos ao mesmo tempo. Para o especialista em localização, o mesmo conjunto de ferramentas de localização pode ser aplicado a ambos os tipos de conteúdo, fornecendo uma abordagem unificada para a tradução do conteúdo.

## O que vem a seguir {#what-is-next}

Obrigado por começar a sua jornada de localização sem periféricos de AEM! Agora que você leu este documento, deve:

* Entenda os conceitos básicos de entrega de conteúdo sem periféricos.
* Familiarize-se com o suporte AEM sem periféricos e localização.

Aproveite esse conhecimento e continue sua jornada de localização sem periféricos AEM revisando o documento [Comece com AEM localização sem periféricos](getting-started.md), onde você terá uma visão geral de como o AEM gerencia o conteúdo sem periféricos e conhecerá suas ferramentas de localização.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada de localização sem cabeçalho revisando o documento [Introdução a AEM localização sem cabeçalho,](getting-started.md) os seguintes são alguns recursos adicionais opcionais que fazem um mergulho mais profundo em alguns conceitos mencionados neste documento, mas eles não são solicitados a continuar com a jornada sem cabeçalho.

* [MSM e Tradução](/help/sites-cloud/administering/msm-and-translation.md)  - Os detalhes do AEM Multi-Site Manager e como ele funciona com suas ferramentas de tradução
