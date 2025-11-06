---
title: Configure o RTE para criar páginas da Web e sites acessíveis.
description: Saiba como configurar o Editor de Rich Text para criar sites acessíveis no [!DNL Adobe Experience Manager].
contentOwner: AG
exl-id: 54050fc9-0348-4033-8e2b-b3897588cb62
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 1%

---

# Configurar o RTE para criar sites acessíveis {#configure-rte-accessible-sites}

O [!DNL Adobe Experience Manager] oferece suporte a recursos de acessibilidade padrão, como texto alternativo para imagens e recursos adicionais que podem ser acessados ao criar conteúdo. Os autores de conteúdo usam esses recursos com componentes que usam o editor de rich text (RTE). Os recursos incluem a adição de texto alternativo, informações estruturais por meio de cabeçalhos e elementos de parágrafo, e assim por diante.

Para obter uma compreensão das configurações típicas do RTE, consulte [configurar o RTE](rich-text-editor.md) e [configurar plug-ins do RTE para a funcionalidade específica](configure-rich-text-editor-plug-ins.md).

Use a configuração dos plug-ins do RTE para configurar e personalizar os recursos relacionados à acessibilidade. Por exemplo, use `paraformat` para adicionar elementos semânticos extras de nível de bloco, incluindo a extensão do número de níveis de cabeçalho com suporte além dos `H1` básicos, `H2` e `H3` fornecidos por padrão. A edição de rich text é possível usando muitos componentes da interface do usuário de criação. Os componentes usados com frequência são texto, imagem, download e assim por diante.

A funcionalidade do RTE pode ser disponibilizada em muitos componentes. O componente principal é o componente `Text`.

Para o componente `Text` em [!DNL Experience Manager], a seguinte captura de tela exibe o editor de rich text com vários plug-ins habilitados, incluindo `paraformat`:

![Componente de texto do RTE no modo de tela cheia](assets/rte-toolbar-full-screen-mode.png)

## Configurar os recursos do plug-in {#configuring-the-plugin-features}

Para obter instruções sobre como configurar o RTE, consulte [configurar a página Editor de Rich Text](rich-text-editor.md). O artigo abrange:

* [Plug-ins e seus recursos](rich-text-editor.md#aboutplugins)
* [Locais de configuração](rich-text-editor.md#understand-the-configuration-paths-and-locations)
* [Ativar um plug-in e configurar a propriedade de recursos](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)
* [Configurar outras funcionalidades do RTE](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)

Para ativar alguns ou todos os recursos de um plug-in, configure o plug-in na sub-ramificação `rtePlugins` apropriada no CRXDE Lite.

![CRXDE Lite mostrando um exemplo de rtePlugin](assets/example-rteplugin-crxde-lite.png)

### Exemplo para especificar formatos de parágrafo disponíveis no campo de seleção de RTE {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Novos formatos de bloco semântico são disponibilizados para seleção.

1. Dependendo do seu RTE, determine e navegue até o [local de configuração](rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Habilite o campo de seleção de parágrafos](rich-text-editor.md) ao [ativar o plug-in](rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Especifique os formatos que deseja disponibilizar no campo de seleção de parágrafos](rich-text-editor.md).
1. Os formatos de parágrafo são disponibilizados ao autor de conteúdo a partir dos campos de seleção no RTE.

Com elementos estruturais disponíveis no RTE por meio das opções de formato de parágrafo, o [!DNL Experience Manager] fornece uma boa base para o desenvolvimento de conteúdo acessível. Os autores de conteúdo não podem usar o RTE para formatar o tamanho da fonte, as cores ou outros atributos relacionados, impedindo a criação de formatação em linha. Em vez disso, os autores podem selecionar os elementos estruturais apropriados, como cabeçalhos, e usar estilos globais escolhidos na opção Estilos para garantir uma marcação limpa e opções melhores para os usuários que navegam com suas próprias folhas de estilos e conteúdo estruturado corretamente.

## Uso do recurso de edição do Source {#use-of-the-source-edit-feature}

Em alguns casos, os autores de conteúdo considerarão necessário examinar e ajustar o código-fonte do HTML criado usando o RTE. Por exemplo, um conteúdo criado no RTE pode exigir mais marcação para garantir a conformidade com a WCAG 2.0. Isso pode ser feito com a opção [edição de origem](rich-text-editor.md#aboutplugins) do RTE. Você pode especificar o recurso [`sourceedit` no `misctools` plug-in](rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Use o recurso `sourceedit` com cuidado. Quaisquer erros de digitação e os recursos não compatíveis podem causar problemas.

<!--
TBD ENGREVIEW: Is this only applicable to Classic UI? 

## Adding Support for further HTML Elements and Attributes {#adding-support-for-additional-html-elements-and-attributes}

To further extend the accessibility features of [!DNL Experience Manager], it is possible to extend the existing components based on the RTE (such as the `Text` and `Table` components) with extra elements and attributes.

The following procedure illustrates how to extend the `Table` component with a `Caption` element that provides information about a data table to assistive technology users:

### Example: Add a caption to a table properties dialog {#example-adding-the-caption-to-the-table-properties-dialog}

In the constructor of the `TablePropertiesDialog`, add an extra text input field that is used for editing the caption. Set the `itemId` to `caption` (the DOM attribute’s name) to automatically handle its content.

In a `Table`, set the attribute to the DOM element or or remove it from the DOM element. The dialog in the `config` object passed the value. Set or remove the DOM attributes using the corresponding `CQ.form.rte.Common` methods (`com` is a shortcut for `CQ.form.rte.Common`). Using `CQ.form.rte.Common` methods avoids common pitfalls with browser implementations.

>[!NOTE]
>
>This procedure is only suitable for the classic UI.

### Step-by-step instructions {#step-by-step-instructions}

1. Start CRXDE Lite. For example: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`. Create intermediate folders if those do not exist.

1. Copy `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` to `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js` file to edit.

1. In the `constructor` method, before the mention of `var dialogRef = this;`, add the following code:

   ```javascript
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Open `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js` file.

1. Add the following code at the end of the `transferConfigToTable` method:

   ```javascript
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. To save your changes, click **[!UICONTROL Save All]**.

## Best practices and limitations {#best-practices-limitations-tips}

* A plain text field is not the only type of input allowed for the value of the caption element. You can use any ExtJS widget, that provides the caption’s value through its `getValue()` method.
* To add editing capabilities for more elements and attributes, ensure that:

  * The `itemId` property for each corresponding field is set to the name of the appropriate DOM attribute (`TablePropertiesDialog`).
  * The attribute is set and/or removed on the DOM element explicitly (`Table`).
-->

>[!MORELIKETHIS]
>
>* [Um guia rápido para os padrões da WCAG](/help/compliance/accessibility/quick-guide-wcag.md)
>* [Como criar conteúdo acessível no Experience Manager](/help/sites-cloud/authoring/page-editor/accessible-content.md)
