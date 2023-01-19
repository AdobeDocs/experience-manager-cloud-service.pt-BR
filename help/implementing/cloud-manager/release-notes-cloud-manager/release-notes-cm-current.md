---
title: Notas de versão do Cloud Manager 2023.1.0 no Adobe Experience Manager as a Cloud Service
description: Estas são as notas de versão do Cloud Manager 2024.1.0 no AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 26a2ed4ee613b77c192652ae9afa99d5a86f72ce
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 33%

---


# Notas de versão do Cloud Manager 2023.1.0 no Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta as notas de versão do Cloud Manager versão 2023.1.0 AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para obter as notas de versão atuais do Adobe Experience Manager as a Cloud Service.

## Data de lançamento {#release-date}

A data de lançamento da versão 2023.1.0 do Cloud Manager AEM as a Cloud Service é 19 de janeiro de 2023. A próxima versão está planejada para 16 de fevereiro de 2023.

## Novidades {#what-is-new}

* Os aprimoramentos de usabilidade foram ao atualizar estilos de cursor que distinguem entre onde os usuários podem realizar ações e o ponteiro padrão.

* Em listas de ambientes e execuções de pipeline, agora é possível acessar detalhes clicando na linha individual.

* Os Relatórios de teste da interface do usuário personalizada agora são copiados para o armazenamento do Cloud Manager e podem ser acessados por meio da chamada da API do Cloud Manager.

* Os usuários agora podem fazer a transição entre estados de widget em execução usando setas para a esquerda e para a direita.

   ![Transições de widget em execução](assets/go-live-transitions.gif)

* Autoatendimento [criação de programas habilitados para HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) agora é possível quando direitos e permissões correspondentes estão disponíveis.

## Correções de erros {#bug-fixes}

* O Cloud Manager impedirá que duas execuções de pipeline sejam iniciadas ao mesmo tempo (ou quase ao mesmo tempo), evitando falhas de pipeline.
