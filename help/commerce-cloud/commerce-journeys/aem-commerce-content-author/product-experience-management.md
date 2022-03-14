---
title: Criação de experiências de produto
description: Saiba como criar experiências de produto.
exl-id: 4ae70e40-fdf1-4a37-b4dd-0c4882d77908
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 1%

---

# Criação de experiências de produto {#building-experiences}

Saiba como gerenciar experiências de produtos.

## A História Até Agora {#story-so-far}

No documento anterior da jornada Conteúdo e Comércio da AEM, [Gerenciar experiências de catálogo de produtos preparados](staged-catalog.md), você aprendeu a gerenciar experiências de catálogos de produtos preparados.

## Objetivo {#objective}

Este documento ajuda você a entender como criar o conteúdo e as experiências do produto.

## Gerenciamento de experiência do produto {#management}

O Gerenciamento de experiência do produto é a disciplina para decorar dados do produto (que é de propriedade de um PIM ou solução comercial) com conteúdo de marketing no AEM. Esses dados de produto enriquecidos com conteúdo podem ser usados em vários canais para criar uma experiência de compra imersiva.

No AEM, você pode criar vários tipos de conteúdo e vinculá-los ao catálogo de produtos. O conteúdo associado pode ser facilmente descoberto e usado, o que leva a uma alta produtividade.

### Ativos {#assets}

Em um alto nível, há dois tipos de ativos relacionados a produtos: produto e marketing. Os ativos do produto geralmente são gerenciados por comerciantes e têm como foco mostrar o produto (principalmente na frente de um fundo neutro). Os ativos são gerenciados na solução comercial ou na AEM Assets (com uma integração do Assets com a solução comercial/pim).

Os ativos de marketing estão relacionados à promoção e ao uso do produto, que geralmente é de propriedade do marketing. Os exemplos mostram vários produtos (&quot;compre a aparência&quot;), em um contexto específico (&quot;coleção de quedas ao ar livre&quot;) ou pdfs de instruções. A CIF fornece uma maneira fácil de vincular qualquer ativo AEM ao objeto do catálogo de produtos.

Abra as propriedades do ativo e alterne para a **Comércio** guia . Essa guia permite gerenciar a associação com produtos. A tabela abaixo do seletor fornece informações adicionais para os objetos vinculados (visível apenas com uma seleção). Clique no ícone de detalhes para obter uma visão completa do cockpit de produtos. Para associar um novo objeto, clique no ícone do seletor de produtos (ícone de pasta), selecione um objeto e feche o seletor.

![ativos pem](assets/pem-assets.png)

### Fragmentos de experiência {#experience-fragments}

Fragmentos de experiência são uma excelente maneira de criar conteúdo de produto reutilizável ou individual em escala. A associação funciona de forma semelhante a um ativo. Abra as propriedades e alterne para a guia **Comércio** guia . Essa guia permite gerenciar a associação com produtos e categorias. As tabelas abaixo dos seletores fornecem informações adicionais para os objetos vinculados (visíveis apenas com uma seleção). Clique no ícone de detalhes para obter uma visão completa do cockpit de produtos. Para associar um novo objeto, clique no ícone do seletor de produtos (ícone de pasta), selecione um objeto e feche o seletor.

![pem xf](assets/pem-xf.png)

### Fragmentos de conteúdo {#content-fragments}

Fragmentos de conteúdo são o melhor tipo de conteúdo para qualquer conteúdo estruturado. Isso pode ser usado para aumentar os dados externos do produto com dados de marketing adicionais ou para criar conteúdo sem periféricos. A associação de um Fragmento de conteúdo a um objeto de catálogo de produtos ocorre por meio dos tipos de referência de produto ou categoria no Editor do modelo de fragmento de conteúdo. Basta arrastar e soltar o tipo de referência direito no modelo e configurar o campo . Esses tipos suportam seleção única ou múltipla.

![modelo pem cf](assets/pem-cf-model.png)

Se você criar um novo Fragmento do conteúdo com base nesse modelo, esses tipos de referência fornecerão uma maneira fácil de selecionar o objeto certo usando o respectivo seletor.

![pem cf](assets/pem-cf.png)

### Cockpit do produto {#product-cockpit}

Introduzimos o cockpit de produtos (ou console) num dos módulos anteriores. O cockpit é uma maneira fácil não só de navegar no catálogo de produtos, mas também de ver todo o conteúdo AEM associado num só local. Acesse o console do produto e abra as propriedades de um produto que tenha conteúdo associado. Alterne para a respectiva guia para ver o conteúdo associado.

