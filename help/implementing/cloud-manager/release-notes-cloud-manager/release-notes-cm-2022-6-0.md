---
title: Notas de versão do Cloud Manager 2022.6.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2022.6.0 em AEM as a Cloud Service.
feature: Release Information
exl-id: 0a348836-74cd-4fd4-aef4-6ffbd6483c24
source-git-commit: e05c2fa2cfb035ed363e2c80d4aac33b022bd435
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 35%

---

# Notas de versão do Cloud Manager 2022.6.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2022.6.0 AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager versão 2022.6.0 em AEM as a Cloud Service é 9 de junho de 2022. A próxima versão está planejada para 30 de junho de 2022.

## Novidades {#what-is-new}

* Um novo cartão de boas-vindas na página de destino do Cloud Manager fornece aos usuários acesso rápido a tutoriais de integração e métricas de progresso relacionadas ao locatário.
   * Esse recurso será implementado em fases durante a semana seguinte ao lançamento da versão 2022.06.0.
* Os usuários com as permissões necessárias podem acessar um novo [Painel de licenças](/help/implementing/cloud-manager/license-dashboard.md) na página de aterrissagem do Cloud Manager para exibir detalhes dos direitos disponíveis para o locatário.
   * O AEM Sites é a primeira solução para a qual o consumo de disponibilidade e uso é fornecido por meio do painel do Cloud Manager.
   * Esse recurso será implementado em uma abordagem em fases nas semanas seguintes à versão 2022.06.0.
* [Nova subconta do Relic e gerenciamento de usuários de autoatendimento](/help/implementing/cloud-manager/user-access-new-relic.md) O agora está disponível por meio da interface do usuário do Cloud Manager.
   * Esse recurso será implementado em uma abordagem em fases nas semanas seguintes à versão 2022.06.0.
* Um novo widget Go Live na página inicial dos programas de produção do Cloud Service agora fornece orientação para se preparar para uma experiência dinâmica bem-sucedida.
* [Os artefatos da build agora podem ser reutilizados](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) ao usar o espelhamento de Git.

## Alterações na API {#api-changes}

* A API [`List Programs`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getPrograms) foi descontinuada e a [`List Programs for Tenant`](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/getProgramsForTenant) deve ser usada em seu lugar.
   * A `List Programs` continua funcionando, mas seu uso gerará mensagens de aviso em logs.
   * Ele não será mais compatível após três meses.
