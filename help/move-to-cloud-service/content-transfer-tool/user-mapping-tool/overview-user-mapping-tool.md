---
title: Visão geral da ferramenta Mapeamento de usuários
description: Visão geral da ferramenta Mapeamento de usuários
source-git-commit: 9d131daf5b6a0b1530ebff48627f6130ef716f3e
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---


# Visão geral da ferramenta Mapeamento de usuários {#overview-user-mapping-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Ferramenta de mapeamento de usuários"
>abstract="A ferramenta Transferência de conteúdo ajuda a mover usuários e grupos do sistema de AEM existente para AEM as a Cloud Service. Os usuários e grupos existentes precisam ser mapeados para suas IDs IMS para evitar usuários e grupos duplicados na instância do autor do Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Considerações importantes sobre o uso da ferramenta Mapeamento de usuários"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Usar a ferramenta Mapeamento de usuários"

## Introdução {#introduction}

Como parte da jornada de transição para o Adobe Experience Manager (AEM) as a Cloud Service, é necessário mover usuários e grupos do sistema de AEM existente para AEM as a Cloud Service. Isso é feito pela ferramenta Transferência de conteúdo.

Uma mudança importante em AEM as a Cloud Service é o uso totalmente integrado de IDs de Adobe para acessar o nível de criação.  Isso requer o uso do [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS), que fornece o logon único em todos os aplicativos de nuvem do Adobe. Para obter mais detalhes, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). Devido a essa alteração, usuários e grupos existentes precisam ser mapeados para suas IDs de IMS para evitar usuários e grupos duplicados na instância de autor do Cloud Service.

## Ferramenta de mapeamento de usuários {#mapping-tool}

A ferramenta Transferência de conteúdo (sem Mapeamento de usuários) migrará qualquer usuário e grupo associado ao conteúdo que está sendo migrado. A Ferramenta de mapeamento de usuários faz parte da Ferramenta de transferência de conteúdo e seu único objetivo é modificar os usuários e grupos para que eles possam ser reconhecidos corretamente pelo IMS, a funcionalidade de logon único usada por AEM as a Cloud Service. Quando essas modificações forem feitas, a ferramenta Transferência de conteúdo migrará os usuários e grupos do conteúdo especificado como de costume.
