---
title: Filtros
description: Saiba como definir filtros para limitar as opções disponíveis no editor, como componentes disponíveis, opções de RTE e seleção de ativos.
feature: Developing
role: Admin, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 2%

---


# Filtros {#filters}

Saiba como definir filtros para limitar as opções disponíveis no editor, como componentes disponíveis, opções de RTE e seleção de ativos.

## Configuração de filtros {#configuring-filters}

Ao usar o Editor universal, é possível restringir as opções permitidas para determinada funcionalidade definindo um filtro. Um filtro é uma lista de itens ou ações disponíveis para o contexto específico. Por exemplo, você pode filtrar os componentes disponíveis para serem inseridos em um contêiner, [filtrar as opções disponíveis no RTE](/help/implementing/universal-editor/configure-rte.md) e [filtrar os ativos disponíveis](/help/implementing/universal-editor/configure-assets-selector.md) no seletor de ativos.

Todos os filtros devem ser definidos de forma semelhante.

1. [Adicionar tag de script para apontar para a definição do filtro](#add-tag)
1. [Definir o filtro](#define-filter)
1. [Referência ao filtro](#reference-filter)

Vamos ver um exemplo de componentes de filtragem por componente de contêiner.

## Definição de Filtro de Referência {#add-tag}

Primeiro, introduza uma tag de script adicional, que aponta para a definição do filtro.

Para nosso exemplo, filtrar componentes permitidos por contêiner, a tag pode ter esta aparência.

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

## Definir o filtro {#define-filter}

Uma definição de filtro contém JSON com uma ID exclusiva ao filtro e aos critérios do filtro.

Para o nosso exemplo, filtrar componentes permitidos por contêiner, pode ser semelhante ao seguinte, o que restringiria um contêiner para permitir apenas a adição de texto e imagens.

```json
[
  {
    "id": "container-filter",
    "components": ["text", "image"]
   }
]
```

Definir o atributo `components` em uma definição de filtro como `null` permite todos os componentes, como se não houvesse filtros.

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

## Referência ao filtro {#reference-filter}

Para usar o filtro, você deve consultar a definição dele. Você pode fazer isso ao:

* Referenciar o filtro a partir do componente de contêiner adicionando a propriedade `data-aue-filter`, transmitindo a ID do filtro.

  ```html
  data-aue-filter="container-filter"
  ```

* Referenciando o filtro a partir da sua [definição de componente](/help/implementing/universal-editor/component-definition.md) transmitindo a ID do filtro.

  ```json
  {
     "title":"My Container",
     "id":"my-container",
     "model": "my-model",
     "filter": "container-filter",
     ...
  }
  ```

## Recursos adicionais {#additional-resources}

Saiba mais sobre outras opções de personalização e extensão disponíveis para o Universal Editor nos documentos:

* [Configuração do RTE para o Editor universal](/help/implementing/universal-editor/configure-rte.md)
* [Configuração de filtros para o seletor de Assets](/help/implementing/universal-editor/configure-assets-selector.md)
* [Personalização do Editor universal](/help/implementing/universal-editor/customizing.md)
* [Extensão do Universal Editor](/help/implementing/universal-editor/extending.md)
