---
title: Desenvolvimento sem cabeça para AEM Sites como Cloud Service
description: O uso de recursos avançados, como Modelos de conteúdo, Fragmentos de conteúdo e a API GraphQL, AEM como Cloud Service, permite gerenciar suas experiências centralmente e servi-las em canais.
translation-type: tm+mt
source-git-commit: 712a99095494ab333cf0ebb2ac9fffe3f5945f3b
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 3%

---


# Desenvolvimento sem cabeça para AEM Sites como Cloud Service {#headless-development}

O uso de recursos avançados, como Modelos de conteúdo, Fragmentos de conteúdo e a API GraphQL, AEM como Cloud Service, permite gerenciar suas experiências centralmente e servi-las em canais.

## Visão geral {#overview}

A implementação sem responsável está se tornando cada vez mais importante para fornecer experiências à sua audiência, onde quer que elas estejam e independentemente do canal.

A implementação sem cabeçalho perde o gerenciamento de páginas e componentes, como é tradicional em soluções totalmente empilhadas e híbridas, e foca na criação de fragmentos de conteúdo reutilizáveis e neutros em canais e em seus delivery entre canais. É um padrão de desenvolvimento moderno e dinâmico para implementar experiências da Web.

![Modelos de implementação AEM](assets/aem-implementation-models.png)

## AEM como um Cloud Service e sem cabeça {#aem-headless}

A AEM como Cloud Service é uma ferramenta flexível para o modelo de implementação sem cabeça, oferecendo três serviços poderosos:

1. Modelos de conteúdo
   * Os Modelos de conteúdo são representação estruturada do conteúdo.
   * Eles são definidos pelos arquitetos de informações no editor AEM Content Fragment Model.
   * Os Modelos de conteúdo servem de base para Fragmentos de conteúdo.
1. Fragmentos de conteúdo
   * Fragmentos de conteúdo são instanciações de modelos de conteúdo.
   * Eles são criados por autores de conteúdo usando o editor AEM Fragmento de conteúdo.
   * Eles são armazenados no AEM Assets e gerenciados na interface do usuário de administração do Assets.
1. API de conteúdo para delivery
   * A API AEM GraphQL oferece suporte ao delivery do fragmento do conteúdo.
   * A API REST da AEM Assets suporta operações CRUD de fragmento de conteúdo.
   * O delivery de conteúdo direto também é possível com a exportação JSON do [Componente principal do fragmento de conteúdo.](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/components/content-fragment-component.html)

## Guias de introdução sem cabeçalho {#getting-started}

Os Guias de introdução sem cabeçalho apresentam um caminho simples para criar, gerenciar e fornecer experiências usando o AEM como Cloud Service em cinco etapas. Cada guia baseia-se no anterior, portanto, é recomendável explorá-los minuciosamente e em ordem.

1. [Criando uma configuração](getting-started/create-configuration.md)
1. [Criação de um modelo de fragmento de conteúdo](getting-started/create-content-model.md)
1. [Criação de uma pasta de ativos](getting-started/create-assets-folder.md)
1. [Criação de um fragmento de conteúdo](getting-started/create-content-fragment.md)
1. [Acessar e fornecer fragmentos de conteúdo](getting-started/create-api-request.md)

## Público {#audience}

As tarefas descritas nos [Guias de introdução sem cabeçalho](#getting-started) são necessárias para uma demonstração básica completa dos recursos sem cabeçalho AEM. Qualquer pessoa com acesso de administrador a uma instância de AEM de teste pode seguir esses guias para entender o delivery sem cabeçalho no AEM, embora alguém com experiência de desenvolvedor seja ideal.

No entanto, em uma situação de produção, as tarefas serão executadas por pessoas diferentes em um número variado de vezes. Por exemplo:

* **Os** administradores precisarão configurar a configuração inicial e a estrutura de pastas para o conteúdo normalmente apenas uma vez ou esporadicamente.
* **Os** arquitetos de informações em geral adicionarão novos modelos à medida que as necessidades da organização forem evoluindo.
* **As** autoridades de conteúdo criarão continuamente novo conteúdo como Fragmentos de conteúdo com base nos modelos definidos pelos arquitetos.

Os Guias de introdução sem cabeçalho indicam quem normalmente executaria as tarefas descritas e com que frequência.

## Próxima etapa {#next-step}

Pronto para aprender mais? Em seguida, comece lendo a primeira parte do Guia de introdução sem cabeçalho: [Criação de uma Configuração.](getting-started/create-configuration.md)
