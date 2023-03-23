---
title: Introdução ao Headless para AEM
description: Saiba mais sobre o Headless no Adobe Experience Manager (AEM) com uma combinação de documentações detalhadas e jornadas headless. Saiba como recursos como Modelos de fragmentos de conteúdo, Fragmentos de conteúdo e uma API do GraphQL são usados para potencializar experiências headless.
landing-page-description: Entenda como usar e administrar o Headless no Adobe Experience Manager as a Cloud Service.
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 6d8d75cd0b01154f420dd3d5f14589bb8a2b8297
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 75%

---


# Introdução ao Adobe Experience Manager as a Headless CMS {#introduction-aem-headless}

Saiba como usar o Adobe Experience Manager (AEM) como um CMS sem interface (Sistema de gerenciamento de conteúdo), com recursos como Modelos de fragmentos de conteúdo, Fragmentos de conteúdo e uma API do GraphQL que juntos potencializam as experiências sem periféricos em escala.

Você pode ler a documentação detalhada dos vários recursos envolvidos e/ou seguir a seleção de [jornadas headless para obter uma visão geral dos primeiros passos](#first-steps).

>[!NOTE]
>
>Consulte também [O que é Headless?](/help/headless/what-is-headless.md) para obter uma introdução a conceitos e terminologia sobre headless.

## Visão geral {#overview}

O AEM Headless é uma solução CMS do Experience Manager que permite que o conteúdo estruturado (Fragmentos de conteúdo) no AEM seja consumido por qualquer aplicativo via HTTP, usando GraphQL. As implementações headless permitem a entrega de experiências entre plataformas e canais em escala.

A implementação sem cabeçalho prescinde do gerenciamento de página e componente, como é tradicional em soluções completas e híbridas. Em vez disso, ele se concentra na criação de fragmentos de conteúdo neutros em canais e reutilizáveis e em seu delivery entre canais. É um padrão de desenvolvimento moderno e dinâmico para implementar experiências na web.

![Modelos de implementação do AEM](assets/aem-implementation-models.png)

## Recursos {#aem-headless-features}

O AEM as a Cloud Service é uma ferramenta flexível para o modelo de implementação headless, oferecendo três recursos avançados:

1. **Modelos de fragmentos do conteúdo**
   * Os Modelos de fragmento de conteúdo são representações estruturadas do conteúdo.
   * Os Modelos de fragmento de conteúdo são definidos por arquitetos de informações no editor de Modelo de fragmento de conteúdo AEM.
   * Os Modelos de fragmentos do conteúdo são a base dos Fragmentos do conteúdo.
1. **Fragmentos de conteúdo**
   * Um Fragmento de conteúdo é criado com base em um Modelo de fragmento de conteúdo.
   * Os Fragmentos de conteúdo são criados por autores de conteúdo, usando o editor Fragmento de conteúdo AEM .
   * Os Fragmentos de conteúdo são armazenados como AEM Assets, mas podem ser gerenciados por meio do Console de ativos ou da variável [Console Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/content-fragments-console.md).
1. **API de conteúdo para entrega**
   * A API GraphQL do AEM é compatível com a entrega de fragmentos de conteúdo.
   * A API REST do AEM Assets é compatível com operações CRUD de fragmentos de conteúdo.
   * A entrega direta de conteúdo também é possível com a [exportação em JSON do componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=pt-BR).

## Suas primeiras etapas {#first-steps}

Há vários recursos disponíveis para oferecer uma introdução às funcionalidades headless do AEM. Cada guia é personalizado para diferentes casos de uso e públicos.

| Recurso | Descrição | Tipo | Público | Est. Hora |
|---|---|---|---|---|
| [Jornada de desenvolvedores headless](/help/journey-headless/developer/overview.md) | **Para desenvolvedores novatos no AEM e em tecnologias headless**: comecem aqui para obter uma introdução abrangente ao AEM e seus recursos headless, desde a teoria do headless até a inauguração do seu primeiro projeto headless. | Guia | Desenvolvedores **novatos no AEM e no headless** | 1 hora |
| [Configuração do headless](/help/headless/setup/introduction.md) | **Para usuários experientes do AEM** que precisam de um breve resumo dos principais recursos headless do AEM, confira esta visão geral de início rápido. | Configuração de referência | Desenvolvedores e administradores **com experiência no AEM** | 20 minutos |
| [Tutorial prático do headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=pt-BR) | **Se estiver familiarizado com o AEM e preferir uma abordagem prática**, este tutorial aborda diretamente a implementação de um aplicativo headless simples. | Tutorial | Desenvolvedores | 2 horas |
| [Jornada do arquiteto headless](/help/journey-headless/architect/overview.md) | **Para arquitetos novatos no AEM e em tecnologias headless**: comecem aqui para obter uma introdução aos recursos avançados, flexíveis e headless do Adobe Experience Manager as a Cloud Service e aprender como modelar conteúdo para seu projeto. | Guia | Arquitetos | 1 hora |
| [Jornada de criação headless](/help/journey-headless/author/overview.md) | **Para usuários empresariais novatos no AEM e em tecnologias headless**: comecem aqui para obter uma introdução aos recursos avançados, flexíveis e headless do Adobe Experience Manager as a Cloud Service e aprender como modelar conteúdo para seu projeto. | Guia | Criadores de conteúdo | 1 hora |
| [Jornada de tradução headless](/help/journey-headless/translation/overview.md) | Para os **interessados na abordagem de tradução ao headless do AEM**. Saiba mais sobre tecnologias headless e como criar e atualizar projetos de tradução no AEM, de A a Z. | Guia | Especialistas em tradução | 1 hora |

## Comparação entre headful e headless {#headful-headless}

Este guia tem como foco o modelo completo de implementação headless do AEM. No entanto, “headful ou headless” não precisa ser uma escolha binária no AEM. Os recursos headless podem ser usados para gerenciar e entregar conteúdo a vários pontos de contato, além de permitir que os autores de conteúdo editem aplicativos de página única. Tudo no AEM.

>[!TIP]
>
>Consulte o documento [Headful e Headless no AEM](/help/implementing/developing/headful-headless.md) para obter mais informações.