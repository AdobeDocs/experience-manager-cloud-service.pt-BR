---
title: Criação de tags em aplicativos AEM
description: Trabalhar programaticamente com tags ou estender tags em um aplicativo de AEM personalizado
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Criação de tags em aplicativos AEM {#building-tagging-into-aem-applications}

Para o objetivo de trabalhar programaticamente com tags ou estender tags em um aplicativo de AEM personalizado, este documento descreve o uso da variável

* [API de marcação](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

que interage com o

* [Estrutura de marcação](tagging-framework.md)

Para obter informações relacionadas à marcação:

* Consulte [Usar tags](/help/sites-cloud/authoring/features/tags.md) para obter informações sobre como marcar o conteúdo como um autor de conteúdo.
* Consulte Administração de tags para obter a perspectiva do administrador sobre como criar e gerenciar tags, bem como sobre quais tags de conteúdo foram aplicadas.

## Visão geral da API de marcação {#overview-of-the-tagging-api}

A implementação da [estrutura de marcação](tagging-framework.md) no AEM permite o gerenciamento de tags e conteúdo de tags usando a API JCR. `TagManager` garante que as tags inseridas como valores na propriedade da matriz da  `cq:tags` sequência de caracteres não sejam duplicadas, remove  `TagID`as tags apontadas para tags e atualizações não existentes  `TagID`para tags movidas ou mescladas. `TagManager` O usa um ouvinte de observação JCR que reverte quaisquer alterações incorretas. As classes principais estão no pacote [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html):

* `JcrTagManagerFactory` - retorna uma implementação baseada em JCR de um  `TagManager`. É a implementação de referência da API de marcação.
* `TagManager` - permite resolver e criar tags por caminhos e nomes.
* `Tag` - define o objeto da tag.

### Obter um TagManager baseado em JCR {#getting-a-jcr-based-tagmanager}

Para recuperar uma instância `TagManager`, você precisa ter um JCR `Session` e chamar `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

No contexto típico do Sling, você também pode adaptar a um `TagManager` do `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperação de um objeto de tag {#retrieving-a-tag-object}

Um `Tag` pode ser recuperado por meio do `TagManager`, resolvendo uma tag existente ou criando uma nova:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para a implementação baseada em JCR, que mapeia `Tags` para JCR `Nodes`, você pode usar diretamente o mecanismo `adaptTo` do Sling se tiver o recurso (por exemplo, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Embora uma tag possa ser convertida somente *de* um recurso (não um nó), uma tag pode ser convertida *para* tanto em um nó quanto em um recurso:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Não é possível adaptar diretamente de `Node` a `Tag`, porque `Node` não implementa o método Sling `Adaptable.adaptTo(Class)`.

### Obter e definir tags {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Pesquisar por tags {#searching-for-tags}

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
>O `RangeIterator` válido a ser usado é:
>
>`com.day.cq.commons.RangeIterator`

### Exclusão de tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replicação de tags {#replicating-tags}

É possível usar o serviço de replicação (`Replicator`) com tags porque elas são do tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## O Coletor de lixo de tags {#the-tag-garbage-collector}

O coletor de lixo da tag é um serviço em segundo plano que limpa as tags ocultas e não utilizadas. Tags ocultas e não utilizadas são tags abaixo de `/content/cq:tags` que têm uma propriedade `cq:movedTo` e não são usadas em um nó de conteúdo. Eles têm uma contagem de zero. Ao usar esse processo de exclusão lento, o nó de conteúdo (ou seja, a propriedade `cq:tags` ) não precisa ser atualizado como parte da operação de movimentação ou mesclagem. As referências na propriedade `cq:tags` são atualizadas automaticamente quando a propriedade `cq:tags` é atualizada, por exemplo, por meio da caixa de diálogo de propriedades da página.

O coletor de lixo da tag é executado por padrão uma vez por dia. Isso pode ser configurado em:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Pesquisa de tags e Lista de tags {#tag-search-and-tag-listing}

A pesquisa por tags e a listagem de tags funcionam da seguinte maneira:

* A pesquisa por `TagID` pesquisa as tags que têm a propriedade `cq:movedTo` definida como `TagID` e segue pelos `cq:movedTo` `TagID`s.
* A pesquisa pelo título da tag pesquisa somente as tags que não têm uma propriedade `cq:movedTo` .

## Tags em diferentes idiomas {#tags-in-different-languages}

Uma tag `title` pode ser definida em idiomas diferentes. Uma propriedade sensível ao idioma é então adicionada ao nó da tag. Essa propriedade tem o formato `jcr:title.<locale>`, por exemplo `jcr:title.fr` para a tradução em francês. `<locale>` deve ser uma sequência de caracteres de localidade ISO em letras minúsculas e usar sublinhado (`_`) em vez de hífen/traço (`-`), por exemplo:  `de_ch`.

Por exemplo, quando a tag **Animais** é adicionada à página **Produtos**, o valor `stockphotography:animals` é adicionado à propriedade `cq:tags` do nó `/content/wknd/en/products/jcr:content`. A tradução é referenciada a partir do nó da tag .

A API do lado do servidor localizou `title` métodos relacionados:

* [`com.day.cq.tagging.Tag`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

No AEM, o idioma pode ser obtido no idioma da página ou no idioma do usuário.

Para marcação, a localização depende do contexto, pois a tag `titles` pode ser exibida no idioma da página, no idioma do usuário ou em qualquer outro idioma.

### Adicionar um novo idioma à caixa de diálogo Editar tag {#adding-a-new-language-to-the-edit-tag-dialog}

O procedimento a seguir descreve como adicionar um novo idioma (por exemplo, finlandês) à caixa de diálogo **Tag Edit**:

1. Em **CRXDE**, edite a propriedade de vários valores `languages` do nó `/content/cq:tags`.
1. Adicione `fi_fi`, que representa a localidade finlandesa, e salve as alterações.

O finlandês agora está disponível na caixa de diálogo tag das propriedades da página e na caixa de diálogo **Editar tag** ao editar uma tag no console **Marcação**.

>[!NOTE]
>
>O novo idioma precisa ser um dos idiomas reconhecidos AEM, ou seja, precisa estar disponível como um nó abaixo de `/libs/wcm/core/resources/languages`.
