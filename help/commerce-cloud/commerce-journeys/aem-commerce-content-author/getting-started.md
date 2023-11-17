---
title: Introdução à criação da CIF
description: Introdução à criação da CIF.
exl-id: 0bef4d8c-0ad3-4ec8-ab08-8c83203b3b68
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 3%

---

# AEM Introdução à criação do CIF {#getting-started}

Saiba mais sobre a criação do CIF no Adobe Experience Manager (AEM).

## A história até agora {#story-so-far}

No documento anterior desta jornada de Conteúdo e Comércio do AEM, [Saiba mais sobre o conteúdo e o comércio do AEM](/help/commerce-cloud/introduction.md)No entanto, você aprendeu a teoria básica e os conceitos de CMS headless e AEM Content and Commerce.

Este artigo se baseia nesses fundamentos.

## Objetivo {#objective}

Este documento ajuda você a entender como usar o CIF para criação específica de conteúdo e comércio. Depois de ler, você deverá:

* Entenda os conceitos de criação de CIF usando o Editor universal
* Como acessar dados do catálogo de produtos no AEM usando seletores de produto e categoria
* Como acessar dados de conteúdo e comércio usando o cockpit do produto e o AEM Omnisearch

## Criação de CIF no editor universal {#cif-authoring}

O CIF estende o Editor universal com recursos para acessar os dados do produto em tempo real sem sair do contexto:

Abra o painel lateral e selecione &quot;Produtos&quot; na lista suspensa.
![Selecionar tipo de produto](assets/asset-finder-overview.png)

Você pode navegar pelo catálogo de produtos ou usar o campo de pesquisa de texto completo para localizar produtos.
![tipo de produto](assets/asset-finder-search.png)

Os produtos podem ser soltos em componentes que oferecem suporte a quedas de produtos (por exemplo, teaser de produto, carrossel de produto) diretamente na página que cria automaticamente um componente de teaser de produto.

## Seletores de categoria e produto {#pickers}

Se os dados de produto e categoria forem necessários em componentes de comércio ou diálogos de back-office do AEM, os autores do AEM poderão usar seletores que são elementos da interface do usuário para pesquisar e selecionar confortavelmente os dados do catálogo de produtos.

### Seletor de produtos

Clicar no ícone de pasta abre a interface modal do seletor (por exemplo, teaser de produto)
![seletor de produto](assets/product-picker-open.png)

Os produtos podem ser encontrados navegando pela estrutura do catálogo à esquerda ou pesquisando. A pesquisa de texto completo respeita a categoria selecionada e limita os resultados da pesquisa a essa categoria.
![pasta do seletor de produtos](assets/product-picker-folders.png)

Os produtos com variações são marcados com um ícone de pasta que pode ser clicado para mostrar todas as variações.
![variantes do seletor de produtos](assets/product-picker-variants.png)
![grades do seletor de produtos abertas](assets/product-picker-variants-open.png)

### Seletor de Categoria

Funciona como um seletor de produtos. Clicar no ícone de pasta abre a interface modal do seletor (por exemplo, carrossel de categorias)
![seletor de categoria](assets/category-picker-open.png)

Navegue pela estrutura do catálogo à esquerda e selecione a categoria.
![seletor de categoria](assets/category-picker-folders.png)

## Cockpit do produto {#cockpit}

O cockpit do produto é um local central para acessar rapidamente o catálogo de produtos com todo o conteúdo enriquecido. Você aprenderá em um dos próximos módulos a enriquecer dados do produto com conteúdo. Por enquanto, vamos nos concentrar no acesso aos dados do produto.

No menu principal, clique em commerce para ver uma lista de todos os catálogos de produtos anexados.
![item de menu comércio](assets/commerce-menu-item.png)

Isso mostra uma lista de todos os catálogos de produtos conectados.
![catálogos integrados do cockpit](assets/cockpit-Integrated-catalogs.png)

O catálogo de produtos mostra, por padrão, todas as categorias de primeiro nível com todos os produtos. Clicar em uma categoria abre essa categoria com todos os produtos e subcategorias relacionados, incluindo seus produtos.
![catálogo de produtos cockpit](assets/cockpit-product-catalog.png)

Você pode abrir as propriedades do produto clicando no ícone de propriedade. O ícone é exibido ao passar o mouse sobre um bloco de produto.
![propriedades do produto cockpit](assets/cockpit-properties.png)

Todas as propriedades do produto são somente leitura porque os dados são carregados em tempo real do back-end conectado. A alteração das propriedades do produto deve ser feita no sistema de back-end, que é o sistema de registro. A guia **Variantes** só aparecem se o produto tiver variações. Clicar na guia exibe todas as variações com seus atributos.
![variantes de produto do cockpit](assets/cockpit-properties-variants.png)

As guias restantes mostram todo o conteúdo de AEM associado ao produto. Essas guias são discutidas em um dos módulos a seguir.

## AEM Omnisearch {#omnisearch}

Usar o Omnisearch é uma maneira fácil de encontrar conteúdo AEM usando a pesquisa de texto completo. O CIF amplia o Omnisearch com a pesquisa em texto completo de catálogos de produtos com seu conteúdo AEM associado.
![item de menu comércio](assets/omnisearch.png)

O Omnisearch executa uma pesquisa de texto completo no back-end de comércio para encontrar todos os produtos relacionados. O resultado está listado em **Ver todos os produtos**. O Omnisearch também pesquisa no AEM o conteúdo associado ao produto pesquisado. Os resultados estão listados nas respectivas categorias de AEM. Neste exemplo, um fragmento de conteúdo está relacionado ao produto.

## O que vem a seguir {#what-is-next}

Agora que concluiu esta parte da jornada, você deve:

* Entenda os conceitos de criação de CIF usando o Editor universal
* Como acessar o catálogo de produtos no AEM usando seletores de produto e categoria
* Como acessar dados de conteúdo e comércio usando o cockpit do produto e o AEM Omnisearch

Desenvolva esse conhecimento e continue sua jornada revisando o documento a seguir [Gerenciar páginas e modelos do catálogo de produtos](catalog-templates.md), onde você aprende a criar e personalizar sua primeira experiência de catálogo de produtos.

## Recursos adicionais {#additional-resources}

Embora seja recomendável seguir para a próxima parte da jornada-[Gerenciar páginas e modelos do catálogo de produtos](catalog-templates.md)-a seguir estão alguns recursos opcionais que aprofundam alguns conceitos mencionados aqui. No entanto, esses recursos opcionais não são necessários para continuar na jornada.

* [Configurando lojas e catálogos](/help/commerce-cloud/getting-started.md#catalog)
