---
title: Fragmentos de conteúdo
description: Os fragmentos de conteúdo do Adobe Experience Manager as a Cloud Service permitem projetar, criar, preparar e usar conteúdo independente de canal que também pode ser usado ao criar suas páginas.
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
solution: Experience Manager Sites
feature: Authoring, Content Fragments
role: User
source-git-commit: 369f0be002413d164911515349b3e25d33eb8b2f
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 82%

---

# Fragmentos de conteúdo {#content-fragments}

Os fragmentos de conteúdo no Adobe Experience Manager (AEM) as a Cloud Service são [criados e gerenciados como ativos independentes da página](/help/sites-cloud/administering/content-fragments/overview.md), permitindo criar conteúdo não vinculado a canais, juntamente com variações (podem ser específicas de cada canal). Você pode usar esses fragmentos e suas variações ao criar suas páginas de conteúdo.

>[!CAUTION]
>
>Esta página deve ser lida junto com [Trabalho com fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md) (e páginas relacionadas), pois apresenta a terminologia e os conceitos básicos, além de informações sobre como criar e gerenciar fragmentos e fornecer fragmentos de conteúdo estruturados a canais diferentes das páginas do AEM.

>[!NOTE]
>
>Os fragmentos de conteúdo são um recurso do **Sites**, mas são armazenados como **Assets**.
>
>Eles são gerenciados principalmente com o console **[Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)**, embora ainda possam ser gerenciados no console **[Assets](/help/assets/content-fragments/content-fragments-managing.md)**.
>
>O editor padrão de [Fragmentos de conteúdo - Criação](/help/sites-cloud/administering/content-fragments/authoring.md) é o novo editor; acessado do console **Fragmentos de conteúdo** e do console **Assets**.
>
>Para usar o [editor original](/help/assets/content-fragments/content-fragments-variations.md), abra o novo editor e desative a opção **Novo Editor**.

>[!NOTE]
>
>**Fragmentos de conteúdo** e **[fragmentos de experiência](/help/sites-cloud/authoring/fragments/content-fragments.md)** são recursos diferentes no AEM:
>* Os **fragmentos de conteúdo** são conteúdos editoriais com definição e estrutura, mas sem design visual e/ou layout adicional. Eles podem ser usados para acessar dados estruturados, incluindo textos, números, datas, entre outros.
>* **Fragmentos de experiência** são conteúdo totalmente apresentado; um fragmento de uma página da Web.
>
>Fragmentos de experiência podem incluir conteúdo na forma de Fragmentos de conteúdo, mas não o contrário.
>
>Para obter mais informações, consulte [Entenda sobre os fragmentos de conteúdo e fragmentos de experiência do AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=pt-BR).

Os fragmentos de conteúdo habilitam:

* **Estratégias de marketing e campanha**
   * A revisão de conteúdo por meio de fragmentos de conteúdo gerenciados centralmente.
* **Creative Pro**
   * O rastreamento de ativos criativos por meio de coleções associadas aos fragmentos de conteúdo.
* **Redatores**
   * Escreva no editor de fragmento de conteúdo do AEM.
   * A criação de variações de conteúdo.
   * A associação de conteúdos relevantes ao fragmento de conteúdo.
   * O uso do controle de versão/fluxo de trabalho.
   * É possível compartilhar o fragmento de conteúdo.
   * O gerenciamento centralizado de traduções.
* **Produtores e gerentes de jornadas**
   * A seleção de fragmentos e variações predefinidos no processo de criação do AEM.
   * A confiança de que o fragmento e o conteúdo associado estarão sempre atualizados, já que os redatores e criadores fazem suas atualizações em fragmentos e ativos gerenciados centralmente.
   * A confiança de que o conteúdo de mídia associado está sendo preparado por relevância.
   * A criação de variações de conteúdo ad hoc a qualquer momento, garantindo que essas variações continuem sendo gerenciadas centralmente no fragmento.

## Adicionar um fragmento de conteúdo à sua página     {#adding-a-content-fragment-to-your-page}

1. Abra a página para edição.
2. Adicione o componente **Fragmento de conteúdo**; do navegador **Componentes** ou **Inserir novo componente**.
3. Você pode:
   * Abra o navegador de **ativos** e filtre por **Fragmentos de conteúdo** (o filtro padrão é por Imagens). Em seguida, arraste o fragmento necessário para a instância do componente.
   * Selecione o componente do fragmento de conteúdo e clique em **Configurar** na barra de ferramentas. Na caixa de diálogo, é possível abrir a caixa de diálogo de seleção para procurar e selecionar o **Fragmento de conteúdo** necessário.

   >[!NOTE]
   >
   >Um método alternativo é arrastar um fragmento de conteúdo específico diretamente para a página. Essa ação cria o componente associado (Fragmento de conteúdo) de maneira automática.

