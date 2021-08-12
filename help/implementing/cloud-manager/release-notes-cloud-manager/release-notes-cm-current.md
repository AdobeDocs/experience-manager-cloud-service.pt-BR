---
title: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.8.0
description: Notas de versão do Cloud Manager no AEM as a Cloud Service versão 2021.8.0
feature: Informações da versão
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 05cd993df7293691a0f8b91e9bde278ec7b7af69
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 5%

---

# Notas de versão do Cloud Manager no Adobe Experience Manager as a Cloud Service 2021.8.0 {#release-notes}

Esta página descreve as Notas de versão do Cloud Manager no AEM as a Cloud Service 2021.8.0.

>[!NOTE]
>Para ver as Notas de versão atuais do Adobe Experience Manager como um Cloud Service, clique [aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

## Data de lançamento {#release-date}

A Data de lançamento do Cloud Manager no AEM as a Cloud Service 2021.8.0 é 12 de agosto de 2021.
A próxima versão está planejada para 09 de setembro de 2021.

### Novidades {#what-is-new}

* Os clientes do Cloud Service agora podem visualizar os relatórios do Contrato de nível de serviço (SLA) no Cloud Manager. Esta informação será disponibilizada progressivamente nos próximos meses.

* O tipo e a gravidade das regras de qualidade IndexType e `IndexDamAssetLucene` foram alterados. Agora, ambos são Bugs do Blocker *serverity*.

* Novas regras de qualidade do índice Oak foram introduzidas para abranger configurações assíncronas e tika.

* Aumente o número máximo de certificados SSL por programa para 50.

* Capacidade de autoatendimento para permitir que os usuários criem e gerenciem vários repositórios por meio da interface do usuário do Cloud Manager.

* SonarQube estava lendo desnecessariamente os dados do histórico do Git. Em bases de código grandes, isso poderia resultar em uma penalidade desnecessária no desempenho da build.

* Agora há uma API disponível para invalidar o cache de dependência Maven por pipeline.

* A versão do AEM Project Archetype usada pelo Cloud Manager foi atualizada para a versão 28.

### Correções de erros {#bug-fixes}

* O status Atualizar disponível não deve ser exibido quando a versão mais recente for menor que a versão atual.

* A integração inicial estava falhando para novas organizações com nomes muito longos.

* Ocasionalmente, quando um pipeline é acionado duas vezes por algum motivo, resulta em uma das execuções falhando com o erro *cannot update pipeline execution status* .


