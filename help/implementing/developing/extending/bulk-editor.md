---
title: Configuração da edição de itens em massa das propriedades da página
description: Saiba como configurar a edição em massa para editar as propriedades de várias páginas de uma só vez.
exl-id: 0d10c6b9-8643-479d-adc1-4066d227e83d
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 1%

---

# Configuração da edição de itens em massa das propriedades da página {#configuring-bulk-editing-of-page-properties}

[A edição em massa das propriedades da página](/help/sites-cloud/authoring/sites-console/edit-page-properties.md#from-the-sites-console-multiple-pages) permite editar as propriedades de várias páginas de uma só vez.

## Considerações {#considerations}

As propriedades da página não estão ativadas para edição em massa como padrão. Eles devem ser ativados explicitamente. Ao definir as propriedades de página para que estejam disponíveis para edição de itens em massa, você precisa considerar certas implicações, como:

* Determinados campos geralmente são únicos. Você deve decidir se é significativo ativar esses campos para edição de itens em massa, quando um valor será aplicado.
   * Por exemplo, títulos de página são quase sempre exclusivos.
* Determinados campos podem ter vários valores que precisam de representação significativa ao renderizar.
   * Por exemplo, uma lista suspensa de status chamada **Pronto para publicação**. Isso pode ter vários valores antes da edição em massa, como **pronto**, **em revisão**, **em andamento**, e assim por diante.

Devido à possibilidade de vários valores, é recomendável habilitar apenas os seguintes tipos de campo para edição em massa.

* `/libs/granite/ui/components/foundation/form/textfield`
* `/libs/granite/ui/components/foundation/form/textarea`
* `/libs/granite/ui/components/foundation/form/tagspicker`
* `/libs/granite/ui/components/foundation/form/datepicker`
* `/libs/granite/ui/components/foundation/form/pathbrowser`
* `/libs/granite/ui/components/foundation/form/checkbox`

## Ativar um campo {#enabling-a-field}

Essas etapas usam o `/apps/core/wcm/components/page/v1/page` do [conteúdo de amostra do WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) como exemplo para habilitar a edição em massa em um campo em um ambiente de desenvolvimento.

1. Usando o CRXDE, abra o componente de página.
1. Navegue até o campo obrigatório dentro da definição `cq:dialog`.
1. Defina a seguinte propriedade no nó do campo:

   * **Nome**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

1. Selecione **Salvar tudo** para manter suas atualizações.

## Limitações {#limitations}

A edição em massa das propriedades da página é:

* Não disponível para páginas em uma live copy.
* Disponível somente para páginas com o mesmo tipo de recurso.
