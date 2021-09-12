---
title: Fluxo de atividades na linha do tempo
description: Este artigo descreve como exibir registros de atividades para ativos na linha do tempo.
contentOwner: AG
feature: Asset Reports,Asset Management
role: Admin,User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
source-git-commit: 0d0a3247e42e0f4a9b2965104814fe6bcd8e6128
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 24%

---

# Exibir logs de operações de ativos no fluxo de atividades {#activity-stream-in-timeline}

Esse recurso exibe registros de atividades para ativos na linha do tempo. Se você executar qualquer uma das seguintes operações relacionadas a ativos em [!DNL Experience Manager Assets], o recurso de fluxo de Atividade atualizará a linha do tempo para refletir a atividade.

As seguintes operações são registradas no fluxo de atividade:

* Criar
* Excluir
* Download (incluindo representações)
* Publicação
* Desfazer publicação
* Aprovar
* Rejeitar
* Mover

Os registros de atividades a serem exibidos na linha do tempo são obtidos do local `/var/audit/com.day.cq.dam/content/dam` no CRX, onde os arquivos de registro são armazenados.  Além disso, a atividade da linha do tempo é registrada quando novos ativos são carregados ou os existentes são modificados e verificados em [!DNL Experience Manager] por meio de [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) ou [[!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>Fluxos de trabalho transitórios não são exibidos na linha do tempo, pois nenhuma informação de histórico é salva para esses fluxos de trabalho.

Para exibir o fluxo de atividades, execute uma ou mais das operações no ativo, selecione o ativo e escolha **[!UICONTROL Linha do tempo]** na lista GlobalNavigation.

<!-- ![timeline-2](assets/timeline-2.png) -->

A linha do tempo exibe o fluxo de atividades para as operações que você executa nos ativos.

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>O local de armazenamento de log padrão das tarefas **[!UICONTROL Publicar]** e **[!UICONTROL Cancelar publicação]** é `/var/audit/com.day.cq.replication/content`. Para tarefas **[!UICONTROL Mover]**, o local padrão é `/var/audit/com.day.cq.wcm.core.page`.
