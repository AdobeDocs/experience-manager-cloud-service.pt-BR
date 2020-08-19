---
title: Visão geral dos resultados do teste - Cloud Services
description: Visão geral dos resultados do teste - Cloud Services
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 16%

---


# Visão geral {#overview}

As execuções de pipeline do Cloud Manager para o Cloud Services oferecerão suporte à execução de testes que são executados no ambiente de preparo. Isso contrasta com os testes executados durante a etapa Build and Unit Testing, que são executados offline, sem acesso a nenhum ambiente AEM em execução.

Há três categorias amplas de testes suportadas pelo Cloud Manager para Cloud Services Pipeline:

1. [Teste de qualidade de código](/help/implementing/cloud-manager/code-quality-testing.md)
1. [Teste funcional](/help/implementing/cloud-manager/functional-testing.md)
1. [Teste de auditoria de conteúdo](/help/implementing/cloud-manager/content-audit-testing.md)

Esses testes podem ser:

* Escrito pelo cliente
* Adobe
* Ferramenta de código aberto (alimentada pelo Farol do Google)

   >[!NOTE]
   > Os testes escritos pelo cliente e os testes por Adobe são executados em uma infraestrutura de contêiner projetada para executar esses tipos de testes.

