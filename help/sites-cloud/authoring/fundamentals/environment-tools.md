---
title: Ambiente e ferramentas de criação
description: O ambiente de criação do AEM fornece vários mecanismos para organização e edição de conteúdo
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '2163'
ht-degree: 100%

---


# Ambiente e ferramentas de criação {#authoring-the-environment-and-tools}

O ambiente de criação do AEM fornece vários mecanismos para organização e edição de conteúdo. As ferramentas fornecidas são acessadas de vários consoles e editores de página.

## Gerenciar o site {#managing-your-site}

O console **Sites** permite navegar e gerenciar o site, usando a barra de cabeçalho, a barra de ferramentas, os ícones de ação (aplicáveis ao recurso selecionado), as navegações estruturais e, quando selecionados, os trilhos secundários (por exemplo, linha do tempo e referências).

Por exemplo, exibição de coluna:

![Exibição de coluna](/help/sites-cloud/authoring/assets/column-view.png)

## Editar conteúdo da página {#editing-page-content}

Você pode editar uma página com o editor de páginas. Por exemplo:

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

![Editor de página](/help/sites-cloud/authoring/assets/page-editor.png)

>[!NOTE]
>
>Na primeira vez que você abrir uma página para edição, uma série de slides oferecerá um tour dos recursos.
>
>Ignore o tour, se desejar, e repita-o a qualquer momento selecionando o menu **Informações da página.**

## Acessar ajuda {#accessing-help}

Ao editar uma página, a **Ajuda** pode ser acessada de:

