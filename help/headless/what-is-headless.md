---
title: O que é um CMS headless?
description: Saiba mais sobre CMS Headless. Como funcionam? Quais são as alternativas e as diferenças? Por que usar um CMS headless?
exl-id: 53f24f69-ad49-4b8e-9a91-36cd64c1f2b9
feature: Headless
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 100%

---

# O que é um CMS headless? {#what-is-a-headless-cms}

Atualmente, o gerenciamento de conteúdo headless é um desenvolvimento essencial para o design da Web, pois permite dissociar os aplicativos de front-end (do lado do cliente) do back-end (sistema de gerenciamento de conteúdo). Um CMS headless é, portanto, responsável pelos serviços de gerenciamento de conteúdo (back-end), juntamente com os mecanismos que permitem que os aplicativos (front-end) acessem esse conteúdo.

Mas o que o termo realmente significa? Aqui oferecemos uma introdução (muito rápida) aos principais conceitos.

## O que é um sistema de gerenciamento de conteúdo (CMS)? {#content-management-system}

Vamos começar com os conceitos básicos: o que é um sistema de gerenciamento de conteúdo?

Um sistema de gerenciamento de conteúdo (CMS) armazena, gerencia e fornece o conteúdo usado para fornecer suas experiências online.

## CMS tradicional {#traditional-cms}

Tradicionalmente, um CMS inclui a funcionalidade de back-end para armazenamento e entrega de conteúdo, juntamente com a tecnologia de front-end usada para renderizar a marcação para uma experiência que o seu navegador exibirá (a camada de apresentação).

Ele é muito eficiente pois fornece controle total do conteúdo e da formatação, no entanto, não possui toda a flexibilidade necessária para o cenário atual de mudanças rápidas; por exemplo, ao estabelecer uma interface com aplicativos externos.

## CMS headless {#headless-cms}

Agora, com um sistema de gerenciamento de conteúdo headless, o back-end e o front-end são dissociados.

A parte headless representa o back-end de conteúdo, já que um Sistema de gerenciamento de conteúdo (CMS) headless é um sistema exclusivamente back-end, projetado e criado explicitamente como um repositório de conteúdo que torna o conteúdo acessível por meio de uma API, para exibição em qualquer dispositivo.

O front-end, que é desenvolvido e mantido de maneira independente, busca conteúdo do back-end headless usando uma API de entrega de conteúdo, normalmente no formato JSON. Por exemplo, como um aplicativo em React ou Angular (aplicativo de página única (SPA)).

Um CMS headless de back-end geralmente exige que o conteúdo seja estruturado, com base em um modelo ou esquema. Isso auxilia os aplicativos clientes a solicitar o conteúdo correto para renderizar uma experiência. Alguns CMS podem expor conteúdo estruturado e não estruturado no formato JSON.

Uma característica importante dessa topologia é que o conteúdo entregue pelo CMS headless no formato JSON é um conteúdo puro, sem informações de design ou layout. Em uma implementação de CMS headless, toda a formatação e layout são mantidos pelo aplicativo de front-end dissociado.

Uma vantagem importante de uma topologia de CMS headless é a capacidade de reutilizar conteúdo em vários canais, que podem usar diferentes implementações de front-end do lado do cliente. Isso pode tornar o processo de desenvolvimento de front-end mais eficiente. Mas também significa que o processo de desenvolvimento da experiência de front-end pode se tornar muito centrado em código e TI, com essa última tornando-se responsável pela experiência.

## APIs de entrega de conteúdo {#content-delivery-apis}

Um CMS headless pode fornecer uma ou várias maneiras de expor conteúdo aos aplicativos do lado do cliente. Normalmente, APIs REST HTTP, APIs GraphQL ou ambas.

Embora uma API REST possa parecer uma maneira mais fácil de solicitar conteúdo (por exemplo, ao fornecer arquivos JSON para todo o conteúdo que corresponde a um critério), ela normalmente entrega conteúdo em excesso para um aplicativo cliente. Isso pode fazer com que o cliente precise analisar e filtrar o conteúdo realmente necessário para renderizar.

Por outro lado, o GraphQL é um mecanismo mais focado e permite que os aplicativos clientes consultem exatamente o conteúdo necessário para renderizar uma experiência.

## CMS de pilha completa {#fullstack-cms}

Um CMS de pilha completa geralmente representa a topologia tradicional de gerenciamento e entrega de conteúdo, incluindo o back-end de conteúdo e a tecnologia de front-end para renderizar experiências. A entrega de conteúdo em CMS de pilha completa geralmente ocorre por APIs internas de entrega de conteúdo. Geralmente, a funcionalidade de front-end é específica para o CMS de pilha completa. Essa combinação da tecnologia de front-end com o back-end de conteúdo permite a criação de uma experiência “o que você vê é o formato final” (WYSIWYG) como um benefício essencial.

## CMS híbrido {#hybrid-cms}

Uma evolução moderna do CMS de pilha completa pode ser um CMS híbrido. O objetivo é combinar o melhor dos dois mundos:

* o desenvolvimento eficiente de front-end entre canais, utilizando ferramentas modernas de front-end,
* ao mesmo tempo em que mantém a criação de experiência WYSIWYG para capacitar usuários não técnicos e evitar que a TI se torne um obstáculo para o gerenciamento de experiências e conteúdo entre organizações.

Isso é feito adotando estruturas modernas de front-end, como o React, porém mantendo um contato essencial mínimo com o back-end de conteúdo.

## CMS dissociado {#decoupled-cms}

Embora o termo CMS dissociado seja, por vezes, utilizado de forma independente, ele descreve essencialmente um CMS headless de back-end, enfatizando sua característica principal de ser dissociado do aplicativo front-end do lado do cliente.

## CMS headful {#headful-cms}

Esse é outro termo para um CMS tradicional.

## Leitura adicional {#further-reading}

Leia mais sobre como usar o AEM em uma topologia de CMS headless aqui:

* [Introdução ao Adobe Experience Manager as a Headless CMS](/help/headless/introduction.md)
