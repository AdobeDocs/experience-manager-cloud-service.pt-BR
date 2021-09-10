---
title: Integração com Git
description: Integração com Git - Cloud Services
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: 21669a29fbfd1072b637f407f5220825c4d1edbb
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---

# Integração do Git com o Adobe Cloud Manager {#git-integration}

O Adobe Cloud Manager vem provisionado com um único repositório Git usado para implantar código usando os pipelines de CI/CD do Cloud Manager. Os clientes podem usar o repositório Git do Cloud Manager imediatamente. Os clientes também têm a opção de integrar um repositório Git no local ou **gerenciado pelo cliente** com o Cloud Manager.

## Visão geral da integração do Git {#git-integration-overview}

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

Esta série de vídeos explora vários casos de uso quando se trata de integrar um repositório Git gerenciado pelo cliente ao Cloud Manager, incluindo:

* [Sincronização inicial](#initial-sync)
* [Estratégia básica de ramificação](#branching-strategy)
* [Desenvolvimento de ramificação de recursos](#feature-development)
* [Implantação de produção](#production-deployment)
* [Sincronização das tags de versão](#sync-tags)

A série de vídeos assume um conhecimento básico do gerenciamento de git e do controle de origem. Consulte os [recursos adicionais abaixo](#additional-resources) para obter mais detalhes sobre o git.

>[!NOTE]
>
>As etapas e convenções de nomenclatura descritas nesta série de vídeo representam algumas práticas recomendadas para trabalhar com um repositório Git gerenciado pelo cliente e o Cloud Manager. Espera-se que as convenções e os fluxos de trabalho descritos sejam adaptados a equipes de desenvolvimento individuais.

## Sincronização inicial {#initial-sync}

Primeiras etapas para sincronizar um repositório Git gerenciado pelo cliente com o repositório Git do Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Estratégia básica de ramificação {#branching-strategy}

Siga o vídeo abaixo para saber mais sobre as estratégias básicas de ramificação.

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Desenvolvimento de ramificação de recursos {#feature-development}

Use uma ramificação de recursos para isolar alterações de código em um repositório Git gerenciado pelo cliente e sincronizar com o repositório Git do Cloud Manager, a fim de usar um pipeline de não produção para testes de qualidade e validação de código.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Implantação de produção {#production-deployment}

Prepare o código para uma versão de produção em um repositório Git gerenciado pelo cliente e sincronize com o repositório Git do Cloud Manager para implantar em ambientes de preparo e produção.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Sincronização das tags de versão {#sync-tags}

Sincronize as tags de versão de um repositório Git do Cloud Manager em um repositório Git gerenciado pelo cliente para fornecer visibilidade sobre qual código foi implantado em ambientes de preparo e produção.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Recursos adicionais {#additional-resources}

* [Recursos do GitHub](https://try.github.io)
* [Atlassiano Git Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Folha de características do Git](https://education.github.com/git-cheat-sheet-education.pdf)
