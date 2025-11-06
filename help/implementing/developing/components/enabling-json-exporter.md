---
title: Habilitação de exportação em JSON para um componente
description: Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 6%

---

# Habilitação de exportação em JSON para um componente {#enabling-json-export-for-a-component}

Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.

## Visão geral {#overview}

A exportação JSON é baseada em [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html) e na estrutura [Exportador de Modelo Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (que depende de [Anotações Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Isso significa que o componente deve ter um Modelo Sling se precisar exportar JSON. Portanto, siga estas duas etapas para ativar a exportação JSON em qualquer componente.

* [Definir um modelo do Sling para o componente](#define-a-sling-model-for-the-component)
* [Anotar a interface do Modelo do Sling](#annotate-the-sling-model-interface)

## Definir um modelo do Sling para o componente {#define-a-sling-model-for-the-component}

Primeiro, um modelo Sling deve ser definido para o componente.

>[!NOTE]
>
>Para obter um exemplo do uso de Modelos Sling, consulte o artigo [Desenvolvendo exportadores de modelos Sling no AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=pt-BR).

A classe de implementação do Modelo do Sling deve ser anotada com o seguinte:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Isso garante que seu componente possa ser exportado sozinho, usando o seletor `.model` e a extensão `.json`.

Além disso, isso especifica que a classe Sling Model pode ser adaptada à interface `ComponentExporter`.

>[!NOTE]
>
>As anotações Jackson geralmente não são especificadas no nível de classe do Modelo Sling, mas no nível da interface do Modelo. Isso garante que a Exportação JSON seja considerada como parte da API do componente.

>[!NOTE]
>
>As classes `ExporterConstants` e `ComponentExporter` vêm do pacote `com.adobe.cq.export.json`.

### Uso de vários seletores {#multiple-selectors}

Embora não seja um caso de uso padrão, é possível configurar vários seletores além do seletor `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

No entanto, nesse caso, o seletor `model` deve ser o primeiro e a extensão deve ser `.json`.

## Anotar a interface do modelo Sling {#annotate-the-sling-model-interface}

Para ser considerada pela estrutura do Exportador JSON, a interface Modelo deve implementar a interface `ComponentExporter` (ou `ContainerExporter`, no caso de um componente de contêiner).

A interface do Modelo Sling correspondente (`MyComponent`) seria então anotada usando [anotações Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir como ela deve ser exportada (serializada).

A interface do modelo deve ser anotada corretamente para definir quais métodos devem ser serializados. Por padrão, todos os métodos que respeitam a convenção de nomenclatura usual para getters são serializados e derivarão seus nomes de propriedade JSON naturalmente dos nomes de getter. Isso pode ser evitado ou substituído usando `@JsonIgnore` ou `@JsonProperty` para renomear a propriedade JSON.

## Exemplo {#example}

[Os Componentes Principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction) oferecem suporte à exportação JSON e podem ser usados como referência.

Para obter um exemplo, consulte a implementação do Modelo Sling do Componente principal de imagem e sua interface anotada.

## Documentação relacionada {#related-documentation}

* [Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)
* [Modelos de fragmentos do conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [Criação com fragmentos de conteúdo](/help/sites-cloud/authoring/fragments/content-fragments.md)
* [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction) e o [componente de Fragmento de Conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=pt-BR)
