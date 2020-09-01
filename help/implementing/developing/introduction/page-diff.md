---
title: Desenvolvendo e comparação de páginas
description: Entenda como o recurso Diferença de página funciona e como ele pode afetar um desenvolvedor
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 11%

---


# Desenvolvendo e comparação de páginas {#developing-and-page-diff}

## Visão geral do recurso {#feature-overview}

A criação de conteúdo é um processo iterativo. Criar com eficiência exige poder ver o que mudou de uma iteração para outra. Visualizar uma versão da página e, em seguida, a outra é um processo ineficiente e propenso a erros. Um autor deseja comparar a página atual com uma versão anterior lado a lado com as diferenças destacadas.

O diff da página permite que um usuário compare a página atual com inicializações, versões anteriores etc. Para obter detalhes sobre esse recurso do usuário, consulte Diferença de [página](/help/sites-cloud/authoring/features/page-diff.md).

## Detalhes da operação {#operation-details}

Ao comparar versões de uma página, a versão anterior que o usuário deseja comparar é recriada por AEM em segundo plano para facilitar a diferença. Isso é necessário para que o conteúdo seja renderizado [para comparação](/help/sites-cloud/authoring/features/page-diff.md)lado a lado.

Esta operação de recriação é feita por AEM interna e é transparente para o usuário e não requer intervenção. No entanto, um administrador que visualiza o repositório, por exemplo, no CRX DE Lite, veria essas versões recriadas dentro da estrutura de conteúdo.

Quando o conteúdo é comparado, a árvore inteira até a página a ser comparada é recriada no seguinte local:

`/tmp/versionhistory/`

Uma tarefa de limpeza é executada automaticamente para limpar esse conteúdo temporário.

## Permissões  {#permissions}

O diff ocorre no cliente por meio da comparação DOM, tornando o processo diff simples, no entanto, há várias limitações que precisam ser consideradas pelo desenvolvedor.

* Este recurso usa classes CSS que não têm nomes espaçados para o Produto AEM. Se outras classes CSS personalizadas ou classes CSS de terceiros com os mesmos nomes forem incluídas na página, a exibição do diff poderá ser afetada.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Como o diff é do lado do cliente e é executado no carregamento da página, todos os ajustes no DOM após a execução do serviço de comparação do lado do cliente não serão contabilizados. Este fato pode afetar

   * Componentes que usam AJAX para incluir conteúdo
   * Aplicativos de página única
   * Componentes baseados em JavaScript que manipulam o DOM na interação do usuário.
