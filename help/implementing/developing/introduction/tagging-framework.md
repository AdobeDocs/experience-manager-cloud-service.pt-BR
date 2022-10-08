---
title: Estrutura de marcação do AEM
description: Marque o conteúdo e aproveite a infraestrutura de marcação de AEM para categorizá-lo e organizá-lo.
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 0%

---

# A estrutura de marcação de AEM {#aem-tagging-framework}

A marcação permite que o conteúdo seja categorizado e organizado. As tags podem ser classificadas por namespace e taxonomia. Para obter informações detalhadas sobre o uso de tags:

* Consulte [Uso de tags](/help/sites-cloud/authoring/features/tags.md) para obter informações sobre como marcar conteúdo como um autor de conteúdo.
* Consulte Administração de tags para obter a perspectiva do administrador sobre como criar e gerenciar tags, bem como sobre quais tags de conteúdo foram aplicadas.

Este artigo se concentra na estrutura subjacente que suporta a marcação no AEM e como aproveitá-lo como desenvolvedor.

## Introdução {#introduction}

Para marcar o conteúdo e aproveitar a infraestrutura de marcação de AEM :

* A tag deve existir como um nó do tipo [`cq:Tag`](#cq-tag-node-type) nos termos do [nó raiz da taxonomia.](#taxonomy-root-node)
* O nó de conteúdo marcado `NodeType` deve incluir o [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mistura.
* O [`TagID`](#tagid) é adicionado ao nó de conteúdo [`cq:tags`](#cq-tags-property) e resolve para um nó do tipo [`cq:Tag`.](#cq-tag-node-type)

## cq:Tag Node Type {#cq-tag-node-type}

A declaração de uma tag é capturada no repositório em um nó do tipo `cq:Tag.`

* Uma tag pode ser uma palavra simples (por exemplo, `sky`) ou representar uma taxonomia hierárquica (por exemplo, `fruit/apple`, o que significa tanto o fruto genérico como a maçã mais específica).
* As tags são identificadas por um `TagID`.
* Uma tag tem meta informações opcionais, como um título, títulos localizados e uma descrição. O título deve ser exibido nas interfaces do usuário em vez de `TagID`, quando presente.

A estrutura de marcação também fornece a capacidade de restringir autores e visitantes do site a usar somente tags específicas e predefinidas.

### Características da tag {#tag-characteristics}

* O tipo de nó é `cq:Tag`.
* O nome do nó é um componente do [`TagID`.](#tagid)
* O [`TagID`](#tagid) sempre inclui uma [namespace.](#tag-namespace)
* O `jcr:title` a propriedade (o Título a ser exibido na interface do usuário) é opcional.
* O `jcr:description` é opcional.
* Ao conter nós filho, é referido como um [tag container.](#container-tags)
* A tag é armazenada no repositório abaixo de um caminho base chamado [nó raiz da taxonomia.](#taxonomy-root-node)

### TagID {#tagid}

A `TagID` identifica um caminho que resolve um nó de tag no repositório.

Normalmente, a variável `TagID` é um encurtador `TagID` começar com o namespace ou pode ser um valor absoluto `TagID` a partir do [nó raiz da taxonomia.](#taxonomy-root-node)

Quando o conteúdo é marcado, se ainda não existir, a variável [`cq:tags`](#cq-tags-property) é adicionada ao nó de conteúdo e a variável `TagID` é adicionado ao `String` valor da matriz.

O `TagID` consiste em um [namespace](#tag-namespace) seguido pelo `TagID`. [Tags do contêiner](#container-tags) têm subtags que representam uma ordem hierárquica na taxonomia. As subtags podem ser usadas para referenciar tags da mesma forma que qualquer `TagID`. Por exemplo, marcar conteúdo com `fruit` é permitido, mesmo que seja uma tag container com subtags , como `fruit/apple` e `fruit/banana`.

### Nó raiz da taxonomia {#taxonomy-root-node}

O nó raiz da taxonomia é o caminho base para todas as tags no repositório. O nó raiz da taxonomia deve *not* ser um nó do tipo `cq:Tag`.

Em AEM, o caminho base é `/content/cq:tags` e o nó raiz é do tipo `cq:Folder`.

### Namespace de tag {#tag-namespace}

Os namespaces permitem agrupar itens. O caso de uso mais comum é ter um namespace por site (por exemplo, público versus interno) ou por aplicativo maior (por exemplo, Sites ou Assets), mas os namespaces podem ser usados para várias outras necessidades. Os namespaces são usados na interface do usuário para mostrar apenas o subconjunto de tags (ou seja, tags de um determinado namespace) que é aplicável ao conteúdo atual.

O namespace da tag é o primeiro nível na subárvore da taxonomia, que é o nó imediatamente abaixo do [nó raiz da taxonomia.](#taxonomy-root-node) Um namespace é um nó do tipo `cq:Tag` cujo pai não é um `cq:Tag` tipo de nó.

Todas as tags têm um namespace. Se nenhum namespace for especificado, a tag será atribuída ao namespace padrão, que é `TagID` `default`, ou seja `/content/cq:tags/default`.  O padrão do Título é `Standard Tags`em tais casos.

### Tags do contêiner {#container-tags}

Uma tag container é um nó do tipo `cq:Tag` contendo qualquer número e tipo de nós filhos, o que possibilita aprimorar o modelo de tags com metadados personalizados.

Além disso, tags de contêiner (ou supertags) em uma taxonomia servem como subsoma de todas as subtags: por exemplo, conteúdo marcado com `fruit/apple` é considerado como marcado com `fruit` também, ou seja, pesquisar conteúdo apenas marcado com `fruit` também encontraria o conteúdo marcado com `fruit/apple`.

### Resolvendo TagIDs {#resolving-tagids}

Se a ID da tag contiver dois pontos (`:`), o sinal de dois pontos separa o namespace da tag ou da subtaxonomia, que são então separadas por barras normais (`/`). Se a ID da tag não tiver dois pontos, o namespace padrão será implícito.

O local padrão e único das tags está abaixo `/content/cq:tags`.

Tags que fazem referência a caminhos ou caminhos não existentes que não apontam para um `cq:Tag` são considerados inválidos e são ignorados.

A tabela a seguir mostra algumas amostras `TagID`s, seus elementos e como a função `TagID` resolve para um caminho absoluto no repositório:

| `TagID` | Namespace | ID local | Tags do contêiner | Tag Folha | Caminho absoluto da tag do repositório |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (nenhum) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (nenhum) | (nenhum) | (nenhum) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Localização do título da tag {#localization-of-tag-title}

Quando a tag inclui a string de título opcional `jcr:title`, é possível localizar o título para exibição ao adicionar a propriedade `jcr:title.<locale>`.

Para obter mais detalhes, consulte:

* [Tags em diferentes idiomas,](tagging-applications.md#tags-in-different-languages) que descreve o uso das APIs como um desenvolvedor
* Gerenciamento de tags em diferentes idiomas, que descreve o uso do console Marcação como administrador

### Controle de acesso {#access-control}

As tags existem como nós no repositório no [nó raiz da taxonomia.](#taxonomy-root-node) Permitir ou negar que autores e visitantes do site criem tags em um determinado namespace pode ser obtido definindo ACLs apropriadas no repositório.

Negar permissões de leitura para determinadas tags ou namespaces controlará a capacidade de aplicar tags a conteúdo específico.

Uma prática típica inclui:

* Permitir o `tag-administrators` acesso de gravação de grupo/função para todos os namespaces (adicionar/modificar em `/content/cq:tags`). Este grupo vem com AEM pronto para uso.
* Permitir que usuários/autores leiam o acesso a todos os namespaces que devem ser legíveis a eles (em sua maioria, todos).
* Permitir que usuários/autores gravem acesso aos namespaces, onde as tags devem ser livremente definidas por usuários/autores (`add_node` under `/content/cq:tags/some_namespace`)

## Conteúdo marcável : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Para que os desenvolvedores de aplicativos anexem tags a um tipo de conteúdo, o registro do nó ([CND](https://jackrabbit.apache.org/node-type-notation.html)) deve incluir o `cq:Taggable` mistura ou o `cq:OwnerTaggable` mistura.

O `cq:OwnerTaggable` mixin, que herda de `cq:Taggable`, destina-se a indicar que o conteúdo pode ser classificado pelo proprietário/autor. No AEM, é apenas um atributo do `cq:PageContent` nó . O `cq:OwnerTaggable` a mixin não é exigida pela estrutura de marcação.

>[!NOTE]
>
>Recomenda-se ativar somente as tags no nó de nível superior de um item de conteúdo agregado (ou em seu `jcr:content` nó ). Os exemplos incluem:
>
>* Páginas (`cq:Page`) em que `jcr:content`o nó é do tipo `cq:PageContent`, que inclui o `cq:Taggable` mistura.
>* Ativos (`cq:Asset`) em que `jcr:content/metadata` o nó sempre tem o `cq:Taggable` mistura.


### Notação de tipo de nó (CND) {#node-type-notation-cnd}

As definições de Tipo de nó existem no repositório como arquivos CND. A notação CND é definida como parte do [Documentação do JCR.](https://jackrabbit.apache.org/node-type-notation.html).

As definições essenciais para os Tipos de nó incluídos no AEM são as seguintes:

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## cq:tags Propriedade {#cq-tags-property}

O `cq:tags` a propriedade é um `String` matriz usada para armazenar um ou mais `TagID`s quando forem aplicadas ao conteúdo por autores ou visitantes do site. A propriedade só tem significado quando adicionada a um nó que é definido com a variável [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mistura.

>[!NOTE]
>
>Para aproveitar AEM funcionalidade de marcação, os aplicativos desenvolvidos e personalizados não devem definir outras propriedades de tag além de `cq:tags`.

## Mover e mesclar tags {#moving-and-merging-tags}

Veja a seguir uma descrição dos efeitos no repositório ao mover ou mesclar tags usando o console Marcação .

Quando a tag A é movida ou unida na tag B em `/content/cq:tags`:

* A tag A não é excluída e recebe uma `cq:movedTo` propriedade.
   * `cq:movedTo` aponta para a tag B.
   * Essa propriedade significa que a tag A foi movida ou mesclada na tag B.
   * A tag B movida atualizará essa propriedade de acordo.
   * A tag A é então oculta e é mantida somente no repositório para resolver IDs de tag em nós de conteúdo que apontam para a tag A.
   * O coletor de lixo da tag remove tags como a tag A, uma vez que mais nós de conteúdo apontam para elas.
   * Um valor especial para a variável `cq:movedTo` a propriedade é `nirvana`, que é aplicado quando a tag é excluída, mas não pode ser removida do repositório porque há subtags com uma `cq:movedTo` isso tem de ser mantido.

      >[!NOTE]
      >
      >O `cq:movedTo` só será adicionada à tag movida ou unida se uma dessas condições for atendida:
      >
      > 1. A tag é usada no conteúdo (o que significa que ela tem uma referência). OU
      > 1. A tag tem filhos que já foram movidos.

* A tag B é criada (no caso de uma movimentação) e recebe uma `cq:backlinks` propriedade.
   * `cq:backlinks` mantém as referências na outra direção, ou seja, mantém uma lista de todas as tags que foram movidas para ou mescladas com a tag B.
   * Isso é necessário principalmente para manter `cq:movedTo` propriedades atualizadas quando a tag B for movida/mesclada/excluída também ou quando a tag B for ativada, nesse caso todas as tags de backlinks também deverão ser ativadas.

      >[!NOTE]
      >
      >O `cq:backlinks` só será adicionada à tag movida ou unida se uma dessas condições for atendida:
      >
      > 1. A tag é usada no conteúdo (o que significa que ela tem uma referência). OU
      > 1. A tag tem filhos que já foram movidos.


Ler um `cq:tags` a propriedade de um nó de conteúdo envolve a seguinte resolução:

1. Se não houver correspondência em `/content/cq:tags`, nenhuma tag é retornada.
1. Se a tag tiver uma `cq:movedTo` do conjunto de propriedades, a ID da tag referenciada é seguida.
   * Essa etapa é repetida, desde que a tag seguida tenha uma `cq:movedTo` propriedade.
1. Se a tag seguida não tiver uma `cq:movedTo` , a tag será lida.

Para publicar a alteração quando uma tag tiver sido movida ou mesclada, a variável `cq:Tag` e todos os seus backlinks devem ser replicados. Isso é feito automaticamente quando a tag é ativada no console de administração de tags.

Atualizações posteriores no `cq:tags` limpa automaticamente as referências antigas. Isso é acionado porque a resolução de uma tag movida pela API retorna a tag de destino, fornecendo a ID da tag de destino.
