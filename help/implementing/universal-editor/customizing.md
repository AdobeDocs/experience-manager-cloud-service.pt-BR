---
title: Personalização do Editor universal
description: Saiba mais sobre as diferentes opções para personalizar o Editor universal para atender às necessidades dos autores de conteúdo.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: a72b4b7921a1a379bcd089682c02b0519fe3af8a
workflow-type: tm+mt
source-wordcount: '522'
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

## Desativar a publicação para o Live {#publish-live}

Determinados workflows de criação podem impedir a publicação no serviço em tempo real.

A opção **Live** na janela de publicação pode, portanto, ser totalmente suprimida em um aplicativo adicionando os seguintes metadados.

```html
<meta name="urn:adobe:aue:config:disable" content="publish-live"/>
```

## Desativar o cancelamento de publicação {#unpublish}

Determinados workflows de criação exigem um processo de aprovação antes que a publicação do conteúdo seja desfeita. Nessas situações, a opção de desfazer a publicação não deve estar disponível para nenhum autor.

Portanto, o botão **Cancelar publicação** pode ser totalmente suprimido em um aplicativo adicionando os seguintes metadados.

```html
<meta name="urn:adobe:aue:config:disable" content="unpublish"/>
```

## Desativar a página aberta {#open-page}

O botão **Abrir Página** pode ser totalmente suprimido em um aplicativo adicionando os seguintes metadados.

```html
<meta name="urn:adobe:aue:config:disable" content="header-open-page" />
```

## Desabilitação do Botão Duplicar {#duplicate-button}

Determinados fluxos de trabalho de criação podem precisar limitar a capacidade do autor de conteúdo de duplicar componentes. Você pode desabilitar o [ícone de duplicação](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) adicionando os seguintes metadados.

```html
<meta name="urn:adobe:aue:config:disable" content="duplicate"/>
```

## Desativação de Copiar e Colar {#copy-paste}

Determinados fluxos de trabalho de criação podem precisar limitar a capacidade do autor de conteúdo de copiar e colar componentes. Você pode desabilitar os [ícones copiar e colar](/help/sites-cloud/authoring/universal-editor/authoring.md#copy-paste) adicionando os seguintes metadados.

```html
<meta name="urn:adobe:aue:config:disable" content="copy"/>
```

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

Você pode especificar uma URL de visualização personalizada por meio de uma metaconfiguração de `urn:adobe:aue:config:preview`, que será aberta ao clicar no botão **Abrir página** na barra de ferramentas superior direita do editor [](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar).

Para fazer isso, basta incluir o URL de visualização desejado em uma meta tag do aplicativo instrumentado, como no exemplo a seguir.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
