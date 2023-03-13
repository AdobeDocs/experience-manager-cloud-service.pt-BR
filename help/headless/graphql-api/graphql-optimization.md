---
title: Otimização de consultas do GraphQL
description: Saiba como otimizar suas consultas do GraphQL ao filtrar, paginar e classificar os fragmentos de conteúdo no Adobe Experience Manager as a Cloud Service para entrega de conteúdo headless.
source-git-commit: cda6d7e382b090fd726b27e565da08c8b1c80008
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 0%

---


# Otimização de consultas do GraphQL {#optimizing-graphql-queries}

>[!NOTE]
>
>Antes de aplicar essas recomendações de otimização, considere [Atualização dos fragmentos de conteúdo para paginação e classificação na filtragem do GraphQL](/help/headless/graphql-api/graphql-optimized-filtering-content-update.md) para obter o melhor desempenho.

Em uma instância do AEM com um alto número de Fragmentos de conteúdo que compartilham o mesmo modelo, as consultas de lista do GraphQL podem se tornar caras (em termos de recursos).

Isso ocorre porque *all* os fragmentos que compartilham um modelo em uso na consulta do GraphQL devem ser carregados na memória. Isso consome tempo e memória. A filtragem, que pode reduzir o número de itens no conjunto de resultados (final), só pode ser aplicada **após** carregando todo o conjunto de resultados na memória.

Isso pode levar à impressão de que mesmo pequenos conjuntos de resultados (podem) resultam em mau desempenho. No entanto, na realidade, a lentidão é causada pelo tamanho do conjunto de resultados inicial, pois ele deve ser manipulado internamente antes que a filtragem possa ser aplicada.

Para reduzir problemas de desempenho e memória, esse conjunto de resultados inicial deve ser mantido o menor possível.

O AEM fornece duas abordagens para a otimização de consultas do GraphQL:

