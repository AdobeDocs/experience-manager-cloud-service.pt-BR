---
title: Referência de predicado do construtor de consultas
description: Referência de predicado para a API do Construtor de consultas.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 2%

---

# Referência de predicado do construtor de consultas {#query-builder-predicate-reference}

## Geral {#general}

### root {#root}

Este é o grupo de predicado raiz. Ele suporta todos os recursos de um grupo e permite definir parâmetros de consulta global.

O nome &quot;raiz&quot; nunca é usado em um query, está implícito.

#### Propriedades {#properties-18}

* **`p.offset`** - número que indica o início da página de resultados, ou seja, quantos itens devem ser ignorados
* **`p.limit`** - número que indica o tamanho da página
* **`p.guessTotal`** - recomendado: evitar calcular o total dos resultados que podem ser onerosos; um número que indica o total máximo para contar até (por exemplo, 1000, um número que dá aos usuários feedback suficiente sobre o tamanho bruto e números exatos para resultados menores) ou `true` para contar somente até o mínimo necessário `p.offset` + `p.limit`
* **`p.excerpt`** - se definido como `true`, inclua o trecho de texto completo no resultado
* **`p.hits`** - (somente para o servlet JSON) selecione a maneira como as ocorrências são gravadas como JSON, com essas ocorrências padrão (extensíveis por meio do serviço ResultHitWriter):
   * **`simple`** - itens mínimos como `path`, `title`, `lastmodified`, `excerpt` (se definido)
   * **`full`** - sling JSON rendering do nó, com `jcr:path` indicando o caminho da ocorrência: por padrão, apenas lista as propriedades diretas do nó, e inclui uma árvore mais profunda com `p.nodedepth=N`, com 0 significando a subárvore inteira e infinita; adicionar `p.acls=true` para incluir as permissões JCR da sessão atual no item de resultado fornecido (mapeamentos: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)
   * **`selective`** - somente as propriedades especificadas em `p.properties`, que é um espaço separado (use `+` em URLs) lista de caminhos relativos; se o caminho relativo tiver uma profundidade `>1` estes serão representados como objetos filhos; o especial `jcr:path` inclui o caminho da ocorrência

### grupo {#group}

Esse predicado permite construir condições aninhadas. Os grupos podem conter grupos aninhados. Tudo em um query do Query Builder está implicitamente em um grupo raiz, que pode ter `p.or` e `p.not` também.

Este é um exemplo de correspondência de uma de duas propriedades com um valor:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Conceitualmente `(1_property` OU `2_property)`.

Este é um exemplo de grupos aninhados:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Isso busca o termo **Gerenciamento** nas páginas em `/content/wknd/ch/de` ou em ativos em `/content/dam/wknd`.

Conceitualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Esteja ciente de que tais junções OU precisam de bons índices por motivos de desempenho.

#### Propriedades {#properties-6}

* **`p.or`** - se definido como `true`, somente um predicado no grupo deve corresponder. O padrão é `false`, o que significa que tudo deve corresponder
* **`p.not`** - se definido como `true`, nega o grupo (o padrão é `false`)
* **`<predicate>`** - adiciona predicados aninhados
* **`N_<predicate>`** - adiciona vários predicados aninhados ao mesmo tempo, como `1_property, 2_property, ...`

### orderby {#orderby}

Esse predicado permite classificar os resultados. Se for necessário solicitar por várias propriedades, esse predicado precisará ser adicionado várias vezes usando o prefixo número, como `1_orderby=first`, `2_oderby=second`.

#### Propriedades {#properties-13}

* **`orderby`** - o nome da propriedade JCR indicado por um @ à esquerda, por exemplo `@jcr:lastModified` ou `@jcr:content/jcr:title`, ou outro predicado na consulta, por exemplo `2_property`, sobre o qual classificar
* **`sort`** - a direção de ordenação, ou `desc` para descendentes ou `asc` para ascendente (padrão)
* **`case`** - se definido como `ignore` não diferenciará maiúsculas de minúsculas, o que significa `a` comes before `B`; se estiver vazio ou deixado de fora, a classificação diferencia maiúsculas de minúsculas, o que significa `B` comes before `a`

