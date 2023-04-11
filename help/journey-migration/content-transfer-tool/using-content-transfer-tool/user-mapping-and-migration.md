---
title: Mapeamento de usuários e migração principal
description: Visão geral do mapeamento de usuários e da migração principal
source-git-commit: 5475f9995513d09e61bd8f52242b3e74b8d4694c
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 18%

---

# Mapeamento de usuários e migração principal {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Mapeamento de usuário"
>abstract="A ferramenta de Transferência de conteúdo ajuda a mover usuários e grupos do sistema existente do AEM para o AEM as a Cloud Service. Os usuários existentes devem ser mapeados para suas IDs IMS para evitar que elas sejam duplicadas na instância do autor do Cloud Service."

>[!NOTE]
>Para versões anteriores da Ferramenta de Mapeamento de Usuário, consulte o [documentação herdada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introdução {#introduction}

Como parte da jornada de transição para o Adobe Experience Manager (AEM) as a Cloud Service, é necessário mover usuários e grupos do sistema existente do AEM para o AEM as a Cloud Service. Isso é feito através da ferramenta de Transferência de conteúdo.

Uma mudança importante do AEM as a Cloud Service é o uso totalmente integrado de Adobe IDs para acessar o nível do autor. É preciso usar o [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS), que fornece um logon único para todos os aplicativos de nuvem da Adobe. Para obter mais detalhes, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html#identity-management). Por causa dessa alteração, os usuários existentes precisam ser mapeados para suas IDs de IMS para evitar usuários duplicados na instância do autor do Cloud Service. Como os grupos em AEM tradicionais são fundamentalmente diferentes dos grupos no IMS, os grupos não são mapeados, mas os dois conjuntos de grupos devem ser reconciliados após a conclusão da migração.

## Detalhes de mapeamento e migração do usuário {#user-mapping-detail}

A ferramenta Transferência de conteúdo e o Cloud Acceleration Manager migrarão todos os usuários associados ao conteúdo que está sendo migrado. Esse mapeamento é feito automaticamente e se pode ser controlado por um alternador antes que a extração seja iniciada. A configuração padrão do botão de alternância pode ser substituída pelo usuário ao iniciar a extração.

* Se o sistema de origem for uma instância do autor, por padrão, a opção para fazer o mapeamento é _on_, já que esse é o processo recomendado.
* Se o sistema de origem for uma instância de publicação, por padrão, a opção para fazer o mapeamento é _off_, já que os usuários normalmente não são migrados ou usados em instâncias de publicação.

## Considerações importantes ao mapear e migrar usuários {#important-considerations}


### Casos excepcionais {#exceptional-cases}

Os seguintes casos específicos são registrados:

1. Se um usuário não tiver endereço de email na `profile/email` do seu *jcr* o usuário ou grupo em questão pode ser migrado, mas não será mapeado. Esse é o caso mesmo se o endereço de email for usado como nome de usuário para fazer logon.

1. Se o usuário estiver desativado, ele será tratado como se não estivesse desativado. Ele é mapeado e migrado normalmente e permanece desativado na instância da nuvem.

1. Se um usuário existir na instância de destino do AEM Cloud Service com o mesmo nome de usuário (rep:principalName) de um dos usuários na instância de origem do AEM, o usuário ou grupo em questão não será migrado.

1. Se um usuário for migrado sem primeiro ser mapeado por meio do Mapeamento de usuário ou se o endereço de email não corresponder ao endereço de email usado para fazer logon no IMS, no sistema da nuvem de destino, ele não poderá fazer logon usando a ID IMS. Eles podem fazer logon usando o método AEM tradicional, mas lembrem-se de que isso não é normalmente o que é desejado ou esperado.


## Considerações adicionais {#additional-considerations}

* Se a configuração **Limpar o conteúdo existente na instância do Cloud antes da assimilação** for definido, os usuários já transferidos na instância do Cloud Service serão excluídos junto com todo o repositório existente e um novo repositório será criado para assimilar conteúdo. Isso também redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino, e é verdadeiro para um usuário administrador adicionado ao **administradores** grupo. O usuário administrador deve ser adicionado novamente ao **administradores** para recuperar o token de acesso para CTT.
* Quando os upups de conteúdo são executados, se o conteúdo não for transferido porque não foi alterado desde a transferência anterior, os usuários e grupos associados a esse conteúdo também não são transferidos, mesmo se os usuários e grupos tiverem sido alterados enquanto isso. Isso ocorre porque os usuários e grupos são migrados junto com o conteúdo ao qual estão associados.
* Se a instância do AEM Cloud Service de destino tiver um usuário com um nome de usuário diferente, mas o mesmo endereço de email de um dos usuários na instância de AEM de origem e o Mapeamento de usuários estiver ativado, uma mensagem de erro será gravada nos logs e o usuário do AEM de origem não será transferido, pois somente um usuário com um determinado endereço de email é permitido no sistema de destino.
