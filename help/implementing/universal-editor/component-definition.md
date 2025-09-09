---
title: Definição de componente
description: Entenda o contrato JSON entre a definição do componente e o Editor universal em detalhes.
feature: Developing
role: Admin, Architect, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: b4e61ec6abcaf73119f8963d72317759b2bd7c76
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Definição de componente {#component-definition}

Entenda o contrato JSON entre a definição do componente e o Editor universal em detalhes.

## Visão geral {#overview}

O arquivo `component-definition.json` define os componentes disponíveis para seus autores de conteúdo para o projeto. Este documento explica em detalhes a finalidade desse arquivo e como o Editor universal o usa para apresentar aos autores os componentes de criação de página.

>[!TIP]
>
>Para obter uma visão geral do processo de modelagem de conteúdo, consulte o documento [Modelagem de Conteúdo para Criação no WYSIWYG com Projetos do Edge Delivery Services.](https://www.aem.live/developer/component-model-definitions)

>[!TIP]
>
>Não é necessário criar seu próprio arquivo `component-definition.json` do zero. O modelo de projeto que você usa para [inicializar seu projeto](https://www.aem.live/developer/ue-tutorial) contém um [arquivo `component-definition.json` totalmente funcional](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) que você pode adaptar às suas necessidades.

## Exemplo de definição de componente {#example}

Veja a seguir um exemplo completo, mas simples de `component-definition.json`.

```json
{
  "groups":[
    {
      "title":"General Components",
      "id":"general",
      "components":[
        {
          "title":"Text",
          "id":"text",
          "model": "text",
          "filter": "texts",
          "plugins":{
            "aem":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            },
            "aem65":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```

## `groups` {#groups}

`groups` define os grupos de componentes que o autor vê no Editor Universal ao clicar no ícone **Adicionar** no painel de propriedades do editor para [adicionar um novo componente a uma página](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components). Grupos ajudam a organizar os componentes. Os grupos comuns podem ser **Componentes Gerais** e **Componentes Avançados**.

* `title` define a descrição textual do grupo mostrado na interface do usuário do editor.
* `id` identifica exclusivamente o grupo.

## `components` {#components}

`components` define quais componentes pertencem a um grupo.

* `title` define a descrição textual do componente mostrado na interface.
* `id` identifica exclusivamente o componente.
   * O [modelo de componente](/help/implementing/universal-editor/field-types.md#model-structure) do mesmo `id` define os campos do componente.
   * Por ser exclusivo, ele pode ser usado, por exemplo, em uma [definição de filtro](/help/implementing/universal-editor/filtering.md) para determinar quais componentes podem ser adicionados a um contêiner.
* `model` define qual [modelo](/help/implementing/universal-editor/field-types.md#model-structure) é usado com o componente.
   * Portanto, o modelo é mantido centralmente na definição do componente e não precisa ser [especificado na instrumentação.](/help/implementing/universal-editor/field-types.md#instrumentation)
   * Isso permite mover componentes entre contêineres.
* `filter` define qual [filtro](/help/implementing/universal-editor/filtering.md) deve ser usado com o componente.

## `plugins` {#plugins}

`plugins` define qual plug-in é responsável pela persistência do componente. Os plug-ins comuns incluem:

* `aem` para [AEM as a Cloud Service.](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service)
* `aem65` para [AEM 6.5.](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65) e [AEM 6.5 LTS](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65-lts)
* `xwalk` para [Criação com o AEM Sites para Edge Delivery Services.](https://www.aem.live/developer/ue-tutorial)

## `page` ou `cf` {#page-cf}

Depois que o `plugin` é definido, é necessário indicar se ele está relacionado à página ou ao fragmento.

* `page` indica que o componente é conteúdo na página atual.
* `cf` indica que o componente está relacionado ao conteúdo em um [Fragmento de conteúdo](/help/assets/content-fragments/content-fragments.md).

### `page` {#page}

Se o componente for conteúdo da página, você pode fornecer as seguintes informações.

* `resourceType` define o [Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType` usado para renderizar o componente.
* `template` define chave/valores opcionais a serem gravados automaticamente no componente recém-criado e define qual filtro e/ou modelo deve ser aplicado ao componente.
   * Útil para texto explicativo, de amostra ou de espaço reservado.

#### `template` {#template}

Ao fornecer pares de chave/valor opcionais, o `template` pode gravá-los automaticamente no novo componente. Além disso, os seguintes valores opcionais também podem ser especificados.

### `cf` {#cf}

Se o componente estiver relacionado ao conteúdo em um Fragmento de conteúdo, você poderá fornecer as seguintes informações.

* `name` define um nome opcional salvo no JCR para o componente recém-criado.
   * Apenas informativo e geralmente não exibido na interface do usuário como `title` é.
* `cfModel` define o modelo de [Fragmento de Conteúdo](/help/assets/content-fragments/content-fragments-models.md) para o componente recém-criado.
* `cfFolder` define em qual pasta o fragmento de conteúdo será criado.
* `title` define o título do novo fragmento de conteúdo.
* `description` define uma descrição do novo fragmento de conteúdo.
* `template` define chave/valores opcionais a serem gravados automaticamente no fragmento de conteúdo recém-criado.
   * Útil para texto explicativo, de amostra ou de espaço reservado.

### `cf` Pode ser implícito {#cf-implied}

Se a página for [instrumentada](/help/implementing/universal-editor/getting-started.md#instrument-page) para apontar para um campo de referência, `cf` será presumido.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

Nesse caso, `cf` é presumido, porque `data-aue-prop` aponta para um campo de referência. Sem o `data-aue-prop`, o Editor Universal assumirá `page`, pois nesse caso os componentes não são vinculados por meio de um campo de referência.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

Componentes são simplesmente subnós abaixo do recurso.
