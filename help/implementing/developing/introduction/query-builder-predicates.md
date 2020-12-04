---
title: Referência de previsão do Construtor de query
description: Prever referência para a API do Construtor de Query.
translation-type: tm+mt
source-git-commit: 90b635cb31af910e08bdee7925cec0c7beb05318
workflow-type: tm+mt
source-wordcount: '2221'
ht-degree: 1%

---


# Referência de previsão do Query Builder {#query-builder-predicate-reference}

## Geral {#general}

### raiz {#root}

Este é o grupo de previsão raiz. Ele suporta todos os recursos de um grupo e permite a configuração de parâmetros de query globais.

O nome &quot;raiz&quot; nunca é usado em um query, é implícito.

#### Propriedades {#properties-18}

* **`p.offset`** - número que indica o start da página de resultados, ou seja, quantos itens ignorar
* **`p.limit`** - número que indica o tamanho da página
* **`p.guessTotal`** - recomendado: Evitar calcular o total dos resultados que possam ser dispendiosos; um número que indica o total máximo para contar até (por exemplo, 1000, um número que dá aos usuários feedback suficiente sobre o tamanho bruto e números exatos para obter resultados menores) ou  `true` para contar apenas até o mínimo necessário  `p.offset` +  `p.limit`
* **`p.excerpt`** - se estiver definido como  `true`, incluir um excerto de texto completo no resultado
* **`p.hits`** - (somente para o servlet JSON) selecione a maneira como as ocorrências são gravadas como JSON, com essas ocorrências padrão (extensíveis por meio do serviço ResultHitWriter):
   * **`simple`** - itens mínimos como  `path`,  `title`,  `lastmodified`,  `excerpt` (se definidos)
   * **`full`** - renderização JSON do nó, com  `jcr:path` indicação do caminho da ocorrência: por padrão, apenas lista as propriedades diretas do nó, inclui uma árvore mais profunda com  `p.nodedepth=N`, o que significa 0, a subárvore infinita inteira; adicione  `p.acls=true` para incluir as permissões do JCR da sessão atual no item de resultado fornecido (mapeamentos:  `create` =  `add_node`,  `modify` =  `set_property`,  `delete` =  `remove`)
   * **`selective`** - somente as propriedades especificadas em  `p.properties`, que é uma lista separada por espaços (use  `+` em URLs) de caminhos relativos; se o caminho relativo tiver uma profundidade,  `>1` eles serão representados como objetos filhos; a  `jcr:path` propriedade especial inclui o caminho da ocorrência

### grupo {#group}

Este predicado permite construir condições aninhadas. Os grupos podem conter grupos aninhados. Tudo o que está em um query do Construtor de Query está implicitamente em um grupo raiz, que também pode ter parâmetros `p.or` e `p.not`.

A seguir, há um exemplo de correspondência entre uma de duas propriedades e um valor:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Isto é conceitualmente `(1_property` OU `2_property)`.

Este é um exemplo para grupos aninhados:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Isso pesquisa o termo **Management** nas páginas em `/content/wknd/ch/de` ou nos ativos em `/content/dam/wknd`.

Isto é conceitualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Esteja ciente de que tais junções OU precisam de bons índices por motivos de desempenho.

#### Propriedades {#properties-6}

* **`p.or`** - se definido como  `true`, apenas um predicado no grupo deve corresponder. O padrão é `false`, o que significa que todos devem corresponder
* **`p.not`** - se estiver definido como  `true`, nega o grupo (o padrão é  `false`)
* **`<predicate>`** - adiciona predicados aninhados
* **`N_<predicate>`** - adiciona vários predicados aninhados ao mesmo tempo, como  `1_property, 2_property, ...`

### orderby {#orderby}

Esse predicado permite a classificação dos resultados. Se a ordem por várias propriedades for necessária, esse predicado precisa ser adicionado várias vezes usando o prefixo number, como `1_orderby=first`, `2_oderby=second`.

#### Propriedades {#properties-13}

