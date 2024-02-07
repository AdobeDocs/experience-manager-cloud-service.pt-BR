---
title: Modelagem de conteúdo para criação no AEM com projetos Edge Delivery Services
description: Saiba como a modelagem de conteúdo funciona para a criação de AEM com projetos Edge Delivery Services e como modelar seu próprio conteúdo.
source-git-commit: 8f3c7524ae8ee642a9aee5989e03e6584a664eba
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 1%

---


# Modelagem de conteúdo para criação no AEM com projetos Edge Delivery Services {#content-modeling}

Saiba como a modelagem de conteúdo funciona para a criação de AEM com projetos Edge Delivery Services e como modelar seu próprio conteúdo.

{{aem-authoring-edge-early-access}}

## Pré-requisitos {#prerequisites}

Os projetos que usam a criação de AEM com Edge Delivery Services herdam a maioria dos mecanismos de qualquer outro projeto Edge Delivery Services, independentemente da fonte de conteúdo ou [método de criação.](/help/edge/authoring.md)

Antes de começar a modelar o conteúdo para seu projeto, primeiro leia a documentação a seguir.

* [Introdução - Tutorial do desenvolvedor](/help/edge/developer/tutorial.md)
* [Marcação, Seções, Blocos e Bloqueio automático](/help/edge/developer/markup-sections-blocks.md)
* [Bloquear coleção](/help/edge/developer/block-collection.md)

É essencial compreender esses conceitos para criar um modelo de conteúdo atraente que funcione de forma independente da origem do conteúdo. Este documento fornece detalhes sobre os mecanismos implementados especificamente para a criação do AEM.

## Conteúdo padrão {#default-content}

**Conteúdo padrão** É um conteúdo que um autor intuitivamente colocaria em uma página sem adicionar nenhuma semântica adicional. Isso inclui texto, cabeçalhos, links e imagens. Esse conteúdo é autoexplicativo em sua função e propósito.

No AEM, esse conteúdo é implementado como componentes com modelos muito simples e predefinidos, que incluem tudo o que pode ser serializado no Markdown e no HTML.

* **Texto**: Rich text (incluindo elementos de lista e texto forte ou em itálico)
* **Título**: Texto, tipo (c1-c6)
* **Imagem**: Origem, descrição
* **Botão**: texto, título, url, tipo (padrão, primário, secundário)

O modelo desses componentes faz parte da [Boilerplate para criação de AEM com Edge Delivery Services.](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112)

## Blocos {#blocks}

Os blocos são usados para criar conteúdo mais rico com estilos e funcionalidades específicas. Ao contrário do conteúdo padrão, os blocos exigem semântica adicional. Blocos podem ser comparados a [componentes no editor de página AEM.](/help/implementing/developing/components/overview.md)

Os blocos são essencialmente pedaços de conteúdo decorados pelo JavaScript e estilizados com uma folha de estilos.

### Definição do modelo de bloco {#model-definition}

Ao usar a criação do AEM com o Edge Delivery Services, o conteúdo dos blocos deve ser modelado explicitamente para fornecer ao autor a interface para criar conteúdo. Basicamente, é necessário criar um modelo para que a interface do usuário de criação saiba quais opções apresentar ao autor com base no bloco.

A variável [`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) file define o modelo de blocos. Os campos definidos no modelo de componente são mantidos como propriedades no AEM e renderizados como células na tabela que compõe um bloco.

```json
{
  "id": "hero",
  "fields": [
    {
      "component": "reference",
      "valueType": "string",
      "name": "image",
      "label": "Image",
      "multi": false
    },
    {
      "component": "text-input",
      "valueType": "string",
      "name": "imageAlt",
      "label": "Alt",
      "value": ""
    },
    {
      "component": "text-area",
      "name": "text",
      "value": "",
      "label": "Text",
      "valueType": "string"
    }
  ]
}
```

Observe que nem todos os blocos devem ter um modelo. Alguns blocos são simplesmente [contêineres](#container) para uma lista de filhos, onde cada filho tem seu próprio modelo.

Também é necessário definir quais blocos existem e quais podem ser adicionados a uma página usando o Editor universal. A variável [`component-definitions.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) arquivo lista os componentes à medida que são disponibilizados pelo Universal Editor.

