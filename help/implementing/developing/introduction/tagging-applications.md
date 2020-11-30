---
title: Criação de tags em aplicativos AEM
description: Trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado
translation-type: tm+mt
source-git-commit: ce55065c3ae6a2350ed06811af76477df7c11291
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---


# Criação de tags em aplicativos AEM {#building-tagging-into-aem-applications}

Para a finalidade de trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado, este documento descreve o uso da variável

* [API de marcação](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

que interage com o

* [Estrutura de marcação](tagging-framework.md)

Para obter informações relacionadas à marcação:

* Consulte [Uso de tags](/help/sites-cloud/authoring/features/tags.md) para obter informações sobre como marcar conteúdo como um autor de conteúdo.
* Consulte Administração de tags para obter a perspectiva do administrador sobre como criar e gerenciar tags, bem como para quais tags de conteúdo foram aplicadas.

## Visão geral da API de marcação {#overview-of-the-tagging-api}

A implementação da estrutura [de](tagging-framework.md) marcação no AEM permite o gerenciamento de tags e do conteúdo de tags usando a API JCR. `TagManager` garante que as tags digitadas como valores na propriedade da matriz de `cq:tags` string não sejam duplicadas, ela remove `TagID`as tags apontadas para tags e atualizações não existentes `TagID`para tags movidas ou unidas. `TagManager` usa um ouvinte de observação JCR que reverte quaisquer alterações incorretas. As classes principais estão no pacote [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) :

* `JcrTagManagerFactory` - retorna uma implementação de uma `TagManager`. É a implementação de referência da API de marcação.
* `TagManager` - permite resolver e criar tags por caminhos e nomes.
* `Tag` - define o objeto de tag.

### Obtendo um TagManager baseado em JCR {#getting-a-jcr-based-tagmanager}

Para recuperar uma `TagManager` instância, é necessário ter um JCR `Session` e chamar `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

No contexto Sling típico, você também pode se adaptar a um `TagManager` dos `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Como recuperar um objeto de tag {#retrieving-a-tag-object}

Uma tag `Tag` pode ser recuperada pelo `TagManager`, resolvendo uma tag existente ou criando uma nova:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para a implementação baseada em JCR, que mapeia `Tags` para JCR `Nodes`, você pode usar diretamente o `adaptTo` mecanismo do Sling se tiver o recurso (por exemplo, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Embora uma tag possa ser convertida somente *de um recurso (não de um nó), uma tag pode ser convertida* em ** um nó e um recurso:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Não é possível adaptar diretamente de `Node` para, porque `Tag` não implementa o `Node` `Adaptable.adaptTo(Class)` método Sling.

### Obtendo e configurando tags {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Pesquisando por tags {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>O uso válido `RangeIterator` é:
>
>`com.day.cq.commons.RangeIterator`

### Excluindo tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replicação de tags {#replicating-tags}

É possível usar o serviço de replicação (`Replicator`) com tags, pois elas são do tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## O Coletor de Lixo da Etiqueta {#the-tag-garbage-collector}

O coletor de lixo de tags é um serviço em segundo plano que limpa as tags que estão ocultas e não são usadas. As tags ocultas e não usadas são tags abaixo `/content/cq:tags` que têm uma `cq:movedTo` propriedade e não são usadas em um nó de conteúdo. Eles têm uma contagem zero. Ao usar esse processo de exclusão lento, o nó de conteúdo (ou seja, a `cq:tags` propriedade) não precisa ser atualizado como parte da operação de movimentação ou mesclagem. As referências na `cq:tags` propriedade são automaticamente atualizadas quando a `cq:tags` propriedade é atualizada, por exemplo, por meio da caixa de diálogo de propriedades da página.

O coletor de lixo da tag é executado por padrão uma vez por dia. Isso pode ser configurado em:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Pesquisa de tags e Lista de tags {#tag-search-and-tag-listing}

A pesquisa por tags e a listagem de tags funcionam da seguinte maneira:

* A pesquisa por `TagID` pesquisa as tags que têm a propriedade `cq:movedTo` definida como `TagID` e que seguem por `cq:movedTo` `TagID`s.
* A pesquisa pelo título da tag pesquisa somente as tags que não possuem uma `cq:movedTo` propriedade.

## Tags em diferentes idiomas {#tags-in-different-languages}

Uma tag `title` pode ser definida em idiomas diferentes. Uma propriedade sensível ao idioma é então adicionada ao nó da tag. Esta propriedade tem o formato `jcr:title.<locale>`, por exemplo, `jcr:title.fr` para a tradução em francês. `<locale>` deve ser uma sequência de caracteres de localidade ISO em minúsculas e usar sublinhado (`_`) em vez de hífen/traço (`-`), por exemplo: `de_ch`.

Por exemplo, quando a tag **Animais** é adicionada à página **Produtos** , o valor `stockphotography:animals` é adicionado à propriedade `cq:tags` do nó `/content/wknd/en/products/jcr:content`. A tradução é referenciada a partir do nó da tag.

A API do lado do servidor tem métodos localizados `title`relacionados:

* [`com.day.cq.tagging.Tag`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

Em AEM, o idioma pode ser obtido do idioma da página ou do idioma do usuário.

Para marcação, a localização depende do contexto, pois a tag `titles` pode ser exibida no idioma da página, no idioma do usuário ou em qualquer outro idioma.

### Adicionar um novo idioma à caixa de diálogo Editar tag {#adding-a-new-language-to-the-edit-tag-dialog}

O procedimento a seguir descreve como adicionar um novo idioma (por exemplo, finlandês) à caixa de diálogo Editar **** tag:

1. No **CRXDE**, edite a propriedade de vários valores `languages` do nó `/content/cq:tags`.
1. Adicione `fi_fi`, que representa a localidade finlandesa, e salve as alterações.

Finlandês agora está disponível na caixa de diálogo de tags das propriedades da página e na caixa de diálogo **Editar tag** ao editar uma tag no console **Marcação** .

>[!NOTE]
>
>A nova língua precisa ser uma das línguas reconhecidas AEM, ou seja, precisa estar disponível como um nó abaixo `/libs/wcm/core/resources/languages`.
