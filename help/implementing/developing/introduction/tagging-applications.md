---
title: Criação de tags em aplicativos do AEM
description: Trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Criação de tags em aplicativos do AEM {#building-tagging-into-aem-applications}

Para fins de trabalho programático com tags ou extensão de tags em um aplicativo AEM personalizado, este documento descreve o uso da

* [API de marcação](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

que interage com o

* [Estrutura de marcação](tagging-framework.md)

Para obter informações relacionadas à marcação:

* Consulte [Uso de tags](/help/sites-cloud/authoring/sites-console/tags.md) para obter informações sobre como marcar conteúdo como autor de conteúdo.
* Consulte Administração de tags para obter a perspectiva de um administrador sobre a criação e o gerenciamento de tags e a quais tags de conteúdo foram aplicadas.

## Visão geral da API de marcação {#overview-of-the-tagging-api}

A execução do [estrutura de marcação](tagging-framework.md) no AEM permite o gerenciamento de tags e conteúdo de tags usando a API JCR. `TagManager` garante que as tags sejam inseridas como valores na variável `cq:tags` as propriedades da matriz de cadeias de caracteres não estão duplicadas, ela remove `TagID`s apontando para tags e atualizações não existentes `TagID`s para tags movidas ou mescladas. `TagManager` O usa um ouvinte de observação JCR que reverte quaisquer alterações incorretas. As classes principais estão na [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html) pacote:

* `JcrTagManagerFactory` - retorna uma implementação baseada em JCR de um `TagManager`. É a implementação de referência da API de marcação.
* `TagManager` - permite a resolução e a criação de tags por caminhos e nomes.
* `Tag` - define o objeto de tag.

### Obter um TagManager baseado em JCR {#getting-a-jcr-based-tagmanager}

Para recuperar um `TagManager` instância, é necessário ter um JCR `Session` e para chamar `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

No contexto Sling típico, também é possível adaptar a uma `TagManager` do `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperação de um objeto de tag {#retrieving-a-tag-object}

A `Tag` pode ser recuperado por meio da variável `TagManager`, resolvendo uma tag existente ou criando uma:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para a implementação baseada em JCR, que mapeia `Tags` no JCR `Nodes`, você pode usar o do Sling diretamente `adaptTo` mecanismo se você tiver o recurso (por exemplo, como `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Embora uma tag só possa ser convertida *de* um recurso (não um nó), uma tag pode ser convertida *para* um nó e um recurso:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Adaptando-se diretamente do `Node` para `Tag` não é possível, porque `Node` não implementa o Sling `Adaptable.adaptTo(Class)` método.

### Obter e definir tags {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags (resource);

// Setting tags to a Resource:
tagManager.setTags (resource, tags);
```

### Pesquisando tags {#searching-for-tags}

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
>O válido `RangeIterator` usar é:
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

## O coletor de lixo da tag {#the-tag-garbage-collector}

O coletor de lixo da tag é um serviço em segundo plano que limpa as tags ocultas e não usadas. Tags ocultas e não usadas são as tags abaixo `/content/cq:tags` que tenham um `cq:movedTo` e não são usados em um nó de conteúdo. Elas têm uma contagem de zero. Ao usar esse processo de exclusão lento, o nó de conteúdo (ou seja, o `cq:tags` ) não precisa ser atualizada como parte da operação de mover ou mesclar. As referências no `cq:tags` são atualizados automaticamente quando a variável `cq:tags` A propriedade do é atualizada, por exemplo, por meio da caixa de diálogo de propriedades da página.

O coletor de lixo da tag é executado por padrão uma vez por dia. Isso pode ser configurado em:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Pesquisa de tags e listagem de tags {#tag-search-and-tag-listing}

A pesquisa de tags e a listagem de tags funcionam da seguinte maneira:

* A pesquisa por `TagID` O pesquisa as tags que têm a propriedade `cq:movedTo` definir como `TagID` e prossegue através do `cq:movedTo` `TagID`s
* A pesquisa por título de tag pesquisa somente tags que não têm um `cq:movedTo` propriedade.

## Tags em diferentes idiomas {#tags-in-different-languages}

Uma tag `title` podem ser definidos em diferentes idiomas. Em seguida, uma propriedade que diferencia idiomas é adicionada ao nó da tag. Essa propriedade tem o formato `jcr:title.<locale>`, por exemplo, `jcr:title.fr` pela tradução francesa. `<locale>` deve ser uma sequência de caracteres de localidade ISO em minúsculas e usar sublinhado (`_`) em vez de hífen/traço (`-`), por exemplo: `de_ch`.

Por exemplo, quando a variável **Animais** é adicionada à guia **Produtos** página, o valor `stockphotography:animals` é adicionado à propriedade `cq:tags` do nó `/content/wknd/en/products/jcr:content`. A tradução é referenciada a partir do nó da tag.

A API do lado do servidor localizou `title`Métodos relacionados ao:

* [`com.day.cq.tagging.Tag`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths ()`
   * `getLocalizedTitles ()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

No AEM, o idioma pode ser obtido no idioma da página ou no idioma do usuário.

Para marcação, a localização depende do contexto como tag `titles` pode ser exibido no idioma da página, no idioma do usuário ou em qualquer outro idioma.

### Adicionar um novo idioma à caixa de diálogo Editar tag {#adding-a-new-language-to-the-edit-tag-dialog}

O procedimento a seguir descreve como adicionar um novo idioma (por exemplo, finlandês) à **Editar tag** diálogo:

1. Entrada **CRXDE**, edite a propriedade de vários valores `languages` do nó `/content/cq:tags`.
1. Adicionar `fi_fi`, que representa o local da Finlândia, e salve as alterações.

O finlandês agora está disponível na caixa de diálogo de tag das propriedades da página e no **Editar tag** caixa de diálogo ao editar uma tag no **Marcação** console.

>[!NOTE]
>
>A nova língua deve ser uma das línguas reconhecidas pelo AEM. Ou seja, ele deve estar disponível como um nó abaixo `/libs/wcm/core/resources/languages`.
