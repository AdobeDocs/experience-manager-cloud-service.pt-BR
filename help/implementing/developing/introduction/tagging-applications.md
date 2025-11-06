---
title: Criação de tags em aplicativos do AEM
description: Trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado
exl-id: a106dce1-5d51-406a-a563-4dea83987343
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Criação de tags em aplicativos do AEM {#building-tagging-into-aem-applications}

Para trabalhar programaticamente com tags ou estender tags em um aplicativo AEM personalizado, este documento descreve o uso da

* [API de marcação](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

que interage com o

* [Estrutura de marcação](tagging-framework.md)

Para obter informações relacionadas à marcação:

* Consulte [Usando Tags](/help/sites-cloud/authoring/sites-console/tags.md) para obter informações sobre como marcar conteúdo como autor de conteúdo.
* Consulte Administração de tags para obter a perspectiva de um administrador sobre a criação e o gerenciamento de tags e a quais tags de conteúdo foram aplicadas.

## Visão geral da API de marcação {#overview-of-the-tagging-api}

A implementação da [estrutura de marcação](tagging-framework.md) no AEM permite o gerenciamento de tags e conteúdo de tags usando a API JCR. `TagManager` garante que as marcas inseridas como valores na propriedade de matriz da cadeia de caracteres `cq:tags` não sejam duplicadas, remove `TagID`s que apontam para marcas não existentes e atualiza `TagID`s para marcas movidas ou mescladas. `TagManager` usa um ouvinte de observação JCR que reverte quaisquer alterações incorretas. As classes principais estão no pacote [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html):

* `JcrTagManagerFactory` - retorna uma implementação baseada em JCR de um `TagManager`. É a implementação de referência da API de marcação.
* `TagManager` - permite resolver e criar marcas por caminhos e nomes.
* `Tag` - define o objeto de marca.

### Obter um TagManager baseado em JCR {#getting-a-jcr-based-tagmanager}

Para recuperar uma instância `TagManager`, é necessário ter um JCR `Session` e chamar `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

No contexto Sling típico, você também pode adaptar para um `TagManager` do `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperação de um objeto de tag {#retrieving-a-tag-object}

Um `Tag` pode ser recuperado por meio de `TagManager`, resolvendo uma marca existente ou criando uma:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para a implementação baseada em JCR, que mapeia `Tags` para JCR `Nodes`, você pode usar diretamente o mecanismo `adaptTo` do Sling se tiver o recurso (por exemplo, como `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Embora uma marca só possa ser convertida *de* um recurso (não um nó), uma marca pode ser convertida *em* tanto em um nó quanto em um recurso:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Adaptar diretamente de `Node` a `Tag` não é possível, porque `Node` não implementa o método Sling `Adaptable.adaptTo(Class)`.

### Obter e definir tags {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
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
>O `RangeIterator` válido a ser usado é:
>
>`com.day.cq.commons.RangeIterator`

### Exclusão de tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replicação de tags {#replicating-tags}

É possível usar o serviço de replicação (`Replicator`) com marcas porque elas são do tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## O coletor de lixo da tag {#the-tag-garbage-collector}

O coletor de lixo da tag é um serviço em segundo plano que limpa as tags ocultas e não usadas. Marcas ocultas e não usadas são marcas abaixo de `/content/cq:tags` que têm uma propriedade `cq:movedTo` e não são usadas em um nó de conteúdo. Elas têm uma contagem de zero. Ao usar esse processo de exclusão lento, o nó de conteúdo (ou seja, a propriedade `cq:tags`) não precisa ser atualizado como parte da operação de movimentação ou mesclagem. As referências na propriedade `cq:tags` são atualizadas automaticamente quando a propriedade `cq:tags` é atualizada, por exemplo, por meio da caixa de diálogo de propriedades da página.

O coletor de lixo da tag é executado por padrão uma vez por dia. Isso pode ser configurado em:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Pesquisa de tags e listagem de tags {#tag-search-and-tag-listing}

A pesquisa de tags e a listagem de tags funcionam da seguinte maneira:

* A pesquisa por `TagID` pesquisa as tags que têm a propriedade `cq:movedTo` definida como `TagID` e segue pelo `cq:movedTo` `TagID`s.
* A pesquisa por título de tag só pesquisa as tags que não têm uma propriedade `cq:movedTo`.

## Tags em diferentes idiomas {#tags-in-different-languages}

Uma marca `title` pode ser definida em diferentes idiomas. Em seguida, uma propriedade que diferencia idiomas é adicionada ao nó da tag. Essa propriedade tem o formato `jcr:title.<locale>`, por exemplo, `jcr:title.fr` para a tradução em francês. `<locale>` deve ser uma cadeia de caracteres de localidade ISO em letras minúsculas e usar sublinhado (`_`) em vez de hífen/traço (`-`), por exemplo: `de_ch`.

Por exemplo, quando a marca **Animais** é adicionada à página **Produtos**, o valor `stockphotography:animals` é adicionado à propriedade `cq:tags` do nó `/content/wknd/en/products/jcr:content`. A tradução é referenciada a partir do nó da tag.

A API do lado do servidor localizou métodos relacionados a `title`:

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

No AEM, o idioma pode ser obtido do idioma da página ou do idioma do usuário.

Para marcação, a localização depende do contexto, pois a marca `titles` pode ser exibida no idioma da página, no idioma do usuário ou em qualquer outro idioma.

### Adicionar um novo idioma à caixa de diálogo Editar tag {#adding-a-new-language-to-the-edit-tag-dialog}

O procedimento a seguir descreve como adicionar um novo idioma (por exemplo, finlandês) à caixa de diálogo **Editar tag**:

1. No **CRXDE**, edite a propriedade de vários valores `languages` do nó `/content/cq:tags`.
1. Adicione `fi_fi`, que representa a localidade finlandesa, e salve as alterações.

O finlandês agora está disponível na caixa de diálogo de marcas das propriedades da página e na caixa de diálogo **Editar Marca** ao editar uma marca no console **Marcação**.

>[!NOTE]
>
>O novo idioma deve ser um dos idiomas reconhecidos pela AEM. Ou seja, ele deve estar disponível como um nó abaixo de `/libs/wcm/core/resources/languages`.
