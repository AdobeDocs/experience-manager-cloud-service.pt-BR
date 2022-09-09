---
title: Práticas recomendadas de consulta e indexação
description: Saiba como otimizar seus índices e consultas com base nas diretrizes de práticas recomendadas do Adobe.
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
source-git-commit: afeff7cfb8606eb58126a4ca62ce9e6e58c44215
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---

# Práticas recomendadas de consulta e indexação {#query-and-indexing-best-practices}

Em AEM as a Cloud Service, todos os aspectos operacionais relativos à indexação são automatizados. Isso permite que os desenvolvedores se concentrem na criação de consultas eficientes e suas definições de índice correspondentes.

## Quando utilizar queries {#when-to-use-queries}

As consultas são uma maneira de acessar o conteúdo, mas não são a única possibilidade. Em muitas situações, o conteúdo no repositório pode ser acessado com mais eficiência por outros meios. Você deve considerar se as consultas são a melhor maneira e a mais eficiente de acessar o conteúdo do seu caso de uso.

### Design de repositório e taxonomia {#repository-and-taxonomy-design}

Ao projetar a taxonomia de um repositório, vários fatores precisam ser considerados. Isso inclui controles de acesso, localização, herança de propriedade de componente e página e muito mais.

Ao projetar uma taxonomia que atenda a essas preocupações, também é importante considerar a &quot;versabilidade&quot; do design de indexação. Nesse contexto, a navegabilidade é a capacidade de uma taxonomia permitir que o conteúdo seja acessado de forma previsível com base em seu caminho. Isso possibilita um sistema mais eficiente, mais fácil de manter do que um que requer a execução de várias consultas.

Além disso, ao projetar uma taxonomia, é importante considerar se a ordem é importante. Nos casos em que a ordenação explícita não é necessária e um grande número de nós irmãos é esperado, é preferível usar um tipo de nó não ordenado, como `sling:Folder` ou `oak:Unstructured`. Nos casos em que a encomenda é obrigatória, `nt:unstructured` e `sling:OrderedFolder` seria mais adequado.

### Consultas nos componentes {#queries-in-components}

Como as consultas podem ser uma das operações de taxação mais realizadas em um sistema de AEM, é recomendável evitá-las em seus componentes. Ter várias consultas executadas sempre que uma página é renderizada pode, com frequência, degradar o desempenho do sistema. Há duas estratégias que podem ser usadas para evitar a execução de consultas ao renderizar componentes: **[nós de percurso](#traversing-nodes)** e **[resultados da busca prévia.](#prefetching-results)**

### Nós de passagem {#traversing-nodes}

Se o repositório for projetado de forma que permita o conhecimento prévio da localização dos dados necessários, o código que recupera esses dados dos caminhos necessários poderá ser implantado sem a necessidade de executar consultas para encontrá-los.

Um exemplo disso seria renderizar o conteúdo que se encaixe em uma determinada categoria. Uma abordagem seria organizar o conteúdo com uma propriedade de categoria que possa ser consultada para preencher um componente que mostre itens em uma categoria.

Uma melhor abordagem seria estruturar esse conteúdo em uma taxonomia por categoria para que possa ser recuperado manualmente.

Por exemplo, se o conteúdo for armazenado em uma taxonomia semelhante a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

o `/content/myUnstructuredContent/parentCategory/childCategory` simplesmente pode ser recuperado, seus filhos podem ser analisados e usados para renderizar o componente.

Além disso, ao lidar com um conjunto de resultados pequeno ou homogêneo, pode ser mais rápido atravessar o repositório e coletar os nós necessários, em vez de criar um query para retornar o mesmo conjunto de resultados. De um modo geral, devem ser evitadas questões sempre que possível.

### Resultados da pré-busca {#prefetching-results}

Às vezes, o conteúdo ou os requisitos em torno do componente não permitem o uso do caminho do nó como um método de recuperação dos dados necessários. Nesses casos, as consultas necessárias precisam ser executadas antes que o componente seja renderizado para garantir o desempenho ideal.

Se os resultados necessários para o componente puderem ser calculados no momento da criação e não houver expectativa de que o conteúdo será alterado, a consulta poderá ser executada após uma alteração ter sido feita.

Se os dados ou o conteúdo forem alterados regularmente, a consulta poderá ser executada de acordo com uma programação ou por meio de um ouvinte para obter atualizações sobre os dados subjacentes. Em seguida, os resultados podem ser gravados em um local compartilhado no repositório. Qualquer componente que precise desses dados pode extrair os valores desse único nó sem precisar executar um query no tempo de execução.

Uma estratégia semelhante pode ser usada para manter o resultado em um cache na memória, que é preenchido na inicialização e atualizado sempre que as alterações são feitas (usando um JCR) `ObservationListener` ou um Sling `ResourceChangeListener`).

## Otimizando consultas {#optimizing-queries}

A documentação do Oak fornece um [visão geral de alto nível de como as consultas são executadas.](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing) Esta é a base de todas as atividades de otimização descritas neste documento.

AEM as a Cloud Service fornece a Ferramenta de Desempenho da Consulta, projetada para dar suporte à implementação de consultas eficientes.

* Ele exibe queries já executados com suas características de desempenho relevantes e o plano de query.
* Ela permite executar consultas ad-hoc em vários níveis, começando por exibir o plano de consulta até executar a consulta completa.

