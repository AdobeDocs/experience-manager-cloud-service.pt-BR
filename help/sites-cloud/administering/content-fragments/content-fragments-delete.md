---
title: Fragmentos de conteúdo - excluir considerações
description: Revise essas importantes considerações antes de definir as políticas de exclusão dos Fragmentos de conteúdo no AEM. Os Fragmentos de conteúdo são uma ferramenta poderosa para fornecer conteúdo sem interface, e as implicações de excluí-los devem ser cuidadosamente consideradas.
source-git-commit: a06024b4d4b6e5e750ed4c1e27f55283513b78a2
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 10%

---

# Fragmentos de conteúdo - excluir considerações {#content-fragments-delete-considerations}

Revise essas importantes considerações antes de definir as políticas de exclusão dos Fragmentos de conteúdo no AEM. Os Fragmentos de conteúdo são uma ferramenta poderosa para fornecer conteúdo sem interface, e as implicações de excluí-los devem ser cuidadosamente consideradas.

## Permissões - Excluir ou não excluir {#permissions-delete-or-not-delete}

A capacidade de excluir conteúdo é poderosa, mas potencialmente sensível, com muitos setores precisando restringir e controlar a distribuição desses privilégios.

Em relação às permissões de exclusão, os Fragmentos de conteúdo devem ser considerados em dois níveis:

1. **O Fragmento do conteúdo como uma única entidade.**

   * **Caso de uso**: Um usuário que precisa editar/atualizar um fragmento de conteúdo - **e excluir um fragmento inteiro**.
   * **Permissões**: A permissão Excluir pode ser atribuída por meio do Gerenciamento de usuários e/ou do Gerenciamento de grupos. <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **As várias subentidades que compõem um fragmento de conteúdo; por exemplo, variações, subnós.**

   A operação básica do editor de fragmentos de conteúdo requer que esses subelementos transitórios possam ser excluídos. Por exemplo, ao manipular variações; também ao editar metadados ou gerenciar conteúdo associado.

   * **Caso de uso**: Um usuário que precisa editar/atualizar um fragmento de conteúdo - **sem ter permissão para excluir um fragmento inteiro**.
   * **Permissões**: Consulte [Permissões necessárias somente para a funcionalidade do editor](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>Quando um usuário não tem permissões de exclusão, o editor de Fragmento de conteúdo opera em *somente leitura* modo. <!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>Consulte também Como auditar operações de gerenciamento de usuários em AEM. <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## Permissões necessárias somente para a funcionalidade do editor {#permissions-required-for-editor-functionality-only}

Para usuários que precisam editar/atualizar um fragmento de conteúdo, **sem permitir que excluam um fragmento inteiro**, permissões específicas devem ser atribuídas, já que a operação básica do editor de fragmentos de conteúdo requer que elementos transitórios secundários possam ser excluídos.

Por exemplo, ao manipular variações; também ao editar metadados ou gerenciar conteúdo associado.

>[!NOTE]
>
>As permissões de exclusão, necessárias para editar/atualizar um Fragmento de conteúdo, estão incluídas na permissão de exclusão atribuída por meio do Gerenciamento de usuários e/ou grupos. <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

As permissões necessárias para editar/atualizar um fragmento precisam ser aplicadas ao nó que contém o fragmento de conteúdo ou a um nó pai apropriado (em qualquer nível em `/content/dam`). Quando atribuídas a esse nó pai, as permissões serão aplicadas a todos os nós dentro dessa ramificação.

Por exemplo, uma pasta que manterá todos os fragmentos de conteúdo, como:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>Definir as permissões em `/content/dam` também é possível, pois todos os fragmentos de conteúdo são armazenados aqui.
>
>No entanto, essa ação aplica as mesmas permissões de exclusão a *all* outros tipos de ativos também.

Os pré-requisitos de permissões para permitir que um usuário e/ou grupo específico edite/atualize um fragmento de conteúdo são:

>[!NOTE]
>
>Esta lista mostra todos os privilégios necessários, não apenas os privilégios de exclusão.

* Para os nós ou pastas do Fragmento de conteúdo:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* Para o `jcr:content`nó de todos os Fragmentos de conteúdo:

   * `jcr:addChildNodes`, `jcr:modifyProperties` e `jcr:removeChildNodes`

* Para todos os nós abaixo `jcr:content` de todos os Fragmentos de conteúdo:

   * `jcr:addChildNodes`, `jcr:modifyProperties` e `jcr:removeChildNodes`, `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
