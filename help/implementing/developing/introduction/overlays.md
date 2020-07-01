---
title: Sobreposições para Adobe Experience Manager como Cloud Service
description: O AEM como Cloud Service usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades
translation-type: tm+mt
source-git-commit: 8028682f19ba6ba7db6b60a2e5e5f5843f7ac11f
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---


# Sobreposições no AEM como um Cloud Service {#overlays-in-aem}

O Adobe Experience Manager como Cloud Service usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades (por exemplo, criação de página).

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

A sobreposição é um termo que pode ser usado em muitos contextos. Neste contexto (estender o AEM como um Cloud Service), uma sobreposição significa usar a funcionalidade predefinida e impor suas próprias definições sobre isso (para personalizar a funcionalidade padrão).

Em uma instância padrão, a funcionalidade predefinida é mantida em `/libs` e é recomendável definir sua sobreposição (personalizações) sob a `/apps` ramificação (usando um caminho [de](#search-paths) pesquisa para resolver os recursos).

* A interface habilitada para toque usa sobreposições relacionadas ao [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html):

   * Método

      * Reconstrua a `/libs` estrutura apropriada em `/apps`.

         Isso não requer uma cópia 1:1, pois a Fusão [de recursos de](/help/implementing/developing/introduction/sling-resource-merger.md) Sling é usada para fazer referência cruzada às definições originais necessárias. A fusão Sling Resource presta serviços de acesso e fusão de recursos através de mecanismos de diferenciação (diferenciação).

      * Faça quaisquer alterações em `/apps`.
   * Vantagens

      * Mais robusto para as alterações apresentadas em `/libs`.
      * Apenas redefina o que é realmente necessário.


<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>A Fusão [de Recursos de](/help/implementing/developing/introduction/sling-resource-merger.md) Sling e os métodos relacionados só podem ser utilizados com [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Isso significa que a criação de uma sobreposição com uma estrutura de esqueleto é apropriada apenas para a interface de usuário padrão habilitada para toque.

As sobreposições são o método recomendado para muitas alterações, como configurar seus consoles ou criar sua categoria de seleção para o navegador de ativos no painel lateral (usado durante a criação de páginas). São exigidos como:

<!--
Overlays are the recommended method for many changes, such as [configuring your consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) or [creating your selection category to the asset browser in the side panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (used when authoring pages). They are required as:
-->

* Você não ****deve fazer alterações na`/libs`ramificação **Qualquer alteração feita pode ser perdida, pois essa ramificação está sujeita a alterações sempre que as atualizações forem aplicadas à sua instância.

* Eles concentram suas alterações em um local; tornando mais fácil para você rastrear, migrar, fazer backup e/ou depurar as alterações conforme necessário.

## Caminhos de pesquisa {#search-paths}

O AEM usa um caminho de pesquisa para localizar um recurso, pesquisando (por padrão) primeiro a `/apps` ramificação e, em seguida, a `/libs` ramificação. Esse mecanismo significa que sua sobreposição `/apps` (e as personalizações definidas) terão prioridade.

Para sobreposições, o recurso fornecido é uma agregação dos recursos e propriedades recuperados, dependendo dos caminhos de pesquisa definidos na configuração do OSGi.

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->