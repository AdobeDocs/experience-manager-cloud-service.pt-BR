---
title: Desenvolvimento e diff de página
description: Entenda como o recurso Diferença de página funciona e como ele pode afetar um desenvolvedor
exl-id: 03c08616-2203-4b90-bed6-4836266e2507
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 12%

---

# Desenvolvimento e diff de página {#developing-and-page-diff}

## Visão geral do recurso {#feature-overview}

A criação de conteúdo é um processo iterativo. A criação com eficiência requer a capacidade de ver o que foi alterado de uma iteração para outra. Visualizar uma versão da página e, em seguida, a outra é ineficiente e sujeita a erros. Um autor deseja poder comparar a página atual com uma versão anterior lado a lado com as diferenças destacadas.

A comparação de páginas permite que um usuário compare a página atual com inicializações, versões anteriores e assim por diante. Para obter detalhes sobre este recurso de usuário, consulte [Diferença de Página](/help/sites-cloud/authoring/sites-console/page-diff.md).

## Detalhes da operação {#operation-details}

Ao comparar versões de uma página, a versão anterior que o usuário deseja comparar é recriada pelo AEM em segundo plano para facilitar o diferencial. Esta versão anterior é necessária para renderizar o conteúdo [para comparação lado a lado](/help/sites-cloud/authoring/sites-console/page-diff.md).

Essa operação de recriação é feita pela AEM internamente e é transparente para o usuário e não requer nenhuma intervenção. No entanto, um administrador que visualizasse o repositório, por exemplo, no CRXDE Lite, veria essas versões recriadas na estrutura do conteúdo.

Quando o conteúdo é comparado, a árvore inteira até a página que será comparada é recriada no seguinte local:

`/tmp/versionhistory/`

Uma tarefa de limpeza é executada automaticamente para limpar esse conteúdo temporário.

## Limitações {#limitations}

O diferencial ocorre no lado do cliente por meio da comparação de DOM, tornando o processo de diferencial simples. No entanto, há várias limitações que devem ser consideradas pelo desenvolvedor.

* Esse recurso usa classes CSS que não têm namespace para o produto AEM. Se outras classes CSS personalizadas ou classes CSS de terceiros com os mesmos nomes forem incluídas na página, a exibição do diferencial poderá ser afetada.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Como o recurso de diferencial é executado no lado do cliente e no carregamento da página, os ajustes no DOM após a execução do serviço de diferencial do lado do cliente não são considerados. Esse processo pode afetar o seguinte:

   * Componentes que usam o AJAX para incluir conteúdo
   * Aplicativos de página única
   * Componentes baseados em JavaScript que manipulam o DOM na interação do usuário.
