---
title: Desenvolvimento autônomo do AEM Sites as a Cloud Service
description: Saiba como o AEM como um Cloud Service poderoso de recursos sem cabeçalho, como Modelos de conteúdo, Fragmentos de conteúdo e a API GraphQL trabalham juntos para permitir que você gerencie suas experiências centralmente e as distribua pelos canais.
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 2%

---


# Desenvolvimento sem periféricos para o AEM Sites as a Cloud Service {#headless-development}

Saiba como o AEM como um Cloud Service poderoso de recursos sem cabeçalho, como Modelos de conteúdo, Fragmentos de conteúdo e a API GraphQL trabalham juntos para permitir que você gerencie suas experiências centralmente e as distribua pelos canais.

## Visão geral {#overview}

A implementação sem periféricos está se tornando cada vez mais importante para fornecer experiências ao seu público-alvo, onde quer que estejam e independentemente do canal.

A implementação sem cabeçalho perde o gerenciamento de página e componente, como é tradicional em soluções de pilha completa e híbridas, e se concentra na criação de fragmentos de conteúdo neutros em canais e reutilizáveis, além de seu delivery entre canais. É um padrão de desenvolvimento moderno e dinâmico para implementar experiências da Web.

![Modelos de implementação de AEM](assets/aem-implementation-models.png)

## Comparação entre Cabeça e Sem Cabeça {#headful-headless}

Este documento se concentra no modelo de implementação sem periféricos de AEM. No entanto, o headful versus headless não precisam ser uma escolha binária no AEM. Os recursos headless podem ser usados para gerenciar e entregar seu conteúdo a uma variedade de endpoints, além de permitir que os autores de conteúdo editem aplicativos de página única. Tudo em AEM.

>[!TIP]
>
>Consulte o documento [Cabeçalho e Sem Cabeça em AEM](/help/implementing/developing/headful-headless.md) para obter mais informações.

## AEM como um Cloud Service e sem cabeçalho {#aem-headless}

O AEM as a Cloud Service é uma ferramenta flexível para o modelo de implementação sem periféricos, oferecendo três serviços poderosos:

1. Modelos de conteúdo
   * Os Modelos de conteúdo são representação estruturada do conteúdo.
   * Eles são definidos pelos arquitetos de informações no editor AEM do Modelo de fragmento de conteúdo.
   * Os Modelos de conteúdo são a base dos Fragmentos de conteúdo.
1. Fragmentos de conteúdo
   * Fragmentos de conteúdo são instanciações de modelos de conteúdo.
   * Eles são criados por autores de conteúdo usando o editor AEM Fragmento de conteúdo .
   * Eles são armazenados no AEM Assets e gerenciados na interface do usuário do administrador do Assets.
1. API de conteúdo para entrega
   * A API GraphQL da AEM é compatível com a entrega de Fragmento de conteúdo.
   * A API REST do AEM Assets suporta operações CRUD de Fragmento de conteúdo.
   * A entrega de conteúdo direto também é possível com a exportação JSON do [Componente principal do fragmento de conteúdo.](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/components/content-fragment-component.html)

## Guias de introdução sem cabeçalho {#getting-started}

Os Guias de introdução sem cabeçalho apresentam um caminho simples para criar, gerenciar e fornecer experiências usando o AEM como Cloud Service em cinco etapas. Cada guia tem como base o anterior, portanto, é recomendável explorá-lo detalhadamente e em ordem.

1. [Criação de uma configuração](getting-started/create-configuration.md)
1. [Criação de um modelo de fragmento de conteúdo](getting-started/create-content-model.md)
1. [Criação de uma pasta de ativos](getting-started/create-assets-folder.md)
1. [Criação de um fragmento de conteúdo](getting-started/create-content-fragment.md)
1. [Acesso e entrega de fragmentos de conteúdo](getting-started/create-api-request.md)

## Público {#audience}

As tarefas descritas nos [Guias de introdução sem cabeçalho](#getting-started) são necessárias para uma demonstração completa e básica dos recursos sem cabeçalho AEM. Qualquer pessoa com acesso de administrador a uma instância de AEM de teste pode seguir esses guias para entender a entrega sem periféricos no AEM, embora alguém com experiência de desenvolvedor seja ideal.

No entanto, em uma situação de produção, as tarefas serão executadas por personas diferentes em um número variável de vezes. Por exemplo:

* **** Os administradores precisarão configurar a configuração inicial e a estrutura de pastas para o conteúdo normalmente apenas uma vez ou esporadicamente.
* **Em geral,** os arquitetos de informações adicionarão novos modelos à medida que as necessidades da organização evoluírem.
* **Os** autores de conteúdo criarão continuamente novo conteúdo como Fragmentos de conteúdo com base nos modelos definidos pelos arquitetos.

Os Guias de introdução sem cabeçalho apontam quem normalmente executaria as tarefas descritas e com que frequência.

## Próxima etapa {#next-step}

Pronto para aprender mais? Em seguida, comece lendo a primeira parte do Guia de Introdução Sem Cabeça: [Criando uma Configuração.](getting-started/create-configuration.md)
