---
title: Usar o Git com o Cloud Manager
description: Saiba como usar os repositórios Git do Cloud Manager e como integrar seu próprio repositório Git local gerenciado pelo cliente com o Cloud Manager.
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 96%

---

# Usar o Git com o Cloud Manager {#git-integration}

O Adobe Cloud Manager vem provisionado com um único repositório Git que é usado para implantar código usando os pipelines de CI/CD do Cloud Manager.

Você pode usar o repositório Git do Cloud Manager imediatamente, mas também tem a opção de integrar um repositório Git gerenciado pelo cliente ao Cloud Manager.

## Visão geral da integração do Git {#git-integration-overview}

Esta série de vídeos explora vários casos de uso ao integrar um repositório Git gerenciado pelo cliente ao Cloud Manager, incluindo:

* [Sincronização inicial](#initial-sync)
* [Estratégia básica de ramificação](#branching-strategy)
* [Desenvolvimento de ramificação de recursos](#feature-development)
* [Implantação em produção](#production-deployment)
* [Sincronização das tags de versão](#sync-tags)

A série de vídeos pressupõe conhecimento básico sobre Git e gerenciamento de controle de origem. Consulte os [recursos adicionais abaixo](#additional-resources) para obter mais detalhes sobre o Git.

>[!VIDEO](https://video.tv.adobe.com/v/31192?captions=por_br)

As etapas e convenções de nomenclatura descritas nesta série de vídeos representam algumas práticas recomendadas para trabalhar com um repositório Git gerenciado pelo cliente no Cloud Manager. Espera-se que as convenções e os fluxos de trabalho descritos sejam adaptados para casos de uso individuais.

## Sincronização inicial {#initial-sync}

Neste vídeo, conheça as primeiras etapas para sincronizar um repositório Git gerenciado pelo cliente com o repositório Git do Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/31191/?captions=por_br&quality=12)

## Estratégia básica de ramificação {#branching-strategy}

Neste vídeo, conheça as estratégias básicas de ramificação.

>[!VIDEO](https://video.tv.adobe.com/v/31190/?captions=por_br&quality=12)

## Desenvolvimento de ramificação de recursos {#feature-development}

Use uma ramificação de recursos para isolar alterações de código em um repositório Git gerenciado pelo cliente e sincronizar com o repositório Git do Cloud Manager, a fim de usar um pipeline de não produção para testes de validação e qualidade de código.

>[!VIDEO](https://video.tv.adobe.com/v/31189/?captions=por_br&quality=12)

## Implantação de produção {#production-deployment}

Prepare o código para uma versão de produção em um repositório Git gerenciado pelo cliente e sincronize com o repositório Git do Cloud Manager para implantar em ambientes de preparo e produção.

>[!VIDEO](https://video.tv.adobe.com/v/31188/?captions=por_br&quality=12)

## Sincronizar tags de versão {#sync-tags}

Sincronize as tags de versão de um repositório git do Cloud Manager em um repositório git gerenciado pelo cliente para fornecer visibilidade do código que foi implementado nos ambientes de preparo e produção.

>[!VIDEO](https://video.tv.adobe.com/v/31187/?captions=por_br&quality=12)

## Recursos adicionais {#additional-resources}

* [Recursos do GitHub](https://docs.github.com/pt/get-started/getting-started-with-git/set-up-git)
* [Tutoriais sobre Git da Atlassian](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Folha de referências do Git](https://education.github.com/git-cheat-sheet-education.pdf)
