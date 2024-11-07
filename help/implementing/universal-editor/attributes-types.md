---
title: Atributos e Tipos de Item
description: Saiba mais sobre os atributos de dados e os tipos de item exigidos pelo Universal Editor.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Architect, Developer
source-git-commit: a7b48559e5bf60c86fecd73a8bcef6c9aaa03b80
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 65%

---


# Atributos e tipos {#attributes-types}

Saiba mais sobre os atributos de dados e os tipos de item exigidos pelo Universal Editor.

## Introdução {#introduction}

Para que um aplicativo possa ser editado pelo Editor universal, ele deve ser instrumentado corretamente. O que significa incluir os metadados apropriados para que a ferramenta possa editar o conteúdo do aplicativo. Este documento detalha os atributos e os tipos de item desses metadados.

>[!NOTE]
>
>A validação do conteúdo é executada no lado do servidor. O Editor universal funciona apenas com os atributos de dados. A validação de que eles se encaixam no modelo/estrutura deve ser abordada no nível da API.

## Propriedades de dados {#data-properties}

| Propriedade dos dados | Descrição |
|---|---|
| `data-aue-resource` | Para saber mais sobre o URN do recurso, consulte a seção [Instrumentar a página do documento Introdução ao Editor universal no AEM](getting-started.md#instrument-thepage) |
| `data-aue-prop` | Para saber mais sobre o atributo do recurso, consulte a seção [Instrumentar a página do documento Introdução ao Editor universal no AEM](getting-started.md#instrument-thepage) |
| `data-aue-type` | [Tipo do item editável](#item-types) (por exemplo, texto, imagem e referência) |
| `data-aue-filter` | Define quais referências podem ser usadas |
| `data-aue-label` | Define um rótulo personalizado para um item selecionável que é exibido no editor. <br>Caso`data-aue-model` seja definido, o rótulo será recuperado por meio do modelo |
| `data-aue-model` | Define um modelo usado para edição baseada em formulário no painel de propriedades |
| `data-aue-behavior` | Define o [comportamento de uma instrumentação](#behaviors), por exemplo, texto ou imagem autônoma também pode imitar um componente para torná-lo móvel ou excluível |

## Tipos de item {#item-types}

| `data-aue-type` | Descrição | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` | `data-aue-behavior` |
|---|---|---|---|---|---|---|---|
| `text` | O texto é editável nas tags HTML, mas somente em um formato de texto simples; a formatação Rich Text não está disponível. Isso é bastante usado em componentes de título, por exemplo | Opcional | Obrigatório | n/a | Opcional | n/a | Opcional |
| `richtext` | O texto é editável com recursos completos de Rich Text. O RTE será exibido no painel direito | Opcional | Obrigatório | n/a | Opcional | n/a | Opcional |
| `media` | O editável é um ativo, por exemplo, imagem ou vídeo | Opcional | Obrigatório | Opcional<br>lista de critérios de filtro de imagem ou vídeo que é passada para o seletor de ativos | Opcional | n/a | Opcional |
| `container` | O item editável atua como um container de componentes, o que também é conhecido como um Sistema de parágrafo. | Depende do <br>, veja abaixo | Depende do <br>, veja abaixo | Opcional<br>uma lista de componentes permitidos | Opcional | n/a | n/a |
| `component` | O item editável é um componente. Ele não acrescenta nenhuma funcionalidade extra, É obrigatório indicar partes móveis/excluíveis do DOM e para abrir o painel de propriedades e seus campos | Obrigatório | n/a | n/a | Opcional | Opcional | n/a |
| `reference` | O editável é uma referência, por exemplo, Fragmento de conteúdo, Fragmento de experiência ou Produto | Depende do <br>, veja abaixo | Depende do <br>, veja abaixo | Opcional<br>lista de critérios de filtro para fragmentos de conteúdo, produtos ou fragmentos de experiência que é passada para o seletor de referência | Opcional | Opcional | n/a |

Dependendo do caso de uso, `data-aue-prop` ou `data-aue-resource` podem ou não ser exigidos. Por exemplo:

* O `data-aue-resource` é necessário se você consultar fragmentos de conteúdo por meio de GraphQL e desejar tornar a lista editável no contexto.
* O `data-aue-prop` é necessário caso você possua um componente que renderize o conteúdo de um fragmento de conteúdo referenciado e deseje atualizar a referência desse componente.

## Comportamentos {#behaviors}

| `data-aue-behavior` | Descrição |
|---|---|
| `component` | Usado para permitir componentes de mimetismo de texto, richtext e mídia independentes para que também possam ser movidos e excluídos na página |
| `container` | Usado para permitir que os contêineres sejam tratados como seus próprios componentes para que possam ser movidos e excluídos na página |
