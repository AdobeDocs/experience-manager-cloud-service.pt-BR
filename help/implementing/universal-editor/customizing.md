---
title: Personalização e extensão do Editor universal
description: Saiba mais sobre os diferentes pontos de extensão e outros recursos que permitem personalizar a interface do usuário do Editor universal para atender às necessidades dos autores de conteúdo.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: afcb3cbc2b0868de7bac9446eb07ae30c033de66
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# Personalização e extensão do Editor universal {#customizing-extending}

Saiba mais sobre os diferentes pontos de extensão e outros recursos que permitem personalizar a experiência de criação do Editor universal para atender às necessidades dos autores de conteúdo.

## Visão geral {#overview}

O Editor universal permite dois tipos de adaptação para as necessidades do seu projeto.

* [Personalizando o Editor Universal](#customizing) - A funcionalidade padrão do Editor Universal pode ser adaptada por meio de várias configurações de personalização.
* [Extensão da interface do Universal Editor](#extending) - A interface do Universal Editor também pode ser estendida usando o App Builder para atender às suas necessidades de projetos.

Ambos os tipos são detalhados nas seções a seguir.

## Personalização do Editor universal {#customizing}

O Editor universal oferece várias opções integradas para personalizar sua funcionalidade.

### Desabilitar publicação {#disable-publish}

Determinados workflows de criação exigem que o conteúdo seja revisado antes de ser publicado. Nessas situações, a opção de publicar não deve estar disponível para nenhum autor.

Portanto, o botão **Publish** pode ser totalmente suprimido em um aplicativo adicionando os seguintes metadados.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

### Componentes de filtragem {#filtering-components}

Você pode restringir os componentes permitidos por contêiner no Editor universal usando filtros de componente. Consulte o documento [Componentes de Filtragem](/help/implementing/universal-editor/filtering.md) para obter mais informações.

### Mostrar e ocultar componentes condicionalmente no painel Propriedades {#conditionally-hide}

Embora um componente ou componentes possam estar disponíveis para os autores, pode haver certas situações em que isso não faça sentido. Nesses casos, você pode ocultar componentes no painel de propriedades adicionando um atributo `condition` aos [ campos do modelo de componente.](/help/implementing/universal-editor/field-types.md#fields)

As condições podem ser definidas usando o esquema JsonLogic [.](https://jsonlogic.com/) Se a condição for verdadeira, o campo será exibido. Se a condição for falsa, o campo ficará oculto.

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

### URLs de visualização personalizados {#custom-preview-urls}

Você pode especificar uma URL de visualização personalizada por meio de uma metaconfiguração `urn:adobe:aue:config:preview`, que será aberta ao clicar no botão **Abrir página** na barra de ferramentas superior direita do editor [.](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar)

Isso é particularmente útil para aplicativos com requisitos de visualização específicos, como os [que usam Edge Delivery Services com criação no WYSIWYG.](/help/edge/wysiwyg-authoring/authoring.md)

Para fazer isso, basta incluir o URL de visualização desejado em uma meta tag do aplicativo instrumentado, como no exemplo a seguir.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```

## Extensão da interface do editor universal {#extending}

Como um serviço do Adobe Experience Cloud, a interface do editor universal pode ser estendida usando o App Builder e o Experience Manager.

As extensões de interface do usuário são aplicativos do JavaScript criados com o Adobe App Builder que podem ser incorporados em aplicativos de interface do usuário executados no Adobe Experience Cloud Unified Shell, como o Editor universal. Você pode adicionar seus próprios botões e ações ao menu de cabeçalho e ao painel de propriedades, bem como criar seus próprios eventos para o Editor universal.

Se você quiser explorar essas possibilidades, consulte os seguintes recursos:

1. [Extensibilidade da Interface do Usuário](https://developer.adobe.com/uix/docs/) - Esta é a documentação do desenvolvedor para a extensão da Interface do Usuário.
1. [Guias de Extensibilidade da Interface do Usuário](https://developer.adobe.com/uix/docs/guides/) - Instruções detalhadas sobre como desenvolver sua própria extensão
1. [Os Pontos de Extensão do Editor Universal](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - Documentação de pontos de extensão específicos do Editor Universal

>[!TIP]
>
>Se preferir aprender por exemplo, consulte o [tutorial sobre extensibilidade da interface do AEM.](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview) Embora se concentre na extensão do console de Fragmentos de Conteúdo, os conceitos para implementar uma extensão de interface no Editor Universal são os mesmos.

[Usando o Extension Manager no AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/), você pode habilitar ou desabilitar suas extensões por instância, acessar extensões próprias do Adobe, inclusive as do Universal Editor, e muito mais.
