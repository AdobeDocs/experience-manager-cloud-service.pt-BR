---
title: Personalização de exibições das propriedades da página
description: Saiba como as propriedades de página são visualizadas e editadas pelos autores.
exl-id: 363b3c2d-f965-485f-bdae-2ea5b4cecb83
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Personalização de exibições das propriedades da página{#customizing-views-of-page-properties}

Cada página tem um conjunto de [propriedades](/help/sites-cloud/authoring/sites-console/page-properties.md) que podem ser visualizadas e editadas pelos usuários. Algumas são necessárias ao criar a página (criar exibição), outras podem ser visualizadas e editadas (editar exibição) em um estágio posterior. Essas propriedades de página são definidas e disponibilizadas pela caixa de diálogo (`cq:dialog`) do componente de página apropriado.

O estado padrão de cada propriedade de página é:

* Oculto na exibição de criação (por exemplo, **Criar página** assistente)

* Disponível na exibição de edição (por exemplo, **Propriedades de exibição**)

Os campos devem ser configurados especificamente se qualquer alteração for necessária. Isso é feito usando as propriedades apropriadas do nó:

* Propriedade da página a ser disponibilizada no modo de exibição de criação (por exemplo, assistente **Criar Página**):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* Propriedade da página a ser disponibilizada no modo de exibição de edição, como a opção **Exibir**/**Editar** **Propriedades**:

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

>[!TIP]
>
>Consulte o [tutorial Extensão das propriedades de página](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html?lang=pt-BR) para obter um guia sobre como personalizar as propriedades de página.

## Configuração das propriedades da página {#configuring-your-page-properties}

Você também pode configurar os campos disponíveis configurando a caixa de diálogo do componente de página e aplicando as propriedades de nó apropriadas.

Por exemplo, por padrão, o assistente [**Criar página**](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page) mostra os campos agrupados em **Mais títulos e descrições**. Para ocultá-los, você configura:

1. Crie seu componente de página em `/apps`.
1. Crie uma substituição (usando a *diff de caixa de diálogo* fornecida pelo [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md)) para a seção `basic` do seu componente de página; por exemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. Defina a propriedade `path` em `basic` para apontar para a substituição da guia básica (veja a próxima etapa também). Por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Crie uma substituição da seção `basic` - `moretitles` no caminho correspondente; por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique a propriedade do nó apropriada:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**: `false`

   A seção **Mais Títulos e Descrição** não será mais exibida no assistente **Criar Página**.

>[!NOTE]
>
>Ao configurar propriedades de página para uso com live copies, consulte [Estendendo o Gerenciador de Vários Sites](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) para obter mais detalhes.

## Exemplo de configuração das propriedades da página {#sample-configuration-of-page-properties}

Este exemplo demonstra a técnica de diálogo diff do [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md), incluindo o uso de [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties). Também ilustra o uso de `cq:showOnCreate` e `cq:hideOnEdit`.

Você pode encontrar o código desta página em [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog).