## Predicados {#predicates}

### boolproperty {#boolproperty}

Esse predicado corresponde nas propriedades booleanas do JCR. Aceita apenas os valores `true` e `false`. No caso de `false`, corresponderá se a propriedade tiver o valor `false` ou se não existir. Isso pode ser útil para verificar sinalizadores booleanos que são definidos somente quando ativados.

O herdado `operation` não tem significado.

Esse predicado suporta extração de facetas e fornece compartimentos para cada `true` ou `false` , mas somente para propriedades existentes.

#### Propriedades {#properties}

* **`boolproperty`** - caminho relativo para a propriedade, por exemplo `myFeatureEnabled` ou `jcr:content/myFeatureEnabled`
* **`value`** - valor para verificar a propriedade, `true` ou `false`

### contentfragment {#contentfragment}

Esse predicado restringe o resultado a fragmentos de conteúdo.

* Não é compatível com a filtragem.
* Ele não oferece suporte à extração de facetas.

#### Propriedades {#properties-1}

* **`contentfragment`** - Ele pode ser usado com qualquer valor para verificar fragmentos de conteúdo.

### `dateComparison` {#datecomparison}

Esse predicado compara duas propriedades de data JCR entre si. Pode testar se são iguais, desiguais, maiores ou maiores que ou iguais.

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa.

#### Propriedades {#properties-2}

* **`property1`** - propriedade path to first date
* **`property2`** - caminho para a segunda propriedade de data
* **`operation`**
   * `=` para correspondência exata (padrão)
   * `!=` para comparação de desigualdade
   * `>` para `property1` maior que `property2`
   * `>=` para `property1` maior que ou igual a `property2`

### daterange {#daterange}

Esse predicado corresponde às propriedades de data do JCR em relação a um intervalo de data/hora. Ele usa o formato ISO8601 para datas e horas (`YYYY-MM-DDTHH:mm:ss.SSSZ`) e também permite representações parciais, como `YYYY-MM-DD`. Como alternativa, o carimbo de data e hora pode ser fornecido como hora POSIX.

Você pode procurar qualquer valor entre dois carimbos de data e hora, qualquer valor mais recente ou mais antigo que uma determinada data e também escolher entre intervalos inclusivos e abertos.

Ele suporta extração de facetas e fornece buckets `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year`e `earlier than last year`.

Não é compatível com a filtragem.

#### Propriedades {#properties-3}

* **`property`** - caminho relativo para um `DATE` propriedade , por exemplo `jcr:lastModified`
* **`lowerBound`** - limite de data inferior vinculado para verificar a propriedade, por exemplo, `2014-10-01`
* **`lowerOperation`** - `>` (mais recente) ou `>=` (em ou mais recente), aplica-se à variável `lowerBound`. O padrão é `>`
* **`upperBound`** - limite superior para verificar a propriedade, por exemplo, `2014-10-01T12:15:00`
* **`upperOperation`** - `<` (mais antigo) ou `<=` (em ou mais), aplica-se à variável `upperBound`. O padrão é `<`
* **`timeZone`** - ID do fuso horário a ser usado quando não for fornecido como uma string de data ISO-8601. O padrão é o fuso horário padrão do sistema.

### excludepaths {#excludepaths}

Esse predicado exclui nós do resultado, onde seu caminho corresponde a uma expressão regular.

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa.

Ele não oferece suporte à extração de facetas.

#### Propriedades {#properties-4}

* **`excludepaths`** - a expressão regular corresponde aos caminhos de resultado, excluindo os correspondentes do resultado.

### texto completo {#fulltext}

Esse predicado pesquisa termos no índice de texto completo.

Não é compatível com a filtragem.

Ele não oferece suporte à extração de facetas.

