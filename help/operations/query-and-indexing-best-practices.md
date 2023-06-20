---
title: Práticas recomendadas de consulta e indexação
description: Saiba como otimizar seus índices e consultas com base nas diretrizes de práticas recomendadas da Adobe.
topic-tags: best-practices
exl-id: 37eae99d-542d-4580-b93f-f454008880b1
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 95%

---

# Práticas recomendadas de consulta e indexação {#query-and-indexing-best-practices}

No AEM as a Cloud Service, todos os aspectos operacionais relativos à indexação são automatizados. Isso permite que os desenvolvedores se concentrem na criação de consultas eficientes e suas definições de índice correspondentes.

## Quando utilizar consultas {#when-to-use-queries}

As consultas são uma maneira de acessar conteúdo, mas não são a única possibilidade. Em muitas situações, o conteúdo do repositório pode ser acessado com mais eficiência por outros meios. Você deve considerar se as consultas são a melhor e mais eficiente maneira de acessar o conteúdo no seu caso de uso.

### Design de repositório e taxonomia {#repository-and-taxonomy-design}

Ao projetar a taxonomia de um repositório, vários fatores precisam ser considerados. Entre eles, controles de acesso, localização, herança de propriedade de componente e página e muito mais.

Ao projetar uma taxonomia que atenda a essas questões, também é importante considerar a flexibilidade do design de indexação. Nesse contexto, a “flexibilidade” é a capacidade de uma taxonomia permitir que o conteúdo seja acessado de forma previsível com base em seu caminho. Isso torna o sistema mais eficiente e fácil de manter do que um que requer a execução de várias consultas.

Além disso, ao projetar uma taxonomia, é importante considerar se a ordenação é importante. Nos casos em que a ordenação explícita não é obrigatória e um grande número de nós semelhantes é esperado, é preferível usar um tipo de nó não ordenado, como `sling:Folder` ou `oak:Unstructured`. Nos casos em que a ordenação é obrigatória, `nt:unstructured` e `sling:OrderedFolder` seriam mais adequados.

### Consultas em componentes {#queries-in-components}

