---
title: Sobreposições para o Adobe Experience Manager as a Cloud Service
description: O AEM as a Cloud Service usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# Sobreposições no AEM as a Cloud Service {#overlays-in-aem}

O Adobe Experience Manager as a Cloud Service usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades (por exemplo, criação de página).

Sobreposição é um termo que pode ser usado em muitos contextos. Nesse contexto, estender o AEM as a Cloud Service, uma sobreposição significa usar a funcionalidade predefinida e impor suas próprias definições sobre ela para personalizar a funcionalidade padrão.

Em uma instância padrão, a funcionalidade predefinida é mantida em `/libs` e é prática recomendada definir sua sobreposição (personalizações) na ramificação `/apps` (usando um [caminho de pesquisa](#search-paths) para resolver os recursos).

* A interface de usuário habilitada para toque usa sobreposições relacionadas ao [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html):

   * Método

      * Reconstruir a estrutura `/libs` apropriada em `/apps`.

        Esta reestruturação não requer uma cópia de 1:1 porque o [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) é usado para fazer referência cruzada às definições originais necessárias. O Sling Resource Merger fornece serviços para acessar e mesclar recursos com mecanismos de diferenciação.

      * Em `/apps`, faça as alterações.

   * Vantagens

      * Mais robusto para alterações em `/libs`.
      * Apenas redefina o que é necessário.

>[!CAUTION]
>
>O [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) e os métodos relacionados só podem ser usados com o [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Essa regra significa que a criação de uma sobreposição com uma estrutura de esqueleto só é apropriada para a interface de usuário padrão habilitada para toque.

Sobreposições são o método recomendado para muitas alterações. Por exemplo, configurar seus consoles ou criar sua categoria de seleção no navegador de ativos no painel lateral (usado ao criar páginas). Elas são necessárias como:

* **Na ramificação `/libs`, *não* faz alterações**
Qualquer alteração feita pode ser perdida, pois essa ramificação pode sofrer alterações sempre que atualizações forem aplicadas à instância.

* Eles concentram as alterações em um local, facilitando o rastreamento, a migração, o backup ou a depuração das alterações, conforme necessário.

## Caminhos de pesquisa {#search-paths}

O AEM usa um caminho de pesquisa para localizar um recurso, pesquisando primeiro - por padrão - a ramificação `/apps` e depois a ramificação `/libs`. Esse mecanismo significa que sua sobreposição em `/apps` (e as personalizações definidas lá) tem prioridade.

Para sobreposições, o recurso entregue é uma agregação dos recursos e propriedades recuperados, dependendo dos caminhos de pesquisa definidos na configuração do OSGi.
