---
title: Introdução ao AEM Screens as a Cloud Service
description: Compreenda o AEM Screens as a Cloud Service.
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: 53086e2ec6d9d962a8f1cb1cc40f0601da74ac63
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 59%

---


# Introdução ao AEM Screens as a Cloud Service {#introduction-screens-cloud}

Com o Adobe Experience Manager (AEM) Screens as a Cloud Service, você pode criar experiências envolventes e dinâmicas de sinalização digital, destinadas ao consumo em espaços públicos. É a próxima evolução do AEM Screens e representa um grande salto para frente em usabilidade e escalabilidade.

O AEM Screens as a Cloud Service é uma solução de sinalização digital que permite aos profissionais de marketing criar e gerenciar experiências digitais dinâmicas em escala. Além disso, envolve diferentes tipos de telas físicas como parte de uma estratégia abrangente de marketing digital. Ele estende a oferta do Adobe omnicanal além dos canais usuais da Web e móveis, para incluir também os canais de sinalização digital que estão ao nosso redor. O AEM Screens as a Cloud Service permite experiências de usuário mais relevantes, contextuais, produtivas e antecipatórias por meio de uma compreensão profunda da criação de conteúdo, da montagem de conteúdo, do gerenciamento de eventos acionados e da reprodução de mídia para todos os consumidores e visitantes em qualquer espaço público.

## Compreensão dos componentes no Screens as a Cloud Service {#understanding-components}

Screens as a Cloud Service têm dois componentes principais:

* O **[Provedor de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=pt-BR)**, que é um complemento do Screens executado no AEM Cloud Service ou no Adobe Managed Services (AMS). O Provedor de conteúdo do Screens permite que o autor de conteúdo crie e gerencie canais. Os autores de conteúdo podem adicionar um novo conteúdo, editar um conteúdo sem se preocupar com os detalhes da criação de exibições ou do registro do player. O Provedor de conteúdo fornece uma abstração dos detalhes subjacentes do desenvolvimento de conteúdo, exibições ou registro de player.

* **[Provedor de Serviços](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=pt-BR)**, que é o serviço de gerenciamento de sinalização digital em execução no Adobe I/O Runtime. O Provedor de serviços da Screens permite que os autores, desenvolvedores e administradores de conteúdo gerenciem exibições e players para reprodução de conteúdo depois que o conteúdo é adicionado aos canais. Além disso, o provedor de serviços da Screens informa ao orquestrador onde e quando o conteúdo será reproduzido em alto nível.


## Visão geral da arquitetura {#architectural-overview}

Como usuário do AEM Screens as a Cloud Service, você pode adicionar e gerenciar conteúdo em canais. Você pode registrar e gerenciar exibições e players a partir das interfaces projetadas especificamente para o Screens as a Cloud Service, ou seja, o **Provedor de Serviços da Screens** e o **Provedor de Conteúdo do Screens**.

![Visão geral da arquitetura](/help/screens-cloud/assets/architecture-screenscloud.png)
