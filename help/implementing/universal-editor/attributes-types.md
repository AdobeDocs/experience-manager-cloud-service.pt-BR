---
title: Atributos e Tipos de Item
description: Saiba mais sobre os atributos de dados e os tipos de item exigidos pelo Universal Editor.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 45%

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
| `data-aue-filter` | Define:<br>- Quais funcionalidades de RTE estão habilitadas<br>- Quais componentes podem ser adicionados a um contêiner<br>- Quais ativos podem ser adicionados a um tipo de mídia |
| `data-aue-label` | Define um rótulo personalizado para um item selecionável que é exibido no editor |
| `data-aue-model` | Define um modelo usado para edição baseada em formulário no painel de propriedades |
| `data-aue-behavior` | Obsoleto. Uma vez, ele definiu o comportamento de uma instrumentação para permitir que texto, richtext e mídia independentes mimetizassem componentes para que eles também pudessem ser movidos e excluídos na página, oferecendo um único valor potencial de `component`. Essa propriedade agora é ignorada e quando um item com `data-aue-resource` é filho direto de um contêiner, ele é automaticamente considerado um componente. |

## Tipos de item {#item-types}

| `data-aue-type` | Descrição | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` |
|---|---|---|---|---|---|---|
| `text` | O texto é editável nas tags HTML, mas somente em um formato de texto simples; a formatação Rich Text não está disponível. Isso é bastante usado em componentes de título, por exemplo | Opcional | Obrigatório | n/a | Opcional | n/a |
| `richtext` | O texto é editável com recursos completos de Rich Text. O RTE será exibido no painel direito | Opcional | Obrigatório | n/a | Opcional | n/a |
| `media` | O editável é um ativo, por exemplo, imagem ou vídeo | Opcional | Obrigatório | Opcional<br>lista de critérios de filtro de imagem ou vídeo que é passada para o seletor de ativos | Opcional | n/a |
| `container` | O item editável atua como um container de componentes, o que também é conhecido como um Sistema de parágrafo. | Depende do <br>, veja abaixo | Depende do <br>, veja abaixo | Opcional<br>uma lista de componentes permitidos | Opcional | n/a |
| `component` | O item editável é um componente. Ele não acrescenta nenhuma funcionalidade extra, É obrigatório indicar partes móveis/excluíveis do DOM e para abrir o painel de propriedades e seus campos | Obrigatório | n/a | n/a | Opcional | Opcional |
| `reference` | O editável é uma referência, por exemplo, Fragmento de conteúdo, Fragmento de experiência ou Produto | Depende do <br>, veja abaixo | Depende do <br>, veja abaixo | Opcional<br>lista de critérios de filtro para fragmentos de conteúdo, produtos ou fragmentos de experiência que é passada para o seletor de referência | Opcional | Opcional |

`data-aue-resource` é sempre necessário, pois é a chave primária que indica onde as alterações de conteúdo são gravadas.

* Não é necessário diretamente na tag em que o `data-aue-type` está definido.
* Caso não esteja definido, o atributo `data-aue-resource` de um pai mais próximo será usado.

`data-aue-prop` é obrigatório sempre que você quiser editar em contexto, exceto para um contêiner em que é opcional (se o contêiner for um fragmento de conteúdo e a prop apontar para um campo de várias referências).

* O `data-aue-prop` é o atributo a ser atualizado para a chave primária de `data-aue-resource`.
