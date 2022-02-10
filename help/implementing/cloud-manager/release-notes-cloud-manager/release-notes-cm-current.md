---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2022.02.0
description: Estas são as notas de versão do Cloud Manager AEM as a Cloud Service versão 2022.02.0.
feature: Release Information
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 2%

---


# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2022.02.0 {#release-notes}

Esta página descreve as notas de versão do Cloud Manager AEM as a Cloud Service 2022.02.0.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager AEM as a Cloud Service 2022.02.0 é 10 de fevereiro de 2022. A próxima versão está prevista para 10 de março de 2022.

## Novidades {#what-is-new}

* Novo acelerado [pipelines de configuração da camada da Web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) foram introduzidos para implantar exclusivamente a configuração HTTPD/dispatcher
   * Você deve estar AEM versão `2021.12.6151.20211217T120950Z` para usar esse recurso.
   * Esse recurso será implementado em uma abordagem em fases durante as duas semanas seguintes à versão 2022.02.0.
* A experiência de página de aterrissagem do Cloud Manager foi atualizada para oferecer navegação aprimorada, fácil alternância entre exibições de grade/bloco e pop-ups para resumo rápido do programa.
* Um novo limite de falha (`< D`) foi adicionado ao [métrica de classificação de confiabilidade.](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * Os clientes com problemas graves de qualidade que afetam a estabilidade do sistema, relacionados principalmente a índices inválidos e processos de fluxo de trabalho, não poderão implantar até que esses problemas sejam resolvidos.
* A gravidade da `BannedPath` [regra de qualidade](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) O foi alterado de bloqueador para crítico.
* O assistente de pipeline informará o usuário quando uma atualização de ambiente de AEM pode ser necessária antes de configurar um [pipelines de configuração da camada da Web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) associado a ela.

## Correções de erros {#bug-fixes}

* As senhas antigas do repositório Git agora são sempre invalidadas quando uma nova senha é gerada.
* A atualização de variáveis de ambiente por meio da API não interfere mais na execução de um pipeline em raras situações.
