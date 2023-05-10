---
title: Notas de versão do Cloud Manager 2023.4.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2023.4.0 no AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: be39b09b609cccff916db462af9a84149d23a698
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 100%

---


# Notas de versão do Cloud Manager 2023.4.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2023.4.0 no AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager 2023.4.0 no AEM as a Cloud Service é 13 de abril de 2023. A próxima versão está planejada para 11 de maio de 2023.

## Novidades {#what-is-new}

* [O arquétipo de projeto do AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=pt-BR) foi atualizado para a versão 41.

## Correções de erros {#bug-fixes}

* Quando um [certificado](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) expirar, os [nomes de domínio](/help/implementing/cloud-manager/custom-domain-names/introduction.md) e as [listas de permissões de IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md) associados ao certificado não serão mais removidos da CDN.  Nesses casos, o site continuará acessível.
* A interface do Cloud Manager fornecerá avisos antecipados mais visíveis de que o [certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) está prestes a expirar.
* Foi corrigida uma situação rara em que os clientes não conseguiam criar um novo ambiente ou excluir um ambiente.
