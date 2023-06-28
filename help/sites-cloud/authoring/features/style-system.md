---
title: Sistema de estilos
description: O sistema de estilos permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente para que autores de conteúdo possam selecioná-las ao editarem o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando-o mais flexível.
exl-id: 224928dd-e365-4f3e-91af-4d8d9f47efdd
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 59%

---

# Sistema de estilos{#style-system}

O sistema de estilos permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente para que autores de conteúdo possam selecioná-las ao editarem o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando esse componente mais flexível.

Isso elimina a necessidade de desenvolver um componente personalizado para cada estilo ou personalizar a caixa de diálogo do componente para ativar essa funcionalidade de estilo. Ele resulta em componentes mais reutilizáveis que podem ser adaptados de forma rápida e fácil às necessidades dos autores de conteúdo sem nenhum desenvolvimento de back-end para AEM.

## Caso de uso  {#use-case}

Os autores de modelo não precisam apenas da capacidade de configurar como os componentes funcionam para os autores de conteúdo, mas também de configurar várias variações visuais alternativas de um componente.

Da mesma forma, os autores de conteúdo precisam não apenas da capacidade de estruturar e organizar seu conteúdo, mas também de selecionar como ele é apresentado visualmente.

O Sistema de estilos fornece uma solução unificada para os requisitos do autor de modelo e do autor de conteúdo:

* Os autores dos modelos podem definir classes de estilo na política de conteúdo dos componentes.
* Os autores de conteúdo podem selecionar essas classes em uma lista suspensa ao editar o componente em uma página para que possam aplicar os estilos correspondentes.

A classe de estilo é então inserida no elemento wrapper de decoração do componente para que o desenvolvedor do componente não precise se preocupar com a manipulação de estilos, além de fornecer suas regras CSS.

## Visão geral {#overview}

O uso do Sistema de estilos geralmente funciona da seguinte maneira.

1. O web designer cria diferentes variações visuais de um componente.

1. O desenvolvedor de HTML recebe a saída dos componentes em HTML e as variações visuais desejadas para implementar.

1. O desenvolvedor de HTML define as classes CSS que correspondem a cada variação visual e que devem ser inseridas no elemento que envolve os componentes.

1. O desenvolvedor de HTML implementa o código CSS correspondente (e, opcionalmente, o código JS) para cada uma das variações visuais, de modo a serem exibidas conforme a definição.

1. O desenvolvedor do AEM coloca o CSS fornecido (e o JS opcional) em uma [Biblioteca do cliente](/help/implementing/developing/introduction/clientlibs.md) e a implanta.

1. O desenvolvedor do AEM ou o autor do modelo define os modelos de página e edita a política de cada componente estilizado, adicionando as classes CSS definidas, fornecendo nomes amigáveis a cada estilo e indicando quais estilos podem ser combinados.

1. O autor da página do AEM pode escolher os estilos criados no editor de páginas no menu de estilo da barra de ferramentas do componente.

Observe que apenas as três últimas etapas são realizadas no AEM. Isso significa que todo o desenvolvimento do CSS e do JavaScript necessários pode ser feito sem AEM.

Na verdade, a implementação de estilos requer apenas a implantação no AEM e a seleção nos componentes dos modelos desejados.

O diagrama a seguir ilustra a arquitetura do Sistema de estilos.

![aem-style-system](/help/sites-cloud/authoring/assets/style-system-architecture.png)

## Utilização {#use}

