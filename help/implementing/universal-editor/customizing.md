---
title: Personalização e extensão do Editor universal
description: Saiba mais sobre os diferentes pontos de extensão e outros recursos que permitem personalizar a interface do usuário do Editor universal para atender às necessidades dos autores de conteúdo.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: bdd67fb383bf20399eacaf9b9c086ea8468ea742
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---


# Personalização e extensão do Editor universal {#customizing-extending}

Saiba mais sobre os diferentes pontos de extensão e outros recursos que permitem personalizar a experiência de criação do Editor universal para atender às necessidades dos autores de conteúdo.

## Visão geral {#overview}

O Editor universal permite dois tipos de adaptação para as necessidades do seu projeto.

* [Personalização do Editor universal](#customizing) - A funcionalidade padrão do Universal Editor pode ser adaptada por meio de várias configurações de personalização.
* [Extensão da interface do editor universal](#extending) - A interface do usuário do Editor universal também pode ser estendida usando o Construtor de aplicativos para atender às necessidades dos projetos.

Ambos os tipos são detalhados nas seções a seguir.

## Personalização do Editor universal {#customizing}

O Editor universal oferece várias opções integradas para personalizar sua funcionalidade.

### Desabilitar publicação {#disable-publish}

Determinados workflows de criação exigem que o conteúdo seja revisado antes de ser publicado. Nessas situações, a opção de publicar não deve estar disponível para nenhum autor.

A variável **Publish** Portanto, o botão pode ser totalmente suprimido em um aplicativo adicionando os seguintes metadados.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

### Componentes de filtragem {#filtering-components}

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

### Mostrar e ocultar componentes condicionalmente no painel Propriedades {#conditionally-hide}

Embora um componente ou componentes possam estar disponíveis para os autores, pode haver certas situações em que isso não faça sentido. Nesses casos, você pode ocultar componentes no painel de propriedades adicionando um `condition` atributo para o [campos do modelo de componente.](/help/implementing/universal-editor/field-types.md#fields)

As condições podem ser definidas usando [Esquema JsonLogic.](https://jsonlogic.com/) Se a condição for verdadeira, o campo será exibido. Se a condição for falsa, o campo ficará oculto.

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

![Campo de texto exibido](assets/shown.png)

>[!ENDTABS]

## Extensão da interface do editor universal {#extending}

Como um serviço do Adobe Experience Cloud, a interface do Editor universal pode ser estendida usando o Construtor de aplicativos e o Experience Manager.

Extensões de interface são aplicativos JavaScript criados com o Adobe App Builder que podem ser incorporados em aplicativos de interface do usuário executados no Adobe Experience Cloud Unified Shell, como o Universal Editor. Você pode adicionar seus próprios botões e ações ao menu de cabeçalho e ao painel de propriedades, bem como criar seus próprios eventos para o Editor universal.

Se você quiser explorar essas possibilidades, consulte os seguintes recursos:

1. [Extensibilidade da interface](https://developer.adobe.com/uix/docs/) - Esta é a documentação do desenvolvedor para a extensão da interface do usuário.
1. [Guias de extensibilidade da interface](https://developer.adobe.com/uix/docs/guides/) - Instruções detalhadas sobre como desenvolver sua própria extensão
1. [Os Pontos de Extensão do Universal Editor](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - Documentação de ponto de extensão específico do Editor universal

>[!TIP]
>
>Se preferir aprender através do exemplo, consulte a [Tutorial de extensibilidade da interface do AEM.](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview) Embora se concentre na extensão do console de Fragmentos de conteúdo, os conceitos para implementar uma extensão de interface no Editor universal são os mesmos.

[Utilização do Extension Manager no AEM Sites,](https://developer.adobe.com/uix/docs/extension-manager/) você pode ativar ou desativar suas extensões por instância, acessar extensões próprias do Adobe, incluindo as do Universal Editor, e muito mais.