* **`orderby`** - o nome da propriedade JCR indicado por @ à esquerda, por exemplo,  `@jcr:lastModified` ou  `@jcr:content/jcr:title`, ou outro predicado no query, por exemplo  `2_property`, no qual classificar
* **`sort`** - direção de classificação,  `desc` para decrescente ou  `asc` crescente (padrão)
* **`case`** - se estiver pronto para  `ignore` tornar o processo de triagem insensível, o que significa que  `a` vem antes  `B`; se vazio ou deixado de fora, a classificação diferencia maiúsculas de minúsculas, o que significa que  `B` vem antes  `a`

## Predicados {#predicates}

### boolproperty {#boolproperty}

Esse predicado corresponde às propriedades booleanas do JCR. Aceita somente os valores `true` e `false`. No caso de `false`, corresponderá se a propriedade tiver o valor `false` ou se não existir. Isso pode ser útil para verificar sinalizadores booleanos que só são definidos quando ativados.

O parâmetro herdado `operation` não tem significado.

Esse predicado suporta extração de facetas e fornece compartimentos para cada valor `true` ou `false`, mas somente para propriedades existentes.

#### Propriedades {#properties}

* **`boolproperty`** - caminho relativo para a propriedade, por exemplo  `myFeatureEnabled` ou  `jcr:content/myFeatureEnabled`
* **`value`** - valor para verificar a propriedade,  `true` ou  `false`

### contentfragment {#contentfragment}

Esse predicado restringe o resultado a fragmentos de conteúdo.

* Ele não oferece suporte à filtragem.
* Ele não suporta extração de facetas.

#### Propriedades {#properties-1}

* **`contentfragment`** - Ele pode ser usado com qualquer valor para verificar fragmentos de conteúdo.

### `dateComparison` {#datecomparison}

Este predicado compara duas propriedades de data JCR entre si. Pode testar se são iguais, desiguais, maiores ou maiores que ou iguais.

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa.

#### Propriedades {#properties-2}

* **`property1`** - propriedade path to first date
* **`property2`** - caminho para a segunda propriedade de data
* **`operation`**
   * `=` para correspondência exata (padrão)
   * `!=` para comparação de desigualdade
   * `>` para  `property1` maiores que  `property2`
   * `>=` para  `property1` maior que ou igual a  `property2`

### daterange {#daterange}

Esse predicado corresponde às propriedades de data do JCR em relação a um intervalo de data/hora. Isso usa o ISO8601
formato para datas e horas (`YYYY-MM-DDTHH:mm:ss.SSSZ`) e permite também representações parciais, como `YYYY-MM-DD`. Como alternativa, o carimbo de data e hora pode ser fornecido como tempo POSIX.

Você pode procurar qualquer coisa entre dois carimbos de data e hora, qualquer coisa mais recente ou mais antiga que uma data específica, e também escolher entre intervalos inclusivos e abertos.

Ele suporta extração de facetas e fornece buckets `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year` e `earlier than last year`.

Ele não oferece suporte à filtragem.

#### Propriedades {#properties-3}

* **`property`** - caminho relativo para uma  `DATE` propriedade, por exemplo  `jcr:lastModified`
* **`lowerBound`** - data limite inferior vinculada para verificar a propriedade, por exemplo  `2014-10-01`
* **`lowerOperation`** -  `>` (mais recente) ou  `>=` (mais recente), aplica-se ao  `lowerBound`. O padrão é `>`
* **`upperBound`** - limite superior para verificar a propriedade, por exemplo,  `2014-10-01T12:15:00`
* **`upperOperation`** -  `<` (mais antigo) ou  `<=` (mais antigo), aplica-se ao  `upperBound`. O padrão é `<`
* **`timeZone`** - ID do fuso horário a ser usado quando não for fornecido como uma string de data ISO-8601. O padrão é o fuso horário padrão do sistema.

### excludepath{#excludepaths}

Esse predicado exclui os nós do resultado onde seu caminho corresponde a uma expressão regular.

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa.

Ele não suporta extração de facetas.

#### Propriedades {#properties-4}

* **`excludepaths`** - expressão regular comparada com caminhos de resultado, excluindo os correspondentes do resultado.

