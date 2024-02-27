---
title: Publicar conteúdo para o Edge Delivery Services
description: Saiba como a publicação de conteúdo funciona com o Edge Delivery Services e como publicar conteúdo de AEM com o Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
source-git-commit: 58d85886ef04b548c09e3ef9308fe596dd3eda38
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Publicar conteúdo para o Edge Delivery Services {#publishing-edge}

Com o Edge Delivery Services, a publicação de conteúdo é contínua, independentemente da fonte de conteúdo:

* Conteúdo baseado em documento - Consulte [Publicar seção](/help/edge/docs/authoring.md) da documentação do Edge Delivery Services.
* Conteúdo do AEM - Consulte os detalhes abaixo.

## Fluxo de publicação do AEM {#publishing-flow}

Ao usar o Editor universal para criar conteúdo AEM, publicar é tão simples quanto clicar no **Publish** no Editor Universal. Consulte o documento [Publicar conteúdo com o Editor universal.](/help/sites-cloud/authoring/universal-editor/publishing.md)

O fluxo de informações ao publicar é o seguinte. Depois que o autor inicia a publicação, esse fluxo é automático e é ilustrado aqui para fins de informação.

>[!NOTE]
>
>São permitidos até 5.000 caminhos publicados pela interface do usuário de criação ou por workflows por dia. Integrações que criam cargas de trabalho de publicação em massa não são compatíveis.

![O fluxo de informações ao publicar do AEM para o Edge Delivery Services](assets/publishing-flow.png)

1. O autor de conteúdo publica conteúdo AEM no Editor universal.
1. Um evento de publicação é enviado para a fila do pipeline de Adobe.
1. O serviço de publicação de entrega de borda encaminha os eventos relevantes para a API de administração de entrega de borda.
1. O Edge Delivery extrai e assimila o HTML semântico do autor AEM.
1. O AEM é atualizado com o status de publicação.

## Como começar {#how-to-get-started}

Entre em contato com o representante da Adobe para obter acesso a esse recurso.
