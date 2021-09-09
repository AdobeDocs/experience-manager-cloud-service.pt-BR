---
title: Sobreposições para o Adobe Experience Manager as a Cloud Service
description: O AEM as a Cloud Service usa o princípio de sobreposições para permitir estender e personalizar os consoles e outras funcionalidades
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---

# Sobreposições no AEM as a Cloud Service {#overlays-in-aem}

O Adobe Experience Manager as a Cloud Service usa o princípio de sobreposições para permitir estender e personalizar os consoles e outras funcionalidades (por exemplo, criação de página).

Sobreposição é um termo que pode ser usado em muitos contextos. Neste contexto (estender AEM como um Cloud Service), uma sobreposição significa usar a funcionalidade predefinida e impor suas próprias definições sobre isso (para personalizar a funcionalidade padrão).

Em uma instância padrão, a funcionalidade predefinida é mantida em `/libs` e é prática recomendada definir sua sobreposição (personalizações) na ramificação `/apps` (usando um [caminho de pesquisa](#search-paths) para resolver os recursos).

* A interface habilitada para toque usa sobreposições relacionadas ao [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html):

   * Método

      * Reconstrua a estrutura `/libs` apropriada em `/apps`.

         Isso não requer uma cópia 1:1, pois o [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) é usado para fazer referência cruzada às definições originais necessárias. O Sling Resource Merger fornece serviços para o acesso e a fusão de recursos através de mecanismos de diferenciação (diferenciação).

      * Faça as alterações em `/apps`.
   * Vantagens

      * Mais robusto para alterações em `/libs`.
      * Apenas redefina o que é realmente necessário.


>[!CAUTION]
>
>O [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) e os métodos relacionados só podem ser usados com [Granite](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Isso significa que a criação de uma sobreposição com uma estrutura de esqueleto é adequada apenas para a interface de usuário padrão habilitada para toque.

As sobreposições são o método recomendado para muitas alterações, como configurar seus consoles ou criar sua categoria de seleção para o navegador de ativos no painel lateral (usado durante a criação de páginas). São exigidas como:

* Você ***não deve* fazer alterações na ramificação `/libs`**Quaisquer alterações feitas podem ser perdidas, pois essa ramificação pode ser alterada sempre que as atualizações forem aplicadas à sua instância.

* Eles concentram suas alterações em um local; tornando mais fácil para você rastrear, migrar, fazer backup e/ou depurar as alterações, conforme necessário.

## Caminhos de pesquisa {#search-paths}

AEM usa um caminho de pesquisa para localizar um recurso, pesquisando (por padrão) primeiro a ramificação `/apps` e depois a ramificação `/libs`. Esse mecanismo significa que sua sobreposição em `/apps` (e as personalizações definidas lá) terá prioridade.

Para sobreposições, o recurso entregue é um agregado dos recursos e propriedades recuperados, dependendo dos caminhos de pesquisa definidos na configuração do OSGi.
