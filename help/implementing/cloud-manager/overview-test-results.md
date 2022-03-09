---
title: Visão geral dos testes do Cloud Manager
description: Obtenha uma visão geral dos três tipos de testes que o Cloud Manager executa automaticamente para garantir a qualidade de seu código personalizado.
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 5%

---


# Visão geral dos testes do Cloud Manager {#overview}

Há três categorias de testes compatíveis com o Cloud Manager para pipelines do Cloud Services.

1. [Teste de qualidade do código](/help/implementing/cloud-manager/code-quality-testing.md)

   * O teste de qualidade do código avalia a qualidade do código de seu aplicativo.
   * O pipeline de qualidade de código é executado imediatamente após a etapa de build em todos os pipelines de não-produção e produção.
   * O [regras de qualidade do código personalizado](/help/implementing/cloud-manager/custom-code-quality-rules.md) executadas pelo Cloud Manager são criadas com base nas práticas recomendadas da AEM Engineering.

1. [Teste funcional](/help/implementing/cloud-manager/functional-testing.md)

   * O ensaio funcional faz parte da fase de ensaio de uma conduta de produção.

1. [Teste de auditoria de experiência](/help/implementing/cloud-manager/experience-audit-testing.md)

   * O teste da auditoria de experiência é ativado em todos os pipelines de produção do Cloud Manager e não pode ser ignorado.

Esses testes podem ser:

* escrito pelo cliente
* Adobe-write
* Criado com ferramentas de código aberto

>[!NOTE]
>
> Testes escritos pelo cliente e testes Adobe-escritos são executados em uma infraestrutura contêiner projetada para a execução desses testes.
