---
title: Fluxo de atividades na linha do tempo
description: Este artigo descreve como exibir logs de atividades para ativos na linha do tempo.
contentOwner: AG
feature: Asset Reports, Asset Management
role: Admin, User
exl-id: 8dd82c31-f88e-4407-9b6d-c87033d7a823
hide: true
hidefromtoc: true
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 32%

---

# Exibir logs de operação de ativos no fluxo de atividades {#activity-stream-in-timeline}

Esse recurso exibe logs de atividades para ativos na linha do tempo. Se você executar qualquer uma das seguintes operações relacionadas ao ativo em [!DNL Experience Manager Assets], o recurso de fluxo de Atividade atualizará a linha do tempo para refletir a atividade.

As seguintes operações são registradas no fluxo de atividade:

* Criar
* Excluir
* Download (incluindo representações)
* Publicação
* Desfazer a publicação
* Aprovar
* Rejeitar
* Mover

Os registros de atividades a serem exibidos na linha do tempo são obtidos do local `/var/audit/com.day.cq.dam/content/dam` no CRX, onde os arquivos de registro são armazenados.  Além disso, a atividade da linha do tempo é registrada quando novos ativos são carregados ou os existentes são modificados e verificados no [!DNL Experience Manager] por meio do [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) ou do [[!DNL Experience Manager] aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=pt-BR).

>[!NOTE]
>
>Os workflows transitórios não são exibidos na linha do tempo, pois nenhuma informação de histórico é salva para esses workflows.

Para exibir o fluxo da atividade, execute uma ou mais operações no ativo, selecione o ativo e escolha **[!UICONTROL Linha do tempo]** na lista GlobalNav.

<!-- ![timeline-2](assets/timeline-2.png) -->

A linha do tempo exibe o fluxo de atividades para as operações executadas nos ativos.

<!-- ![activity_stream](assets/activity_stream.png) -->

>[!NOTE]
>
>O local de armazenamento de log padrão das tarefas **[!UICONTROL Publicar]** e **[!UICONTROL Cancelar publicação]** é `/var/audit/com.day.cq.replication/content`. Para tarefas **[!UICONTROL Mover]**, o local padrão é `/var/audit/com.day.cq.wcm.core.page`.

**Consulte também**

* [Traduzir ativos](translate-assets.md)
* [API HTTP de ativos](mac-api-assets.md)
* [Formatos de arquivo compatíveis com os ativos](file-format-support.md)
* [Pesquisar ativos](search-assets.md)
* [Ativos conectados](use-assets-across-connected-assets-instances.md)
* [Relatórios de ativos](asset-reports.md)
* [Esquemas de metadados](metadata-schemas.md)
* [Baixar ativos](download-assets-from-aem.md)
* [Gerenciar metadados](manage-metadata.md)
* [Pesquisar aspectos](search-facets.md)
* [Gerenciar coleções](manage-collections.md)
* [Importação de metadados em massa](metadata-import-export.md)
* [Publicar o Assets no AEM e no Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
