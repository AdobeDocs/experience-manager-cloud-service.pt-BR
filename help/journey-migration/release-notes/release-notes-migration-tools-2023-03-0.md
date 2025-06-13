---
title: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.03.0
description: Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.03.0
feature: Release Information
exl-id: cdc57cca-e10a-4b0d-b803-910ccc9350a6
role: Admin
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 7%

---

# Notas de versão das Ferramentas de migração no AEM as a Cloud Service versão 2023.03.0 {#release-notes}

Esta página descreve as Notas de versão das Ferramentas de migração no AEM as a Cloud Service 2023.03.0.

## Analisador de práticas recomendadas {#bpa-release}

### Data de lançamento {#release-date-bpa}

A data de lançamento do Analisador de práticas recomendadas v2.1.40 é 3 de março de 2023.

### Novidades {#what-is-new-bpa}

* O BPA agora pode detectar e relatar nós conflitantes - nós com o mesmo `jcr:uuid`. Essas descobertas são sinalizadas como críticas, pois podem levar a falhas de assimilação de conteúdo ao mover o conteúdo para o AEM as a Cloud Service.
* O BPA agora pode detectar e relatar o uso de Ouvintes de eventos. É recomendável refatorar esse tipo de mecanismo de tratamento de eventos para trabalhos do sling ao mudar para o AEM as a Cloud Service.

### Correções de erros {#bug-fixes-bpa}

* O BPA relatava falsos positivos em `grouprendercondition`. Isso foi corrigido.

## Ferramenta Transferência de conteúdo {#ctt-release}

### Data de lançamento {#release-date-ctt}

A data de lançamento da ferramenta de transferência de conteúdo v2.0.16 é 8 de março de 2023.

### Novidades {#what-is-new-ctt}

* O mapeamento de usuários foi simplificado e integrado à etapa de extração de conteúdo. Nenhuma configuração é necessária e, por padrão, o mapeamento de usuários é feito automaticamente quando o usuário inicia a extração de conteúdo. O usuário tem a opção de desativar o mapeamento de usuários, se necessário.
* A etapa de pré-cópia usando o [AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) foi integrada à Ferramenta de transferência de conteúdo para acelerar significativamente as extrações de conteúdo. A pré-cópia é configurada e instalada automaticamente quando essa versão da CTT é instalada. Por padrão, quando a extração é iniciada, a pré-cópia é executada automaticamente para conjuntos de migração maiores que 200 GB. O usuário tem a opção de desativá-la, se necessário. Saiba mais [aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=pt-BR).
* A CTT agora pode ser usada em servidores Windows.

### Correções de erros {#bug-fixes-ctt}

* Várias correções de erros para melhorar a resiliência da extração de conteúdo.