![cockpit pem](assets/pem-cockpit.png)

Clicar no ícone de ação abrirá esse conteúdo em uma nova guia do navegador.

## Enriquecimento de páginas individuais de produto e categoria {#enrich}

Nos módulos anteriores, você aprendeu a trabalhar com vários modelos de catálogo de produtos. Vários modelos são uma ótima maneira de criar modelos diferentes, mas não são necessários em muitos casos. Em muitos casos, o mesmo modelo pode ser usado em combinação com espaços reservados para o conteúdo individual. A CIF é compatível com espaços reservados para Fragmentos de conteúdo e Fragmentos de experiência.

Vamos começar com o espaço reservado do Fragmento de experiência. Abra um modelo de produto no editor de AEM. Arraste e solte a **Fragmento de experiência de comércio** no modelo e abra a caixa de diálogo de configuração.

![espaço reservado para pem](assets/pem-placeholder.png)

Abra a caixa de diálogo do componente e insira um nome para esse espaço reservado. O nome do espaço reservado é necessário e permite adicionar quantos espaços reservados forem necessários.

![caixa de diálogo do pem XF](assets/pem-dialog-xf.png)

Abra o Fragmento de experiência associado a um produto na etapa anterior. Abra as propriedades e alterne para a guia commerce . Insira o mesmo nome de espaço reservado em **Local do espaço reservado do catálogo**.

![pem xf](assets/pem-xf.png)

Agora arraste e solte a **Fragmento de conteúdo de comércio** no modelo e abra a caixa de diálogo de configuração.

![caixa de diálogo do pem CF](assets/pem-dialog-cf.png)

Essa caixa de diálogo está reutilizando a caixa de diálogo Fragmento do conteúdo do componente principal . Encontre mais informações em recursos adicionais. A única diferença é que o **Elemento de link** propriedade que configura o campo identificador (SKU do produto ou UID da categoria) no modelo do Fragmento de conteúdo.

Visualizar agora uma página de produto que tem um Fragmento de conteúdo e/ou Fragmento de experiência associado. Quando o AEM renderiza uma página, ele faz uma pesquisa para cada espaço reservado com base no tipo (Fragmento de conteúdo ou experiência), no identificador e no nome do espaço reservado para Fragmentos de experiência. O AEM usa um resolvedor de URL para obter o identificador (SKU para produtos, UID para categorias). Se uma Experiência ou Fragmento de conteúdo for retornado, ele será renderizado no local do espaço reservado, caso contrário, o espaço reservado será ignorado.

![resultado do pem](assets/pem-result.png)

## Tornar o conteúdo comprável {#making-shoppable}

Também é possível tornar uma página de AEM comum comprável adicionando componentes de comércio. Crie uma nova página de conteúdo no AEM e abra a página vazia no editor.

![página vazia do pem](assets/pem-page-empty.png)

Primeiro, arraste e solte um componente de detalhes do produto na página. Em seguida, alterne para a barra lateral Ativos, alterne para produtos e selecione um produto. Arraste e solte o produto no componente do produto. Isso mostrará um componente de produto comum em uma página de conteúdo.

![página do produto pem](assets/pem-page-product.png)

Se você criou conteúdo associado para esse produto, alterne na barra lateral Ativos para **Conteúdo comercial associado**. Esta guia mostra todo AEM conteúdo que foi associado a este produto. Isso permite agora embelezar as páginas com qualquer conteúdo associado rapidamente.

![página enriquecida com pem](assets/pem-page-enriched.png)

## Fim da Jornada? {#end-of-journey}

Parabéns! Você concluiu a jornada do desenvolvedor de conteúdo e comércio AEM! Agora você deve:

* saiba como associar qualquer conteúdo AEM a objetos de catálogo de produtos
* usar espaços reservados para enriquecer individualmente as páginas de produto e categoria
* saiba como tornar o conteúdo passível de compra e usar a guia conteúdo associado

Agora você está pronto para gerenciar experiências de produtos usando Conteúdo e Comércio de AEM. No entanto, AEM conteúdo e comércio têm muitas opções adicionais disponíveis. Confira alguns dos recursos adicionais disponíveis no [Seção Recursos adicionais](#additional-resources) para saber mais sobre os recursos que você viu nesta jornada.

## Recursos adicionais {#additional-resources}

* [Criação de experiências comerciais](/help/commerce-cloud/authoring/authoring-commerce-experiences.md)
* [Cockpit do produto](/help/commerce-cloud/authoring/product-cockpit.md)
* [Componente do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=en)
