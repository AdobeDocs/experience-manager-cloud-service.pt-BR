---
title: Estrutura da interface do AEM
description: A interface do usuário do AEM tem vários princípios subjacentes e é composta de vários elementos principais
exl-id: ac211716-d699-4fdb-a286-a0a1122c86c5
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 4%

---

# Estrutura da interface do AEM {#structure-of-the-aem-ui}

A interface do usuário do AEM tem vários princípios subjacentes e é composta de vários elementos principais:

## Consoles {#consoles}

### Layout básico e redimensionamento {#basic-layout-and-resizing}

A interface do usuário abrange dispositivos móveis e de desktop, embora em vez de criar dois estilos, AEM usa um estilo que funciona para todas as telas e dispositivos.

Todos os módulos usam o mesmo layout básico, AEM isso pode ser visto como:

![Console do AEM Sites](assets/ui-sites-console.png)

O layout adere a um estilo de design responsivo e se acomodará ao tamanho do dispositivo/janela usado.

Por exemplo, quando a resolução fica abaixo de 1024px (como em um dispositivo móvel), a exibição será ajustada adequadamente:

![Visualização móvel do console Sites](assets/ui-sites-mobile.png)

### Barra do cabeçalho {#header-bar}

![Barra de cabeçalho de AEM](assets/ui-header-bar.png)

A barra de cabeçalho mostra elementos globais incluindo:

* O logotipo e o produto/solução específico que você está usando no momento; para AEM isso também forma um link para a Navegação global
* Pesquisar
* Ícone para acessar os recursos de ajuda
* Ícone para acessar outras soluções
* Um indicador de (e acesso a) quaisquer alertas ou itens da Caixa de entrada que estão aguardando você
* O ícone do usuário, juntamente com um link para o gerenciamento de perfis

### Barra de ferramentas {#toolbar}

A barra de ferramentas é contextual à sua localização e supera as ferramentas relevantes para controlar a exibição ou os ativos na página abaixo. A barra de ferramentas é específica do produto, mas há uma compatibilidade entre os elementos.

Em qualquer local, a barra de ferramentas mostra as ações disponíveis no momento:

![Barra de ferramentas AEM Sites](assets/ui-sites-toolbar.png)

Também depende de um recurso estar selecionado no momento:

![Barra de ferramentas AEM Sites selecionada](assets/ui-sites-toolbar-selected.png)

### Painel esquerdo {#left-rail}

O painel esquerdo pode ser aberto/oculto, conforme necessário, para mostrar:

* **Somente conteúdo**
* **Árvore de conteúdo**
* **Linha do tempo**
* **Referências**
* **Filtro**

O padrão é **Somente conteúdo** (painel oculto).

![Painel esquerdo](assets/ui-left-rail.png)

## Criação de página {#page-authoring}

Ao criar páginas, as áreas estruturais são as seguintes.

### Quadro de conteúdo {#content-frame}

O conteúdo da página é renderizado no quadro de conteúdo. O quadro de conteúdo é completamente independente do editor - para garantir que não haja conflitos devido a CSS ou javascript.

O quadro de conteúdo está na seção à direita da janela, abaixo da barra de ferramentas.

![Quadro de conteúdo](assets/ui-content-frame.png)

### Quadro do editor {#editor-frame}

O quadro do editor habilita os recursos de edição.

O quadro do editor é um contêiner (abstrato) para todos os elementos de criação de página. Ela fica sobre o quadro de conteúdo e inclui:

* A barra de ferramentas superior
* O painel lateral
* Todas as sobreposições
* Qualquer outro elemento de criação de página; por exemplo, a barra de ferramentas do componente

![Quadro do editor](assets/ui-editor-frame.png)

### Painel lateral {#side-panel}

Ele contém três guias padrão. O **Ativos** e **Componentes** as guias permitem selecionar esses elementos, arrastá-los do painel e soltá-los na página. O **Árvore de conteúdo** permite inspecionar a hierarquia do conteúdo na página.

O painel lateral está oculto por padrão. Quando selecionado, será mostrado no lado esquerdo ou deslizará para cobrir toda a janela quando o tamanho da janela estiver abaixo de 1024px; como, por exemplo, em um dispositivo móvel.

![Painel lateral](assets/ui-side-panel.png)

### Painel lateral - Ativos {#side-panel-assets}

Na guia Ativos , é possível selecionar entre a faixa de ativos. Também é possível filtrar por um termo específico ou selecionar um grupo.

![Guia Ativos](assets/ui-side-panel-assets.png)

### Painel lateral - Grupos de ativos {#side-panel-asset-groups}

Na guia Ativos , há uma lista suspensa que pode ser usada para selecionar os grupos de ativos específicos.

![Grupos de ativos](assets/ui-side-panel-asset-groups.png)

### Painel lateral - Componentes {#side-panel-components}

Na guia Componentes , é possível selecionar entre as várias opções de componentes. Também é possível filtrar por um termo específico ou selecionar um grupo.

![Guia Componentes](assets/ui-side-panel-components.png)

### Painel lateral - Árvore de conteúdo {#side-panel-content-tree}

Na guia Árvore de conteúdo , é possível exibir a hierarquia do conteúdo na página. Clicar em uma entrada na guia vai para e seleciona o item na página no editor.

![Árvore de conteúdo](assets/ui-side-panel-content-tree.png)

### Sobreposições {#overlays}

Eles sobrepõem o quadro de conteúdo e são usados pela variável [camadas](#layer) para compreender os mecanismos de como você pode interagir (de forma totalmente transparente) com os componentes e seu conteúdo.

As sobreposições vivem no quadro do editor (com todos os outros elementos de criação de página), embora elas realmente sobreponham os componentes apropriados no quadro de conteúdo.

![Sobreposições](assets/ui-overlays.png)

### Camada {#layer}

Uma camada é um conjunto de funcionalidades independente que pode ser ativado para:

* Fornecer uma exibição diferente da página
* Permitir manipular e/ou interagir com uma página

As camadas fornecem funcionalidade sofisticada para a página inteira, em vez de ações específicas em um componente individual.

AEM vem com várias camadas já implementadas para criação de página; incluindo, por exemplo, editar, visualizar e anotar camadas.

>[!NOTE]
>
>Camadas são um conceito poderoso que afeta a exibição do usuário e a interação com o conteúdo da página. Ao desenvolver suas próprias camadas, é necessário garantir que a camada seja limpa ao sair.

### Seletor de camada {#layer-switcher}

O alternador de camadas permite escolher a camada que deseja usar. Quando fechado, indica a camada em uso no momento.

O alternador de camadas está disponível como uma lista suspensa na barra de ferramentas (na parte superior da janela, dentro do quadro do editor).

![Seletor de camada](assets/ui-layer-switcher.png)

### Component Toolbar {#component-toolbar}

Cada instância de um componente revelará a barra de ferramentas ao clicar (uma vez ou com um clique duplo lento). A barra de ferramentas contém as ações específicas (por exemplo, copiar, colar, abrir o editor) que estão disponíveis para a instância do componente na página.

Dependendo do espaço disponível, as barras de ferramentas do componente são posicionadas no canto superior ou inferior direito do componente adequado.

![Barra de ferramentas Componente](assets/ui-component-toolbar.png)

## Informações adicionais {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

Para obter mais informações técnicas, consulte o [Conjunto de documentação JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) para o editor de páginas.
