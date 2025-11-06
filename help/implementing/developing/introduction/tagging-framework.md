---
title: Estrutura de marcação do AEM
description: Marque o conteúdo e use a infraestrutura de Marcação do AEM para categorizá-lo e organizá-lo.
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 0%

---

# A estrutura de marcação do AEM {#aem-tagging-framework}

A marcação permite que o conteúdo seja categorizado e organizado. As tags podem ser classificadas por um namespace e uma taxonomia. Para obter informações detalhadas sobre o uso de tags:

* Consulte [Usando Tags](/help/sites-cloud/authoring/sites-console/tags.md) para obter informações sobre como marcar conteúdo como autor de conteúdo.
* Consulte Administração de tags para obter a perspectiva de um administrador sobre a criação e o gerenciamento de tags e a quais tags de conteúdo foram aplicadas.

Este artigo se concentra na estrutura subjacente que oferece suporte à marcação no AEM e em como usá-lo como desenvolvedor.

## Introdução {#introduction}

Para marcar conteúdo e usar a infraestrutura de marcação da AEM:

* A marca deve existir como um nó do tipo [`cq:Tag`](#cq-tag-node-type) no [nó raiz de taxonomia](#taxonomy-root-node).
* O nó de conteúdo marcado `NodeType` deve incluir o mixin [`cq:Taggable`](#taggable-content-cq-taggable-mixin).
* O [`TagID`](#tagid) é adicionado à propriedade [`cq:tags`](#cq-tags-property) do nó de conteúdo e é resolvido para um nó do tipo [`cq:Tag`](#cq-tag-node-type).

## Tipo de nó cq:Tag {#cq-tag-node-type}

A declaração de uma marca é capturada no repositório em um nó do tipo `cq:Tag.`

* Uma marca pode ser uma palavra simples (por exemplo, `sky`) ou representar uma taxonomia hierárquica (por exemplo, `fruit/apple`, significando a fruta genérica e a maçã mais específica).
* As marcas são identificadas por um `TagID` exclusivo.
* Uma tag tem informações meta opcionais, como um título, títulos localizados e uma descrição. O título deve ser exibido nas interfaces do usuário em vez de `TagID`, quando presente.

A estrutura de marcação também restringe os autores e visitantes do site a usar somente tags específicas e predefinidas.

### Características da tag {#tag-characteristics}

* O tipo de nó é `cq:Tag`.
* O nome do nó é um componente de [`TagID`](#tagid).
* O [`TagID`](#tagid) sempre inclui um [namespace](#tag-namespace).
* A propriedade `jcr:title` (o Título a ser exibido na interface do usuário) é opcional.
* A propriedade `jcr:description` é opcional.
* Quando contém nós filhos, é referido como uma [marca de contêiner](#container-tags).
* A marca é armazenada no repositório abaixo de um caminho base chamado [nó raiz de taxonomia](#taxonomy-root-node).

### TagID {#tagid}

Um `TagID` identifica um caminho que é resolvido para um nó de marca no repositório.

Normalmente, o `TagID` é uma abreviação `TagID` começando com o namespace ou pode ser um `TagID` absoluto começando do [nó raiz de taxonomia](#taxonomy-root-node).

Quando o conteúdo é marcado, se ainda não existir, a propriedade [`cq:tags`](#cq-tags-property) é adicionada ao nó de conteúdo e a `TagID` é adicionada ao valor da matriz `String` da propriedade.

`TagID` consiste em um [namespace](#tag-namespace) seguido pelo `TagID` local. [Marcas de contêiner](#container-tags) têm submarcas que representam uma ordem hierárquica na taxonomia. Submarcas podem ser usadas para fazer referência a marcas iguais a qualquer `TagID` local. Por exemplo, a marcação de conteúdo com `fruit` é permitida, mesmo que seja uma marca de contêiner com submarcas, como `fruit/apple` e `fruit/banana`.

### Nó raiz da taxonomia {#taxonomy-root-node}

O nó raiz da taxonomia é o caminho base para todas as tags no repositório. O nó raiz de taxonomia deve *não* ser um nó do tipo `cq:Tag`.

No AEM, o caminho base é `/content/cq:tags` e o nó raiz é do tipo `cq:Folder`.

### Namespace da tag {#tag-namespace}

Os namespaces permitem agrupar itens. O caso de uso mais comum é ter um namespace por site (por exemplo, público versus interno) ou por aplicativo maior (por exemplo, Sites ou Assets), mas os namespaces podem ser usados para várias outras necessidades. Os namespaces são usados na interface para mostrar apenas o subconjunto de tags (ou seja, tags de um determinado namespace) que é aplicável ao conteúdo atual.

O namespace da marca é o primeiro nível na subárvore de taxonomia, que é o nó imediatamente abaixo do [nó raiz de taxonomia](#taxonomy-root-node). Um namespace é um nó do tipo `cq:Tag` cujo pai não é um tipo de nó `cq:Tag`.

Todas as tags têm um namespace. Se nenhum namespace for especificado, a marca será atribuída ao namespace padrão, que é `TagID` `default`, ou seja, `/content/cq:tags/default`. O padrão do Título é `Standard Tags` nesses casos.

### Tags de contêiner {#container-tags}

Uma marca de contêiner é um nó do tipo `cq:Tag` que contém qualquer número e tipo de nós filhos, o que permite aprimorar o modelo de marca com metadados personalizados.

Além disso, as tags container (ou supertags) em uma taxonomia servem como a soma de todas as subtags. Por exemplo, o conteúdo marcado com `fruit/apple` também é considerado marcado com `fruit`. Ou seja, pesquisar conteúdo marcado com `fruit` também localizaria o conteúdo marcado com `fruit/apple`.

### Resolvendo TagIDs {#resolving-tagids}

Se a ID da marca contiver dois pontos (`:`), os dois pontos separarão o namespace da marca ou subtaxonomia, que são então separadas por barras normais (`/`). Se a ID da tag não tiver dois pontos, o namespace padrão será implícito.

O local padrão e único das marcas está abaixo de `/content/cq:tags`.

As marcas que fazem referência a caminhos ou caminhos não existentes que não apontam para um nó `cq:Tag` são consideradas inválidas e são ignoradas.

A tabela a seguir mostra alguns exemplos de `TagID`s, seus elementos e como `TagID` é resolvido para um caminho absoluto no repositório:

| `TagID` | Namespace | ID local | Tags de contêiner | Tag de folha | Caminho absoluto da tag do repositório |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (nenhum) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (nenhum) | (nenhum) | (nenhum) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Localização do título da tag {#localization-of-tag-title}

Quando a marca inclui a cadeia de caracteres de título opcional `jcr:title`, é possível localizar o título para exibição adicionando a propriedade `jcr:title.<locale>`.

Para obter mais detalhes, consulte o seguinte:

* [Marcas em Diferentes Idiomas](tagging-applications.md#tags-in-different-languages) descrevem o uso das APIs como um desenvolvedor
* Gerenciamento de tags em diferentes idiomas, que descrevem o uso do console de marcação como administrador

### Controle de acesso {#access-control}

As marcas existem como nós no repositório no [nó raiz de taxonomia](#taxonomy-root-node). Permitir ou negar que autores e visitantes do site criem tags em um determinado namespace pode ser obtido definindo ACLs apropriadas no repositório.

A negação de permissões de leitura para determinadas tags ou namespaces controla a capacidade de aplicar tags a um conteúdo específico.

Uma prática típica inclui:

* Permitindo acesso de gravação de grupo/função `tag-administrators` a todos os namespaces (adicionar/modificar em `/content/cq:tags`). Esse grupo vem com AEM pronto para uso.
* Permitir que usuários/autores leiam todos os namespaces que devem ser legíveis para eles (principalmente todos).
* Permitir que usuários/autores gravem acesso aos namespaces em que as marcas devem ser definidas livremente por usuários/autores (`add_node` em `/content/cq:tags/some_namespace`)

## Conteúdo Marcável: CQ:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Para que os desenvolvedores de aplicativos anexem a marcação a um tipo de conteúdo, o registro do nó ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) deve incluir o mixin `cq:Taggable` ou `cq:OwnerTaggable`.

O mixin `cq:OwnerTaggable`, que herda de `cq:Taggable`, destina-se a indicar que o conteúdo pode ser classificado pelo proprietário/autor. No AEM, é apenas um atributo do nó `cq:PageContent`. O mixin `cq:OwnerTaggable` não é exigido pela estrutura de marcação.

>[!NOTE]
>
>É recomendável habilitar tags somente no nó de nível superior de um item de conteúdo agregado (ou em seu nó `jcr:content`). Por exemplo:
>
>* Páginas (`cq:Page`) onde o nó `jcr:content` é do tipo `cq:PageContent`, que inclui o mixin `cq:Taggable`.
>* Assets (`cq:Asset`) onde o nó `jcr:content/metadata` sempre tem o mixin `cq:Taggable`.

### Notação de tipo de nó (CND) {#node-type-notation-cnd}

As definições de Tipo de nó existem no repositório como arquivos CND. A notação CND é definida como parte da [documentação JCR](https://jackrabbit.apache.org/jcr/node-type-notation.html).

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

## Propriedade cq:tags {#cq-tags-property}

A propriedade `cq:tags` é uma matriz `String` usada para armazenar um ou mais `TagID`s quando eles são aplicados ao conteúdo por autores ou visitantes do site. A propriedade só tem significado quando adicionada a um nó definido com o mixin [`cq:Taggable`](#taggable-content-cq-taggable-mixin).

>[!NOTE]
>
>Para usar a funcionalidade de marcação do AEM, os aplicativos desenvolvidos e personalizados não devem definir propriedades de marca diferentes de `cq:tags`.

## Mover e mesclar tags {#moving-and-merging-tags}

Veja a seguir uma descrição dos efeitos no repositório ao mover ou mesclar tags usando o console Marcação.

Quando a marca A é movida ou mesclada na marca B em `/content/cq:tags`:

* A marca A não foi excluída e recebe uma propriedade `cq:movedTo`.
   * `cq:movedTo` pontos para a marca B.
   * Essa propriedade significa que a tag A foi movida ou mesclada na tag B.
   * Mover a tag B atualiza essa propriedade adequadamente.
   * A tag A fica oculta e só é mantida no repositório para que possa resolver IDs de tag em nós de conteúdo que apontem para a tag A.
   * O coletor de lixo da tag remove tags como a tag A assim que os nós de conteúdo não apontam mais para elas.
   * Um valor especial para a propriedade `cq:movedTo` é `nirvana`, que é aplicado quando a marca é excluída, mas não pode ser removida do repositório porque há submarcas com um `cq:movedTo` que deve ser mantido.

     >[!NOTE]
     >
     >A propriedade `cq:movedTo` só será adicionada à marca movida ou mesclada se qualquer uma destas condições for atendida:
     >
     > 1. A tag é usada no conteúdo (o que significa que tem uma referência). OU
     > 1. A tag tem filhos que já foram movidos.
     >
* A marca B é criada (se houver uma movimentação) e recebe uma propriedade `cq:backlinks`.
   * `cq:backlinks` mantém as referências na outra direção. Ou seja, ela mantém uma lista de todas as tags que foram movidas ou mescladas com a tag B.
   * Essa funcionalidade é necessária principalmente para manter as propriedades `cq:movedTo` atualizadas quando a tag B também é movida/mesclada/excluída ou quando a tag B é ativada, caso em que todas as tags de backlinks também devem ser ativadas.

     >[!NOTE]
     >
     >A propriedade `cq:backlinks` só será adicionada à marca movida ou mesclada se qualquer uma destas condições for atendida:
     >
     > 1. A tag for usada no conteúdo (o que significa que tem uma referência) ou
     > 1. A tag tem filhos que já foram movidos.

A leitura de uma propriedade `cq:tags` de um nó de conteúdo envolve a seguinte resolução:

1. Se não houver correspondência em `/content/cq:tags`, nenhuma tag será retornada.
1. Se a marca tiver um conjunto de propriedades `cq:movedTo`, a ID de marca referenciada será seguida.
   * Esta etapa será repetida desde que a marca seguida tenha uma propriedade `cq:movedTo`.
1. Se a marca seguida não tiver uma propriedade `cq:movedTo`, a marca será lida.

Para publicar a alteração quando uma marca for movida ou mesclada, o nó `cq:Tag` e todos os seus backlinks deverão ser replicados. Essa replicação é feita automaticamente quando a tag é ativada no console de administração de tags.

Atualizações posteriores na propriedade `cq:tags` da página limpam automaticamente as referências antigas. A limpeza é acionada porque a resolução de uma tag movida pela API retorna a tag de destino, fornecendo a ID da tag de destino.
