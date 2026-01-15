---
title: Casos de uso do editor universal e caminhos de aprendizagem
description: Saiba mais sobre os principais casos de uso do Universal Editor e como aprender sobre seu uso e como implementá-lo em seus próprios projetos.
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Developer
source-git-commit: 9adf2bc4f9f25ee7fc0a39b0f1a3ae9e45fce7d2
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# Casos de uso do editor universal e caminhos de aprendizagem {#use-cases-learning-paths}

Saiba mais sobre os principais casos de uso do Universal Editor e como saber mais sobre seu uso e como implementá-lo em seus próprios projetos.

## Visão geral {#overview}

O Universal Editor é um editor visual versátil que faz parte do Adobe Experience Manager Sites. Ele permite que os autores executem a edição &quot;o que você vê é o que você obtém&quot; (WYSIWYG) de qualquer experiência headless ou headful.

Este documento explica esses dois casos de uso em detalhes e mostra como você pode saber mais sobre eles para implementar o Editor universal em seu próprio projeto.

>[!TIP]
>
>Se você ainda não tiver feito isso, revise o documento [Introdução ao Universal Editor](/help/implementing/universal-editor/introduction.md) para obter uma visão geral completa e o valor do Universal Editor.

## Casos de uso {#use-cases}

O Universal Editor apresenta um editor visual conveniente e intuitivo para seus autores de conteúdo, independentemente do tipo de conteúdo que eles estejam criando. Os dois principais casos de uso são:

* [Criação no WYSIWYG](#wysiwyg-authoring) - Use o console do AEM Sites para gerenciar o conteúdo e criar páginas no AEM usando o Universal Editor
* [Criação headless](#headless-authoring) - crie conteúdo em seu próprio aplicativo headless personalizado usando o editor universal.

### Criação no WYSIWYG {#wysiwyg-authoring}

Se já estiver familiarizado com o AEM, poderá usar o console Sites para criar e gerenciar suas páginas e editá-las com o Universal Editor.

Dessa forma, você pode se beneficiar das ferramentas disponíveis no console Sites, como gerenciamento de página (copiar, colar, mover) e fluxos de trabalho, mas também se beneficiar do editor universal moderno.

Se este for seu caso de uso, como uma próxima etapa imediata, consulte os documentos a seguir para obter uma visão geral completa de como começar a usar o Universal Editor no AEM.

1. [Guia de Introdução do Desenvolvedor para criação no WYSIWYG com o Edge Delivery Services](https://www.aem.live/developer/ue-tutorial) - Introdução ao primeiro projeto do Universal Editor no AEM
1. [Criação de Blocos Instrumentados para uso com o Editor Universal](https://www.aem.live/developer/universal-editor-blocks) - Saiba como instrumentar blocos para tornar seu conteúdo editável no Editor Universal
1. [Modelagem de conteúdo para criação no WYSIWYG com Projetos do Edge Delivery Services](https://www.aem.live/developer/component-model-definitions) - Saiba mais sobre os detalhes de como os blocos são estruturados para modelar efetivamente seu conteúdo para uso com o Editor Universal.

Depois de ler esses documentos, você pode retornar a esta página para saber mais sobre o caso de uso de criação headless e como o Universal Editor funciona em geral.

### Criação headless {#headless-authoring}

Se você já tiver um aplicativo headless, poderá usar o Editor universal para criar conteúdo para o aplicativo e manter seu conteúdo como Fragmentos de conteúdo no AEM. O único requisito é que o aplicativo seja instrumentado para permitir o uso do Editor universal.

Se este for seu caso de uso, como uma próxima etapa imediata, consulte o documento a seguir para obter um exemplo de um aplicativo headless instrumentado para usar o Editor universal.

* [Aplicativo de amostra do SecurBank para o editor universal](/help/implementing/universal-editor/securbank.md)

Depois de ler esse documento, você pode retornar a esta página para saber mais sobre o caso de uso de criação do WYSIWYG e como o Editor universal funciona em geral.

{{ue-headless-auth}}

## Como o Editor Universal Funciona {#how-ue-works}

O poder do Editor universal é sua capacidade de criar qualquer conteúdo no local, fornecendo ao autor de conteúdo uma interface do usuário totalmente intuitiva e unificada, independentemente do conteúdo.

O Editor Universal funciona da seguinte maneira.

1. Um desenvolvedor instrumenta o aplicativo ou a página para usar o Editor universal. Essa instrumentação informa ao editor qual conteúdo é editável e como mantê-lo.
   * Se você seguir a documentação do [Guia de Introdução do Desenvolvedor para Criação no WYSIWYG com o Edge Delivery Services](https://www.aem.live/developer/ue-tutorial), suas páginas serão automaticamente instrumentadas.
   * Para criação headless, seu aplicativo pode ser facilmente instrumentado.
1. O autor de conteúdo carrega o Editor universal, que, por sua vez, carrega sua página para edição. Por ser instrumentado, ele sabe qual conteúdo é editável e como deve ser representado e persistente.
1. O autor de conteúdo edita o conteúdo da página em uma interface intuitiva do WYSIWYG, editando no local.
1. O Editor universal mantém as alterações automaticamente de volta à fonte de dados.

Se você quiser saber mais sobre a arquitetura do Universal Editor, consulte o documento [Arquitetura do Universal Editor](/help/implementing/universal-editor/architecture.md).

## Conceitos do editor universal {#concepts}

Para que uma página ou aplicativo seja editável pelo Editor universal, ele deve ser instrumentado corretamente.

* [Atributos e Tipos](/help/implementing/universal-editor/attributes-types.md) - Para que um aplicativo ou página seja editável pelo Universal Editor, ele deve ser instrumentado corretamente. Isso inclui a inclusão dos metadados adequados para que o editor possa editar o conteúdo do aplicativo.
* [Definições de Modelo, Campos e Tipos de Componentes](/help/implementing/universal-editor/field-types.md) - Quando os metadados estiverem presentes para habilitar a edição de um componente, você definirá quais campos e tipos de componentes eles poderão manipular no painel de propriedades do editor.
* [Eventos do Universal Editor](/help/implementing/universal-editor/events-universal-editor.md) - Você pode personalizar ainda mais seu aplicativo aprimorando a experiência de edição no aplicativo, consumindo eventos que o Universal Editor emite em conteúdo ou interações de interface do usuário.

O editor universal também pode ser adaptado às necessidades do projeto.

* [Personalizando o Editor Universal](/help/implementing/universal-editor/customizing.md) - A experiência do Editor Universal pode ser adaptada filtrando vários aspectos do editor ou estendendo a funcionalidade do editor.
* [Extensão do Editor Universal](/help/implementing/universal-editor/extending.md) - A interface do usuário do Editor Universal pode ser estendida para expandir seus recursos para atender às necessidades do projeto.
