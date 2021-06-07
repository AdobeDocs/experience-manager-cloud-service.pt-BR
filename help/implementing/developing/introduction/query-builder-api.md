---
title: API do Construtor de consulta
description: A funcionalidade do Construtor de consultas de compartilhamento de ativos é exposta por meio de uma API Java e uma API REST.
exl-id: d5f22422-c9da-4c9d-b81c-ffa5ea7cdc87
source-git-commit: a446efacb91f1a620d227b9413761dd857089c96
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 0%

---

# API do Construtor de consulta {#query-builder-api}

O Construtor de consultas oferece uma maneira fácil de consultar o repositório de conteúdo do AEM. A funcionalidade é exposta por meio de uma API Java e uma API REST. Este documento descreve essas APIs.

O construtor de consultas do lado do servidor ([`QueryBuilder`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html)) aceitará uma descrição de consulta, criará e executará uma consulta XPath, filtrará opcionalmente o conjunto de resultados e também extrairá facetas, se desejado.

A descrição da consulta é simplesmente um conjunto de predicados ([`Predicate`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/Predicate.html)). Os exemplos incluem um predicado de texto completo, que corresponde à função `jcr:contains()` no XPath.

Para cada tipo de predicado, há um componente avaliador ([`PredicateEvaluator`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/PredicateEvaluator.html)) que sabe como lidar com esse predicado específico para XPath, filtragem e extração de faceta. É muito fácil criar avaliadores personalizados, que são conectados por meio do tempo de execução do componente OSGi.

A REST API fornece acesso a exatamente os mesmos recursos por meio de HTTP, com respostas sendo enviadas em JSON.

