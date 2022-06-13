---
title: O que é um CMS sem periféricos?
description: Saiba mais sobre o CMS sem periféricos. Como funcionam? Quais são as alternativas e as diferenças? Por que você deseja usar um CMS sem cabeçalho?
source-git-commit: 35064ef7d9a4a3f2368667be02b11840b29d56f0
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---


# O que é um CMS sem periféricos? {#what-is-a-headless-cms}

O gerenciamento de conteúdo sem periféricos é um desenvolvimento essencial para o design da Web atual, que dissocia os aplicativos de primeiro plano do lado do cliente do back-end do sistema de gerenciamento de conteúdo. Um CMS sem periféricos é, portanto, responsável pelos serviços de gerenciamento de conteúdo (backend), juntamente com os mecanismos que permitem que os aplicativos (front-end) acessem esse conteúdo.

Mas o que o termo realmente significa? Aqui oferecemos uma introdução (muito rápida) aos principais conceitos.

## O que é um Sistema de Gerenciamento de Conteúdo (CMS)? {#content-management-system}

Vamos começar com os conceitos básicos: o que é um sistema de gerenciamento de conteúdo?

Um sistema de gerenciamento de conteúdo (CMS) armazena, gerencia e fornece o conteúdo usado para fornecer suas experiências online.

## CMS tradicional {#traditional-cms}

Tradicionalmente, um CMS inclui a funcionalidade de back-end para armazenamento e entrega de conteúdo, juntamente com a tecnologia de front-end usada para renderizar a marcação para uma experiência que seu navegador exibirá (a camada de apresentação).

Muito poderoso, fornecendo controle total do conteúdo e da formatação, mas perdendo alguma da flexibilidade necessária no ambiente em rápida mudança atual; por exemplo, ao interligar com aplicativos externos.

## CMS sem periféricos {#headless-cms}

Com um sistema de gerenciamento de conteúdo sem periféricos, o back-end e o front-end agora são dissociados.

A parte sem periféricos é o back-end do conteúdo.

* &quot;*Um sistema de gerenciamento de conteúdo sem periféricos, ou CMS sem periféricos, é um sistema de gerenciamento de conteúdo (CMS) de back-end criado desde o início como um repositório de conteúdo que torna o conteúdo acessível por meio de uma API para exibição em qualquer dispositivo.*

   Consulte [Wikipedia](https://en.wikipedia.org/wiki/Headless_content_management_system).

O front-end, que é desenvolvido e mantido de maneira independente, busca conteúdo do back-end sem periféricos usando uma API de entrega de conteúdo, normalmente no formato JSON. Por exemplo, pode ser como um aplicativo React ou Angular (Aplicativo de página única (SPA)).

Um back-end CMS sem periféricos geralmente requer que o conteúdo seja estruturado, com base em um modelo ou esquema. Isso facilita os aplicativos clientes que solicitam o conteúdo correto para renderizar uma experiência. Alguns CMS podem expor conteúdo estruturado e não estruturado no formato JSON.

Uma característica principal dessa topologia é que o conteúdo servido pelo CMS sem periféricos no formato JSON é puro conteúdo, sem informações de design ou layout. Em uma implementação CMS sem cabeçalho, toda a formatação e layout são mantidos pelo aplicativo de front-end dissociado.

Uma vantagem importante de uma topologia CMS sem periféricos é a capacidade de reutilizar conteúdo em vários canais, que podem usar diferentes implementações de primeiro plano do lado do cliente. Isso pode tornar o processo de desenvolvimento de primeiro plano mais eficiente. Mas também significa que o processo de desenvolvimento de experiência de ponta pode se tornar muito centralizado em código e em TI, com a TI, essencialmente, possuindo a experiência.

## APIs de entrega de conteúdo {#content-delivery-apis}

Um CMS sem periféricos pode fornecer uma ou várias maneiras de expor o conteúdo aos aplicativos do lado do cliente. Mais comumente, APIs REST do HTTP, APIs GraphQL ou ambas.

Embora uma REST API possa parecer uma maneira mais fácil de solicitar conteúdo (por exemplo, fornecendo JSON para todo o conteúdo que corresponde a um critério), normalmente eles fornecem muito conteúdo para um aplicativo cliente. Isso pode resultar na necessidade do cliente analisar e filtrar o conteúdo realmente necessário para renderização.

Por outro lado, GraphQL é um mecanismo mais focado para permitir que aplicativos clientes consultem exatamente o conteúdo necessário para renderizar uma experiência.

## CMS de pilha completa {#fullstack-cms}

Um CMS de pilha completa geralmente representa a topologia tradicional para o gerenciamento e entrega de conteúdo, ao incluir o back-end de conteúdo e a tecnologia de front-end para renderizar experiências. A entrega de conteúdo em CMS de pilha completa geralmente ocorre por APIs internas de entrega de conteúdo. A funcionalidade de primeiro plano é normalmente específica para o CMS de pilha completa. Essa combinação de tecnologia de ponta com back-end de conteúdo permite a criação de experiência com o que você vê é o que você obtém (WYSIWYG) como um benefício essencial.

## CMS híbrido {#hybrid-cms}

Uma evolução moderna do CMS de pilha completa pode ser um CMS híbrido. O objetivo é combinar o melhor dos dois mundos:

* desenvolvimento eficiente de frontend em todos os canais, utilizando ferramentas modernas de frontend,
* ao mesmo tempo em que mantém a criação de experiência WYSIWYG para capacitar usuários não técnicos e evitar que a TI se torne um gargalo para o conteúdo interorganizacional e o gerenciamento de experiências.

Isso é feito ao adotar estruturas modernas de primeiro plano, como o React, mas mantendo um mínimo essencial de combinação com o back-end de conteúdo.

## CMS dissociado {#decoupled-cms}

Embora o termo CMS dissociado seja, por vezes, utilizado de forma independente, descreve essencialmente um back-end CMS sem interface, sublinhando a sua característica principal de ser dissociado do aplicativo front-end do lado do cliente.

## CMS Cabeça {#headful-cms}

Esse é outro termo para um CMS tradicional.

## Leitura adicional {#further-reading}

Leia mais sobre como usar AEM em uma topologia CMS sem periféricos aqui:

* [Introdução ao Adobe Experience Manager as a Headless CMS](/help/headless/introduction.md)
