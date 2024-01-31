---
title: Personalização da interface
description: Saiba mais sobre os diferentes pontos de extensão que permitem personalizar a interface do usuário do Editor universal para atender às necessidades dos autores de conteúdo.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 1bc65e65e6ce074a050e21137ce538b5c086665f
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Personalização da interface {#customizing-ui}

Saiba mais sobre os diferentes pontos de extensão que permitem personalizar a interface do usuário do Editor universal para atender às necessidades dos autores de conteúdo.

## Desabilitar publicação {#disable-publish}

Determinados workflows de criação exigem que o conteúdo seja revisado antes de ser publicado. Nessas situações, a opção de publicar não deve estar disponível para nenhum autor.

A variável **Publish** Portanto, o botão pode ser totalmente suprimido em um aplicativo adicionando os seguintes metadados.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## Componentes de filtragem {#filtering-components}

Ao usar o Editor universal, é possível restringir os componentes permitidos por componente do contêiner. Para fazer isso, é necessário introduzir uma tag de script adicional, que aponta para a definição do filtro.

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

Uma definição de filtro pode ser semelhante à seguinte, o que restringiria um contêiner para permitir apenas a adição de texto e imagens.

```json
[
  {
    "id": "container-filter",
     "components": ["text", "image"]
   }
]
```

Em seguida, você pode fazer referência à definição de filtro a partir do componente de Contêiner adicionando a propriedade `data-aue-filter`, transmitindo a ID do filtro definido anteriormente.

```html
data-aue-filter="container-filter"
```

Definição de `components` atributo em uma definição de filtro para `null` permite todos os componentes, como se não houvesse filtros.

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```
