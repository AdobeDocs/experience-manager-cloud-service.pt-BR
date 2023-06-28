---
title: Atributos e tipos
description: Saiba mais sobre os atributos e tipos de dados exigidos pelo Editor universal.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 82%

---

# Atributos e tipos {#attributes-types}

Saiba mais sobre os atributos e tipos de dados exigidos pelo Editor universal.

## Introdução {#introduction}

Para que um aplicativo possa ser editado pelo Editor universal, ele deve ser instrumentado corretamente. O que significa incluir os metadados apropriados para que a ferramenta possa editar o conteúdo do aplicativo. Este documento detalha os atributos e os tipos desses metadados.

>[!NOTE]
>
>A validação do conteúdo é executada no lado do servidor. O Editor universal funciona apenas com os atributos de dados. A validação para se adequar ao modelo/estrutura precisa ser abordada no nível da API.

## Propriedades de dados {#data-properties}

| Propriedade dos dados | Descrição |
|---|---|
| `itemid` | Para saber mais sobre o URN do recurso, consulte a seção [Instrumentar a página do documento Introdução ao Editor universal no AEM](getting-started.md#instrument-thepage) |
| `itemprop` | Para saber mais sobre o atributo do recurso, consulte a seção [Instrumentar a página do documento Introdução ao Editor universal no AEM](getting-started.md#instrument-thepage) |
| `itemtype` | Tipo do item editável (por exemplo, texto, imagem e referência) |
| `data-editor-itemfilter` | Define quais referências podem ser usadas |
| `data-editor-itemlabel` | Define um rótulo personalizado para um item selecionável que é exibido no editor <br>No caso `itemmodel` for definido, o rótulo será recuperado por meio do modelo |
| `data-editor-itemmodel` | Define um modelo usado para edição baseada em formulário no painel de propriedades |
| `data-editor-behavior` | Define o comportamento de uma instrumentação, por exemplo, textos ou imagens isoladas também podem atuar como um componente, para que possam ser movidos ou excluídos |

## Tipos de item {#item-types}

| `itemtype` | Descrição | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | O texto é editável nas tags HTML, mas somente em um formato de texto simples; a formatação Rich Text não está disponível. Isso é bastante usado em componentes de título, por exemplo | Opcional | Obrigatório | n/a | Opcional | n/a | Opcional |
| `richtext` | O texto é editável com recursos completos de Rich Text. O RTE é mostrado no painel direito | Opcional | Obrigatório | n/a | Opcional | n/a | Opcional |
| `media` | O item editável é um ativo, por exemplo, uma imagem ou vídeo | Opcional | Obrigatório | Opcional<br>lista de critérios de filtro de imagem ou vídeo que é passada para o seletor de ativos | Opcional | n/a | Opcional |
| `container` | O item editável atua como um container de componentes, o que também é conhecido como um Sistema de parágrafo. | Depende do <br>, veja abaixo | Depende do <br>, veja abaixo | Opcional<br>uma lista de componentes permitidos | Opcional | n/a | n/a |
| `component` | O item editável é um componente. Não acrescenta funcionalidade adicional; é necessário para indicar partes móveis/excluíveis do DOM e para abrir o painel de propriedades e seus campos | Obrigatório | n/a | n/a | Opcional | Opcional | n/a |
| `reference` | O item editável é uma referência, por exemplo, um fragmento de conteúdo, fragmento de experiência ou produto | Depende do <br>, veja abaixo | Depende do <br>, veja abaixo | Opcional<br>lista de critérios de filtro para fragmentos de conteúdo, produtos ou fragmentos de experiência que é passada para o seletor de referência | Opcional | Opcional | n/a |

Dependendo do caso de uso, `itemprop` ou `itemid` podem ou não ser exigidos. Por exemplo:

* O `itemid` é necessário se você consultar fragmentos de conteúdo por meio de GraphQL e desejar tornar a lista editável no contexto.
* O `itemprop` é necessário caso você possua um componente que renderize o conteúdo de um fragmento de conteúdo referenciado e deseje atualizar a referência desse componente.

## Comportamentos {#behaviors}

| `data-editor-behavior` | Descrição |
|---|---|
| `component` | Pode ser usado para permitir que textos, Rich Text ou mídias isoladas imitem o comportamento de componentes, de modo que também possam ser movidos ou excluídos na página |

## Recursos adicionais {#additional-resources}

Para saber mais sobre o Editor universal, consulte estes documentos.

* [Introdução ao Universal Editor](introduction.md) : saiba como o Editor universal permite editar qualquer aspecto de qualquer conteúdo em qualquer implementação para que você possa fornecer experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência do desenvolvedor de última geração.
* [Criação de conteúdo com o Editor universal](authoring.md): saiba como é fácil e intuitivo para os autores criarem conteúdo usando o Editor universal.
* [Publicação de conteúdo com o Editor universal](publishing.md): saiba como o Editor visual universal publica o conteúdo e como seus aplicativos podem lidar com esse conteúdo.
* [Introdução ao Editor universal no AEM](getting-started.md): saiba como obter acesso ao Editor universal e começar a instrumentar seu primeiro aplicativo do AEM para utilizá-lo.
* [Arquitetura do Editor universal](architecture.md): saiba mais sobre a arquitetura do Editor universal e como os dados fluem entre seus serviços e camadas.
* [Autenticação do Editor universal](authentication.md): saiba como funciona a autenticação do Editor universal.
