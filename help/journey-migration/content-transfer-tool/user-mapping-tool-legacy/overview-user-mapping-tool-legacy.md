---
title: Visão geral da ferramenta Mapeamento de usuários (herdado)
description: Visão geral da ferramenta Mapeamento de usuários (herdado)
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 22%

---

# Visão geral da ferramenta Mapeamento de usuários (herdado) {#overview-user-mapping-tool}

>[!INFO]
>
>Esta documentação se refere a uma versão obsoleta da ferramenta. Para obter mais informações sobre a versão mais recente, consulte [Mapeamento de usuários e migração de entidade de segurança](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

<!-- Alexandru: drafting this for now

NOTE: "LEGACY" for user mapping includes everything before (i.e. not including) 2.0.16 of CTT.

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## Introdução {#introduction}

Como parte da jornada de transição para o Adobe Experience Manager (AEM) as a Cloud Service AEM AEM, você deve mover usuários e grupos do seu sistema existente para o as a Cloud Service. Essa migração é feita pela Ferramenta de transferência de conteúdo.

Uma mudança importante do AEM as a Cloud Service é o uso totalmente integrado de Adobe IDs para acessar o nível do autor. Essa integração exige o uso da [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS) que fornece logon único em todos os aplicativos de nuvem do Adobe. Para obter mais detalhes, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=en#identity-management). Devido a essa alteração, os usuários e grupos existentes devem ser mapeados para suas IDs IMS para evitar usuários e grupos duplicados na instância de autor do Cloud Service.

## Ferramenta de Mapeamento de usuários {#mapping-tool}

A ferramenta Transferência de conteúdo (sem o mapeamento de usuários) migra todos os usuários e grupos associados ao conteúdo que está sendo migrado. A Ferramenta de mapeamento de usuário faz parte da Ferramenta de transferência de conteúdo. Seu único objetivo é editar os usuários para que eles sejam reconhecidos corretamente pelo IMS, a funcionalidade de logon único usada pelo AEM as a Cloud Service. Depois que essas modificações são feitas, a ferramenta Transferência de conteúdo migra os usuários e grupos do conteúdo especificado como de costume.

### O que vem a seguir {#whats-next}

Depois de descobrir o que é uma ferramenta de Mapeamento de usuários, você estará pronto para revisar considerações importantes e casos excepcionais antes de usar a ferramenta de Mapeamento de usuários. Consulte [Considerações importantes da ferramenta de Mapeamento de usuários](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) para obter mais detalhes.
