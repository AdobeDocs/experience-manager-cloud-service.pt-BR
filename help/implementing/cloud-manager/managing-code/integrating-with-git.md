---
title: Uso do Git com o Cloud Manager
description: Saiba como usar os repositórios Git do Cloud Manager e como integrar seu próprio repositório Git gerenciado pelo cliente no local com o Cloud Manager.
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Uso do Git com o Cloud Manager {#git-integration}

O Adobe Cloud Manager vem provisionado com um único repositório Git usado para implantar código usando os pipelines de CI/CD do Cloud Manager.

Você pode usar o repositório Git do Cloud Manager imediatamente, mas também tem a opção de integrar um repositório Git gerenciado pelo cliente ao Cloud Manager.

## Visão geral da integração do Git {#git-integration-overview}

Esta série de vídeos explora vários casos de uso ao integrar um repositório Git gerenciado pelo cliente ao Cloud Manager, incluindo:

* [Sincronização inicial](#initial-sync)
* [Estratégia básica de ramificação](#branching-strategy)
* [Desenvolvimento de ramificação de recursos](#feature-development)
* [Implantação de produção](#production-deployment)
* [Sincronização das tags de versão](#sync-tags)

A série de vídeos assume um conhecimento básico do gerenciamento de git e do controle de origem. Consulte a [recursos adicionais abaixo](#additional-resources) para obter mais detalhes sobre git.

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

As etapas e convenções de nomenclatura descritas nesta série de vídeo representam algumas práticas recomendadas para trabalhar com um repositório Git gerenciado pelo cliente no Cloud Manager. Espera-se que as convenções e os fluxos de trabalho descritos sejam adaptados para casos de uso individuais.

## Sincronização inicial {#initial-sync}

Neste vídeo, aprenda as primeiras etapas para sincronizar um repositório Git gerenciado pelo cliente com o repositório Git do Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Estratégia básica de ramificação {#branching-strategy}

Neste vídeo, conheça as estratégias básicas de ramificação.

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Desenvolvimento de ramificação de recursos {#feature-development}

Use uma ramificação de recursos para isolar alterações de código em um repositório Git gerenciado pelo cliente e sincronizar com o repositório Git do Cloud Manager, a fim de usar um pipeline de não produção para testes de qualidade e validação de código.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Implantação de produção {#production-deployment}

Prepare o código para uma versão de produção em um repositório Git gerenciado pelo cliente e sincronize com o repositório Git do Cloud Manager para implantar em ambientes de preparo e produção.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Sincronização das tags de versão {#sync-tags}

Sincronize as tags de versão de um repositório Git do Cloud Manager em um repositório Git gerenciado pelo cliente para fornecer visibilidade de qual código foi implantado em ambientes de preparo e produção.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Recursos adicionais {#additional-resources}

* [Recursos do GitHub](https://try.github.io)
* [Atlassiano Git Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Folha de características do Git](https://education.github.com/git-cheat-sheet-education.pdf)
