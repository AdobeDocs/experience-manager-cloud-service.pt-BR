---
title: Visão geral da ferramenta de Mapeamento de usuários (Legado)
description: Visão geral da ferramenta Mapeamento de usuários (herdado)
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
hide: true
hidefromtoc: true
source-git-commit: 8a258c2c929f9af84a1cde99072291a3e7f6cfc3
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 88%

---

# Visão geral da ferramenta Mapeamento de usuários (herdado) {#overview-user-mapping-tool}

>[!INFO]
>
>Esta documentação se refere a uma versão obsoleta da ferramenta. Para obter mais informações sobre a versão mais recente, consulte [Mapeamento de usuários e migração de entidade de segurança](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

<!-- Alexandru: drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="User Mapping Tool"
>abstract="The Content Transfer Tool helps you move users and groups from your existing AEM system to AEM as a Cloud Service. Existing users and groups need to be mapped to their IMS IDs to avoid duplicate users and groups on the Cloud Service author instance."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Important Considerations for using User Mapping Tool"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Using User Mapping Tool"

-->

## Introdução {#introduction}

Como parte da jornada de transição para o Adobe Experience Manager (AEM) as a Cloud Service, é necessário mover usuários e grupos do sistema existente do AEM para o AEM as a Cloud Service. Isso é feito através da ferramenta de Transferência de conteúdo.

Uma mudança importante do AEM as a Cloud Service é o uso totalmente integrado de Adobe IDs para acessar o nível do autor.  É preciso usar o [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS), que fornece um logon único para todos os aplicativos de nuvem da Adobe. Para obter mais detalhes, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=pt-BR#identity-management). Devido a essa alteração, usuários e grupos existentes precisam ser mapeados de acordo com suas IDs do IMS para evitar usuários e grupos duplicados na instância de autor do Cloud Service.

## Ferramenta de Mapeamento de usuários {#mapping-tool}

A ferramenta de Transferência de conteúdo (sem o Mapeamento de usuários) migrará qualquer usuário e grupo associado ao conteúdo que está sendo migrado. A ferramenta de Mapeamento de usuários faz parte da ferramenta de Transferência de conteúdo e seu único objetivo é modificar os usuários para que eles possam ser reconhecidos corretamente pelo IMS, a funcionalidade de logon único usada pelo AEM as a Cloud Service. Quando essas modificações forem feitas, a ferramenta de Transferência de conteúdo migrará os usuários e grupos do conteúdo especificado como de costume.

### O que vem a seguir {#whats-next}

Depois de descobrir o que é uma ferramenta de Mapeamento de usuários, você estará pronto para revisar considerações importantes e casos excepcionais antes de usar a ferramenta de Mapeamento de usuários. Consulte [Considerações importantes da ferramenta de Mapeamento de usuários](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md) para obter mais detalhes.