* [Filtragem híbrida](#hybrid-filtering)
* [Paginação](#paging) (ou paginação)

   * [Classificação](#sorting) não está diretamente relacionado à otimização, mas ao paging

Cada abordagem tem seus próprios casos de uso e limitações. Este documento fornece informações sobre Filtragem e Paginação Híbrida, com algumas [práticas recomendadas](#best-practices) para otimizar consultas do GraphQL.

## Filtragem híbrida {#hybrid-filtering}

A filtragem híbrida combina a filtragem JCR com a filtragem AEM.

Ela aplica um filtro JCR (na forma de uma restrição de consulta) antes de carregar o conjunto de resultados na memória para filtragem por AEM. Isso é para reduzir o conjunto de resultados carregado na memória, pois o filtro JCR remove resultados supérfluos antes disso.

>[!NOTE]
>
>Por motivos técnicos (por exemplo, flexibilidade, aninhamento de fragmentos), o AEM não pode delegar toda a filtragem ao JCR.

Essa técnica mantém a flexibilidade que os filtros do GraphQL fornecem, enquanto delega o máximo possível da filtragem para JCR.

## Paginação {#paging}

O GraphQL no AEM oferece suporte para dois tipos de paginação:

* [paginação baseada em limite/deslocamento](/help/headless/graphql-api/content-fragments.md#list-offset-limit)
Isso é usado para consultas de lista; elas terminam com 
`List`; por exemplo, `articleList`.
Para usá-lo, você deve fornecer a posição do primeiro item a ser retornado (a variável `offset`) e o número de itens a serem retornados (a variável `limit`ou tamanho de página).

* [paginação baseada em cursor](/help/headless/graphql-api/content-fragments.md#paginated-first-after) (representante: `first`e `after`) Fornece uma ID exclusiva para cada item; também conhecido como cursor.
Na query, você especifica o cursor do último item da página anterior, mais o tamanho da página (o número máximo de itens a serem retornados).

   Como a paginação baseada em cursor não se encaixa nas estruturas de dados de consultas baseadas em lista, o AEM introduziu o `Paginated` tipo de consulta; por exemplo, `articlePaginated`. As estruturas de dados e os parâmetros utilizados seguem o [Especificação de conexão do cursor do GraphQL](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >Atualmente, o AEM oferece suporte à paginação de encaminhamento (usando `after`/`first` parâmetros).
   >
   >Paginação retroativa (usando `before`/`last` parâmetros) não são compatíveis.

## Classificação {#sorting}

A classificação só poderá ser eficiente se todos os critérios de classificação estiverem relacionados a fragmentos de nível superior.

Se a ordem de classificação incluir um ou mais campos localizados em um fragmento aninhado, todos os fragmentos que compartilham o modelo de nível superior deverão ser carregados na memória. Isso causa um impacto negativo no desempenho.

>[!NOTE]
>
>A classificação em campos de nível superior também tem um impacto (embora pequeno) no desempenho.

## Práticas recomendadas     {#best-practices}

O principal objetivo de todas as otimizações é reduzir o conjunto de resultados inicial. As práticas recomendadas listadas aqui fornecem maneiras de fazer isso. Eles podem (e devem) ser combinados.

### Filtrar somente nas propriedades de nível superior {#filter-top-level-properties-only}

Atualmente, a filtragem no nível JCR funciona somente para fragmentos de nível superior.

Se um filtro aborda os campos de um fragmento aninhado, o AEM precisa recorrer ao carregamento (na memória) de todos os fragmentos que compartilham o modelo subjacente.

Você ainda pode otimizar essas consultas do GraphQL combinando expressões de filtro em campos de fragmentos de nível superior e aqueles em campos de fragmentos aninhados com o [Operador AND](#logical-operations-in-filter-expressions).

### Usar a estrutura de conteúdo {#use-content-structure}

No AEM, geralmente é considerada uma boa prática usar a estrutura do repositório para restringir o escopo do conteúdo a ser processado.

Essa abordagem também deve ser aplicada a queries do GraphQL.

Isso pode ser feito aplicando um filtro no `_path` campo do fragmento de nível superior:

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>A linha à direita `/` em `value` é necessário para obter o melhor desempenho.

### Usar paginação {#use-paging}

Também é possível usar a paginação para reduzir o conjunto de resultados inicial; especialmente se suas solicitações não usarem filtragem e classificação.

Se você filtrar ou classificar fragmentos aninhados, as consultas paginadas ainda poderão ficar lentas, pois o AEM ainda poderá precisar carregar quantidades maiores de fragmentos na memória. Portanto, se você combinar a filtragem e a paginação, considere as regras de filtragem (como mencionado acima).

Para a paginação, a classificação é igualmente importante, pois os resultados paginados são sempre classificados - de forma explícita ou implícita.

Se você estiver interessado principalmente em recuperar apenas as primeiras páginas, não há diferença significativa entre o uso da variável `...List` ou `...Paginated` consultas. No entanto, se o aplicativo estiver interessado em ler mais de uma ou duas páginas, considere `...Paginated` consulta, pois tem um desempenho notavelmente melhor com as páginas posteriores.

### Operações lógicas em expressões de filtro {#logical-operations-in-filter-expressions}

Se estiver filtrando em fragmentos aninhados, você ainda poderá aproveitar a filtragem JCR fornecendo um filtro de acompanhamento em um campo de nível superior combinado usando o `AND` operador.

Um caso de uso típico seria restringir o escopo da consulta usando um filtro no `_path` do fragmento de nível superior e filtre por campos adicionais que podem estar no nível superior ou em um fragmento aninhado.

Nesse caso, as diferentes expressões de filtro seriam combinadas com `AND`. Portanto, o filtro ativado `_path` pode limitar efetivamente o conjunto de resultados inicial. Todos os outros filtros em campos de nível superior também podem ajudar a reduzir o conjunto de resultados inicial, desde que sejam combinados com `AND`.

Expressões de filtro combinadas com `OR` não pode ser otimizado se fragmentos aninhados estiverem envolvidos. `OR` expressões só podem ser otimizadas se *não* fragmentos aninhados estão envolvidos.

### Evitar filtrar em campos de texto multilinha {#avoid-filtering-multiline-textfields}

Os campos de um campo de texto multilinha (html, markdown, texto simples, json) não podem ser filtrados por uma consulta JCR, pois o conteúdo desses campos deve ser calculado dinamicamente.

Se ainda precisar filtrar em um campo de texto de várias linhas, considere limitar o tamanho do conjunto de resultados inicial adicionando expressões de filtro adicionais e combinando-as com `AND`. Limitar o escopo por meio da filtragem no `_path` é uma boa abordagem também.

### Evitar filtragem em campos virtuais {#avoid-filtering-virtual-fields}

Campos virtuais (a maioria dos campos começa com `_`) são calculados enquanto uma consulta GraphQL é executada e, portanto, estão fora do escopo da filtragem baseada em JCR.

Uma exceção importante é a `_path` que pode ser usado efetivamente para reduzir o tamanho do conjunto de resultados inicial - se o conteúdo for estruturado de acordo (consulte [Usar a estrutura de conteúdo](#use-content-structure)).

### Filtragem: exclusões {#filtering-exclusions}

Há várias outras situações em que uma expressão de filtro não pode ser avaliada no nível JCR (e, portanto, deve ser evitada para alcançar o melhor desempenho):

* Filtrar expressões em um `Float` valor que usa o `_sensitiveness` opção de filtro e onde `_sensitiveness` está definido como qualquer coisa diferente de `0.0` .

* Filtrar expressões em um `String` usando o `_ignoreCase` opção de filtro.

* Filtragem ativada `null` valores.

* Filtros em arrays com `_apply: ALL_OR_EMPTY`.

* Filtros em arrays com `_apply: INSTANCES`, `_instances: 0`.

* Filtrar expressões usando o `CONTAINS_NOT` operador.

* Filtrar expressões em um `Calendar`, `Date` ou `Time` valor que usa o `NOT_AT` operador.