* O seletor [**Informações da página**](/help/sites-cloud/authoring/fundamentals/page-properties.md#page-properties) que mostra os slides de introdução (como na primeira vez que você acessa o editor)
* A caixa de diálogo [Configuração](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) para componentes específicos (usando o ícone ? na barra de ferramentas da caixa de diálogo), que mostra a ajuda sensível ao contexto

Mais [recursos relacionados à ajuda estão disponíveis nos consoles](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help).

## Navegador de componentes   {#components-browser}

Os componentes são os blocos de construção do conteúdo do AEM. Você coloca vários componentes em uma página e configura as opções para criar a página de conteúdo com o AEM.

O navegador de componentes mostra todos os componentes disponíveis para uso na sua página atual. Eles podem ser arrastados para o local apropriado e depois editados para adição de conteúdo.

O navegador de componentes é uma guia dentro do painel lateral (junto com o [navegador de ativos](#assets-browser) e a [árvore de conteúdo](#content-tree)). Para abrir (ou fechar) o painel lateral, use o ícone na parte superior esquerda da barra de ferramentas:

![Ativar/desativar painel lateral](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

Ao abrir o painel lateral, ele deslizará para ser aberto no lado esquerdo (selecione a guia **Componentes**, conforme necessário). Quando estiver aberta, você pode navegar por todos os componentes disponíveis para a sua página.

A aparência e o manuseio real dependem do tipo de dispositivo usado:

* **Dispositivo móvel (por exemplo iPad)**

   O navegador de componente cobre completamente a página sendo editada.

   Para adicionar um componente à sua página, toque e segure o componente desejado e mova-o para a direita - o navegador de componente será fechado para mostrar a página novamente - onde você poderá posicionar o componente.

   ![Navegador de componentes em dispositivos móveis](/help/sites-cloud/authoring/assets/component-browser-mobile.png)

* **Dispositivo de desktop**

   O navegador de componente é aberto no lado esquerdo da janela.

   Para adicionar um componente à página, clique no componente e arraste-o para o local desejado.

   ![Navegador de componentes no desktop](/help/sites-cloud/authoring/assets/component-browser-desktop.png)

   Os componentes são representados por

   * Nome do componente
   * Grupo do componente (em cinza)
   * Ícone ou abreviação
      * Os ícones dos componentes padrão são monocromáticos.
      * As abreviações são sempre os dois primeiros caracteres do nome do componente.

   Na barra de ferramentas superior, no navegador **Componentes**, é possível:

   * Filtrar componentes por nome.
   * Limitar a exibição para um grupo específico usando a seleção suspensa.

   Para obter uma descrição mais detalhada do componente, clique ou toque no ícone de informações ao lado do componente no navegador **Componentes** (se disponível). Por exemplo, para o **Fragmento de conteúdo**:

   ![Informações do navegador de componentes](/help/sites-cloud/authoring/assets/component-browser-information.png)

   Para mais informações sobre os componentes disponíveis para você, consulte o [Console de componentes](/help/sites-cloud/authoring/features/components-console.md).

>[!NOTE]
>
>Um dispositivo móvel é detectado quando a largura é inferior a 1024px. Esse também pode ser o caso para uma janela pequena de desktop.

## Navegador de ativos {#assets-browser}

O navegador de ativos mostra todos os [ativos](/help/assets/home.md) disponíveis para o uso direto na sua página atual.

O navegador de ativos é um guia no painel lateral juntamente com o [navegador de componentes](#components-browser) e a [árvore de conteúdo](#content-tree). Para abrir ou fechar o painel lateral, use o ícone na parte superior esquerda da barra de ferramentas:

![Ativar/desativar painel lateral](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

Ao abrir o painel lateral, ele deslizará do lado esquerdo. Selecione a guia **Ativos** se necessário.

![Botão Navegador de ativos](/help/sites-cloud/authoring/assets/assets-browser-button.png)

Quando o navegador de ativos está aberto, você pode navegar pelos ativos disponíveis para sua página. A rolagem infinita é usada para expandir a lista quando necessário.

![Navegador de ativos](/help/sites-cloud/authoring/assets/assets-browser.png)

Para adicionar um ativo à página, selecione e arraste para o local desejado. Isso pode ser:

* Um componente existente do tipo adequado.
   * Por exemplo, você pode arrastar um ativo de imagem para um componente de imagem.
* Um [espaço reservado](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-placeholder) no sistema de parágrafo para criar um novo componente do tipo adequado.
   * Por exemplo, você pode arrastar um ativo de imagem para o sistema de parágrafo para criar um componente de imagem.

>[!NOTE]
>
>Essa ação está disponível para tipos de ativos e componentes específicos. Consulte [Inserir um componente usando o navegador de ativos](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-using-the-assets-browser) para obter mais detalhes.

Na barra de ferramentas superior dos ativos, é possível filtrá-los por:

* Nome
* Caminho
* Tipo de ativo como imagens, vídeos, documentos, parágrafos, Fragmentos de conteúdo e Fragmentos de experiência
* Características do ativo, como orientação e estilo
   * Disponíveis somente para determinados tipos de ativos

A aparência e o manuseio real dependem do tipo de dispositivo usado:

* **Dispositivo móvel**

   O navegador de ativos cobre completamente a página que está sendo editada.

   Para adicionar um ativo à sua página, toque e segure o ativo desejado, em seguida, mova-o para a direita - o navegador de ativos será fechado para mostrar a página novamente, onde você poderá adicionar o ativo ao componente desejado.

   ![Navegador de ativos em dispositivos móveis](/help/sites-cloud/authoring/assets/assets-browser-mobile.png)

* **Dispositivo de desktop**

   O navegador de ativos é aberto no lado esquerdo da janela.

   Para adicionar um ativo à página, clique no ativo e arraste-o para o componente ou local desejado.

   ![Navegador de ativos no desktop](/help/sites-cloud/authoring/assets/assets-browser-desktop.png)

>[!NOTE]
>
>Um dispositivo móvel é detectado quando a largura é menor do que 1024px; ou seja, também está em uma janela de desktop pequena.

Se você precisar fazer uma alteração rápida em um ativo, pode iniciar o [editor de ativos](/help/assets/manage-digital-assets.md) diretamente do navegador de ativos, clicando no ícone de edição mostrado ao lado do nome do ativo.

![Botão Editar ativos](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## Árvore de conteúdo {#content-tree}

A **Árvore de conteúdo** fornece uma visão geral de todos os componentes na página em uma hierarquia, de modo que seja possível visualizar rapidamente como a página é composta.

A Árvore de conteúdo é uma guia dentro do painel lateral (junto com o navegador de ativos e de componentes). Para abrir (ou fechar) o painel lateral, use o ícone na parte superior esquerda da barra de ferramentas:

![Botão Árvore de conteúdo](/help/sites-cloud/authoring/assets/content-tree-button.png)

Ao abrir o painel lateral, ele deslizará para ser aberto (a partir do lado esquerdo). Selecione a guia **Árvore de conteúdo**, se necessário. Quando aberta, é exibida uma representação de exibição em árvore de sua página ou modelo, para que seja mais fácil entender como o conteúdo é estruturado hierarquicamente. Além disso, em uma página complexa, facilita alternar entre os componentes da página.

![Árvore de conteúdo](/help/sites-cloud/authoring/assets/content-tree-editor.png)

Uma página pode ser facilmente composta por vários componentes do mesmo tipo, portanto a árvore de conteúdo (componente) exibe o texto descritivo (em cinza) após o nome do tipo de componente (em preto). O texto descritivo é originado de propriedades comuns do componente, como título ou texto.

Os tipos de componentes serão exibidos no idioma do usuário, enquanto o texto de descrição do componente apresenta o idioma da página.

Clicar no ícone de divisa ao lado de um componente recolherá ou expandirá o respectivo nível.

![Expansão de divisa da Árvore de conteúdo](/help/sites-cloud/authoring/assets/content-tree-chevron.png)

Clicar no componente realçará o componente no editor de páginas. As ações disponíveis dependerão do estado da página:

* Por exemplo, uma página básica:

   ![Árvore de conteúdo realçada](/help/sites-cloud/authoring/assets/content-tree-highlighted.png)

   Os componentes de uma página básica terão as opções normais.

   Se você clicar em um componente na árvore que seja editável, um ícone de chave inglesa aparecerá à direita do nome. Clicar no ícone de edição iniciará diretamente a caixa de diálogo referente ao componente.

   ![Botão Editar árvore de conteúdo](/help/sites-cloud/authoring/assets/content-tree-edit.png)

* Uma página que faz parte de uma live copy, em que os componentes são herdados de outra página, terá uma seleção reduzida de opções, incluindo as opções de herança. <!--A page that is part of a [livecopy](/help/sites-administering/msm.md), where components are inherited from another page:-->

>[!NOTE]
>
>A Árvore de conteúdo não ficará disponível se você estiver editando uma página em um dispositivo móvel (se a largura do navegador for menor do que 1024px).

## Fragmentos: navegador do conteúdo associado {#fragments-associated-content-browser}

Se a página contiver Fragmentos do conteúdo, então você também terá acesso ao [navegador para o conteúdo associado](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content).

## Referências {#references}

As **referências** mostram as conexões com a página selecionada:

* Blueprints
* Lançamentos
* Live copies
* Cópias de idioma
* Links de entrada
* Uso do componente de referência: conteúdo emprestado e concedido

Abra o console e navegue até o recurso desejado, e abra **Referências** usando:

![Opção Referências](/help/sites-cloud/authoring/assets/references.png)

[Selecione o recurso desejado](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) para mostrar uma lista de tipos de referências relevantes para esse recurso:

![Detalhes de referências](/help/sites-cloud/authoring/assets/references-detail.png)

Selecione o tipo de referência apropriado para obter mais informações. Em determinadas situações, outras ações estão disponíveis ao selecionar uma referência específica, incluindo:

* **Links de entrada**, fornecem uma lista de páginas que fazem referência à página, junto com acesso direto a **Editar** uma dessas páginas ao selecionar um link específico
* Instâncias de conteúdo emprestado e concedido usando o componente **Referência**, daqui você pode navegar até a página de referência/referenciada
* [Lançamentos](/help/sites-cloud/authoring/launches/overview.md), fornecem acesso a lançamentos relacionados
* As Live Copies exibem os caminhos de todas as live copies que são baseadas no recurso selecionado. <!--[Live Copies](/help/sites-administering/msm.md) displays the paths of all live copies that are based on the selected resource.-->
* Blueprint fornece detalhes e várias ações <!--[Blueprint](/help/sites-administering/msm-best-practices.md), provides details and various actions-->
* Cópias de idiomas fornecem detalhes e várias ações <!--[Languages Copies](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel), provides details and various actions-->

## Eventos - Linha do tempo {#events-timeline}

Para os recursos adequados (por exemplo, as páginas no console **Sites** ou os ativos no console **Ativos**), a [linha do tempo pode ser usada para mostrar a atividade recente de qualquer item selecionado](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline).

Abra o console e navegue até o recurso desejado, e abra **Linha do tempo** usando:

![Opção Linha do tempo](/help/sites-cloud/authoring/assets/timeline.png)

[Selecione o recurso desejado](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources), em seguida escolha **Exibir todos** ou **Atividades** para listar as ações recentes nos recursos selecionados:

![Detalhes da linha do tempo](/help/sites-cloud/authoring/assets/timeline-detail.png)

## Informações da página {#page-information}

As Informações da página (ícone de equalizador) abrem um menu que também fornece os detalhes sobre a última edição e a última publicação. Dependendo das características da página, de seu site e instância, mais ou menos opções podem estar disponíveis:

![Opção Informações da página](/help/sites-cloud/authoring/assets/page-information.png)

* [Abrir propriedades](/help/sites-cloud/authoring/fundamentals/page-properties.md)
* Página de implantação <!--[Rollout Page](/help/sites-administering/msm.md#msm-from-the-ui)-->
* [Iniciar fluxo de trabalho](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [Bloquear página](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)
* [Publicar página](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-pages-1)
* [Desfazer a publicação da página](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)
* [Editar modelo](/help/sites-cloud/authoring/features/templates.md)
* [Exibir como publicado](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)
* [Exibir no admin](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
* [Ajuda](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)
* [Promover lançamento](/help/sites-cloud/authoring/launches/promoting.md) (somente se a página for um lançamento)

Além disso, **Informações da página** pode fornecer acesso ao Analytics e a recomendações, quando apropriado.

## Modos de página   {#page-modes}

Há vários modos ao editar uma página, o que permite ações diferentes:

* [Edição](/help/sites-cloud/authoring/fundamentals/editing-content.md) - o modo a ser usado ao editar o conteúdo da página.
* [Layout](/help/sites-cloud/authoring/features/responsive-layout.md) - permite que você crie e edite seu layout responsivo dependente do dispositivo (se a página for baseada em um contêiner de layout)
* [Direcionamento](/help/sites-cloud/authoring/personalization/targeted-content.md) - aumenta a relevância do conteúdo através do direcionamento e medição em todos os canais.
* [Distorção](/help/sites-cloud/authoring/features/page-versions.md#timewarp) - permite que você veja o status de uma página em um ponto específico no tempo.
* [Status da Live Copy](/help/sites-cloud/authoring/fundamentals/editing-content.md#live-copy-status) - permite ter uma visão geral rápida do status da live copy e quais componentes são ou não herdados.
* [Visualização](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages)- o modo usado para visualizar a página da forma que será exibida no ambiente de publicação; ou navegar usando os links no conteúdo.
* [Anotar](/help/sites-cloud/authoring/fundamentals/annotations.md) - usado para adicionar ou exibir anotações na página.

Você pode acessar esses itens usando os ícones no canto superior direito. O ícone real será alterado para refletir o modo usado no momento:

![Modos de página](/help/sites-cloud/authoring/assets/page-modes.png)

>[!NOTE]
>
>* Dependendo das características da página, alguns modos podem não estar disponíveis.
>* O acesso a alguns modos exige permissões/privilégios adequados.
>* O modo Desenvolvedor não está disponível em dispositivos móveis devido a restrições de espaço.
>* Existe um [atalho de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) (`Ctrl-Shift-M`) para alternar entre o modo de **Visualização** e o atualmente selecionado (por exemplo, **Editar**, **Layout** etc).

>



## Seleção de caminho {#path-selection}

Ao criar, geralmente é necessário selecionar outro recurso, como ao definir um link para outra página ou recurso ou ao selecionar uma imagem. Para selecionar um caminho com facilidade, os [campos de caminho](#path-fields) oferecem o recurso de completar automaticamente, e o [navegador de caminho](#path-browser) permite uma seleção mais robusta.

### Campos de caminho   {#path-fields}

Para ilustração, o exemplo usado aqui é o componente de imagem. Para obter mais informações sobre como usar e editar componentes, consulte [Componentes para criação de página](/help/sites-cloud/authoring/fundamentals/components.md).

Agora, os campos de caminho têm funcionalidade antecipada e de preenchimento automático, para facilitar a localização de um recurso.

Clicar no botão **Abrir caixa de diálogo** no campo de caminho abre a caixa de diálogo [navegador de caminho](#path-browser) para permitir opções mais detalhadas de seleção.

![Botão Abrir caixa de diálogo de seleção](/help/sites-cloud/authoring/assets/open-selection-dialog-button.png)

Como alternativa, comece a digitar no campo de caminho e o AEM oferecerá caminhos correspondentes à medida que você digita.

![Botão Abrir caixa de diálogo de seleção](/help/sites-cloud/authoring/assets/path-selection-completion.png)

### Navegador de caminhos {#path-browser}

O navegador de caminho é organizado da mesma maneira que a [exibição de coluna](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) do console de sites, permitindo uma seleção mais detalhada dos recursos.

![Navegador de caminhos](/help/sites-cloud/authoring/assets/path-browser.png)

* Uma vez que um recurso é selecionado, o botão **Selecionar** no canto superior direito da caixa de diálogo ficará ativo. Clique ou toque para confirmar a seleção ou **Cancele** para interromper.
* Se o contexto permite a seleção de vários recursos, selecionar um recurso também ativa o botão **Selecionar**, mas, além disso, adiciona uma contagem do número de recursos selecionados no canto superior direito da janela. Clique no **X** ao lado do número para desmarcar tudo.
* Ao navegar pela árvore, sua localização é refletida nas navegações estruturais, na parte superior da caixa de diálogo. Essas navegações estruturais também podem ser usadas para avançar rapidamente na hierarquia do recurso.
* A qualquer momento, você pode usar o campo de pesquisa na parte superior da caixa de diálogo. Clique no **X** no campo de pesquisa para cancelar a pesquisa.
* Para limitar sua pesquisa, você pode revelar as opções de filtro e filtrar seus resultados com base em um determinado caminho.

   ![Opção Filtros](/help/sites-cloud/authoring/assets/filters-option.png)

## Atalhos de teclado {#keyboard-shortcuts}

Vários [atalhos de teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) estão disponíveis.
