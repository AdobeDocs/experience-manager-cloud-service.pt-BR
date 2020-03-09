---
title: Sistema de estilos
description: O Sistema de estilos permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente, de modo que o autor de conteúdo possa selecioná-los ao editar o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando-o mais flexível.
translation-type: ht
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Sistema de estilos {#style-system}

O Sistema de estilos permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente, de modo que o autor de conteúdo possa selecioná-los ao editar o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando-o mais flexível.

Isso elimina a necessidade de desenvolver um componente personalizado para cada estilo ou personalizar a caixa de diálogo do componente para permitir essa funcionalidade de estilo. Isso resulta em componentes mais reutilizáveis, que podem ser adaptados de forma rápida e fácil às necessidades dos autores de conteúdo, sem exigir uma implantação de back-end no AEM.

## Caso de uso   {#use-case}

Os autores de modelos precisam ter a capacidade de configurar a forma como os componentes funcionam para os autores de conteúdo, bem como configurar algumas variações visuais alternativas de um componente.

Da mesma forma, os autores de conteúdo precisam ter a capacidade de estruturar e organizar o conteúdo, além de selecionar a maneira como ele é apresentado visualmente.

O sistema de estilos fornece uma solução unificada para os requisitos do autor de modelo e do autor de conteúdo:

* Os autores de modelos podem definir classes de estilo na política de conteúdo de componentes.
* Os autores de conteúdo podem selecionar essas classes em uma lista suspensa ao editar o componente em uma página para aplicar os estilos correspondentes.

A classe de estilo é inserida no elemento wrapper de decoração do componente para que o desenvolvedor do componente não precise se preocupar com a manipulação de estilos além de fornecer as regras de CSS.

## Visão geral {#overview}

O uso do sistema de estilos geralmente funciona da seguinte maneira.

1. O web designer cria diferentes variações visuais de um componente.
1. O desenvolvedor de HTML recebe a saída dos componentes em HTML e as variações visuais desejadas para implementar.
1. O desenvolvedor de HTML define as classes CSS que correspondem a cada variação visual e que devem ser inseridas no elemento que envolve os componentes.
1. O desenvolvedor de HTML implementa o código CSS correspondente (e, opcionalmente, o código JS) para cada uma das variações visuais, de modo a serem exibidas conforme a definição.
1. O desenvolvedor do AEM coloca o CSS fornecido (e o JS opcional) em uma Biblioteca do cliente e a implanta. <!--The AEM developer places the provided CSS (and optional JS) in a [Client Library](/help/sites-developing/clientlibs.md) and deploys it.-->
1. O desenvolvedor do AEM ou o autor do modelo define os modelos de página e edita a política de cada componente estilizado, adicionando as classes CSS definidas, fornecendo nomes amigáveis a cada estilo e indicando quais estilos podem ser combinados.
1. O autor da página do AEM pode escolher os estilos criados no editor de páginas no menu de estilo da barra de ferramentas do componente.

Observe que somente as três últimas etapas são realmente realizadas no AEM. Isso significa que todo o desenvolvimento dos códigos CSS e Javascript necessários pode ser feito sem o AEM.

A aplicação real dos estilos requer apenas a implantação no AEM e a seleção nos componentes dos modelos desejados.

O diagrama a seguir ilustra a arquitetura do sistema de estilos.

![Arquitetura do sistema de estilos](/help/sites-cloud/authoring/assets/style-system-architecture.png)

## Uso {#use}

Para demonstrar o recurso, estilos precisam ser criados para um componente. As seções a seguir [Como um autor de conteúdo](#as-a-content-author) e [Como um autor de modelo](#as-a-template-author) descrevem como usar a funcionalidade do sistema de estilos, usando o sistema de estilos, considerando que os componentes já tenham estilos configurados.

Se você desejar usar o sistema de estilos em seus próprios componentes, faça o seguinte:

1. Instale o CSS como bibliotecas de cliente, conforme descrito na seção [Visão geral](#overview).
1. Configure as classes CSS que deseja disponibilizar para os autores de conteúdo, conforme descrito na seção [Como um autor de modelo](#as-a-template-author).
1. Os autores de conteúdo podem usar os estilos conforme descrito na seção [Como um autor de conteúdo](#as-a-content-author).

### Como um autor de conteúdo   {#as-a-content-author}

1. Edite uma página que tenha um componente com um estilo configurado.
1. Selecione um componente com estilo configurado, como o componente **Lista**, como exemplo aqui.

   ![Estilos de criação](/help/sites-cloud/authoring/assets/style-system-author.png)

1. Toque ou clique no botão **Estilos** na barra de ferramentas do componente **Lista** para abrir o menu de estilos e alterar a aparência do componente.

   ![Criação de estilos por seleção](/help/sites-cloud/authoring/assets/style-system-author-select.png)

   >[!NOTE]
   >
   >Neste exemplo, os estilos de **Layout** (**Bloco** e **Grade**) são mutuamente exclusivos, enquanto que as opções de **Exibição** (**Imagem** ou **Data**) podem ser combinadas. Isso pode [ser configurado no modelo como autor do modelo](#as-a-template-author).

### Como um autor de modelo   {#as-a-template-author}

1. Ao editar uma página de conteúdo para a qual deseja configurar estilos, edite o modelo da página por meio de **Informações da página -> Editar modelo**.

   ![Editar modelo](/help/sites-cloud/authoring/assets/style-system-template.png)

1. Edite a política do componente para o qual deseja configurar os estilos, como o componente **Lista**, tocando ou clicando no botão **Política** do componente.

   ![Política do componente de modelo](/help/sites-cloud/authoring/assets/style-system-template-policy.png)

1. Na guia Estilos das propriedades, é possível ver como os estilos foram configurados.

   ![Guia Estilos da janela de propriedades](/help/sites-cloud/authoring/assets/style-system-template-styles.png)

   * **Nome do grupo:** os estilos podem ser agrupados no menu de estilos que o autor de conteúdo verá ao configurar o estilo do componente.
   * **Estilos podem ser combinados:** permite a seleção simultânea de vários estilos desse grupo.
   * **Nome do estilo:** a descrição do estilo que será exibida para o autor do conteúdo ao configurar o estilo do componente.
   * **Classes de CSS:** o nome real da classe CSS associada ao estilo.
   Use as alças de arrastar para organizar a ordem dos grupos e dos estilos nos grupos. Use os ícones Adicionar ou Excluir para adicionar ou remover grupos ou estilos nos grupos.

>[!CAUTION]
>
>As classes CSS (bem como qualquer Javascript necessário) configuradas como propriedades de estilo da política de um componente devem ser implantadas como Bibliotecas do cliente para funcionarem. <!-- The CSS classes (as well as any necessary Javascript) configured as style properties of a component's policy must be deployed as [Client Libraries](/help/sites-developing/clientlibs.md) in order to work.-->

## Configurar {#setup}

>[!NOTE]
>
>A versão 2 dos componentes principais é completamente habilitada para usufruir do sistema de estilos e não exige configuração adicional.
>
>Siga as próximas etapas para habilitar o sistema de estilos para seus próprios componentes personalizados ou para estender os componentes principais da versão 1 para usar o recurso.

Para que um componente funcione com o sistema de estilos do AEM e mostre a guia Estilo na caixa de diálogo de design, o desenvolvedor do componente deve incluir a guia do produto com as seguintes configurações no componente:

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

Com o componente configurado, os estilos configurados pelos autores da página serão inseridos automaticamente pelo AEM no elemento de decoração que o AEM adiciona ao redor de cada componente editável. O componente não precisa fazer mais nada para que isso ocorra.

### Estilos com nomes de elemento   {#styles-with-element-names}

Um desenvolvedor também pode configurar uma lista de nomes de elementos permitidos para os estilos no componente por meio da propriedade de matriz da sequência `cq:styleElements`. Na guia Estilos da política na caixa de diálogo de design, o autor do modelo também pode escolher um nome de elemento para definir cada estilo. Isso definirá o nome de elemento do wrapper.

Essa propriedade é definida no nó `cq:Component`. Por exemplo:

* `/apps/wknd/components/content/contentfragment@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>Evite definir nomes de elemento para os estilos que podem ser combinados. Quando vários nomes de elemento são definidos, a ordem de prioridade é:
>
>1. HTL tem precedência sobre tudo: `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. Entre os vários estilos ativos, o primeiro estilo na lista de estilos configurados na política do componente é aplicado.
>1. Por fim, a `cq:tagName`/ `cq:htmlTag` do componente será considerada como um valor de fallback.
>



Essa capacidade de definir nomes de estilo é útil para componentes muito genéricos, como o Contêiner de layout ou o componente de Fragmento do conteúdo, para oferecer-lhes significado adicional.

Por exemplo, permite que um Contêiner de layout receba uma semântica como `<main>`, `<aside>`, `<nav>`, etc.