Para demonstrar o recurso, usaremos como exemplo a implementação da [WKND](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=pt-BR) do [componente de título](https://www.adobe.com/go/aem_cmp_title_v2_br) do componente principal.

As seções a seguir, [Como um autor de conteúdo](#as-a-content-author) e [Como um autor de modelo](#as-a-template-author) descrevem como testar a funcionalidade do Sistema de estilos usando o Sistema de estilos da WKND.

Se você desejar usar o Sistema de estilos em seus próprios componentes, faça o seguinte:

1. Instale o CSS como bibliotecas de clientes, conforme discutido na seção [Visão geral](#overview).
1. Configure as classes CSS que você deseja disponibilizar para os autores de conteúdo, conforme descrito na seção [Como autor de modelo](#as-a-template-author).
1. Os autores de conteúdo podem usar os estilos conforme descrito na seção [Como um autor de conteúdo](#as-a-content-author).

### Como autor de conteúdo  {#as-a-content-author}

1. Depois de instalar o projeto WKND, navegue até a página inicial principal no idioma inglês da WKND em `http://<host>:<port>/sites.html/content/wknd/language-masters/en` e edite a página.
1. Selecione um componente de **Título** mais abaixo da página

   ![Sistema de estilos do autor](/help/sites-cloud/authoring/assets/style-system-author1.png)

1. Toque ou clique no botão **Estilos** na barra de ferramentas do componente **Lista** para abrir o menu de estilos e alterar a aparência do componente.

   ![Seleção de estilos](/help/sites-cloud/authoring/assets/style-system-author2.png)

   >[!NOTE]
   >
   >Neste exemplo, os estilos de **Cores** (**Preto**, **Branco** e **Cinza**) são mutuamente exclusivos, enquanto as opções de **Estilo** (**Sublinhado**, **Alinhar à direita** e **Miniespaçamento**) podem ser combinadas. Isso pode ser [configurado no modelo como o autor do modelo](#as-a-template-author).

### Como autor de modelo  {#as-a-template-author}

1. Ao editar a página inicial mestre em inglês do WKND em `http://<host>:<port>/sites.html/content/wknd/language-masters/en`, edite o modelo da página em **Informações da página -> Editar modelo**.

   ![Editar modelo](/help/sites-cloud/authoring/assets/style-system-edit-template.png)

1. Edite a política do componente de **Título** tocando ou clicando no botão **Política** do componente.

   ![Editar política](/help/sites-cloud/authoring/assets/style-system-edit-policy.png)

1. Na guia Estilos das propriedades, é possível ver como os estilos foram configurados.

   ![Editar propriedades](/help/sites-cloud/authoring/assets/style-system-properties.png)

   * **Nome do grupo:** Os estilos podem ser agrupados no menu de estilo que o autor do conteúdo verá ao configurar o estilo do componente.
   * **Os estilos podem ser combinados:** Permite que vários estilos dentro desse grupo sejam selecionados ao mesmo tempo.
   * **Nome do estilo:** A descrição do estilo que será exibido ao autor do conteúdo ao configurar o estilo do componente.
   * **Classes CSS:** O nome real da classe CSS associada ao estilo.

   Use as alças de arrastar para organizar a ordem dos grupos e os estilos dentro dos grupos. Use os ícones adicionar ou excluir para adicionar ou remover grupos ou estilos nos grupos.

>[!CAUTION]
>
>As classes CSS - e qualquer JavaScript necessário - configuradas como propriedades de estilo da política de um componente, devem ser implantadas como [Bibliotecas de clientes](/help/implementing/developing/introduction/clientlibs.md) para trabalhar.

## Configurar {#setup}

Os Componentes principais versão 2 e posteriores estão habilitados para se beneficiarem do Sistema de estilos e não exigem configuração adicional.

As etapas a seguir são necessárias apenas para ativar o Sistema de estilos para os seus próprios componentes personalizados ou para [habilitar a guia Estilos opcional na caixa de diálogo Editar.](#enable-styles-tab-edit)

### Habilitar guia Estilo na caixa de diálogo Design {#enable-styles-tab-design}

Para que um componente funcione com o sistema de estilos do AEM e mostre a guia Estilo na caixa de diálogo Design, o desenvolvedor do componente deve incluir essa guia com as seguintes configurações no componente:

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
Essa configuração aplica [sobreposições](/help/implementing/developing/introduction/overlays.md) por meio do [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md).

Com o componente configurado, os estilos configurados pelos autores da página são inseridos automaticamente pelo AEM no elemento de decoração que o AEM envolve automaticamente cada componente editável. O componente em si não precisa fazer mais nada para que isso aconteça.

### Habilitar a guia Estilos na caixa de diálogo Editar {#enable-styles-tab-edit}

Uma guia Estilos opcional na caixa de diálogo Editar também está disponível. Diferentemente da guia Design, a guia Editar não é essencial para o funcionamento do sistema de estilos, mas é uma interface alternativa e opcional para um autor de conteúdo definir estilos.

A guia Editar pode ser incluída de maneira semelhante na guia Design:

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
Essa configuração aplica [sobreposições](/help/implementing/developing/introduction/overlays.md) por meio do [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md).

>[!NOTE]
>
A guia Estilos na caixa de diálogo Editar não está habilitada por padrão.

### Estilos com nomes de elemento  {#styles-with-element-names}

Um desenvolvedor também pode configurar uma lista de nomes de elementos permitidos para os estilos no componente por meio da propriedade de matriz da sequência `cq:styleElements`. Em seguida, na guia Estilos da política na caixa de diálogo de design, o autor do modelo também pode escolher um nome de elemento a ser definido para cada estilo. Isso definirá o nome do elemento do elemento wrapper.

Essa propriedade é definida no nó `cq:Component`. Por exemplo:

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
Evite definir nomes de elementos para estilos que podem ser combinados. Quando vários nomes de elemento são definidos, a ordem de prioridade é:
>
1. HTL tem precedência sobre tudo: `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
1. Entre os vários estilos ativos, o primeiro estilo na lista de estilos configurados na política do componente é aplicado.
1. Por fim, as `cq:htmlTag`/ `cq:tagName` é considerado um valor de fallback.
>

Essa capacidade de definir nomes de estilo é útil para componentes genéricos, como o Contêiner de layout ou o componente de Fragmento do conteúdo, para oferecer-lhes significado adicional.

Por exemplo, permite que um Contêiner de layout receba uma semântica como `<main>`, `<aside>`, `<nav>`, etc.
