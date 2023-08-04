---
title: Criação de experiências de produto
description: Saiba como criar conteúdo de produto que pode ser usado em vários canais para criar uma experiência de compra imersiva.
exl-id: 4ae70e40-fdf1-4a37-b4dd-0c4882d77908
source-git-commit: 412e206a66de470e2798aafc58bcac93dc7e3cad
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 4%

---

# Criação de experiências de produto {#building-experiences}

Saiba como gerenciar experiências de produtos.

## A história até agora {#story-so-far}

No documento anterior da jornada de Conteúdo e Comércio do AEM, [Gerenciar experiências de catálogo de produtos por etapas](staged-catalog.md), você aprendeu a gerenciar experiências de catálogo de produtos por etapas.

## Objetivo {#objective}

Este documento ajuda você a entender como criar conteúdo e experiências de produto.

## Gerenciamento da experiência do produto {#management}

O Gerenciamento de experiência do produto é a disciplina para decorar dados do produto (que pertence a um PIM ou solução comercial) com conteúdo de marketing no AEM. Esses dados de produto enriquecidos com conteúdo podem ser usados em vários canais para criar uma experiência de compra imersiva.

No AEM, é possível criar vários tipos de conteúdo e vinculá-los ao catálogo de produtos. O conteúdo associado pode ser facilmente descoberto e usado, o que resulta em alta produtividade.

### Assets {#assets}

Em um alto nível, há dois tipos de ativos relacionados aos produtos: produto e marketing. Os ativos do produto geralmente são gerenciados pelos comerciantes e se concentram em mostrar o produto (principalmente na frente de um fundo neutro). Os ativos são gerenciados na solução comercial ou na AEM Assets (com uma integração do Assets à solução comercial/pim).

Os ativos de marketing estão relacionados à promoção e ao uso do produto que geralmente pertence ao marketing. Exemplos são: exibição de vários produtos (&quot;comprar a aparência&quot;), em um contexto específico (&quot;coleção de outono ao ar livre&quot;) ou pdfs de instruções. A CIF fornece uma maneira fácil de vincular qualquer ativo AEM ao objeto de catálogo de produtos.

Abra as propriedades do ativo e alterne para a guia **Commerce** guia. Essa guia permite gerenciar a associação com produtos. A tabela abaixo do seletor fornece informações adicionais para os objetos vinculados (visíveis apenas com uma seleção). Clique no ícone de detalhes para obter uma exibição completa na ferramenta cockpit do produto. Para associar um novo objeto, clique no ícone do seletor de produtos (ícone de pasta), selecione um objeto e feche o seletor.

![ativos pem](assets/pem-assets.png)

### Fragmentos de experiência {#experience-fragments}

Fragmentos de experiência são uma ótima maneira de criar conteúdo reutilizável ou de produto individual em escala. A associação funciona de forma semelhante a um ativo. Abra as propriedades e alterne para a guia **Commerce** guia. Essa guia permite gerenciar a associação com produtos e categorias. As tabelas abaixo dos seletores fornecem informações adicionais para os objetos vinculados (visíveis apenas com uma seleção). Clique no ícone de detalhes para obter uma exibição completa na ferramenta cockpit do produto. Para associar um novo objeto, clique no ícone do seletor de produtos (ícone de pasta), selecione um objeto e feche o seletor.

![pem xf](assets/pem-xf.png)

### Fragmentos de conteúdo {#content-fragments}

Fragmentos de conteúdo são o melhor tipo de conteúdo para qualquer conteúdo estruturado. Isso pode ser usado para aumentar os dados externos do produto com dados de marketing adicionais ou para criar conteúdo de forma headless. A associação de um fragmento de conteúdo a um objeto de catálogo de produtos ocorre por meio dos tipos de referência de produto ou categoria no Editor de modelos de fragmento de conteúdo. Basta arrastar e soltar o tipo de referência correto no modelo e configurar o campo. Esses tipos oferecem suporte para seleção única ou múltipla.

![modelo pem cf](assets/pem-cf-model.png)

Se você criar um novo Fragmento de conteúdo com base nesse modelo, esses tipos de referência fornecerão uma maneira fácil de selecionar o objeto correto usando o respectivo seletor.

![pem cf](assets/pem-cf.png)

### Cockpit do produto {#product-cockpit}

Introduzimos o cockpit (ou console) do produto em um dos módulos anteriores. O cockpit é uma maneira fácil não apenas de navegar no catálogo de produtos, mas também de ver todo o conteúdo AEM associado em um único lugar. Vá para o console do produto e abra as propriedades de um produto com conteúdo associado. Alterne para a respectiva guia para ver o conteúdo associado.

