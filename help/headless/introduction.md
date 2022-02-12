---
title: Introdução ao AEM headless
description: Adobe Experience Manager (AEM) Recursos de autoajuda headless e links de documentação. Saiba como recursos como Modelos de conteúdo, Fragmentos de conteúdo e uma API GraphQL são usados para potencializar experiências headless com AEM.
landing-page-description: Entenda como usar e administrar o Experience Manager Headless as a Cloud Service.
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---


# Introdução ao Adobe Experience Manager Headless  {#introduction-aem-headless}

Saiba como os recursos do Adobe Experience Manager (AEM) como Modelos de conteúdo, Fragmentos de conteúdo e uma API GraphQL são usados para potencializar experiências sem interface em escala.

## Visão geral {#overview}

AEM Headless é uma solução CMS do Experience Manager que permite que o conteúdo estruturado (Fragmentos de conteúdo) no AEM seja consumido por qualquer aplicativo via HTTP usando GraphQL. As implementações headless permitem a entrega de experiências em plataformas e canais em escala.

A implementação sem cabeçalho perde o gerenciamento de página e componente, como é tradicional em soluções de pilha completa e híbridas, e se concentra na criação de fragmentos de conteúdo neutros em canais e reutilizáveis, além de seu delivery entre canais. É um padrão de desenvolvimento moderno e dinâmico para implementar experiências da Web.

![Modelos de implementação de AEM](assets/aem-implementation-models.png)

## Recursos de AEM sem periféricos {#aem-headless-features}

AEM as a Cloud Service é uma ferramenta flexível para o modelo de implementação sem periféricos, oferecendo três recursos avançados:

1. **Modelos de conteúdo**
   * Os Modelos de conteúdo são representação estruturada do conteúdo.
   * Os Modelos de conteúdo são definidos pelos arquitetos de informações no editor do Modelo de fragmento de conteúdo AEM.
   * Os Modelos de conteúdo são a base dos Fragmentos de conteúdo.
1. **Fragmentos de conteúdo**
   * Os Fragmentos de conteúdo são criados com base em um Modelo de conteúdo.
   * Criado por autores de conteúdo por meio do editor AEM Fragmento de conteúdo .
   * Os Fragmentos de conteúdo são armazenados no AEM Assets e gerenciados na interface do usuário de administração do Assets.
1. **API de conteúdo para entrega**
   * A API GraphQL da AEM é compatível com a entrega de Fragmento de conteúdo.
   * A API REST do AEM Assets suporta operações CRUD de Fragmento de conteúdo.
   * A entrega de conteúdo direto também é possível com a variável [Exportação JSON do Componente principal do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html).

## Seus primeiros passos com AEM headless {#first-steps}

Há vários recursos disponíveis para começar a usar AEM recursos sem periféricos. Cada guia é personalizado para diferentes casos de uso e públicos-alvo.

| Recurso | Descrição | Tipo | Público | Est. Hora |
|---|---|---|---|---|
| [Jornada de desenvolvedores headless](/help/journey-headless/developer/overview.md) | **Para desenvolvedores novos em AEM e sem periféricos** tecnologias, comece aqui para obter uma introdução abrangente ao AEM e seus recursos sem periféricos da teoria dos sem periféricos passando a funcionar com seu primeiro projeto sem periféricos. | Guia | Desenvolvedores **novo no AEM e sem periféricos** | 1 hora |
| [Configuração Sem Cabeça](/help/headless/setup/introduction.md) | **Para usuários de AEM experientes** que precisam de um breve resumo dos principais recursos AEM sem periféricos, confira esta visão geral de início rápido. | Configuração de referência | Desenvolvedores, administradores **com AEM experiência** | 20 minutos |
| [Tutorial prático sem cabeçalho](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Se preferir uma abordagem prática e estiver familiarizado com AEM**, este tutorial mergulha diretamente na implementação de um aplicativo sem cabeçalho simples. | Tutorial | Desenvolvedores | 2 horas |
| [Jornada de arquitetura headless](/help/journey-headless/architect/overview.md) | **Para arquitetos novos em AEM e sem periféricos** tecnologias, comece aqui para obter uma introdução aos recursos avançados, flexíveis e sem periféricos do Adobe Experience Manager as a Cloud Service e como modelar o conteúdo para seu projeto. | Guia | Arquitetos | 1 hora |
| [Jornada de criação sem cabeçalho](/help/journey-headless/author/overview.md) | **Para usuários empresariais novos em AEM e sem periféricos** tecnologias, comece aqui para obter uma introdução aos recursos avançados, flexíveis e sem periféricos do Adobe Experience Manager as a Cloud Service e como modelar o conteúdo para seu projeto. | Guia | Criadores de conteúdo | 1 hora |
| [Jornada de tradução headless](/help/journey-headless/translation/overview.md) | Para aqueles **interessado em AEM abordagem de tradução para o headless**. Saiba mais sobre tecnologias sem periféricos e como criar e atualizar projetos de tradução em AEM de A a Z. | Guia | Especialistas em tradução | 1 hora |

## Comparação entre headful e headless {#headful-headless}

Este guia tem como foco o modelo completo de implementação sem cabeçalho do AEM. No entanto, o headful versus headless não precisam ser uma escolha binária no AEM. Os recursos headless podem ser usados para gerenciar e fornecer conteúdo a vários pontos de contato, além de permitir que os autores de conteúdo editem aplicativos de página única. Tudo em AEM.

>[!TIP]
>
>Consulte o documento [Cabeça e Sem Cabeça no AEM](/help/implementing/developing/headful-headless.md) para obter mais informações.