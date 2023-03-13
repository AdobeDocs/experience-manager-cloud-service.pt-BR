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

O Adobe Experience Manager as a Cloud Service usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades (por exemplo, criação de página).

Sobreposição é um termo que pode ser usado em muitos contextos. Neste contexto (estender o AEM as a Cloud Service), uma sobreposição significa usar a funcionalidade predefinida e impor suas próprias definições sobre ela (para personalizar a funcionalidade padrão).

Em uma instância padrão, a funcionalidade predefinida é mantida em `/libs` e é prática recomendada definir sua sobreposição (personalizações) no `/apps` ramificação (usando um [caminho de pesquisa](#search-paths) para resolver os recursos).

* A interface habilitada para toque usa [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)sobreposições relacionadas ao:

   * Método

      * Reconstrua o apropriado `/libs` estrutura em `/apps`.

         Isso não exige uma cópia 1:1, pois o [Fusão de recursos do Sling](/help/implementing/developing/introduction/sling-resource-merger.md) é usado para cruzar as definições originais necessárias. O Sling Resource Merger fornece serviços para acessar e mesclar recursos por meio de mecanismos de diferenciação.

      * Faça as alterações em `/apps`.
   * Vantagens

      * Mais robusta às mudanças no `/libs`.
      * Apenas redefina o que é realmente necessário.


>[!CAUTION]
>
>A variável [Fusão de recursos do Sling](/help/implementing/developing/introduction/sling-resource-merger.md) e os métodos relacionados só podem ser usados com [Granite](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Isso significa que a criação de uma sobreposição com uma estrutura de esqueleto só é apropriada para a interface de usuário padrão habilitada para toque.

As sobreposições são o método recomendado para muitas alterações, como configurar seus consoles ou criar sua categoria de seleção no navegador de ativos no painel lateral (usado ao criar páginas). Elas são necessárias como:

* Você ***não deve* fazer alterações no `/libs` ramificação **Qualquer alteração feita pode ser perdida, pois essa ramificação pode sofrer alterações sempre que atualizações forem aplicadas à instância.

* Eles concentram as alterações em um local, facilitando o rastreamento, a migração, o backup e/ou a depuração das alterações, conforme necessário.

## Caminhos de pesquisa {#search-paths}

O AEM usa um caminho de pesquisa para encontrar um recurso, pesquisando (por padrão) primeiro o `/apps` e depois a variável `/libs` filial. Esse mecanismo significa que sua sobreposição no `/apps` (e as personalizações definidas lá) terão prioridade.

Para sobreposições, o recurso entregue é uma agregação dos recursos e propriedades recuperados, dependendo dos caminhos de pesquisa definidos na configuração do OSGi.
