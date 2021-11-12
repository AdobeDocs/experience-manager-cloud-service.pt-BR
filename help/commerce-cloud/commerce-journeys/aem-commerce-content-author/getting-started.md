---
title: Introdução à criação da CIF
description: Introdução à criação da CIF
source-git-commit: a98d525512dcba790d002d6a4042558962c36c97
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 0%

---

# Introdução à criação AEM CIF {#getting-started}

Saiba mais sobre AEM criação na CIF.

## A História Até Agora {#story-so-far}

No documento anterior desta jornada de Conteúdo e Comércio de AEM, [Saiba mais sobre conteúdo e comércio AEM](/help/commerce-cloud/introduction.md), você aprendeu a teoria básica do que é um CMS sem periféricos e agora deve entender os conceitos básicos de Conteúdo e Comércio AEM.

Este artigo tem por base esses fundamentos.

## Objetivo {#objective}

Este documento ajuda você a entender como usar a CIF para criação específica de conteúdo e comércio. Depois de ler, você deve:

* Entenda os conceitos da criação da CIF usando o Editor universal
* Como acessar os dados do catálogo de produtos no AEM usando seletores de produto e categoria
* Como acessar dados de conteúdo e comércio usando o cockpit de produtos e AEM Omnisearch

## Criação da CIF no editor universal {#cif-authoring}

A CIF amplia o Editor universal com recursos para acessar os dados do produto em tempo real sem deixar o contexto:

Abra o painel lateral e selecione &quot;Produtos&quot; na lista suspensa.
![Selecionar tipo de produto](assets/asset-finder-overview.png)

Você pode navegar pelo catálogo de produtos ou usar o campo de pesquisa de texto completo para localizar produtos.
![tipo de produto](assets/asset-finder-search.png)

Os produtos podem ser soltos em componentes que suportam quedas de produtos (por exemplo, teaser de produto, carrossel de produtos) diretamente na página que cria automaticamente um componente de teaser de produto.

## Seletores de produto e categoria {#pickers}

Se os dados de produto e categoria forem necessários em componentes de comércio ou caixas de diálogo AEM back-office, AEM autores podem usar seletores que são elementos da interface do usuário para pesquisar e selecionar confortavelmente os dados do catálogo de produtos.

### Seletor de produtos

Clicar no ícone de pasta abrirá a interface do usuário modal do seletor (por exemplo, teaser de produto)
![seletor de produto](assets/product-picker-open.png)

Os produtos podem ser encontrados navegando pela estrutura do catálogo à esquerda ou pesquisando. A pesquisa de texto completo respeitará a categoria selecionada e limitará os resultados da pesquisa a essa categoria.
![pasta selecionador de produtos](assets/product-picker-folders.png)

Os produtos com variações são marcados com um ícone de pasta que pode ser clicado para mostrar todas as variações.
![variantes do seletor de produto](assets/product-picker-variants.png)
![variantes do seletor de produto abertas](assets/product-picker-variants-open.png)

### Seletor de categoria

Funciona como um seletor de produtos. Clicar no ícone de pasta abrirá a interface do usuário modal do seletor (por exemplo, carrossel de categoria)
![seletor de categoria](assets/category-picker-open.png)

Navegue pela estrutura do catálogo à esquerda e selecione a categoria .
![seletor de categoria](assets/category-picker-folders.png)

## Cockpit do produto {#cockpit}

O cockpit de produtos é um local central para aceder rapidamente ao catálogo de produtos com todo o seu conteúdo enriquecido. Você aprenderá em um dos próximos módulos como enriquecer os dados do produto com conteúdo. Por enquanto, vamos nos concentrar em acessar os dados do produto.

No menu principal, clique em commerce para ver uma lista de todos os catálogos de produtos anexados.
![item de menu de comércio](assets/commerce-menu-item.png)

Mostra uma lista de todos os catálogos de produtos conectados.
![catálogos integrados do cockpit](assets/cockpit-Integrated-catalogs.png)

O catálogo de produtos mostra, por padrão, todas as categorias de primeiro nível com todos os produtos. Clicar em uma categoria abrirá essa categoria com todos os produtos e subcategorias relacionados, incluindo seus produtos.
![catálogo de produtos da cabine](assets/cockpit-product-catalog.png)

É possível abrir as propriedades do produto clicando no ícone de propriedade. O ícone é exibido ao passar o mouse sobre um bloco de produto.
![propriedades do produto cockpit](assets/cockpit-properties.png)

Todas as propriedades do produto são somente leitura porque os dados são carregados em tempo real do back-end conectado. A alteração das propriedades do produto deve ser feita no sistema de back-end que é o sistema de registro. A guia **Variantes** só aparecerá se o produto tiver variações. Clicar na guia exibirá todas as variações com seus atributos.
![variantes de produto de cockpit](assets/cockpit-properties-variants.png)

As guias restantes mostram todo AEM conteúdo associado ao produto. Discutiremos essas guias em um dos próximos módulos.

## AEM Omnisearch {#omnisearch}

Usar o Omnisearch é uma maneira fácil de encontrar conteúdo AEM usando pesquisa de texto completo. A CIF amplia o Omnisearch com a pesquisa de texto completo de catálogos de produtos com seu conteúdo AEM associado.
![item de menu de comércio](assets/omnisearch.png)

O Omnisearch executará uma pesquisa de texto completo no backend de comércio para localizar todos os produtos relacionados. O resultado está listado em **Ver todos os produtos**. O Omnisearch também pesquisará AEM conteúdo associado ao produto pesquisado. Os resultados serão listados nas respectivas categorias de AEM. Neste exemplo, um Fragmento de conteúdo está relacionado ao produto.

## O que vem a seguir {#what-is-next}

Agora que você concluiu esta parte da jornada, deve:

* Entenda os conceitos da criação da CIF usando o Editor universal
* Como acessar o catálogo de produtos no AEM usando seletores de produto e categoria
* Como acessar dados de conteúdo e comércio usando o cockpit de produtos e AEM Omnisearch

Aproveite esse conhecimento e continue sua jornada revisando o documento em seguida [Gerenciar páginas e modelos do catálogo de produtos](catalog-templates.md), onde você aprenderá a criar e personalizar sua primeira experiência de catálogo de produtos.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada revisando o documento [Gerenciar páginas e modelos do catálogo de produtos](catalog-templates.md), a seguir estão alguns recursos adicionais e opcionais que aprofundam alguns conceitos mencionados neste documento, mas não é necessário que eles continuem na jornada.

* [Configuração de lojas e catálogos](/help/commerce-cloud/getting-started.md#catalog)