![pem cockpit](assets/pem-cockpit.png)

Clicar no ícone de ação abrirá esse conteúdo em uma nova guia do navegador.

## Enriquecimento de páginas de produto e categoria individuais {#enrich}

Nos módulos anteriores, você aprendeu a trabalhar com vários modelos de catálogo de produtos. Vários modelos são uma ótima maneira de criar modelos diferentes, mas não são necessários em muitos casos. Em muitos casos, o mesmo modelo pode ser usado em combinação com espaços reservados para conteúdo individual. A CIF oferece suporte a espaços reservados para Fragmentos de conteúdo e Fragmentos de experiência.

Vamos começar com o espaço reservado para Fragmento de experiência. Abra um modelo de produto no editor de AEM. Arraste e solte a **Fragmento de experiência do Commerce** no modelo e abra a caixa de diálogo de configuração.

![espaço reservado para pem](assets/pem-placeholder.png)

Abra a caixa de diálogo do componente e insira um nome para esse espaço reservado. O nome do espaço reservado é obrigatório e permite adicionar quantos espaços reservados forem necessários.

![caixa de diálogo pem XF](assets/pem-dialog-xf.png)

Abra o Fragmento de experiência que você associou a um produto na etapa anterior. Abra as propriedades e alterne para a guia comércio. Insira o mesmo nome de espaço reservado em **Local do espaço reservado do catálogo**.

![pem xf](assets/pem-xf.png)

Agora, arraste e solte a **Fragmento de conteúdo do Commerce** no modelo e abra a caixa de diálogo de configuração.

![caixa de diálogo pem CF](assets/pem-dialog-cf.png)

Essa caixa de diálogo está reutilizando a caixa de diálogo Fragmento de conteúdo do componente principal. Encontre mais informações em recursos adicionais. A única diferença é a **Elemento do link** propriedade que configura o campo identificador (SKU do produto ou UID da categoria) no modelo de Fragmento de conteúdo.

Visualize agora uma página de produto que tem um Fragmento de conteúdo e/ou Fragmento de experiência associado. Quando o AEM renderiza uma página, ele faz uma pesquisa por cada espaço reservado com base no tipo (Conteúdo ou Fragmento de experiência), identificador e nome do espaço reservado para Fragmentos de experiência. O AEM usa um resolvedor de URL para obter o identificador (SKU para produtos, UID para categorias). Se um Fragmento de experiência ou conteúdo for retornado, ele será renderizado no local do espaço reservado, caso contrário, o espaço reservado será ignorado.

![resultado pem](assets/pem-result.png)

## Tornar o conteúdo shoppable {#making-shoppable}

Também é possível fazer com que uma página AEM comum possa ser comprada adicionando componentes comerciais. Crie uma nova página de conteúdo no AEM e abra a página vazia no editor.

![página vazia de pem](assets/pem-page-empty.png)

Primeiro, arraste e solte um componente de detalhes do produto na página. Em seguida, alterne para a barra lateral Ativos, alterne para produtos e selecione um produto. Arraste e solte esse produto no componente do produto. Isso mostrará um componente de produto regular em uma página de conteúdo.

![página do produto pem](assets/pem-page-product.png)

Se você tiver criado conteúdo associado para esse produto, alterne na barra lateral do Assets para **Conteúdo de comércio associado**. Esta guia mostra todo o conteúdo do AEM associado a este produto. Isso permite que você embeleze rapidamente as páginas com qualquer conteúdo associado.

![página enriquecida com pem](assets/pem-page-enriched.png)

## Fim da jornada? {#end-of-journey}

Parabéns! Você concluiu a jornada para desenvolvedores de conteúdo e comércio do AEM! Agora você deve:

* entenda como associar qualquer conteúdo AEM a objetos de catálogo de produtos
* usar espaços reservados para enriquecer individualmente as páginas de produto e categoria
* saber como tornar o conteúdo comprável e usar a guia conteúdo associado

Agora você está pronto para gerenciar experiências de produto usando Conteúdo e Comércio AEM. No entanto, o AEM Content and Commerce tem muitas opções adicionais disponíveis. Confira alguns dos recursos adicionais disponíveis na [seção Recursos adicionais](#additional-resources) para saber mais sobre os recursos que você viu nesta jornada.

## Recursos adicionais {#additional-resources}

* [Criação de experiências de comércio](/help/commerce-cloud/authoring/authoring-commerce-experiences.md)
* [Cockpit do produto](/help/commerce-cloud/authoring/product-cockpit.md)
* [Componente Fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=en)
