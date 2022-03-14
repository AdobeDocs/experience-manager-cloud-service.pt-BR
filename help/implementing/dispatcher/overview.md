---
title: Visão geral do fluxo de entrega de conteúdo
description: Visão geral do fluxo de entrega de conteúdo
exl-id: fe42fb9e-cdf4-43e1-b688-7cecf4124fa5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---

# Fluxo de entrega de conteúdo {#content-delivery}

A página atual detalha a entrega do conteúdo do serviço de publicação em AEM as a Cloud Service. A entrega de conteúdo do serviço de publicação inclui:

* CDN
* AEM dispatcher
* AEM publicar

O fluxo de dados é o seguinte:

1. O URL é adicionado no navegador
1. Solicitação feita à CDN mapeada no DNS para esse domínio
1. Se o conteúdo for totalmente armazenado em cache no CDN, o CDN o retornará ao navegador
1. Se o conteúdo não for totalmente armazenado em cache, a CDN chamará (proxy reverso) o dispatcher
1. Se o conteúdo estiver totalmente armazenado em cache no dispatcher, o dispatcher o enviará para a CDN
1. Se o conteúdo não estiver totalmente armazenado em cache, o dispatcher chamará (proxy reverso) para a publicação do AEM
1. O conteúdo é renderizado pelo navegador, que também pode armazená-lo em cache, dependendo dos cabeçalhos

Por padrão, o tipo de conteúdo HTML/texto é definido para expirar após 300s (5 minutos) na camada do dispatcher, um limite que o cache do dispatcher e o CDN respeitam. Durante as reimplantações do serviço de publicação, o cache do dispatcher é limpo e subsequentemente aquecido antes que os novos nós de publicação aceitem o tráfego.

As seções abaixo fornecem mais detalhes sobre a entrega de conteúdo, incluindo a configuração e o armazenamento em cache do CDN.

Estão disponíveis informações sobre replicação do serviço de criação para o serviço de publicação [here](/help/operations/replication.md).
