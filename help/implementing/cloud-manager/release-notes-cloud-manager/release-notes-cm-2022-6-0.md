---
title: Notas de versão do Cloud Manager 2022.6.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2022.6.0 em AEM as a Cloud Service.
feature: Release Information
source-git-commit: 5200ee315ad88dae4b52c0ea904489e73f62a8a0
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 1%

---


# Notas de versão do Cloud Manager 2022.6.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2022.6.0 AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager versão 2022.6.0 em AEM as a Cloud Service é 9 de junho de 2022. A próxima versão está planejada para 30 de junho de 2022.

## Novidades {#what-is-new}

* A interface do usuário do Cloud Manager agora permite [restauração de conteúdo de autoatendimento](/help/operations/backup.md) para um estado em boas condições do ambiente de nuvem AEM.
   * Esse recurso será implementado em uma abordagem em fases nas semanas seguintes à versão 2022.06.0.
* Um novo cartão de boas-vindas na página de aterrissagem do Cloud Manager fornece aos usuários acesso rápido a tutoriais de integração e métricas de progresso relacionadas ao locatário.
   * Esse recurso será implementado em uma abordagem em fases na semana seguinte à versão 2022.06.0.
* Os usuários com as permissões necessárias podem acessar um novo [Painel de licenças](/help/implementing/cloud-manager/license-dashboard.md) na página de aterrissagem do Cloud Manager para exibir detalhes dos direitos disponíveis para o locatário.
   * O AEM Sites é a primeira solução para a qual o consumo de disponibilidade e uso é fornecido por meio do painel do Cloud Manager.
   * Esse recurso será implementado em uma abordagem em fases nas semanas seguintes à versão 2022.06.0.
* [Nova subconta do Relic e gerenciamento de usuários de autoatendimento](/help/implementing/cloud-manager/user-access-new-relic.md) O agora está disponível por meio da interface do usuário do Cloud Manager.
   * Esse recurso será implementado em uma abordagem em fases nas semanas seguintes à versão 2022.06.0.
* Um novo widget Go Live na página inicial dos programas de produção do Cloud Service agora fornece orientação para se preparar para uma experiência dinâmica bem-sucedida.
* [Os artefatos da build agora podem ser reutilizados](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) ao usar o espelhamento de git.

## Alterações na API {#api-changes}

* O [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) A API foi substituída e [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) deve ser usada em vez disso.
   * `List Programs` continua a funcionar, mas seu uso gerará mensagens de aviso em logs.
   * Ele não será mais suportado após três meses.

