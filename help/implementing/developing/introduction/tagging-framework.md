---
title: Estrutura de marcação AEM
description: Marque o conteúdo e aproveite a infraestrutura de Marcação de AEM para categorizá-lo e organizá-lo.
translation-type: tm+mt
source-git-commit: 4bf023068aa69fb6b69c6f2443703ea2bbbf7d42
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---


# A estrutura de marcação AEM {#aem-tagging-framework}

A marcação permite que o conteúdo seja categorizado e organizado. As tags podem ser classificadas por uma namespace e uma taxonomia. Para obter informações detalhadas sobre o uso de tags:

* Consulte [Usando tags](/help/sites-cloud/authoring/features/tags.md) para obter informações sobre como marcar conteúdo como autor de conteúdo.
* Consulte Administração de tags para obter a perspectiva do administrador sobre como criar e gerenciar tags, bem como para quais tags de conteúdo foram aplicadas.

Este artigo foca na estrutura subjacente que suporta a marcação em AEM e como potencializá-la como um desenvolvedor.

## Introdução {#introduction}

Para marcar o conteúdo e aproveitar a infraestrutura de Marcação de AEM:

* A tag deve existir como um nó do tipo [`cq:Tag`](#cq-tag-node-type) no nó raiz de [taxonomia.](#taxonomy-root-node)
* O `NodeType` do nó de conteúdo marcado deve incluir a combinação [`cq:Taggable`](#taggable-content-cq-taggable-mixin).
* O [`TagID`](#tagid) é adicionado à propriedade [`cq:tags`](#cq-tags-property) do nó de conteúdo e é resolvido para um nó do tipo [`cq:Tag`.](#cq-tag-node-type)

## cq:Tipo de nó de tag {#cq-tag-node-type}

A declaração de uma tag é capturada no repositório em um nó do tipo `cq:Tag.`

* Uma tag pode ser uma palavra simples (por exemplo, `sky`) ou representam uma taxonomia hierárquica (por exemplo, `fruit/apple`, que significa tanto o fruto genérico como a maçã mais específica).
* As tags são identificadas por um `TagID` exclusivo.
* Uma tag tem informações meta opcionais, como um título, títulos localizados e uma descrição. O título deve ser exibido nas interfaces do usuário em vez de `TagID`, quando presente.

A estrutura de marcação também fornece a capacidade de restringir autores e visitantes do site a usar somente tags específicas e predefinidas.

### Características da tag {#tag-characteristics}

* O tipo de nó é `cq:Tag`.
* O nome do nó é um componente de [`TagID`.](#tagid)
* [`TagID`](#tagid) sempre inclui uma namespace [.](#tag-namespace)
* A propriedade `jcr:title` (o Título a ser exibido na interface do usuário) é opcional.
* A propriedade `jcr:description` é opcional.
* Ao conter nós filho, é chamado de tag [container.](#container-tags)
* A tag é armazenada no repositório abaixo de um caminho base chamado [nó raiz de taxonomia.](#taxonomy-root-node)

### TagID {#tagid}

Um `TagID` identifica um caminho que é resolvido para um nó de tag no repositório.

Geralmente, `TagID` é um `TagID` abreviado que começa com a namespace ou pode ser um `TagID` absoluto a partir do nó raiz de [taxonomia.](#taxonomy-root-node)

Quando o conteúdo é marcado, se ainda não existir, a propriedade [`cq:tags`](#cq-tags-property) é adicionada ao nó de conteúdo e `TagID` é adicionada ao valor da matriz `String` da propriedade.

O `TagID` consiste em uma [namespace](#tag-namespace) seguida pelo `TagID` local. [Container ](#container-tags) tagshave subtags que representam uma ordem hierárquica na taxonomia. As subtags podem ser usadas para referenciar tags como qualquer `TagID` local. Por exemplo, marcar conteúdo com `fruit` é permitido, mesmo que seja uma tag de container com subtags, como `fruit/apple` e `fruit/banana`.

### Nó raiz de taxonomia {#taxonomy-root-node}

O nó raiz de taxonomia é o caminho base para todas as tags no repositório. O nó raiz de taxonomia deve *e não* ser um nó do tipo `cq:Tag`.

No AEM, o caminho base é `/content/cq:tags` e o nó raiz é do tipo `cq:Folder`.

### Namespace de tags {#tag-namespace}

Namespaces permitem agrupar itens. O caso de uso mais comum é ter uma namespace por site (por exemplo, público versus interno) ou por aplicativo maior (por exemplo, Sites ou Ativos), mas as namespaces podem ser usadas para várias outras necessidades. As namespaces são usadas na interface do usuário para mostrar apenas o subconjunto de tags (ou seja, tags de determinada namespace) que se aplica ao conteúdo atual.

A namespace da tag é o primeiro nível na subárvore de taxonomia, que é o nó imediatamente abaixo do nó raiz de [taxonomia.](#taxonomy-root-node) Uma namespace é um nó do tipo  `cq:Tag` cujo pai não é um tipo de  `cq:Tag` nó.

Todas as tags têm uma namespace. Se nenhuma namespace for especificada, a tag será atribuída à namespace padrão, que é `TagID` `default`, ou seja, `/content/cq:tags/default`.  Nesses casos, o padrão do Título é `Standard Tags`.

### Tags de container {#container-tags}

Uma tag de container é um nó do tipo `cq:Tag` que contém qualquer número e tipo de nós secundários, o que permite aprimorar o modelo de tag com metadados personalizados.

Além disso, as tags de container (ou super tags) em uma taxonomia servem como subsoma de todas as subtags: por exemplo, o conteúdo marcado com `fruit/apple` também é considerado marcado com `fruit`, isto é, procurar por conteúdo marcado com `fruit` também encontraria o conteúdo marcado com `fruit/apple`.

### Resolvendo TagIDs {#resolving-tagids}

Se a ID da tag contiver dois pontos (`:`), os dois pontos separarão a namespace da tag ou da subtaxonomia, que são então separados por barras normais (`/`). Se a ID da tag não tiver dois pontos, a namespace padrão será implícita.

O local padrão e único das tags está abaixo de `/content/cq:tags`.

As tags que fazem referência a caminhos ou caminhos não existentes que não apontam para um nó `cq:Tag` são consideradas inválidas e são ignoradas.

A tabela a seguir mostra algumas amostras `TagID`s, seus elementos e como `TagID` é resolvido para um caminho absoluto no repositório:

| `TagID` | Namespace | ID local | Tag(s) do container | Tag Folha | Caminho absoluto da tag do repositório |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (nenhum) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (nenhum) | (nenhum) | (nenhum) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Localização do título da tag {#localization-of-tag-title}

Quando a tag inclui a string de título opcional `jcr:title`, é possível localizar o título para exibição adicionando a propriedade `jcr:title.<locale>`.

Para obter mais detalhes, consulte:

* [Tags em diferentes idiomas, ](tagging-applications.md#tags-in-different-languages) que descreve o uso das APIs como desenvolvedor
* Gerenciamento de tags em diferentes idiomas, que descreve o uso do console Marcação como administrador

### Controle de acesso {#access-control}

As tags existem como nós no repositório no nó raiz de [taxonomia.](#taxonomy-root-node) Permitir ou negar que autores e visitantes do site criem tags em uma determinada namespace pode ser alcançado ao configurar ACLs apropriadas no repositório.

Negar permissões de leitura para determinadas tags ou namespaces controlará a capacidade de aplicar tags a um conteúdo específico.

Uma prática típica inclui:

* Permitindo o acesso de gravação de `tag-administrators` grupo/função a todas as namespaces (adicione/modifique em `/content/cq:tags`). Este grupo vem com AEM prontos.
* Permitir que usuários/autores leiam acesso a todas as namespaces que deveriam ser legíveis para eles (na maioria das vezes, todas).
* Permitir que usuários/autores gravem acesso às namespaces nas quais as tags devem ser definidas livremente por usuários/autores (`add_node` em `/content/cq:tags/some_namespace`)

## Conteúdo marcável: cq:Mistura marcável {#taggable-content-cq-taggable-mixin}

Para que os desenvolvedores de aplicativos anexem a marcação a um tipo de conteúdo, o registro do nó ([CND](https://jackrabbit.apache.org/node-type-notation.html)) deve incluir a combinação `cq:Taggable` ou `cq:OwnerTaggable`.

A combinação `cq:OwnerTaggable`, que herda de `cq:Taggable`, serve para indicar que o conteúdo pode ser classificado pelo proprietário/autor. No AEM, é apenas um atributo do nó `cq:PageContent`. A combinação `cq:OwnerTaggable` não é exigida pela estrutura de marcação.

>[!NOTE]
>
>É recomendável ativar somente tags no nó de nível superior de um item de conteúdo agregado (ou em seu nó `jcr:content`). Os exemplos incluem:
>
>* Páginas (`cq:Page`) nas quais o nó `jcr:content`é do tipo `cq:PageContent`, que inclui a combinação `cq:Taggable`.
>* Ativos (`cq:Asset`) nos quais o nó `jcr:content/metadata` sempre tem a combinação `cq:Taggable`.


### Notação de tipo de nó (CND) {#node-type-notation-cnd}

As definições de Tipo de nó existem no repositório como arquivos CND. A notação CND é definida como parte da documentação [JCR.](https://jackrabbit.apache.org/node-type-notation.html).

As definições essenciais para os tipos de nó incluídos no AEM são as seguintes:

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

## cq:tags Property {#cq-tags-property}

A propriedade `cq:tags` é uma matriz `String` usada para armazenar um ou mais `TagID`s quando são aplicados ao conteúdo por autores ou visitantes do site. A propriedade só tem significado quando adicionada a um nó definido com a combinação [`cq:Taggable`](#taggable-content-cq-taggable-mixin).

>[!NOTE]
>
>Para aproveitar AEM funcionalidade de marcação, os aplicativos desenvolvidos personalizados não devem definir propriedades de tags diferentes de `cq:tags`.

## Mover e mesclar tags {#moving-and-merging-tags}

A seguir está uma descrição dos efeitos no repositório ao mover ou mesclar tags usando o console Marcação.

Quando a tag A é movida ou unida na tag B sob `/content/cq:tags`:

* A tag A não é excluída e recebe uma propriedade `cq:movedTo`.
   * `cq:movedTo` aponta para a tag B.
   * Essa propriedade significa que a tag A foi movida ou mesclada para a tag B.
   * Mover a tag B atualizará essa propriedade de acordo.
   * A tag A fica então oculta e é mantida somente no repositório para resolver IDs de tag em nós de conteúdo que apontam para a tag A.
   * O coletor de lixo de tags remove tags como a tag A, uma vez que nenhum nó de conteúdo aponta para elas.
   * Um valor especial para a propriedade `cq:movedTo` é `nirvana`, que é aplicado quando a tag é excluída, mas não pode ser removida do repositório porque há subtags com `cq:movedTo` que devem ser mantidas.

      >[!NOTE]
      >
      >A propriedade `cq:movedTo` só será adicionada à tag movida ou unida se uma dessas condições for atendida:
      >
      > 1. A tag é usada no conteúdo (o que significa que ela tem uma referência). OU
      > 1. A tag tem filhos que já foram movidos.


* A tag B é criada (no caso de uma movimentação) e recebe uma propriedade `cq:backlinks`.
   * `cq:backlinks` mantém as referências na outra direção, isto é, mantém uma lista de todas as tags que foram movidas para ou mescladas com a tag B.
   * Isso é necessário principalmente para manter as propriedades `cq:movedTo` atualizadas quando a tag B também é movida/unida/excluída ou quando a tag B é ativada, nesse caso, todas as tags de backlinks também devem ser ativadas.

      >[!NOTE]
      >
      >A propriedade `cq:backlinks` só será adicionada à tag movida ou unida se uma dessas condições for atendida:
      >
      > 1. A tag é usada no conteúdo (o que significa que ela tem uma referência). OU
      > 1. A tag tem filhos que já foram movidos.


A leitura de uma propriedade `cq:tags` de um nó de conteúdo envolve a seguinte resolução:

1. Se não houver correspondência em `/content/cq:tags`, nenhuma tag será retornada.
1. Se a tag tiver uma propriedade `cq:movedTo` definida, a ID da tag referenciada será seguida.
   * Essa etapa é repetida, contanto que a tag seguida tenha uma propriedade `cq:movedTo`.
1. Se a tag seguida não tiver uma propriedade `cq:movedTo`, a tag será lida.

Para publicar a alteração quando uma tag tiver sido movida ou unida, o nó `cq:Tag` e todos os seus backlinks devem ser replicados. Isso é feito automaticamente quando a tag é ativada no console de administração de tags.

Atualizações posteriores para a propriedade `cq:tags` da página limpam automaticamente as referências antigas. Isso é acionado porque a resolução de uma tag movida pela API retorna a tag de destino, fornecendo assim a ID da tag de destino.
