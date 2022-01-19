---
title: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2021.12.0
description: Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2021.12.0
feature: Release Information
source-git-commit: 2788db9338da5499b4a9e72ce196e4ae9857b5d5
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---


# Notas de versão para Ferramentas de migração AEM versão as a Cloud Service 2021.12.0 {#release-notes}

Esta página descreve as Notas de versão para as Ferramentas de migração AEM as a Cloud Service 2021.12.0.

>[!NOTE]
>Para ver as Notas de versão atuais do Adobe Experience Manager as a Cloud Service, clique em [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR).

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.2 é 1 de dezembro de 2021.

### Novidades {#what-is-new-bpa}

* Capacidade de detectar e relatar a versão do ACS commons usada.
* Capacidade de detectar e relatar o número de usuários e subgrupos em um grupo.
* Capacidade de detectar e relatar valores de propriedade de nó no MongoDB que excedem 16MB.

### Correções de erros {#bug-fixes-bpa}

* A detecção de componentes de base foi refinada para reduzir falsos negativos.
* Para clientes do AEM Forms, mensagens de BPA relacionadas a `EMAIL_PDF_SUBMIT_ACTION` não estar disponível AEM as a Cloud Service foi corrigido.


## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A Data de lançamento da ferramenta Transferência de conteúdo v1.7.10 é 8 de dezembro de 2021.

### Novidades {#what-is-new-ctt}

* Alternar adicionada à fase de assimilação na ferramenta Transferência de conteúdo para permitir que os usuários desativem [pré-cópia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) durante a ingestão. Para velocidades ideais de ingestão, a pré-cópia durante a ingestão deve ser desativada para pequenos conjuntos de migração ou se apenas alguns blobs foram adicionados desde a última ingestão.
* Mapeamento de usuários atualizado para usar a API de gerenciamento de usuários aprimorada, que permite obter 2000 usuários por vez, melhorando significativamente o desempenho.
