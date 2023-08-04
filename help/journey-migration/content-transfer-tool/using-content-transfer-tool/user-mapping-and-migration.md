---
title: Mapeamento de usuários e migração principal
description: Visão geral do mapeamento de usuários e da migração principal no AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 8c73805b6ed1b7a03c65b4d21a4252c1412a5742
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 10%

---

# Mapeamento de usuários e migração principal {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Mapeamento de usuários"
>abstract="A ferramenta de Transferência de conteúdo ajuda a mover usuários e grupos de seu sistema existente do Adobe Experience Manager (AEM) para o AEM as a Cloud Service. Os usuários existentes devem ser mapeados para suas IDs IMS para evitar que elas sejam duplicadas na instância do autor do Cloud Service."

>[!NOTE]
>Para versões anteriores da Ferramenta de mapeamento de usuários, consulte a [documentação herdada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introdução {#introduction}

Como parte da jornada de transição para o Adobe Experience Manager (AEM) as a Cloud Service AEM AEM, você deve mover usuários e grupos do seu sistema existente para o as a Cloud Service. Essa tarefa é realizada pela ferramenta Transferência de conteúdo.

Uma mudança importante do AEM as a Cloud Service é o uso totalmente integrado de Adobe IDs para acessar o nível do autor. Este processo requer a utilização do [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS) que fornece logon único em todos os aplicativos de nuvem do Adobe. Para obter mais detalhes, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). Devido a essa alteração, os usuários existentes devem ser mapeados para suas IDs IMS para evitar usuários duplicados na instância do autor do Cloud Service. Como os grupos no AEM tradicional são fundamentalmente diferentes dos grupos no IMS, os grupos não são mapeados, mas os dois conjuntos de grupos devem ser reconciliados após a conclusão da migração.

## Detalhes da migração do usuário {#user-migration-detail}

A ferramenta Transferência de conteúdo e o Cloud Acceleration Manager migrarão para o sistema de nuvem todos os usuários associados ao conteúdo que está sendo migrado.

## Detalhes de Mapeamento de Usuário {#user-mapping-detail}

Os usuários do AEM podem ser mapeados para usuários correspondentes do Adobe IMS com o mesmo endereço de email.  Esse mapeamento pode ser feito automaticamente na CTT e se é feito pode ser controlado por um botão antes de iniciar a extração. A configuração padrão do alternador pode ser substituída pelo usuário ao iniciar a extração.

* Se o sistema de origem for uma instância de autor, por padrão, a opção para fazer o mapeamento será _em_, pois esse é o processo recomendado.
* Se o sistema de origem for uma instância de publicação, por padrão, a opção para fazer o mapeamento será _desligado_, pois os usuários normalmente não são migrados ou usados em instâncias de publicação.

## Considerações importantes ao mapear e migrar usuários {#important-considerations}


### Casos excepcionais {#exceptional-cases}

Os seguintes casos específicos são registrados:

1. Se um usuário não tiver um endereço de email no `profile/email` do seu *jcr* , o usuário ou grupo em questão pode ser migrado, mas não está mapeado. Esse cenário é o caso mesmo se o endereço de email for usado como um nome de usuário para logon.

1. Se o usuário estiver desativado, será tratado da mesma forma que se não estivesse desativado. Ele é mapeado e migrado normalmente e permanece desativado na instância da nuvem.

1. Se existir um usuário na instância do AEM Cloud Service de destino com o mesmo nome de usuário (rep:principalName) de um dos usuários na instância de AEM de origem, o usuário em questão não será migrado.

1. Se um usuário for migrado sem ser mapeado por meio do Mapeamento de usuários, ele não poderá fazer logon usando a ID IMS no sistema de nuvem de destino. Ou, se o endereço de email não corresponder ao endereço de email usado para fazer logon no IMS, no sistema de nuvem de destino também não será possível fazer logon usando a ID do IMS. Eles podem conseguir fazer logon usando o método tradicional do AEM, mas esse método normalmente não é o que se deseja ou se espera.


## Considerações adicionais {#additional-considerations}

* Se a configuração **Apagar conteúdo existente na instância da nuvem antes da assimilação** estiver definido, os usuários já transferidos na instância do Cloud Service serão excluídos juntamente com todo o repositório existente. E um novo repositório é criado para onde o conteúdo é assimilado. Esse processo também redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino, e é verdadeiro para um usuário administrador adicionado à **administradores** grupo. O usuário administrador deve ser lido na caixa **administradores** grupo para recuperar o token de acesso para CTT.
* Quando atualizações complementares de conteúdo são executadas, se o conteúdo não for transferido porque não foi alterado desde a transferência anterior, os usuários e grupos associados a esse conteúdo também não serão transferidos. Essa regra é verdadeira mesmo se os usuários e grupos tiverem sido alterados enquanto isso. Isso ocorre porque usuários e grupos são migrados junto com o conteúdo ao qual estão associados.
* Se a instância de destino do AEM Cloud Service tiver um usuário com um nome de usuário diferente, mas com o mesmo endereço de email de um dos usuários na instância de origem do AEM e o Mapeamento de usuário estiver ativado, os logs registrarão uma mensagem de erro. Além disso, o usuário AEM de origem não é transferido, pois somente um usuário com determinado endereço de email é permitido no sistema de destino.

## Resumo final e relatório {#final-report}

Depois que a extração e a assimilação forem concluídas com êxito, um relatório será gerado mostrando os detalhes da migração principal. Consulte [Como validar a migração principal](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) para obter os detalhes.
