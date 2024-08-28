---
title: Migrar grupos de usuários fechados
description: Saiba mais sobre as considerações especiais necessárias para habilitar Grupos de usuários fechados após a migração do conteúdo para o Adobe Experience Manager as a Cloud Service.
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
feature: Migration
role: Admin
source-git-commit: 5b0dfb847a1769665899d6dd693a7946832fe7d1
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 12%

---


# Migrar grupos de usuários fechados {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="Migração de grupos de usuários fechados"
>abstract="Atualmente, a migração de grupos de usuários fechados (CUG, sigla em inglês) requer algumas verificações e etapas para garantir a operação após a migração."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=pt-BR" text="Grupos de Usuários Fechados no AEM"

Atualmente, os Grupos de usuários fechados (CUG) precisam de algumas etapas adicionais para funcionarem no ambiente de destino de uma migração. Este documento explica o cenário e as etapas necessárias para protegê-los da maneira desejada.

## Migração de grupos de usuários fechados (CUGs)

Os grupos são incluídos automaticamente em uma migração CTT/CAM para o Adobe Experience Manager as a Cloud Service se estiverem associados ao conteúdo migrado por meio da ACL desse conteúdo ou de seu nó de política CUG. A verificação de que o grupo e seus membros existem deve ser feita antes da ativação. Os grupos referenciados em uma política CUG são chamados aqui de &quot;grupos CUGs&quot;.

Para usar CUGs no AEM as a Cloud Service, os usuários devem estar presentes na instância do autor e ser membros dos grupos CUGs relevantes.  Isso pode ser feito usando pacotes ou, se os usuários CUGs forem usuários do IMS, eles já poderão estar presentes.  Os usuários de CUGs devem então se tornar membros dos grupos de CUGs do AEM.

Para ativar o comportamento CUGs na instância do Publish,
1. Os grupos CUGs devem ser ativados (o que replica eles e seus membros para a instância do Publish) e
1. As páginas protegidas com políticas CUGs devem ser publicadas (o que permite que a instância do Publish e o rastreiem as políticas).
1. Depois que todas as páginas forem publicadas, verifique a funcionalidade de cada página protegida por CUG.

Para obter informações adicionais, consulte [Grupos de usuários fechados](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=pt-BR).
