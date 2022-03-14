---
title: Visão geral da ferramenta Mapeamento de usuários
description: Visão geral da ferramenta Mapeamento de usuários
exl-id: 17ed5721-093e-4491-b8c4-3dadcaa6598b
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 10%

---

# Visão geral da ferramenta Mapeamento de usuários {#overview-user-mapping-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Ferramenta de Mapeamento de usuários"
>abstract="A ferramenta Transferência de conteúdo ajuda a mover usuários e grupos do sistema de AEM existente para AEM as a Cloud Service. Os usuários e grupos existentes precisam ser mapeados para suas IDs IMS para evitar usuários e grupos duplicados na instância do autor do Cloud Service."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="Considerações importantes sobre o uso da ferramenta Mapeamento de usuários"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="Utilização da ferramenta Mapeamento de usuários"

## Introdução {#introduction}

Como parte da jornada de transição para o Adobe Experience Manager (AEM) as a Cloud Service, é necessário mover usuários e grupos do sistema de AEM existente para AEM as a Cloud Service. Isso é feito pela ferramenta Transferência de conteúdo.

Uma mudança importante do AEM as a Cloud Service é o uso totalmente integrado de Adobe IDs para acessar o nível do autor.  Isso requer o uso da variável [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS), que fornece o logon único em todos os aplicativos de nuvem do Adobe. Para obter mais detalhes, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management). Devido a essa alteração, usuários e grupos existentes precisam ser mapeados para suas IDs de IMS para evitar usuários e grupos duplicados na instância de autor do Cloud Service.

## Ferramenta de Mapeamento de usuários {#mapping-tool}

A ferramenta Transferência de conteúdo (sem Mapeamento de usuários) migrará qualquer usuário e grupo associado ao conteúdo que está sendo migrado. A Ferramenta de mapeamento de usuários faz parte da Ferramenta de transferência de conteúdo e seu único objetivo é modificar os usuários e grupos para que eles possam ser reconhecidos corretamente pelo IMS, a funcionalidade de logon único usada por AEM as a Cloud Service. Quando essas modificações forem feitas, a ferramenta Transferência de conteúdo migrará os usuários e grupos do conteúdo especificado como de costume.

### O que vem a seguir {#whats-next}

Depois de descobrir o que é uma ferramenta de Mapeamento de usuários, você estará pronto para revisar considerações importantes e casos excepcionais antes de usar a ferramenta Mapeamento de usuários. Consulte [Considerações importantes para a ferramenta Mapeamento de usuários](/help/journey-migration/content-transfer-tool/user-mapping-tool/considerations-user-mapping-tool.md) para obter mais detalhes.
