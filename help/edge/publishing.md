---
title: Publicar conteúdo para o Edge Delivery Services
description: Saiba como a publicação de conteúdo funciona com o Edge Delivery Services e como publicar conteúdo de AEM com o Edge Delivery Services.
feature: Edge Delivery Services
source-git-commit: 166525b6987215a64521d1ff63a222187376ba65
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---


# Publicar conteúdo para o Edge Delivery Services {#publishing-edge}

Com o Edge Delivery Services, a publicação de conteúdo é contínua, independentemente da fonte de conteúdo:

* Conteúdo baseado em documento - Consulte [Publicar seção](/help/edge/docs/authoring.md) da documentação do Edge Delivery Services.
* Conteúdo do AEM - Consulte os detalhes abaixo.

## Fluxo de publicação do AEM {#publishing-flow}

Ao usar o Editor universal para criar conteúdo AEM, publicar é tão simples quanto clicar no **Publish** no Editor Universal. Consulte o documento [Publicar conteúdo com o Editor universal.](/help/implementing/universal-editor/publishing.md)

O fluxo de informações ao publicar é o seguinte. Depois que o autor inicia a publicação, esse fluxo é automático e é ilustrado aqui para fins de informação.

![O fluxo de informações ao publicar do AEM para o Edge Delivery Services](assets/publishing-flow.png)

1. O autor de conteúdo publica conteúdo AEM no Editor universal.
1. Um evento de publicação é enviado para a fila do pipeline de Adobe.
1. O serviço de publicação de entrega de borda encaminha os eventos relevantes para a API de administração de entrega de borda.
1. O Edge Delivery extrai e assimila o HTML semântico do autor AEM.
1. O AEM é atualizado com o status de publicação.

## Como começar {#how-to-get-started}

Entre em contato com o representante da Adobe para obter acesso a esse recurso.
