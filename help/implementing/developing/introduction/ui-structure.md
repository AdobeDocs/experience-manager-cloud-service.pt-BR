---
title: Estrutura da IU AEM
description: A interface do usuário AEM tem vários princípios subjacentes e é composta por vários elementos chave
translation-type: tm+mt
source-git-commit: 0ae4a4695f3d869b9372694396711ca8626e1df1
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 2%

---


# Estrutura da IU AEM {#structure-of-the-aem-ui}

A interface do usuário AEM tem vários princípios subjacentes e é composta de vários elementos chave:

## Consoles {#consoles}

### Layout básico e redimensionamento {#basic-layout-and-resizing}

A interface do usuário atende a dispositivos móveis e de desktop, embora em vez de criar dois estilos, AEM usa um estilo que funciona para todas as telas e dispositivos.

Todos os módulos usam o mesmo layout básico, AEM isso pode ser visto como:

![Console AEM Sites](assets/ui-sites-console.png)

O layout segue um estilo de design responsivo e acomodará-se ao tamanho do dispositivo/janela que você está usando.

Por exemplo, quando a resolução for inferior a 1024px (como em um dispositivo móvel), a tela será ajustada de acordo:

![Visualização móvel do console Sites](assets/ui-sites-mobile.png)

### Barra do cabeçalho {#header-bar}

![Barra de cabeçalho AEM](assets/ui-header-bar.png)

A barra de cabeçalho mostra elementos globais incluindo:

* O logotipo e o produto/solução específicos que você está usando no momento; para AEM isso também forma um link para a Navegação global
* Pesquisar  
* Ícone para acessar os recursos de ajuda
* Ícone para acessar outras soluções
* Um indicador de (e acesso a) quaisquer alertas ou itens da Caixa de entrada que estejam esperando por você
* O ícone do usuário, juntamente com um link para o gerenciamento de perfis

### Barra de ferramentas {#toolbar}

A barra de ferramentas é contextual para o seu local e apresenta as ferramentas relevantes para controlar a visualização ou os ativos na página abaixo. A barra de ferramentas é específica do produto, mas há alguma compatibilidade com os elementos.

Em qualquer local, a barra de ferramentas mostra as ações disponíveis no momento:

![Barra de ferramentas do AEM Sites](assets/ui-sites-toolbar.png)

Também depende se um recurso está selecionado no momento:

![Barra de ferramentas AEM Sites selecionada](assets/ui-sites-toolbar-selected.png)

### Painel esquerdo {#left-rail}

O painel esquerdo pode ser aberto/oculto, conforme necessário, para mostrar:

* **Somente conteúdo**
* **Árvore de conteúdo**
* **Linha do tempo**
* **Referências**
* **Filtro**

O padrão é Somente **** conteúdo (painel oculto).

![Painel esquerdo](assets/ui-left-rail.png)

## Criação de página {#page-authoring}

Ao criar páginas, as áreas estruturais são as seguintes.

### Quadro de conteúdo {#content-frame}

O conteúdo da página é renderizado no quadro de conteúdo. O quadro de conteúdo é completamente independente do editor - para garantir que não haja conflitos devido a CSS ou javascript.

O quadro de conteúdo está na seção à direita da janela, abaixo da barra de ferramentas.

![Quadro de conteúdo](assets/ui-content-frame.png)

### Quadro do editor {#editor-frame}

O quadro do editor permite os recursos de edição.

O quadro do editor é um container (abstrato) para todos os elementos de criação da página. Ele fica sobre o quadro de conteúdo e inclui:

* A barra de ferramentas superior
* O painel lateral
* Todas as sobreposições
* Qualquer outro elemento de criação de página; por exemplo, a barra de ferramentas do componente

![Quadro do editor](assets/ui-editor-frame.png)

### Painel lateral {#side-panel}

Isso contém três guias padrão. As guias **Ativos** e **Componentes** permitem selecionar esses elementos e arrastá-los do painel e soltá-los na página. A guia **Árvore** de conteúdo permite inspecionar a hierarquia de conteúdo na página.

O painel lateral está oculto por padrão. Quando selecionada, esta opção será mostrada no lado esquerdo ou deslizará para cobrir a janela inteira quando o tamanho da janela estiver abaixo de uma largura de 1024px; como, por exemplo, em um dispositivo móvel.

![Painel lateral](assets/ui-side-panel.png)

### Painel lateral - Ativos {#side-panel-assets}

Na guia Ativos, é possível selecionar na faixa de ativos. Você também pode filtrar um termo específico ou selecionar um grupo.

![Guia Ativos](assets/ui-side-panel-assets.png)

### Painel lateral - Grupos de ativos {#side-panel-asset-groups}

Na guia Ativos, há uma lista suspensa que você pode usar para selecionar os grupos de ativos específicos.

![Grupos de ativos](assets/ui-side-panel-asset-groups.png)

### Painel lateral - Componentes {#side-panel-components}

Na guia Componentes, é possível selecionar a partir do intervalo de componentes. Você também pode filtrar um termo específico ou selecionar um grupo.

![Guia Componentes](assets/ui-side-panel-components.png)

### Painel lateral - Árvore de conteúdo {#side-panel-content-tree}

Na guia Árvore de conteúdo, é possível visualização a hierarquia de conteúdo na página. Clicar em uma entrada na guia vai para e seleciona o item na página dentro do editor.

![Árvore de conteúdo](assets/ui-side-panel-content-tree.png)

### Sobreposições {#overlays}

Elas sobrepõem o quadro de conteúdo e são usadas pelas [camadas](#layer) para perceber os mecanismos de como você pode interagir (de forma totalmente transparente) com os componentes e seu conteúdo.

As sobreposições vivem no quadro do editor (com todos os outros elementos de criação de página), embora na verdade sobreponham os componentes apropriados no quadro de conteúdo.

![Sobreposições](assets/ui-overlays.png)

### Camada {#layer}

Uma camada é um conjunto independente de funcionalidades que pode ser ativado para:

* Fornecer uma visualização diferente da página
* Permitir manipular e/ou interagir com uma página

As camadas fornecem funcionalidade sofisticada para a página inteira, em vez de ações específicas em um componente individual.

AEM vem com várias camadas já implementadas para a criação de páginas; incluindo, por exemplo, editar, pré-visualização e anotar camadas.

>[!NOTE]
>
>As camadas são um conceito poderoso que afeta a visualização do usuário e a interação com o conteúdo da página. Ao desenvolver suas próprias camadas, é necessário garantir que a camada seja limpa quando ela for fechada.

### Comutador de camada {#layer-switcher}

O alternador de camadas permite que você escolha a camada que deseja usar. Quando fechada, indica a camada que está sendo usada no momento.

O alternador de camadas está disponível como uma lista suspensa na barra de ferramentas (na parte superior da janela, no quadro do editor).

![Alternador de camada](assets/ui-layer-switcher.png)

### Component Toolbar {#component-toolbar}

Cada instância de um componente revelará sua barra de ferramentas quando clicada (uma vez ou com um clique em duplo lento). A barra de ferramentas contém as ações específicas (por exemplo, copiar, colar, abrir editor) que estão disponíveis para a instância do componente na página.

Dependendo do espaço disponível, as barras de ferramentas do componente são posicionadas no canto superior ou inferior direito do componente apropriado.

![Barra de ferramentas Componente](assets/ui-component-toolbar.png)

## Informações adicionais {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

Para obter mais informações técnicas, consulte a documentação [JS definida](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) para o editor de página habilitado para toque.
