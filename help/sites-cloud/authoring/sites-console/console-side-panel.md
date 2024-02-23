---
title: Painel lateral do console Sites
description: Saiba como usar o painel lateral no console de sites AEM para entender e navegar melhor pelo seu conteúdo.
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 23%

---


# Painel lateral do console Sites {#side-panel}

Saiba como usar o painel lateral no AEM **Sites** para melhor entender e navegar pelo seu conteúdo.

## Orientação {#orientation}

Por padrão, o painel lateral é fechado quando você insere a variável **Sites** console. Dessa forma, a tela é totalmente dedicada ao conteúdo.

Toque ou clique no **Painel lateral** ícone no **Sites** barra de ferramentas do console para ativar o painel lateral e escolher a visualização do conteúdo.

* [Somente conteúdo](#content-only)
* [Árvore de conteúdo](#content-tree)
* [Linha do tempo](#timeline)
* [Referências](#references)
* [Site](#site)
* [Filtro](#filter)
* [Análise de configuração](#setup-analytics)

![Exibições do painel lateral do console Sites](assets/sites-console-side-panel-views.png)

A exibição atual selecionada é indicada por uma marca de seleção azul na lista suspensa e o ícone do painel lateral na barra de ferramentas é atualizado com o nome da exibição selecionada.

## Somente conteúdo {#content-only}

Essa exibição do painel lateral está efetivamente desativando-a, ou seja, mostra apenas o conteúdo do site.

>[!TIP]
>
>Usar o acento grave/backtick `´` atalho do teclado para alternar para a exibição somente conteúdo do painel lateral.

## Árvore de conteúdo {#content-tree}

Essa exibição do painel lateral exibe o conteúdo em uma hierarquia de árvore. A árvore de conteúdo pode ser usada para navegar rapidamente pela hierarquia do site no painel lateral e exibir muitas informações sobre as páginas na pasta atual.

![A visualização de árvore de conteúdo do painel lateral](assets/console-side-panel-content-tree.png)

Uma divisa apontando para a direita ao lado de um item na árvore indica um nó que pode ser expandido para revelar seus filhos. Toque ou clique na divisa para revelar as crianças.

O console exibe o conteúdo do item selecionado atualmente na árvore de conteúdo.

Usando o painel lateral da árvore de conteúdo em conjunto com uma exibição de lista ou exibição de cartões, você pode ver facilmente a estrutura hierárquica do projeto e navegar facilmente pela estrutura de conteúdo com o painel lateral da árvore de conteúdo e exibir informações detalhadas da página na exibição de lista.

>[!TIP]
>
>* Use o `Alt+1` atalho do teclado para alternar para a exibição de árvore de conteúdo do painel lateral.
>* Depois que uma entrada da exibição hierárquica é selecionada, as teclas de seta podem ser usadas para navegar rapidamente pela hierarquia.
>* Consulte os [atalhos de teclado](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) para obter mais informações.

## Linha do tempo {#timeline}

A linha do tempo pode ser usada para exibir eventos que afetaram o recurso selecionado. Também é possível usá-lo para iniciar determinados eventos, como fluxos de trabalho ou versões.

![Detalhes da linha do tempo](/help/sites-cloud/authoring/assets/timeline-detail.png)

A variável **Linha do tempo** o painel lateral permite exibir vários eventos relacionados a um item selecionado que podem ser selecionados como tipos em uma lista suspensa:

* Comentários
* [Anotações](/help/sites-cloud/authoring/page-editor/annotations.md)
* [Atividades](/help/sites-cloud/authoring/personalization/activities.md)
* [Lançamentos](/help/sites-cloud/authoring/launches/overview.md)
* [Versões](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Fluxos de trabalhos](/help/sites-cloud/authoring/workflows/overview.md)
   * Observe que nenhuma informação será mostrada para fluxos de trabalho transitórios, pois nenhuma informação de histórico é salva para eles.<!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
* Exibir todos

Além disso, você pode adicionar/exibir comentários sobre o item selecionado usando o **Comentário** mostrada na parte inferior da lista de eventos. Digitar um comentário seguido por `Return` registrará o comentário. É exibido quando **Comentários** ou **Mostrar tudo** é selecionado.

No **Sites** console também é possível acessar recursos adicionais através do botão de reticências ao lado da **Comentário** campo.

* [Salvar uma versão](/help/sites-cloud/authoring/sites-console/page-versions.md)
* [Iniciar um fluxo de trabalho](/help/sites-cloud/authoring/workflows/applying.md)

![Campo de comentário do console Sites](assets/sites-console-comment-ellipsis.png)

>[!TIP]
>
>* Use o `Alt+2` atalho de teclado para alternar para a exibição de linha do tempo do painel lateral.
>* Consulte os [atalhos de teclado](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) para obter mais informações.

## Referências {#references}

A variável **Referências** a exibição mostra uma lista de tipos de referências para ou do recurso selecionado no console.

![Detalhes de referências](assets/console-side-panel-references-detail.png)

Selecione o tipo de referência apropriado para obter mais informações. Em determinadas situações, outras ações estarão disponíveis ao selecionar uma referência específica, incluindo:

* **Links de entrada**, fornece uma lista de páginas que fazem referência à página, juntamente com acesso direto a **Editar** uma dessas páginas ao selecionar um link específico.
   * Isso só pode mostrar links estáticos, não links gerados dinamicamente, como no componente List.
* [Lançamentos](/help/sites-cloud/authoring/launches/overview.md), fornecem acesso a lançamentos relacionados
* As [Live Copies](/help/sites-cloud/administering/msm/overview.md) exibem os caminhos de todas as live copies que são baseadas no recurso selecionado.
* [Blueprint](/help/sites-cloud/administering/msm/best-practices.md), fornece detalhes e várias ações
* [Cópias de idiomas](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel), fornece detalhes e várias ações

## Site {#site}

A variável **Site** a exibição do painel lateral mostra detalhes de sites [criado usando um modelo de site.](/help/sites-cloud/administering/site-creation/create-site.md)

![Painel do site](assets/console-side-panel-site-paenl.png)

Consulte o documento [Usar o painel Site para gerenciar o tema do site](/help/sites-cloud/administering/site-creation/site-rail.md) para obter mais detalhes sobre como é possível usar o painel para gerenciar a [tema do site.](/help/sites-cloud/administering/site-creation/site-themes.md).

Se você ainda não tiver configurado o pipeline de front-end para habilitar a criação de site com base em temas, o painel lateral oferecerá essa opção.

![Opção para ativar o pipeline de front-end no painel lateral](assets/sites-console-side-panel-site.png)

>[!TIP]
>
>Uma descrição completa do processo de criação de um site a partir de um modelo e personalização de seu tema pode ser encontrada na [Jornada rápida de criação de sites.](/help/journey-sites/quick-site/overview.md)

## Filtro {#filter}

A variável **Filtro** é semelhante ao [recurso de pesquisa](/help/sites-cloud/authoring/search.md) com os filtros de localização apropriados já definidos, permitindo filtrar ainda mais o conteúdo que deseja exibir.

![Exemplo de filtro](assets/console-side-panel-filter.png)

Ao contrário de outras exibições do painel lateral, para alternar para outra exibição, toque ou clique no `X` no campo de pesquisa.

## Análise de configuração {#setup-analytics}

Essa visualização permite configurar rapidamente o Adobe Analytics para um site selecionado.

![Configurar o Analytics](assets/sites-console-side-panel-setup-analytics.png)
