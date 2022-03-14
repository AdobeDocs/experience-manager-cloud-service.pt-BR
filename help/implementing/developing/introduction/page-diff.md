---
title: Desenvolvimento e diff de página
description: Entenda como o recurso Diferencial de página funciona e como ele pode afetar um desenvolvedor
exl-id: 03c08616-2203-4b90-bed6-4836266e2507
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 11%

---

# Desenvolvimento e diff de página {#developing-and-page-diff}

## Visão geral dos recursos {#feature-overview}

A criação de conteúdo é um processo iterativo. Criar com eficiência exige poder ver o que mudou de uma iteração para outra. Visualizar uma versão da página e, em seguida, a outra é um processo ineficiente e propenso a erros. Um autor deseja poder comparar a página atual com uma versão anterior lado a lado com as diferenças destacadas.

O diferencial de páginas permite que um usuário compare a página atual com inicializações, versões anteriores etc. Para obter detalhes sobre este recurso do usuário, consulte [Diff da página](/help/sites-cloud/authoring/features/page-diff.md).

## Detalhes da Operação {#operation-details}

Ao comparar versões de uma página, a versão anterior que o usuário deseja comparar é recriada por AEM em segundo plano para facilitar o diferencial. Isso é necessário para poder renderizar o conteúdo [para comparação lado a lado](/help/sites-cloud/authoring/features/page-diff.md).

Essa operação de recriação é feita por AEM internamente e é transparente para o usuário e não requer intervenção. No entanto, um administrador que visualiza o repositório, por exemplo, no CRX DE Lite, veria essas versões recriadas na estrutura de conteúdo.

Quando o conteúdo é comparado, a árvore inteira até a página a ser comparada é recriada no seguinte local:

`/tmp/versionhistory/`

Uma tarefa de limpeza é executada automaticamente para limpar esse conteúdo temporário.

## Limitações           {#limitations}

O diferencial ocorre no lado do cliente por meio da comparação de DOM, tornando o processo de comparação simples, no entanto, há várias limitações que precisam ser consideradas pelo desenvolvedor.

* Esse recurso usa classes CSS que não são nomeadas espaçadas para o Produto AEM. Se outras classes CSS personalizadas ou classes CSS de terceiros com os mesmos nomes forem incluídas na página, a exibição do diferencial poderá ser afetada.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Como o diferencial é do lado do cliente e é executado no carregamento da página, os ajustes no DOM após a execução do serviço de comparação do lado do cliente não serão contabilizados. Pode afetar

   * Componentes que usam AJAX para incluir conteúdo
   * Aplicativos de página única
   * Componentes baseados em JavaScript que manipulam o DOM na interação do usuário.
