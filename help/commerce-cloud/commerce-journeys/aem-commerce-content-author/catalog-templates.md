---
title: Gerenciar páginas e modelos do catálogo de produtos
description: Saiba como gerenciar páginas e modelos de catálogo de produtos
source-git-commit: b84896e70df0c22aea1581d8d0d0561e8bc4b24d
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---

# Gerenciar páginas e modelos do catálogo de produtos {#product-catalog}

Saiba como gerenciar páginas e modelos de catálogo de produtos.

## A História Até Agora {#story-so-far}

No documento anterior da jornada de criação Conteúdo e Comércio da AEM, [Introdução às AEM noções básicas de criação da CIF](getting-started.md), você aprendeu sobre a criação da CIF.

Este artigo tem por base esses fundamentos.

## Objetivo {#objective}

Este documento ajuda você a entender como gerenciar páginas e modelos de catálogo de produtos. Depois de ler, você deve:

* entender os conceitos dos templates de catálogo
* como funcionam os modelos genéricos
* criaram um modelo individual

## O conceito básico {#basic-concept}

A loja Venia vem com uma experiência típica de catálogo de produtos com navegação e landing page, categoria (PLP) e páginas detalhadas do produto (PDP).

As páginas de catálogo são criadas dinamicamente usando um modelo de catálogo da CIF AEM e dados de produto em tempo real que são buscados no endpoint de comércio quando necessário. Cada catálogo tem um modelo genérico para páginas de produto e categoria.
![estrutura de catálogo](assets/catalog-structure.png)

O componente de navegação mostra páginas de conteúdo e catálogo. É possível mostrar a landing page do catálogo ou as categorias de primeiro nível na navegação. Passar o mouse sobre uma categoria mostrará categorias de segundo nível como uma segunda linha.
![navegação no catálogo](assets/catalog-navigation.png)

Clicar em uma categoria abrirá a página da categoria (ou a página da lista de produtos).

![PLP](assets/catalog-plp.png)

Clicar em um produto abrirá a página de detalhes do produto.

![PLP](assets/catalog-pdp.png)

## Os modelos {#templates}

### Modelos genéricos {#generic}

O modelo de catálogo Venia genérico usa o Componente principal da lista de produtos. Esse componente exibe a imagem da categoria, se disponível, e os produtos da categoria.
![modelo de categoria](assets/category-template.png)

O modelo de produto Venia genérico usa o Componente principal de detalhes do produto. Esse componente exibe informações do produto para vários tipos de produtos e ações de adicionar ao carrinho.
![modelo de produto](assets/product-template.png)

### Editar modelos {#edit-templates}

Os modelos podem ser editados abrindo diretamente a página de modelo ou alternando para o modo de edição ao navegar em uma página de catálogo de produtos. Lembre-se de que alterar a página alterará o modelo e não apenas a página específica do produto/categoria.

### Modelos específicos de categoria ou produto {#specific}

A CIF é compatível com vários modelos com apenas alguns cliques. Para criar outro template, selecione o template genérico da respectiva categoria e crie uma nova página usando o **Criar** ação.

![criar página de modelo](assets/create-template-page.png)

Selecione o respectivo produto ou modelo de categoria.

![criar modelo selecionar](assets/create-template-select.png)

Insira o título e crie a página.

![criar modelo insira](assets/create-template-enter.png)

Observe que você agora tem um template específico no genérico .

![criar hierarquia de modelo](assets/create-template-hierachry.png)

Abra o modelo . É exatamente como o template de categoria genérico.

![criar modelo novo](assets/create-template-new.png)

Adicione qualquer imagem na parte superior da página.

![criar atualização de modelo](assets/create-template-update.png)

O template pode ser visualizado com qualquer categoria/produto. Abrir **Informações da página** e depois selecione **Exibir com categoria/produto**. Selecione o produto/categoria no seletor para obter uma visualização com este produto/categoria. Selecionar **Compre a aparência** categoria para obter uma visualização do modelo atualizado.

![criar modelo ](assets/create-template-picker.png)

Agora, precisamos atribuir esse template à categoria específica. Abra as propriedades na **Informações da página** e alterne para a guia commerce . Clique no ícone de pasta para selecionar a variável **Compre a aparência** categoria do seletor de categorias. É possível atribuir várias categorias a um modelo e também incluir subcategorias ao ativar a caixa de seleção.

![criar modelo associado](assets/create-template-associate.png)

Volte para a página inicial principal e clique em **Compre a aparência** categoria para ver o modelo específico. Todas as outras categorias ainda usam o template genérico .

![criar resultado do modelo](assets/create-template-result.png)

O mesmo fluxo de trabalho pode ser aplicado para criar modelos de produto individuais.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada, deve:

* entender os conceitos dos templates de catálogo
* como funcionam os modelos genéricos
* criaram um modelo individual

Aproveite esse conhecimento e continue sua jornada revisando o documento em seguida [Gerenciar experiências de catálogo de produtos preparados](staged-catalog.md), onde você aprenderá a trabalhar com dados de produtos preparados e AEM inicializações.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada revisando o documento [Gerenciar experiências de catálogo de produtos preparados](staged-catalog.md), a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada sem periféricos:

* [Criação de várias categorias e páginas de produto](/help/commerce-cloud/authoring/multi-template-usage.md)
* [Guia de migração para o Experience Manager Cloud Service](/help/commerce-cloud/migration.md) - Como migrar de uma versão antiga para o complemento CIF (Commerce Integration Framework) da AEM
