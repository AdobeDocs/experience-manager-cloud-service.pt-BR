---
title: Gerenciamento de principais
description: Gerenciamento de entidades para migração, usando o Admin Console
exl-id: a75598d0-8f59-466b-984e-dfe527388c2a
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 6%

---

# Gerenciamento de principais {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="Gerenciamento de principais"
>abstract="Saiba o que é preciso para gerenciar usuários durante ou após uma migração de conteúdo"

Antes de o conteúdo ser transferido para o ambiente de nuvem do AEM as a Cloud Service, há algumas tarefas que podem ser executadas no Admin Console.  São eles: criar usuários, criar grupos e atribuir usuários a grupos; esses usuários e grupos existirão no IMS, o serviço Identity Management da Adobe, usado para gerenciar usuários e grupos para todos os serviços na nuvem da Adobe.

## Criar grupos e seus usuários no Admin Console

[Usar o Admin Console para entidades de segurança do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up) fornece instruções detalhadas sobre como criar usuários e grupos no IMS e como adicionar os usuários aos grupos ao mesmo tempo ou posteriormente.  O documento inclui três opções para criá-los: manualmente por meio da Admin Console, por meio de upload de CSV pela Admin Console e por meio de uma Ferramenta de sincronização de usuários.

A opção manual permite criar um grupo ou usuário por vez; o upload de CSV permite criar e vincular vários usuários e grupos de uma só vez; e a Ferramenta de sincronização de usuários permite usar um IDP existente para criar e gerenciar os usuários e grupos do IMS.

Depois que um usuário usa o IMS para fazer logon no AEM, uma representação do AEM do usuário será criada.  Além disso, todos os grupos IMS em que o usuário estiver terão grupos AEM equivalentes criados no AEM.  Esses usuários e grupos do AEM criados com o IMS ainda são gerenciados principalmente usando o Admin Console.

Após a conclusão da migração de conteúdo, os grupos IMS normalmente precisarão ter algumas configurações adicionais para que os usuários possam acessar o conteúdo migrado.  Consulte [Migrando Entidades Após a Migração](/help/journey-migration/managing-principals-after-migration.md)

Consulte também [Tutorial, usuários, grupos e permissões do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions) para saber mais sobre como os usuários e grupos do AEM e do IMS são integrados e administrados.
