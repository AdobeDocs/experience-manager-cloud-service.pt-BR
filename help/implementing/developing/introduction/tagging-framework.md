---
title: Estrutura de marcação do AEM
description: Marque o conteúdo e aproveite a infraestrutura de marcação AEM para categorizá-lo e organizá-lo.
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 0%

---

# A estrutura de marcação AEM {#aem-tagging-framework}

A marcação permite que o conteúdo seja categorizado e organizado. As tags podem ser classificadas por um namespace e uma taxonomia. Para obter informações detalhadas sobre o uso de tags:

* Consulte [Uso de tags](/help/sites-cloud/authoring/features/tags.md) para obter informações sobre como marcar conteúdo como autor de conteúdo.
* Consulte Administração de tags para obter a perspectiva de um administrador sobre a criação e o gerenciamento de tags e sobre quais tags de conteúdo foram aplicadas.

Este artigo se concentra na estrutura subjacente que oferece suporte à marcação no AEM e em como aproveitá-lo como desenvolvedor.

## Introdução {#introduction}

Para marcar conteúdo e aproveitar a infraestrutura de marcação AEM:

* A tag deve existir como um nó do tipo [`cq:Tag`](#cq-tag-node-type) no [nó raiz de taxonomia.](#taxonomy-root-node)
* O do nó de conteúdo marcado `NodeType` deve incluir o [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* A variável [`TagID`](#tagid) é adicionado ao do nó de conteúdo [`cq:tags`](#cq-tags-property) propriedade e é resolvido para um nó do tipo [`cq:Tag`.](#cq-tag-node-type)

## cq:Tag Node Type {#cq-tag-node-type}

A declaração de uma tag é capturada no repositório em um nó do tipo `cq:Tag.`

* Uma tag pode ser uma palavra simples (por exemplo, `sky`) ou representam uma taxonomia hierárquica (por exemplo, `fruit/apple`, ou seja, a fruta genérica e a maçã mais específica).
* As tags são identificadas por um único `TagID`.
* Uma tag tem informações meta opcionais, como um título, títulos localizados e uma descrição. O título deve ser exibido nas interfaces do usuário, em vez da tag `TagID`, quando presente.

A estrutura de marcação também fornece a capacidade de restringir autores e visitantes do site a usar somente tags específicas e predefinidas.

### Características da tag {#tag-characteristics}

* O tipo de nó é `cq:Tag`.
* O nome do nó é um componente do [`TagID`.](#tagid)
* A variável [`TagID`](#tagid) sempre inclui um [namespace.](#tag-namespace)
* A variável `jcr:title` (o Título a ser exibido na interface do usuário) é opcional.
* A variável `jcr:description` é opcional.
* Ao conter nós filhos, é chamado de [tag container.](#container-tags)
* A tag é armazenada no repositório abaixo de um caminho base chamado de [nó raiz de taxonomia.](#taxonomy-root-node)

### TagID {#tagid}

A `TagID` identifica um caminho que é resolvido para um nó de tag no repositório.

Normalmente, a variável `TagID` é uma abreviação `TagID` começando com o namespace ou pode ser um valor absoluto `TagID` a partir do [nó raiz de taxonomia.](#taxonomy-root-node)

Quando o conteúdo for marcado, se ainda não existir, a variável [`cq:tags`](#cq-tags-property) é adicionada ao nó de conteúdo e à variável `TagID` é adicionado à propriedade do `String` valor da matriz.

A variável `TagID` consiste em um [namespace](#tag-namespace) seguido pelo local `TagID`. [Tags de contêiner](#container-tags) ter subtags que representam uma ordem hierárquica na taxonomia. Subtags podem ser usadas para fazer referência a tags como qualquer local `TagID`. Por exemplo, marcar conteúdo com `fruit` é permitida, mesmo se for uma tag container com subtags, como `fruit/apple` e `fruit/banana`.

### Nó raiz da taxonomia {#taxonomy-root-node}

O nó raiz da taxonomia é o caminho base para todas as tags no repositório. O nó raiz da taxonomia deve *não* ser um nó do tipo `cq:Tag`.

No AEM, o caminho base é `/content/cq:tags` e o nó raiz é do tipo `cq:Folder`.

### Namespace da tag {#tag-namespace}

Os namespaces permitem agrupar itens. O caso de uso mais comum é ter um namespace por site (por exemplo, público versus interno) ou por aplicativo maior (por exemplo, Sites ou Assets), mas os namespaces podem ser usados para várias outras necessidades. Os namespaces são usados na interface para mostrar apenas o subconjunto de tags (ou seja, tags de um determinado namespace) que é aplicável ao conteúdo atual.

O namespace da tag é o primeiro nível na subárvore de taxonomia, que é o nó imediatamente abaixo de [nó raiz de taxonomia.](#taxonomy-root-node) Um namespace é um nó do tipo `cq:Tag` cujo pai não é um `cq:Tag` tipo de nó.

Todas as tags têm um namespace. Se nenhum namespace for especificado, a tag será atribuída ao namespace padrão, que é `TagID` `default`, ou seja, `/content/cq:tags/default`.  O padrão do Título é `Standard Tags`nesses casos.

### Tags de contêiner {#container-tags}

Uma tag container é um nó do tipo `cq:Tag` que contém qualquer número e tipo de nós secundários, o que permite aprimorar o modelo de tag com metadados personalizados.

Além disso, as tags de contêiner (ou supertags) em uma taxonomia servem como a subsoma de todas as subtags: por exemplo, conteúdo marcado com `fruit/apple` é considerado marcado com `fruit` também, ou seja, a pesquisa de conteúdo marcado com `fruit` também localizaria o conteúdo marcado com `fruit/apple`.

### Resolvendo TagIDs {#resolving-tagids}

Se a ID da tag contiver dois pontos (`:`), os dois pontos separam o namespace da tag ou subtaxonomia, que são então separadas por barras normais (`/`). Se a ID da tag não tiver dois pontos, o namespace padrão será implícito.

O local padrão e único das tags é abaixo de `/content/cq:tags`.

Tags que fazem referência a caminhos ou caminhos não existentes que não apontam para um `cq:Tag` são considerados inválidos e são ignorados.

A tabela a seguir mostra algumas amostras `TagID`s, seus elementos e como o `TagID` resolve para um caminho absoluto no repositório:

| `TagID` | Namespace | ID local | Tag(s) de contêiner | Tag de folha | Caminho absoluto da tag do repositório |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (nenhuma) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (nenhuma) | (nenhuma) | (nenhuma) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Localização do título da tag {#localization-of-tag-title}

Quando a tag inclui a string de título opcional `jcr:title`, é possível localizar o título para exibição adicionando a propriedade `jcr:title.<locale>`.

Para obter mais detalhes, consulte:

* [Tags em diferentes idiomas,](tagging-applications.md#tags-in-different-languages) que descreve o uso das APIs como um desenvolvedor
* Gerenciamento de tags em diferentes idiomas, que descreve o uso do console de marcação como administrador

### Controle de acesso {#access-control}

As tags existem como nós no repositório, na variável [nó raiz de taxonomia.](#taxonomy-root-node) Permitir ou negar que autores e visitantes do site criem tags em um determinado namespace pode ser obtido definindo ACLs apropriadas no repositório.

Negar permissões de leitura para determinadas tags ou namespaces controlará a capacidade de aplicar tags a um conteúdo específico.

Uma prática típica inclui:

* Permitindo que o `tag-administrators` acesso de gravação de grupo/função a todos os namespaces (adicionar/modificar em `/content/cq:tags`). Esse grupo vem com AEM pronto para uso.
* Permitir que usuários/autores leiam todos os namespaces que devem ser legíveis para eles (principalmente todos).
* Permitir que usuários/autores gravem acesso aos namespaces em que as tags devem ser definidas livremente por usuários/autores (`add_node` em `/content/cq:tags/some_namespace`)

## Conteúdo Marcável : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Para que os desenvolvedores de aplicativos anexem a marcação a um tipo de conteúdo, o registro ([CND](https://jackrabbit.apache.org/node-type-notation.html)) devem incluir a `cq:Taggable` mixin ou o `cq:OwnerTaggable` mixin.

A variável `cq:OwnerTaggable` mixin, que herda de `cq:Taggable`, destina-se a indicar que o conteúdo pode ser classificado pelo proprietário/autor. No AEM, é apenas um atributo do `cq:PageContent` nó. A variável `cq:OwnerTaggable` O mixin não é exigido pela estrutura de marcação.

>[!NOTE]
>
>É recomendável ativar tags somente no nó de nível superior de um item de conteúdo agregado (ou em sua `jcr:content` nó). Os exemplos incluem:
>
>* Páginas (`cq:Page`) em que o `jcr:content`o nó é do tipo `cq:PageContent`, que inclui a `cq:Taggable` mixin.
>* Ativos (`cq:Asset`) em que o `jcr:content/metadata` o nó sempre tem o `cq:Taggable` mixin.


### Notação de tipo de nó (CND) {#node-type-notation-cnd}

As definições de Tipo de nó existem no repositório como arquivos CND. A notação CND é definida como parte da variável [Documentação JCR.](https://jackrabbit.apache.org/node-type-notation.html).

As definições essenciais para os Tipos de nós incluídos no AEM são as seguintes:

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

A variável `cq:tags` propriedade é um `String` matriz usada para armazenar um ou mais `TagID`s quando são aplicados ao conteúdo por autores ou visitantes do site. A propriedade só tem significado quando adicionada a um nó definido com o [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.

>[!NOTE]
>
>Para aproveitar a funcionalidade de marcação AEM, os aplicativos desenvolvidos de forma personalizada não devem definir propriedades de tag diferentes de `cq:tags`.

## Mover e mesclar tags {#moving-and-merging-tags}

Veja a seguir uma descrição dos efeitos no repositório ao mover ou mesclar tags usando o console Marcação.

Quando a tag A é movida ou mesclada na tag B em `/content/cq:tags`:

* A tag A não é excluída e recebe um `cq:movedTo` propriedade.
   * `cq:movedTo` aponta para a tag B.
   * Essa propriedade significa que a tag A foi movida ou mesclada na tag B.
   * Mover a tag B atualizará essa propriedade adequadamente.
   * A tag A fica oculta e é mantida somente no repositório para resolver IDs de tag em nós de conteúdo que apontam para a tag A.
   * O coletor de lixo da tag remove tags como a tag A assim que os nós de conteúdo não apontam mais para elas.
   * Um valor especial para o `cq:movedTo` propriedade é `nirvana`, que é aplicado quando a tag é excluída, mas não pode ser removida do repositório porque há subtags com uma `cq:movedTo` que deve ser mantido.

      >[!NOTE]
      >
      >A variável `cq:movedTo` A propriedade só será adicionada à tag movida ou mesclada se qualquer uma dessas condições for atendida:
      >
      > 1. A tag é usada no conteúdo (o que significa que tem uma referência). OU
      > 1. A tag tem filhos que já foram movidos.

* A tag B é criada (no caso de uma movimentação) e recebe um `cq:backlinks` propriedade.
   * `cq:backlinks` mantém as referências na outra direção, ou seja, mantém uma lista de todas as tags que foram movidas para ou mescladas com a tag B.
   * Isso é necessário principalmente para manter `cq:movedTo` propriedades atualizadas quando a tag B é movida/mesclada/excluída ou quando a tag B é ativada, nesse caso, todas as tags de backlinks também devem ser ativadas.

      >[!NOTE]
      >
      >A variável `cq:backlinks` A propriedade só será adicionada à tag movida ou mesclada se qualquer uma dessas condições for atendida:
      >
      > 1. A tag é usada no conteúdo (o que significa que tem uma referência). OU
      > 1. A tag tem filhos que já foram movidos.


Ler um `cq:tags` A propriedade de um nó de conteúdo envolve a seguinte resolução:

1. Se não houver correspondência em `/content/cq:tags`, nenhuma tag é retornada.
1. Se a tag tiver uma `cq:movedTo` for definida, a ID da tag referenciada será seguida.
   * Esta etapa é repetida desde que a tag seguida tenha uma `cq:movedTo` propriedade.
1. Se a tag seguida não tiver um `cq:movedTo` propriedade, a tag será lida.

Para publicar a alteração quando uma tag tiver sido movida ou mesclada, a variável `cq:Tag` e todos os seus backlinks devem ser replicados. Isso é feito automaticamente quando a tag é ativada no console de administração de tags.

Atualizações posteriores no da página `cq:tags` propriedade automaticamente limpa as referências antigas. Isso é acionado porque a resolução de uma tag movida pela API retorna a tag de destino, fornecendo a ID da tag de destino.
