---
title: Componentes de filtragem
description: Saiba como restringir os componentes permitidos por contêiner no Editor universal usando filtros de componente.
feature: Developing
role: Admin, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# Componentes de filtragem {#filtering-components}

Saiba como restringir os componentes permitidos por contêiner no Editor universal usando filtros de componente.

## Filtros {#filters}

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

Em seguida, você pode fazer referência à definição de filtro a partir do componente de contêiner adicionando a propriedade `data-aue-filter`, transmitindo a ID do filtro definido anteriormente.

```html
data-aue-filter="container-filter"
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

>[!TIP]
>
>Saiba mais sobre outras opções de personalização e extensão disponíveis para o Universal Editor nos documentos:
>
>* [Personalizando o Editor Universal](/help/implementing/universal-editor/customizing.md)
>* [Estendendo o Editor Universal](/help/implementing/universal-editor/extending.md)
