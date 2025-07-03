---
title: Metadados JSON-LD
description: Saiba como ativar e verificar o recurso JSON+LD no AEM CIF.
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 547d3721-e094-4a42-8a7c-27e4ef97ea9c
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 2%

---

# Metadados JSON-LD {#json-ld}

Este guia explica como ativar e verificar o recurso JSON+LD no AEM CIF.

>[!NOTE]
>
> Este recurso é experimental.

## Ativar JSON+LD na configuração do CIF {#enabling}

Por padrão, a caixa de seleção **Habilitar JSON+LD** não está visível na configuração do CIF. Para ativar esse recurso, o projeto deve incluir a configuração OSGi necessária, que permite que a caixa de seleção seja exibida. Essa configuração permite que os usuários alternem o suporte a scripts JSON+LD nas páginas de produtos.
Para disponibilizar a caixa de seleção **Habilitar JSON+LD** na configuração do CIF, adicione a seguinte configuração OSGi ao seu projeto: `
com.adobe.cq.cif.components.models.JsonLdFeatureEnable`.
Para obter mais detalhes sobre como adicionar essa configuração, consulte [Adiciona configuração para Json-Ld](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.cif.components.models.JsonLdFeatureEnable.cfg.json) no repositório público aem-CIF-guides-venia.

Depois que essa configuração for adicionada e implantada, a caixa de seleção ficará visível nas definições de configuração do CIF e aqui estão as etapas para habilitar o **JSON+LD**:

1. Navegue até Configuração do CIF no AEM.
1. Cancelar herança.
1. Marque a caixa de seleção **Habilitar JSON+LD**.
1. Salve a configuração.

## Verificar JSON+LD em uma Página de detalhes do produto (PDP) {#verify}

Para ilustrar as etapas para verificar JSON+LD, o projeto Venia é usado como exemplo, em que a configuração JSON+LD necessária já foi adicionada para habilitar o recurso. Estas são as etapas a serem seguidas:

1. Navegue até a instância local do AEM e abra a Página de detalhes do produto (PDP): http://localhost:4502/editor.html/content/venia/us/en/products/product-page.html
1. Crie um produto na Página de detalhes do produto (PDP).
1. Alternar para o modo **Exibir como Publicação**.
1. Abra a **Exibir Página Source** em seu navegador.
1. Procure por JSON+LD na origem da página.

Se configurado corretamente, você encontrará o script JSON+LD associado ao produto inserido na página.

## Exemplo de estrutura JSON+LD para um produto {#sample}

Abaixo está um exemplo da estrutura **JSON+LD** para a saia de Agatha, criada na página PDP do projeto Venia:

```
<script type="application/ld+json">
{
  "@context": "http://schema.org",
  "@type": "Product",
  "sku": "VSK05",
  "name": "Agatha Skirt",
  "image": "https://mcstaging.catalogservice4commerce.fun/media/catalog/product/cache/926ea6fc2ad48a7202ff4587b6c2768e/v/s/vsk05-pe_main_2.jpg",
  "description": "The Agatha Skirt has a large circumference that lends itself to all sorts of drama...",
  "@id": "product-ef4fa1dc72",
  "offers": [
    {
      "@type": "Offer",
      "sku": "VSK05-KH-S",
      "url": "/content/venia/us/en/products/product-page.html/agatha-skirt.html",
      "priceCurrency": "USD",
      "price": 78.0
    },
    {
      "@type": "Offer",
      "sku": "VSK05-RN-XS",
      "availability": "InStock",
      "priceSpecification": {
        "@type": "UnitPriceSpecification",
        "priceType": "https://schema.org/ListPrice",
        "price": 18.0,
        "priceCurrency": "USD"
      },
      "price": 46.0
    }
  ]
}
</script>
```

## Mapeamento de atributos JSON+LD para o GraphQL {#mapping}

Os atributos JSON+LD podem ser mapeados para consultas do GraphQL no AEM CIF, garantindo que os dados estruturados reflitam dinamicamente as informações do produto recuperadas pelo GraphQL.

### Exemplo de mapeamento de produto {#example}

| Atributo JSON+LD | Atributo do Magento GraphQL | Obrigatório (S/N) |
|---------------------------------|-------------------|---|
| sku | sku | N |
| offers.url | Lógica personalizada | N |
| offers.SpecialPricedate | special_to_date | N |
| offers.sku | sku | N |
| offers.priceSpecification.priceCurrency | moeda | Y |
| offers.priceSpecification.price | preço_regular | N |
| offers.priceCurrency | moeda | Y |
| offers.price | special_price | Y |
| offers.image | media_gallery.url | N |
| offers.availability | stock_status | N |
| name | name | Y |
| imagem | media_gallery.url | Y |
| descrição | descrição | N |
| aggregateRating.reviewCount | review_count | N |
| aggregateRating.ratingValue | rating_summary | N |
| @id | id | N |

Esse mapeamento garante que o script JSON+LD seja preenchido dinamicamente com base nos dados do produto recuperados por consultas do GraphQL.

Para testar sua estrutura JSON+LD, você pode usar o [Teste de Resultados Avançados - Console de Pesquisa do Google](https://search.google.com/test/rich-results/result?id=wtU3LVIEM8H7Aaf5qqK9qw). Essa ferramenta fornece feedback detalhado, incluindo se os atributos necessários estão presentes ou ausentes, e ajuda a garantir que seus dados estruturados sejam implementados corretamente.
