---
title: Overlays para Adobe Experience Manager como Cloud Service
description: AEM como Cloud Service usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades
translation-type: tm+mt
source-git-commit: 8028682f19ba6ba7db6b60a2e5e5f5843f7ac11f
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 2%

---


# Sobreposições no AEM as a Cloud Service {#overlays-in-aem}

A Adobe Experience Manager como Cloud Service usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades (por exemplo, criação de página).

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

A sobreposição é um termo que pode ser usado em muitos contextos. Neste contexto (estender AEM como um Cloud Service), uma sobreposição significa usar a funcionalidade predefinida e impor suas próprias definições sobre isso (para personalizar a funcionalidade padrão).

Em uma instância padrão, a funcionalidade predefinida é mantida em `/libs` e é recomendável definir sua sobreposição (personalizações) na ramificação `/apps` (usando um [caminho de pesquisa](#search-paths) para resolver os recursos).

* A interface de usuário habilitada para toque usa sobreposições relacionadas a [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html):

   * Método

      * Reconstrua a estrutura `/libs` apropriada em `/apps`.

         Isso não requer uma cópia 1:1, pois [Sling Resource Fusion](/help/implementing/developing/introduction/sling-resource-merger.md) é usado para fazer referência cruzada às definições originais necessárias. A fusão Sling Resource presta serviços de acesso e fusão de recursos através de mecanismos de diferenciação (diferenciação).

      * Faça quaisquer alterações em `/apps`.
   * Vantagens

      * Mais robusto às alterações em `/libs`.
      * Apenas redefina o que é realmente necessário.


<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>O [Sling Resource Fusion](/help/implementing/developing/introduction/sling-resource-merger.md) e os métodos relacionados só podem ser utilizados com [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Isso significa que a criação de uma sobreposição com uma estrutura de esqueleto é apropriada apenas para a interface de usuário padrão habilitada para toque.

As sobreposições são o método recomendado para muitas alterações, como configurar seus consoles ou criar sua categoria de seleção para o navegador de ativos no painel lateral (usado durante a criação de páginas). São exigidos como:

<!--
Overlays are the recommended method for many changes, such as [configuring your consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) or [creating your selection category to the asset browser in the side panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (used when authoring pages). They are required as:
-->

* Você ***não deve* fazer alterações na `/libs` ramificação **Qualquer alteração que você fizer poderá ser perdida, pois essa ramificação poderá ser alterada sempre que as atualizações forem aplicadas à sua instância.

* Eles concentram suas alterações em um local; tornando mais fácil para você rastrear, migrar, fazer backup e/ou depurar as alterações conforme necessário.

## Caminhos de pesquisa {#search-paths}

AEM usa um caminho de pesquisa para localizar um recurso, pesquisando (por padrão) primeiro a ramificação `/apps` e depois a ramificação `/libs`. Esse mecanismo significa que sua sobreposição em `/apps` (e as personalizações definidas ali) terá prioridade.

Para sobreposições, o recurso fornecido é uma agregação dos recursos e propriedades recuperados, dependendo dos caminhos de pesquisa definidos na configuração do OSGi.

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->