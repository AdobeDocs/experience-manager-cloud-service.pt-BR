---
title: Mapeamento de usuários e migração principal
description: Visão geral do mapeamento de usuários e da migração principal no AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: bf1260f9a49012bbcb4138e0a5498d8dda451b6a
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 4%

---

# Mapeamento de usuários e migração principal {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="Migração de usuários"
>abstract="A ferramenta de Transferência de conteúdo ajuda a mover usuários e grupos de seu sistema existente do Adobe Experience Manager (AEM) para o AEM as a Cloud Service. Os usuários existentes devem ser mapeados para que possam fazer logon por meio de suas IDs de IMS."

>[!NOTE]
>Para versões anteriores da Ferramenta de mapeamento de usuários, consulte a [documentação herdada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introdução {#introduction}

Como parte da jornada de transição para o Adobe Experience Manager (AEM) as a Cloud Service AEM AEM, os usuários e grupos (ou &quot;principais&quot;) devem ser migrados dos sistemas existentes para o as a Cloud Service. Essa tarefa é realizada pela ferramenta Transferência de conteúdo.

Uma mudança importante no AEM as a Cloud Service é o uso totalmente integrado de IDs de Adobe para acessar o nível do autor. Este processo requer a utilização do [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS) que fornece logon único em todos os aplicativos de nuvem do Adobe. Para obter mais detalhes, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). Por causa dessa alteração, os usuários existentes devem ser mapeados para suas IDs do IMS para que possam acessar o AEMaaCS usando seus perfis do IMS. Como os grupos no AEM tradicional são fundamentalmente diferentes dos grupos no IMS, os grupos não são mapeados, mas os dois conjuntos de grupos devem ser reconciliados após a conclusão da migração.

## Detalhes da migração principal {#principal-migration-detail}

A ferramenta Transferência de conteúdo e o Cloud Acceleration Manager migrarão para o sistema de nuvem quaisquer entidades principais associadas ao conteúdo que está sendo migrado. A ferramenta Transferência de conteúdo faz isso copiando todas as entidades principais do sistema AEM de origem durante o processo de extração. A assimilação de CAM seleciona e migra somente as entidades principais associadas ao conteúdo que está sendo assimilado. Se um principal estiver em uma política de ACL ou CUG de conteúdo migrado, esse principal e todos os grupos em que estiver e seus grupos ancestrais (principais) serão migrados. Além disso, se um principal no conteúdo for um grupo, todos os seus grupos descendentes (filhos) e usuários também serão migrados.

## Detalhes de Mapeamento de Usuário {#user-mapping-detail}

Os usuários do AEM podem ser mapeados para usuários correspondentes do Adobe IMS com o mesmo endereço de email. Esse mapeamento pode ser feito automaticamente na CTT (durante a etapa de extração) e se é feito ou não pode ser controlado por um botão antes do início da extração. A configuração padrão do alternador pode ser substituída pelo usuário ao iniciar a extração.

* Se o sistema de origem for uma instância de autor, por padrão, a opção para fazer o mapeamento será _em_, pois esse é o processo recomendado.
* Se o sistema de origem for uma instância de publicação, por padrão, a opção para fazer o mapeamento será _desligado_, pois os usuários normalmente não são migrados ou usados em instâncias de publicação; ou se forem usados, normalmente é usado um sistema de autenticação diferente (ou seja, não IMS) para eles.

Independentemente de os usuários serem ou não mapeados durante a extração, eles, juntamente com os grupos, serão migrados para o sistema de nuvem durante a assimilação se estiverem associados ao conteúdo que está sendo migrado.

## Considerações importantes ao mapear e migrar usuários {#important-considerations}

### Casos excepcionais {#exceptional-cases}

Os seguintes casos específicos são registrados:

1. Se um usuário não tiver um endereço de email no `profile/email` do seu *jcr* , o usuário em questão pode ser migrado, mas não está mapeado. Esse cenário é o caso mesmo se o endereço de email for usado como um nome de usuário para logon.
2. Se o usuário estiver desativado, ele será tratado da mesma forma que outros usuários; será mapeado e migrado normalmente e permanecerá desativado na instância da nuvem.
3. Se um principal existir com qualquer um dos mesmos dados restritos de exclusividade (rep:principalName, rep:authorizableId, jcr:uuid ou rep:externalId) na instância do AEM de origem e na instância do AEM Cloud Service de destino, o principal em questão não é migrado e o principal existente no sistema de nuvem permanece inalterado. Isso é registrado no Relatório de migração principal.
4. Se um usuário não for mapeado para o IMS por meio do mapeamento de usuários, o perfil do usuário no sistema AEM da nuvem não será reconhecido pelo IMS; nesse caso, se ele fizer logon pelo IMS, um novo perfil (duplicado) será criado no AEM, mas não conterá suas informações de perfil anteriores. O perfil de usuário original existirá no sistema AEM da nuvem, mas ele não poderá fazer logon por meio do IMS, somente usando o método AEM tradicional (logon local). Por esse motivo, o mapeamento de todos os usuários é altamente recomendado para todas as migrações de autor.

## Considerações adicionais {#additional-considerations}

* Se a configuração **Apagar conteúdo existente na instância da nuvem antes da assimilação** for definido, as entidades de segurança transferidas anteriormente para a instância do Cloud Service serão excluídas junto com todo o repositório existente; um novo repositório será criado no qual o conteúdo será assimilado. Esse processo também redefine todas as configurações, incluindo permissões na instância do Cloud Service de destino, e é verdadeiro para um usuário administrador adicionado à **administradores** grupo. O usuário administrador deve ser adicionado novamente à **administradores** grupo para recuperar o token de acesso para assimilação de CTT/CAM.
* Quando assimilações que não excluem são executadas (**Apagar conteúdo existente** é desdefinido), se o conteúdo não for transferido porque não foi alterado desde a transferência anterior, os usuários e grupos associados a esse conteúdo também não serão transferidos. Essa regra é verdadeira mesmo se os usuários e grupos tiverem sido alterados no sistema de origem. Isso ocorre porque os usuários e grupos só são migrados junto com o conteúdo ao qual estão associados. Por causa disso, todas as entidades de segurança novas em um grupo no sistema de origem não serão migradas, a menos que façam parte de um grupo diferente que esteja sendo migrado ou na ACL de conteúdo diferente que esteja sendo migrado. Para migrar esses principais posteriormente, considere usar pacotes ou excluir principais do destino e migrar novamente o conteúdo relevante (Extrair com substituição e Assimilar com apagamento).
* Endereços de email duplicados não são permitidos no IMS, mas são permitidos no AEM (tanto no local quanto na nuvem). Um usuário pode fazer logon no AEM por meio do IMS usando seu endereço de email e será conectado ao perfil de usuário referenciado pelo IMS.
* Consulte [Migração de grupos de usuários fechados](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) para considerações extras sobre entidades de segurança usadas em uma política de Grupo fechado de usuários (CUG).

## Resumo final e relatório {#final-report}

Depois que a extração e a assimilação forem concluídas com êxito, um relatório será gerado mostrando os detalhes da migração principal. Consulte [Como validar a migração principal](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) para obter os detalhes.
