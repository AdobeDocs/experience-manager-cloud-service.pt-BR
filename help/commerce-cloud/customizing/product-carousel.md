---
title: Atributos personalizados para o carrossel de produtos CIF
description: AEM Saiba como estender o componente Carrossel do produto CIF atualizando o Modelo Sling e personalizando a marcação.
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 594f0e6ec88851c86134be8d5d7f1719f74ddf4f
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Atributos personalizados para o carrossel de produtos CIF {#product-carousel}

## Introdução {#intro}

O componente Carrossel de produtos é estendido por todo este tutorial. Como primeira etapa, adicione uma instância do Carrossel do produto à página inicial para entender a funcionalidade da linha de base:

1. Navegue até a Página inicial do site, por exemplo [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)
1. Insira um novo componente Carrossel do produto no container do layout principal da página.
   ![Componente do carrossel de produtos](/help/commerce-cloud/assets/product-carousel-component.png)
1. Expanda o painel lateral (se ainda não estiver sendo exibido) e na lista suspensa do localizador de ativos selecione **Produtos**.
     ![Produtos do carrossel](/help/commerce-cloud/assets/carousel-products.png)    
1. Isso deve exibir uma lista de produtos disponíveis em uma instância conectada do Adobe Commerce.
   ![Instância conectada](/help/commerce-cloud/assets/connected-instance.png)
1. Os produtos serão exibidos abaixo com as propriedades padrão:
   ![Produto mostrado com propriedades](/help/commerce-cloud/assets/discount.png)

## Atualizar o modelo do Sling {#update-sling-model}

É possível estender a lógica de negócios do Carrossel de produtos implementando um Modelo do Sling:

1. No IDE, navegue no módulo principal para `core/src/main/java/com/venia/core/models/commerce` e crie uma interface CustomCarousel que estende a interface CIF ProductCarousel:

   ```
   package com.venia.core.models.commerce;
   import com.adobe.cq.commerce.core.components.models.productcarousel.ProductCarousel;
   public interface CustomCarousel extends ProductCarousel {
   }
   ```
1. Em seguida, crie uma classe de implementação `CustomCarouselImpl.java` em `core/src/main/java/com/venia/core/models/commerce/CustomCarouselImpl.java`.
O padrão de delegação para Modelos do Sling permite `CustomCarouselImpl` para referência `ProductCarousel` por meio da `sling:resourceSuperType` propriedade:

   ```
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductCarousel productCarousel;
   ```

1. A anotação @PostConstruct garante que esse método seja chamado quando o Modelo Sling for inicializado. A consulta do GraphQL do produto já foi estendida usando o método extendProductQueryWith para recuperar atributos. Atualize a consulta do GraphQL para incluir o atributo na consulta parcial:

   ```
   @PostConstruct
   private void initModel() {
   productsRetriever = productCarousel.getProductsRetriever();
   
   if(productCarousel.getProductsRetriever() != null)
   productCarousel.getProductsRetriever().extendProductQueryWith(p -> p
   .createdAt()
   .addCustomSimpleField("accessory_gemstone_addon")
   );
   }
   ```

   No código acima, a variável `addCustomSimpleField` é usado para recuperar o `accessory_gemstone_addon` atributo.

## Personalização da marcação {#customize-markup}

Para personalizar ainda mais a marcação:

1. Criar uma cópia de `productcard.html` de `/apps/core/cif/components/commerce/productcarousel/v1/productcarousel` (o caminho crxde do componente principal) para o módulo ui.apps `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productcarousel/productcard.html`.

1. Editar `productcard.html` para chamar o atributo personalizado, que é mencionado na classe de implementação:

   ```xml
   ..
   <div
       data-product-sku="${product.commerceIdentifier.value}"
       data-product-base-sku="${product.combinedSku.baseSku}"
       id="${product.id}"
       data-cmp-data-layer="${product.data.json}"
       class="card product__card">
       <span>${product.product.responseData['accessory_gemstone_addon']}</span>
       <a href="${product.URL}"
           target="${productCarousel.linkTarget}"
   ..
   ```

1. Salve as alterações e implante as atualizações no AEM usando o comando Maven, em um terminal de linha de comando. Você poderá ver o atributo personalizado `accessory_gemstone_addon` para os produtos selecionados na página.
