---
title: Publicar conteúdo para o Edge Delivery Services
description: Saiba como a publicação de conteúdo funciona com o Edge Delivery Services e como publicar conteúdo de AEM com o Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
source-git-commit: 3ee1ba83518c3d4fba59b0c98b31e5c63a2eb6ab
workflow-type: tm+mt
source-wordcount: '295'
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
1. O serviço de publicação do Edge Delivery Services encaminha os eventos relevantes para a API de administrador do Edge Delivery Services.
1. O Edge Delivery extrai e assimila o HTML semântico do autor AEM.
1. O AEM é atualizado com o status de publicação.

>[!NOTE]
>
>Por padrão, a API de administrador do Edge Delivery Services não está protegida e pode ser usada para publicar ou desfazer a publicação de documentos sem autenticação. Para configurar a autenticação para a API de administrador, conforme documentado em [Configurando a autenticação para autores](https://www.aem.live/docs/authentication-setup-authoring), seu projeto deve ser provisionado com uma API_KEY, que concede acesso ao serviço de publicação. [Entre em contato com a equipe de Adobe no Slack](/help/edge/docs/slack.md) para obter orientação.

## Como começar {#how-to-get-started}

Entre em contato com o representante da Adobe para obter acesso a esse recurso.
