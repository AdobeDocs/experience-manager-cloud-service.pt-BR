---
title: Ativação de exportação em JSON para um componente
description: Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 12%

---

# Ativação de exportação em JSON para um componente {#enabling-json-export-for-a-component}

Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.

## Visão geral {#overview}

A exportação JSON é baseada em [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html)e no [Exportador de modelo Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) quadro regulamentar (que, por sua vez, se baseia [Anotações Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Isso significa que o componente deve ter um Modelo Sling se precisar exportar JSON. Portanto, será necessário seguir essas duas etapas para habilitar a exportação JSON em qualquer componente.

* [Definir um modelo do Sling para o componente](#define-a-sling-model-for-the-component)
* [Anotar a interface do Modelo do Sling](#annotate-the-sling-model-interface)

## Definir um modelo do Sling para o componente {#define-a-sling-model-for-the-component}

Primeiro, um modelo Sling deve ser definido para o componente.

>[!NOTE]
>
>Para obter um exemplo do uso de Modelos Sling, consulte o artigo [Desenvolvimento de exportadores de modelos de sling no AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=pt-BR).

A classe de implementação do Modelo do Sling deve ser anotada com o seguinte:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Isso garante que seu componente possa ser exportado sozinho, usando o `.model` seletor e o `.json` extensão.

Além disso, especifica que a classe Modelo do Sling pode ser adaptada na variável `ComponentExporter` interface.

>[!NOTE]
>
>As anotações Jackson geralmente não são especificadas no nível de classe do Modelo Sling, mas no nível da interface do Modelo. Isso garante que a Exportação JSON seja considerada como parte da API do componente.

>[!NOTE]
>
>A variável `ExporterConstants` e `ComponentExporter` as classes são provenientes da `com.adobe.cq.export.json` pacote.

### Uso de vários seletores {#multiple-selectors}

Embora não seja um caso de uso padrão, é possível configurar vários seletores além do `model` seletor.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

No entanto, nesse caso, a `model` seletor deve ser o primeiro seletor e a extensão deve ser `.json`.

## Anotar a interface do modelo Sling {#annotate-the-sling-model-interface}

Para ser considerada pela estrutura do Exportador JSON, a interface do Modelo deve implementar a `ComponentExporter` (ou `ContainerExporter`, no caso de um componente de contentor).

A interface do modelo Sling correspondente (`MyComponent`) seria então anotado usando [Anotações Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir como ele deve ser exportado (serializado).

A interface do modelo precisa ser anotada corretamente para definir quais métodos devem ser serializados. Por padrão, todos os métodos que respeitam a convenção de nomenclatura usual para getters são serializados e derivarão seus nomes de propriedade JSON naturalmente dos nomes de getter. Isso pode ser evitado ou substituído usando `@JsonIgnore` ou `@JsonProperty` para renomear a propriedade JSON.

## Exemplo {#example}

[Os Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) são compatíveis com a exportação JSON e podem ser usados como referência.

Para obter um exemplo, consulte a implementação do Modelo Sling do Componente principal de imagem e sua interface anotada.

## Documentação relacionada {#related-documentation}

Para obter mais detalhes, consulte:

* [Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)
* [Modelos de fragmentos do conteúdo](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [Criação com fragmentos de conteúdo](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) e a variável [Componente Fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=pt-BR)