```json
{
  "title": "Hero",
  "id": "hero",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "Hero",
          "model": "hero"
        }
      }
    }
  }
}
```

É possível usar um modelo para muitos blocos. Por exemplo, alguns blocos podem compartilhar um modelo que define um texto e uma imagem.

Para cada bloco, o desenvolvedor:

* Deve usar o `core/franklin/components/block/v1/block` tipo de recurso, a implementação genérica da lógica de bloco no AEM.
* É necessário definir o nome do bloco, que será renderizado no cabeçalho da tabela do bloco.
* Pode definir um [ID do modelo.](/help/implementing/universal-editor/field-types.md#model-structure)
* Pode definir um [ID do filtro.](/help/implementing/universal-editor/customizing.md#filtering-components)

Todas essas informações são armazenadas no AEM quando um bloco é adicionado a uma página.

>[!WARNING]
>
>Embora possível, não é necessário implementar componentes personalizados de AEM. Os componentes para Edge Delivery Services fornecidos pelo AEM são suficientes e oferecem certos painéis de proteção para facilitar o desenvolvimento.
>
>Por esse motivo, o Adobe não recomenda usar tipos de recursos AEM personalizados.

### Estrutura de blocos {#block-structure}

As propriedades dos blocos são [definido nos modelos de componente](#model-definition) e persistiu como tal no AEM. As propriedades são renderizadas como células na estrutura semelhante à tabela do bloco.

#### Blocos simples {#simple}

Na forma mais simples, um bloco renderiza cada propriedade em uma única linha/coluna na ordem em que as propriedades são definidas no modelo.

No exemplo a seguir, a imagem é definida primeiro no modelo e o texto em segundo lugar. Assim, eles são renderizados com a imagem em primeiro lugar e o texto em segundo lugar.

##### Dados {#data-simple}

```json
{
  "name": "Hero",
  "model": "hero",
  "image": "/content/dam/image.png",
  "imageAlt": "Helix - a shape like a corkscrew",
  "text": "<h1>Welcome to AEM</h1>"
}
```

##### Marcação {#markup-simple}

```html
<div class="hero">
  <div>
    <div>
      <picture>
        <img src="/content/dam/image.png" alt="Helix - a shape like a corkscrew">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <h1>Welcome to AEM</h1>
    </div>
  </div>
</div>
```

Observe que alguns tipos de valores permitem inferir a semântica na marcação e as propriedades são combinadas em em células únicas. Esse comportamento é descrito na seção [Digite Inferência.](#type-inference)

#### Bloco de valor-chave {#key-value}

Em muitos casos, é recomendável decorar a marcação semântica renderizada, adicionar nomes de classe CSS, adicionar novos nós ou movê-los no DOM e aplicar estilos.

Em outros casos, no entanto, o bloco é lido como uma configuração de par de valores chave.

Um exemplo disso é o [metadados da seção.](/help/edge/developer/markup-sections-blocks.md#sections) Nesse caso de uso, o bloco pode ser configurado para renderizar como uma tabela de pares de valores chave. Consulte a seção [Seções e metadados de seção](#sections-metadata) para obter mais informações.

##### Dados {#data-key-value}

```json
{
  "name": "Featured Articles",
  "model": "spreadsheet-input",
  "key-value": true,
  "source": "/content/site/articles.json",
  "keywords": ['Developer','Courses'],
  "limit": 4
}
```

##### Marcação {#markup-key-value}

```html
<div class="featured-articles">
  <div>
    <div>source</div>
    <div><a href="/content/site/articles.json">/content/site/articles.json</a></div>
  </div>
  <div>
    <div>keywords</div>
    <div>Developer,Courses</div>
  <div>
  <div>
    <div>limit</div>
    <div>4</div>
  </div>
</div>
```

#### Blocos de contêiner {#container}

Ambas as estruturas anteriores têm uma única dimensão: a lista de propriedades. Os blocos de contêiner permitem adicionar filhos (geralmente do mesmo tipo ou modelo) e, portanto, são bidimensionais. Esses blocos ainda suportam suas próprias propriedades renderizadas como linhas com uma única coluna primeiro. Mas também permitem adicionar filhos, para os quais cada item é renderizado como linha e cada propriedade como coluna dentro dessa linha.

No exemplo a seguir, um bloco aceita uma lista de ícones vinculados como filhos, onde cada ícone vinculado tem uma imagem e um link. Observe a [ID do filtro](/help/implementing/universal-editor/customizing.md#filtering-components) definido nos dados do bloco para fazer referência à configuração de filtro.

##### Dados {#data-container}

```json
{
  "name": "Our Partners",
  "model": "text-only",
  "filter": "our-partners",
  "text": "<p>Our community of partners is ...</p>",
  "item_0": {
    "model": "linked-icon",
    "image": "/content/dam/partners/foo.png",
    "imageAlt": "Icon of Foo",
    "link": "https://foo.com/"
  },
  "item_1": {
    "model": "linked-icon"
    "image": "/content/dam/partners/bar.png",
    "imageAlt": "Icon of Bar",
    "link": "https://bar.com"
  }
}
```

##### Marcação {#markup-container}

```html
<div class="our-partners">
  <div>
    <div>
        Our community of partners is ...
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/foo.png" alt="Icon of Foo">
      </picture>
    </div>
    <div>
      <a href="https://foo.com">https://foo.com</a>
    </div>
  </div>
  <div>
    <div>
      <picture>
         <img src="/content/dam/partners/bar.png" alt="Icon of Bar">
      </picture>
    </div>
    <div>
      <a href="https://bar.com">https://bar.com</a>
    </div>
  </div>
</div>
```

### Criação de modelos de conteúdo semântico para blocos {#creating-content-models}

Com o [mecânica da estrutura do bloco explicada,](#block-structure) é possível criar um modelo de conteúdo que mapeie o conteúdo persistente no AEM de um para um para o nível de entrega.

No início de cada projeto, um modelo de conteúdo deve ser cuidadosamente considerado para cada bloco. Ele deve ser agnóstico em relação à fonte de conteúdo e à experiência de criação para permitir que os autores os alternem ou combinem ao reutilizar implementações e estilos de bloco. Mais detalhes e orientações gerais podem ser encontrados em [Modelo de David (tomada 2).](https://www.aem.live/docs/davidsmodel) Mais especificamente, a [coleção de blocos](/help/edge/developer/block-collection.md) O contém um conjunto abrangente de modelos de conteúdo para casos de uso específicos de padrões comuns de interface do usuário.

Para a criação do AEM com o Edge Delivery Services, isso levanta a questão de como fornecer um modelo atraente de conteúdo semântico quando as informações são criadas com formulários compostos por vários campos, em vez de editar a marcação semântica no contexto, como um rich text.

Para resolver esse problema, há três métodos que facilitam a criação de um modelo de conteúdo atraente:

* [Inferência de tipo](#type-inference)
* [Recolher Campo](#field-collapse)
* [Agrupamento de elementos](#element-grouping)

>[!NOTE]
>
>As implementações de bloco podem desconstruir o conteúdo e substituir o bloco por um DOM renderizado pelo lado do cliente. Embora isso seja possível e intuitivo para um desenvolvedor, não é a prática recomendada para os Edge Delivery Services.

#### Inferência de tipo {#type-inference}

Para alguns valores, podemos inferir o significado semântico a partir dos próprios valores. Esses valores incluem:

* **Imagens** - Se uma referência a um recurso no AEM for um ativo com um tipo MIME que comece com `image/`, a referência é renderizada como `<picture><img src="${reference}"></picture>`.
* **Links** - Se uma referência existe no AEM e não é uma imagem, ou se o valor começa com `https?://`  ou `#`, a referência é renderizada como `<a href="${reference}">${reference}</a>` .
* **Rich Text** - Se um valor aparado começar com um parágrafo (`p`, `ul`, `ol`, `h1`-`h6`, etc.), o valor será renderizado como rich text.
* **Nomes de classe** - A `classes` é tratada como opções de bloco e renderizada no cabeçalho da tabela para [blocos simples,](#simple) ou como lista de valores para itens em uma [bloco de contêiner.](#container)
* **Listas de valores** - Se um valor for uma propriedade de vários valores e o primeiro valor não for nenhum dos anteriores, todos os valores serão concatenados como uma lista separada por vírgulas.

Todo o resto será renderizado como texto simples.

#### Recolher Campo {#field-collapse}

O recolhimento de campo é o mecanismo que combina vários valores de campo em um único elemento semântico com base em uma convenção de nomenclatura usando os sufixos `Title`, `Type`, `Alt`, e `Text` (todas diferenciam maiúsculas de minúsculas). Qualquer propriedade que termine com qualquer um desses sufixos não será considerada um valor, mas como um atributo de outra propriedade.

##### Imagens {#image-collapse}

###### Dados {#data-image}

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

###### Marcação {#markup-image}

```html
<picture>
  <img src="/content/dam/red-car.png" alt="A red car on a road">
</picture>
```

##### Links e botões {#links-buttons-collapse}

###### Dados {#data-links-buttons}

```json
{
  "link": "https://www.adobe.com",
  "linkTitle": "Navigate to adobe.com",
  "linkText": "adobe.com",
  "linkType": "primary"
}
```

###### Marcação {#markup-links-buttons}

Não `linkType`ou `linkType=default`

```html
<a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
```

`linkType=primary`

```html
<strong>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</strong>
```

`linkType=secondary`

```html
<em>
  <a href="https://www.adobe.com" title="Navigate to adobe.com">adobe.com</a>
</em>
```

##### Cabeçalhos {#headings-collapse}

###### Dados {#data-headings}

```json
{
  "heading": "Getting started",
  "headingType": "h2"
}
```

###### Marcação {#markup-headings}

```html
<h2>Getting started</h2>
```

#### Agrupamento de elementos {#element-grouping}

Enquanto [recolher campo](#field-collapse) é sobre combinar várias propriedades em um único elemento semântico, o agrupamento de elementos é sobre concatenar vários elementos semânticos em uma única célula. Isso é particularmente útil para casos de uso em que o autor deve ser restrito no tipo e no número de elementos que pode criar.

Por exemplo, o autor deve criar apenas um subtítulo, título e uma única descrição de parágrafo combinada com no máximo dois botões de chamada para ação. O agrupamento desses elementos produz uma marcação semântica que pode ser estilizada sem mais ações.

##### Dados {#data-grouping}

```json
{
  "name": "teaser",
  "model": "teaser",
  "image": "/content/dam/teaser-background.png",
  "imageAlt": "A group of people sitting on a stage",
  "teaserText_subtitle": "Adobe Experience Cloud"
  "teaserText_title": "Meet the Experts"
  "teaserText_titleType": "h2"
  "teaserText_description": "<p>Join us in this ask me everything session...</p>"
  "teaserText_cta1": "https://link.to/more-details",
  "teaserText_cta1Text": "More Details"
  "teaserText_cta2": "https://link.to/sign-up",
  "teaserText_cta2Text": "RSVP",
  "teaserText_cta2Type": "primary"
}
```

##### Marcação {#markup-grouping}

```html
<div class="teaser">
  <div>
    <div>
      <picture>
        <img src="/content/dam/teaser-background.png" alt="A group of people sitting on a stage">
      </picture>
    </div>
  </div>
  <div>
    <div>
      <p>Adobe Experience Cloud</p>
      <h2>Meet the Experts</h2>
      <p>Join us in this ask me everything session ...</p>
      <p><a href="https://link.to/more-details">More Details</a></p>
      <p><strong><a href="https://link.to/sign-up">RSVP</a></strong></p>
    </div>
  </div>
</div>
```

## Seções e metadados de seção {#sections-metadata}

Da mesma forma que um desenvolvedor pode definir e modelar vários [blocos,](#blocks) eles podem definir diferentes seções.

O modelo de conteúdo do Edge Delivery Services permite deliberadamente apenas um único nível de aninhamento, ou seja, qualquer conteúdo ou bloco padrão contido em uma seção. Isso significa que, para ter componentes visuais mais complexos que possam conter outros componentes, eles precisam ser modelados como seções e combinados juntos usando o bloqueio automático do lado do cliente. Exemplos típicos disso são abas e seções recolhíveis, como acordeões.

Uma seção pode ser definida da mesma forma que um bloco, mas com o tipo de recurso de `core/franklin/components/section/v1/section`. As seções podem ter um nome e um [ID do filtro,](/help/implementing/universal-editor/customizing.md#filtering-components) que são utilizados pela [Editor universal](/help/implementing/universal-editor/introduction.md) apenas, bem como uma [ID do modelo,](/help/implementing/universal-editor/field-types.md#model-structure) que é usado para renderizar os metadados da seção. O modelo é, dessa forma, o modelo do bloco de metadados da seção, que será anexado automaticamente a uma seção como bloco de valor principal se não estiver vazio.

A variável [ID do modelo](/help/implementing/universal-editor/field-types.md#model-structure) e [ID do filtro](/help/implementing/universal-editor/customizing.md#filtering-components) da seção padrão é `section`. Ela pode ser usada para alterar o comportamento da seção padrão. O exemplo a seguir adiciona alguns estilos e e uma imagem de plano de fundo ao modelo de metadados da seção.

```json
{
  "id": "section",
  "fields": [
    {
      "component": "multiselect",
      "name": "style",
      "value": "",
      "label": "Style",
      "valueType": "string",
      "options": [
        {
          "name": "Fade in Background",
          "value": "fade-in"
        },
        {
          "name": "Highlight",
          "value": "highlight"
        }
      ]
    },
    {
      "component": "reference",
      "valueType": "string",
      "name": "background",
      "label": "Image",
      "multi": false
    }
  ]
}
```

O exemplo a seguir define uma seção de guia, que pode ser usada para criar um bloco de guias combinando seções consecutivas com um atributo de dados de título de guia em um bloco de guias durante o bloqueio automático.

```json
{
  "title": "Tab",
  "id": "tab",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/section/v1/section",
        "template": {
          "name": "Tab",
          "model": "tab",
          "filter": "section"
        }
      }
    }
  }
}
```

## Metadados de página {#page-metadata}

Os documentos podem ter uma página [bloco de metadados,](/help/edge/authoring.md#metadata--seo) que é usado para definir qual `<meta>` os elementos são renderizados na variável `<head>` de uma página. As propriedades de página das páginas no AEM são mapeadas de forma as a Cloud Service para aquelas que estão disponíveis prontas para uso para Edge Delivery Services, como `title`, `description`, `keywords`, etc.

Antes de explorar mais detalhadamente como definir seus próprios metadados, revise os documentos a seguir para entender o conceito de metadados da página primeiro.

* [Metadados](https://www.aem.live/developer/block-collection/metadata)
* [Metadados em massa](/help/edge/docs/bulk-metadata.md)

Também é possível definir metadados de página adicionais de duas maneiras.

### Planilhas de metadados {#metadata-spreadsheets}

É possível definir metadados por caminho ou por padrão de caminho de maneira semelhante a uma tabela no AEM as a Cloud Service. Há uma interface de criação para dados semelhantes a tabelas disponíveis semelhante ao Excel ou ao Google Sheets.

Para criar essa tabela, crie uma página e use o modelo de Metadados no console Sites.

>[!NOTE]
>
>Ao editar a planilha de metadados, alterne para **Visualizar** já que a criação ocorre na própria página, não no editor.

Nas propriedades de página da planilha, defina os campos de metadados necessários junto com o URL. Em seguida, adicione metadados por caminho de página ou padrão de caminho de página, em que o campo de URL está relacionado aos caminhos públicos mapeados, e não ao caminho de conteúdo no AEM.

Verifique se a planilha foi adicionada ao mapeamento de caminho antes de publicá-la.

```text
mappings:
  - /content/site/:/
  - /content/site/metadata:/metadata.json
```

### Propriedades da página {#page-properties}

Também é possível definir um modelo de componente para os metadados da página, que serão disponibilizados para o autor como uma guia da caixa de diálogo de propriedades da página do AEM Sites.

Para fazer isso, crie um modelo de componente com a ID `page-metadata`.

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text-input",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

Há alguns nomes de campo que têm um significado especial e serão ignorados ao servir a interface da caixa de diálogo de criação:

* **`cq:tags`** - Por padrão, `cq:tags` não são adicionados aos metadados. Adicionando-os à `page-metadata` adicionará as IDs de tag como uma lista separada por vírgulas como um `tags` meta tag no cabeçalho.
* **`cq:lastModified`** - `cq:lastModified` adicionará seus dados como `last-modified` na cabeça.