Como as consultas podem ser uma das operações mais exigentes realizadas em um sistema AEM, é recomendável evitá-las em seus componentes. A execução de várias consultas cada vez que uma página é renderizada pode prejudicar o desempenho do sistema. Há duas estratégias que podem ser usadas para evitar a execução de consultas ao renderizar componentes: **[nós de passagem](#traversing-nodes)** e **[resultados de busca prévia.](#prefetching-results)**

### Nós de passagem {#traversing-nodes}

Se o repositório for projetado de uma forma que permita o conhecimento prévio da localização dos dados necessários, o código que recupera esses dados dos caminhos necessários poderá ser implantado sem a necessidade de executar consultas para encontrá-los.

Um exemplo disso seria a renderização de um conteúdo que se encaixe em uma determinada categoria. Uma abordagem seria organizar o conteúdo com uma propriedade de categoria que possa ser consultada para preencher um componente que mostre itens em uma categoria.

No entanto, uma melhor abordagem seria estruturar esse conteúdo em uma taxonomia por categoria para que ele possa ser recuperado manualmente.

Por exemplo, se o conteúdo for armazenado em uma taxonomia semelhante a:

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

o nó `/content/myUnstructuredContent/parentCategory/childCategory` pode simplesmente ser recuperado e seus secundários podem ser analisados e usados para renderizar o componente.

Além disso, ao lidar com um conjunto de resultados pequeno ou homogêneo, pode ser mais rápido percorrer o repositório e coletar os nós necessários, em vez de criar uma consulta para retornar o mesmo conjunto de resultados. Como consideração geral, as consultas devem ser evitadas sempre que possível.

### Resultados de busca prévia {#prefetching-results}

Às vezes, o conteúdo ou os requisitos do componente não permitem o uso de nós de passagem como um método de recuperação dos dados necessários. Nesses casos, as consultas obrigatórias precisam ser executadas antes que o componente seja renderizado para garantir um desempenho ideal.

Se os resultados obrigatórios para o componente puderem ser calculados no momento da criação e não houver expectativa de que o conteúdo seja alterado, a consulta poderá ser executada após uma alteração ter sido feita.

Se os dados ou o conteúdo forem alterados regularmente, a consulta poderá ser executada de acordo com uma programação ou por meio de um ouvinte para obter atualizações sobre os dados subjacentes. Em seguida, os resultados podem ser gravados em um local compartilhado no repositório. Qualquer componente que precise desses dados pode extrair os valores desse único nó, sem precisar executar uma consulta em tempo de execução.

Uma estratégia semelhante pode ser usada para manter o resultado em uma memória cache, que é preenchida na inicialização e atualizada sempre que as alterações são feitas (usando um JCR `ObservationListener` ou um Sling `ResourceChangeListener`).

## Otimização de consultas {#optimizing-queries}

A documentação do Oak fornece uma [visão geral de alto nível de como as consultas são executadas.](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-processing) Isso forma a base de todas as atividades de otimização descritas neste documento.

O AEM as a Cloud Service fornece a Ferramenta de desempenho de consulta, desenvolvida para ajudar na implementação de consultas eficientes.

* Ela exibe consultas já executadas com suas características de desempenho relevantes e o plano de consulta.
* Ela permite executar consultas ad-hoc em vários níveis, desde a exibição do plano de consulta até a execução da consulta completa.

A Ferramenta de desempenho de consulta pode ser acessada por meio do [Console do desenvolvedor no Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=pt-BR#queries) A Ferramenta de desempenho de consulta do AEM as a Cloud Service fornece mais detalhes sobre a execução da consulta do que a versão AEM 6.x.

Este gráfico ilustra o fluxo geral de uso da Ferramenta de desempenho de consulta na otimização de consultas.

![Fluxo de otimização de consulta](assets/query-optimization-flow.png)

### Usar um índice {#use-an-index}

Cada consulta deve usar um índice para fornecer desempenho ideal. Na maioria dos casos, os índices prontos para uso existentes devem ser suficientes para lidar com as consultas.

Às vezes, as propriedades personalizadas precisam ser adicionadas a um índice existente, para que restrições adicionais possam ser consultadas usando o índice. Consulte o documento [Pesquisa e indexação de conteúdo](/help/operations/indexing.md#changing-an-index) para obter mais detalhes. A variável [Folha de características de consulta JCR](#jcr-query-cheatsheet) seção deste documento descreve como deve ser uma definição de propriedade em um índice para suportar um tipo de consulta específico.

### Use os critérios certos {#use-the-right-criteria}

A restrição primária em qualquer consulta deve ser uma correspondência de propriedade, pois este é o tipo mais eficiente. Adicionar mais restrições de propriedade limita ainda mais o resultado.

O mecanismo de consulta considera apenas um único índice. Isso significa que um índice existente pode e deve ser personalizado adicionando mais propriedades de índice personalizadas a ele.

A seção [Folha de características de consulta JCR](#jcr-query-cheatsheet) deste documento lista as restrições disponíveis e também descreve como criar uma definição de índice adequada para uso. Use a [Ferramenta de desempenho da consulta](#query-performance-tool) para testar a consulta e garantir que o índice correto esteja sendo usado e que o mecanismo de consulta não precise avaliar restrições fora do índice.

### Ordenação {#ordering}

Se uma ordem específica do resultado for solicitada, há duas maneiras de o mecanismo de consulta alcançar isso:

1. O índice pode entregar o resultado completo e na ordem correta.
   * Isso funciona se as propriedades usadas para a ordenação forem anotadas com `ordered=true` na definição do índice.
1. O mecanismo de consulta executa o processo de ordenação.
   * Isso pode ocorrer quando o mecanismo de consulta executa a filtragem fora do índice ou a propriedade de ordenação não é anotada com a propriedade `ordered=true`.
   * Isso requer que o conjunto completo de resultados seja lido na memória para classificação, o que é muito mais lento do que a primeira opção.

### Restringir o tamanho do resultado {#restrict-result-size}

O tamanho recuperado do resultado da consulta é um fator importante no desempenho da consulta. Como o resultado é recebido lentamente, há uma diferença entre obter apenas os primeiros 20 resultados e obter 10.000 resultados, tanto em tempo de execução quanto em uso de memória.

Isso também significa que o tamanho do conjunto de resultados só poderá ser determinado corretamente se todos os resultados forem obtidos. Por esse motivo, o conjunto de resultados obtido deve ser sempre limitado, seja aumentando a consulta (consulte a seção [Folha de características de consulta JCR](#jcr-query-cheatsheet) para obter detalhes) ou limitando as leituras dos resultados.

Esse limite também impede que o mecanismo de consulta atinja o **limite de passagem** de 100.000 nós, o que resulta em uma interrupção forçada da consulta.

Consulte a seção [Consultas com muitos resultados](#queries-with-large-result-sets) deste documento se um conjunto de resultados potencialmente grande tiver de ser processado por completo.

## Folha de características de consulta JCR {#jcr-query-cheatsheet}

Para auxiliar na criação de consultas JCR e definições de índice eficientes, a [Folha de características de consulta JCR](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/practices/best-practices-for-queries-and-indexing.html?lang=pt-BR#jcrquerycheatsheet) está disponível para download e uso como referência durante o desenvolvimento.

Ela contém exemplos de consulta para o QueryBuilder, XPath e SQL-2, e abrange vários cenários que se comportam de maneira diferente em termos de desempenho de consulta. Ela também fornece recomendações sobre como criar ou personalizar índices do Oak. O conteúdo desta Folha de características se aplica ao AEM as a Cloud Service e ao AEM 6.5.

## Consultas com conjuntos de resultados grandes {#queries-with-large-result-sets}

Embora seja recomendável evitar consultas com conjuntos de resultados grandes, há casos válidos em que eles precisam ser processados. Muitas vezes, o tamanho do resultado não é conhecido antecipadamente. Portanto, algumas precauções devem ser tomadas para tornar o processamento confiável.

* A consulta não deve ser executada dentro de uma solicitação. Em vez disso, a consulta deve ser executada como parte de uma tarefa do Sling ou de um fluxo de trabalho do AEM. Esses processos não têm limitações em seu tempo de execução total e são reiniciados caso a instância fique inativa durante o processamento da consulta e de seus resultados.
* Para superar o limite de consulta de 100.000 nós, você deve considerar usar uma [Paginação keyset](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Keyset_Pagination) e dividir a consulta em várias subconsultas.

## Passagem pelo repositório {#repository-traversal}

As consultas que percorrem o repositório não usam um índice e são registradas com uma mensagem semelhante à seguinte.

```text
28.06.2022 13:32:52.804 *WARN* [127.0.0.1 [1656415972414] POST /libs/settings/granite/operations/diagnosis/granite_queryperformance.explain.json HTTP/1.1] org.apache.jackrabbit.oak.plugins.index.Cursors$TraversingCursor Traversed 98000 nodes with filter Filter(query=select [jcr:path], [jcr:score], * from [nt:base] as a /* xpath: //* */, path=*) called by com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet.getHeuristics; consider creating an index or changing the query
```

Com este trecho de log, você pode determinar:

* A própria consulta: `//*`
* O código Java que executou esta consulta: `com.adobe.granite.queries.impl.explain.query.ExplainQueryServlet::getHeuristics` para ajudar a identificar o criador da consulta.

Com essas informações, é possível otimizar a consulta usando os métodos descritos na seção [Otimização de consultas](#optimizing-queries) deste documento.
