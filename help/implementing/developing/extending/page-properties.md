---
title: Personalização de exibições das propriedades da página
description: Saiba como as propriedades de página são visualizadas e editadas pelos autores.
exl-id: 363b3c2d-f965-485f-bdae-2ea5b4cecb83
source-git-commit: d2352e66b380f5a3654e2fc99ce4204b32066683
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Personalização de exibições das propriedades da página{#customizing-views-of-page-properties}

Cada página tem um conjunto de [propriedades](/help/sites-cloud/authoring/sites-console/page-properties.md) que podem ser visualizadas e editadas pelos usuários. Algumas são necessárias ao criar a página (criar exibição), outras podem ser visualizadas e editadas (editar exibição) em um estágio posterior. Essas propriedades da página são definidas e disponibilizadas pela caixa de diálogo (`cq:dialog`) do componente de página apropriado.

O estado padrão de cada propriedade de página é:

* Oculto na visualização de criação (por exemplo, **Criar página** assistente)

* Disponível na visualização de edição (por exemplo, **Propriedades da exibição**)

Os campos devem ser configurados especificamente se qualquer alteração for necessária. Isso é feito usando as propriedades apropriadas do nó:

* A propriedade da página que estará disponível na visualização de criação (por exemplo, **Criar página** assistente):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* A propriedade da página a estar disponível na visualização de edição, como a **Exibir**/**Editar**  **Propriedades** opção:

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

>[!TIP]
>
>Consulte a [Tutorial de extensão das propriedades da página](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) para obter um guia sobre como personalizar as propriedades da página.

## Configuração das propriedades da página {#configuring-your-page-properties}

Você também pode configurar os campos disponíveis configurando a caixa de diálogo do componente de página e aplicando as propriedades de nó apropriadas.

Por exemplo, por padrão, a variável [**Criar página** assistente](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page) mostra os campos agrupados em **Mais títulos e descrições**. Para ocultá-los, você configura:

1. Crie seu componente de página em `/apps`.
1. Criar uma substituição (usando *diff da caixa de diálogo* fornecido pelo [Fusão de recursos do Sling](/help/implementing/developing/introduction/sling-resource-merger.md)) para o `basic` do seu componente de página; por exemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. Defina o `path` propriedade em `basic` para apontar para a substituição da guia básica (consulte a próxima etapa também). Por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Criar uma substituição de `basic` - `moretitles` no caminho correspondente; por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique a propriedade do nó apropriada:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**: `false`

   A variável **Mais títulos e descrições** A seção não será mais exibida na **Criar página** assistente.

>[!NOTE]
>
>Ao configurar propriedades de página para uso com live copies, consulte [Extensão do gerenciador de vários sites](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) para obter mais detalhes.

## Exemplo de configuração das propriedades da página {#sample-configuration-of-page-properties}

Esta amostra demonstra a técnica de diálogo diff do [Fusão de recursos do Sling](/help/implementing/developing/introduction/sling-resource-merger.md) incluindo a utilização de [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties). Ilustra igualmente a utilização de `cq:showOnCreate` e `cq:hideOnEdit`.

Você pode encontrar o código desta página em [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog).
