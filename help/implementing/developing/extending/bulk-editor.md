---
title: Configuração da edição de itens em massa das propriedades da página
description: Saiba como configurar a edição em massa para editar as propriedades de várias páginas de uma só vez.
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---


# Configuração da edição de itens em massa das propriedades da página {#configuring-bulk-editing-of-page-properties}

[Edição em massa das propriedades da página](/help/sites-cloud/authoring/fundamentals/page-properties.md#from-the-sites-console-multiple-pages) permite editar as propriedades de várias páginas de uma só vez.

## Considerações {#considerations}

As propriedades da página não estão ativadas para edição em massa como padrão. Eles devem ser ativados explicitamente. Ao definir as propriedades de página para que estejam disponíveis para edição de itens em massa, você precisa considerar certas implicações, como:

* Determinados campos geralmente são únicos. Você deve decidir se é significativo ativar esses campos para edição de itens em massa, quando um valor será aplicado.
   * Por exemplo, títulos de página são quase sempre exclusivos.
* Determinados campos podem ter vários valores que precisam de representação significativa ao renderizar.
   * Por exemplo, uma lista suspensa de status chamada **Pronto para publicação**. Isso pode ter vários valores antes da edição em massa, como **pronto**, **em revisão**, **em andamento**, etc.

Devido à possibilidade de vários valores, é recomendável habilitar apenas os seguintes tipos de campo para edição em massa.

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## Ativar um campo {#enabling-a-field}

Essas etapas usam o `/apps/core/wcm/components/page/v1/page` do [Conteúdo de amostra do WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) como exemplo para permitir a edição em massa em um campo em um ambiente de desenvolvimento.

1. Usando o CRXDE, abra o componente de página.
1. Navegue até o campo obrigatório na `cq:dialog` definição.
1. Defina a seguinte propriedade no nó do campo:

   * **Nome**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

1. Selecionar **Salvar tudo** para continuar com suas atualizações.

## Limitações {#limitations}

A edição em massa das propriedades da página é:

* Não disponível para páginas em uma live copy.
* Disponível somente para páginas com o mesmo tipo de recurso.
