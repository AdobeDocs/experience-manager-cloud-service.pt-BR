---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2022.02.0
description: Estas são as notas de versão do Cloud Manager AEM as a Cloud Service versão 2022.02.0.
feature: Release Information
exl-id: da0643a0-78f8-4e9d-9cc9-a1a17067a08c
source-git-commit: 0c4a42595800f7f1d0869bf647c3ec99023b12c5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2022.02.0 {#release-notes}

Esta página descreve as notas de versão do Cloud Manager AEM as a Cloud Service 2022.02.0.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2022.02.0 é 10 de fevereiro de 2022. A próxima versão está planejada para 10 de março de 2022.

## Novidades {#what-is-new}

* Os novos e acelerados [Pipelines de configuração no nível da Web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) foram introduzidos para implantar exclusivamente a configuração do HTTPD/Dispatcher.
   * Você deve estar usando a versão `2021.12.6151.20211217T120950Z` do AEM, ou mais recente, e [aceitar o modo flexível das ferramentas do Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) para usar esse recurso.
   * Esse recurso será implementado por meio de uma abordagem em fases durante as duas semanas seguintes ao lançamento da versão 2022.02.0.
* A experiência de página de aterrissagem do Cloud Manager foi atualizada para oferecer navegação aprimorada, fácil alternância entre exibições de grade/bloco, além de popovers que oferecem um resumo rápido do programa.
* Um novo limite de falha (`< D`) foi adicionado à [métrica de avaliação de confiabilidade.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * Clientes com problemas graves de qualidade que afetam a estabilidade do sistema, relacionados principalmente a índices e processos de fluxo de trabalho inválidos, não poderão implantar até que esses problemas sejam resolvidos.
* A gravidade da `BannedPath` [regra de qualidade](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) foi alterada de bloqueadora para crítica.
* O assistente de pipeline informará o usuário quando uma atualização de ambiente do AEM for necessária antes de definir um [Pipeline de configuração no nível da Web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) associado a ela.

## Correções de erros {#bug-fixes}

* As senhas antigas do repositório Git agora são invalidadas sempre que uma nova senha é gerada.
* A atualização de variáveis de ambiente por meio da API não interfere mais na execução de um pipeline em situações raras.
