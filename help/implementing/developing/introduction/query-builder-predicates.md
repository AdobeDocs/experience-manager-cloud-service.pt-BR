---
title: Referência de predicado do construtor de consultas
description: Referência de predicado para a API do Construtor de consultas no AEM as a Cloud Service.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2270'
ht-degree: 1%

---

# Referência de predicado do construtor de consultas {#query-builder-predicate-reference}

## Geral {#general}

### raiz {#root}

O grupo de predicados raiz. Suporta todos os recursos de um grupo e permite a definição de parâmetros de consulta globais.

O nome &quot;raiz&quot; nunca é usado em uma consulta; ele está implícito.

#### Propriedades {#properties-18}

* **`p.offset`** - número que indica o início da página de resultados, ou seja, quantos itens devem ser ignorados.
* **`p.limit`** - número indicando o tamanho da página.
* **`p.guessTotal`** - recomendado: evite calcular o total do resultado completo, que pode ser caro. Um número que indica o total máximo para contar até (por exemplo, 1000, um número que fornece aos usuários feedback suficiente sobre o tamanho bruto e números exatos para resultados menores). Ou `true` para contar somente até o mínimo necessário `p.offset` + `p.limit`.
* **`p.excerpt`** - se definido como `true`, incluir trecho de texto completo no resultado.
* **`p.indexTag`** - se definido, incluirá uma opção de marca de índice na consulta (consulte [Marca de Índice de Opção de Consulta](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-option-index-tag)).
* **`p.facetStrategy`** - se definido como `oak`, o Construtor de Consultas delegará a extração de facetas à Oak (consulte [Facetas](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#facets)).
* **`p.hits`** - (somente para o servlet JSON) selecione a forma como as ocorrências são gravadas como JSON, com essas ocorrências padrão (extensíveis por meio do serviço ResultHitWriter).
   * **`simple`** - itens mínimos como `path`, `title`, `lastmodified`, `excerpt` (se definido).
   * **`full`** - sling JSON rendering do nó, com `jcr:path` indicando o caminho da ocorrência. Por padrão, apenas lista as propriedades diretas do nó, inclui uma árvore mais profunda com `p.nodedepth=N`, com 0 significando a subárvore inteira e infinita. Adicione `p.acls=true` para incluir as permissões JCR da sessão atual no item de resultado fornecido (mapeamentos: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).
   * **`selective`** - somente propriedades especificadas em `p.properties`, que é uma lista de caminhos relativos separada por espaços (use `+` em URLs). Se o caminho relativo tiver uma profundidade `>1`, essas propriedades serão representadas como objetos filho. A propriedade especial `jcr:path` inclui o caminho da ocorrência.

### grupo {#group}

Esse predicado permite criar condições aninhadas. Os grupos podem conter grupos aninhados. Tudo em uma consulta do Construtor de Consultas está implicitamente em um grupo raiz, que também pode ter `p.or` e `p.not` parâmetros.

Este é um exemplo para corresponder uma das duas propriedades a um valor:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Conceitualmente, é `(1_property` OR `2_property)`.

Veja a seguir um exemplo de grupos aninhados:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Pesquisa o termo **Gerenciamento** nas páginas em `/content/wknd/ch/de` ou nos ativos em `/content/dam/wknd`.

Conceitualmente, é `fulltext AND ( (path AND type) OR (path AND type) )`. Essas associações OR precisam de bons índices por motivos de desempenho.

#### Propriedades {#properties-6}

* **`p.or`** - se definido como `true`, somente um predicado no grupo deve corresponder. O padrão é `false`, o que significa que todos devem corresponder
* **`p.not`** - se definido como `true`, nega o grupo (o padrão é `false`)
* **`<predicate>`** - adiciona predicados aninhados
* **`N_<predicate>`** - adiciona vários predicados aninhados ao mesmo tempo, como `1_property, 2_property, ...`

### orderby {#orderby}

Este predicado permite classificar os resultados. Se a ordenação por várias propriedades for necessária, esse predicado deverá ser adicionado várias vezes usando o prefixo numérico, como `1_orderby=first`, `2_oderby=second`.

#### Propriedades {#properties-13}

* **`orderby`** - nome de propriedade JCR indicado por um @ à esquerda, por exemplo, `@jcr:lastModified` ou `@jcr:content/jcr:title`, ou outro predicado na consulta, por exemplo, `2_property`, no qual classificar
* **`sort`** - direção de classificação, `desc` para decrescente ou `asc` para crescente (padrão)
* **`case`** - se definido como `ignore`, ele faz com que a classificação diferencie maiúsculas de minúsculas, o que significa que `a` vem antes de `B`; se estiver vazio ou for deixado de fora, a classificação diferencia maiúsculas de minúsculas, o que significa que `B` vem antes de `a`

## Predicados {#predicates}

### boolproperty {#boolproperty}

Este predicado corresponde às propriedades booleanas do JCR. Aceita apenas os valores `true` e `false`. Se o valor for `false`, ele corresponderá se a propriedade tiver o valor `false` ou se ela não existir. Esse predicado é útil para verificar se há sinalizadores booleanos que só são definidos quando ativados.

O parâmetro `operation` herdado não tem significado.

Este predicado oferece suporte para a extração de facetas e fornece compartimentos para cada valor `true` ou `false`, mas somente para propriedades existentes.

#### Propriedades {#properties}

* **`boolproperty`** - caminho relativo para a propriedade, por exemplo, `myFeatureEnabled` ou `jcr:content/myFeatureEnabled`
* **`value`** - valor para verificar a propriedade, `true` ou `false`

### contentfragment {#contentfragment}

Esse predicado restringe o resultado aos fragmentos de conteúdo.

* Ela não oferece suporte à filtragem.
* Não há suporte para extração de facetas.

#### Propriedades {#properties-1}

* **`contentfragment`** - Pode ser usado com qualquer valor para verificar fragmentos de conteúdo.

### `dateComparison` {#datecomparison}

Esse predicado compara duas propriedades de data JCR entre si. É possível testar se eles são iguais, desiguais, maiores ou maiores ou iguais.

Um predicado somente de filtragem e não pode usar um índice de pesquisa.

#### Propriedades {#properties-2}

* **`property1`** - caminho para a propriedade da primeira data
* **`property2`** - caminho para a segunda propriedade de data
* **`operation`**
   * `=` para correspondência exata (padrão)
   * `!=` para comparação de desigualdade
   * `>` para `property1` maior que `property2`
   * `>=` para `property1` maior ou igual a `property2`

### intervalo de datas {#daterange}

Esse predicado corresponde às propriedades de data do JCR em relação a um intervalo de data/hora. Usa o ISO8601
formato para datas e horas (`YYYY-MM-DDTHH:mm:ss.SSSZ`) e também permite representações parciais, como `YYYY-MM-DD`. Como alternativa, o carimbo de data e hora pode ser fornecido como hora POSIX.

Você pode procurar qualquer item entre dois carimbos de data e hora, qualquer item mais recente ou mais antigo que uma determinada data, e também escolher entre intervalos inclusivos e abertos.

Ela oferece suporte à extração de facetas e fornece compartimentos `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year` e `earlier than last year`.

Ela não oferece suporte à filtragem.

#### Propriedades {#properties-3}

* **`property`** - caminho relativo para uma propriedade `DATE`, por exemplo, `jcr:lastModified`
* **`lowerBound`** - data mais baixa associada à verificação da propriedade, por exemplo, `2014-10-01`
* **`lowerOperation`** - `>` (mais recente) ou `>=` (em ou mais recente), aplica-se a `lowerBound`. O padrão é `>`
* **`upperBound`** - limite superior para verificar a propriedade, por exemplo, `2014-10-01T12:15:00`
* **`upperOperation`** - `<` (mais antigo) ou `<=` (mais antigo), aplica-se a `upperBound`. O padrão é `<`
* **`timeZone`** - ID de fuso horário a ser usada quando não for fornecida como uma cadeia de caracteres de data ISO-8601. O padrão é o fuso horário padrão do sistema.

### excludepaths {#excludepaths}

Esse predicado exclui nós do resultado em que seu caminho corresponde a uma expressão regular.

Um predicado somente de filtragem e não pode usar um índice de pesquisa.

Não há suporte para extração de facetas.

#### Propriedades {#properties-4}

* **`excludepaths`** - expressão regular correspondente em caminhos de resultados, excluindo os correspondentes do resultado.

### texto completo {#fulltext}

Pesquisa por termos no índice de texto completo.

Ela não oferece suporte à filtragem.

Não há suporte para extração de facetas.

#### Propriedades {#properties-5}

* **`fulltext`** - os termos de pesquisa de texto completo
* **`relPath`** - o caminho relativo a ser pesquisado na propriedade ou no subnó. Essa propriedade é opcional.

### hasPermission {#haspermission}

Este predicado restringe o resultado a itens nos quais a sessão atual tem os [privilégios JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges) especificados.

Um predicado somente de filtragem e não pode usar um índice de pesquisa. Não há suporte para extração de facetas.

#### Propriedades {#properties-7}

* **`hasPermission`** - todos os privilégios JCR separados por vírgulas que a sessão do usuário atual deve ter para o nó em questão. Por exemplo, `jcr:write`, `jcr:modifyAccessControl`

### idioma {#language}

Esse predicado encontra páginas do AEM em um idioma específico. Ela verifica a propriedade de idioma da página e o caminho da página, que geralmente inclui o idioma ou o local em uma estrutura de site de nível superior.

Um predicado somente de filtragem e não pode usar um índice de pesquisa.

Ela oferece suporte à extração de facetas e a intervalos para cada código de idioma exclusivo.

#### Propriedades {#properties-8}

* **`language`** - código de idioma ISO, por exemplo, `de`

### principal ativo {#mainasset}

Esse predicado verifica se um nó é um ativo principal do DAM e não um subativo. Basicamente, cada nó não está dentro de um nó sub assets. Ele não verifica o tipo de nó `dam:Asset`. Para usar este predicado, defina `mainasset=true` ou `mainasset=false`. Não há mais propriedades.

Um predicado somente de filtragem e não pode usar um índice de pesquisa.

Ela oferece suporte à extração de facetas e fornece dois buckets para ativos principais e secundários.

#### Propriedades {#properties-9}

* **`mainasset`** - booleano, `true` para ativos principais, `false` para subativos

### memberOf {#memberof}

Este predicado encontra itens que são membros de uma [coleção de recursos de sling](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html) específica.

Um predicado somente de filtragem e não pode usar um índice de pesquisa.

Não há suporte para extração de facetas.

#### Propriedades {#properties-10}

* **`memberOf`** - caminho da coleção de recursos do Sling

### nodename {#nodename}

Esse predicado corresponde aos nomes de nó do JCR.

Ela oferece suporte à extração de facetas e buckets para cada nome de nó único (nome de arquivo).

#### Propriedades {#properties-11}

* **`nodename`** - padrão de nome de nó que permite curingas: `*` = qualquer caractere ou nenhum caractere, `?` = qualquer caractere, `[abc]` = somente caracteres entre colchetes

### não expirado {#notexpired}

Esse predicado corresponde a itens, verificando se uma propriedade de data JCR é maior ou igual à hora atual do servidor. Ela pode ser usada para verificar um valor `expiresAt` e limita os resultados apenas aos valores que ainda não expiraram (`notexpired=true`) ou que já expiraram (`notexpired=false`).

Ela não oferece suporte à filtragem.

Ela suporta a extração de facetas da mesma forma que o predicado [`daterange`](#daterange).

#### Propriedades {#properties-12}

* **`notexpired`** - booleano, `true` para ainda não expirado (data futura ou igual), `false` para expirado (data no passado) (obrigatório)
* **`property`** - caminho relativo para a propriedade `DATE` a ser verificada (obrigatório)

### caminho {#path}

Esse predicado pesquisa em um determinado caminho.

Não há suporte para extração de facetas.

#### Propriedades {#properties-14}

* **`path`** - Define o padrão do caminho.
   * Dependendo da propriedade `exact`, a subárvore inteira corresponde (como ao anexar `//*` em xpath, mas observe que ela não inclui o caminho base), ou apenas um caminho exato corresponde, o que pode incluir curingas (`*`).
      * O padrão é `true`.
&lt;!—   * Se a propriedade `self` for definida, a subárvore inteira, incluindo o nó base, será pesquisada.—>
* **`exact`** - se `exact` for `true`, o caminho exato deve corresponder, mas pode conter curingas simples (`*`), que correspondem a nomes, mas não `/`; se for `false` (padrão), todos os descendentes serão incluídos (opcional).
* **`flat`** - pesquisa somente os filhos diretos (como anexar `/*` em xpath) (usado somente se `exact` não for verdadeiro, opcional).
* **`self`** - pesquisa a subárvore, mas inclui o nó base fornecido como caminho (sem curingas).
   * *Observação importante*: um problema foi identificado com a propriedade `self` na implementação atual do construtor de consultas e usá-lo em consultas pode não produzir resultados de pesquisa corretos. Não é possível alterar a implementação atual da propriedade `self` porque isso pode interromper os aplicativos existentes que dependem dela. Devido a esta funcionalidade, a propriedade `self` foi preterida; é recomendável evitar sua utilização.

### propriedade {#property}

Esse predicado corresponde às propriedades do JCR e seus valores.

Ela oferece suporte à extração de facetas e fornece compartimentos para cada valor de propriedade exclusivo nos resultados.

#### Propriedades {#properties-15}

* **`property`** - caminho relativo para a propriedade, por exemplo, `jcr:title`.
* **`value`** - valor para verificar a propriedade; segue o tipo de propriedade JCR para conversões de cadeia de caracteres.
* **`N_value`** - use `1_value`, `2_value`, ... para verificar se há vários valores (combinados com `OR` por padrão, com `AND`, se `and=true`).
* **`and`** - definido como `true` para combinar vários valores (`N_value`) com `AND`
* **`operation`**
   * `equals` para correspondência exata (padrão).
   * `unequals` para comparação de desigualdade.
   * `like` por usar a função xpath `jcr:like` (opcional).
   * `not` para nenhuma correspondência (por exemplo, `not(@prop)` em xpath, o parâmetro do valor é ignorado).
   * `exists` para verificação de existência.
      * `true` a propriedade deve existir.
      * `false` é o mesmo que `not` e é o padrão.
* **`depth`** - número de níveis curingas abaixo dos quais a propriedade/caminho relativo pode existir (por exemplo, `property=size depth=2` verifica `node/size`, `node/*/size` e `node/*/*/size`).

### rangeproperty {#rangeproperty}

Este predicado corresponde a uma propriedade JCR em relação a um intervalo. Aplica-se a propriedades com tipos lineares como `LONG`, `DOUBLE` e `DECIMAL`. Para `DATE`, consulte o predicado [`daterange`](#daterange) que otimizou a entrada de formato de data.

Você pode definir um limite inferior, um limite superior ou ambos. A operação (por exemplo, menor que ou menor que ou igual a) também pode ser especificada para limites inferior e superior individualmente.

Não há suporte para extração de facetas.

#### Propriedades {#properties-16}

* **`property`** - caminho relativo para a propriedade
* **`lowerBound`** - limite inferior para verificar propriedade
* **`lowerOperation`** - `>` (padrão) ou `>=`, aplica-se a `lowerValue`
* **`upperBound`** - limite superior para verificar propriedade
* **`upperOperation`** - `<` (padrão) ou `<=`, aplica-se a `lowerValue`
* **`decimal`** - `true` se a propriedade marcada for do tipo Decimal

### relativedaterange {#relativedaterange}

Este predicado corresponde às propriedades `JCR DATE` em um intervalo de data/hora usando deslocamentos de tempo relativos à hora atual do servidor. Você pode especificar `lowerBound` e `upperBound` usando um valor de milissegundo ou a sintaxe Bugzilla `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos). Prefixe com `-` para indicar um deslocamento negativo antes da hora atual. Se você especificar apenas `lowerBound` ou `upperBound`, o padrão é `0`, representando a hora atual.

Por exemplo:

* `upperBound=1h` (e nenhum `lowerBound`) seleciona nada na próxima hora
* `lowerBound=-1d` (e nenhum `upperBound`) seleciona nada nas últimas 24 horas
* `lowerBound=-6M` e `upperBound=-3M` selecionam qualquer item nos últimos 3 a 6 meses
* `lowerBound=-1500` e `upperBound=5500` selecionam algo entre 1500 milissegundos de idade e 5500 milissegundos no futuro
* `lowerBound=1d` e `upperBound=2d` selecionam qualquer coisa depois de amanhã

Ele não leva anos bissextos em consideração e todos os meses são 30 dias.

Ela não oferece suporte à filtragem.

Ela suporta a extração de facetas da mesma forma que o predicado [`daterange`](#daterange).

#### Propriedades {#properties-17}

* **`upperBound`** - data máxima associada em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) relativa à hora atual do servidor. Use `-` para deslocamento negativo
* **`lowerBound`** - data mais baixa associada em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) relativa à hora atual do servidor. Use `-` para deslocamento negativo

### savedquery {#savedquery}

Esse predicado inclui todos os predicados de uma consulta persistente do Construtor de consultas na consulta atual como um predicado de subgrupo.

Ela não executa uma consulta extra, mas estende a consulta atual.

As consultas podem ser persistidas de forma programática usando `QueryBuilder#storeQuery()`. O formato pode ser uma propriedade de várias linhas `String` ou um nó `nt:file` que contém a consulta como um arquivo de texto no formato de propriedades Java™.

Não há suporte para extração de facetas para os predicados da consulta salva.

#### Propriedades {#properties-19}

* **`savedquery`** - caminho para a consulta salva (propriedade `String` ou nó `nt:file`)

### semelhante {#similar}

Este predicado é uma pesquisa de similaridade usando JCR XPath&#39;s `rep:similar()`.

Ela não oferece suporte à filtragem e à extração de facetas.

#### Propriedades {#properties-20}

* **`similar`** - caminho absoluto para o nó para o qual serão localizados nós semelhantes
* **`local`** - um caminho relativo para um nó descendente ou `.` para o nó atual (opcional, o padrão é `.`)

### tag {#tag}

Esse predicado pesquisa por conteúdo marcado com uma ou mais tags, especificando caminhos de título de tag.

Ele oferece suporte à extração de facetas e fornece compartimentos para cada tag exclusiva, usando o caminho do título da tag atual.

#### Propriedades {#properties-21}

* **`tag`** - caminho do título da marca a ser procurado, por exemplo, `properties:orientation/landscape`
* **`N_value`** - use `1_value`, `2_value`, ... para verificar várias marcas (combinadas com `OR` por padrão, com `AND` se `and=true`)
* **`property`** - propriedade (ou caminho relativo para a propriedade) a ser examinada (padrão `cq:tags`)

### tagid {#tagid}

Esse predicado pesquisa por conteúdo marcado com uma ou mais tags, especificando IDs de tag.

Ela é compatível com a extração de facetas e fornece compartimentos para cada tag exclusiva, usando a ID de tag atual.

#### Propriedades {#properties-22}

* **`tagid`** - ID da marca a ser procurada, por exemplo, `properties:orientation/landscape`
* **`N_value`** - use `1_value`, `2_value`, ... para verificar várias IDs de marcas (combinadas com `OR` por padrão, com `AND` se `and=true`)
* **`property`** - propriedade (ou caminho relativo para a propriedade) a ser examinada (padrão `cq:tags`)

### tagsearch {#tagsearch}

Esse predicado pesquisa por conteúdo marcado com uma ou mais tags, especificando palavras-chave. Ela procura primeiro por tags contendo essas palavras-chave em seus títulos e, em seguida, restringe o resultado a apenas itens marcados com essas palavras-chave.

Não há suporte para extração de facetas.

#### Propriedades {#Properties-1}

* **`tagsearch`** - palavra-chave a ser procurada em títulos de marcas
* **`property`** - propriedade (ou caminho relativo para propriedade) a ser considerada (padrão `cq:tags`)
* **`lang`** - para pesquisar apenas um determinado título de marca localizado (por exemplo, `de`)
* **`all`** - valor booleano para pesquisar todo o texto completo da marca, ou seja, todos os títulos, descrições e assim por diante (tem precedência sobre `lang`)

### tipo {#type}

Esse predicado restringe os resultados a um tipo de nó JCR específico, tanto tipos de nó primário quanto `mixin` tipos. Ele também encontra subtipos desse tipo de nó. Os índices de pesquisa do repositório devem abranger os tipos de nó para uma execução eficiente.

Ela suporta a extração de facetas e fornece intervalos para cada tipo único nos resultados.

#### Propriedades {#Properties-2}

* **`type`** - tipo de nó ou nome `mixin` para procurar, por exemplo, `cq:Page`
