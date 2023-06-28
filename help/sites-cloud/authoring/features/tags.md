---
title: Uso de tags
description: As tags são um método rápido e fácil de classificar conteúdo em um site
exl-id: d2a9f578-fe0a-48ea-851c-2c84463661e0
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 75%

---

# Uso de tags   {#using-tags}

As tags são um método rápido e fácil de classificar conteúdo em um site. As tags podem ser consideradas palavras-chave ou rótulos que podem ser anexados a uma página, um ativo ou outro conteúdo para permitir que as pesquisas localizem esse conteúdo e conteúdo relacionado.

* Consulte Administração de tags para obter informações sobre como criar e gerenciar tags e sobre quais tags de conteúdo foram aplicadas. <!-- See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, and to which content tags have been applied.-->
* Consulte [Marcação para desenvolvedores](/help/implementing/developing/introduction/tagging-framework.md) para obter informações sobre a estrutura de marcação e incluir e estender tags em aplicativos personalizados.

## Dez razões para usar marcação {#ten-reasons-to-use-tagging}

1. **Organização do conteúdo** - a marcação facilita a vida dos autores, pois eles podem organizar rapidamente o conteúdo com pouco esforço.
1. **Organização de tags** - enquanto tags organizam conteúdo, taxonomias/espaços de nome hierárquicos organizam tags.
1. **Tags profundamente organizadas** - com a capacidade de criar tags e subtags, é possível expressar sistemas taxonômicos inteiros, abrangendo termos, subtermos e seus relacionamentos. É possível criar uma segunda (ou terceira) hierarquia de conteúdo em paralelo à oficial.
1. **Marcação controlada** - a marcação pode ser controlada com a aplicação de permissões a tags e/ou espaços de nome para controlar a criação e a aplicação de tags.
1. **Marcação flexível** - tags têm muitos nomes e faces: tags, termos de taxonomia, categorias, rótulos e muito mais. Elas são flexíveis em seu modelo de conteúdo e na maneira como podem ser usadas. Por exemplo, ao estruturar dados demográficos de direcionamento, categorizar e classificar conteúdo ou criar uma hierarquia de conteúdo secundário.
1. **Pesquisas aprimoradas** - o componente de pesquisa padrão no AEM inclui amplamente tags criadas e tags aplicadas, às quais é possível aplicar filtros para restringir os resultados apenas àqueles que são relevantes.
1. **Habilitação de SEO** - aplicadas como propriedades de página aparecerão automaticamente nas metatags da página, tornando-a visível para os mecanismos de pesquisa.
1. **Sofisticação simples** - tags podem ser criadas simplesmente a partir de uma palavra e com o toque de um botão. Posteriormente, um título, uma descrição e um número ilimitado de etiquetas podem ser adicionadas para fornecer mais semântica à tag.
1. **Consistência básica** - o sistema de marcação é um componente central do AEM e é usado por todos os recursos do AEM para categorizar o conteúdo. Além disso, a API de marcação está disponível para os desenvolvedores criarem aplicativos ativados para marcação com acesso às mesmas taxonomias.
1. **Combina estrutura e flexibilidade** - AEM é ideal para trabalhar com informações estruturadas, devido ao aninhamento de páginas e caminhos. Ela é igualmente eficiente ao trabalhar com informações não estruturadas, devido à pesquisa integrada de texto completo. A marcação combina os pontos fortes da estrutura e da flexibilidade.

Ao projetar a estrutura de conteúdo para um site e o esquema de metadados para ativos, considere a abordagem mais leve e acessível que a marcação oferece.

## Aplicação de tags   {#applying-tags}

No ambiente de criação, os autores podem aplicar tags acessando as propriedades da página e digitando uma ou mais tags no campo **Tags/Palavras-chave**.

Para aplicar tags predefinidas, na janela **Propriedades da página**, use o campo **Tags** e a janela **Selecionar tags**. A guia **Tags padrão** é o namespace padrão, o que significa que não há `namespace-string:` prefixado à taxonomia. <!-- To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window.-->

![Selecionar várias tags](/help/sites-cloud/authoring/assets/tags-select.png)

## Publicação de tags {#publishing-tags}

Semelhante à forma como você pode publicar e desfazer a publicação de páginas, é possível executar o seguinte em tags e namespaces:

### Ativar {#activate}

* Ativar tags individuais.

  Assim como com as páginas, tags recém-criadas precisam ser ativadas antes de serem disponibilizadas no ambiente de publicação.

>[!NOTE]
>
>Quando você ativa uma página, uma caixa de diálogo é aberta automaticamente e permite ativar tags não ativadas pertencentes a essa página.

### Desativar {#deactivate}

* Desativar as tags selecionadas.
