---
title: Fragmentos de conteúdo
description: Os Fragmentos de conteúdo do Adobe Experience Manager as a Cloud Service permitem projetar, criar, selecionar e usar conteúdo independente da página
translation-type: tm+mt
source-git-commit: be65ba65fb6bbd7634da882ef8337565f1fce477
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 100%

---


# Fragmentos de conteúdo {#content-fragments}

Os Fragmentos de conteúdo no Adobe Experience Manager (AEM) as a Cloud Service são [criados e gerenciados como ativos de página independentes](/help/assets/content-fragments/content-fragments.md).

Eles permitem criar conteúdo não vinculado a canais, juntamente com variações (podem ser específicas de cada canal). Em seguida, é possível usar estes fragmentos e suas variações ao criar suas páginas de conteúdo.

Juntamente com o exportador JSON atualizado, os fragmentos de conteúdo estruturados também podem ser usados para fornecer o conteúdo do AEM através do Content Services a canais diferentes das páginas do AEM.

>[!NOTE]
>
>**Fragmentos de conteúdo** e **[Fragmentos de experiência](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** são recursos diferentes no AEM:
>
>* **Fragmentos de conteúdo** são conteúdos editoriais, principalmente texto e imagens relacionadas. Eles são puro conteúdo, sem design e layout.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado e, portanto, fragmentos de uma página da Web.
>
>Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.

>[!CAUTION]
>
>Esta página deve ser lida junto com a seção [Trabalhar com fragmentos de conteúdo](/help/assets/content-fragments/content-fragments.md) (e páginas relacionadas), pois apresenta a terminologia e os conceitos básicos, além dos processos de criação e de gerenciamento de fragmentos.

Os fragmentos do conteúdo permitem:

* **Estratégia de marketing e campanha**
   * Analise o conteúdo por meio de fragmentos do conteúdo gerenciados centralmente.
* **Creative Pro**
   * Rastreamento de ativos criativos por meio de coleções associadas aos fragmentos do conteúdo.
* **Redatores** 
   * Escreva no editor de fragmento de conteúdo do AEM.
   * É possível criar variações de conteúdo.
   * É possível associar o conteúdo relevante com o fragmento do conteúdo.
   * É possível usar controle de versão/fluxo de trabalho.
   * É possível compartilhar o fragmento de conteúdo.
   * É possível gerenciar traduções centralmente.
* **Produtores e Gerentes de jornada**
   * Selecione de fragmentos e variações predefinidos com a criação no AEM.
   * É possível confiar que o fragmento e o conteúdo associado estejam sempre atualizados, já que os redatores e criadores fazem suas atualizações em fragmentos e ativos centralmente gerenciados.
   * É possível confiar no conteúdo de mídia associado que está sendo preparado para relevância.
   * É possível criar variações de conteúdo ad hoc dinamicamente, ao mesmo tempo, garantir que elas permaneçam gerenciadas centralmente no fragmento.

## Adicionar um fragmento de conteúdo à sua página     {#adding-a-content-fragment-to-your-page}

1. Abra a página para edição. 
2. Adicione o componente **Fragmento de conteúdo**; do navegador **Componentes** ou **Inserir novo componente**. 
3. Você pode:
   * Abra o navegador de **ativos** e filtre por **Fragmentos de conteúdo** (o filtro padrão é por Imagens). Em seguida, arraste o fragmento necessário na instância do componente.
   * Selecione o componente do fragmento de conteúdo e clique em **Configurar** na barra de ferramentas. Na caixa de diálogo, é possível abrir a caixa de diálogo de seleção para procurar e selecionar o **Fragmento de conteúdo** necessário.

   >[!NOTE]
   >
   >Um método alternativo é arrastar um fragmento de conteúdo específico diretamente para a página. Essa ação cria o componente associado (Fragmento de conteúdo) de maneira automática.

4. Inicialmente, o conteúdo do elemento **Principal** e do **Mestre** (variação) serão mostrados. Você pode [selecionar outros elementos e/ou variações](#selecting-the-element-or-variation) conforme necessário.

   ![Fragmentos de conteúdo no navegador de ativos](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >Para mais informações sobre outras funcionalidades de edição, consulte também:
   >
   >* [Layout responsivo](/help/sites-cloud/authoring/features/responsive-layout.md)
   >* [Editar conteúdo da página](/help/sites-cloud/authoring/fundamentals/editing-content.md)


### Selecionar o elemento ou a variação {#selecting-the-element-or-variation}

Abra a caixa de diálogo **Configuração** do fragmento para configurar o fragmento para o uso na página atual. A caixa de diálogo pode depender do componente usado.

>[!NOTE]
>
>Consulte também [Componentes principais, Componente do fragmento de conteúdo](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/components/content-fragment-component.html)

Na caixa de diálogo de configuração apropriada, você pode selecionar os parâmetros disponíveis, incluindo:

* **Fragmento de conteúdo**
   * Especifique o fragmento a ser usado.
* **Modo de exibição**:
   * **Elemento de texto simples**
   * **Vários elementos**
* **Elemento**
   * Dependendo do modelo usado, haverá uma seleção disponível.

   >[!NOTE]
   >
   >Os elementos disponíveis dependem do modelo usado.

* **Variação**
   * O padrão **Mestre** sempre estará disponível.
   * Uma seleção ficará disponível se as variações forem criadas para o fragmento.

* **ID**

   * **Atributo da ID HTML a ser aplicada ao componente.**

### Conexão rápida ao editor de fragmentos     {#quick-connection-to-fragment-editor}

É possível abrir a origem do fragmento para edição (o ativo) usando o ícone **Editar** na barra de ferramentas do componente. Assim, você pode [editar e gerenciar o fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md).

>[!CAUTION]
>
>Como sempre, editar a origem do fragmento afetará todas as páginas que fazem referência a esse fragmento de conteúdo.

### Adicionar conteúdo intermediário     {#adding-in-between-content}

Quando um fragmento de conteúdo específico for adicionado à página, há um espaço reservado para **Arrastar os componentes aqui** entre cada parágrafo HTML (e na parte superior/inferior) do fragmento.

Isso permite adicionar mais conteúdo [intermediário](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments), o conteúdo do fragmento (em qualquer um dos pontos disponíveis), sem precisar alterar o fragmento-raiz.

Para conteúdo intermediário, você pode:

* Adicionar componentes do [navegador Componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
* Adicionar ativos no [Navegador de ativos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
* Usar [Conteúdo associado](#using-associated-content) como uma origem de conteúdo intermediário.

>[!CAUTION]
>
>O conteúdo intermediário é o conteúdo da página. Não é armazenado no fragmento de conteúdo.

![Inserir componente](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>Você também pode [inserir ativos visuais (imagens) ao fragmento propriamente dito](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Os ativos visuais inseridos no fragmento propriamente dito são anexados ao parágrafo anterior no fragmento. Isso significa que não é possível posicionar conteúdo intermediário entre um ativo visual e o parágrafo anterior. Se você precisar desse nível de conexão, pode adicionar a imagem ao fragmento (como [fragmento de mídia mista](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)).

>[!CAUTION]
>
>Depois de adicionar o conteúdo intermediário a um fragmento de conteúdo na página, a alteração da estrutura do fragmento de conteúdo subjacente (ou seja, no editor de fragmentos de conteúdo) pode causar resultados errôneos/inesperados.
>
>Quando isso ocorre, o conteúdo intermediário é mantido como está:
>
>* Os componentes intermediários têm uma posição absoluta na sequência de componentes do fluxo de fragmentos. Essa posição não muda, mesmo quando o conteúdo dos parágrafos no fragmento sofre alteração.
>
>  Isso causa a impressão de que o posicionamento relativo mudou, pois os parágrafos intermediários não têm relacionamento contextual com os parágrafos (fragmento) ao lado dos quais estão posicionados.
>* A menos que as duas estruturas de parágrafo entrem em conflito; nesse caso, o conteúdo intermediário não é exibido (embora ainda esteja presente internamente).


### Usar conteúdo associado     {#using-associated-content}

Se você tiver [conteúdo associado ](/help/assets/content-fragments/content-fragments-assoc-content.md) ao [fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md), esses ativos estarão disponíveis no painel lateral (depois de colocar o fragmento na página de conteúdo). O conteúdo associado é uma fonte especial para [conteúdo intermediário](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments).

>[!NOTE]
>
>Existem vários métodos de adicionar [ativos visuais (por exemplo, imagens)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) ao fragmento e/ou página.

>[!NOTE]
>
>Se você tiver vários fragmentos de conteúdo em uma página, a guia **Conteúdo associado** exibirá os ativos adequados para todos os fragmentos.

Após adicionar um fragmento com conteúdo associado à página, uma nova guia (**Conteúdo associado**) será aberta no painel lateral.

Aqui, é possível arrastar os ativos para o local desejado (para um componente existente ou para a posição desejada onde o componente adequado será criado): 

![Inserção de uma imagem](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### Ativos inseridos no fragmento {#assets-inserted-into-the-fragment}

Se os ativos (por exemplo, imagens) tiverem sido inseridos no próprio fragmento (como [fragmentos de mídia mista](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)), as opções para editar esses ativos no editor de páginas serão limitadas.

Por exemplo, para uma imagem, é possível

* Cortar, girar ou inverter a imagem.
* Adicionar um título ou texto alternativo.
* Especificar um tamanho.
* Configurar o layout.

Outras alterações, como mover, copiar ou excluir, devem ser feitas no editor de fragmentos.

### Publicação {#publishing}

Os fragmentos precisam ser publicados para que possam ser usados em suas páginas da Web publicadas:

* Um fragmento pode ser publicado depois de [ criar o fragmento no console de Ativos](/help/assets/content-fragments/content-fragments-managing.md#publishing-and-referencing-a-fragment).
* Se um *fragmento não publicado* for usado em uma página que está sendo publicada, ele também poderá ser publicado neste momento.
