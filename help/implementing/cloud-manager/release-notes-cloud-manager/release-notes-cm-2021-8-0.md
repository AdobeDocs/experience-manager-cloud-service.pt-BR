---
title: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.8.0
description: Notas de versão do Cloud Manager AEM versão as a Cloud Service 2021.8.0
feature: Release Information
exl-id: cf1d5c4f-404a-4ced-90f2-273c710adc0f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.8.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager AEM as a Cloud Service 2021.8.0.

>[!NOTE]
>Para ver as Notas de versão atuais do Adobe Experience Manager as a Cloud Service, clique em [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

## Data de lançamento {#release-date}

A Data de lançamento do Cloud Manager AEM as a Cloud Service 2021.8.0 é 12 de agosto de 2021.

### Novidades {#what-is-new}

* Os clientes do Cloud Service agora podem visualizar os relatórios do Contrato de nível de serviço (SLA) no Cloud Manager. Esta informação será disponibilizada progressivamente nos próximos meses.
Consulte [Relatórios de SLA](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sla-reporting.html) para saber mais.

* O tipo e a gravidade do IndexType e `IndexDamAssetLucene` as regras de qualidade foram alteradas. Estes são agora os dois Bugs do Bloqueador *servidão*.

* Novas regras de qualidade do índice Oak foram introduzidas para abranger configurações assíncronas e tika.

* Aumente o número máximo de certificados SSL por programa para 50.

* Capacidade de autoatendimento para permitir que os usuários criem e gerenciem vários repositórios por meio da interface do usuário do Cloud Manager.

* SonarQube estava lendo desnecessariamente os dados do histórico do Git. Em bases de código grandes, isso poderia resultar em uma penalidade desnecessária no desempenho da build.

* Agora há uma API disponível para invalidar o cache de dependência Maven por pipeline.

* A versão do AEM Project Archetype usada pelo Cloud Manager foi atualizada para a versão 29.

### Correções de erros {#bug-fixes}

* O status Atualizar disponível não deve ser exibido quando a versão mais recente for menor que a versão atual.

* A integração inicial estava falhando para novas organizações com nomes muito longos.

* Ocasionalmente, quando um pipeline é acionado duas vezes por algum motivo, resulta em uma das execuções falhar com *não é possível atualizar o status de execução do pipeline* erro.
