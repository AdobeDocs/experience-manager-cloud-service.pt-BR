---
title: Criação de tags em aplicativos do AEM
description: Trabalhar programaticamente com tags ou estender tags em um aplicativo de AEM personalizado
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 1%

---

# Criação de tags em aplicativos do AEM {#building-tagging-into-aem-applications}

Para o objetivo de trabalhar programaticamente com tags ou estender tags em um aplicativo de AEM personalizado, este documento descreve o uso da variável

* [API de marcação](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

que interage com o

* [Estrutura de marcação](tagging-framework.md)

Para obter informações relacionadas à marcação:

* Consulte [Uso de tags](/help/sites-cloud/authoring/features/tags.md) para obter informações sobre como marcar conteúdo como um autor de conteúdo.
* Consulte Administração de tags para obter a perspectiva do administrador sobre como criar e gerenciar tags, bem como sobre quais tags de conteúdo foram aplicadas.

## Visão geral da API de marcação {#overview-of-the-tagging-api}

A aplicação do [estrutura de marcação](tagging-framework.md) no AEM permite o gerenciamento de tags e conteúdo de tags usando a API JCR. `TagManager` garante que as tags sejam inseridas como valores no `cq:tags` a propriedade da matriz de sequência de caracteres não está duplicada, ela remove `TagID`s apontando para tags e atualizações não existentes `TagID`s para tags movidas ou unidas. `TagManager` O usa um ouvinte de observação JCR que reverte quaisquer alterações incorretas. As classes principais estão no [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html) pacote:

* `JcrTagManagerFactory` - retorna uma implementação baseada em JCR de um `TagManager`. É a implementação de referência da API de marcação.
* `TagManager` - permite resolver e criar tags por caminhos e nomes.
* `Tag` - define o objeto da tag.

### Obter um TagManager baseado em JCR {#getting-a-jcr-based-tagmanager}

Para recuperar um `TagManager` , é necessário ter um JCR `Session` e para chamar `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

No contexto típico do Sling, você também pode se adaptar a um `TagManager` do `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperação de um objeto de tag {#retrieving-a-tag-object}

A `Tag` podem ser recuperadas por meio do `TagManager`, resolvendo uma tag existente ou criando uma nova:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para a implementação baseada em JCR, que mapeia `Tags` no JCR `Nodes`, você pode usar diretamente o Sling `adaptTo` mecanismo se você tiver o recurso (por exemplo, como `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Enquanto uma tag só pode ser convertida *from* um recurso (não um nó), uma tag pode ser convertida *para* um nó e um recurso:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Adaptação direta de `Node` para `Tag` não é possível, porque `Node` não implementa o Sling `Adaptable.adaptTo(Class)` método .

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
>O `RangeIterator` para usar é:
>
>`com.day.cq.commons.RangeIterator`

### Exclusão de tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replicação de tags {#replicating-tags}

É possível usar o serviço de replicação (`Replicator`) com tags, pois as tags são do tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## O Coletor de lixo de tags {#the-tag-garbage-collector}

O coletor de lixo da tag é um serviço em segundo plano que limpa as tags ocultas e não utilizadas. Tags ocultas e não usadas são tags abaixo `/content/cq:tags` que tenham uma `cq:movedTo` e não são usadas em um nó de conteúdo. Eles têm uma contagem de zero. Ao usar esse processo de exclusão lento, o nó de conteúdo (ou seja, o `cq:tags` ) não precisa ser atualizada como parte da operação de movimentação ou mesclagem. As referências no `cq:tags` são atualizadas automaticamente quando a variável `cq:tags` é atualizada, por exemplo, por meio da caixa de diálogo Propriedades da página.

O coletor de lixo da tag é executado por padrão uma vez por dia. Isso pode ser configurado em:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Pesquisa de tags e Lista de tags {#tag-search-and-tag-listing}

A pesquisa por tags e a listagem de tags funcionam da seguinte maneira:

* A pesquisa de `TagID` pesquisa as tags que têm a propriedade `cq:movedTo` defina como `TagID` e prossegue através da `cq:movedTo` `TagID`s.
* A pesquisa pelo título da tag pesquisa somente as tags que não têm uma `cq:movedTo` propriedade.

## Tags em diferentes idiomas {#tags-in-different-languages}

Uma tag `title` pode ser definido em idiomas diferentes. Uma propriedade sensível ao idioma é então adicionada ao nó da tag. Essa propriedade tem o formato `jcr:title.<locale>`, por exemplo, `jcr:title.fr` para a tradução em francês. `<locale>` deve ser uma sequência de caracteres de localidade ISO em letras minúsculas e usar sublinhado (`_`) em vez de hífen/traço (`-`), por exemplo: `de_ch`.

Por exemplo, quando a variável **Animais** é adicionada à variável **Produtos** página, o valor `stockphotography:animals` é adicionado à propriedade `cq:tags` do nó `/content/wknd/en/products/jcr:content`. A tradução é referenciada a partir do nó da tag .

A API do lado do servidor foi localizada `title`-métodos relacionados:

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

Para marcação, a localização depende do contexto como tag `titles` pode ser exibido no idioma da página, no idioma do usuário ou em qualquer outro idioma.

### Adicionar um novo idioma à caixa de diálogo Editar tag {#adding-a-new-language-to-the-edit-tag-dialog}

O procedimento a seguir descreve como adicionar um novo idioma (por exemplo, finlandês) ao **Editar tag** caixa de diálogo:

1. Em **CRXDE**, edite a propriedade de vários valores `languages` do nó `/content/cq:tags`.
1. Adicionar `fi_fi`, que representa a localidade finlandesa, e salva as alterações.

O finlandês agora está disponível na caixa de diálogo de tags das propriedades da página e no **Editar tag** ao editar uma tag no **Marcação** console.

>[!NOTE]
>
>O novo idioma precisa ser um dos idiomas reconhecidos AEM, ou seja, precisa estar disponível como um nó abaixo `/libs/wcm/core/resources/languages`.