#### Propriedades {#properties-5}

* **`fulltext`** - o(s) termo(s) de pesquisa de texto completo
* **`relPath`** - o caminho relativo a ser pesquisado na propriedade ou no subnó . Essa propriedade é opcional.

### hasPermission {#haspermission}

Esse predicado restringe o resultado a itens em que a sessão atual tem o especificado [Privilégios JCR.](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa. Ele não oferece suporte à extração de facetas.

#### Propriedades {#properties-7}

* **`hasPermission`** - privilégios JCR separados por vírgulas que a sessão do usuário atual TODOS devem ter para o nó em questão; por exemplo `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Este predicado encontra AEM páginas em um idioma específico. Isso observa a propriedade de idioma da página e o caminho da página que geralmente inclui o idioma ou o local em uma estrutura de site de nível superior.

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa.

Ele suporta extração de facetas e fornece compartimentos para cada código de idioma exclusivo.

#### Propriedades {#properties-8}

* **`language`** - código de idioma ISO, por exemplo `de`

### ativo principal {#mainasset}

Esse predicado verifica se um nó é um ativo principal do DAM e não um subativo. Basicamente, todos os nós não dentro de um nó de sub-ativos. Observe que isso não verifica a variável `dam:Asset` tipo de nó. Para usar esse predicado, basta definir `mainasset=true` ou `mainasset=false`. Não há mais propriedades.

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa.

Ele suporta extração de facetas e fornece dois buckets para os ativos principal e secundário.

#### Propriedades {#properties-9}

* **`mainasset`** - booleano, `true` para os principais ativos, `false` para subativos

### memberOf {#memberof}

Este predicado encontra itens que são membros de um [coleção de recursos sling](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa.

Ele não oferece suporte à extração de facetas.

#### Propriedades {#properties-10}

* **`memberOf`** - caminho da coleção de recursos do Sling

### nodename {#nodename}

Esse predicado corresponde aos nomes do nó JCR.

Ele suporta extração de facetas e fornece buckets para cada nome de nó exclusivo (nome de arquivo).

#### Propriedades {#properties-11}

* **`nodename`** - padrão de nome de nó que permite curingas: `*` = qualquer ou nenhum caractere, `?` = qualquer caractere, `[abc]` = somente caracteres entre colchetes

### não textuoso {#notexpired}

Esse predicado corresponde itens verificando se uma propriedade de data JCR é maior ou igual à hora atual do servidor. Isso pode ser usado para verificar uma `expiresAt` limite os resultados somente àqueles que ainda não expiraram (`notexpired=true`) ou que já expiraram (`notexpired=false`).

Não é compatível com a filtragem.

Ele oferece suporte à extração de facetas da mesma forma que a variável [`daterange`](#daterange) predicado.

#### Propriedades {#properties-12}

* **`notexpired`** - booleano, `true` para ainda não expirado (data futura ou igual), `false` expirado (data anterior) (obrigatório)
* **`property`** - caminho relativo para a `DATE` propriedade a ser verificada (obrigatório)

### path {#path}

Esse predicado pesquisa dentro de um determinado caminho.

Ele não oferece suporte à extração de facetas.

#### Propriedades {#properties-14}

* **`path`** - Isso define o padrão de caminho.
   * Dependendo do `exact` , a subárvore inteira corresponderá (como anexar) `//*` no xpath, mas observe que isso não inclui o caminho base) ou apenas uma correspondência exata de caminho, que pode incluir curingas (`*`).
      * O padrão é `true`
   * Se a variável `self`for definida, a subárvore inteira, incluindo o nó base, será pesquisada.
* **`exact`** - se `exact` é `true`, o caminho exato deve corresponder, mas pode conter curingas simples (`*`), que correspondem aos nomes, mas não `/`; se for `false` (padrão) todos os descendentes são incluídos (opcional)
* **`flat`** - pesquisa apenas os filhos diretos (como anexar `/*` em xpath) (usado somente se `exact` não é verdadeiro, opcional)
* **`self`** - pesquisa a subárvore, mas inclui o nó base fornecido como caminho (sem curingas)

### propriedade {#property}

Esse predicado corresponde às propriedades do JCR e seus valores.

Ele suporta extração de facetas e fornece buckets para cada valor de propriedade exclusivo nos resultados.

#### Propriedades {#properties-15}

* **`property`** - caminho relativo para a propriedade, por exemplo `jcr:title`
* **`value`** - valor para verificar a propriedade; segue o tipo de propriedade JCR para conversões de string
* **`N_value`** - utilização `1_value`, `2_value`, ... para verificar vários valores (combinados com `OR` por padrão, com `AND` if `and=true`)
* **`and`** - defina como `true` para combinar vários valores (`N_value`) com `AND`
* **`operation`**
   * `equals` para correspondência exata (padrão)
   * `unequals` para comparação de desigualdade
   * `like` para usar o `jcr:like` função xpath (opcional)
   * `not` para nenhuma correspondência (por exemplo, `not(@prop)` no xpath, o parâmetro do valor será ignorado)
   * `exists` verificação da existência
      * `true` a propriedade deve existir
      * `false` é igual a `not` e é o padrão
* **`depth`** - número de níveis curingas abaixo dos quais a propriedade/caminho relativo pode existir (por exemplo, `property=size depth=2` verificará `node/size`, `node/*/size` e `node/*/*/size`)

### rangeproperty {#rangeproperty}

Esse predicado corresponde a uma propriedade JCR em relação a um intervalo. Isso se aplica a propriedades com tipos lineares como `LONG`, `DOUBLE` e `DECIMAL`. Para `DATE` consulte o [`daterange`](#daterange) predicado que otimizou a entrada de formato de data.

Você pode definir um limite inferior, um limite superior ou ambos. A operação (por exemplo, menor ou menor ou igual a) também pode ser especificada individualmente para limite inferior e superior.

Ele não oferece suporte à extração de facetas.

#### Propriedades {#properties-16}

* **`property`** - caminho relativo para a propriedade
* **`lowerBound`** - limite inferior para verificar a propriedade
* **`lowerOperation`** - `>` (padrão) ou `>=`, aplica-se ao `lowerValue`
* **`upperBound`** - limite superior para verificar a propriedade
* **`upperOperation`** - `<` (padrão) ou `<=`, aplica-se ao `lowerValue`
* **`decimal`** - `true` se a propriedade marcada for do tipo Decimal

### relativedaterange {#relativedaterange}

Este predicado corresponde `JCR DATE` propriedades em relação a um intervalo de data/hora usando deslocamentos de tempo relativos à hora atual do servidor. Você pode especificar `lowerBound` e `upperBound` usando um valor de milissegundo ou a sintaxe Bugzilla `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos). Prefixo com `-` para indicar um deslocamento negativo antes do tempo atual. Se você especificar somente `lowerBound` ou `upperBound`, o outro assumirá como padrão `0`, representando a hora atual.

Por exemplo:

* `upperBound=1h` e não `lowerBound`) seleciona qualquer item na próxima hora
* `lowerBound=-1d` e não `upperBound`) seleciona qualquer item nas últimas 24 horas
* `lowerBound=-6M` e `upperBound=-3M` seleciona qualquer item nos últimos 3 a 6 meses
* `lowerBound=-1500` e `upperBound=5500` seleciona algo entre 1500 milissegundos e 5500 milissegundos no futuro
* `lowerBound=1d` e `upperBound=2d` seleciona qualquer coisa depois de amanhã

Observe que não leva anos bissextos em consideração e todos os meses são 30 dias.

Não é compatível com a filtragem.

Ele oferece suporte à extração de facetas da mesma forma que a variável [`daterange`](#daterange) predicado.

#### Propriedades {#properties-17}

* **`upperBound`** - limite de data superior em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) em relação ao tempo atual do servidor, use `-` para desvio negativo
* **`lowerBound`** - limite de data inferior em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) em relação ao tempo atual do servidor, use `-` para desvio negativo

### savedquery {#savedquery}

Esse predicado inclui todos os predicados de uma consulta persistente do Construtor de consultas na consulta atual como um predicado de subgrupo.

Observe que isso não executará uma query extra, mas estenderá a query atual.

As consultas podem ser mantidas programaticamente usando `QueryBuilder#storeQuery()`. O formato pode ser de várias linhas `String` ou `nt:file` nó que contém a consulta como um arquivo de texto no formato de propriedades Java.

Ela não oferece suporte à extração de facetas para os predicados da consulta salva.

#### Propriedades {#properties-19}

* **`savedquery`** - caminho para a consulta salva (`String` propriedade ou `nt:file` node)

### semelhante {#similar}

Esse predicado é uma pesquisa de semelhança usando o JCR XPath `rep:similar()`.

Ele não oferece suporte à filtragem e não oferece suporte à extração de facetas.

#### Propriedades {#properties-20}

* **`similar`** - caminho absoluto para o nó para o qual encontrar nós semelhantes
* **`local`** - um caminho relativo para um nó descendente ou `.` para o nó atual (opcional, o padrão é `.`)

### tag {#tag}

Isso prevê pesquisas de conteúdo marcado com uma ou mais tags, especificando caminhos de título de tag.

Ele suporta extração de facetas e fornece buckets para cada tag única, usando seu caminho de título de tag atual.

#### Propriedades {#properties-21}

* **`tag`** - caminho do título da tag a ser procurado, por exemplo `properties:orientation/landscape`
* **`N_value`** - utilização `1_value`, `2_value`, ... para verificar várias tags (combinadas com `OR` por padrão, com `AND` if `and=true`)
* **`property`** - propriedade (ou caminho relativo para propriedade) a ser observada (padrão) `cq:tags`)

### tagid {#tagid}

Isso prevê pesquisas de conteúdo marcado com uma ou mais tags, especificando IDs de tags.

Ele suporta extração de facetas e fornece buckets para cada tag única, usando sua ID de tag atual.

#### Propriedades {#properties-22}

* **`tagid`** - ID da tag a ser procurada, por exemplo `properties:orientation/landscape`
* **`N_value`** - utilização `1_value`, `2_value`, ... para verificar várias IDs de tag (combinadas com `OR` por padrão, com `AND` if `and=true`)
* **`property`** - propriedade (ou caminho relativo para propriedade) a ser observada (padrão) `cq:tags`)

