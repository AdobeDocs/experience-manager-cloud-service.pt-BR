---
title: Notas de versão do Cloud Manager 2022.5.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2022.5.0 em AEM as a Cloud Service.
feature: Release Information
source-git-commit: 47a8f736a74b26e0b9748a74488d2abacd48f6cc
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 3%

---


# Notas de versão do Cloud Manager 2022.5.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager 2022.5.0 AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento do Cloud Manager versão 2022.5.0 em AEM as a Cloud Service 5 de maio de 2022. A próxima versão está planejada para 9 de junho de 2022.

## Novidades {#what-is-new}

* A página Ambientes tem uma coluna para exibir AEM Versão do ambiente.
* A execução do pipeline agora exibirá erros de nível superior da interface do usuário na tela de execução.
* Reexecute a Etapa de implantação de produção por meio da interface do usuário do Cloud Manager.
* Reutilize a etapa de implantação de criação de imagens para executar novamente a implantação de produção.
* Nova API para permitir a exclusão de autoatendimento da infraestrutura de rede.

## Correções de erros {#bug-fixes}

* O botão &quot;Baixar logs&quot; nos logs de etapas do Teste de interface do usuário não estava baixando os logs.
* Algumas execuções estavam travadas no contexto do acionador de confirmação e do cancelamento da etapa de aprovação.
