---
title: Personalização de Consoles
description: Saiba mais sobre as diferentes opções que o AEM fornece para personalizar os consoles da sua instância de criação.
exl-id: 832f9a86-07c4-4229-a0dc-8ad50a8195b0
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Personalização de Consoles {#customizing-consoles}

O AEM fornece opções para personalizar os consoles (e o [funcionalidade de criação de página](/help/implementing/developing/extending/page-authoring.md)) da sua instância de criação.

## Clientlibs {#clientlibs}

As clientlibs permitem estender a implementação padrão para oferecer uma nova funcionalidade, ao mesmo tempo em que reutiliza funções, objetos e métodos padrão. Ao personalizar com clientlibs, você pode criar sua própria clientlib em `/apps.` Por exemplo, ele pode conter o código necessário para o componente personalizado.

Consulte [Uso de bibliotecas do lado do cliente no AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md).

## Sobreposições {#overlays}

As sobreposições se baseiam nas definições de nó e permitem sobrepor a funcionalidade padrão encontrada em `/libs` com sua própria funcionalidade personalizada em `/apps`. Ao criar uma sobreposição, uma cópia 1:1 do original não é necessária, pois [Fusão de recursos do Sling](/help/implementing/developing/introduction/sling-resource-merger.md) permite a herança.

As sobreposições podem ser usadas de várias maneiras para estender os consoles AEM. Vários exemplos são fornecidos nas seções a seguir.

Consulte também [Sobreposições para o Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

>[!TIP]
>
>Se estiver interessado em opções para personalizar a experiência de criação, consulte [Personalização da criação de página](/help/implementing/developing/extending/page-authoring.md).

## Personalizando a View Default para uma Console {#customizing-the-default-view-for-a-console}

É possível personalizar a exibição padrão (coluna, cartão, lista) de um console:

* Você pode reordenar as exibições sobrepondo a entrada necessária em:

   * `/libs/wcm/core/content/sites/jcr:content/views`

   * A primeira entrada é o padrão.

   * Os nós disponíveis estão correlacionados com as opções de visualização disponíveis:

      * `column`
      * `card`
      * `list`

* Por exemplo, em uma sobreposição para uma lista:

   * `/apps/wcm/core/content/sites/jcr:content/views/list`

   * Defina a seguinte propriedade:

      * **Nome**: `sling:orderBefore`
      * **Tipo**: `String`
      * **Valor**: `column`

### Adicionar uma nova ação à barra de ferramentas {#add-a-new-action-to-the-toolbar}

Você pode criar seus próprios componentes e incluir as bibliotecas de clientes correspondentes para ações personalizadas.

* Por exemplo, talvez você queira criar um **Promover para redes sociais** ação em:

   * `/apps/wcm/core/clientlibs/sites/js/socialmedia.js`

   * Ele pode ser conectado a um item da barra de ferramentas no console:

   * `/apps/<yourProject>/admin/ext/launches`

   * Por exemplo, no modo de seleção:

   * `content/jcr:content/body/content/header/items/selection/items/socialmedia`

### Restringir uma ação da barra de ferramentas a um grupo específico {#restrict-a-toolbar-action-to-a-specific-group}

Você pode usar uma condição de renderização personalizada para sobrepor a ação padrão e impor condições específicas que devem ser atendidas antes de ser renderizada.

Por exemplo, você pode criar um componente para controlar as condições de renderização de acordo com um grupo:

* `/apps/myapp/components/renderconditions/group`

Para aplicá-los ao **Criar site** ação no console sites:

* `/libs/wcm/core/content/sites`

1. Crie a sobreposição:

   * `/apps/wcm/core/content/sites`

1. Em seguida, adicione a condição de renderização para a ação:

   * `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

Usando propriedades nesse nó, você pode definir a variável `groups` autorizado a executar a ação específica; por exemplo, `administrators`

### Personalização de Colunas na Exibição de Lista {#customizing-columns-in-list-view}

Para personalizar as colunas na exibição de lista:

1. Sobrepor a lista de colunas disponíveis.

   * No nó:

     `/apps/wcm/core/content/common/availablecolumns`

1. Adicione novas colunas ou remova as existentes.

Se quiser inserir dados adicionais, é necessário escrever um [PageInfoProvider](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) com um `pageInfoProviderType` propriedade.

>[!NOTE]
>
>Esse recurso é otimizado para colunas de campos de texto. Para outros tipos de dados, é possível sobrepor `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` in `/apps`.

### Filtrar recursos {#filtering-resources}

Ao usar um console, o usuário geralmente precisa selecionar entre recursos como páginas, componentes ou ativos. Isso pode tomar a forma de uma lista na qual o autor deve escolher um item.

Para manter a lista em um tamanho razoável e também relevante para o caso de uso, um filtro pode ser implementado no formato de um predicado personalizado. Consulte [Personalização da criação de página](/help/implementing/developing/extending/page-authoring.md#filtering-resources) para obter detalhes.
