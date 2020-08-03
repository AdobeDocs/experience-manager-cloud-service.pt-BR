---
title: Configurações avançadas de URL
description: Configurações avançadas de URL
translation-type: tm+mt
source-git-commit: 3a235e3d8e2d97e413f445df1f0bfe52e97024b3
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---


# Configurações avançadas de URL {#url}

[AEM CIF Componentes](https://github.com/adobe/aem-core-cif-components) principais fornece configurações avançadas para personalizar os URLs das páginas de produtos e categorias. Muitas implementações personalizarão esses URLs para fins de otimização de mecanismo de pesquisa (SEO).  O vídeo a seguir mostra detalhes sobre como configurar o `UrlProvider` Serviço e os recursos do [Sling Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para personalizar os URLs das páginas de produto e categoria.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuração {#configuration}

Para configurar o `UrlProvider` serviço de acordo com os requisitos SEO e precisar de um projeto, é necessário fornecer uma configuração OSGI para a configuração &quot;CIF do provedor de URL&quot; e configurar o serviço conforme descrito abaixo.

>[!NOTE]
>
> O projeto da loja [de referência de](https://github.com/adobe/aem-cif-guides-venia) Venia, veja abaixo, inclui configurações de amostra para demonstrar o uso de URLs personalizados para páginas de produtos e categorias.

### Modelo de URL da página do produto {#product}

Isso configura os URLs das páginas de produtos com as seguintes propriedades:

* **Modelo** de URL do produto: define o formato de URLs com um conjunto de espaços reservados. O valor padrão é `{{page}}.{{url_key}}.html#{{variant_sku}}`, o que acaba gerando URLs como, por exemplo, `/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange`
   * `{{page}}` foi substituído por `/content/venia/us/en/products/product-page`
   * `{{url_key}}` foi substituída por Magento `url_key` de propriedade do produto, `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` foi substituída pela variante selecionada no momento, aqui `MH01-M-Orange`
* **Localização** do identificador do produto: define o local do identificador que será usado para buscar os dados do produto. O valor padrão é `SELECTOR`, o outro valor possível é `SUFFIX`. Com o URL de exemplo anterior, isso significa que o identificador `chaz-kangeroo-hoodie` será usado para buscar os dados do produto.
* **Tipo** de identificador do produto: define o tipo do identificador a ser usado ao buscar os dados do produto. O valor padrão é `URL_KEY`, o outro valor possível é `SKU`. Com o URL de exemplo anterior, isso significa que os dados do produto serão obtidos com um filtro Magento GraphQL como `filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`.

### Modelo de URL da página de lista do produto {#product-list}

Isso configura os URLs das páginas de categoria ou lista do produto com as seguintes propriedades:

* **Modelo** de URL de Categoria: define o formato de URLs com um conjunto de espaços reservados. O valor padrão é `{{page}}.{{id}}.html`, o que acaba gerando URLs como, por exemplo, `/content/venia/us/en/products/category-page.3.html`
   * `{{page}}` foi substituído por `/content/venia/us/en/products/category-page`
   * `{{id}}` foi substituída por Magento, aqui `id` a propriedade da categoria `3`
* **Localização** do identificador de Categoria: define o local do identificador que será usado para buscar os dados do produto. O valor padrão é `SELECTOR`, o outro valor possível é `SUFFIX`. Com o URL de exemplo anterior, isso significa que o identificador `3` será usado para buscar os dados do produto.
* **Tipo** de identificador de Categoria: define o tipo do identificador a ser usado ao buscar os dados do produto. O valor padrão e o valor atualmente suportado é `ID`. Com o URL de exemplo anterior, isso significa que os dados da categoria serão obtidos com um filtro Magento GraphQL como `category(id:3)`.

É possível adicionar propriedades personalizadas para cada modelo, desde que os dados correspondentes estejam sendo definidos pelos componentes que usam o `UrlProvider`. Verifique, por exemplo, o código da `ProductListItemImpl` classe para descobrir como isso é implementado.

Também é possível substituir o `UrlProvider` serviço por um serviço OSGi totalmente personalizado. Nesse caso, é necessário implementar a `UrlProvider` interface e registrá-la com uma classificação de serviço mais alta para substituir a implementação padrão.

## Combinar com mapeamentos Sling {#sling-mapping}

Além do `UrlProvider`, também é possível configurar os [Sling Mappings](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para reescrever e processar URLs. O projeto AEM Archetype também fornece [um exemplo de configuração](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) para configurar alguns Mapeamentos Sling para a porta 4503 (publicação) e 80 (despachante).

## Combinar com AEM Dispatcher {#dispatcher}

As regravações de URL também podem ser alcançadas usando AEM servidor HTTP Dispatcher com `mod_rewrite` módulo. O [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) fornece uma referência AEM configuração do Dispatcher que já inclui regras [básicas de](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) regravação para o tamanho gerado.

## Exemplo

O projeto da loja [de referência de](https://github.com/adobe/aem-cif-guides-venia) Venia inclui configurações de amostra para demonstrar o uso de URLs personalizados para páginas de produtos e categorias. Isso permite que cada projeto configure padrões de URL individuais para páginas de produtos e categorias de acordo com suas necessidades de SEO. É utilizada uma combinação de imagens CIF `UrlProvider` e Sling, conforme descrito acima.

>[!NOTE]
>
>Essa configuração deve ser ajustada com o domínio externo usado pelo projeto. Os Mapeamentos Sling estão funcionando com base no nome do host e no domínio. Portanto, essa configuração é desativada por padrão e deve ser ativada antes da implantação. Para fazer isso, renomeie a `hostname.adobeaemcloud.com` pasta Sling Mapping de `ui.content/src/main/content/jcr_root/etc/map.publish/https` acordo com o nome de domínio usado e ative essa configuração adicionando `resource.resolver.map.location="/etc/map.publish"` à `JcrResourceResolver` configuração do projeto.

## Recursos adicionais

* [Venia Reference store](https://github.com/adobe/aem-cif-guides-venia)
* [Mapeamento de recursos AEM](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Mapeamentos Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
