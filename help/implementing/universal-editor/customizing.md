---
title: Personalização da experiência de criação no Universal Editor
description: Saiba mais sobre os diferentes pontos de extensão e outros recursos que permitem personalizar a interface do usuário do Editor universal para atender às necessidades dos autores de conteúdo.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 11a244b7dd4810fbfec92b3effc362102e7322dc
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---


# Personalização da experiência de criação no Universal Editor {#customizing-ue}

Saiba mais sobre os diferentes pontos de extensão e outros recursos que permitem personalizar a experiência de criação do Editor universal para atender às necessidades dos autores de conteúdo.

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

## Mostrar e ocultar componentes condicionalmente no painel Propriedades {#conditionally-hide}

Embora um componente ou componentes possam estar disponíveis para os autores, pode haver certas situações em que isso não faça sentido. Nesses casos, você pode ocultar componentes no painel de propriedades adicionando um `condition` atributo para o [campos do modelo de componente.](/help/implementing/universal-editor/field-types.md#fields)

As condições podem ser definidas usando [Esquema JsonLogic.](https://jsonlogic.com/) Se a condição for verdadeira, o campo será exibido. Se a condição for falsa, o campo ficará oculto.

### Modelo de amostra {#sample-model}

```json
 {
    "id": "conditionally-revealed-component",
    "fields": [
      {
        "component": "boolean",
        "label": "Shall the text field be revealed?",
        "name": "reveal",
        "valueType": "boolean"
      },
      {
        "component": "text-input",
        "label": "Hidden text field",
        "name": "hidden-text",
        "valueType": "string",
        "condition": { "===": [{"var" : "reveal"}, true] }
      }
    ]
 }
```

#### Condição falsa {#false}

![Campo de texto oculto](assets/hidden.png)

#### Condição Verdadeira {#true}

![Campo de texto exibido](assets/shown.png)

