---
title: Ativando a exportação JSON para um componente
description: Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 4%

---

# Ativando a Exportação JSON para um Componente {#enabling-json-export-for-a-component}

Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.

## Visão geral {#overview}

A exportação JSON é baseada em [Modelos do Sling](https://sling.apache.org/documentation/bundles/models.html) e na estrutura [Exportador de Modelo do Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (que ela mesma depende de [Anotações do Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Isso significa que o componente deve ter um Modelo do Sling se precisar exportar JSON. Portanto, será necessário seguir essas duas etapas para habilitar a exportação JSON em qualquer componente.

* [Definir um Modelo do Sling para o componente](#define-a-sling-model-for-the-component)
* [Anotar a interface do Modelo do Sling](#annotate-the-sling-model-interface)

## Definir um Modelo do Sling para o Componente {#define-a-sling-model-for-the-component}

Primeiro, um Modelo do Sling deve ser definido para o componente.

>[!NOTE]
>
>Para obter um exemplo de uso de Modelos do Sling, consulte o artigo [Desenvolvendo exportadores de modelos do Sling em AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

A classe de implementação do Modelo Sling deve ser anotada com o seguinte:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Isso garante que seu componente possa ser exportado sozinho, usando o seletor `.model` e a extensão `.json`.

Além disso, isso especifica que a classe do Modelo do Sling pode ser adaptada à interface `ComponentExporter` .

>[!NOTE]
>
>As anotações Jackson geralmente não são especificadas no nível de classe do Modelo do Sling, mas no nível de interface do Modelo. Isso garante que a Exportação JSON seja considerada como parte da API do componente.

>[!NOTE]
>
>As classes `ExporterConstants` e `ComponentExporter` vêm do pacote `com.adobe.cq.export.json`.

### Uso de vários seletores {#multiple-selectors}

Embora não seja um caso de uso padrão, é possível configurar vários seletores além do seletor `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

No entanto, nesse caso, o seletor `model` deve ser o primeiro seletor e a extensão deve ser `.json`.

## Anotar a interface do modelo Sling {#annotate-the-sling-model-interface}

Para ser considerado pela estrutura do Exportador JSON, a interface Modelo deve implementar a interface `ComponentExporter` (ou `ContainerExporter`, no caso de um componente de contêiner).

A interface do Modelo Sling correspondente (`MyComponent`) seria anotada usando [Anotações Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir como ela deve ser exportada (serializada).

A interface Modelo precisa ser anotada corretamente para definir quais métodos devem ser serializados. Por padrão, todos os métodos que respeitam a convenção de nomenclatura usual para getters serão serializados e derivarão seus nomes de propriedades JSON naturalmente dos nomes getter. Isso pode ser evitado ou substituído usando `@JsonIgnore` ou `@JsonProperty` para renomear a propriedade JSON.

## Exemplo {#example}

[Os ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) Componentes principais são compatíveis com a exportação de JSON e podem ser usados como referência.

Para obter um exemplo, consulte a implementação do Modelo do Sling do Componente principal de imagem e sua interface anotada.

## Documentação relacionada {#related-documentation}

Para obter mais detalhes, consulte:

* [Fragmentos de conteúdo no guia do usuário Ativos](/help/assets/content-fragments/content-fragments.md)
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
* [Criação com fragmentos de conteúdo](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componentes principais ](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) e o componente Fragmento  [de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)
