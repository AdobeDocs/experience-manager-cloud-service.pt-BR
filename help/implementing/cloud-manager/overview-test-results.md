---
title: Visão geral dos resultados do teste - Cloud Services
description: Visão geral dos resultados do teste - Cloud Services
translation-type: tm+mt
source-git-commit: b3548e3920fed45f6d1de54a49801d3971aa6bba
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Visão geral {#overview}

Há três categorias amplas de testes suportadas pelo Cloud Manager para Cloud Services Pipeline:

1. [Teste de qualidade de código](/help/implementing/cloud-manager/code-quality-testing.md)

   O teste de qualidade de código avalia a qualidade do código do aplicativo. O pipeline Code-Quality é executado imediatamente após a etapa de construção em todos os gasodutos de não-produção e de produção.

   As Regras [de qualidade de código](/help/implementing/cloud-manager/custom-code-quality-rules.md) personalizadas executadas pelo Gerenciador de nuvem são criadas com base nas práticas recomendadas da AEM Engenharia.

1. [Teste funcional](/help/implementing/cloud-manager/functional-testing.md)

   O Teste Funcional faz parte da fase de teste de uma tubulação de produção.

1. [Teste de auditoria de conteúdo](/help/implementing/cloud-manager/content-audit-testing.md)

   O Teste de auditoria de conteúdo está ativado em todos os Pipelines de produção do Cloud Manager e não pode ser ignorado.

Esses testes podem ser:

* Escrito pelo cliente
* Adobe
* Ferramenta fonte aberta

   >[!NOTE]
   > Os testes escritos pelo cliente e os testes por Adobe são executados em uma infraestrutura de contêiner projetada para executar esses tipos de testes.

