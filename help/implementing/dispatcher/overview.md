---
title: Visão geral do fluxo de entrega de conteúdo
description: Saiba mais sobre o fluxo de dados de entrega de conteúdo e como publicar seu conteúdo
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
feature: Dispatcher
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 87%

---

# Fluxo de entrega de conteúdo {#content-delivery}

A página atual detalha a entrega de conteúdo do serviço de publicação no AEM as a Cloud Service. A entrega de conteúdo do serviço de publicação inclui:

* CDN
* AEM Dispatcher
* Editor de AEM

O fluxo de dados é o seguinte:

1. O URL é adicionado no navegador
1. Uma solicitação é feita à CDN mapeada no DNS para esse domínio
1. Se o conteúdo for totalmente armazenado em cache na CDN, ela o enviará ao navegador
1. Se o conteúdo não for totalmente armazenado em cache, a CDN chamará (proxy reverso) o Dispatcher
1. Se o conteúdo estiver totalmente armazenado em cache no Dispatcher, ele o enviará para a CDN
1. Se o conteúdo não estiver totalmente armazenado em cache, o Dispatcher chamará (proxy reverso) a publicação do AEM
1. O conteúdo é renderizado pelo navegador, que também pode armazená-lo em cache, dependendo dos cabeçalhos

Por padrão, o tipo de conteúdo HTML/texto é definido para expirar após 300 s (5 minutos) na camada do Dispatcher, um limite que é respeitado pelo cache do Dispatcher e pela CDN. Durante as reimplantações do serviço de publicação, o cache do Dispatcher é limpo e, em seguida, aquecido antes que os novos nós de publicação aceitem o tráfego.

As seções a seguir fornecem mais detalhes sobre a entrega de conteúdo:

* [Configuração da CDN](/help/implementing/dispatcher/cdn.md)
* [Armazenamento em cache](/help/implementing/dispatcher/caching.md)

Para obter informações sobre a replicação do serviço de autoria para o serviço de publicação, consulte [Replicação](/help/operations/replication.md).
