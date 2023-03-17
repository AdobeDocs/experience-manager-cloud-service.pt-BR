---
title: Atributos e tipos
description: Saiba mais sobre os atributos e tipos de dados exigidos pelo Editor Universal.
source-git-commit: f454475b65da8f410812bbbe30ca5fc393be410a
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 7%

---


# Atributos e tipos {#attributes-types}

Saiba mais sobre os atributos e tipos de dados exigidos pelo Editor Universal.

## Introdução {#introduction}

Para que um aplicativo possa ser editado pelo Editor universal, ele deve ser instrumentado corretamente. Isso inclui a inclusão dos metadados adequados para que o editor possa editar o conteúdo do aplicativo. Este documento detalha os atributos e os tipos desses metadados.

>[!NOTE]
>
>A validação de conteúdo é executada no lado do servidor. O Editor Universal funciona apenas com os atributos de dados. A validação de que eles se encaixam no modelo/estrutura precisa ser abordada no nível da API.

## Propriedades de dados {#data-properties}

| Propriedade de dados | Descrição |
|---|---|
| `itemid` | URL para o recurso, consulte a seção [Instrua a página do documento Introdução ao Editor Universal em AEM](getting-started.md#instrument-thepage) |
| `itemprop` | Atributo do recurso, consulte a seção [Instrua a página do documento Introdução ao Editor Universal em AEM](getting-started.md#instrument-thepage) |
| `itemtype` | Tipo do item editável (por exemplo, texto, imagem, referência, etc.) |
| `data-editor-itemfilter` | Define quais referências podem ser usadas |
| `data-editor-itemlabel` | Define um rótulo personalizado para um item selecionável que é exibido no editor <br>Em caso `itemmodel` for definido, o rótulo será recuperado por meio do modelo |
| `data-editor-itemmodel` | Define um modelo que será usado para edição baseada em formulário no painel de propriedades |
| `data-editor-behavior` | Define o comportamento de uma instrumentação, por exemplo, texto ou imagem independente também pode imitar um componente para torná-lo móvel ou deletável |

## Tipos de item {#item-types}

| `itemtype` | Descrição | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | O texto é editável nas tags HTML, mas somente em um formato de texto simples, sem formatação Rich Text disponível, isso é comumente usado em componentes de título, por exemplo | Opcional | Obrigatório | n/a | Opcional | n/a | Opcional |
| `richtext` | O texto é editável com recursos completos de rich text. O RTE será exibido no painel direito | Opcional | Obrigatório | n/a | Opcional | n/a | Opcional |
| `media` | O editável é um ativo, por exemplo, imagem ou vídeo | Opcional | Obrigatório | Opcional<br>lista de critérios do filtro de imagem ou vídeo que é passada para o seletor de ativos | Opcional | n/a | Opcional |
| `container` | O editável se comporta como contêiner de componentes também conhecidos como Sistema de parágrafo. | Depende <br>veja abaixo | Depende <br>veja abaixo | Opcional<br>uma lista de componentes permitidos | Opcional | n/a | n/a |
| `component` | O editável é um componente. Não adiciona funcionalidade adicional, será necessário para indicar partes móveis/excluídas do DOM e para abrir o painel de propriedades e seus campos | Obrigatório | n/a | n/a | Opcional | Opcional | n/a |
| `reference` | O editável é uma referência, por exemplo, Fragmento de conteúdo, Fragmento de experiência ou Produto | Depende <br>veja abaixo | Depende <br>veja abaixo | Opcional<br>lista de critérios de filtro de Fragmento de conteúdo, Produto ou Fragmento de experiência que é passada para o seletor de referência | Opcional | Opcional | n/a |

Dependendo do caso de uso `itemprop` ou `itemid` podem ou não ser exigidas. Por exemplo:

* `itemid` é necessário se você consultar Fragmentos de conteúdo por meio do GraphQL e desejar tornar a lista editável no contexto.
* `itemprop` é necessário caso tenha um componente que renderize o conteúdo de um Fragmento de conteúdo referenciado e deseje atualizar a referência no componente.

## Comportamentos {#behaviors}

| `data-editor-behavior` | Descrição |
|---|---|
| `component` | Pode ser usado para tornar independentes o texto, o rich text e os componentes mimáticos de mídia, de modo que também sejam móveis e excluíveis na página |

## Recursos adicionais {#additional-resources}

Para saber mais sobre o Universal Editor, consulte estes documentos.

* [Introdução ao Editor Universal](introduction.md) - Saiba como o Editor Universal permite editar qualquer aspecto de qualquer conteúdo em qualquer implementação para fornecer experiências excepcionais, aumentar a velocidade do conteúdo e fornecer uma experiência de desenvolvedor de última geração.
* [Criação de conteúdo com o editor universal](authoring.md) - Saiba como é fácil e intuitivo para os autores de conteúdo criar conteúdo usando o Editor Universal.
* [Introdução ao Editor universal no AEM](getting-started.md) - Saiba como obter acesso ao Universal Editor e como começar a instrumentar seu primeiro aplicativo AEM para usá-lo.
* [Arquitetura do editor universal](architecture.md) - Saiba mais sobre a arquitetura do Editor Universal e como os dados fluem entre seus serviços e camadas.
* [Autenticação do editor universal](authentication.md) - Saiba como o Editor Universal se autentica.
