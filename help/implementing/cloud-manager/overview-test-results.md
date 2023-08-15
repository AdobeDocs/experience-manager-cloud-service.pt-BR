---
title: Visão geral dos testes do Cloud Manager
description: Obtenha uma visão geral dos três tipos de testes que o Cloud Manager executa automaticamente para garantir a qualidade do seu código personalizado.
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 91%

---


# Visão geral dos testes do Cloud Manager {#overview}

Há três categorias de testes compatíveis com o Cloud Manager para os pipelines do Cloud Services.

1. [Teste de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md)

   * O teste de qualidade avalia a qualidade do código do seu aplicativo.
   * O pipeline de qualidade do código é executado imediatamente após a etapa de compilação em todos os pipelines de não-produção e produção.
   * As [regras personalizadas de qualidade do código](/help/implementing/cloud-manager/custom-code-quality-rules.md) executadas pelo Cloud Manager são criadas com base nas práticas recomendadas pela Engenharia do AEM.

1. [Teste funcional](/help/implementing/cloud-manager/functional-testing.md)

   * O teste funcional faz parte da fase de testes de um [pipeline de produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e, opcionalmente, de um [pipeline de não produção](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

1. [Teste de auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md)

   * O teste de auditoria de experiência está habilitado em todos os pipelines de produção do Cloud Manager e não pode ser ignorado.

Esses testes podem ser:

* Elaborados pelo cliente
* Elaborados pela Adobe
* Criados com ferramentas de código aberto

>[!NOTE]
>
> Os testes elaborados pelo cliente e pela Adobe são executados em uma infraestrutura contida projetada para a execução desses testes.
