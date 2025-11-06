---
title: Fragmentos de conteúdo - Considerações sobre a exclusão
description: Analise essas considerações importantes antes de definir as políticas de exclusão de fragmentos de conteúdo no AEM. Os fragmentos de conteúdo são uma ferramenta eficiente para fornecer conteúdo headless, e as implicações de excluí-los devem ser cuidadosamente consideradas.
feature: Content Fragments
role: User, Developer
exl-id: d1726bff-3aa8-4758-bee7-0cacea1f660a
solution: Experience Manager Sites
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 46%

---

# Excluir considerações para fragmentos de conteúdo {#delete-considerations-content-fragments}

Analise essas considerações importantes antes de definir as políticas de exclusão de fragmentos de conteúdo no AEM. Os fragmentos de conteúdo são uma ferramenta eficiente para fornecer conteúdo headless, e as implicações de excluí-los devem ser cuidadosamente consideradas.

## Permissões — Excluir ou não excluir {#permissions-delete-or-not-delete}

A capacidade de excluir conteúdo é uma ferramenta poderosa, mas também perigosa, com muitos setores precisando restringir e controlar a distribuição desses privilégios.

Com relação às permissões de exclusão, os fragmentos de conteúdo devem ser considerados em dois níveis:

1. **O fragmento do conteúdo como uma única entidade.**

   * **Caso de uso**: um usuário que deve editar/atualizar um Fragmento de conteúdo - **e excluir um fragmento inteiro**.
   * **Permissões**: a permissão de exclusão pode ser atribuída por meio do gerenciamento de usuários e/ou grupos.

2. **As várias subentidades que compõem um Fragmento de Conteúdo; por exemplo, variações, subnós.**

   A operação básica do editor de Fragmento de conteúdo requer que esses subelementos transitórios possam ser excluídos. Por exemplo, ao manipular variações; também ao editar metadados ou gerenciar conteúdo associado.

   * **Caso de uso**: um usuário que deve editar/atualizar um Fragmento de conteúdo - **sem ter permissão para excluir um fragmento inteiro**.
   * **Permissões**: consulte [Permissões necessárias somente para funcionalidade de edição](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>Consulte também Como auditar operações de gerenciamento de usuários no AEM.

## Permissões necessárias somente para funcionalidade de edição {#permissions-required-for-editor-functionality-only}

Para usuários que precisam editar/atualizar um fragmento de conteúdo, **sem permitir que excluam um fragmento inteiro**, permissões específicas devem ser atribuídas, já que a operação básica do editor de fragmentos de conteúdo requer que subelementos transitórios possam ser excluídos.

Por exemplo, ao manipular variações; também ao editar metadados ou gerenciar conteúdo associado.

>[!NOTE]
>
>As permissões de exclusão, necessárias para editar/atualizar um fragmento de conteúdo, estão incluídas na permissão de exclusão atribuída por meio do gerenciamento de usuários e/ou grupos.

As permissões necessárias para editar/atualizar um fragmento devem ser aplicadas ao nó que contém o Fragmento de conteúdo ou a um nó principal apropriado (em qualquer nível em `/content/dam`). Quando atribuídas a esse nó principal, as permissões são aplicadas a todos os nós dentro dessa ramificação.

Por exemplo, uma pasta para armazenar todos os fragmentos de conteúdo, como:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>Definir as permissões em `/content/dam` também é possível, pois todos os Fragmentos de conteúdo são armazenados aqui.
>
>No entanto, essa ação aplica as mesmas permissões de exclusão a *todos* os outros tipos de ativos também.

Os pré-requisitos de permissões para permitir que um usuário e/ou grupo específico edite/atualize um Fragmento de conteúdo são:

>[!NOTE]
>
>Esta lista mostra todos os privilégios necessários, não apenas os privilégios de exclusão.

* Para os nós ou pastas do fragmento de conteúdo:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* Para o nó `jcr:content` de todos os fragmentos de conteúdo:

   * `jcr:addChildNodes`, `jcr:modifyProperties` e `jcr:removeChildNodes`

* Para todos os nós abaixo de `jcr:content` de todos os fragmentos de conteúdo:

   * `jcr:addChildNodes`, `jcr:modifyProperties`, e `jcr:removeChildNodes`, `jcr:removeNode`
