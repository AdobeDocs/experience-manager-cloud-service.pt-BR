---
title: Gerenciar páginas e modelos do catálogo de produtos
description: Saiba como gerenciar páginas e modelos do catálogo de produtos
exl-id: 0d795d85-c865-40d5-941e-e02ee96fdd11
feature: Commerce Integration Framework
role: Admin
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---


# Gerenciar páginas e modelos do catálogo de produtos {#product-catalog}

Saiba como gerenciar páginas e modelos do catálogo de produtos.

## A história até agora {#story-so-far}

No documento anterior da jornada de criação do AEM Content and Commerce, [Introdução às noções básicas de criação do AEM CIF,](/help/commerce-cloud/cif-storefront/commerce-journeys/aem-commerce-content-author/getting-started.md) você aprendeu as noções básicas de criação do CIF.

Este artigo se baseia nesses fundamentos.

## Objetivo {#objective}

Este documento ajuda você a entender como gerenciar páginas e modelos do catálogo de produtos. Depois de ler esse documento, você deverá:

* entender os conceitos dos modelos de catálogo
* como os modelos genéricos funcionam
* criou um modelo individual

## O conceito básico {#basic-concept}

A loja Venia vem com uma experiência típica de catálogo de produtos com navegação, aterrissagem, categoria (PLP) e páginas de detalhes do produto (PDP).

Páginas de catálogo são criadas dinamicamente usando um modelo de catálogo do AEM CIF e dados de produto em tempo real que são buscados no endpoint de comércio, quando necessário. Cada catálogo tem um modelo genérico para páginas de produto e categoria.

![estrutura do catálogo](assets/catalog-structure.png)

O componente de navegação mostra as páginas de conteúdo e catálogo. É possível mostrar a landing page do catálogo ou as categorias de primeiro nível na navegação. Passar o mouse sobre uma categoria mostrará categorias de segundo nível como uma segunda linha.

![navegação no catálogo](assets/catalog-navigation.png)

Clicar em uma categoria abre a página de categoria (ou a página de lista de produtos).

![PLP](assets/catalog-plp.png)

Clicar em um produto abre a página de detalhes do produto.

![PLP](assets/catalog-pdp.png)

## Os modelos {#templates}

### Modelos genéricos {#generic}

O modelo de catálogo Venia genérico usa o componente principal da lista de produtos. Esse componente exibe a imagem da categoria, se disponível, e os produtos da categoria.

![modelo de categoria](assets/category-template.png)

O modelo de produto genérico Venia usa o Componente principal de Detalhes do produto. Este componente exibe informações do produto para vários tipos de produtos e ações complementares ao carrinho.

![modelo de produto](assets/product-template.png)

### Editar Modelos {#edit-templates}

Os modelos podem ser editados abrindo diretamente a página de modelo ou alternando para o modo de edição ao navegar em uma página de catálogo de produtos. Lembre-se de que alterar a página alterará o modelo e não apenas a página específica do produto/categoria.

### Modelos de Categoria ou Produto Específicos {#specific}

O CIF suporta vários modelos com apenas alguns cliques. Para criar outro modelo, selecione o modelo genérico na respectiva categoria e crie uma página usando a ação **Criar**.

![criar página de modelo](assets/create-template-page.png)

Selecione o respectivo modelo de produto ou categoria.

![criar seleção de modelo](assets/create-template-select.png)

Insira o título e crie a página.

![criar entrada de modelo](assets/create-template-enter.png)

Observe que agora você tem um template específico sob o genérico.

![criar hierarquia de modelo](assets/create-template-hierachry.png)

Abra o template. Ele se parece exatamente com o modelo de categoria genérico.

![criar novo modelo](assets/create-template-new.png)

Adicione qualquer imagem na parte superior da página.

![criar atualização de modelo](assets/create-template-update.png)

O modelo pode ser visualizado com qualquer categoria/produto. Abra **Informações da Página** e selecione **Exibir com categoria/produto**. Selecione o produto/categoria no seletor para obter uma visualização com este produto/categoria. Selecione a categoria **Comprar a aparência** para obter uma visualização do modelo atualizado.

![criar modelo &#x200B;](assets/create-template-picker.png)

Agora é necessário atribuir esse template à categoria específica. Abra as propriedades no menu **Informações da página** e alterne para a guia Comércio. Clique no ícone de pasta para selecionar a categoria **Comprar a aparência** no seletor de categorias. É possível atribuir várias categorias a um modelo e também incluir subcategorias ativando a caixa de seleção.

![criar associação de modelo](assets/create-template-associate.png)

Volte para a página inicial principal e clique na categoria **Shop The Look** para ver o modelo específico. Todas as outras categorias ainda usam o template genérico.

![criar resultado do modelo](assets/create-template-result.png)

O mesmo fluxo de trabalho pode ser aplicado para criar modelos de produtos individuais.

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada, você deve:

* entender os conceitos dos modelos de catálogo
* como os modelos genéricos funcionam
* criou um modelo individual

Desenvolva esse conhecimento e prossiga com sua jornada revisando a seguir o documento [Gerenciar experiências de catálogo de produtos por etapas](/help/commerce-cloud/cif-storefront/commerce-journeys/aem-commerce-content-author/staged-catalog.md), no qual você aprenderá a trabalhar com dados de produtos por etapas e inicializações do AEM.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada revisando o documento [Gerenciar experiência de catálogo de produtos por etapa](/help/commerce-cloud/cif-storefront/commerce-journeys/aem-commerce-content-author/staged-catalog.md), os recursos opcionais a seguir fornecerão uma melhor explicação dos conceitos mencionados neste documento. Porém, eles não são obrigatórios para continuar na jornada headless:

* [Criação de várias categorias e páginas de produto](/help/commerce-cloud/cif-storefront/authoring/multi-template-usage.md)
* [Guia de migração para o Experience Manager Cloud Service](/help/commerce-cloud/cif-storefront/migration.md) - Como migrar de uma versão antiga para o complemento AEM Commerce integration framework (CIF)
