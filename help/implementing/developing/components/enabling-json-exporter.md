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

A exportação JSON baseia-se nos Modelos [de](https://sling.apache.org/documentation/bundles/models.html)Sling e no quadro do Exportador [do Modelo de](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) Sling (que, por sua vez, se baseia em anotações [](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)Jackson).

Isso significa que o componente deve ter um Modelo Sling se precisar exportar JSON. Portanto, você precisará seguir estas duas etapas para ativar a exportação JSON em qualquer componente.

* [Definir um Modelo Sling para o componente](#define-a-sling-model-for-the-component)
* [Anotar na interface do Sling Model](#annotate-the-sling-model-interface)

## Definir um Modelo Sling para o Componente {#define-a-sling-model-for-the-component}

Primeiro, um Modelo Sling deve ser definido para o componente.

>[!NOTE]
>
>Para obter um exemplo de uso de modelos Sling, consulte o artigo [Desenvolvendo exportadores de modelos Sling em AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

A classe de implementação do Modelo Sling deve ser anotada com o seguinte:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Isso garante que seu componente possa ser exportado sozinho, usando o `.model` seletor e a `.json` extensão.

Além disso, isso especifica que a classe Sling Model pode ser adaptada à `ComponentExporter` interface.

>[!NOTE]
>
>As anotações Jackson geralmente não são especificadas no nível de classe do Sling Model, mas sim no nível de interface do Modelo. Isso garante que a exportação JSON seja considerada como parte da API do componente.

>[!NOTE]
>
>As `ExporterConstants` e `ComponentExporter` as aulas vêm do `com.adobe.cq.export.json` pacote.

### Uso de vários seletores {#multiple-selectors}

Embora não seja um caso de uso padrão, é possível configurar vários seletores além do `model` seletor.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Entretanto, nesse caso, o `model` seletor deve ser o primeiro seletor e a extensão deve ser `.json`.

## Anotar na interface do modelo Sling {#annotate-the-sling-model-interface}

A fim de ser tido em conta pelo quadro do exportador JSON, a interface modelo deve implementar a `ComponentExporter` interface (ou `ContainerExporter`, no caso de um componente container).

A interface correspondente do Modelo Sling (`MyComponent`) seria anotada usando anotações [](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) Jackson para definir como deve ser exportada (serializada).

A interface Modelo precisa ser anotada corretamente para definir quais métodos devem ser serializados. Por padrão, todos os métodos que respeitam a convenção de nomenclatura comum para getters serão serializados e derivarão seus nomes de propriedades JSON naturalmente dos nomes do getter. Isso pode ser impedido ou substituído usando `@JsonIgnore` ou `@JsonProperty` para renomear a propriedade JSON.

## Exemplo {#example}

[Os Componentes](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) principais suportam exportação JSON e podem ser usados como referência.

Para ver um exemplo, consulte a implementação do Modelo Sling do Componente principal de imagem e sua interface anotada.

## Related Documentation {#related-documentation}

Para mais informações, consulte:

* [Fragmentos de conteúdo no guia do usuário Ativos](/help/assets/content-fragments/content-fragments.md)
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
* [Criação com fragmentos de conteúdo](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componentes](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) principais e o componente Fragmento [do conteúdo](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/components/content-fragment-component.html)
