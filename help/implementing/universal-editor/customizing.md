---
title: Personalização do Editor universal
description: Saiba mais sobre as diferentes opções para personalizar o Editor universal para atender às necessidades dos autores de conteúdo.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 98879fe30482e042da05a390e75d11c0adf7dba9
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---


# Personalização do Editor universal {#customizing}

Saiba mais sobre as diferentes opções para personalizar o Editor universal para atender às necessidades dos autores de conteúdo.

>[!TIP]
>
>O Editor Universal também oferece muitos [pontos de extensão](/help/implementing/universal-editor/extending.md), permitindo expandir sua funcionalidade para atender às necessidades do projeto.

## Desabilitar publicação {#disable-publish}

Determinados workflows de criação exigem que o conteúdo seja revisado antes de ser publicado. Nessas situações, a opção de publicar não deve estar disponível para nenhum autor.

Portanto, o botão **Publicar** pode ser totalmente suprimido em um aplicativo adicionando os seguintes metadados.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## Desativar publicação para visualização {#publish-preview}

Alguns fluxos de trabalho de criação podem impedir a publicação no [serviço de visualização](/help/sites-cloud/authoring/sites-console/previewing-content.md) (se disponível).

A opção **Visualizar** na janela de publicação pode, portanto, ser totalmente suprimida em um aplicativo adicionando os seguintes metadados.

```html
<meta name="urn:adobe:aue:config:disable" content="publish-preview"/>
```

## Componentes de filtragem {#filtering-components}

Você pode restringir os componentes permitidos por contêiner no Editor universal usando filtros de componente. Consulte o documento [Componentes de Filtragem](/help/implementing/universal-editor/filtering.md) para obter mais informações.

## Mostrar e ocultar componentes condicionalmente no painel Propriedades {#conditionally-hide}

Embora um componente ou componentes possam estar disponíveis para os autores, pode haver certas situações em que isso não faça sentido. Nesses casos, você pode ocultar componentes no painel de propriedades adicionando um atributo `condition` aos [campos do modelo de componente](/help/implementing/universal-editor/field-types.md#fields).

As condições podem ser definidas usando o [esquema JsonLogic](https://jsonlogic.com/). Se a condição for verdadeira, o campo será exibido. Se a condição for falsa, o campo ficará oculto.

>[!BEGINTABS]

>[!TAB Modelo de amostra]

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

>[!TAB Condição falsa]

![Campo de texto oculto](assets/hidden.png)

>[!TAB Condição Verdadeira]

![Campo de texto mostrado](assets/shown.png)

>[!ENDTABS]

## URLs de visualização personalizados {#custom-preview-urls}

Você pode especificar uma URL de visualização personalizada por meio de uma metaconfiguração de `urn:adobe:aue:config:preview`, que será aberta ao clicar no botão **Abrir página** na barra de ferramentas superior direita do editor [&#128279;](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar).

Isso é particularmente útil para aplicativos com requisitos de visualização específicos, como os [que usam o Edge Delivery Services com criação no WYSIWYG](/help/edge/wysiwyg-authoring/authoring.md).

Para fazer isso, basta incluir o URL de visualização desejado em uma meta tag do aplicativo instrumentado, como no exemplo a seguir.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