A Ferramenta de Desempenho da Consulta pode ser acessada por meio do [Console do desenvolvedor no Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=pt-BR#queries) AEM Ferramenta de desempenho de consulta da as a Cloud Service fornece mais informações sobre os detalhes da execução da consulta na versão AEM 6.x.

Este gráfico ilustra o fluxo geral para usar a Ferramenta de Desempenho da Consulta para otimizar consultas.

![Fluxo de otimização de consulta](assets/query-optimization-flow.png)

### Usar um índice {#use-an-index}

Cada query deve usar um índice para fornecer desempenho ideal. Na maioria dos casos, os índices prontos para uso existentes devem ser suficientes para lidar com consultas.

Às vezes, as propriedades personalizadas precisam ser adicionadas a um índice existente, para que restrições adicionais possam ser consultadas usando o índice. Consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md#changing-an-index) para obter mais detalhes. O [Folha de características da consulta JCR](#jcr-query-cheatsheet) A seção deste documento descreve como deve ser uma definição de propriedade em um índice para oferecer suporte a um tipo de query específico.

### Use os critérios certos {#use-the-right-criteria}

A restrição primária em qualquer query deve ser uma correspondência de propriedade, pois este é o tipo mais eficiente. Adicionar mais restrições de propriedade limita ainda mais o resultado.

O mecanismo de query considera apenas um único índice. Isso significa que um índice existente pode e deve ser personalizado adicionando mais propriedades de índice personalizadas a ele.

O [Folha de Consulta JCR](#jcr-query-cheatsheet) A seção deste documento lista as restrições disponíveis e também descreve como uma definição de índice precisa ser exibida para que seja escolhida. Use o [Ferramenta de desempenho da consulta](#query-performance-tool) para testar a query e garantir que o índice correto seja usado e que o mecanismo de query não precise avaliar restrições fora do índice.

### Solicitação {#ordering}

Se uma ordem específica do resultado for solicitada, há duas maneiras de o mecanismo de consulta alcançar isso:

1. O índice pode entregar o resultado completamente e na ordem correta.
   * Isso funcionará se as propriedades usadas para pedido forem anotadas com `ordered=true` na definição do índice.
1. O mecanismo de query executa o processo de solicitação.
   * Isso pode ocorrer quando o mecanismo de consulta executa a filtragem fora do índice ou a propriedade de ordenação não é anotada com a variável `ordered=true` propriedade.
   * Isso requer que o conjunto completo de resultados seja lido na memória para classificação, o que é muito mais lento do que a primeira opção.

### Restringir o tamanho do resultado {#restrict-result-size}

O tamanho recuperado do resultado da consulta é um fator importante no desempenho da consulta. Como o resultado é buscado de maneira preguiçosa, há uma diferença em apenas obter os primeiros 20 resultados em comparação a obter 10.000 resultados, tanto em tempo de execução quanto em uso de memória.

Isso também significa que o tamanho do conjunto de resultados só poderá ser determinado corretamente se todos os resultados forem obtidos. Por esse motivo, o conjunto de resultados buscados deve ser sempre limitado, aumentando o query (consulte [Folha de Consulta JCR](#jcr-query-cheatsheet) para obter detalhes) ou limitando as leituras dos resultados.

Esse limite também impede que o mecanismo de consulta atinja a variável **limite de travessia** de 100.000 nós, o que resulta em uma interrupção forçada da consulta.

Consulte a seção [Consultas com grandes resultados](#queries-with-large-result-sets) deste documento se um conjunto de resultados potencialmente grande tiver de ser completamente processado.

## Folha de características da consulta JCR {#jcr-query-cheatsheet}

Para dar suporte à criação de consultas JCR eficientes e definições de índice, o [Folha de Consulta JCR](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html#jcrquerycheatsheet) está disponível para download e uso como referência durante o desenvolvimento.

Ele contém consultas de amostra para o QueryBuilder, XPath e SQL-2, abrangendo vários cenários que se comportam de forma diferente em termos de desempenho de consulta. Também fornece recomendações sobre como criar ou personalizar índices do Oak. O conteúdo desta Folha de Cálculo se aplica a AEM as a Cloud Service e AEM 6.5.

## Consultas com Conjuntos de Resultados Grandes {#queries-with-large-result-sets}

Embora seja recomendável evitar consultas com conjuntos de resultados grandes, há casos válidos em que conjuntos de resultados grandes devem ser processados. Muitas vezes, o tamanho do resultado não é conhecido antecipadamente, pelo que devem ser tomadas algumas precauções para tornar o processamento fiável.

* A consulta não deve ser executada dentro de uma solicitação. Em vez disso, a consulta deve ser executada como parte de um Trabalho do Sling ou de um fluxo de trabalho AEM. Eles não têm limitações em seu tempo de execução total e são reiniciados caso a instância fique inativa durante o processamento da query e seus resultados.
* Para superar o limite de consulta de 100.000 nós, você deve considerar usar [Paginação do conjunto de chaves](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) e dividir a query em várias subconsultas.

## Traversal do Repositório {#repository-traversal}

As consultas que atravessam o repositório não usam um índice e estão fazendo logon com uma mensagem semelhante à seguinte.

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

Com este trecho de log, você pode determinar:

* O próprio query: `//*`
* O código Java que executou esta consulta: `com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics` para ajudar a identificar o criador do query.

Com essas informações, é possível otimizar essa consulta usando os métodos descritos no [Otimizando consultas](#optimizing-queries) seção deste documento.
