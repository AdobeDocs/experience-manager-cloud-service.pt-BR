---
title: Ativando a exportação JSON para um componente
description: Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 7%

---


# Ativando a exportação JSON para um componente {#enabling-json-export-for-a-component}

Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.

## Visão geral {#overview}

A exportação JSON é baseada em [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html) e na estrutura [Exportador de Modelo Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (que depende ela própria de [anotações Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Isso significa que o componente deve ter um Modelo Sling se precisar exportar JSON. Portanto, você precisará seguir estas duas etapas para ativar a exportação JSON em qualquer componente.

* [Definir um Modelo Sling para o componente](#define-a-sling-model-for-the-component)
* [Anotar na interface do Sling Model](#annotate-the-sling-model-interface)

## Definir um Modelo Sling para o Componente {#define-a-sling-model-for-the-component}

Primeiro, um Modelo Sling deve ser definido para o componente.

>[!NOTE]
>
>Para obter um exemplo de uso de Modelos Sling, consulte o artigo [Desenvolvimento de exportadores de modelos Sling em AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

A classe de implementação do Modelo Sling deve ser anotada com o seguinte:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Isso garante que seu componente possa ser exportado sozinho, usando o seletor `.model` e a extensão `.json`.

Além disso, isso especifica que a classe Sling Model pode ser adaptada à interface `ComponentExporter`.

>[!NOTE]
>
>As anotações Jackson geralmente não são especificadas no nível de classe do Sling Model, mas sim no nível de interface do Modelo. Isso garante que a exportação JSON seja considerada como parte da API do componente.

>[!NOTE]
>
>As classes `ExporterConstants` e `ComponentExporter` vêm do pacote `com.adobe.cq.export.json`.

### Usando vários seletores {#multiple-selectors}

Embora não seja um caso de uso padrão, é possível configurar vários seletores além do seletor `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Entretanto, nesse caso, o seletor `model` deve ser o primeiro seletor e a extensão deve ser `.json`.

## Anotar na interface do modelo Sling {#annotate-the-sling-model-interface}

Para ser tida em conta pelo quadro do Exportador JSON, a interface Model deve implementar a interface `ComponentExporter` (ou `ContainerExporter`, no caso de um componente de container).

A interface correspondente do Modelo Sling (`MyComponent`) seria anotada usando [anotações Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir como deve ser exportada (serializada).

A interface Modelo precisa ser anotada corretamente para definir quais métodos devem ser serializados. Por padrão, todos os métodos que respeitam a convenção de nomenclatura comum para getters serão serializados e derivarão seus nomes de propriedades JSON naturalmente dos nomes do getter. Isso pode ser evitado ou substituído usando `@JsonIgnore` ou `@JsonProperty` para renomear a propriedade JSON.

## Exemplo {#example}

[Os Componentes principais ](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) suportam a exportação JSON e podem ser usados como referência.

Para ver um exemplo, consulte a implementação do Modelo Sling do Componente principal de imagem e sua interface anotada.

## Documentação relacionada {#related-documentation}

Para mais informações, consulte:

* [Fragmentos de conteúdo no guia do usuário Ativos](/help/assets/content-fragments/content-fragments.md)
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
* [Criação com fragmentos de conteúdo](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componentes principais ](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) e o componente Fragmento  [do conteúdo](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/components/content-fragment-component.html)