>[!NOTE]
>
>A API do QueryBuilder é criada usando a API JCR. Você também pode consultar o JCR AEM usando a API JCR de um pacote OSGi. Para obter informações, consulte [Consultando dados do Adobe Experience Manager usando a API JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Sessão Gem {#gem-session}

[AEM ](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-index.html) Gemis mergulha uma série de aprofundamentos técnicos no Adobe Experience Manager, fornecidos por especialistas em Adobe.

Você pode [revisar a sessão dedicada ao construtor de consultas](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-search-forms-using-querybuilder.html) para obter uma visão geral e usar a ferramenta.

## Consultas de exemplo {#sample-queries}

Essas amostras são fornecidas na notação do estilo das propriedades Java. Para usá-los com a API do Java, use um Java `HashMap` como na amostra da API a seguir.

Para o `QueryBuilder` Servlet JSON, cada exemplo inclui um link de amostra para uma instalação AEM (no local padrão, `http://<host>:<port>`). Observe que é necessário fazer logon na instância do AEM antes de usar esses links.

>[!CAUTION]
>
>Por padrão, o servlet JSON do construtor de consultas exibe no máximo 10 ocorrências.
>
>Adicionar o seguinte parâmetro permite que o servlet exiba todos os resultados da consulta:
>
>`p.limit=-1`

>[!NOTE]
>
>Para exibir os dados JSON retornados em seu navegador, você pode usar um plug-in como JSONView para Firefox.

### Retornar todos os resultados {#returning-all-results}

A consulta a seguir **retornará dez resultados** (ou para ser preciso no máximo dez), mas informará o número de ocorrências **que estão realmente disponíveis:**:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
orderby=path
```

A mesma consulta (com o parâmetro `p.limit=-1`) retornará todos os resultados **(pode ser um número alto, dependendo da sua instância):**

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&orderby=path&p.limit=-1`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.limit=-1
orderby=path
```

### Usar p.guessTotal para retornar os resultados {#using-p-guesstotal-to-return-the-results}

A finalidade do parâmetro `p.guessTotal` é retornar o número apropriado de resultados que podem ser mostrados ao combinar os valores mínimos viáveis `p.offset` e `p.limit`. A vantagem de usar esse parâmetro é o desempenho aprimorado com grandes conjuntos de resultados. Isso evita calcular o total completo (por exemplo, chamar `result.getSize()`) e ler todo o conjunto de resultados, otimizado até o mecanismo e índice OAK. Essa pode ser uma diferença significativa quando há centenas de milhares de resultados, tanto no tempo de execução quanto no uso da memória.

A desvantagem do parâmetro é que os usuários não veem o total exato. Mas você pode definir um número mínimo como `p.guessTotal=1000` para que ele sempre leia até 1000, para que você obtenha totais exatos para conjuntos de resultados menores, mas se for mais que isso, você só poderá mostrar &quot;e mais&quot;.

Adicione `p.guessTotal=true` à consulta abaixo para ver como funciona:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=true&orderby=path`

```xml
path=/content
1_property=sling:resourceType
1_property.value=wknd/components/structure/page
1_property.operation=like
p.guessTotal=true
orderby=path
```

A query retornará o padrão `p.limit` de `10` resultados com um deslocamento `0`:

```xml
"success": true,
"results": 10,
"total": 10,
"more": true,
"offset": 0,
```

Você também pode usar um valor numérico para contar até um número personalizado de resultados máximos. Use a mesma consulta como acima, mas altere o valor de `p.guessTotal` para `50`:

`http://<host>:<port>/bin/querybuilder.json?path=/content&1_property=sling:resourceType&1_property.value=wknd/components/structure/page&1_property.operation=like&p.guessTotal=50&orderby=path`

Ele retornará um número com o mesmo limite padrão de 10 resultados com um deslocamento 0, mas exibirá apenas um máximo de 50 resultados:

```xml
"success": true,
"results": 10,
"total": 50,
"more": true,
"offset": 0,
```

### Implementação da paginação {#implementing-pagination}

Por padrão, o Construtor de consultas também forneceria o número de ocorrências. Dependendo do tamanho do resultado, isso pode demorar muito tempo, pois determinar a contagem precisa envolve verificar cada resultado para o controle de acesso. A maioria do total é usada para implementar a paginação da interface do usuário final. Como determinar a contagem exata pode ser lenta, é recomendável usar o recurso guessTotal para implementar a paginação.

Por exemplo, a interface do usuário pode adaptar a seguinte abordagem:

* Obter e exibir a contagem precisa do número total de ocorrências ([SearchResult.getTotalMatches()](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/result/SearchResult.html#getTotalMatches) ou total na resposta `querybuilder.json`) são menores ou iguais a 100;
* Defina `guessTotal` como 100 ao fazer a chamada para o Construtor de consultas.

* A resposta pode ter o seguinte resultado:

   * `total=43`,  `more=false`  - Indica que o número total de ocorrências é 43. A interface do usuário pode exibir até dez resultados como parte da primeira página e fornecer paginação para as próximas três páginas. Também é possível usar essa implementação para exibir um texto descritivo como **&quot;43 resultados encontrados&quot;**.
   * `total=100`,  `more=true`  - Indica que o número total de ocorrências é maior que 100 e que a contagem exata não é conhecida. A interface do usuário pode exibir até dez como parte da primeira página e fornecer paginação para as próximas dez páginas. Também é possível usar essa opção para exibir um texto como **&quot;mais de 100 resultados encontrados&quot;**. Conforme o usuário vai para as próximas páginas, as chamadas feitas para o Construtor de consultas aumentariam o limite de `guessTotal` e também dos parâmetros `offset` e `limit`.

`guessTotal` também deve ser usada em casos em que a interface do usuário precisa usar a rolagem infinita, para evitar que o Construtor de consultas determine a contagem exata de ocorrências.

### Encontre arquivos jar e ordene-os, primeiro mais recentes {#find-jar-files-and-order-them-newest-first}

`http://<host>:<port>/bin/querybuilder.json?type=nt:file&nodename=*.jar&orderby=@jcr:content/jcr:lastModified&orderby.sort=desc`

```xml
type=nt:file
nodename=*.jar
orderby=@jcr:content/jcr:lastModified
orderby.sort=desc
```

### Encontre todas as páginas e ordene-as pela última modificação {#find-all-pages-and-order-them-by-last-modified}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
```

### Encontre todas as páginas e ordene-as pela última modificação, decrescente {#find-all-pages-and-order-them-by-last-modified-but-descending}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&orderby=@jcr:content/cq:lastModified&orderby.sort=desc`

```xml
type=cq:Page
orderby=@jcr:content/cq:lastModified
orderby.sort=desc
```

### Pesquisa de texto completo, Solicitada pela Pontuação {#fulltext-search-ordered-by-score}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Management&orderby=@jcr:score&orderby.sort=desc`

```xml
fulltext=Management
orderby=@jcr:score
orderby.sort=desc
```

### Pesquisar por páginas com uma certa tag {#search-for-pages-tagged-with-a-certain-tag}

`http://<host>:<port>/bin/querybuilder.json?type=cq:Page&tagid=wknd:activity/cycling&tagid.property=jcr:content/cq:tags`

```xml
type=cq:Page
tagid=wknd:activity/cycling
tagid.property=jcr:content/cq:tags
```

Use o predicado `tagid` como no exemplo, se você souber a ID de tag explícita.

Use o predicado `tag` para o caminho do título da tag (sem espaços).

Como, no exemplo anterior, você está procurando por páginas (`cq:Page` nós), é necessário usar o caminho relativo desse nó para o predicado `tagid.property`, que é `jcr:content/cq:tags`. Por padrão, o `tagid.property` seria simplesmente `cq:tags`.

### Pesquisar vários caminhos (usando grupos) {#search-under-multiple-paths-using-groups}

`http://<host>:<port>/bin/querybuilder.json?fulltext=Experience&group.1_path=/content/wknd/us/en/magazine&group.2_path=/content/wknd/us/en/adventures&group.p.or=true`

```xml
fulltext=Experience
group.p.or=true
group.1_path=/content/wknd/us/en/magazine
group.2_path=/content/wknd/us/en/adventures
```

Esse query usa um *grupo* (chamado `group`), que atua para delimitar subexpressões em uma query, assim como os parênteses fazem em notações mais padrão. Por exemplo, a consulta anterior pode ser expressa em um estilo mais familiar como:

`"Experience" and ("/content/wknd/us/en/magazine" or "/content/wknd/us/en/adventures")`

No grupo do exemplo, o predicado `path` é usado várias vezes. Para diferenciar e ordenar as duas instâncias do predicado (a ordenação é necessária para alguns predicados), você deve prefixar os predicados com `N_`, onde `N` é o índice de ordenação. No exemplo anterior, os predicados resultantes são `1_path` e `2_path`.

O `p` em `p.or` é um delimitador especial que indica que o que segue (neste caso, um `or`) é um *parâmetro* do grupo, em vez de um subpredicado do grupo, como `1_path`.

Se nenhum `p.or` for fornecido, todos os predicados serão ANDed em conjunto, ou seja, cada resultado deve satisfazer todos os predicados.

>[!NOTE]
>
>Não é possível usar o mesmo prefixo numérico em uma única consulta, mesmo para predicados diferentes.

### Pesquisar propriedades {#search-for-properties}

Aqui você está procurando por todas as páginas de um determinado modelo, usando a propriedade `cq:template` :

`http://<host>:<port>/bin/querybuilder.json?property=cq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPageContent`

```xml
type=cq:PageContent
property=cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

Isso tem a desvantagem de que os nós `jcr:content` das páginas, não as próprias páginas, são retornados. Para resolver isso, você pode pesquisar por caminho relativo:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3acontent%2fcq%3atemplate&property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&type=cq%3aPage`

```xml
type=cq:Page
property=jcr:content/cq:template
property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
```

### Procurar várias propriedades {#search-for-multiple-properties}

Ao usar o predicado de propriedade várias vezes, é necessário adicionar os prefixos de número novamente:

`http://<host>:<port>/bin/querybuilder.json?1_property=jcr%3acontent%2fcq%3atemplate&1_property.value=%2fconf%2fwknd%2fsettings%2fwcm%2ftemplates%2fadventure-page-template&2_property=jcr%3acontent%2fjcr%3atitle&2_property.value=Cycling%20Tuscany&type=cq%3aPage`

```xml
type=cq:Page
1_property=jcr:content/cq:template
1_property.value=/conf/wknd/settings/wcm/templates/adventure-page-template
2_property=jcr:content/jcr:title
2_property.value=Cycling Tuscany
```

### Procurar vários valores de propriedade {#search-for-multiple-property-values}

Para evitar grandes grupos quando quiser procurar vários valores de uma propriedade (`"A" or "B" or "C"`), você pode fornecer vários valores ao predicado `property`:

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

Para propriedades de vários valores, também é possível exigir que vários valores correspondam a (`"A" and "B" and "C"`):

`http://<host>:<port>/bin/querybuilder.json?property=jcr%3atitle&property.and=true&property.1_value=Cycling%20Tuscany&property.2_value=Ski%20Touring&property.3_value=Whistler%20Mountain%20Biking`

```xml
property=jcr:title
property.and=true
property.1_value=Cycling Tuscany
property.2_value=Ski Touring
property.3_value=Whistler Mountain Biking
```

## Refinando o que é retornado {#refining-what-is-returned}

Por padrão, o Servlet JSON do QueryBuilder retornará um conjunto padrão de propriedades para cada nó no resultado da pesquisa (por exemplo, caminho, nome, título etc.). Para obter controle sobre quais propriedades são retornadas, é possível fazer o seguinte:

Especifique

```xml
p.hits=full
```

nesse caso, todas as propriedades serão incluídas para cada nó:

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
```

Uso

```xml
p.hits=selective
```

e especifique as propriedades que deseja obter

```xml
p.properties
```

separados por um espaço:

`http://<host>:<port>/bin/querybuilder.json?p.hits=selective&p.properties=sling%3aresourceType%20jcr%3aprimaryType&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=selective
p.properties=sling:resourceType jcr:primaryType
```

Outra coisa que você pode fazer é incluir nós filhos na resposta do Query Builder. Para fazer isso, você precisa especificar

```xml
p.nodedepth=n
```

onde `n` é o número de níveis que você deseja que a consulta retorne. Observe que para que um nó filho seja retornado, ele deve ser especificado pelo seletor de propriedades

```xml
p.hits=full
```

Exemplo:

`http://<host>:<port>/bin/querybuilder.json?p.hits=full&p.nodedepth=5&property=jcr%3atitle&property.value=Cycling%20Tuscany`

```xml
property=jcr:title
property.value=Cycling Tuscany
p.hits=full
p.nodedepth=5
```

## Mais Predicados {#morepredicates}

Para obter mais predicados, consulte a página [Referência de predicado do construtor de consultas](query-builder-predicates.md).

Você também pode verificar o [Javadoc para as `PredicateEvaluator` classes](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/PredicateEvaluator.html). O Javadoc para essas classes contém a lista de propriedades que você pode usar.

O prefixo do nome da classe (por exemplo, `similar` em [`SimilarityPredicateEvaluator`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/SimilarityPredicateEvaluator.html)) é a *propriedade principal* da classe. Essa propriedade também é o nome do predicado a ser usado na query (em minúsculas).

Para essas propriedades principais, você pode encurtar a consulta e usar `similar=/content/en` em vez da variante totalmente qualificada `similar.similar=/content/en`. O formulário totalmente qualificado deve ser usado para todas as propriedades não principais de uma classe.

## Exemplo de uso da API do Query Builder {#example-query-builder-api-usage}

```java
   String fulltextSearchTerm = "WKND";

    // create query description as hash map (simplest way, same as form post)
    Map<String, String> map = new HashMap<String, String>();

// create query description as hash map (simplest way, same as form post)
    map.put("path", "/content");
    map.put("type", "cq:Page");
    map.put("group.p.or", "true"); // combine this group with OR
    map.put("group.1_fulltext", fulltextSearchTerm);
    map.put("group.1_fulltext.relPath", "jcr:content");
    map.put("group.2_fulltext", fulltextSearchTerm);
    map.put("group.2_fulltext.relPath", "jcr:content/@cq:tags");

    // can be done in map or with Query methods
    map.put("p.offset", "0"); // same as query.setStart(0) below
    map.put("p.limit", "20"); // same as query.setHitsPerPage(20) below

    Query query = builder.createQuery(PredicateGroup.create(map), session);
    query.setStart(0);
    query.setHitsPerPage(20);

    SearchResult result = query.getResult();

    // paging metadata
    int hitsPerPage = result.getHits().size(); // 20 (set above) or lower
    long totalMatches = result.getTotalMatches();
    long offset = result.getStartIndex();
    long numberOfPages = totalMatches / 20;

    //Place the results in XML to return to client
    DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    Document doc = builder.newDocument();

    //Start building the XML to pass back to the AEM client
    Element root = doc.createElement( "results" );
    doc.appendChild( root );

    // iterating over the results
    for (Hit hit : result.getHits()) {
       String path = hit.getPath();

      //Create a result element
      Element resultel = doc.createElement( "result" );
      root.appendChild( resultel );

      Element pathel = doc.createElement( "path" );
      pathel.appendChild( doc.createTextNode(path ) );
      resultel.appendChild( pathel );
    }
```

O mesmo query executada por HTTP usando o Servlet do Construtor de Consultas (JSON):

`http://<host>:<port>/bin/querybuilder.json?path=/content&type=cq:Page&group.p.or=true&group.1_fulltext=WKND&group.1_fulltext.relPath=jcr:content&group.2_fulltext=WKND&group.2_fulltext.relPath=jcr:content/@cq:tags&p.offset=0&p.limit=20`

## Armazenando e Carregando Consultas {#storing-and-loading-queries}

As consultas podem ser armazenadas no repositório para que você possa usá-las posteriormente. O `QueryBuilder` fornece o método `storeQuery` com a seguinte assinatura:

```java
void storeQuery(Query query, String path, boolean createFile, Session session) throws RepositoryException, IOException;
```

Ao usar o método [`QueryBuilder#storeQuery`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html#storeQuery-com.day.cq.search.Query-java.lang.String-boolean-javax.jcr.Session-), o `Query` especificado é armazenado no repositório como um arquivo ou como uma propriedade de acordo com o valor do argumento `createFile`. O exemplo a seguir mostra como salvar um `Query` no caminho `/mypath/getfiles` como um arquivo:

```java
builder.storeQuery(query, "/mypath/getfiles", true, session);
```

Qualquer query armazenada anteriormente pode ser carregada do repositório usando o método [`QueryBuilder#loadQuery`](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/QueryBuilder.html#loadQuery-java.lang.String-javax.jcr.Session-):

```java
Query loadQuery(String path, Session session) throws RepositoryException, IOException
```

Por exemplo, um `Query` armazenado no caminho `/mypath/getfiles` pode ser carregado pelo seguinte trecho:

```java
Query loadedQuery = builder.loadQuery("/mypath/getfiles", session);
```

## Teste e depuração {#testing-and-debugging}

Para reproduzir e depurar consultas do Query Builder, você pode usar o console do Query Builder em

`http://<host>:<port>/libs/cq/search/content/querydebug.html`

ou, alternativamente, o servlet JSON do Query Builder em

`http://<host>:<port>/bin/querybuilder.json?path=/tmp`

`path=/tmp` é apenas um exemplo.

### Depuração geral do Recommendations {#general-debugging-recommendations}

### Obter XPath Explicável via Registro {#obtain-explain-able-xpath-via-logging}

Explicar **todas as** consultas durante o ciclo de desenvolvimento em relação ao conjunto de índice de destino.

1. Habilite logs DEBUG para o QueryBuilder para obter consulta XPath subjacente explicável
   * Vá até `https://<host>:<port>/system/console/slinglog`. Crie um novo agente de log para `com.day.cq.search.impl.builder.QueryImpl` em **DEBUG**.
1. Depois que DEBUG for ativado para a classe acima, os logs exibirão o XPath gerado pelo Query Builder.
1. Copie a consulta XPath da entrada de log para a consulta do Query Builder associada, Por exemplo:
   * `com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]`
1. Cole a consulta XPath em Explain Query como XPath para obter o plano de consulta.

### Obter XPath explicável por meio do Query Builder Debugger {#obtain-explain-able-xpath-via-the-query-builder-debugger}

Use o AEM Query Builder Debugger para gerar uma consulta XPath explicável.

![Query Builder Debugger](assets/query-builder-debugger.png)

1. Forneça a consulta do Query Builder no depurador do Query Builder
1. Executar a pesquisa
1. Obter o XPath gerado
1. Cole a consulta XPath em Explain Query como XPath para obter o plano de consulta

>[!NOTE]
>
>Consultas que não são do Query Builder (XPath, JCR-SQL2) podem ser fornecidas diretamente para Explicar Consulta.

## Depuração de consultas com registro {#debugging-queries-with-logging}

>[!NOTE]
>
>A configuração dos registradores é descrita no documento [Registro](/help/implementing/developing/introduction/logging.md).

A saída de log (nível INFO) da implementação do construtor de consultas ao executar a consulta descrita na seção anterior [Testes e Depuração:](#testing-and-debugging)

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: limit=20, offset=0[
    {group=group: or=true[
        {1_fulltext=fulltext: fulltext=WKND, relPath=jcr:content}
        {2_fulltext=fulltext: fulltext=WKND, relPath=jcr:content/@cq:tags}
    ]}
    {path=path: path=/content}
    {type=type: type=cq:Page}
]
com.day.cq.search.impl.builder.QueryImpl XPath query: /jcr:root/content//element(*, cq:Page)[(jcr:contains(jcr:content, "WKND") or jcr:contains(jcr:content/@cq:tags, "WKND"))]
com.day.cq.search.impl.builder.QueryImpl no filtering predicates
com.day.cq.search.impl.builder.QueryImpl query execution took 69 ms
```

Se você tiver uma consulta usando avaliadores de predicado que filtram ou usam um pedido personalizado por comparador, isso também será observado na consulta:

```xml
com.day.cq.search.impl.builder.QueryImpl executing query (predicate tree):
null=group: [
    {nodename=nodename: nodename=*.jar}
    {orderby=orderby: orderby=@jcr:content/jcr:lastModified}
    {type=type: type=nt:file}
]
com.day.cq.search.impl.builder.QueryImpl custom order by comparator: jcr:content/jcr:lastModified
com.day.cq.search.impl.builder.QueryImpl XPath query: //element(*, nt:file)
com.day.cq.search.impl.builder.QueryImpl filtering predicates: {nodename=nodename: nodename=*.jar}
com.day.cq.search.impl.builder.QueryImpl query execution took 272 ms
```

## Links Javadoc {#javadoc-links}

| **Javadoc** | **Descrição** |
|---|---|
| [com.day.cq.search](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/package-summary.html) | Query Builder básico e API de consulta |
| [com.day.cq.search.result](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/result/package-summary.html) | API de resultados |
| [com.day.cq.search.facets](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/facets/package-summary.html) | Aspectos |
| [com.day.cq.search.facets.buckets](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/facets/buckets/package-summary.html) | Faixas (contidas em facetas) |
| [com.day.cq.search.eval](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/eval/package-summary.html) | Avaliadores de Predicados |
| [com.day.cq.search.facets.extrators](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/facets/extractors/package-summary.html) | Extratores Facetas (para avaliadores) |
| [com.day.cq.search.writer](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/search/writer/package-summary.html) | Gravador de Ocorrência de Resultado JSON para o servlet do Construtor de Consultas (`/bin/querybuilder.json`) |
