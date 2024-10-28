---
title: Migração de grupo
description: Visão geral da migração de grupo no AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: 7e7b311d425ae6cdee9eb9311c0a12af84f81096
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 4%

---


# Migração de grupo {#group-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_groupmigration"
>title="Migração de grupo"
>abstract="A ferramenta de transferência de conteúdo ajuda a copiar grupos do seu sistema existente do Adobe Experience Manager (AEM) para o AEM as a Cloud Service."

>[!NOTE]
>Para ver as versões anteriores da Ferramenta de Mapeamento de Usuários, consulte a [documentação herdada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introdução {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermigration"
>title="Os usuários não são migrados"
>abstract="A ferramenta de transferência de conteúdo não migra mais os usuários. Os usuários devem ser gerenciados pelo Admin Console."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="Documentação do Admin Console do AEM"
>additional-url="https://adminconsole.adobe.com/" text="Admin Console do AEM"

Como parte da jornada de transição para o Adobe Experience Manager (AEM) as a Cloud Service AEM, os grupos devem ser migrados dos sistemas existentes para o AEM as a Cloud Service. Essa tarefa é realizada pela ferramenta Transferência de conteúdo.

Uma mudança importante do AEM as a Cloud Service é o uso totalmente integrado de IDs de Adobe para acessar o nível do autor. Este processo requer o uso do [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html) para gerenciar usuários e grupos de usuários. As informações do perfil do usuário são centralizadas no Adobe Identity Management System (IMS) que fornece logon único em todos os aplicativos de nuvem do Adobe. Para obter mais detalhes, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). Devido a essa alteração, os usuários são criados automaticamente no AEM quando fazem logon pela primeira vez por meio do IMS.  Assim, a CTT não migra os usuários para o sistema de nuvem.  Os usuários do IMS devem ser colocados em grupos IMS, que podem ser grupos migrados ou novos grupos colocados nos grupos AEM que receberam permissão para acessar o conteúdo AEM que está sendo migrado.  Dessa forma, os usuários no sistema de nuvem terão o mesmo acesso que tinham em seu sistema AEM de origem.

## Detalhes da migração de grupo {#group-migration-detail}

A ferramenta Transferência de conteúdo e o Cloud Acceleration Manager migrarão todos os grupos associados ao conteúdo que está sendo migrado para o sistema de nuvem. A ferramenta Transferência de conteúdo faz isso copiando todos os grupos do sistema AEM de origem durante o processo de extração. A assimilação de CAM seleciona e migra apenas determinados grupos:

* Há vários grupos que estão integrados e já estão presentes no sistema de nuvem de destino; eles nunca são migrados.
* Os grupos de membros diretos de qualquer grupo integrado direta ou indiretamente referenciado em uma política de ACL ou CUG de conteúdo migrado serão migrados, para garantir que os usuários que são membros diretos ou indiretos desses grupos mantenham seu acesso ao conteúdo migrado.
* Se um grupo estiver em uma política de ACL ou CUG do conteúdo migrado, esse grupo será migrado.
* Outros grupos, como aqueles não encontrados em uma política de ACL ou CUG, aqueles que já estão no sistema de destino e aqueles com dados restritos por exclusividade que já estão no sistema de destino, não serão migrados.

Observe que o caminho registrado/relatado para um grupo é somente o primeiro caminho que acionou a migração desse grupo, e esse grupo também pode estar em outros caminhos de conteúdo.

A maioria dos grupos migrados é configurada para ser gerenciada pelo IMS.  Isso significa que um grupo no IMS com o mesmo nome será vinculado ao grupo no AEM, e qualquer usuário do IMS no grupo IMS se tornará usuário do AEM e membros do grupo no AEM.  Isso permite que esses usuários tenham acesso ao conteúdo de acordo com as políticas de ACLs ou CUGs do grupo.

Observe que os grupos migrados não são mais considerados &quot;grupos locais&quot;; são grupos IMS e devem ser recriados no IMS para que possam ser sincronizados entre o AEM e o IMS.  Os grupos podem ser criados no IMS via Admin Console, entre outros métodos, individualmente ou em massa.  Consulte [Gerenciar grupos de usuários](https://helpx.adobe.com/ca/enterprise/using/user-groups.html) para obter detalhes sobre como criar grupos individualmente ou em massa no Admin Console.

A exceção para essa configuração IMS é com grupos criados pelas Coleções Assets. Quando uma coleção é criada no AEM, os grupos são criados para acessar essa coleção; esses grupos são migrados para o sistema de nuvem, mas não são configurados para serem gerenciados pelo IMS.  Para adicionar usuários do IMS a esses grupos, eles devem ser adicionados na página Propriedades do grupo na interface do usuário do Assets, individual ou coletivamente, como parte de outro grupo IMS.


## Recusar Migração de Grupo {#group-migration-option}

A CTT versão 3.0.20 e posterior inclui uma opção para desativar a migração de grupos.  Isso é configurado no console OSGI da seguinte maneira:

* Abra a Configuração OSGI `(http://<server>/system/console/configMgr)`
* Clique na configuração chamada **Configuração do serviço de extração da ferramenta de transferência de conteúdo**
* Desmarque **Incluir grupos na migração** para desabilitar migrações de grupos
* Clique em **Salvar** para garantir que a configuração seja salva e esteja ativa no servidor

Com essa configuração desativada, os grupos não serão migrados e não haverá nenhum relatório de migração principal nem relatório do usuário.

## Relatório do usuário {#user-report}

Durante a migração, os usuários não são migrados, mas os relacionamentos entre grupos de usuários no sistema de origem são perdidos, a menos que sejam capturados de alguma forma.  O Relatório do usuário captura algumas dessas informações no formato de texto em um Relatório do usuário. Nele, cada usuário é relatado (um por linha) juntamente com uma lista de grupos da qual é membro (mas os grupos não migrados não são colocados nessa lista), a menos que a lista de grupos esteja vazia, caso em que o usuário não é exibido. Os grupos relatados junto com cada usuário são aqueles dos quais o usuário é membro direta ou indiretamente no sistema de origem; como os grupos no sistema de origem podem ser aninhados enquanto no sistema de destino não estão, essa lista de grupos oferece suporte à nova estrutura de grupo nivelada no IMS.

No caso de uma limpeza e, em seguida, uma assimilação sem limpeza, os grupos em uma lista do usuário incluirão esses grupos migrados em ambas as fases.

Além dos grupos de cada usuário, há um campo no relatório em que as notas podem ser adicionadas para o usuário (e uma descrição detalhada do significado da nota também está no relatório).  As possíveis observações são:

* Os usuários referenciados diretamente em uma ACL terão *Observação-A* na seção de notas, pois este não é um caso de uso recomendado ou uma prática recomendada.
* Os usuários que são membros diretos de um grupo interno terão a *Nota-B* na seção de notas, pois este também não é um caso de uso recomendado ou uma prática recomendada.

Esses casos podem ocorrer simultaneamente e ao mesmo tempo que os casos anteriores.

O Relatório do usuário é adicionado ao final (e, portanto, faz parte) do Relatório de migração principal (consulte [Resumo final e Relatório](#final-summary-and-report) abaixo).  As informações nesse relatório, incluindo os grupos relatados para cada usuário, podem ser usadas para criar um arquivo de upload de usuário em massa que pode ser usado no Admin Console para criar muitos usuários no IMS em massa.  Os usuários do IMS existentes também podem ser editados em massa.

Consulte [Gerenciar vários usuários | Upload em massa de CSV](https://helpx.adobe.com/ca/enterprise/using/bulk-upload-users.html) para obter detalhes sobre como criar ou editar usuários em massa por meio do Admin Console.

## Considerações adicionais {#additional-considerations}

* Se a configuração **Apagar conteúdo existente na instância da nuvem antes de assimilar** estiver definida, os grupos transferidos anteriormente para a instância do Cloud Service serão excluídos junto com todo o repositório existente; um novo repositório será criado no qual o conteúdo será assimilado. Este processo também redefine todas as configurações, incluindo permissões na instância Cloud Service de destino, e é verdadeiro para qualquer usuário adicionado ao grupo **administradores**. O usuário administrador deve ser adicionado novamente ao grupo **administradores** para recuperar o token de acesso para assimilação de CTT/CAM.
* Quando assimilações que não são de limpeza são executadas (**Limpar conteúdo existente** não está definido), se o conteúdo não for transferido porque não foi alterado desde a transferência anterior, os grupos associados a esse conteúdo também não serão transferidos. Essa regra é verdadeira mesmo se os grupos tiverem sido alterados no sistema de origem. Isso ocorre porque os grupos só são migrados junto com o conteúdo ao qual estão associados. Por causa disso, nesse caso, os grupos que são membros de um grupo no sistema de origem não serão migrados, a menos que façam parte de um grupo diferente que está sendo migrado ou na ACL de conteúdo diferente que está sendo migrado. Para migrar esses grupos posteriormente, considere usar pacotes, excluir grupos do público-alvo e migrar novamente o conteúdo relevante ou migrar novamente usando uma assimilação de limpeza.
* Durante uma assimilação que não é de limpeza, se um grupo existir com qualquer um dos mesmos dados restritos por exclusividade (rep:principalName, rep:authorizableId, jcr:uuid ou rep:externalId) na instância do AEM de origem e na instância do AEM Cloud Service de destino, o grupo em questão será _não_ migrado e o grupo existente no sistema de nuvem permanecerá inalterado. Isso é registrado no Relatório de migração principal.
* Consulte [Migrando Grupos de Usuários Fechados](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) para considerações adicionais sobre grupos usados em uma política de Grupo Fechado de Usuários (CUG).

## Resumo final e relatório

Depois que a extração e a assimilação forem concluídas com êxito, um relatório será gerado mostrando os detalhes da migração do grupo. Consulte [Como validar a migração de grupo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration) para obter detalhes.
