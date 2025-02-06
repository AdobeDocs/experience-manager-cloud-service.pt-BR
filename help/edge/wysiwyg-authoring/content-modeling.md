---
title: Modelagem de conteúdo para criação no WYSIWYG com projetos Edge Delivery Services
description: Saiba como a modelagem de conteúdo funciona para a criação de WYSIWYG com projetos Edge Delivery Services e como modelar seu próprio conteúdo.
exl-id: e68b09c5-4778-4932-8c40-84693db892fd
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '2195'
ht-degree: 0%

---


# Modelagem de conteúdo para criação no WYSIWYG com projetos Edge Delivery Services {#content-modeling}

Saiba como a modelagem de conteúdo funciona para a criação de WYSIWYG com projetos Edge Delivery Services e como modelar seu próprio conteúdo.

## Pré-requisitos {#prerequisites}

Os projetos que usam a Criação de WYSIWYG com Edge Delivery Services herdam a maioria dos mecanismos de qualquer outro projeto Edge Delivery Services, independentemente da fonte de conteúdo ou do [método de criação](/help/edge/wysiwyg-authoring/authoring.md).

Antes de começar a modelar o conteúdo para seu projeto, primeiro leia a documentação a seguir.

* [Introdução - Tutorial do desenvolvedor](/help/edge/developer/tutorial.md)
* [Marcação, Seções, Blocos e Bloqueio automático](/help/edge/developer/markup-sections-blocks.md)
* [Bloquear coleção](/help/edge/developer/block-collection.md)

É essencial compreender esses conceitos para criar um modelo de conteúdo atraente que funcione de forma independente da origem do conteúdo. Este documento fornece detalhes sobre os mecanismos implementados especificamente para a criação do WYSIWYG.

## Conteúdo padrão {#default-content}

**O conteúdo padrão** é o conteúdo que um autor intuitivamente colocaria em uma página sem adicionar nenhuma semântica adicional. Isso inclui texto, cabeçalhos, links e imagens. Esse conteúdo é autoexplicativo em sua função e propósito.

No AEM, esse conteúdo é implementado como componentes com modelos muito simples e predefinidos, que incluem tudo o que pode ser serializado no Markdown e no HTML.

* **Texto**: Rich text (incluindo elementos de lista e texto forte ou itálico)
* **Título**: texto, tipo (h1-h6)
* **Imagem**: Source, descrição
* **Botão**: texto, título, url, tipo (padrão, primário, secundário)