4. Inicialmente, o conteúdo do elemento **Principal** e do **Mestre** (variação) serão mostrados. Você pode [selecionar outros elementos e/ou variações](#selecting-the-element-or-variation) conforme necessário.

   ![Fragmentos de conteúdo no navegador de ativos](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >Para obter mais informações sobre outras funcionalidades de edição, consulte também:
   >
   >* [Layout responsivo](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
   >* [Editar conteúdo da página](/help/sites-cloud/authoring/page-editor/edit-content.md)

### Selecionar o elemento ou a variação {#selecting-the-element-or-variation}

Abra a caixa de diálogo **Configuração** do fragmento para configurar o fragmento para o uso na página atual. A caixa de diálogo pode variar dependendo do componente usado.

>[!NOTE]
>
>Consulte também [Componentes principais, Componente do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=pt-BR)

Na caixa de diálogo de configuração apropriada, é possível selecionar os parâmetros disponíveis, incluindo:

* **Fragmento de conteúdo**
   * Especificar o fragmento a ser usado.
* **Modo de exibição**:
   * **Elemento de texto simples**
   * **Vários elementos**
* **Elemento**
   * Haverá uma seleção disponível dependendo do modelo usado.

  >[!NOTE]
  >
  >Os elementos disponíveis dependem do modelo usado.

* **Variação**
   * O **Mestre** padrão sempre estará disponível.
   * Uma seleção está disponível se variações forem criadas para o fragmento.

* **ID**

   * **Atributo da ID HTML a ser aplicada ao componente.**

### Conexão rápida ao editor de fragmentos     {#quick-connection-to-fragment-editor}

É possível abrir a origem do fragmento para edição (o ativo) usando o ícone **Editar** na barra de ferramentas do componente. Assim, você pode [editar e gerenciar o fragmento de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md).

>[!CAUTION]
>
>Como sempre, editar a origem do fragmento afetará todas as páginas que fazem referência a esse fragmento de conteúdo.

### Adicionar conteúdo intermediário     {#adding-in-between-content}

Quando um fragmento de conteúdo específico for adicionado à página, haverá um espaço reservado para **Arraste os componentes aqui** entre cada parágrafo HTML (e na parte superior/inferior) do fragmento.

Isso permite adicionar conteúdo extra [ao meio (ou seja, conteúdo intermediário)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) ao conteúdo do fragmento (em qualquer um dos pontos disponíveis), sem precisar alterar o fragmento raiz.

Quanto ao conteúdo intermediário, é possível:

* Adicionar componentes do [Navegador de componentes](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)
* Adicionar ativos do [navegador Assets](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser)
* Usar [Conteúdo associado](#using-associated-content) como uma origem de conteúdo intermediário.

>[!CAUTION]
>
>O conteúdo intermediário é o conteúdo da página. Ele não é armazenado no fragmento de conteúdo.

![Inserir componente](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>Também é possível [inserir ativos visuais (imagens) no próprio fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Os ativos visuais inseridos no próprio fragmento de conteúdo são anexados ao parágrafo anterior do fragmento. Isso significa que não é possível posicionar conteúdo intermediário entre um ativo visual e o parágrafo anterior. Se você precisar desse nível de conexão, pode adicionar a imagem ao fragmento (como [fragmento de mídia mista](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)).

>[!CAUTION]
>
>Após adicionar conteúdo intermediário a um fragmento de conteúdo em sua página, alterar a estrutura do fragmento de conteúdo subjacente (ou seja, no editor de fragmentos de conteúdo) pode levar a resultados errôneos/inesperados.
>
>Quando isso ocorre, o conteúdo intermediário é mantido como está:
>
>* Os componentes intermediários têm uma posição absoluta dentro da sequência de componentes no fluxo de fragmentos. Essa posição não muda, mesmo quando o conteúdo dos parágrafos do fragmento é alterado.
>
>  Isso causa a impressão de que o posicionamento relativo mudou, pois os parágrafos intermediários não têm relacionamento contextual com os parágrafos (fragmento) ao lado dos quais estão posicionados.
>* A menos que as duas estruturas de parágrafo entrem em conflito; nesse caso, o conteúdo intermediário não é exibido (embora ainda esteja presente internamente).

### Usar conteúdo associado     {#using-associated-content}

Se tiver [conteúdo associado &#x200B;](/help/assets/content-fragments/content-fragments-assoc-content.md) ao [fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md), esses arquivos estarão disponíveis no painel lateral (após colocar o fragmento na página de conteúdo). O conteúdo associado é essencialmente uma fonte especial de conteúdo para [conteúdo intermediário](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments).

>[!NOTE]
>
>Há vários métodos de adicionar [ativos visuais (por exemplo, imagens)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) ao fragmento e/ou página.

>[!NOTE]
>
>Se você tiver vários fragmentos de conteúdo em uma página, a guia **Conteúdo associado** mostrará os ativos adequados para todos os fragmentos.

Após adicionar um fragmento com conteúdo associado à página, uma nova guia (**Conteúdo associado**) é aberta no painel lateral.

Aqui, é possível arrastar os arquivos para o local desejado (seja para um componente já existente ou para a posição desejada onde o componente adequado será criado): 

![Inserção de uma imagem](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### Ativos inseridos no fragmento {#assets-inserted-into-the-fragment}

Se os ativos (por exemplo, imagens) tiverem sido inseridos no próprio fragmento (como [fragmentos de mídia mista](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)), as opções para editar esses ativos no editor de páginas serão limitadas.

Por exemplo, para uma imagem, é possível

* Cortar, girar ou virar a imagem.
* Adicionar um título ou texto alternativo.
* Especificar um tamanho.
* Também é possível configurar o layout.

Outras alterações, como mover, copiar ou excluir, devem ser feitas no editor de fragmentos.

### Publicação {#publishing}

Os fragmentos precisam ser publicados para que possam ser usados em suas páginas da Web publicadas:

* Um fragmento pode ser publicado depois de [criado no console de Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment).
* Se um *fragmento não publicado* for usado em uma página que está sendo publicada, ele também poderá ser publicado neste momento.

## Exportar fragmentos de conteúdo {#exporting-content-fragments}

Para exportar para o Adobe Target, o JSON pode ser usado para entregar o fragmento. Consulte:

* [Integração com o Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Exportar fragmentos de conteúdo para o Adobe Target](/help/sites-cloud/integrating/content-fragments-target.md)
