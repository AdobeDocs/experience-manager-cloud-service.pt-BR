---
title: Notas de versão do Cloud Manager 2022.3.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2022.3.0 em AEM as a Cloud Service.
feature: Release Information
source-git-commit: 437be8c82a4dee6c9e56af09afa7e9048c8cb3c0
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 3%

---


# Notas de versão do Cloud Manager 2022.3.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2022.3.0 AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager versão 2022.3.0 em AEM as a Cloud Service 10 de março de 2022. A próxima versão está planejada para 7 de abril de 2022.

## Novidades {#what-is-new}

* O acesso ao log de Ambiente de AEM pode ser feito usando a função Desenvolvedor .

## Correções de erros {#bug-fixes}

* Um subconjunto de repositórios git criados manualmente tinha um valor de nome incorreto que impedia a efetivação do recurso de reuso de artefato de compilação. Os nomes desses repositórios foram alterados e os usuários verão o nome corrigido na API/interface do usuário do Cloud Manager.
* Os artefatos de construção provenientes de gasodutos que não são de produção foram reutilizados de forma imprópria em gasodutos de produção em pilha completa.
* Ao adicionar ou editar um pipeline de qualidade de código, as opções para lidar com falhas de métrica não são mais exibidas.
* Algumas configurações inesperadas de variável de pipeline podem causar na etapa de build.
