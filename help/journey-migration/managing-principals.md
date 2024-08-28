---
title: Gerenciando Principais
description: Gerenciar entidades para migração usando o Admin Console
source-git-commit: 5bf497fb2122cc3d3ff0903aeb680a35e90f33b0
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Gerenciando Principais {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="Gerenciando Principais"
>abstract="Saiba o que precisa ser feito para gerenciar usuários durante ou após uma migração de conteúdo"

Antes de o conteúdo ser transferido para o ambiente de nuvem do AEM as a Cloud Service, há algumas tarefas que podem ser executadas no Admin Console.  São eles: criar usuários, criar grupos e atribuir usuários a grupos; esses usuários e grupos existirão no IMS, Adobe Identity Management Service, que é usado para gerenciar usuários e grupos para todos os serviços baseados em nuvem Adobe.

### Criar grupos e seus usuários no Admin Console

[Uso do Admin Console para AEM Principais](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up) fornece instruções detalhadas sobre como criar usuários e grupos no IMS e como adicionar os usuários aos grupos ao mesmo tempo ou posteriormente.  O documento inclui três opções para criá-los: manualmente por meio do Admin Console, por meio do upload de CSV por meio do Admin Console e por meio de uma Ferramenta de sincronização de usuários.

A opção manual permite criar um grupo ou usuário por vez; o upload de CSV permite criar e vincular vários usuários e grupos de uma só vez; e a Ferramenta de sincronização de usuários permite usar um IDP existente para criar e gerenciar os usuários e grupos do IMS.

Depois que um usuário usa o IMS para fazer logon no AEM, uma representação de AEM do usuário será criada.  Além disso, quaisquer grupos IMS em que o usuário esteja terão grupos AEM equivalentes criados no AEM.  Esses usuários e grupos de AEM criados pelo IMS ainda são gerenciados principalmente usando o Admin Console.

Após a conclusão da migração de conteúdo, os grupos IMS normalmente precisarão ter algumas configurações adicionais para que os usuários possam acessar o conteúdo migrado.  Consulte [Migrando Entidades Após a Migração](/help/journey-migration/managing-principals-after-migration.md)

Consulte também [Tutorial, usuários, grupos e permissões de AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions) para saber mais sobre como usuários e grupos de AEM e IMS são integrados e administrados.