---
title: Fragmentos de conteúdo - Considerações sobre a exclusão
description: Analise essas considerações importantes antes de definir as políticas de exclusão de fragmentos de conteúdo no AEM. Os fragmentos de conteúdo são uma ferramenta eficiente para fornecer conteúdo headless, e as implicações de excluí-los devem ser cuidadosamente consideradas.
feature: Content Fragments
role: User
hide: true
index: false
hidefromtoc: true
exl-id: f6698dd8-3e2a-44ac-b00f-df578aa85ffe
source-git-commit: 5ce5746026c5683e79cdc1c9dc96804756321cdb
workflow-type: ht
source-wordcount: '469'
ht-degree: 100%

---

# Fragmentos de conteúdo - Considerações sobre a exclusão {#content-fragments-delete-considerations}

<!--
hide: yes
index: no
hidefromtoc: yes
-->

Analise essas considerações importantes antes de definir as políticas de exclusão de fragmentos de conteúdo no AEM. Os fragmentos de conteúdo são uma ferramenta eficiente para fornecer conteúdo headless, e as implicações de excluí-los devem ser cuidadosamente consideradas.

## Permissões — Excluir ou não excluir {#permissions-delete-or-not-delete}

A capacidade de excluir conteúdo é uma ferramenta poderosa, mas também perigosa, com muitos setores precisando restringir e controlar a distribuição desses privilégios.

Com relação às permissões de exclusão, os fragmentos de conteúdo devem ser considerados em dois níveis:

1. **O fragmento do conteúdo como uma única entidade.**

   * **Caso de uso**: um usuário que precisa editar/atualizar um fragmento de conteúdo **e excluir um fragmento inteiro**.
   * **Permissões**: a permissão de exclusão pode ser atribuída por meio do gerenciamento de usuários e/ou de grupos. <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **As várias entidades secundárias que compõem um fragmento de conteúdo; por exemplo, variações, nós secundários.**

   A operação básica do editor de fragmentos de conteúdo requer que esses elementos transitórios secundários possam ser excluídos. Por exemplo, ao manipular variações; também ao editar metadados ou gerenciar conteúdo associado.

   * **Caso de uso**: um usuário que precisa editar/atualizar um fragmento de conteúdo, mas **sem ter permissão para excluir um fragmento inteiro**.
   * **Permissões**: consulte [Permissões necessárias somente para funcionalidade de edição](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>Quando um usuário não tem permissões de exclusão, o editor de fragmento de conteúdo opera no modo *somente leitura*. <!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>Consulte também Como auditar operações de gerenciamento de usuários no AEM. <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## Permissões necessárias somente para funcionalidade de edição {#permissions-required-for-editor-functionality-only}

Para usuários que precisam editar/atualizar um fragmento de conteúdo, **sem permitir que excluam um fragmento inteiro**, permissões específicas devem ser atribuídas, já que a operação básica do editor de fragmentos de conteúdo requer que elementos transitórios secundários possam ser excluídos.

Por exemplo, ao manipular variações; também ao editar metadados ou gerenciar conteúdo associado.

>[!NOTE]
>
>As permissões de exclusão, necessárias para editar/atualizar um fragmento de conteúdo, estão incluídas na permissão de exclusão atribuída por meio do gerenciamento de usuários e/ou grupos. <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

As permissões necessárias para editar/atualizar um fragmento precisam ser aplicadas ao nó que contém o fragmento de conteúdo ou a um nó principal apropriado (em qualquer nível no `/content/dam`). Quando atribuídas a esse nó principal, as permissões são aplicadas a todos os nós dentro dessa ramificação.

Por exemplo, uma pasta que manterá todos os fragmentos de conteúdo, como:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>Definir as permissões em `/content/dam` também é possível, pois todos os fragmentos de conteúdo são armazenados aqui.
>
>No entanto, essa ação aplica as mesmas permissões de exclusão a *todos* os outros tipos de ativos também.

Os pré-requisitos de permissões para permitir que um usuário e/ou grupo específico edite/atualize um fragmento de conteúdo são:

>[!NOTE]
>
>Esta lista mostra todos os privilégios necessários, não apenas os privilégios de exclusão.

* Para os nós ou pastas do fragmento de conteúdo:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* Para o nó `jcr:content` de todos os fragmentos de conteúdo:

   * `jcr:addChildNodes`, `jcr:modifyProperties` e `jcr:removeChildNodes`

* Para todos os nós abaixo de `jcr:content` de todos os fragmentos de conteúdo:

   * `jcr:addChildNodes`, `jcr:modifyProperties` e `jcr:removeChildNodes`, `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
