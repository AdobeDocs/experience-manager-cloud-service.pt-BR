---
title: Visão geral do fluxo de entrega de conteúdo
description: Visão geral do fluxo de entrega de conteúdo
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 49%

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
1. Se o conteúdo não estiver totalmente armazenado em cache, o CDN chamará (proxy reverso) o Dispatcher
1. Se o conteúdo for totalmente armazenado em cache no Dispatcher, o Dispatcher o fornecerá ao CDN
1. Se o conteúdo não estiver totalmente armazenado em cache, o Dispatcher chamará (proxy reverso) a publicação do AEM
1. O conteúdo é renderizado pelo navegador, que também pode armazená-lo em cache, dependendo dos cabeçalhos

Por padrão, o tipo de conteúdo HTML/texto é definido para expirar após 300 segundos (5 minutos) na camada do Dispatcher, um limite que o cache do Dispatcher e o CDN respeitam. Durante as reimplantações do serviço de publicação, o cache do Dispatcher é limpo e depois aquecido antes que os novos nós de publicação aceitem o tráfego.

As seções a seguir fornecem mais detalhes sobre a entrega de conteúdo:
* [Configuração da CDN](/help/implementing/dispatcher/cdn.md)
* [Armazenamento em cache](/help/implementing/dispatcher/caching.md)


Informações sobre replicação do serviço de autor para o serviço de publicação estão disponíveis [aqui](/help/operations/replication.md).
