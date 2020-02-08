---
title: Uso de tags
description: Tags são um método rápido e fácil de classificar o conteúdo em um site
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Uso de tags {#using-tags}

Tags são um método rápido e fácil de classificar o conteúdo em um site. Tags podem ser consideradas palavras-chave ou rótulos que podem ser anexados a uma página, ativo ou outro conteúdo para permitir que as pesquisas encontrem esse conteúdo e todo o conteúdo relacionado.

* See Administering Tags for information about creating and managing tags, as well as to which content tags have been applied. <!-- See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, as well as to which content tags have been applied.-->
* See Tagging for Developers for information about the tagging framework as well as including and extending tags in custom applications. <!-- See [Tagging for Developers](/help/sites-developing/tags.md) for information about the tagging framework as well as including and extending tags in custom applications.-->

## Dez razões para usar marcação {#ten-reasons-to-use-tagging}

1. **Organizar conteúdo** - Marcar facilita a vida dos autores, pois eles podem organizar rapidamente o conteúdo com pouco esforço.
1. **Organizar tags** - Enquanto as tags organizam o conteúdo, as taxonomias/namespaces hierárquicas organizam as tags.
1. **Tags** profundamente organizadas - Com a capacidade de criar tags e subtags, torna-se possível expressar sistemas taxonômicos inteiros, abrangendo termos, subtermos e seus relacionamentos. É possível criar uma segunda (ou terceira) hierarquia de conteúdo em paralelo à oficial.
1. **Marcação** controlada - A marcação pode ser controlada pela aplicação de permissões a marcadores e/ou espaços de nomes para controlar a criação de marcadores e aplicativos.
1. **Marcação** flexível - As tags têm muitos nomes e rostos: tags, termos de taxonomia, categorias, rótulos e muito mais. Elas são flexíveis em seu modelo de conteúdo e na maneira como podem ser usadas. Por exemplo, ao estruturar dados demográficos de direcionamento, categorizar e classificar conteúdo ou criar uma hierarquia de conteúdo secundário.
1. **Pesquisa** aprimorada - o componente de pesquisa padrão no AEM geralmente inclui tags criadas e aplicadas às quais os filtros podem ser aplicados para restringir os resultados àqueles que são relevantes.
1. **Ativação** de SEO - As tags aplicadas como propriedades de página serão exibidas automaticamente nas métricas da página, tornando-a visível para os mecanismos de pesquisa.
1. **Simples sofisticação** - As tags podem ser simplesmente criadas a partir de uma palavra e do toque de um botão. Posteriormente, um título, uma descrição e um número ilimitado de etiquetas podem ser adicionadas para fornecer mais semântica à tag.
1. **Consistência** principal - o sistema de marcação é um componente principal do AEM e é usado por todos os recursos do AEM para classificar o conteúdo. Além disso, a API de marcação está disponível para os desenvolvedores criarem aplicativos ativados para marcação com acesso às mesmas taxonomias.
1. **Combina estrutura e flexibilidade** - o AEM é ideal para trabalhar com informações estruturadas, devido ao aninhamento de páginas e caminhos. Ele é igualmente eficiente quando se trabalha com informações não estruturadas, devido à pesquisa de texto completo integrada. A marcação combina os pontos fortes de estrutura e flexibilidade.

Ao projetar a estrutura de conteúdo de um site e o esquema de metadados para ativos, considere a abordagem leve e acessível de tags.

## Aplicação de tags {#applying-tags}

In the author environment, authors may apply tags by accessing the page properties and entering one or more tags in the **Tags/Keywords** field.

To apply pre-defined tags, in the **Page Properties** window use the **Tags** field and the **Select Tags** window. The **Standard Tags** tab is the default namespace, which means there is no `namespace-string:` prefixed to the taxonomy. <!-- To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window.-->

![Selecionar várias tags](/help/sites-cloud/authoring/assets/tags-select.png)

## Publicação de tags {#publishing-tags}

Semelhante à forma como você pode publicar e cancelar a publicação de páginas, é possível executar o seguinte em tags e namespaces:

### Ativar {#activate}

* Ativar tags individuais.

   Assim como com as páginas, tags recém-criadas precisam ser ativadas antes de serem disponibilizadas no ambiente de publicação.

>[!NOTE]
>
>Quando você ativa uma página, uma caixa de diálogo é aberta automaticamente e permite ativar tags não ativadas pertencentes à página.

### Desativar {#deactivate}

* Desativar as tags selecionadas.
