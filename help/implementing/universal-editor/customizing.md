---
title: Personalização do Editor universal
description: Saiba mais sobre as diferentes opções para personalizar o Editor universal para atender às necessidades dos autores de conteúdo.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: cb3cf5ee6bb17c33c118c6463272922e0e212c1a
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# Personalização do Editor universal {#customizing}

Saiba mais sobre as diferentes opções para personalizar o Editor universal para atender às necessidades dos autores de conteúdo.

>[!TIP]
>
>O Editor Universal também oferece muitos [pontos de extensão](/help/implementing/universal-editor/extending.md), permitindo expandir sua funcionalidade para atender às necessidades do projeto.

## Uso de tags de configuração do Meta {#meta-tags}

Alguns fluxos de trabalho de criação podem exigir o uso de alguns recursos do Editor universal, e não de outros. Para dar suporte a esses casos diversos, metatags estão disponíveis para configurar ou desativar determinados recursos ou botões do editor.

Use esta marca na seção `<head>` da página para desabilitar um ou mais recursos:

```html
<meta name="urn:adobe:aue:config:disable" content="..." />
```

Se quiser desativar vários recursos, forneça uma lista de valores separados por vírgulas.

A seguir estão os valores com suporte para `content`, ou seja, os recursos que podem ser desabilitados com metatags.

| Valor do conteúdo | Descrição |
|---|---|
| `publish` | Desabilite toda a funcionalidade de [publicação](/help/sites-cloud/authoring/universal-editor/publishing.md), ou seja, o [botão Publicar](/help/sites-cloud/authoring/universal-editor/navigation.md#publish) e o [botão Cancelar publicação](/help/sites-cloud/authoring/universal-editor/navigation.md#ellipsis) |
| `publish-live` | Desabilitar a [publicação](/help/sites-cloud/authoring/universal-editor/publishing.md) em tempo real |
| `publish-preview` | Desabilitar publicação de visualização (se o [serviço de visualização](/help/sites-cloud/authoring/sites-console/previewing-content.md) estiver disponível) |
| `unpublish` | Desabilitar o [botão Cancelar publicação](/help/sites-cloud/authoring/universal-editor/publishing.md#unpublishing-content) ([recurso de visualização](/help/release-notes/universal-editor/preview.md)) |
| `copy` | Desabilita os [botões copiar e colar](/help/sites-cloud/authoring/universal-editor/authoring.md#copy-paste) |
| `duplicate` | Desabilita o [botão duplicar](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) |
| `header-open-page` | Desabilita o [botão Abrir página](/help/sites-cloud/authoring/universal-editor/navigation.md#open-page) |

## Alterando seu endpoint {#custom-endpoint}

Se você não quiser usar o Universal Editor Service, que é hospedado pela Adobe, mas sua própria versão hospedada, poderá defini-lo em uma meta tag. Consulte o documento [Introdução ao Editor Universal no AEM](/help/implementing/universal-editor/getting-started.md##configuration-settings) para obter detalhes.

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

Para fazer isso, basta incluir o URL de visualização desejado em uma meta tag do aplicativo instrumentado, como no exemplo a seguir.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
