---
title: Atributos personalizados para o Carrossel de produtos do CIF
description: Saiba como estender o componente Carrossel de produtos do AEM CIF atualizando o Modelo do Sling e personalizando a marcação.
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 758e0e13-c4d8-4d32-bcc9-91a36b3ffa98
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---


# Atributos personalizados para o Carrossel de produtos do CIF {#product-carousel}

Saiba como estender o componente Carrossel de produtos do AEM CIF atualizando o Modelo do Sling e personalizando a marcação.

## Introdução {#intro}

O componente Carrossel de produtos é estendido por todo este tutorial. Como primeira etapa, adicione uma instância do Carrossel do produto à página inicial para entender a funcionalidade da linha de base:

1. Navegue até a Página Inicial do site, por exemplo [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)
1. Insira um novo componente Carrossel do produto no container do layout principal da página.

   ![Componente do carrossel do produto](/help/commerce-cloud/cif-storefront/assets/product-carousel-component.png)

1. Expanda o painel lateral (se ainda não estiver sendo exibido) e na lista suspensa do localizador de ativos selecione **Produtos**.

   ![Produtos do carrossel](/help/commerce-cloud/cif-storefront/assets/carousel-products.png)

1. Isso deve exibir uma lista de produtos disponíveis em uma instância conectada do Adobe Commerce.

   ![Instância Conectada](/help/commerce-cloud/cif-storefront/assets/connected-instance.png)

1. Os produtos serão exibidos abaixo com as propriedades padrão:

   ![Produto exibido com as propriedades](/help/commerce-cloud/cif-storefront/assets/discount.png)

## Atualizar o modelo do Sling {#update-sling-model}

É possível estender a lógica de negócios do Carrossel de produtos implementando um Modelo do Sling:

1. No IDE, navegue no módulo principal até `core/src/main/java/com/venia/core/models/commerce` e crie uma interface CustomCarousel que estenda a interface ProductCarousel do CIF:

   ```text
   package com.venia.core.models.commerce;
   import com.adobe.cq.commerce.core.components.models.productcarousel.ProductCarousel;
   public interface CustomCarousel extends ProductCarousel {
   }
   ```

1. Em seguida, crie uma classe de implementação `CustomCarouselImpl.java` em `core/src/main/java/com/venia/core/models/commerce/CustomCarouselImpl.java`.

   O padrão de delegação para Modelos do Sling permite que `CustomCarouselImpl` faça referência ao modelo `ProductCarousel` por meio da propriedade `sling:resourceSuperType`:

   ```text
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductCarousel productCarousel;
   ```

1. A anotação `@PostConstruct` garante que esse método seja chamado quando o Modelo Sling for inicializado. A consulta do GraphQL do produto já foi estendida usando o método extendProductQueryWith para recuperar atributos. Atualize a consulta do GraphQL para incluir o atributo na consulta parcial:

   ```javascript
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

   No código acima, o `addCustomSimpleField` é usado para recuperar o atributo `accessory_gemstone_addon`.

## Personalização da marcação {#customize-markup}

Para personalizar ainda mais a marcação:

1. Crie uma cópia de `productcard.html` de `/apps/core/cif/components/commerce/productcarousel/v1/productcarousel` (o caminho crxde do componente principal) para o módulo ui.apps `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productcarousel/productcard.html`.

1. Edite `productcard.html` para chamar o atributo personalizado, que é mencionado na classe de implementação:

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

1. Salve as alterações e implante as atualizações no AEM usando o comando Maven, em um terminal de linha de comando. Você poderá ver o valor do atributo personalizado `accessory_gemstone_addon` para os produtos selecionados na página.
