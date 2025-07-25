---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2021.12.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2021.12.0
feature: Release Information
exl-id: 4155e1c0-cd40-4cbc-9d6c-b106d68a2db5
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 38%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2021.12.0 {#release-notes}

Esta página descreve as Notas de versão das Ferramentas de migração no AEM as a Cloud Service 2021.12.0.

>[!NOTE]
>
>Consulte as [Notas de versão atuais do Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão mais recentes.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.22 é 1º de dezembro de 2021.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e relatar a versão do ACS commons usada.
* Capacidade de detectar e relatar o número de usuários e subgrupos em um grupo.
* Capacidade de detectar e relatar valores de propriedade do nó no MongoDB que excedam 16MB.

### Correções de erros {#bug-fixes-bpa}

* A detecção de componentes de base foi refinada para reduzir falsos negativos.
* Para clientes do AEM Forms, as mensagens de BPA relacionadas a `EMAIL_PDF_SUBMIT_ACTION` não estarem disponíveis no AEM as a Cloud Service foram corrigidas.


## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de Transferência de conteúdo v1.7.10 é 8 de dezembro de 2021.

### Novidades {#what-is-new-ctt}

* Alternância adicionada à fase de assimilação na Ferramenta de transferência de conteúdo para permitir que os usuários desativem a [pré-cópia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=pt-BR) durante a assimilação. Para velocidades de assimilação ideais, a pré-cópia durante a assimilação deve ser desativada para pequenos conjuntos de migração ou se apenas alguns blobs tiverem sido adicionados desde a última assimilação.
* Mapeamento de usuários atualizado para usar a API de gerenciamento de usuários aprimorada, que permite obter 2000 usuários de cada vez, melhorando significativamente o desempenho.
