---
title: Visão geral do fluxo do Delivery de conteúdo
description: Visão geral do fluxo do Delivery de conteúdo
translation-type: tm+mt
source-git-commit: 0080ace746f4a7212180d2404b356176d5f2d72c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Fluxo de Delivery de conteúdo {#content-delivery}

Os detalhes da página atual publicam o delivery de conteúdo do serviço no AEM como um serviço em nuvem. O delivery de conteúdo do serviço de publicação inclui:

* CDN
* Despachante do AEM
* Publicar AEM

O fluxo de dados é o seguinte:

1. O URL é adicionado no navegador
1. Solicitação feita ao CDN mapeada no DNS para esse domínio
1. Se o conteúdo for totalmente armazenado em cache no CDN, o CDN o enviará para o navegador
1. Se o conteúdo não estiver totalmente armazenado em cache, a CDN chamará (proxy reverso) o dispatcher
1. Se o conteúdo for totalmente armazenado em cache no dispatcher, o dispatcher o enviará para a CDN
1. Se o conteúdo não estiver totalmente armazenado em cache, o dispatcher chamará (proxy reverso) para a publicação do AEM
1. O conteúdo é renderizado pelo navegador, que também pode armazená-lo em cache, dependendo dos cabeçalhos

Por padrão, o tipo de conteúdo HTML/texto é definido para expirar depois de 300s (5 minutos) na camada do dispatcher, um limite que tanto o cache do dispatcher quanto o CDN respeitam. Durante as reimplantações do serviço de publicação, o cache do dispatcher é limpo e aquecido posteriormente antes que os novos nós de publicação aceitem o tráfego.

As seções abaixo fornecem mais detalhes sobre o delivery de conteúdo, incluindo configuração e cache de CDN.

Informações sobre replicação do serviço de autor para o serviço de publicação estão disponíveis [aqui](/help/operations/replication.md).
