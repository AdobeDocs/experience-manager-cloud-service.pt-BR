---
title: Exportador JSON para serviços de conteúdo
description: AEM Content Services foram criados para generalizar a descrição e o delivery do conteúdo de/para AEM além de um foco nas páginas da Web. Eles fornecem o delivery do conteúdo para canais que não são tradicionais AEM páginas da Web, usando métodos padronizados que podem ser consumidos por qualquer cliente.
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 7%

---


# Exportador JSON para serviços de conteúdo {#json-exporter-for-content-services}

AEM Content Services foram criados para generalizar a descrição e o delivery do conteúdo de/para AEM além do foco das páginas da Web.

Eles fornecem o delivery do conteúdo para canais que não são tradicionais AEM páginas da Web, usando métodos padronizados que podem ser consumidos por qualquer cliente. Esses canais podem incluir:

* Aplicativos de página única
* Aplicativos móveis nativos
* Outros canais e pontos de contato externos ao AEM

Com fragmentos de conteúdo que usam conteúdo estruturado, você pode fornecer serviços de conteúdo usando o exportador JSON para fornecer o conteúdo de uma página AEM no formato de modelo de dados JSON. Isso pode ser consumido por seus próprios aplicativos.

## Exportador JSON com componentes principais do fragmento de conteúdo {#json-exporter-with-content-fragment-core-components}

Usando o exportador JSON AEM, você pode fornecer o conteúdo de uma página AEM no formato de modelo de dados JSON. Isso pode ser consumido por seus próprios aplicativos.

Dentro AEM delivery é obtido usando o seletor `model` e a `.json` extensão.

`.model.json`

1. Por exemplo, um URL como:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. Fornecerá conteúdo como:

   ![Modelo JSON de conteúdo WKND](assets/json-model-wknd.png)

Como alternativa, é possível fornecer o conteúdo de um fragmento de conteúdo estruturado, direcionando-o especificamente.

Isso é feito usando todo o caminho até o fragmento (por meio do `jcr:content`); por exemplo, com um sufixo como.

`.../jcr:content/root/container/container/contentfragment.model.json`

Sua página pode conter um único fragmento de conteúdo ou vários componentes de vários tipos. Você também pode usar mecanismos como componentes de lista para pesquisar automaticamente o conteúdo relevante.

* Por exemplo, um URL como:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
   ```

* Fornecerá conteúdo como:

   ![Modelo JSON do fragmento de conteúdo WKND](assets/json-model-wknd-content-fragment.png)

   >[!NOTE]
   >
   >Você pode [adaptar seus próprios componentes](enabling-json-exporter.md) para acessar e usar esses dados.

   >[!NOTE]
   >
   >Embora não seja uma implementação padrão, há suporte para [vários seletores,](enabling-json-exporter.md#multiple-selectors) mas eles `model` devem ser os primeiros.

### Informações adicionais {#further-information}

Consulte também:

* API HTTP de ativos
   * [API HTTP de ativos](/help/assets/developer-reference-material-apis.md)
* Modelos Sling:
   * [Modelos Sling - Associando uma classe de modelo a um tipo de recurso desde 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM com JSON:
   * [Ativando a exportação JSON para um componente](enabling-json-exporter.md)

## Related Documentation {#related-documentation}

Para mais informações, consulte:

* [Fragmentos de conteúdo no guia do usuário Ativos](/help/assets/content-fragments/content-fragments.md)
* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
* [Criação com fragmentos de conteúdo](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componentes](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) principais e o componente Fragmento [do conteúdo](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/components/content-fragment-component.html)