O modelo desses componentes faz parte da [Estrutura para criação do WYSIWYG com Edge Delivery Services](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json#L2-L112).

## Blocos {#blocks}

Os blocos são usados para criar conteúdo mais rico com estilos e funcionalidades específicas. Ao contrário do conteúdo padrão, os blocos exigem semântica adicional.

Os blocos são essencialmente pedaços de conteúdo decorados pelo JavaScript e estilizados com uma folha de estilos.

### Definição do modelo de bloco {#model-definition}

Ao usar a criação do WYSIWYG com o Edge Delivery Services, o conteúdo dos blocos deve ser modelado explicitamente para fornecer ao autor a interface para criar conteúdo. Basicamente, é necessário criar um modelo para que a interface do usuário de criação saiba quais opções apresentar ao autor com base no bloco.

O arquivo [`component-models.json`](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-models.json) define o modelo de blocos. Os campos definidos no modelo de componente são mantidos como propriedades no AEM e renderizados como células na tabela que compõe um bloco.

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

Observe que nem todos os blocos devem ter um modelo. Alguns blocos são simplesmente [containers](#container) para uma lista de filhos, onde cada filho tem seu próprio modelo.

Também é necessário definir quais blocos existem e quais podem ser adicionados a uma página usando o Editor universal. O arquivo [`component-definitions.json`](/help/implementing/universal-editor/component-definition.md) lista os componentes à medida que são disponibilizados pelo Editor Universal.

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

* É necessário usar o tipo de recurso `core/franklin/components/block/v1/block`, a implementação genérica da lógica de bloqueio no AEM.
* É necessário definir o nome do bloco, que será renderizado no cabeçalho da tabela do bloco.
   * O nome do bloco é usado para buscar o estilo e o script corretos para decorar o bloco.
* Pode definir um [ID de modelo](/help/implementing/universal-editor/field-types.md#model-structure).
   * A ID do modelo é uma referência ao modelo do componente, que define os campos disponíveis para o autor no painel de propriedades.
* Pode definir uma [ID de filtro](/help/implementing/universal-editor/filtering.md).
   * A ID do filtro é uma referência ao filtro do componente, que permite alterar o comportamento de criação, por exemplo, limitando quais filhos podem ser adicionados ao bloco ou seção, ou quais recursos de RTE estão habilitados.

Todas essas informações são armazenadas no AEM quando um bloco é adicionado a uma página. Se o tipo de recurso ou o nome do bloco estiver ausente, o bloco não será renderizado na página.

>[!WARNING]
>
>Embora possível, não é necessário ou recomendado implementar componentes personalizados do AEM. Os componentes para Edge Delivery Services fornecidos pelo AEM são suficientes e oferecem certos painéis de proteção para facilitar o desenvolvimento.
>
>Os componentes fornecidos pelo AEM renderizam uma marcação que pode ser consumida por [helix-html2md](https://github.com/adobe/helix-html2md) ao publicar no Edge Delivery Services e por [aem.js](https://github.com/adobe/aem-boilerplate/blob/main/scripts/aem.js) ao carregar uma página no Editor Universal. A marcação é o contrato estável entre o AEM e as outras partes do sistema e não permite personalizações. Por esse motivo, os projetos não devem alterar os componentes e não devem usar componentes personalizados.

### Estrutura de blocos {#block-structure}

As propriedades dos blocos são [definidas nos modelos de componentes](#model-definition) e persistem como tal no AEM. As propriedades são renderizadas como células na estrutura semelhante à tabela do bloco.

#### Blocos simples {#simple}

Na forma mais simples, um bloco renderiza cada propriedade em uma única linha/coluna na ordem em que as propriedades são definidas no modelo.

No exemplo a seguir, a imagem é definida primeiro no modelo e o texto em segundo lugar. Assim, eles são renderizados com a imagem em primeiro lugar e o texto em segundo lugar.

>[!BEGINTABS]

>[!TAB Dados]

```json
{
  "name": "Hero",
  "model": "hero",
  "image": "/content/dam/image.png",
  "imageAlt": "Helix - a shape like a corkscrew",
  "text": "<h1>Welcome to AEM</h1>"
}
```

>[!TAB Marcação]

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

>[!TAB Tabela]

```text
+---------------------------------------------+
| Hero                                        |
+=============================================+
| ![Helix - a shape like a corkscrew][image0] |
+---------------------------------------------+
| # Welcome to AEM                            |
+---------------------------------------------+
```

>[!ENDTABS]

Observe que alguns tipos de valores permitem inferir a semântica na marcação e as propriedades são combinadas em em células únicas. Este comportamento é descrito na seção [Inferência de Tipo](#type-inference).

#### Bloco de valor-chave {#key-value}

Em muitos casos, é recomendável decorar a marcação semântica renderizada, adicionar nomes de classe CSS, adicionar novos nós ou movê-los no DOM e aplicar estilos.

Em outros casos, no entanto, o bloco é lido como uma configuração de par de valores chave.

Um exemplo disso são os [metadados de seção](/help/edge/developer/markup-sections-blocks.md#sections). Nesse caso de uso, o bloco pode ser configurado para renderizar como uma tabela de pares de valores chave. Consulte a seção [Seções e metadados da seção](#sections-metadata) para obter mais informações.

>[!BEGINTABS]

>[!TAB Dados]

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

>[!TAB Marcação]

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

>[!TAB Tabela]

```text
+-----------------------------------------------------------------------+
| Featured Articles                                                     |
+=======================================================================+
| source   | [/content/site/articles.json](/content/site/articles.json) |
+-----------------------------------------------------------------------+
| keywords | Developer,Courses                                          |
+-----------------------------------------------------------------------+
| limit    | 4                                                          |
+-----------------------------------------------------------------------+
```

>[!ENDTABS]

#### Blocos de contêiner {#container}

Ambas as estruturas anteriores têm uma única dimensão: a lista de propriedades. Os blocos de contêiner permitem adicionar filhos (geralmente do mesmo tipo ou modelo) e, portanto, são bidimensionais. Esses blocos ainda suportam suas próprias propriedades renderizadas como linhas com uma única coluna primeiro. Mas também permitem adicionar filhos, para os quais cada item é renderizado como linha e cada propriedade como coluna dentro dessa linha.

No exemplo a seguir, um bloco aceita uma lista de ícones vinculados como filhos, onde cada ícone vinculado tem uma imagem e um link. Observe a [ID de filtro](/help/implementing/universal-editor/filtering.md) definida nos dados do bloco para fazer referência à configuração de filtro.

>[!BEGINTABS]

>[!TAB Dados]

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

>[!TAB Marcação]

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

>[!TAB Tabela]

```text
+------------------------------------------------------------ +
| Our Partners                                                |
+=============================================================+
| Our community of partners is ...                            |
+-------------------------------------------------------------+
| ![Icon of Foo][image0] | [https://foo.com](https://foo.com) |
+-------------------------------------------------------------+
| ![Icon of Bar][image1] | [https://bar.com](https://bar.com) |
+-------------------------------------------------------------+
```

>[!ENDTABS]

### Criação de modelos de conteúdo semântico para blocos {#creating-content-models}

Com a [mecânica da estrutura de blocos explicada](#block-structure), é possível criar um modelo de conteúdo que mapeie o conteúdo persistente do AEM de um para um para a camada de entrega.

No início de cada projeto, um modelo de conteúdo deve ser cuidadosamente considerado para cada bloco. Ele deve ser agnóstico em relação à fonte de conteúdo e à experiência de criação para permitir que os autores os alternem ou combinem ao reutilizar implementações e estilos de bloco. Mais detalhes e orientações gerais podem ser encontrados no [Modelo de David (take 2)](https://www.aem.live/docs/davidsmodel). Mais especificamente, a [coleção de blocos](/help/edge/developer/block-collection.md) contém um conjunto extenso de modelos de conteúdo para casos de uso específicos de padrões comuns de interface do usuário.

Para a criação de WYSIWYG com Edge Delivery Services, isso levanta a questão de como fornecer um modelo atraente de conteúdo semântico quando as informações são criadas com formulários compostos por vários campos, em vez de editar a marcação semântica no contexto, como um rich text.

Para resolver esse problema, há três métodos que facilitam a criação de um modelo de conteúdo atraente:

* [Inferência de tipo](#type-inference)
* [Recolher Campo](#field-collapse)
* [Agrupamento de elementos](#element-grouping)

>[!NOTE]
>
>As implementações de bloco podem desconstruir o conteúdo e substituir o bloco por um DOM renderizado pelo lado do cliente. Embora isso seja possível e intuitivo para um desenvolvedor, não é a prática recomendada para os Edge Delivery Services.

#### Inferência de tipo {#type-inference}

Para alguns valores, podemos inferir o significado semântico a partir dos próprios valores. Esses valores incluem:

* **Imagens** - Se uma referência a um recurso no AEM for um ativo com um tipo MIME começando com `image/`, a referência será renderizada como `<picture><img src="${reference}"></picture>`.
* **Links** - Se uma referência existir no AEM e não for uma imagem, ou se o valor começar com `https?://` ou `#`, a referência será renderizada como `<a href="${reference}">${reference}</a>`.
* **Rich Text** - Se um valor aparado começa com um parágrafo (`p`, `ul`, `ol`, `h1`-`h6`, etc.), o valor é renderizado como rich text.
* **Nomes de Classe** - A propriedade `classes` é tratada como [opções de bloco](/help/edge/developer/markup-sections-blocks.md#block-options) e renderizada no cabeçalho da tabela para [blocos simples](#simple), ou como lista de valores para itens em um [bloco de contêiner](#container). É útil se você deseja [estilizar um bloco de forma diferente](/help/edge/wysiwyg-authoring/create-block.md#block-options), mas não precisa criar um bloco totalmente novo.
* **Listas de Valores** - Se um valor for uma propriedade de vários valores e o primeiro valor não for nenhum dos anteriores, todos os valores serão concatenados como uma lista separada por vírgulas.

Todo o resto será renderizado como texto simples.

#### Recolher Campo {#field-collapse}

O recolhimento de campo é o mecanismo que combina vários valores de campo em um único elemento semântico com base em uma convenção de nomenclatura usando os sufixos `Title`, `Type`, `MimeType`, `Alt` e `Text` (todos diferenciam maiúsculas de minúsculas). Qualquer propriedade que termine com qualquer um desses sufixos não será considerada um valor, mas como um atributo de outra propriedade.

##### Imagens {#image-collapse}

>[!BEGINTABS]

>[!TAB Dados]

```json
{
  "image": "/content/dam/red-car.png",
  "imageAlt: "A red card on a road"
}
```

>[!TAB Marcação]

```html
<picture>
  <img src="/content/dam/red-car.png" alt="A red car on a road">
</picture>
```

>[!TAB Tabela]

```text
![A red car on a road][image0]
```

>[!ENDTABS]

##### Links e botões {#links-buttons-collapse}

>[!BEGINTABS]

>[!TAB Dados]

```json
{
  "link": "https://www.adobe.com",
  "linkTitle": "Navigate to adobe.com",
  "linkText": "adobe.com",
  "linkType": "primary"
}
```

>[!TAB Marcação]

Nenhum `linkType` ou `linkType=default`

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

>[!TAB Tabela]

```text
[adobe.com](https://www.adobe.com "Navigate to adobe.com")
**[adobe.com](https://www.adobe.com "Navigate to adobe.com")**
_[adobe.com](https://www.adobe.com "Navigate to adobe.com")_
```

>[!ENDTABS]

##### Cabeçalhos {#headings-collapse}

>[!BEGINTABS]

>[!TAB Dados]

```json
{
  "heading": "Getting started",
  "headingType": "h2"
}
```

>[!TAB Marcação]

```html
<h2>Getting started</h2>
```

>[!TAB Tabela]

```text
## Getting started
```

>[!ENDTABS]

#### Agrupamento de elementos {#element-grouping}

Embora o [recolhimento de campo](#field-collapse) seja sobre a combinação de várias propriedades em um único elemento semântico, o agrupamento de elementos é sobre a concatenação de vários elementos semânticos em uma única célula. Isso é particularmente útil para casos de uso em que o autor deve ser restrito no tipo e no número de elementos que pode criar.

Por exemplo, um componente de teaser pode permitir que o autor crie apenas um subtítulo, título e uma única descrição de parágrafo combinada com no máximo dois botões de chamada para ação. O agrupamento desses elementos produz uma marcação semântica que pode ser estilizada sem mais ações.

O agrupamento de elementos usa uma convenção de nomenclatura, em que o nome do grupo é separado de cada propriedade no grupo por um sublinhado. O recolhimento de campo das propriedades em um grupo funciona conforme descrito anteriormente.

>[!BEGINTABS]

>[!TAB Dados]

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

>[!TAB Marcação]

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

>[!TAB Tabela]

```text
+-------------------------------------------------+
| Teaser                                          |
+=================================================+
| ![A group of people sitting on a stage][image0] |
+-------------------------------------------------+
| Adobe Experience Cloud                          |
| ## Meet the Experts                             |
| Join us in this ask me everything session ...   |
| [More Details](https://link.to/more-details)    |
| [RSVP](https://link.to/sign-up)                 |
+-------------------------------------------------+
```

>[!ENDTABS]

## Seções e metadados de seção {#sections-metadata}

Da mesma forma que um desenvolvedor pode definir e modelar vários [blocos](#blocks), ele pode definir seções diferentes.

O modelo de conteúdo do Edge Delivery Services permite deliberadamente apenas um único nível de aninhamento, ou seja, qualquer conteúdo ou bloco padrão contido em uma seção. Isso significa que, para ter componentes visuais mais complexos que possam conter outros componentes, eles precisam ser modelados como seções e combinados juntos usando o bloqueio automático do lado do cliente. Exemplos típicos disso são abas e seções recolhíveis, como acordeões.

Uma seção pode ser definida da mesma forma que um bloco, mas com o tipo de recurso `core/franklin/components/section/v1/section`. As seções podem ter um nome e uma [ID de filtro](/help/implementing/universal-editor/filtering.md), que são usadas somente pelo [Editor Universal](/help/implementing/universal-editor/introduction.md), bem como uma [ID de modelo](/help/implementing/universal-editor/field-types.md#model-structure), que é usada para renderizar os metadados da seção. O modelo é, dessa forma, o modelo do bloco de metadados da seção, que será anexado automaticamente a uma seção como bloco de valor principal se não estiver vazio.

A [ID do modelo](/help/implementing/universal-editor/field-types.md#model-structure) e a [ID do filtro](/help/implementing/universal-editor/filtering.md) da seção padrão é `section`. Ela pode ser usada para alterar o comportamento da seção padrão. O exemplo a seguir adiciona alguns estilos e e uma imagem de plano de fundo ao modelo de metadados da seção.

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

Os documentos podem ter um [bloco de metadados](https://www.aem.live/developer/block-collection/metadata) da página, que é usado para definir quais `<meta>` elementos são renderizados no `<head>` de uma página. As propriedades de página das páginas no AEM as a Cloud Service são mapeadas para aquelas que estão disponíveis prontas para uso para Edge Delivery Services, como `title`, `description`, `keywords`, etc.

Antes de explorar mais detalhadamente como definir seus próprios metadados, revise os documentos a seguir para entender o conceito de metadados da página primeiro.

* [Metadados](https://www.aem.live/developer/block-collection/metadata)
* [Metadados em massa](/help/edge/docs/bulk-metadata.md)

Também é possível definir metadados de página adicionais de duas maneiras.

### Planilhas de metadados {#metadata-spreadsheets}

É possível definir metadados por caminho ou por padrão de caminho de uma maneira semelhante a uma tabela no AEM as a Cloud Service. Há uma interface de criação para dados semelhantes a tabelas disponíveis semelhante ao Excel ou ao Google Sheets.

Para obter mais detalhes, consulte o documento [Usando Planilhas para Gerenciar Dados Tabulares](/help/edge/wysiwyg-authoring/tabular-data.md) para obter mais informações.

### Propriedades da página {#page-properties}

Muitas das propriedades de página padrão disponíveis no AEM são mapeadas para os respectivos metadados de página em um documento. Isso inclui, por exemplo, `title`, `description`, `robots`, `canonical url` ou `keywords`. Algumas propriedades específicas do AEM também estão disponíveis:

* `cq:lastModified` como `modified-time` no formato ISO8601
* A hora em que o documento foi publicado pela última vez como `published-time` no formato ISO8601
* `cq:tags` como `cq-tags` como uma lista separada por vírgulas das IDs de marcas.

Também é possível definir um modelo de componente para metadados de página personalizados, que será disponibilizado ao autor no Editor universal.

Para fazer isso, crie um modelo de componente com a ID `page-metadata`.

```json
{
  "id": "page-metadata",
  "fields": [
    {
      "component": "text",
      "name": "theme",
      "label": "Theme"
    }
  ]
}
```

## Próximas etapas {#next-steps}

Agora que você sabe como modelar conteúdo, pode criar blocos para seus próprios Edge Delivery Services com o projeto de criação do WYSIWYG.

Consulte o documento [Criação de blocos instrumentados para uso com o Editor universal](/help/edge/wysiwyg-authoring/create-block.md) para saber como criar blocos instrumentados para uso com o Editor universal na criação de projetos do WYSIWYG com Edge Delivery Services.

Se você já estiver familiarizado com a criação de blocos, consulte o documento [Guia de Introdução ao Desenvolvedor para criação no WYSIWYG com o Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) para que você possa começar a usar um novo site do Adobe Experience Manager usando o Edge Delivery Services e o Editor Universal para criação de conteúdo.

>[!TIP]
>
>Para obter uma apresentação completa da criação de um novo projeto do Edge Delivery Services habilitado para criação no WYSIWYG com o AEM as a Cloud Service AEM como fonte de conteúdo, exiba [este webinário de GEMs do](https://experienceleague.adobe.com/en/docs/events/experience-manager-gems-recordings/gems2024/wysiwyg-authoring-and-edge-delivery).

