---
title: Uso do seletor de produto e categoria da CIF
description: Saiba como usar o seletor de produto e categoria da CIF em seus componentes de comércio com o cliente para auxiliar autores e profissionais de marketing a trabalhar com dados de produtos e catálogos de comércio de maneira eficiente.
sub-product: Commerce
topics: Development
version: cloud-service
activity: develop
audience: developer
feature: Commerce Integration Framework
translation-type: tm+mt
source-git-commit: 0f2747190523613d2fa1f4710dee1c28d4a5148f
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---


# Seletores de criação de conteúdo e comércio AEM {#cif-pickers}

A criação de conteúdo e comércio AEM oferece um conjunto de ferramentas de criação para ajudar AEM autores e profissionais de marketing a trabalharem com dados e catálogos de produtos comerciais. O Seletor de produto e o Seletor de categoria fazem parte do complemento CIF e são usados pelos Componentes principais da CIF. Os projetos podem usar esses seletores em qualquer caixa de diálogo de componente para selecionar produtos ou categorias.

## Seletor de produtos {#product-picker}

Para usar o seletor de produtos em um componente de projeto, um desenvolvedor deve adicionar `commerce/gui/components/common/cifproductfield` a uma caixa de diálogo de componente. Por exemplo, use o seguinte para o cq:dialog:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

O campo de produto permite navegar até o produto que um usuário deseja selecionar por meio das diferentes visualizações. Por padrão, o campo do produto retorna a ID do produto, mas pode ser configurado usando o atributo `selectionId`.

O campo seletor de produto oferece suporte às seguintes propriedades opcionais:

- selectionId (id, uid, sku, lesma, Combinar, CombinarSku) - permite escolher o atributo do produto a ser retornado pelo seletor (padrão = id). Usar o sku retorna o sku do produto selecionado, enquanto usa o CombinationSku e retorna uma string como base#variant com os SKUs do produto base e a variante selecionada, ou um único sku se um produto base for selecionado.
- filter (folderOrProduct, folderOrVariant) - filtra o conteúdo a ser renderizado pelo seletor ao navegar na árvore do produto. folderOrProduct - renderiza pastas e produtos. folderOrProductOrVariant - renderiza pastas, produtos e variantes de produtos. Se um produto ou uma variante de produto for renderizada, ela também poderá ser selecionada no seletor. (padrão = folderOrProduct)
- vários (true, false) - habilita a seleção de um ou vários produtos (padrão = false)
- emptyText - para configurar o valor de texto vazio do campo do seletor

Além disso, também há suporte para propriedades de campo de diagnóstico padrão como `name`, `fieldLabel` ou `fieldDescription`.

O componente `cifproductfield` requer a clientlib cif.shell.picker. Para adicionar uma clientlib a uma caixa de diálogo, você pode usar a propriedade extraClientlibs.

Um exemplo completo de trabalho do `cifproductfield` pode ser encontrado no projeto [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml). Consulte também [Personalizando caixas de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) da documentação dos Componentes principais AEM.

## Seletor de categoria {#category-picker}

O seletor de categoria pode ser usado em uma caixa de diálogo de componente, bem como de maneira semelhante ao seletor de produto.

O seguinte trecho pode ser usado em uma configuração cq:dialog:

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

O campo do seletor de categoria oferece suporte às seguintes propriedades opcionais:

- selectionId(id, uid, lesma, idAndUrlPath, uidAndUrlPath) - permite escolher o atributo de categoria a ser retornado pelo seletor (padrão = id). idAndUrlPath &amp; uidAndUrlPath são opções especiais que armazenam id/uid de categoria e url_path separadas por um | caractere como, por exemplo, 1|masculino/tops.
- várias (true, false) - habilita a seleção de uma ou várias categorias (padrão = false)

Além disso, também há suporte para propriedades de campo de diagnóstico padrão como `name`, `fieldLabel` ou `fieldDescription`.

Igual ao componente `cifproductfield`, o componente `cifcategoryfield` também requer a clientlib cif.shell.picker. Para adicionar uma clientlib a uma caixa de diálogo, você pode usar a propriedade `extraClientlibs` . Consulte [Personalizando caixas de diálogo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) da documentação dos Componentes principais AEM.

Um exemplo completo de trabalho do `cifcategoryfield` pode ser encontrado no projeto [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml).
