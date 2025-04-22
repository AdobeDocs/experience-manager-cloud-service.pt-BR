---
title: Publicar conteúdo no Edge Delivery Services
description: Saiba como a publicação de conteúdo funciona com o Edge Delivery Services e como publicar conteúdo do AEM com o Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 32fbb144-9175-47a9-bb5a-ca15f3fcd2d8
role: User
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Publicar conteúdo no Edge Delivery Services {#publishing-edge}

Com o Edge Delivery Services, a publicação de conteúdo é perfeita, independentemente da sua fonte de conteúdo:

* Conteúdo baseado em documento - Consulte a [Seção de publicação](/help/edge/docs/authoring.md) da documentação do Edge Delivery Services.
* Conteúdo do AEM - Consulte os detalhes abaixo.

## Fluxo de publicação do AEM {#publishing-flow}

Ao usar o Editor universal para criar conteúdo do AEM, publicar é tão simples quanto clicar no botão **Publicar** no Editor universal. Consulte o documento [Publicando Conteúdo com o Editor Universal](/help/sites-cloud/authoring/universal-editor/publishing.md).

O fluxo de informações ao publicar é o seguinte. Depois que o autor inicia a publicação, esse fluxo é automático e é ilustrado aqui para fins de informação.

>[!NOTE]
>
>São permitidos até 5.000 caminhos publicados pela interface do usuário de criação ou por workflows por dia. Integrações que criam cargas de trabalho de publicação em massa não são compatíveis. Se o projeto exigir maior capacidade, proponha-o para o [Programa VIP](https://www.aem.live/vip/intake).

![O fluxo de informações ao publicar do AEM no Edge Delivery Services](assets/publishing-flow.png)

1. O autor de conteúdo publica conteúdo do AEM no Editor universal.
1. Um evento de publicação é enviado para a fila de pipeline do Adobe.
1. O serviço de publicação do Edge Delivery Services encaminha os eventos relevantes para a API de administração do Edge Delivery Services.
1. O Edge Delivery extrai e assimila HTML semântico do autor do AEM.
1. O AEM é atualizado com o status de publicação.

>[!NOTE]
>
>Por padrão, a API de administrador do Edge Delivery Services não está protegida e pode ser usada para publicar ou desfazer a publicação de documentos sem autenticação. Para configurar a autenticação para a API de administrador, conforme documentado em [Configurando a Autenticação para Autores](https://www.aem.live/docs/authentication-setup-authoring), seu projeto deve ser provisionado com uma API_KEY, que concede acesso ao serviço de publicação. [Entre em contato com a equipe da Adobe no Slack](/help/edge/docs/slack.md) para obter orientação.