### fulltext {#fulltext}

Esse predicado pesquisa termos no índice de texto completo.

Ele não oferece suporte à filtragem.

Ele não suporta extração de facetas.

#### Propriedades {#properties-5}

* **`fulltext`** - o(s) termo(s) de pesquisa de texto completo
* **`relPath`** - o caminho relativo a ser pesquisado na propriedade ou subnó. Essa propriedade é opcional.

### hasPermission {#haspermission}

Este predicado restringe o resultado a itens onde a sessão atual tem os privilégios [JCR especificados.](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa. Ele não suporta extração de facetas.

#### Propriedades {#properties-7}

* **`hasPermission`** - privilégios JCR separados por vírgulas que a sessão do usuário atual deve ter TODOS para o nó em questão; por exemplo  `jcr:write`,  `jcr:modifyAccessControl`

### language {#language}

Este predicado encontra AEM páginas em um idioma específico. Isso analisa a propriedade de idioma da página e o caminho da página que geralmente inclui o idioma ou a localidade em uma estrutura de site de nível superior.

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa.

Ele oferece suporte à extração de facetas e baldes para cada código de idioma único.

#### Propriedades {#properties-8}

* **`language`** - código de idioma ISO, por exemplo  `de`

### mainasset {#mainasset}

Esse predicado verifica se um nó é um ativo principal DAM e não um subativo. Isto é basicamente cada nó não dentro de um nó de subativos. Observe que isso não verifica o tipo de nó `dam:Asset`. Para usar esse predicado, basta definir `mainasset=true` ou `mainasset=false`. Não há mais propriedades.

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa.

Ele suporta extração de facetas e fornece dois compartimentos para ativos principais e subativos.

#### Propriedades {#properties-9}

* **`mainasset`** - booleano,  `true` para os ativos principais,  `false` para os subativos

### MemberOf {#memberof}

Este predicado encontra itens que são membros de uma coleção de recursos específica [sling](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa.

Ele não suporta extração de facetas.

#### Propriedades {#properties-10}

* **`memberOf`** - caminho da coleção de recursos Sling

### nodename {#nodename}

Esse predicado corresponde aos nomes dos nós do JCR.

Ele suporta extração de facetas e fornece buckets para cada nome de nó exclusivo (nome de arquivo).

#### Propriedades {#properties-11}

* **`nodename`** - padrão de nome de nó que permite curingas:  `*` = any or no char,  `?` = any char,  `[abc]` = only chars entre parênteses

### notexpired {#notexpired}

Este predicado corresponde itens verificando se uma propriedade de data JCR é maior ou igual à hora atual do servidor. Isso pode ser usado para verificar um valor `expiresAt` e limitar os resultados somente àqueles que ainda não expiraram (`notexpired=true`) ou que já expiraram (`notexpired=false`).

Ele não oferece suporte à filtragem.

Ele suporta extração de facetas da mesma forma que o predicado [`daterange`](#daterange).

#### Propriedades {#properties-12}

* **`notexpired`** - booleano,  `true` para ainda não expirado (data no futuro ou igual),  `false` para expirado (data no passado) (obrigatório)
* **`property`** - caminho relativo para a  `DATE` propriedade a ser verificada (obrigatório)

### path {#path}

Esse predicativo pesquisa dentro de um determinado caminho.

Ele não suporta extração de facetas.

#### Propriedades {#properties-14}

* **`path`** - Isso define o padrão do caminho.
   * Dependendo da propriedade `exact`, a subárvore inteira corresponderá (como anexar `//*` no xpath, mas observe que isso não inclui o caminho base) ou somente uma correspondência exata de caminho, que pode incluir curingas (`*`).
      * O padrão é `true`
   * Se a propriedade `self`estiver definida, a subárvore inteira, incluindo o nó base, será pesquisada.
* **`exact`** - se  `exact` for  `true`, o caminho exato deve corresponder, mas pode conter curingas simples (`*`), que correspondem aos nomes, mas não  `/`; se for  `false` (padrão) todos os descendentes serão incluídos (opcional)
* **`flat`** - pesquisa somente os filhos diretos (como anexar  `/*` no xpath) (usado somente se não  `exact` for verdadeiro, opcional)
* **`self`** - pesquisa a subárvore, mas inclui o nó base fornecido como caminho (sem curingas)

### propriedade {#property}

Esse predicado corresponde às propriedades do JCR e seus valores.

Ele suporta extração de facetas e fornece cestos para cada valor de propriedade exclusivo nos resultados.

#### Propriedades {#properties-15}

* **`property`** - caminho relativo para a propriedade, por exemplo  `jcr:title`
* **`value`** - valor para verificar a propriedade; segue o tipo de propriedade JCR para conversões de string
* **`N_value`** - utilização  `1_value`,  `2_value`, ... para verificar vários valores (combinados  `OR` por padrão, com  `AND` if  `and=true`)
* **`and`** - definido  `true` para combinar múltiplos valores (`N_value`com  `AND`
* **`operation`**
   * `equals` para correspondência exata (padrão)
   * `unequals` para comparação de desigualdade
   * `like` para usar a função  `jcr:like` xpath (opcional)
   * `not` para nenhuma correspondência (por exemplo,  `not(@prop)` no xpath, o parâmetro value será ignorado)
   * `exists` para verificação da existência
      * `true` a propriedade deve existir
      * `false` é igual a  `not` e é o padrão
* **`depth`** - número de níveis curingas abaixo dos quais a propriedade/caminho relativo pode existir (por exemplo,  `property=size depth=2` verificará  `node/size`e  `node/*/size`  `node/*/*/size`)

### rangeproperty {#rangeproperty}

Esse predicado corresponde a uma propriedade JCR em relação a um intervalo. Isso se aplica a propriedades com tipos lineares como `LONG`, `DOUBLE` e `DECIMAL`. Para `DATE`, consulte o predicado [`daterange`](#daterange) que otimizou a entrada de formato de data.

É possível definir um limite inferior, um limite superior ou ambos. A operação (por exemplo, menor que ou menor que ou igual a) também pode ser especificada para limite inferior e superior individualmente.

Ele não suporta extração de facetas.

#### Propriedades {#properties-16}

* **`property`** - caminho relativo para a propriedade
* **`lowerBound`** - limite inferior para verificar a propriedade
* **`lowerOperation`** -  `>` (padrão) ou  `>=`, aplica-se à variável  `lowerValue`
* **`upperBound`** - limite superior para verificar a propriedade
* **`upperOperation`** -  `<` (padrão) ou  `<=`, aplica-se à variável  `lowerValue`
* **`decimal`** -  `true` se a propriedade verificada for do tipo Decimal

### relativedaterange {#relativedaterange}

Esse predicado corresponde `JCR DATE` às propriedades em relação a um intervalo de data/hora usando deslocamentos de tempo relativos à hora atual do servidor. Você pode especificar `lowerBound` e `upperBound` usando um valor de milissegundo ou a sintaxe Bugzilla `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos). Prefixo com `-` para indicar um deslocamento negativo antes da hora atual. Se você especificar apenas `lowerBound` ou `upperBound`, o outro assumirá `0` como padrão, representando a hora atual.

Por exemplo:

* `upperBound=1h` (e não  `lowerBound`) seleciona qualquer item na próxima hora
* `lowerBound=-1d` (e não  `upperBound`) seleciona nada nas últimas 24 horas
* `lowerBound=-6M` e  `upperBound=-3M` seleciona qualquer coisa nos últimos 3 a 6 meses
* `lowerBound=-1500` e  `upperBound=5500` seleciona algo entre 1500 milissegundos e 5500 milissegundos no futuro
* `lowerBound=1d` e  `upperBound=2d` seleciona qualquer coisa depois de amanhã

Observe que não leva anos bissextos em consideração e todos os meses são 30 dias.

Ele não oferece suporte à filtragem.

Ele suporta extração de facetas da mesma forma que o predicado [`daterange`](#daterange).

#### Propriedades {#properties-17}

* **`upperBound`** - data limite em milissegundos ou  `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) em relação à hora atual do servidor, usar  `-` para compensação negativa
* **`lowerBound`** - data limite inferior em milissegundos ou  `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) em relação à hora atual do servidor, usar  `-` para compensação negativa

### savedquery {#savedquery}

Este predicado inclui todos os predicados de um query do Construtor de Query persistido no query atual como um predicado de subgrupo.

Observe que isso não executará um query extra, mas estenderá o query atual.

Os query podem ser persistentes programaticamente usando `QueryBuilder#storeQuery()`. O formato pode ser uma propriedade `String` de várias linhas ou um nó `nt:file` que contenha o query como um arquivo de texto no formato de propriedades Java.

Ele não suporta extração de facetas para os predicados do query salvo.

#### Propriedades {#properties-19}

* **`savedquery`** - caminho para o query salvo (`String` propriedade ou  `nt:file` nó)

### similar {#similar}

Este predicado é uma pesquisa de semelhança usando o `rep:similar()` do JCR XPath.

Ele não suporta filtragem e não suporta extração de facetas.

#### Propriedades {#properties-20}

* **`similar`** - caminho absoluto para o nó para o qual encontrar nós semelhantes
* **`local`** - um caminho relativo para um nó descendente ou  `.` para o nó atual (opcional, o padrão é  `.`)

### tag {#tag}

Isso prevê pesquisas de conteúdo marcado com uma ou mais tags, especificando caminhos de título de tag.

Ele suporta extração de facetas e fornece cestos para cada tag exclusiva, usando seu caminho de título de tag atual.

#### Propriedades {#properties-21}

* **`tag`** - caminho do título da tag a procurar, por exemplo  `properties:orientation/landscape`
* **`N_value`** - utilização  `1_value`,  `2_value`, ... para verificar se há várias tags (combinadas com  `OR` por padrão, com  `AND` if  `and=true`)
* **`property`** - propriedade (ou caminho relativo para propriedade) a ser vista (padrão  `cq:tags`)

### tagid {#tagid}

Isso prevê pesquisas de conteúdo marcado com uma ou mais tags, especificando IDs de tags.

Ele suporta extração de facetas e fornece compartimentos para cada tag exclusiva, usando sua ID de tag atual.

#### Propriedades {#properties-22}

* **`tagid`** - ID da tag a ser procurada, por exemplo  `properties:orientation/landscape`
* **`N_value`** - utilização  `1_value`,  `2_value`, ... para verificar a existência de várias IDs de tags (combinadas com  `OR` por padrão, com  `AND` if  `and=true`)
* **`property`** - propriedade (ou caminho relativo para propriedade) a ser vista (padrão  `cq:tags`)

### tagsearch {#tagsearch}

Isso prevê pesquisas de conteúdo marcado com uma ou mais tags, especificando palavras-chave. Isso primeiro pesquisará por tags que contenham essas palavras-chave em seus títulos e, em seguida, restringirá o resultado somente a itens marcados com essas palavras.

Ele não suporta extração de facetas.

#### Propriedades {#Properties-1}

* **`tagsearch`** - palavra-chave para pesquisar em títulos de tag
* **`property`** - propriedade (ou caminho relativo para propriedade) a ser considerada (padrão  `cq:tags`)
* **`lang`** - para pesquisar somente um título de tag localizado (por exemplo,  `de`)
* **`all`** - valor booliano para pesquisar o texto completo da tag, ou seja, todos os títulos, descrição etc. (tem prioridade sobre `lang`)

### tipo {#type}

Esse predicado restringe os resultados a um tipo de nó JCR específico, tanto os tipos de nó primário quanto os tipos de mixin. Isso também localizará subtipos desse tipo de nó. Observe que os índices de pesquisa do repositório precisam abranger os tipos de nó para uma execução eficiente.

Ele suporta extração de facetas e fornece cestos para cada tipo exclusivo nos resultados.

#### Propriedades {#Properties-2}

* **`type`** - tipo de nó ou nome de mistura a ser procurado, por exemplo  `cq:Page`
