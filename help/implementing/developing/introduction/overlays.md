---
title: Sobreposições para o Adobe Experience Manager as a Cloud Service
description: O AEM as a Cloud Service usa o princípio de sobreposições para permitir estender e personalizar os consoles e outras funcionalidades
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# Sobreposições no AEM as a Cloud Service {#overlays-in-aem}

O Adobe Experience Manager as a Cloud Service usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades (por exemplo, criação de página).

Sobreposição é um termo que pode ser usado em muitos contextos. Nesse contexto, estender o AEM as a Cloud Service, uma sobreposição significa usar a funcionalidade predefinida e impor suas próprias definições sobre ela para personalizar a funcionalidade padrão.

Em uma instância padrão, a funcionalidade predefinida é mantida em `/libs` e é prática recomendada definir sua sobreposição (personalizações) no `/apps` ramificação (usando um [caminho de pesquisa](#search-paths) para resolver os recursos).

* A interface habilitada para toque usa [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)sobreposições relacionadas ao:

   * Método

      * Reconstrua o apropriado `/libs` estrutura em `/apps`.

        Essa reestruturação não exige uma cópia 1:1 porque o [Fusão de recursos do Sling](/help/implementing/developing/introduction/sling-resource-merger.md) é usado para cruzar as definições originais necessárias. O Sling Resource Merger fornece serviços para acessar e mesclar recursos com mecanismos de diferenciação.

      * Em `/apps`, fazer alterações.

   * Vantagens

      * Mais robusta às mudanças no `/libs`.
      * Apenas redefina o que é necessário.

>[!CAUTION]
>
>A variável [Fusão de recursos do Sling](/help/implementing/developing/introduction/sling-resource-merger.md) e os métodos relacionados só podem ser usados com [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Essa regra significa que a criação de uma sobreposição com uma estrutura de esqueleto só é apropriada para a interface de usuário padrão habilitada para toque.

Sobreposições são o método recomendado para muitas alterações. Por exemplo, configurar seus consoles ou criar sua categoria de seleção no navegador de ativos no painel lateral (usado ao criar páginas). Elas são necessárias como:

* **No `/libs` filial, *não* fazer alterações**
Qualquer alteração feita pode ser perdida, pois essa ramificação pode sofrer alterações sempre que atualizações forem aplicadas à instância.

* Eles concentram as alterações em um local, facilitando o rastreamento, a migração, o backup ou a depuração das alterações, conforme necessário.

## Caminhos de pesquisa {#search-paths}

O AEM usa um caminho de pesquisa para encontrar um recurso, pesquisando primeiro - por padrão - o `/apps` e depois a variável `/libs` filial. Esse mecanismo significa que sua sobreposição no `/apps` (e as personalizações definidas lá) têm prioridade.

Para sobreposições, o recurso entregue é uma agregação dos recursos e propriedades recuperados, dependendo dos caminhos de pesquisa definidos na configuração do OSGi.