### tagsearch {#tagsearch}

Isso prevê pesquisas de conteúdo marcado com uma ou mais tags, especificando palavras-chave. Isso primeiro pesquisará as tags que contêm essas palavras-chave em seus títulos e, em seguida, restringirá o resultado somente aos itens marcados com elas.

Ele não oferece suporte à extração de facetas.

#### Propriedades {#Properties-1}

* **`tagsearch`** - palavra-chave a ser pesquisada em títulos de tags
* **`property`** - propriedade (ou caminho relativo para propriedade) a ser considerada (padrão `cq:tags`)
* **`lang`** - para pesquisar somente um título de tag localizado (por exemplo, `de`)
* **`all`** - valor booleano para pesquisar o texto completo da tag, ou seja, todos os títulos, descrição etc. (tem precedência sobre `lang`)

### tipo {#type}

Esse predicado restringe os resultados a um tipo de nó JCR específico, ambos os tipos de nó primário ou tipos mixin. Isso também encontrará subtipos desse tipo de nó. Observe que os índices de pesquisa do repositório precisam abranger os tipos de nó para uma execução eficiente.

Ele suporta extração de facetas e fornece buckets para cada tipo exclusivo nos resultados.

#### Propriedades {#Properties-2}

* **`type`** - tipo de nó ou nome mixin a ser procurado, por exemplo `cq:Page`
