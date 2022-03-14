---
title: Ativação de exportação em JSON para um componente
description: Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 11%

---

# Ativação de exportação em JSON para um componente {#enabling-json-export-for-a-component}

Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.

## Visão geral {#overview}

A exportação JSON é baseada em [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html)e no [Exportador de Modelo Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) , que depende [Anotações de Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Isso significa que o componente deve ter um Modelo do Sling se precisar exportar JSON. Portanto, será necessário seguir essas duas etapas para habilitar a exportação JSON em qualquer componente.

* [Definir um Modelo do Sling para o componente](#define-a-sling-model-for-the-component)
* [Anotar a interface do Modelo do Sling](#annotate-the-sling-model-interface)

## Definir um Modelo do Sling para o Componente {#define-a-sling-model-for-the-component}

Primeiro, um Modelo do Sling deve ser definido para o componente.

>[!NOTE]
>
>Para obter um exemplo de uso de Modelos do Sling, consulte o artigo [Desenvolvendo exportadores do modelo Sling em AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=pt-BR).

A classe de implementação do Modelo Sling deve ser anotada com o seguinte:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Isso garante que seu componente possa ser exportado sozinho, usando a variável `.model` e o `.json` extensão.

Além disso, isso especifica que a classe do Modelo do Sling pode ser adaptada ao `ComponentExporter` interface.

>[!NOTE]
>
>As anotações Jackson geralmente não são especificadas no nível de classe do Modelo do Sling, mas no nível de interface do Modelo. Isso garante que a Exportação JSON seja considerada como parte da API do componente.

>[!NOTE]
>
>O `ExporterConstants` e `ComponentExporter` as classes vêm do `com.adobe.cq.export.json` pacote.

### Uso de vários seletores {#multiple-selectors}

Embora não seja um caso de uso padrão, é possível configurar vários seletores além do `model` seletor.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

No entanto, nesse caso, o `model` o seletor deve ser o primeiro seletor e a extensão deve ser `.json`.

## Anotar a interface do modelo Sling {#annotate-the-sling-model-interface}

Para ser considerado pelo quadro do exportador JSON, a interface do modelo deve implementar a variável `ComponentExporter` interface (ou `ContainerExporter`, no caso de um componente de contêiner).

A interface correspondente do Modelo do Sling (`MyComponent`) seria anotada usando [Anotações de Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir como ele deve ser exportado (serializado).

A interface Modelo precisa ser anotada corretamente para definir quais métodos devem ser serializados. Por padrão, todos os métodos que respeitam a convenção de nomenclatura usual para getters serão serializados e derivarão seus nomes de propriedades JSON naturalmente dos nomes getter. Isso pode ser evitado ou substituído por `@JsonIgnore` ou `@JsonProperty` para renomear a propriedade JSON.

## Exemplo {#example}

[Os componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) oferecem suporte para exportação JSON e podem ser usadas como referência.

Para obter um exemplo, consulte a implementação do Modelo do Sling do Componente principal de imagem e sua interface anotada.

## Documentação relacionada {#related-documentation}

Para obter mais detalhes, consulte:

* [Fragmentos de conteúdo no guia do usuário Ativos](/help/assets/content-fragments/content-fragments.md)
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
* [Criação com fragmentos de conteúdo](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) e [Componente do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=pt-BR)
