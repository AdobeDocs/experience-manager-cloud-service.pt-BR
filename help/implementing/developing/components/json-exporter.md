---
title: Exportador JSON para serviços de conteúdo
description: Os Serviços de conteúdo da AEM foram projetados para generalizar a descrição e a entrega de conteúdo de/para o AEM além do foco em páginas da Web. Eles fornecem a entrega de conteúdo para canais que não são páginas da Web tradicionais do AEM, usando métodos padronizados que podem ser consumidos por qualquer cliente.
exl-id: d3ddffb7-cef9-4c86-aa31-175f13f9b4a5
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 17%

---

# Exportador JSON para serviços de conteúdo {#json-exporter-for-content-services}

Os Serviços de conteúdo da AEM foram projetados para generalizar a descrição e a entrega de conteúdo de/para o AEM além do foco das páginas da Web.

Eles realizam a entrega de conteúdo para canais que não são páginas da Web tradicionais do AEM, usando métodos padronizados que podem ser consumidos por qualquer cliente. Esses canais podem incluir:

* Aplicativos de página única
* Aplicativos nativos para dispositivos móveis
* Outros canais e pontos de contato externos ao AEM

Com fragmentos de conteúdo que usam conteúdo estruturado, você pode fornecer serviços de conteúdo usando o exportador JSON para fornecer o conteúdo de uma página do AEM no formato de modelo de dados JSON. Isso pode ser consumido por seus próprios aplicativos.

## Exportador JSON com componentes principais de fragmento de conteúdo {#json-exporter-with-content-fragment-core-components}

Usando o exportador JSON do AEM, você pode fornecer o conteúdo de uma página do AEM no formato de modelo de dados JSON. Isso pode ser consumido por seus próprios aplicativos.

No AEM, a entrega é realizada usando o seletor `model` e a extensão `.json`.

`.model.json`

1. Por exemplo, um URL como:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. Fornecerá conteúdo como:

   ![Modelo JSON de conteúdo WKND](assets/json-model-wknd.png)

Como alternativa, você pode fornecer o conteúdo de um fragmento de conteúdo estruturado direcionando-o especificamente.

Isso é feito usando o caminho inteiro para o fragmento (por meio de `jcr:content`); por exemplo, com um sufixo como.

`.../jcr:content/root/container/container/contentfragment.model.json`

Sua página pode conter um único fragmento de conteúdo ou vários componentes de vários tipos. Você também pode usar mecanismos como componentes de lista para pesquisar automaticamente conteúdo relevante.

* Por exemplo, um URL como:

  ```shell
  http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
  ```

* Fornecerá conteúdo como:

  ![Modelo JSON de fragmento de conteúdo WKND](assets/json-model-wknd-content-fragment.png)

  >[!NOTE]
  >
  >Você pode [adaptar seus próprios componentes](enabling-json-exporter.md) para acessar e usar esses dados.

  >[!NOTE]
  >
  >Embora não seja uma implementação padrão, [há suporte para vários seletores](enabling-json-exporter.md#multiple-selectors), mas `model` deve ser o primeiro.

### Informações adicionais {#further-information}

* API HTTP de ativos
   * [API HTTP de ativos](/help/assets/developer-reference-material-apis.md)
* Modelos Sling:
   * [Modelos do Sling - Associando uma classe de modelo a um tipo de recurso desde 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM com JSON:
   * [Habilitação de exportação em JSON para um componente](enabling-json-exporter.md)

## Documentação relacionada {#related-documentation}

* [Fragmentos de conteúdo](/help/sites-cloud/administering/content-fragments/overview.md)
* [Modelos de fragmentos do conteúdo](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [Criação com fragmentos de conteúdo](/help/sites-cloud/authoring/fragments/content-fragments.md)
* [Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction) e o [componente de Fragmento de Conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=pt-BR)
