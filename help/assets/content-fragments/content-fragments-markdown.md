---
title: Markdown (Assets - Fragmentos de conteúdo)
description: Entenda como o editor de Fragmento de conteúdo usa a sintaxe de Markdown para permitir que você crie conteúdo headless facilmente.
feature: Content Fragments
role: User
exl-id: 7a6d4a63-faf8-4e1c-95da-90db2027a2dd
solution: Experience Manager Sites
source-git-commit: be60f0371e652549cec6e57d1449b6e07b996514
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 67%

---

# Markdown {#markdown}

Quando você está [criando](/help/assets/content-fragments/content-fragments-variations.md#authoring-your-content), o editor de fragmento de conteúdo usa a sintaxe *markdown* para permitir que você grave conteúdo facilmente para entrega headless ou criação de página:

>[!NOTE]
>
>Os Fragmentos de conteúdo são um recurso do Sites, mas são armazenados como **Assets**.
>
>Há dois editores para a criação de fragmentos de conteúdo; embora a funcionalidade básica seja a mesma, há algumas diferenças. Esta seção abrange o editor original, acessado principalmente do console **Assets**. Consulte a documentação do Sites, [Fragmentos de conteúdo - Criação](/help/sites-cloud/administering/content-fragments/authoring.md), para obter detalhes do novo editor (acessado principalmente do console **Fragmentos de conteúdo**).

![Editor do Markdown](/help/assets/content-fragments/assets/cfm-markdown-01.png)

Você pode definir:

* [Notação de cabeçalho](/help/assets/content-fragments/content-fragments-markdown.md#heading-notation)
* [Parágrafos e quebras de linha](/help/assets/content-fragments/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [Links](/help/assets/content-fragments/content-fragments-markdown.md#links)
* [Imagens](/help/assets/content-fragments/content-fragments-markdown.md#images)
* [Citações em bloco](/help/assets/content-fragments/content-fragments-markdown.md#block-quotes)
* [Listas](/help/assets/content-fragments/content-fragments-markdown.md#lists)
* [Ênfase](/help/assets/content-fragments/content-fragments-markdown.md#emphasis)
* [Blocos de código](/help/assets/content-fragments/content-fragments-markdown.md#code-blocks)
* [Escapes de barra invertida](/help/assets/content-fragments/content-fragments-markdown.md#backslash-escapes)

## Notação de cabeçalho {#heading-notation}

Para criar um cabeçalho, coloque um símbolo de hash (#) na frente dele. Um símbolo de hash (#) é usado para um H1, dois símbolos de hash (##) para um H2 e assim por diante. Você pode usar até seis símbolos de hash. Por exemplo:

    `## This is an H2`

    `### This is an H3`

    `###### This is an H6`

Opcionalmente, é possível criar uma H1 sublinhando o texto com sinais de igual e criar uma H2 sublinhando o texto com sinais de menos. Por exemplo:

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## Parágrafos e quebras de linha {#paragraphs-and-line-breaks}

Um parágrafo é apenas uma ou mais linhas consecutivas de texto, separadas por uma ou mais linhas em branco. Uma linha em branco é uma linha que contém apenas espaços ou tabulações. Os parágrafos normais não devem ser recuados com espaços ou tabulações.

Uma quebra de linha é criada ao terminar uma linha com dois ou mais espaços e depois um retorno.

## Links {#links}

Você pode criar links integrados e de referência.

Em ambos os estilos, o texto do link é delimitado por colchetes `[]`.

Estes são exemplos de links integrados:

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example (non-standard) of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

Um link de referência tem a seguinte sintaxe:

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## Imagens {#images}

A sintaxe das imagens é semelhante aos links. Você pode criar imagens integradas e referenciadas.

Por exemplo, uma imagem integrada tem a seguinte sintaxe:

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

A sintaxe inclui:

* Um ponto de exclamação: !;
* seguido por um conjunto de colchetes, contendo o texto alternativo do atributo para a imagem;
* seguido por um conjunto de parênteses, contendo o URL ou o caminho para a imagem e um atributo de título opcional entre aspas duplas ou simples.

Uma imagem de estilo de referência tem a seguinte sintaxe:

    `![Alt text][id]`

Onde &quot;id&quot; é o nome de uma referência de imagem definida. As referências de imagem são definidas usando a sintaxe idêntica às referências de link:

    `[id]: url/to/image "Optional title attribute"`

## Citações em bloco {#block-quotes}

É possível citar o texto adicionando o símbolo > antes dele. Por exemplo:

    `>This is block quotes`

Você pode ter citações de bloco aninhadas. Por exemplo:

    `> This is the first level of quoting.`

    `>`

        `>> This is a nested blockquote.`

    `>`

    `> Back to the first level.`

## Listas {#lists}

É possível criar listas ordenadas e não ordenadas.

Para criar uma lista não ordenada, use o símbolo &ast; (asterisco) antes dos itens na lista. Por exemplo:

    `* item in list`

    `* item in list`

    `* item in list`

Para criar uma lista ordenada, adicione os números, seguidos de um ponto, antes de cada item na lista. Por exemplo:

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## Ênfase {#emphasis}

É possível adicionar um estilo em itálico ou negrito ao texto.

É possível adicionar itálico da seguinte maneira:

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

É possível colocar o texto em negrito da seguinte maneira:

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

Para indicar um trecho de código, envolva-o com aspas invertidas (`` ` ``). Ao contrário de um bloco de código pré-formatado, um trecho de código mostra o código dentro de um parágrafo normal.

Por exemplo:

    ``Use the `printf()` function.``

## Blocos de código {#code-blocks}

Os blocos de código geralmente são usados para ilustrar código-fonte. É possível criar blocos de código recuando o código usando tabulação ou um mínimo de 4 espaços. Por exemplo:

    `This is a normal paragraph.`

        `This is a code block.`

## Escapes de barra invertida {#backslash-escapes}

Você pode usar o escape de barra invertida para gerar caracteres literais, que têm significado especial na formatação da sintaxe. Por exemplo, se você deseja cercar uma palavra com asteriscos literais (em vez de uma tag HTML &lt;em>), você pode usar barras invertidas antes dos asteriscos, desta forma:

    `\\*literal asterisks\\*`

Os escapes de barra invertida estão disponíveis para os seguintes caracteres:

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`
